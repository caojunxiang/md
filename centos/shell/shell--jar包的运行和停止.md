##### 当你有一个jar包，该怎么在linux上运行它呢？

> 刚打包好一个项目，怎么在linux上运行呢？

```sh
nohup /usr/bin/java -jar /home/caojunxiang/my_app/app.jar > /home/caojunxiang/my_app/app.log 2>&1 &
```

> 命令详解：

+ nohup: 不挂断的执行命令，保证程序在后台运行
+ /usr/bin/java： 你的java的路径 
+ -jar：这个不用我说了吧？
+ /home/caojunxiang/my_app/app.jar: jar包路径，
+ 〉 ： 将日志覆盖写入到某文件
+ /home/caojunxiang/my_app/app.log: jar运行日志文件
+ 2>&1：将错误信息输入到正常信息中
+ & ： 固定写法一定要在结尾带上：













