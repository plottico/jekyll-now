---
layout: post
title: RX/TX bandwidth single plot on linux
comments: true
snippet: true
---

Plot current network load (bandwidth utilization) in real-time on a linux box. Both TX and RX are displayed on a single plot. 

<object data="https://plotti.co/plotticonet/300x80.svg" type="image/svg+xml"></object>

Paste this script into console as user root:

```bash
#!/bin/bash
S=1; O=/sys/class/net/eth0/statistics/tx_bytes
I=/sys/class/net/eth0/statistics/rx_bytes
while true; do
  XO=`cat $O`; XI=`cat $I`; sleep $S; YO=`cat $O`; YI=`cat $I`; 
  BPSI="$(((YI-XI)/S*8))"; BPSO="$(((YO-XO)/S*8))";
  wget "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=${BPSI},${BPSO}bps" -q -O /dev/null; 
done &
```

To automatically run it at startup in ubuntu/debian, paste this into a root shell:

```bash 
sed -i "/exit 0/d" /etc/rc.local # remove exit 0
cat >> /etc/rc.local << 'EOF'
S=1; O=/sys/class/net/eth0/statistics/tx_bytes
I=/sys/class/net/eth0/statistics/rx_bytes
while true; do
  XO=`cat $O`; XI=`cat $I`; sleep $S; YO=`cat $O`; YI=`cat $I`; 
  BPSI="$(((YI-XI)/S*8))"; BPSO="$(((YO-XO)/S*8))";
  wget "https://plotti.co/YOUR_HASH?k=YOUR_KEY&d=${BPSI},${BPSO}bps" -q -O /dev/null; 
done &
exit 0
EOF
```

Tags: bash, shell, linux, network, ubuntu
