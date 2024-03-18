---
title: "apm-datacarrier"
sequence: "101"
---

- project: `apm-commons/apm-datacarrier`
- package: `org.apache.skywalking.apm.commons.datacarrier`

```text
Data --> Consumer --> Thread --> Driver --> DataCarrier
```

- QueueBuffer
- data
    - Buffer
    - Channels
    - Group
- thread
    - ConsumerThread
    - MultipleChannelsConsumer

- Data
- Data Consumer
- Thread
- Driver

{:refdef: style="text-align: center;"}
![](/assets/images/skywalking/source/sw-src-data-carrier-buffer.png)
{:refdef}

{:refdef: style="text-align: center;"}
![](/assets/images/skywalking/source/sw-src-data-carrier-channels.png)
{:refdef}

{:refdef: style="text-align: center;"}
![](/assets/images/skywalking/source/sw-src-data-carrier-consumer-thread.png)
{:refdef}

{:refdef: style="text-align: center;"}
![](/assets/images/skywalking/source/sw-src-data-carrier-group.png)
{:refdef}

{:refdef: style="text-align: center;"}
![](/assets/images/skywalking/source/sw-src-data-carrier-multiple-channels-consumer.png)
{:refdef}

