```
uninx-socket
tcp-socket

Nginx与php-fpm通信分析

Nginx与php-fpm通信有两种方式，一种是通过tcp socket和 unix socket。前者是通过ip:端口方式进行通信，后者是通过php启动生成的socket文件进行通信。因此tcp socket的方式可以将两者分布再不同的机器上，只要Nginx能够连接到php服务器的端口即可。后者的方式，是统一主机上进行通讯的方式，因此两者只能再同一台机器上面。
```