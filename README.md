# vol
作为自用的vol，有相关的插件已经整合

# volalitity2

- volatility_2.6_win64_standalone.exe -f [内存镜像] imageinfo

用来找内存镜像的系统类型

- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] pslist

用来找正在进行的程序

- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] malfind

用来找比较可疑的代码注入（有害文件）

- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] malfind -p [进程程序] -D ./

-D 是文件导出

- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] handles -p 880 -t File

handles 句柄 类似于内存地址 返回进程文件地址

- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] ldrmodules

用来查询动态链接库

- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] dlllist

用来查询dll的列表

- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] vadinfo
  
- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] shimcache
  

“**shimcache**” plugin. Windows shimcache was created by Microsoft to identify compatibility issues with executed programs.

从内存文件中找到异常程序植入到系统的开机自启痕迹

分析应用程序兼容性缓冲区缓存注册表项

Shimcache plugin parses the application compatibility shim cache registry key.

- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] mftparser

“**mftparser**” plugin in this to scan for 
& parses potential MFT entries. This plugin extract MFT entries from
 memory. We save the output in a text file so that we easily search.

`NTFS`使用`MFT`条目定义它们对应的文件，有关文件的所有信息，比如大小、时间、权限等都存在`MFT`条目中，或者由`MFT`条目描述存储在`MFT`外部的空间中。

- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] printkey -K "SAM\Domains\Account\Users\Nmaes"
  
  volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] hivelist
  

volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] hashdump -y [起始偏移量] [终止偏移量]

用户密码等注册内容在SAM数据库中，可以把SAM数据库dump下来然后分析
The password from the current user is stored in “*SAM*” hive, and configuration and other system information in the “*SYSTEM*” hive.
然后用hash解密可以获得密码

- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] shutdowntime

查找最后一次关机时间

- 加入自己创建的profile，可以把文件放到相应的文件夹下面

把压缩包放至volatility/volatility/plugins/overlays/linux下，压缩包里面包含一下两个文档。

- 如果要提取的话，使用dumpfiles提取文件volatility -f [内存镜像] --profile=[系统类型] dumpfiles -Q [内存地址] --dump-dir=./
  -Q的参数为 内存地址
  --dump-dir的参数为导出文件的目录
  
- volatility_2.6_win64_standalone.exe -f [内存镜像] --profile=[系统类型] netscan
  

查看网络连接情况

# volalitity3

python vol.py -f [内存镜像] windows.info

用来找内存镜像的系统类型

python vol.py -f [内存镜像] windows.cmdline

查看进程命令行参数，例如：查看软件进行过什么操作等

python vol.py -f [内存镜像] windows.registry.userassist

to see what programs were recently executed on a system.

python vol.py -f [内存镜像] windows.pstree

查看进程树，显示子进程和父进程的关系

python vol.py -f [内存镜像] windows.pslist

查看进程列表，显示当前的进程状态

python vol.py -f [内存镜像] windows.netscan

查看网络的使用情况

# 计算解码

certutil -hashfile 文件名 [解码方式]

# 文件导出

在命令后面加上 `> [文件名.类型]`

# 常见问题

svchost.exe一般是服务services.exe的子进程，并且注入的话svchost也是常见的注入文件

# powershell设置

notepad.exe $Profile

PAGE_READONLY

PAGE_NOACCESS

# linux相关文件

Authentication logs are under `/var/log/auth.log`

`/etc/issue.net` is one of the files that holds the system type info.

# volalitity2网络指令

# 内存取证神器Volatility常用指令大全

## 具体指令开头部分根据Volatility版本做修改即可

查找文件  
volatility -f 19.mem --profile=Win7SP1x86_23418 filescan | grep “Information.xlsx”

列举注册表  
volatility -f neicun.mem --profile=Win7SP1x64 hivelist

查询cmd指令  
volatility -f neicun.mem --profile=Win7SP1x64 cmdline | grep “jdk1.8.0”

查看网络通讯  
volatility -f neicun.mem --profile=Win7SP1x64 netscan

查看系统用户名  
volatility -f neicun.mem --profile=Win7SP1x64 printkey -K “SAM\Domains\Account\Users\Names”

