## 参考資料

* [公式ドキュメント](https://docs.python.org/ja/3/library/time.html)
* [PyMOTW3](https://pymotw.com/3/time/index.html)
* [关于时间的知识](https://mp.weixin.qq.com/s/XeoQGtvfgwm79C0UlsmRTw)

## 用語の説明と慣習

* [エポック (epoch)](https://en.wikipedia.org/wiki/Epoch_(computing)) : 時刻の起点、プラットフォーム依存。
    * *Unix*では(UTC で) 1970年1月1日0時0分0秒を指す
    * *Excel*では(UTC で) 1900年1月**0**日0時0分0秒を指す
* エポック秒 (seconds since the epoch) : エポックからの総経過秒数、たいていはうるう秒 (leap seconds) は含まれていない
* UTC: [協定世界時 (Coordinated Universal Time)](https://ja.wikipedia.org/wiki/協定世界時)
* DST: [夏時間 (Daylight Saving Time)](https://ja.wikipedia.org/wiki/夏時間) のことで、一年のうちの一定期間に 1 時間タイムゾーンを修正


1. 人类的早期生活，依靠观测「天文现象」来测量时间，基于地球自转规律，定义了一套时间标准：「世界时」。
2. 后来人们发现，由于地球公转轨道是一个椭圆，并且地球自转还受到地球内部的影响，自转速度越来越慢，人们发现世界时测算出的时间「不准」。
3. 科学家们开始从「微观世界」寻找更稳定的周期运动，最终确定以「铯原子」的振动频率为基准，制造出了「原子钟」，确立了「世界原子时」，并重新定义了「秒」长度，时长高度精确。
4. 但由于人类社会活动已高度依赖「世界时」，所以科学家们基于「原子时」和「世界时」，最终确立出新的时间标准：「世界协调时」，把它定义成了全球的时间标准，至此，世界标准时间诞生。
5. 中国基于「世界协调时」再加上 8 小时时区之差，确立了「北京时间」，并广播给整个中国大地使用。
6. 「国家授时中心」把北京时间广播给全国的「时间服务器」，我们生活中使用的时间，例如计算机，就是通过时间服务器自动同步校准的。
7. 计算机通过 NTP 完成和时间服务器的「自动校准」，我们的应用程序基于此，才得以获取到准确的时间。
8. NTP 服务应该采用润物细无声的方式同步时间，避免时间发生「倒流」。

> 注意：このモジュールの中の関数は、エポック以前あるいは遠い未来の日付や時刻を扱うことができません


```python
import textwrap
import time

available_clocks = [
    ('monotonic', time.monotonic),
    ('perf_counter', time.perf_counter),
    ('process_time', time.process_time),
    ('time', time.time),
]

for clock_name, func in available_clocks:
    print(textwrap.dedent('''\
    {name}:
        adjustable    : {info.adjustable}
        implementation: {info.implementation}
        monotonic     : {info.monotonic}
        resolution    : {info.resolution}
        current       : {current}
    ''').format(
        name=clock_name,
        info=time.get_clock_info(clock_name),
        current=func())
    )
```

    monotonic:
        adjustable    : False
        implementation: mach_absolute_time()
        monotonic     : True
        resolution    : 1e-09
        current       : 920.109969304
    
    perf_counter:
        adjustable    : False
        implementation: mach_absolute_time()
        monotonic     : True
        resolution    : 1e-09
        current       : 920.110805048
    
    process_time:
        adjustable    : False
        implementation: getrusage(RUSAGE_SELF)
        monotonic     : True
        resolution    : 1e-06
        current       : 0.848872
    
    time:
        adjustable    : True
        implementation: gettimeofday()
        monotonic     : False
        resolution    : 1e-06
        current       : 1604588233.9574778
    


## Wall Clock Time


```python
import time

print("The time is:", time.time())
```

    The time is: 1604588370.425008


`time.time()`はエポック以来の秒数を戻る


```python
import time

print('The time is      :', time.ctime())
later = time.time() + 15
print('15 secs from now :', time.ctime(later))
```

    The time is      : Fri Nov  6 00:02:30 2020
    15 secs from now : Fri Nov  6 00:02:45 2020



```python
`time.ctime(seconds)`はエポック以来の秒数を人間が読める形で時間を表示する
```

## Monotonic Clocks

> `time()`はシステム時間を利用していて、システム時間はユーザー或いはシステム同期サービスで  
> 変えられる。もし時間を測っているならこの影響を受けたくない、そこで登場するのは`monotonic()`


```python
import time

start = time.monotonic()
time.sleep(0.1)
end = time.monotonic()
print(f'start : {start:>9.2f}')
print(f'end   : {end:>9.2f}')
print(f'span  : {end - start:>9.2f}')
```

    start :   1908.15
    end   :   1908.25
    span  :      0.10


`monotonic()`のスタートポイントは定義されていない、ゆえに計算した結果だけ意味ある

## Processor Clock Time


```python
%%writefile foo.py

import hashlib
import time

data = open(__file__, 'rb').read()

for i in range(20):
    h = hashlib.sha1()
    print(time.ctime(), f': {time.time():0.3f} {time.process_time():0.3f}')
    for i in range(300000):
        h.update(data)
    cksum = h.digest()
```

    Writing foo.py



```python
%run foo.py
```

    Fri Nov  6 00:25:12 2020 : 1604589912.435 10.900
    Fri Nov  6 00:25:12 2020 : 1604589912.584 11.043
    Fri Nov  6 00:25:12 2020 : 1604589912.732 11.182
    Fri Nov  6 00:25:12 2020 : 1604589912.867 11.316
    Fri Nov  6 00:25:13 2020 : 1604589913.008 11.453
    Fri Nov  6 00:25:13 2020 : 1604589913.147 11.589
    Fri Nov  6 00:25:13 2020 : 1604589913.298 11.736
    Fri Nov  6 00:25:13 2020 : 1604589913.440 11.875
    Fri Nov  6 00:25:13 2020 : 1604589913.592 12.024
    Fri Nov  6 00:25:13 2020 : 1604589913.735 12.164
    Fri Nov  6 00:25:13 2020 : 1604589913.875 12.302
    Fri Nov  6 00:25:14 2020 : 1604589914.011 12.436
    Fri Nov  6 00:25:14 2020 : 1604589914.156 12.578
    Fri Nov  6 00:25:14 2020 : 1604589914.305 12.724
    Fri Nov  6 00:25:14 2020 : 1604589914.454 12.869
    Fri Nov  6 00:25:14 2020 : 1604589914.595 13.007
    Fri Nov  6 00:25:14 2020 : 1604589914.758 13.160
    Fri Nov  6 00:25:14 2020 : 1604589914.913 13.304
    Fri Nov  6 00:25:15 2020 : 1604589915.052 13.440
    Fri Nov  6 00:25:15 2020 : 1604589915.184 13.570



```python
!rm foo.py
```

`process_time()`は名の通り、プロセスが掛かる時間を測る


```python
import time

template = '{} - {:0.2f} - {:0.2f}'

print(template.format(
    time.ctime(), time.time(), time.process_time())
)

for i in range(3, 0, -1):
    print('Sleeping', i)
    time.sleep(i)
    print(template.format(
        time.ctime(), time.time(), time.process_time())
    )
```

    Fri Nov  6 00:29:22 2020 - 1604590162.28 - 14.85
    Sleeping 3
    Fri Nov  6 00:29:25 2020 - 1604590165.29 - 14.85
    Sleeping 2
    Fri Nov  6 00:29:27 2020 - 1604590167.29 - 14.85
    Sleeping 1
    Fri Nov  6 00:29:28 2020 - 1604590168.30 - 14.85


> プログラムが何もしていないならプロセスクロックは測らない

## Performance Counter


```python
%%writefile bar.py

import hashlib
import time

data = open(__file__, 'rb').read()

loop_start = time.perf_counter()

for i in range(5):
    iter_start = time.perf_counter()
    h = hashlib.sha1()
    for i in range(300000):
        h.update(data)
    cksum = h.digest()
    now = time.perf_counter()
    loop_elapsed = now - loop_start
    iter_elapsed = now - iter_start
    print(time.ctime(), f': {iter_elapsed:0.3f} {loop_elapsed:0.3f}')
```

    Writing bar.py



```python
%run bar.py
```

    Fri Nov  6 00:47:11 2020 : 0.188 0.188
    Fri Nov  6 00:47:11 2020 : 0.186 0.374
    Fri Nov  6 00:47:11 2020 : 0.188 0.561
    Fri Nov  6 00:47:11 2020 : 0.181 0.743
    Fri Nov  6 00:47:12 2020 : 0.188 0.931



```python
!rm bar.py
```

> プログラムの性能を測る際、高解析度のmonotonic clockが大事  
> `perf_counter`はそのために誕生される

※`monotonic()`と同じ、絶対値は意味なく、相対値を利用すべき

## Time Components


```python
import time


def show_struct(s):
    print('  tm_year :', s.tm_year)
    print('  tm_mon  :', s.tm_mon)
    print('  tm_mday :', s.tm_mday)
    print('  tm_hour :', s.tm_hour)
    print('  tm_min  :', s.tm_min)
    print('  tm_sec  :', s.tm_sec)
    print('  tm_wday :', s.tm_wday) # [0,6]の間の数、月曜が 0
    print('  tm_yday :', s.tm_yday) # [1, 366]の間の数  
    print('  tm_isdst:', s.tm_isdst) # 夏時間であるかどうか


print('gmtime:')
show_struct(time.gmtime())
print('\nlocaltime:')
show_struct(time.localtime())
print('\nmktime:', time.mktime(time.localtime()))
```

    gmtime:
      tm_year : 2020
      tm_mon  : 11
      tm_mday : 5
      tm_hour : 15
      tm_min  : 55
      tm_sec  : 11
      tm_wday : 3
      tm_yday : 310
      tm_isdst: 0
    
    localtime:
      tm_year : 2020
      tm_mon  : 11
      tm_mday : 6
      tm_hour : 0
      tm_min  : 55
      tm_sec  : 11
      tm_wday : 4
      tm_yday : 311
      tm_isdst: 0
    
    mktime: 1604591711.0


## Working with Time Zones


```python
import time
import os


def show_zone_info():
    print('  TZ    :', os.environ.get('TZ', '(not set)'))
    print('  tzname:', time.tzname)
    print('  Zone  : {} ({})'.format(
        time.timezone, (time.timezone / 3600)))
    print('  DST   :', time.daylight)
    print('  Time  :', time.ctime())
    print()


print('Default :')
show_zone_info()

ZONES = [
    'GMT',
    'Europe/Amsterdam',
]

for zone in ZONES:
    os.environ['TZ'] = zone
    time.tzset()
    print(zone, ':')
    show_zone_info()
```

    Default :
      TZ    : (not set)
      tzname: ('JST', 'JST')
      Zone  : -32400 (-9.0)
      DST   : 0
      Time  : Fri Nov  6 01:02:09 2020
    
    GMT :
      TZ    : GMT
      tzname: ('GMT', 'GMT')
      Zone  : 0 (0.0)
      DST   : 0
      Time  : Thu Nov  5 16:02:09 2020
    
    Europe/Amsterdam :
      TZ    : Europe/Amsterdam
      tzname: ('CET', 'CEST')
      Zone  : -3600 (-1.0)
      DST   : 1
      Time  : Thu Nov  5 17:02:09 2020
    


## Parsing and Formatting Times


```python
import time


def show_struct(s):
    print('  tm_year :', s.tm_year)
    print('  tm_mon  :', s.tm_mon)
    print('  tm_mday :', s.tm_mday)
    print('  tm_hour :', s.tm_hour)
    print('  tm_min  :', s.tm_min)
    print('  tm_sec  :', s.tm_sec)
    print('  tm_wday :', s.tm_wday)
    print('  tm_yday :', s.tm_yday)
    print('  tm_isdst:', s.tm_isdst)


now = time.ctime()
print('Now:', now)

parsed = time.strptime(now)
print('\nParsed:')
show_struct(parsed)

print('\nFormatted:',
      time.strftime("%a %b %d %H:%M:%S %Y", parsed))
```

    Now: Thu Nov  5 17:03:21 2020
    
    Parsed:
      tm_year : 2020
      tm_mon  : 11
      tm_mday : 5
      tm_hour : 17
      tm_min  : 3
      tm_sec  : 21
      tm_wday : 3
      tm_yday : 310
      tm_isdst: -1
    
    Formatted: Thu Nov 05 17:03:21 2020



```python

```
