## 对比原EFI的修改
 - AppleXcpmCfgLock 设置为 false
 - Tools 增加 CFGLock.efi，UEFIModify.efi
# 安装
## 使用HDMI或者DP线连接显示器，不然出现苹果logo后就黑屏了。
  个人只测试了HDMI线
## BIOS
 - General → Advanced Boot Options：全部取消勾选
 - System Configuration → SATA Operation：勾选AHCI
 - Secure Boot → Secure Boot Enable：取消勾选
 - Intel® Software Guard Extensions™ → Intel® SGX™ Enable：选择Disabled
 - Power Management → Block Sleep：一般不勾选，否则不能进入深度睡眠，深度睡眠影响可切换
 - Virtualization Support → VT for Direct I/O：取消勾选
## 引导
 - OC引导进入cfgLock 值为 0 则无需修改，若为 1，输入 y 修改为 0
 - OC引导进入UEFImodify 执行如下命令设置 DVMT 预分配 (64 MB)
```
setup_var 0x8DC 0x2
```
## 安装后
  进入系统发现 SMC 的其他驱动没有正常加载（可能是用工具调整config.plist时导致格式错误），于是重新将SMCDellSensors.kext等驱动修改为Enable，重启后可以正常检测CPU温度和风扇转速
