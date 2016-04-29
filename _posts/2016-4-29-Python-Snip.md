---
layout: post
title: Python code for non-blocking updates
---

Example of python code for non-blocking update push. Put this in your module as a global definition.

```python
####################################
# PLOTTICO SNIPPET USAGE: 
# >>> plottico.put(0); plottico.put([0,1,2])
PT_KEY = "YOUR_KEY" # plot update push secret here
PT_HASH = "YOUR_HASH" # - https://plotti.co/YOUR_HASH
PT_CAPTION = "" # y axis title
import Queue, threading, urllib2; plottico = Queue.Queue()
def pt_updatr(q, phash, key="", caption=""):
    while True:
        v = q.get()
        if hasattr(v, '__iter__'): v = ','.join(str(x) for x in v)
        urllib2.urlopen("https://plotti.co/%s?d=%s%s&k=%s" % (phash, v, caption, key) ).read(); q.task_done()
pt_wkr = threading.Thread(target=pt_updatr, args=(plottico, PT_HASH, PT_KEY, PT_CAPTION)); pt_wkr.setDaemon(True); pt_wkr.start()
# <<< END PLOTTICO SNIPPPET
####################################
```

To use, put this anywhere in your code:

```python
# to put:
plottico.put(0)
# or:
plottico.put([0,0,0])
```

This defines a global variable `plottico` in your module. You can add different streams to different modules with non-overlapping namespaces (do not do `from XXX import *`).
