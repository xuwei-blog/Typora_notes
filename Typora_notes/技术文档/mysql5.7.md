# mysql5.7编译SOP

[TOC]

| 资料                 | 备注         |
| -------------------- | ------------ |
| mysql-server-5.7.zip | mysql5.7源码 |
| mysql5.7_autoRun.sh  |              |

> 系统代理
>
> ```bash
> # 已验证可行方法
> export http_proxy=http://192.168.56.133:7890
> export https_proxy=http://192.168.56.133:7890
> 
> # 下面方法应该不行吧 没研究
> cat > "/etc/environment" << 'EOF'
> http_proxy=http://192.168.56.133:7890
> https_proxy=http://192.168.56.133:7890
> ftp_proxy=http://192.168.56.133:7890
> no_proxy=localhost,127.0.0.1
> EOF
> 
> sourece /etc/environment
> ```
>
> 换源
>
> ```bash
> # https://mirrors.tuna.tsinghua.edu.cn/help/debian/
> 
> cat > "/etc/apt/sources.list" << 'EOF'
> # 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
> deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free
> # deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free
> 
> deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free
> # deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free
> 
> deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free
> # deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free
> 
> # 以下安全更新软件源包含了官方源与镜像站配置，如有需要可自行修改注释切换
> deb https://security.debian.org/debian-security bullseye-security main contrib non-free
> # deb-src https://security.debian.org/debian-security bullseye-security main contrib non-free
> EOF
> ```



## 1. 将源码拷贝到设备上

```bash
# git clone 或者 download 
https://codeload.github.com/mysql/mysql-server/zip/refs/heads/5.7
```



## 2. 安装依赖

```bash
apt update
sudo apt-get install build-essential cmake libncurses5-dev libssl-dev bison
sudo apt-get install libaio1 libaio-dev
sudo apt-get install zlib1g zlib1g-dev

sudo apt install build-essential cmake libncurses5-dev libssl-dev bison libaio1 libaio-dev zlib1g zlib1g-dev
```



## 3. 进入源码目录编译mysql

```bash
mkdir build && cd build
```

```bash
cmake .. \
  -DCMAKE_INSTALL_PREFIX=/usr/local/mysql \
  -DMYSQL_DATADIR=/usr/local/mysql/data \
  -DSYSCONFDIR=/etc \
  -DWITH_INNOBASE_STORAGE_ENGINE=1 \
  -DWITH_PARTITION_STORAGE_ENGINE=1 \
  -DWITH_FEDERATED_STORAGE_ENGINE=1 \
  -DWITH_BLACKHOLE_STORAGE_ENGINE=1 \
  -DWITH_MYISAM_STORAGE_ENGINE=1 \
  -DENABLED_LOCAL_INFILE=1 \
  -DWITH_READLINE=1 \
  -DWITH_SSL=system \
  -DWITH_ZLIB=system \
  -DDEFAULT_CHARSET=utf8mb4 \
  -DDEFAULT_COLLATION=utf8mb4_unicode_ci \
  -DDOWNLOAD_BOOST=1 \
  -DWITH_BOOST=/root/mysql-server-5.7/boost_download
```





## 4. 构建

```bash
make -j2
# 等待
make install
```





## 5. 初始化mysql用户和组

```bash
groupadd mysql
useradd -r -g mysql -s /bin/false mysql
mkdir -p /usr/local/mysql/data
chown -R mysql:mysql /usr/local/mysql

```



## 6. 初始化mysql

> 没有密码

```bash
/usr/local/mysql/bin/mysqld \
  --initialize-insecure \
  --user=mysql \
  --basedir=/usr/local/mysql \
  --datadir=/usr/local/mysql/data
```

> 有密码

```bash
/usr/local/mysql/bin/mysqld \
  --initialize \
  --user=mysql \
  --basedir=/usr/local/mysql \
  --datadir=/usr/local/mysql/data
```

> 查看密码
>
> ```bash
> cat /usr/local/mysql/data/*.err | grep "temporary password"
> ```

## 7. mysql默认配置my.cnf

> sudo vi /etc/my.cnf

```bash
# MySQL 配置文件示例
# 适用于从源码安装的 MySQL 5.7

[client]
port        = 3306
socket      = /tmp/mysql.sock
default-character-set = utf8mb4

[mysqld]
# 基本路径设置
basedir     = /usr/local/mysql
datadir     = /usr/local/mysql/data
socket      = /tmp/mysql.sock
pid-file    = /usr/local/mysql/data/mysql.pid

# 端口和绑定地址
port        = 3306
bind-address = 0.0.0.0

# 字符集设置
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
skip-character-set-client-handshake

# 默认存储引擎
default-storage-engine = INNODB

# 日志相关
log-error   = /usr/local/mysql/data/mysql.err
general_log = 0
general_log_file = /usr/local/mysql/data/mysql.log
slow_query_log = 1
slow_query_log_file = /usr/local/mysql/data/mysql-slow.log
long_query_time = 2

# 最大连接数
max_connections = 150

# 表缓存设置
table_open_cache = 2000
table_definition_cache = 1000

# 缓冲池设置（根据内存调整）
innodb_buffer_pool_size = 128M
innodb_log_file_size = 48M

# 其他常用设置
innodb_file_per_table = 1
innodb_flush_log_at_trx_commit = 1
sync_binlog = 1
innodb_lock_wait_timeout = 50

# 跳过 DNS 反向解析（加快连接速度）
skip-name-resolve

# 不区分大小写（Linux 上默认是 0；设为 1 表示表名不区分大小写）
lower_case_table_names = 1

# 设置默认 SQL 模式
sql_mode = STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION

[mysqldump]
quick
max_allowed_packet = 16M

[mysql]
no-auto-rehash
default-character-set = utf8mb4

[isamchk]
key_buffer_size = 20M
sort_buffer_size = 256K
read_buffer = 256K
write_buffer = 256K
```



## 8. mysql服务mysql.service

> sudo vi /etc/systemd/system/mysql.service

```bash
[Unit]
Description=MySQL Community Server
After=network.target

[Service]
User=mysql
Group=mysql
ExecStart=/usr/local/mysql/bin/mysqld_safe --defaults-file=/etc/my.cnf
Restart=on-failure
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
```



## 9. mysql环境变量

```bash
echo 'export PATH=/usr/local/mysql/bin:$PATH' >> /etc/profile
source /etc/profile
```



## 10. 测试mysql

```bash
reboot
# 开机后
systemctl status mysql
mysql -u root
```



