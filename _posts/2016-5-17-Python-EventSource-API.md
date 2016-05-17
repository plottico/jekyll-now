---
layout: post
title: Python EventSource push API to get the data
comments: true
snippet: false
---

You can programmatically get real-time updates from plottico using EventSource API. In this example we will use `eventsource` python library. You can install it by issuing 

```bash
pip install eventsource
```

For example, to get this data:

<object data="https://plotti.co/random_sample/300x80.svg" type="image/svg+xml"></object>


This python script will extract the data from `random_sample` stream into python array:


```python
#!/usr/bin/python
from eventsource.client import EventSourceClient

PLOT_HASH = "random_sample"

es = EventSourceClient(url="plotti.co",
                      action = PLOT_HASH,
                      target = "stream",
                      retry = True,
                      keep_alive = True,
                      ssl = True,
                      validate_cert = True)


def process_data(message):
    "will process incoming data"
    data = message.split("\t")[2]
    array = []
    for v in data.split(","):
        try:
            array.append(float(v))
        except:
            pass
    print array # array contains an array of floating-point values recieved


es.handle_stream = process_data
es.poll()
```

You will see the result like this:

```
grandrew@p1:~$ python ./py_es_test.py 
[4.15833229828, 5.28536101629, 2.65816522118]
[4.37887435627, 4.91893815899, 2.54470034079]
[4.23270324901, 4.74048473534, 2.83952247463]
...
```

Tags: python, API
