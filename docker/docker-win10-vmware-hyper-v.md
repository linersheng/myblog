# win10 安装docker后，VMware运行提示 hyper-v不兼容

## 添加新的启动选，系统启动关闭hyper-v 
```
管理员身份运行命令提示符 cmd
bcdedit /copy {current} /d “Windows10 no Hyper-V
bcdedit /set {XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX} hypervisorlaunchtype OFF
将上面的代码替换掉XXX代码即可

重启 Windows10 就能选择是否启用 Hyper-v，在“no Hyper-V”中，可以运行 Vmware 虚拟机，而另一个启动选项运行 Hyper-v
````

## 修改原有的系统启动选择
```
管理员身份运行命令提示符 cmd
bcdedit /set {current} hypervisorlaunchtype OFF
````