```python
!pip show pandas
```

    Name: pandas
    Version: 1.1.3
    Summary: Powerful data structures for data analysis, time series, and statistics
    Home-page: https://pandas.pydata.org
    Author: None
    Author-email: None
    License: BSD
    Location: /Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8/site-packages
    Requires: pytz, numpy, python-dateutil
    Required-by: seaborn


> pandasに依存されるモジュール

## relativedelta


```python
import datetime as dt
import calendar
from dateutil.relativedelta import *
```


```python
NOW = dt.datetime.now()
TODAY = dt.date.today()

print(f"{NOW=}")
print(f"{TODAY=}")
```

    NOW=datetime.datetime(2020, 11, 8, 22, 17, 0, 181993)
    TODAY=datetime.date(2020, 11, 8)



```python
NOW + relativedelta(months=+1) # 翌月
```




    datetime.datetime(2020, 12, 8, 22, 17, 0, 181993)




```python
NOW + relativedelta(months=+1, weeks=+1) # 翌月プラス一週間
```




    datetime.datetime(2020, 12, 15, 22, 17, 0, 181993)




```python
TODAY + relativedelta(months=+1, weeks=+1, hour=10) # 翌月プラス一週間、朝10時
```




    datetime.datetime(2020, 12, 15, 10, 0)




```python
NOW + relativedelta(year=1, month=1) # 年、月が取り替えられた
```




    datetime.datetime(1, 1, 8, 22, 17, 0, 181993)




```python
relativedelta(dt.date(2021, 1, 1), TODAY) # 差分
```




    relativedelta(months=+1, days=+24)




```python
NOW + relativedelta(years=+1, months=-1) # 11ヶ月後
```




    datetime.datetime(2021, 10, 8, 22, 17, 0, 181993)




```python
dt.date(2020, 1, 31) + relativedelta(months=+1) # 限界を超えない
```




    datetime.date(2020, 2, 29)




```python
dt.date(2020, 2, 29) + relativedelta(years=1) # 閏年も
```




    datetime.date(2021, 2, 28)




```python
TODAY + relativedelta(weekday=FR) # 来週の金曜日
```




    datetime.date(2020, 11, 13)




```python
TODAY + relativedelta(weekday=calendar.FRIDAY) # 同じ
```




    datetime.date(2020, 11, 13)




```python
TODAY + relativedelta(day=30, weekday=FR(-1)) # 今月の最後の金曜日
```




    datetime.date(2020, 11, 27)




```python
TODAY + relativedelta(weekday=WE(+1)) # 次の水曜日
```




    datetime.date(2020, 11, 11)




```python
dt.date(2020, 1, 1) + relativedelta(yearday=313) # 何日過ぎたで日付取得
```




    datetime.date(2020, 11, 8)



## rrule


```python
from dateutil.rrule import *
from dateutil.parser import *
from datetime import *
```


```python
# 日ごと、7回
list(rrule(DAILY, count=7, dtstart=parse("20200808T080000")))
```




    [datetime.datetime(2020, 8, 8, 8, 0),
     datetime.datetime(2020, 8, 9, 8, 0),
     datetime.datetime(2020, 8, 10, 8, 0),
     datetime.datetime(2020, 8, 11, 8, 0),
     datetime.datetime(2020, 8, 12, 8, 0),
     datetime.datetime(2020, 8, 13, 8, 0),
     datetime.datetime(2020, 8, 14, 8, 0)]




