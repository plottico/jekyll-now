---
layout: post
title: Linux established connections
---

Plot amount of established connections on a linux box. Paste this script into console as user root:

    #!/bin/bash
    while true; do
    wget -O /dev/null -q "http://plotti.co/plotticonn?k=YOUR_KEY&d=`netstat -tn | grep ESTAB | wc -l`sockets"
    sleep 1
    done &


To automatically run it at startup in ubuntu/debian, paste this into a root shell:

    
    sed '0,/exit 0/{s/exit 0//}' /etc/rc.local # remove exit 0
    cat >> /etc/rc.local << EOF
    while true; do
    wget -O /dev/null -q "http://plotti.co/plotticonn?k=YOUR_KEY&d=`netstat -tn | grep ESTAB | wc -l`sockets"
    sleep 1
    done & # fork to background
    exit 0
    EOF

Tags: bash, shell