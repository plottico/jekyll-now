---
layout: post
title: TX bandwidth utilization on linux
comments: true
snippet: true
---

Plot current transmission network load (bandwidth utilization) in real-time on a linux box. 

<object data="https://plotti.co/plotticonet/300x80.svg" type="image/svg+xml"></object>

Paste this script into console as user root:

```bash
#!/bin/bash
S=1; F=/sys/class/net/eth0/statistics/tx_bytes
while true; do
  X=`cat $F`; sleep $S; Y=`cat $F`; BPS="$(((Y-X)/S*8))";
  wget "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=${BPS}bps" -q -O /dev/null
done &
```

To automatically run it at startup in ubuntu/debian, paste this into a root shell:

```bash 
sed -i "/exit 0/d" /etc/rc.local # remove exit 0
cat >> /etc/rc.local << 'EOF'
S=1; F=/sys/class/net/eth0/statistics/tx_bytes
while true; do
  X=`cat $F`; sleep $S; Y=`cat $F`; BPS="$(((Y-X)/S*8))";
  wget "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=${BPS}bps" -q -O /dev/null
done & # fork to background
exit 0
EOF
```

Tags: bash, shell, linux, network, ubuntu