```python
# クリスマスまで
list(rrule(
    DAILY,
    dtstart=parse("20201109"),
    until=parse("20201225")
))
```




    [datetime.datetime(2020, 11, 9, 0, 0),
     datetime.datetime(2020, 11, 10, 0, 0),
     datetime.datetime(2020, 11, 11, 0, 0),
     datetime.datetime(2020, 11, 12, 0, 0),
     datetime.datetime(2020, 11, 13, 0, 0),
     datetime.datetime(2020, 11, 14, 0, 0),
     datetime.datetime(2020, 11, 15, 0, 0),
     datetime.datetime(2020, 11, 16, 0, 0),
     datetime.datetime(2020, 11, 17, 0, 0),
     datetime.datetime(2020, 11, 18, 0, 0),
     datetime.datetime(2020, 11, 19, 0, 0),
     datetime.datetime(2020, 11, 20, 0, 0),
     datetime.datetime(2020, 11, 21, 0, 0),
     datetime.datetime(2020, 11, 22, 0, 0),
     datetime.datetime(2020, 11, 23, 0, 0),
     datetime.datetime(2020, 11, 24, 0, 0),
     datetime.datetime(2020, 11, 25, 0, 0),
     datetime.datetime(2020, 11, 26, 0, 0),
     datetime.datetime(2020, 11, 27, 0, 0),
     datetime.datetime(2020, 11, 28, 0, 0),
     datetime.datetime(2020, 11, 29, 0, 0),
     datetime.datetime(2020, 11, 30, 0, 0),
     datetime.datetime(2020, 12, 1, 0, 0),
     datetime.datetime(2020, 12, 2, 0, 0),
     datetime.datetime(2020, 12, 3, 0, 0),
     datetime.datetime(2020, 12, 4, 0, 0),
     datetime.datetime(2020, 12, 5, 0, 0),
     datetime.datetime(2020, 12, 6, 0, 0),
     datetime.datetime(2020, 12, 7, 0, 0),
     datetime.datetime(2020, 12, 8, 0, 0),
     datetime.datetime(2020, 12, 9, 0, 0),
     datetime.datetime(2020, 12, 10, 0, 0),
     datetime.datetime(2020, 12, 11, 0, 0),
     datetime.datetime(2020, 12, 12, 0, 0),
     datetime.datetime(2020, 12, 13, 0, 0),
     datetime.datetime(2020, 12, 14, 0, 0),
     datetime.datetime(2020, 12, 15, 0, 0),
     datetime.datetime(2020, 12, 16, 0, 0),
     datetime.datetime(2020, 12, 17, 0, 0),
     datetime.datetime(2020, 12, 18, 0, 0),
     datetime.datetime(2020, 12, 19, 0, 0),
     datetime.datetime(2020, 12, 20, 0, 0),
     datetime.datetime(2020, 12, 21, 0, 0),
     datetime.datetime(2020, 12, 22, 0, 0),
     datetime.datetime(2020, 12, 23, 0, 0),
     datetime.datetime(2020, 12, 24, 0, 0),
     datetime.datetime(2020, 12, 25, 0, 0)]




```python
# 1日おき、5回
list(rrule(
    DAILY,
    interval=2,
    count=5,
    dtstart=parse("20210101")
))
```




    [datetime.datetime(2021, 1, 1, 0, 0),
     datetime.datetime(2021, 1, 3, 0, 0),
     datetime.datetime(2021, 1, 5, 0, 0),
     datetime.datetime(2021, 1, 7, 0, 0),
     datetime.datetime(2021, 1, 9, 0, 0)]




```python
# 2020年1月1日から2021年1月31日まで一月の全ての日曜日
list(rrule(
    YEARLY,
    bymonth=1,
    byweekday=SU,
    dtstart=parse("20200101"),
    until=parse("20210131")
))
```




    [datetime.datetime(2020, 1, 5, 0, 0),
     datetime.datetime(2020, 1, 12, 0, 0),
     datetime.datetime(2020, 1, 19, 0, 0),
     datetime.datetime(2020, 1, 26, 0, 0),
     datetime.datetime(2021, 1, 3, 0, 0),
     datetime.datetime(2021, 1, 10, 0, 0),
     datetime.datetime(2021, 1, 17, 0, 0),
     datetime.datetime(2021, 1, 24, 0, 0),
     datetime.datetime(2021, 1, 31, 0, 0)]




```python
# 年間の毎月最初の土日
list(rrule(
    MONTHLY,
    count=24,
    byweekday=(SA(1),SU(1)),
    dtstart=parse("20210101")
))
```




    [datetime.datetime(2021, 1, 2, 0, 0),
     datetime.datetime(2021, 1, 3, 0, 0),
     datetime.datetime(2021, 2, 6, 0, 0),
     datetime.datetime(2021, 2, 7, 0, 0),
     datetime.datetime(2021, 3, 6, 0, 0),
     datetime.datetime(2021, 3, 7, 0, 0),
     datetime.datetime(2021, 4, 3, 0, 0),
     datetime.datetime(2021, 4, 4, 0, 0),
     datetime.datetime(2021, 5, 1, 0, 0),
     datetime.datetime(2021, 5, 2, 0, 0),
     datetime.datetime(2021, 6, 5, 0, 0),
     datetime.datetime(2021, 6, 6, 0, 0),
     datetime.datetime(2021, 7, 3, 0, 0),
     datetime.datetime(2021, 7, 4, 0, 0),
     datetime.datetime(2021, 8, 1, 0, 0),
     datetime.datetime(2021, 8, 7, 0, 0),
     datetime.datetime(2021, 9, 4, 0, 0),
     datetime.datetime(2021, 9, 5, 0, 0),
     datetime.datetime(2021, 10, 2, 0, 0),
     datetime.datetime(2021, 10, 3, 0, 0),
     datetime.datetime(2021, 11, 6, 0, 0),
     datetime.datetime(2021, 11, 7, 0, 0),
     datetime.datetime(2021, 12, 4, 0, 0),
     datetime.datetime(2021, 12, 5, 0, 0)]




