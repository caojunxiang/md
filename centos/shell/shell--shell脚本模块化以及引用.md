##### shell脚本模块化

> 模块化的优点：
>
> + 功能清晰
> + 易于维护
> + 便于阅读
> + 代码复用

源代码：只有单一的一个run.sh文件 

```sh
#!/bin/bash
# 功能：更新小程序并重新启动

# 设置程序出错时不再继续执行
set -e

# 查找app的进程号并杀死该进程
echo "正在停止--小程序"
process_name=app.jar
pid=$(ps -ef | grep $process_name | grep -v "grep" | awk '{print $2}')
if [ -n "$pid" ]; then
    kill -9 $pid
    echo "已杀死进程：$pid"
else
    echo "未找到进程：$process_name"
fi
echo "已停止"

# 替换jar包
echo "开始更新jar包......"
cp /home/caojunxiang/my_app/management-0.0.1-SNAPSHOT.jar /home/caojunxiang/my_app/app.jar
echo "jar包更新完成"

# 启动jar包
echo "正在启动--小程序"
nohup /usr/bin/java -jar /home/caojunxiang/my_app/app.jar >/home/caojunxiang/my_app/app.log 2>&1 &
echo "启动成功"
```

将上述的文件拆分成三个sh

> vim stop.sh

```sh
#!/bin/bash
# 查找app的进程号并杀死该进程
echo "正在停止--小程序"
process_name=app.jar
pid=$(ps -ef | grep $process_name | grep -v "grep" | awk '{print $2}')
if [ -n "$pid" ]; then
    kill -9 $pid
    echo "已杀死进程：$pid"
else
    echo "未找到进程：$process_name"
fi
echo "已停止"
```

> vim updata_jar.sh

```sh
#!/bin/bash
# 替换jar包
echo "开始更新jar包......"
cp /home/caojunxiang/my_app/management-0.0.1-SNAPSHOT.jar /home/caojunxiang/my_app/app.jar
echo "jar包更新完成"
```

> vim start.sh

```sh
# 启动jar包
echo "正在启动--小程序"
nohup /usr/bin/java -jar /home/caojunxiang/my_app/app.jar >/home/caojunxiang/my_app/app.log 2>&1 &
echo "启动成功"
```

将原来的run.sh做出修改

```sh
#!/bin/bash
# 功能：更新小程序并重新启动

source ./stop.sh
source ./update_jar.sh
source ./start.sh
```

> source 命令： 使用资源，它后面跟的路径里面的命令会被自行 







