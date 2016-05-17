---
layout: post
title: Python random feed
comments: true
snippet: true
---

Plot some random values with python on an embeddable real-time SVG plot. 

<object data="https://plotti.co/random_sample/300x80.svg" type="image/svg+xml"></object>

Here is the full python script that plottico uses internally to feed the sample data. You can just copy-and-paste it and run - it is already configured. You will see your result in the plot below.

```python
#!/usr/bin/python
import urllib2, time, random
rnd = [0.,0.,0.]
phash = "YOUR_HASH"
caption = "rand"
key = "YOUR_KEY"
while True:
    for i in range(len(rnd)): 
        rnd[i]+=(random.random()-0.5)
        if rnd[i] > 10.0: rnd = [0.,0.,0.]
        elif rnd[i] < 0.0: rnd[i] = 0.0
    urllib2.urlopen("https://plotti.co/%s?d=%s,%s&k=%s" % (phash, ','.join(str(x) for x in rnd), caption, key) ).read()
    time.sleep(0.3)
```

Tags: python, random
