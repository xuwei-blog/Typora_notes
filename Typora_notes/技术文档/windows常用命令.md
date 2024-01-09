# windows常用命令

[TOC]



## 查看BIOS版本

> 暂时没发现鸟用

```shell
systeminfo | findstr /I /c:bios
wmic bios get manufacturer, smbiosbiosversion
```

