---
layout: single
title: "Nginx & PHP-FPM boost up"
date: 2018-04-22 21:06
tags: Software Server
---

> 这里很久以前做的一个调试Nginx PHP-FPM性能的一个笔记。

### Nginx

#### apr_socket_recv: Connection reset by peer (104)

```
vi /etc/sysctl.conf
```

net.ipv4.tcp_syncookies 是为了防止洪水攻击, 需要在做压力测试的时候关掉

```
net.ipv4.tcp_syncookies = 0
```

重启设置生效

```
sysctl -p
```

其他参数:

```
net.ipv4.tcp_max_syn_backlog
参数决定了SYN_RECV状态队列的数量，一般默认值为512或者1024，即超过这个数量，系统将不再接受新的TCP连接请求，一定程度上可以防止系统资源耗尽。可根据情况增加该值以接受更多的连接请求。
```

```
net.ipv4.tcp_tw_recycle
参数决定是否加速TIME_WAIT的sockets的回收，默认为0。
```

```
net.ipv4.tcp_tw_reuse
参数决定是否可将TIME_WAIT状态的sockets用于新的TCP连接，默认为0。
```

```
net.ipv4.tcp_max_tw_buckets
参数决定TIME_WAIT状态的sockets总数量，可根据连接数和系统资源需要进行设置。 
```

### PHP-FPM

```
listen.backlog = 1024
pm.max_children = 225
pm = static
pm.max_requests = 10240
```

### ab command
shell script

```
ab -H "Content-Type: application/json" -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hcGkuaGFpd2FpLmNuIiwiYXVkIjoidy5oYWl3YWkuY24iLCJpYXQiOjE0NzQ4NTc0NTQsIm5iZiI6MTQ3NDg1NzQ1NCwiZXhwIjoxNDc1MDMwMjU0LCJ1aWQiOjF9.fbv1W69t1A2zPIMnSRuegEGRWDVYQ_aPi02zbLhfgyc" -H "Cache-Control: no-cache" -c 1000 -n 3000 -r "http://hostname/v1/categories/248/threads?page=1&expand=repliesTen"
```