查看用户密码的哈希  
volatility -f neicun.mem --profile=Win7SP1x64 hashdump -y 0xfffff8a000024010 -s 0xfffff8a000300010

查看导出文件  
volatility -f neicun.mem --profile=Win7SP1x64 dumpfiles -Q 0x000000007e4e5070 -D /root/

查看进程(pslist)  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 pslist > win7_sp1_x86_pslist.txt

进程树形查看方式  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 pstree

查看隐藏进程  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 psxview

查看网络通讯连接(netscan）–类似Windows命令 netstat -an  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 netscan > win7_sp1_x86_NetScan.txt

查看Windows帐户密码Hash(haspdump)  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 hashdump > win7_sp1_x86_hashdump.txt

查看UserAssist应用程序运行记录  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 userassist > win7_sp1_x86_UserAssist.txt

查看进程对应的SID（含用户名）  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 getsids > win7_sp1_x86_GetSID.txt

查看Windows系统挂载的注册表配置单元列表  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 hivelist

导出内存中的注册表配置单元数据（可在取证软件中再次分析）  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 dumpregistry --dump-dir=K:\volatility

查看内存中IE访问历史记录  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 iehistory > win7_sp1_x86_IE_History.txt

查看应用程序运行记录(ShimCache)  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 shimcache > win7_sp1_x86_shimecache.txt

查看系统服务列表及状态  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 svcscan > win7_sp1_x86_ServiceList.txt

导出事件时间线信息（用于基于时间顺序的事件分析）  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 timeliner > win7_sp1_x86_TimeLineEvent.txt

查看VAD信息  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 vadinfo > win7_sp1_x86_VAD_info.txt

查看yara信息  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 yarascan > win7_sp1_x86_yarascan.txt

查看剪贴板(Clipboard)信息  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 clipboard > win7_sp1_x86_Clipboard.txt

查看进程加载的DLL动态链接库  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 dlllist > win7_sp1_x86_DllList.txt

查看GDT信息  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 gdt> win7_sp1_x86_GDT.txt

查看Sockets连接  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 sockets > win7_sp1_x86_Sockets.txt (Win7SP1x86不支持）

volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 sockscan > win7_sp1_x86_SockScan.txt (Win7SP1x86不支持）

查看SSDT表  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 ssdt > win7_sp1_x86_SSDT.txt

volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 eventhooks

查看内存中MFT记录信息  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 mftparser > win7_sp1_x86_MFT_Records.txt

volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 mftparser --output-file=mftverbose.txt -D mftoutput

查看磁盘MBR扇区信息  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 mbrparser > win7_sp1_x86_MBR_Sector.txt

volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 servicediff > win7_sp1_x86_ServiceDiff.txt

volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 hibinfo (Win7SP1x86不支持）

查看打开的文件夹列表  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 shellbags > win7_sp1_x86_shellbags.txt

查看系统最后一次关机时间  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 shutdowntime

获取域缓存密码hash  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 cachedump

获取RSA私钥和SSL公钥  
volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 dumpcerts --dump-dir=K:\volatility

volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 volshell

volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 truecryptmaster

volatility_2.6_win64_standalone -f win7.vmem --profile=Win7SP1x86 truecryptpassphrase

查看环境变量envars

volatility -f 1.vmem --profile=Win7SP1x64 envars

****envars：查看环境变量****

查看运行程序相关的记录，比如最后一次更新时间，运行过的次数等。****serassist****

volatility -f 1.vmem --profile=Win7SP1x64 userassist

volatility -f 1.vmem --profile=Win7SP1x64 ****memdump -p xxx --dump-dir=./****

****memdump：提取出指定进程，常用foremost 来分离里面的文件****

##### Editbox 插件可以用来查看删除的文本信息

`ShellBags`是一组用来记录文件夹（包括挂载网络驱动器文件夹和挂载设备的文件夹）的名称、大小、图标、视图、位置的注册表项，或称为`BagMRU`。每次对文件夹的操作，`ShellBags`的信息都会更新，而且包含时间戳信息。是`Windows`系统改善用户体验的功能之一。即使删除文件夹后，`ShellBags`仍然会保留文件夹的信息。因此可以用来揭示用户的活动。
