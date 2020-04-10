# Linux-
程序编译和运行原理的一些笔记

linux下程序寻找动态库路径（按优先级排列）：

1.编译生成时，指定的搜索路径。
　　在makefile中，一般使用”-Wl -rpath”来指明程序运行时到哪个路径去找库。当指定多个动态库搜索路径时，路径之间用冒号隔开，不能有空格。

2.环境变量LD_LIBRARY_PATH中指定的路径。
       可以使用 echo LD_LIBRARY_PATH查看。一般初始时/lib和/user/lib库包含在里面。用户可以往里面添加。

3./etc/ld.so.cache中缓存的路径。
       /etc/ld.so.conf的第一行有一个引用命令：include ld.so.conf.d/*.conf, 所以可以通过修改/etc/ls.so.conf这个配置文件来增删路径,也可以增加一个.conf文件来配置特有的动态库路径。直接将寻库路径加进来即可，保存后需要运行一下ldconfig重载一下。

4.默认的/lib/和/usr/lib。
　　这两个路径是系统最初就添加在LD_LIBRARY_PATH中，所以将库移动到这里亦可以寻找到。
  
补充：程序运行时不会把当前目录作为默认的寻库路径，除非你在编译时指定了
