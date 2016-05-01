---
layout: post
title: Plot CPU load on linux machine
comments: true
snippet: true
---

Plot current CPU usage percentage on a linux box. 

<object data="https://plotti.co/plottycocpu/300x80.svg" type="image/svg+xml"></object>

You will need to make sure you have `mpstat` utility installed. It usually comes with `sysstat` package.
Paste this script into console as user root:

```bash
apt-get install sysstat

#!/bin/sh
while true; do
wget -O /dev/null -q "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=`mpstat -P ALL 1 1 | awk '/Average:/ && $2 ~ /[0-9]/ {print $3}' | sort -r -g | xargs | sed s/\ /,/g`%cpuload"
done &
```

To automatically run it at startup in ubuntu/debian, paste this into a root shell:

```bash 
sed -i "/exit 0/d" /etc/rc.local # remove exit 0
cat >> /etc/rc.local << 'EOF'
while true; do
wget -O /dev/null -q "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=`mpstat -P ALL 1 1 | awk '/Average:/ && $2 ~ /[0-9]/ {print $3}' | sort -r -g | xargs | sed s/\ /,/g`%cpuload"
done & # fork to background
exit 0
EOF
```

Tags: bash, shell, linux, processor, system