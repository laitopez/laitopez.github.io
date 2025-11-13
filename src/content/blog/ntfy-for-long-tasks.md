---
slug: using-ntfy-sh-for-executing-long-running-commands
title: Using ntfy.sh for executing long running commands and mobile notifications
description: "wtf"
pubDate: "Oct 15 2024"
tags: [productivity, shell]
---

[ntfy.sh](https://github.com/binwiederhier/ntfy) is a cool tool for sending push notifications to your mobile device. Here is a quick guide on how to send notificaitons for long running scripts you execute in your shell

1. Download the app
2. Create a "topic" within the app
3. Using curl, send a request to your topic. e.g. `curl https://ntfy.sh/YOUR_TOPIC`

Let's simulate it. Here is what a notification might look like for a passing script

```sh
sleep 30 && \
curl -H prio:low -d "Laptop backup succeeded" ntfy.sh/YOUR_TOPIC || \
curl -H tags:warning -H prio:high -d "Laptop backup failed" ntfy.sh/jc13test
```

Here is what a notification might look like for a failing script

```sh
false && \
curl -H prio:low -d "Laptop backup succeeded" ntfy.sh/YOUR_TOPIC || \
curl -H tags:warning -H prio:high -d "Laptop backup failed" ntfy.sh/jc13test
```

Great, now just replace `sleep 30` or `false` with your script. e.g. `test.py`
