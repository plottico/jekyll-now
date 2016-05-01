---
layout: post
title: Linux established connections
comments: true
snippet: true
---

Plot amount of established connections on a linux box. 

<object data="https://plotti.co/plotticonn/300x80.svg" type="image/svg+xml"></object>

Paste this script into console as user root:

```bash
#!/bin/bash
while true; do
wget -O /dev/null -q "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=`netstat -tn | grep ESTAB | wc -l`established_connections"
sleep 1
done &
```

To automatically run it at startup in ubuntu/debian, paste this into a root shell:

```bash 
sed -i "/exit 0/d" /etc/rc.local # remove exit 0
cat >> /etc/rc.local << 'EOF'
while true; do
wget -O /dev/null -q "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=`netstat -tn | grep ESTAB | wc -l`established_connections"
sleep 1
done & # fork to background
exit 0
EOF
```

Tags: bash, shell, linux