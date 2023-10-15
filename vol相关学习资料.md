   

     在学习vol的过程中，发现国内相关资源还是很有限的，并且没有一个综合的使用教程，一般都是指令不全或者没有其他的使用介绍（如添加插件，手动制作profile等），所以我在学习的过程中把用到的资源整理了一下，方便大家学习，如果有问题，欢迎各位师傅一起讨论。

对于使用volalitity的建议和常见问题：

    建议1.在进行内存取证的时候将vol2和vol3进行结合使用，vol2能弥补3插件不足，3能弥补2的速度慢，但在做题的过程中，一般都是以vol2为主

    建议2.在搭建环境的时候，最好将linux和windows的环境都配置好，如果能有一台linux机器配置的话更好，但是更建议使用wsl来实现双系统的vol使用，尤其将Linux的一些管道指令用在输出结果中，有奇效

常见问题1.在配置linux的python2的时候可以看这个：[kali linux 中python2不带pip的解决方法_python2没有pip_程序员届的小白菜的博客-CSDN博客](https://blog.csdn.net/weixin_42478365/article/details/116801930)

常见问题2.没有Python.h库，要安装相应的python环境，可以看这个：[解决fatal error: Python.h: No such file or directory报错_呆萌的代Ma的博客-CSDN博客](https://blog.csdn.net/weixin_35757704/article/details/124852304)

常见问题3.没有Crypto.Hash库文件，在python中，Crypto库是pycrypto，使用方法可以看：[今日排错---开发者平台加签pthon报错修复 - 骁珺在努力 - 博客园](https://www.cnblogs.com/i-xiaojun/p/15031410.html)

**vol官方的插件**

[GitHub - volatilityfoundation/volatility: An advanced memory forensics framework](https://github.com/volatilityfoundation/volatility)

**vol的下载地址**

[Release Downloads | Volatility Foundation](https://www.volatilityfoundation.org/releases)

**vol2和vol3各种指令对比**

https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/memory-dump-analysis/volatility-cheatsheet

**vol2的常用指令**

[内存取证-volatility工具的使用 （史上更全教程，更全命令）_路baby的博客-CSDN博客](https://blog.csdn.net/m0_68012373/article/details/127419463)

**vol2的各种外置插件**

[volatility2各类外部插件使用简介_volatility插件_Blus.King的博客-CSDN博客](https://blog.csdn.net/q851579181q/article/details/110956485)

**手动添加profile**

[Linux内存取证制作Volatility的专属profile - 简书](https://www.jianshu.com/p/1f134bf4c20c)

![](C:\Users\21Q017\AppData\Roaming\marktext\images\2023-05-16-06-00-21-image.png)

**vol的题目，基本都做一遍就能把vol掌握差不多**

https://cyberdefenders.org/blueteam-ctf-challenges/41#nav-questions

![](C:\Users\21Q017\AppData\Roaming\marktext\images\2023-05-16-07-37-14-image.png)

点击vol标签，能找到相关的题目
