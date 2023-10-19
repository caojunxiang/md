###### 同样的命令在终端执行OK，但是在shell脚本执行失败的原因

你刚用yum或者apt命令安装了一个程序, 在终端执行完全OK，但是当你把他放在shell脚本中时候，执行这个shell脚本却报错了，提示找不到这个命令,hahaha，对于新手来说真的会谢！

造成这个问题的原因是：环境变量

你可以在终端中输入 echo $PATH 命令来查看环境变量

```shell
[caojunxiang@localhost log]$ echo $PATH
/usr/lib64/qt-3.3/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.362.b08-1.el7_9.x86_64/bin:/home/caojunxiang/.local/bin:/home/caojunxiang/bin

```

此环境变量和shell脚本中的变量不同，



在shell脚本首行写入 echo $PATH 用来打印shell环境变量

```SHELL
#!/bin/bash
echo $PATH
```

执行这个脚本

```sh
[caojunxiang@localhost test]$ ./c.sh
/usr/local/bin:/usr/bin
```

看到没，这里打印的环境变量不同，

如果遇到这种情况有两种解决办法，

1、用绝对路径执行命令

```sh

#!/bin/bash

# 原写法
jar -jar app.jar

# 绝对路径写法-
# 请把/usr/bin/java替换成你的绝对路径,命令后面的参数也改成自己的
/usr/bin/java -jar app.jar

```



2、手动修改环境变量，把运行命令所需要的环境变量添加上去

```sh

#!/bin/bash

# 使用export 修改环境变量
# export PATH 固定写法-重新设置环境变量 
# $PATH原shell环境变量
# :/usr/bin 在原环境变量之后添加的变量，可以添加很多条，每条前面加:
export PATH=$PATH:/usr/bin

jar -jar app.jar

```



