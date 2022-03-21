## Times


```python
import datetime as dt

t = dt.time(1, 2, 3)
print(t)
print('hour       :', t.hour)
print('minute     :', t.minute)
print('second     :', t.second)
print('microsecond:', t.microsecond)
print('tzinfo     :', t.tzinfo)
```

    01:02:03
    hour       : 1
    minute     : 2
    second     : 3
    microsecond: 0
    tzinfo     : None



```python
import datetime as dt

print('Earliest  :', dt.time.min)
print('Latest    :', dt.time.max)
print('Resolution:', dt.time.resolution)
```

    Earliest  : 00:00:00
    Latest    : 23:59:59.999999
    Resolution: 0:00:00.000001


## Dates


```python
import datetime as dt

today = dt.date.today()
print(today)
print('ctime  :', today.ctime())
tt = today.timetuple()
print('tuple  : tm_year  =', tt.tm_year)
print('         tm_mon   =', tt.tm_mon)
print('         tm_mday  =', tt.tm_mday)
print('         tm_hour  =', tt.tm_hour)
print('         tm_min   =', tt.tm_min)
print('         tm_sec   =', tt.tm_sec)
print('         tm_wday  =', tt.tm_wday) # [0,6]の間の数、月曜が 0
print('         tm_yday  =', tt.tm_yday)
print('         tm_isdst =', tt.tm_isdst) # 夏時間であるかどうか
print('Year   :', today.year)
print('Mon    :', today.month)
print('Day    :', today.day)

```

    2020-11-08
    ctime  : Sun Nov  8 00:00:00 2020
    tuple  : tm_year  = 2020
             tm_mon   = 11
             tm_mday  = 8
             tm_hour  = 0
             tm_min   = 0
             tm_sec   = 0
             tm_wday  = 6
             tm_yday  = 313
             tm_isdst = -1
    Year   : 2020
    Mon    : 11
    Day    : 8



```python
import datetime as dt
import time

t = time.time()
print('timestamp       :', t)
print('fromtimestamp(t):', dt.date.fromtimestamp(t))
```

    timestamp       : 1604822120.369205
    fromtimestamp(t): 2020-11-08



```python
import datetime as dt

print('Earliest  :', dt.date.min)
print('Latest    :', dt.date.max)
print('Resolution:', dt.date.resolution)
```

    Earliest  : 0001-01-01
    Latest    : 9999-12-31
    Resolution: 1 day, 0:00:00



```python
import datetime as dt

d1 = dt.date(2008, 8, 8)
print('d1:', d1.ctime())

d2 = d1.replace(year=2020)
print('d2:', d2.ctime())
```

    d1: Fri Aug  8 00:00:00 2008
    d2: Sat Aug  8 00:00:00 2020


## timedeltas


```python
import datetime as dt

print('microseconds:', dt.timedelta(microseconds=1))
print('milliseconds:', dt.timedelta(milliseconds=1))
print('seconds     :', dt.timedelta(seconds=1))
print('minutes     :', dt.timedelta(minutes=1))
print('hours       :', dt.timedelta(hours=1))
print('days        :', dt.timedelta(days=1))
print('weeks       :', dt.timedelta(weeks=1))
```

    microseconds: 0:00:00.000001
    milliseconds: 0:00:00.001000
    seconds     : 0:00:01
    minutes     : 0:01:00
    hours       : 1:00:00
    days        : 1 day, 0:00:00
    weeks       : 7 days, 0:00:00



```python
import datetime as dt

for delta in [dt.timedelta(microseconds=1),
              dt.timedelta(milliseconds=1),
              dt.timedelta(seconds=1),
              dt.timedelta(minutes=1),
              dt.timedelta(hours=1),
              dt.timedelta(days=1),
              dt.timedelta(weeks=1),
              ]:
    print(f'{str(delta):15} = {delta.total_seconds():8} seconds')
```

    0:00:00.000001  =    1e-06 seconds
    0:00:00.001000  =    0.001 seconds
    0:00:01         =      1.0 seconds
    0:01:00         =     60.0 seconds
    1:00:00         =   3600.0 seconds
    1 day, 0:00:00  =  86400.0 seconds
    7 days, 0:00:00 = 604800.0 seconds


## 日付計算


