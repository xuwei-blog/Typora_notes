# systemd学习

[TOC]

# 〇、 概要

```
/etc/systemd/system/ # 自定义
/lib/systemd/system/ # 标准
/usr/lib/systemd/system/ # 包管理器创建的
```





# 一、 Networkmanager网络切换

你提供的 `journalctl` 日志片段展示了 **NetworkManager** 在 **切换网络连接配置（从 NetworkTest3 到 NetworkTest）** 的全过程。我们来逐句分析日志内容，帮助你理解 **NetworkManager 是如何处理网络接口的切换和自动激活的**。

---

## 🧩 背景说明

你使用了 `nmtui` 修改了一个名为 `NetworkTest3` 的连接配置（可能是将其 IP 从固定 IP 改为 DHCP 或者其他更改），并保存后选择“自动应用”。这时：

- NetworkManager 发现配置变更。
- 因为这个连接正在使用中（处于 activated 状态），所以需要重新激活才能生效。
- 但当前用户没有足够的权限执行更新（第一次失败）。
- 后续以 root 权限再次尝试更新成功。
- 然后 NetworkManager 主动 **断开当前连接（NetworkTest3）**，并 **自动激活另一个连接（NetworkTest）**。

---

## 🔍 分析日志流程

### 1. **修改 NetworkTest3 失败**
```
7月 14 10:26:33 station1 NetworkManager[701]: <info> [1752459993.8143] audit: op="connection-update" uuid="f6ac9c46-7e15-49bf-8461-450dddafe5a1" name="NetworkTest3" pid=80812 uid=1000 result="fail" reason="Insufficient privileges"
```

- 用户 UID 1000（普通用户）尝试更新连接 `NetworkTest3`。
- 操作失败，原因是权限不足（缺少 root 权限）。

---

### 2. **修改 NetworkTest3 成功**
```
7月 14 10:27:04 station1 NetworkManager[701]: <info> [1752460024.8731] audit: op="connection-update" uuid="f6ac9c46-7e15-49bf-8461-450dddafe5a1" name="NetworkTest3" args="connection.timestamp,ipv4.addresses" pid=82951 uid=0 result="success"
```

- PID 82951（可能是通过 `sudo` 执行的 nmtui）以 UID 0（root）身份再次更新连接。
- 更新了 `connection.timestamp` 和 `ipv4.addresses` 字段，表示 IP 地址配置发生了变化。

---

### 3. **NetworkManager 开始停用旧连接（NetworkTest3）**
```
7月 14 10:27:24 station1 NetworkManager[701]: <info> [1752460044.3410] device (enp1s0): state change: activated -> deactivating (reason 'user-requested', sys-iface-state: 'managed')
```

- 网络设备 `enp1s0` 正在从“已激活”状态变为“去激活”状态。
- 原因是“用户请求”，说明是由用户操作触发的（即 nmtui 应用了新配置）。

---

### 4. **记录 Deactivation 审计日志**
```
7月 14 10:27:24 station1 NetworkManager[701]: <info> [1752460044.3447] audit: op="connection-deactivate" uuid="f6ac9c46-7e15-49bf-8461-450dddafe5a1" name="NetworkTest3" pid=82951 uid=0 result="success"
```

- 成功将 `NetworkTest3` 连接去激活（disconnect）。

---

### 5. **NetworkManager 自动激活新连接（NetworkTest）**
```
7月 14 10:27:24 station1 NetworkManager[701]: <info> [1752460044.3901] policy: auto-activating connection 'NetworkTest' (49183910-6b96-4879-ab50-0984844529e7)
```

- NetworkManager 决定自动激活一个名为 `NetworkTest` 的连接。
- 这是因为 NetworkManager 的策略引擎（policy）检测到当前没有可用连接，并且该连接被标记为可自动激活。

---

### 6. **开始激活 NetworkTest 连接**
```
7月 14 10:27:24 station1 NetworkManager[701]: <info> [1752460044.3908] device (enp1s0): Activation: starting connection 'NetworkTest' (49183910-6b96-4879-ab50-0984844529e7)
```

- 开始通过 `enp1s0` 接口激活 `NetworkTest` 连接。

---

### 7. **连接状态逐步推进**
以下是一系列的状态转换：
```
disconnected -> prepare
prepare -> config
config -> ip-config
ip-config -> ip-check
ip-check -> secondaries
secondaries -> activated
```

这表示：
- 设备开始准备连接；
- 配置网络接口；
- 获取/设置 IP 地址；
- 进行 IP 地址检查（如冲突检测）；
- 加载辅助地址（如 IPv6）；
- 最终连接成功激活。

---

### 8. **最终连接成功**
```
7月 14 10:27:24 station1 NetworkManager[701]: <info> [1752460044.4012] device (enp1s0): Activation: successful, device activated.
7月 14 10:27:24 station1 NetworkManager[701]: <info> [1752460044.4019] manager: NetworkManager state is now CONNECTED_GLOBAL
```

- `enp1s0` 成功连接到了网络。
- NetworkManager 的全局状态变为 `CONNECTED_GLOBAL`，表示网络完全可用。

---

## ✅ 总结：切换网络接口的完整流程

| 阶段         | 描述                                                        |
| ------------ | ----------------------------------------------------------- |
| 1️⃣ 配置更新   | 使用 `nmtui` 修改连接配置（NetworkTest3）                   |
| 2️⃣ 权限验证   | 第一次更新失败（权限不足），第二次以 root 成功更新          |
| 3️⃣ 停用旧连接 | NetworkManager 停用当前连接（NetworkTest3）                 |
| 4️⃣ 自动激活   | 根据策略自动选择下一个可用连接（NetworkTest）               |
| 5️⃣ 状态迁移   | 设备依次经历 prepare → config → ip-config → ... → activated |
| 6️⃣ 成功连接   | 新连接激活成功，网络恢复正常                                |

---

## 📌 小提示

- 如果你想查看某个连接的详细日志，可以这样过滤：
  ```bash
  journalctl -u NetworkManager --since "1 hour ago" | grep "NetworkTest3\|NetworkTest"
  ```
- 可以使用 `nmcli connection show` 查看所有连接及其 UUID。
- NetworkManager 的自动激活逻辑基于连接优先级、是否设为自动连接等属性。

---

如果你还想进一步了解 NetworkManager 的行为机制（比如自动激活策略、连接优先级等），我也可以为你深入讲解 😊



# ∞ 系统问题整理

## 为啥这个文件删不掉？

![image-20250714171914410](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202507141719704.png)



## systemctl免认证

![image-20250714173730674](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202507141737755.png)

```
sudo nano /etc/polkit-1/localauthority/50-local.d/hello-world-nopasswd.pkla

# 配置内容
[Allow all users to manage systemd units]
Identity=unix-user:*
Action=org.freedesktop.systemd1.manage-units
ResultAny=yes
ResultInactive=yes
ResultActive=yes

sudo systemctl daemon-reload
sudo pkill -HUP polkitd

```



## 