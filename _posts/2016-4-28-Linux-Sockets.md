---
layout: post
title: Linux total open sockets 
---

Plot amount of total open sockets on a linux box. Can be useful in case you may hit the default 1024 connections limit. 

Paste this script into console as user root:

```bash
#!/bin/bash
while true; do
wget -O /dev/null -q http://plotti.co/lock/plotticonn?d=`netstat -tn | wc -l`sockets
sleep 1
done &
```


To automatically run it at startup in ubuntu/debian, paste this into a root shell:

```bash 
sed '0,/exit 0/{s/exit 0//}' /etc/rc.local # remove exit 0
cat >> /etc/rc.local << EOF
while true; do
wget -O /dev/null -q http://plotti.co/lock/plotticonn?d=`netstat -tn | wc -l`sockets
sleep 1
done & # fork to background
exit 0
EOF
```

Tags: bash, shell