```python
import datetime as dt

today = dt.date.today()
print('Today    :', today)

one_day = dt.timedelta(days=1)
print('One day  :', one_day)

yesterday = today - one_day
print('Yesterday:', yesterday)

tomorrow = today + one_day
print('Tomorrow :', tomorrow)

print()
print('tomorrow - yesterday:', tomorrow - yesterday)
print('yesterday - tomorrow:', yesterday - tomorrow)
```

    Today    : 2020-11-08
    One day  : 1 day, 0:00:00
    Yesterday: 2020-11-07
    Tomorrow : 2020-11-09
    
    tomorrow - yesterday: 2 days, 0:00:00
    yesterday - tomorrow: -2 days, 0:00:00



```python
import datetime as dt

one_day = dt.timedelta(days=1)
print('1 day    :', one_day)
print('5 days   :', one_day * 5)
print('1.5 days :', one_day * 1.5)
print('1/4 day  :', one_day / 4)
```

    1 day    : 1 day, 0:00:00
    5 days   : 5 days, 0:00:00
    1.5 days : 1 day, 12:00:00
    1/4 day  : 6:00:00


## 比較


```python
import datetime as dt

print('Times:')
t1 = dt.time(12, 55, 0)
print('  t1:', t1)
t2 = dt.time(13, 5, 0)
print('  t2:', t2)
print('  t1 < t2:', t1 < t2)

print()
print('Dates:')
d1 = dt.date.today()
print('  d1:', d1)
d2 = dt.date.today() + datetime.timedelta(days=1)
print('  d2:', d2)
print('  d1 > d2:', d1 > d2)
```

    Times:
      t1: 12:55:00
      t2: 13:05:00
      t1 < t2: True
    
    Dates:
      d1: 2020-11-08
      d2: 2020-11-09
      d1 > d2: False


## 日付と時間を結合


```python
import datetime as dt

print('Now    :', dt.datetime.now())
print('Today  :', dt.datetime.today())
print('UTC Now:', dt.datetime.utcnow()) # 9時間の差
print()

FIELDS = [
    'year', 'month', 'day',
    'hour', 'minute', 'second',
    'microsecond',
]

d = dt.datetime.now()
for attr in FIELDS:
    print(f'{attr:15}: {getattr(d, attr)}')
```

    Now    : 2020-11-08 17:09:54.786659
    Today  : 2020-11-08 17:09:54.786994
    UTC Now: 2020-11-08 08:09:54.787114
    
    year           : 2020
    month          : 11
    day            : 8
    hour           : 17
    minute         : 9
    second         : 54
    microsecond    : 787375



```python
import datetime as dt

time = dt.time(1, 2, 3)
print('time :', time)

date = dt.date.today()
print('date :', date)

datetime = dt.datetime.combine(date, time)
print('datetime:', datetime)
```

    time : 01:02:03
    date : 2020-11-08
    datetime: 2020-11-08 01:02:03


## 書式化と解析


```python
import datetime as dt

format = "%a %b %d %H:%M:%S %Y"

today = dt.datetime.today()
print('ISO     :', today)

s = today.strftime(format)
print('strftime:', s)

d = dt.datetime.strptime(s, format)
print('strptime:', d.strftime(format))
```

    ISO     : 2020-11-08 17:18:45.292055
    strftime: Sun Nov 08 17:18:45 2020
    strptime: Sun Nov 08 17:18:45 2020


[書式コード](https://docs.python.org/ja/3/library/datetime.html#strftime-and-strptime-format-codes)

* %d : 0埋めした10進数で表記した月中の日にち
* %m : 0埋めした10進数で表記した月
* %y : 0埋めした10進数で表記した西暦の下2桁
* %Y : 0埋めした10進数で表記した西暦4桁
* %H : 0埋めした10進数で表記した時 （24時間表記）
* %I : 0埋めした10進数で表記した時 （12時間表記）
* %M : 0埋めした10進数で表記した分
* %S : 0埋めした10進数で表記した秒
* %f : 0埋めした10進数で表記したマイクロ秒（6桁）
* %A : ロケールの曜日名
* %a : ロケールの曜日名（短縮形）
* %B : ロケールの月名
* %b : ロケールの月名（短縮形）
* %j : 0埋めした10進数で表記した年中の日にち（正月が'001'）
* %U : 0埋めした10進数で表記した年中の週番号 （週の始まりは日曜日）
* %W : 0埋めした10進数で表記した年中の週番号 （週の始まりは月曜日）

