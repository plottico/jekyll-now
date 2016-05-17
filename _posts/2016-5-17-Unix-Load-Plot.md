---
layout: post
title: Unix Load Plot
comments: true
snippet: true
---

Plot current load on a unix host. 

Paste this script into console as user root:

```bash
#!/bin/bash
while true; do
wget -O /dev/null -q "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=,`cat /proc/loadavg | cut -d' ' -f2`,loadavg"
sleep 30
done &
```

To automatically run it at startup in ubuntu/debian, paste this into a root shell:

```bash 
sed -i "/exit 0/d" /etc/rc.local # remove exit 0
cat >> /etc/rc.local << 'EOF'
while true; do
wget -O /dev/null -q "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=,`cat /proc/loadavg | cut -d' ' -f2`,loadavg"
sleep 30
done & # fork to background
exit 0
EOF
```

This is a slow updating plot as unix load is an avarage over several minutes. If you want a faster/slower update then you may want to change `sleep 30` to different interval and in
`cut -d' ' -f2` change `-f2` to `-f1` for faster average and to `-f3` for even slower updates.

Tags: bash, shell, linux, processor, system, load, loadavg