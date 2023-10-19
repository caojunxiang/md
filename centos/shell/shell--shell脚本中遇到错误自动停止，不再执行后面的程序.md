##### shell脚本中遇到错误时中断程序运行,不再执行后面的程序

> 当你在脚本中写了一连串的代码时，如果后面的代码需要前面代码执行正确才能继续执行时，你可以使用set-e
>
> vim test.sh新建一个脚本文件

```sh
#!/bin/bash

# 设置程序出错时不再继续执行
set -e

# 先执行一个正确的命令
pwd
# 再执行一个错误的命令
pwd222
# 再执行pwd
pwd

```



```
[caojunxiang@localhost test]$ ./test.sh
/home/caojunxiang/test
./test.sh:行9: pwd222: 未找到命令
```



第二个错误的命令执行后，提示未找到....后面的不再执行