```python
# 一ヶ月おき、毎月の最初と最後の日曜日、10回カウント
list(rrule(
    MONTHLY,
    interval=2,
    count=10,
    byweekday=(SU(1), SU(-1)),
    dtstart=parse("20210101")
))
```




    [datetime.datetime(2021, 1, 3, 0, 0),
     datetime.datetime(2021, 1, 31, 0, 0),
     datetime.datetime(2021, 3, 7, 0, 0),
     datetime.datetime(2021, 3, 28, 0, 0),
     datetime.datetime(2021, 5, 2, 0, 0),
     datetime.datetime(2021, 5, 30, 0, 0),
     datetime.datetime(2021, 7, 4, 0, 0),
     datetime.datetime(2021, 7, 25, 0, 0),
     datetime.datetime(2021, 9, 5, 0, 0),
     datetime.datetime(2021, 9, 26, 0, 0)]




```python
# 毎月の2日と15日、5回カウント
list(rrule(
    MONTHLY,
    count=5,
    bymonthday=(2, 15),
    dtstart=parse("20201225")
))
```




    [datetime.datetime(2021, 1, 2, 0, 0),
     datetime.datetime(2021, 1, 15, 0, 0),
     datetime.datetime(2021, 2, 2, 0, 0),
     datetime.datetime(2021, 2, 15, 0, 0),
     datetime.datetime(2021, 3, 2, 0, 0)]




```python
list(rrule(
    MONTHLY,
    count=5,
    bymonthday=(-1, 1, ), # 月の最初と最後の日
    dtstart=parse("20201111")
))
```




    [datetime.datetime(2020, 11, 30, 0, 0),
     datetime.datetime(2020, 12, 1, 0, 0),
     datetime.datetime(2020, 12, 31, 0, 0),
     datetime.datetime(2021, 1, 1, 0, 0),
     datetime.datetime(2021, 1, 31, 0, 0)]




```python
list(rrule(
    YEARLY,
    count=4,
    bymonth=(6, 7), # 6月、７月
    dtstart=parse("20200401")
))
```




    [datetime.datetime(2020, 6, 1, 0, 0),
     datetime.datetime(2020, 7, 1, 0, 0),
     datetime.datetime(2021, 6, 1, 0, 0),
     datetime.datetime(2021, 7, 1, 0, 0)]




```python
list(rrule(
    YEARLY,
    count=4,
    interval=3,
    byyearday=(1, 100, 200, 300), # 1年の1日目、100日目、200日目、300日目
    dtstart=parse("20200131T222222")
))
```




    [datetime.datetime(2020, 4, 9, 22, 22, 22),
     datetime.datetime(2020, 7, 18, 22, 22, 22),
     datetime.datetime(2020, 10, 26, 22, 22, 22),
     datetime.datetime(2023, 1, 1, 22, 22, 22)]




```python
list(rrule(
    YEARLY,
    count=3,
    byweekday=MO(20), # 20番目の月曜日
    dtstart=parse("20210105")
))
```




    [datetime.datetime(2021, 5, 17, 0, 0),
     datetime.datetime(2022, 5, 16, 0, 0),
     datetime.datetime(2023, 5, 15, 0, 0)]




```python
list(rrule(
    WEEKLY,
    count=3,
    byweekno=53, #53週目
    byweekday=MO,
    dtstart=parse("20201111")
))
```




    [datetime.datetime(2020, 12, 28, 0, 0),
     datetime.datetime(2026, 12, 28, 0, 0),
     datetime.datetime(2032, 12, 27, 0, 0)]


