```
直接kill -9掉master进程，nginx的work进程并没有停止，如果这个时候我们启动nginx是会提示Address already in use错误。这个时候需要在此关闭work进程，才可以启动成功。
kill -15关闭master进程后，work进程也被关闭了。相当于使用了nignx的stop命令。
```