---
layout: post
title: Bash API to get the data in real-time
comments: true
snippet: false
---

You can programmatically get real-time updates from plottico using EventSource API. This is so simple that you can even do this in a bash (almost)one-liner:

```bash
#!/bin/bash
wget -q -O - "https://plotti.co/random_sample/stream" | while IFS= read -r line; do if [ -n "$line" ]; then data=`echo "$line" | cut -f3`; IFS=',' read -r -a array <<< "$data"
        echo ${array[1]} # do whatever you like with ${array[0]}, ${array[1]}, ... etc
fi; done

```

If you copy-paste these lines in your command prompt you'll get the result like this:

```
7.59360774564
7.09947302731
7.32174092285
...
```

the `array` variable is ready for further processing in your script, for example you can redirect the data to the file to store it.

Tags: bash, API, EventSource
