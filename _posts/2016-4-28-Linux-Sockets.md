---
layout: post
title: Linux total open sockets 
comments: true
snippet: true
---

Plot amount of total open sockets on a linux box. Can be useful in case you may hit the default 1024 connections limit. 

You may also want to plot [amount of established connections]({% post_url 2016-4-29-Established-Connections %}) only.

Paste this script into console as user root:

```bash
#!/bin/bash
while true; do
wget -O /dev/null -q "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=`netstat -tn | wc -l`sockets"
sleep 1
done &
```

To automatically run it at startup in ubuntu/debian, paste this into a root shell:

```bash 
sed -i "/exit 0/d" /etc/rc.local # remove exit 0
cat >> /etc/rc.local << 'EOF'
while true; do
wget -O /dev/null -q "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=`netstat -tn | wc -l`sockets"
sleep 1
done & # fork to background
exit 0
EOF
```

Tags: bash, shell, linux