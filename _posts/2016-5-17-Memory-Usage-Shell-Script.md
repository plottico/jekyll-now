---
layout: post
title: Memory Usage Shell Script
comments: true
snippet: true
---

Plot current load on a unix host. 

<object data="https://plotti.co/plotticoram/300x80.svg" type="image/svg+xml"></object>

Paste this script into console as user root:

```bash
#!/bin/bash
while true; do 
wget -O /dev/null -q "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=`free -m | xargs | awk '{ print $16 / $8 * 100 };'`,\%mem"
sleep 600
done &
```

To automatically run it at startup in ubuntu/debian, paste this into a root shell:

```bash 
sed -i "/exit 0/d" /etc/rc.local # remove exit 0
cat >> /etc/rc.local << 'EOF'
while true; do 
wget -O /dev/null -q "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=`free -m | xargs | awk '{ print $16 / $8 * 100 };'`,\%mem"
sleep 600
done &
exit 0
EOF
```

Tags: bash, shell, linux, processor, system