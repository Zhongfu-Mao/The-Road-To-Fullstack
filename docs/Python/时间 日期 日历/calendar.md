参考資料
* [Pythonのcalendarでカレンダーを取得・出力（テキスト、HTMLなど）](https://note.nkmk.me/python-calendar-text-html-list/)
* [PYMOTW](https://pymotw.com/3/calendar/index.html)

## 月間カレンダー

### month()


```python
import calendar

print(calendar.month(2020, 11)) # 戻り値は文字列
```

       November 2020
    Mo Tu We Th Fr Sa Su
                       1
     2  3  4  5  6  7  8
     9 10 11 12 13 14 15
    16 17 18 19 20 21 22
    23 24 25 26 27 28 29
    30
    



```python
# 引数wで列幅、引数lで行幅を指定可能
print(calendar.month(2020, 11, w=7, l=2))
```

                         November 2020
    
      Mon     Tue     Wed     Thu     Fri     Sat     Sun
    
                                                        1
    
        2       3       4       5       6       7       8
    
        9      10      11      12      13      14      15
    
       16      17      18      19      20      21      22
    
       23      24      25      26      27      28      29
    
       30
    
    


### prmonth()


```python
import calendar

c = calendar.TextCalendar(calendar.SUNDAY) # 日曜日を一週間のスタートとする(デフォルトは月曜日)
c.prmonth(2020, 11)
```

       November 2020
    Su Mo Tu We Th Fr Sa
     1  2  3  4  5  6  7
     8  9 10 11 12 13 14
    15 16 17 18 19 20 21
    22 23 24 25 26 27 28
    29 30


> `prmonth()`はフォーマットずみの月間カレンダーを出力する  
> 一方、`month()`は文字列を戻る

## 年間カレンダー

### calendar()


```python
print(calendar.calendar(2020))
```

                                      2020
    
          January                   February                   March
    Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
           1  2  3  4  5                      1  2                         1
     6  7  8  9 10 11 12       3  4  5  6  7  8  9       2  3  4  5  6  7  8
    13 14 15 16 17 18 19      10 11 12 13 14 15 16       9 10 11 12 13 14 15
    20 21 22 23 24 25 26      17 18 19 20 21 22 23      16 17 18 19 20 21 22
    27 28 29 30 31            24 25 26 27 28 29         23 24 25 26 27 28 29
                                                        30 31
    
           April                      May                       June
    Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
           1  2  3  4  5                   1  2  3       1  2  3  4  5  6  7
     6  7  8  9 10 11 12       4  5  6  7  8  9 10       8  9 10 11 12 13 14
    13 14 15 16 17 18 19      11 12 13 14 15 16 17      15 16 17 18 19 20 21
    20 21 22 23 24 25 26      18 19 20 21 22 23 24      22 23 24 25 26 27 28
    27 28 29 30               25 26 27 28 29 30 31      29 30
    
            July                     August                  September
    Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
           1  2  3  4  5                      1  2          1  2  3  4  5  6
     6  7  8  9 10 11 12       3  4  5  6  7  8  9       7  8  9 10 11 12 13
    13 14 15 16 17 18 19      10 11 12 13 14 15 16      14 15 16 17 18 19 20
    20 21 22 23 24 25 26      17 18 19 20 21 22 23      21 22 23 24 25 26 27
    27 28 29 30 31            24 25 26 27 28 29 30      28 29 30
                              31
    
          October                   November                  December
    Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
              1  2  3  4                         1          1  2  3  4  5  6
     5  6  7  8  9 10 11       2  3  4  5  6  7  8       7  8  9 10 11 12 13
    12 13 14 15 16 17 18       9 10 11 12 13 14 15      14 15 16 17 18 19 20
    19 20 21 22 23 24 25      16 17 18 19 20 21 22      21 22 23 24 25 26 27
    26 27 28 29 30 31         23 24 25 26 27 28 29      28 29 30 31
                              30
    



```python
print(calendar.calendar(
    2020,
    c=3, # 月の間のスペースの数
    m=4  # 1行に出力する月の数
))
```

                                               2020
    
          January                February                March                  April
    Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su
           1  2  3  4  5                   1  2                      1          1  2  3  4  5
     6  7  8  9 10 11 12    3  4  5  6  7  8  9    2  3  4  5  6  7  8    6  7  8  9 10 11 12
    13 14 15 16 17 18 19   10 11 12 13 14 15 16    9 10 11 12 13 14 15   13 14 15 16 17 18 19
    20 21 22 23 24 25 26   17 18 19 20 21 22 23   16 17 18 19 20 21 22   20 21 22 23 24 25 26
    27 28 29 30 31         24 25 26 27 28 29      23 24 25 26 27 28 29   27 28 29 30
                                                  30 31
    
            May                    June                   July                  August
    Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su
                 1  2  3    1  2  3  4  5  6  7          1  2  3  4  5                   1  2
     4  5  6  7  8  9 10    8  9 10 11 12 13 14    6  7  8  9 10 11 12    3  4  5  6  7  8  9
    11 12 13 14 15 16 17   15 16 17 18 19 20 21   13 14 15 16 17 18 19   10 11 12 13 14 15 16
    18 19 20 21 22 23 24   22 23 24 25 26 27 28   20 21 22 23 24 25 26   17 18 19 20 21 22 23
    25 26 27 28 29 30 31   29 30                  27 28 29 30 31         24 25 26 27 28 29 30
                                                                         31
    
         September               October                November               December
    Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su
        1  2  3  4  5  6             1  2  3  4                      1       1  2  3  4  5  6
     7  8  9 10 11 12 13    5  6  7  8  9 10 11    2  3  4  5  6  7  8    7  8  9 10 11 12 13
    14 15 16 17 18 19 20   12 13 14 15 16 17 18    9 10 11 12 13 14 15   14 15 16 17 18 19 20
    21 22 23 24 25 26 27   19 20 21 22 23 24 25   16 17 18 19 20 21 22   21 22 23 24 25 26 27
    28 29 30               26 27 28 29 30 31      23 24 25 26 27 28 29   28 29 30 31
                                                  30
    


### prcal()


```python
import calendar

calendar.prcal(2020)
```

                                      2020
    
          January                   February                   March
    Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
           1  2  3  4  5                      1  2                         1
     6  7  8  9 10 11 12       3  4  5  6  7  8  9       2  3  4  5  6  7  8
    13 14 15 16 17 18 19      10 11 12 13 14 15 16       9 10 11 12 13 14 15
    20 21 22 23 24 25 26      17 18 19 20 21 22 23      16 17 18 19 20 21 22
    27 28 29 30 31            24 25 26 27 28 29         23 24 25 26 27 28 29
                                                        30 31
    
           April                      May                       June
    Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
           1  2  3  4  5                   1  2  3       1  2  3  4  5  6  7
     6  7  8  9 10 11 12       4  5  6  7  8  9 10       8  9 10 11 12 13 14
    13 14 15 16 17 18 19      11 12 13 14 15 16 17      15 16 17 18 19 20 21
    20 21 22 23 24 25 26      18 19 20 21 22 23 24      22 23 24 25 26 27 28
    27 28 29 30               25 26 27 28 29 30 31      29 30
    
            July                     August                  September
    Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
           1  2  3  4  5                      1  2          1  2  3  4  5  6
     6  7  8  9 10 11 12       3  4  5  6  7  8  9       7  8  9 10 11 12 13
    13 14 15 16 17 18 19      10 11 12 13 14 15 16      14 15 16 17 18 19 20
    20 21 22 23 24 25 26      17 18 19 20 21 22 23      21 22 23 24 25 26 27
    27 28 29 30 31            24 25 26 27 28 29 30      28 29 30
                              31
    
          October                   November                  December
    Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
              1  2  3  4                         1          1  2  3  4  5  6
     5  6  7  8  9 10 11       2  3  4  5  6  7  8       7  8  9 10 11 12 13
    12 13 14 15 16 17 18       9 10 11 12 13 14 15      14 15 16 17 18 19 20
    19 20 21 22 23 24 25      16 17 18 19 20 21 22      21 22 23 24 25 26 27
    26 27 28 29 30 31         23 24 25 26 27 28 29      28 29 30 31
                              30


## monthcalendar


```python
import calendar

calendar.monthcalendar(2020, 11)
```




    [[0, 0, 0, 0, 0, 0, 1],
     [2, 3, 4, 5, 6, 7, 8],
     [9, 10, 11, 12, 13, 14, 15],
     [16, 17, 18, 19, 20, 21, 22],
     [23, 24, 25, 26, 27, 28, 29],
     [30, 0, 0, 0, 0, 0, 0]]



> 長さは一ヶ月何週間あるのを示す  
> 月曜日は一週間のスタート  
> ない日は0で表示

## 週の始まりの曜日を設定


```python
import calendar

calendar.setfirstweekday(calendar.SUNDAY)
print(calendar.month(2020, 12))
```

       December 2020
    Su Mo Tu We Th Fr Sa
           1  2  3  4  5
     6  7  8  9 10 11 12
    13 14 15 16 17 18 19
    20 21 22 23 24 25 26
    27 28 29 30 31
    


## ロケールを変更して曜日の文字列を変更


```python
ltc_ja = calendar.LocaleTextCalendar(locale="ja_JP") # 全角文字の幅は考慮されておらず、日本語の場合はレイアウトが崩れてしまう
print(ltc_ja.formatmonth(2020, 11, w=4))
```

                 11月 2020
     月    火    水    木    金    土    日
                                    1
      2    3    4    5    6    7    8
      9   10   11   12   13   14   15
     16   17   18   19   20   21   22
     23   24   25   26   27   28   29
     30
    


## HTMLCalendar


```python
import calendar

c = calendar.HTMLCalendar()
print(c.formatmonth(2020, 12))
```

    <table border="0" cellpadding="0" cellspacing="0" class="month">
    <tr><th colspan="7" class="month">December 2020</th></tr>
    <tr><th class="mon">Mon</th><th class="tue">Tue</th><th class="wed">Wed</th><th class="thu">Thu</th><th class="fri">Fri</th><th class="sat">Sat</th><th class="sun">Sun</th></tr>
    <tr><td class="noday">&nbsp;</td><td class="tue">1</td><td class="wed">2</td><td class="thu">3</td><td class="fri">4</td><td class="sat">5</td><td class="sun">6</td></tr>
    <tr><td class="mon">7</td><td class="tue">8</td><td class="wed">9</td><td class="thu">10</td><td class="fri">11</td><td class="sat">12</td><td class="sun">13</td></tr>
    <tr><td class="mon">14</td><td class="tue">15</td><td class="wed">16</td><td class="thu">17</td><td class="fri">18</td><td class="sat">19</td><td class="sun">20</td></tr>
    <tr><td class="mon">21</td><td class="tue">22</td><td class="wed">23</td><td class="thu">24</td><td class="fri">25</td><td class="sat">26</td><td class="sun">27</td></tr>
    <tr><td class="mon">28</td><td class="tue">29</td><td class="wed">30</td><td class="thu">31</td><td class="noday">&nbsp;</td><td class="noday">&nbsp;</td><td class="noday">&nbsp;</td></tr>
    </table>
    


## タプルのリスト


```python
import calendar

c = calendar.TextCalendar()
c.monthdays2calendar(2020, 11) # 各タプルは(日付, 曜日)の値を持つ,存在しない日付は0
```




    [[(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (0, 5), (1, 6)],
     [(2, 0), (3, 1), (4, 2), (5, 3), (6, 4), (7, 5), (8, 6)],
     [(9, 0), (10, 1), (11, 2), (12, 3), (13, 4), (14, 5), (15, 6)],
     [(16, 0), (17, 1), (18, 2), (19, 3), (20, 4), (21, 5), (22, 6)],
     [(23, 0), (24, 1), (25, 2), (26, 3), (27, 4), (28, 5), (29, 6)],
     [(30, 0), (0, 1), (0, 2), (0, 3), (0, 4), (0, 5), (0, 6)]]




```python
c.yeardays2calendar(2020) # 年間
```




    [[[[(0, 0), (0, 1), (1, 2), (2, 3), (3, 4), (4, 5), (5, 6)],
       [(6, 0), (7, 1), (8, 2), (9, 3), (10, 4), (11, 5), (12, 6)],
       [(13, 0), (14, 1), (15, 2), (16, 3), (17, 4), (18, 5), (19, 6)],
       [(20, 0), (21, 1), (22, 2), (23, 3), (24, 4), (25, 5), (26, 6)],
       [(27, 0), (28, 1), (29, 2), (30, 3), (31, 4), (0, 5), (0, 6)]],
      [[(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (1, 5), (2, 6)],
       [(3, 0), (4, 1), (5, 2), (6, 3), (7, 4), (8, 5), (9, 6)],
       [(10, 0), (11, 1), (12, 2), (13, 3), (14, 4), (15, 5), (16, 6)],
       [(17, 0), (18, 1), (19, 2), (20, 3), (21, 4), (22, 5), (23, 6)],
       [(24, 0), (25, 1), (26, 2), (27, 3), (28, 4), (29, 5), (0, 6)]],
      [[(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (0, 5), (1, 6)],
       [(2, 0), (3, 1), (4, 2), (5, 3), (6, 4), (7, 5), (8, 6)],
       [(9, 0), (10, 1), (11, 2), (12, 3), (13, 4), (14, 5), (15, 6)],
       [(16, 0), (17, 1), (18, 2), (19, 3), (20, 4), (21, 5), (22, 6)],
       [(23, 0), (24, 1), (25, 2), (26, 3), (27, 4), (28, 5), (29, 6)],
       [(30, 0), (31, 1), (0, 2), (0, 3), (0, 4), (0, 5), (0, 6)]]],
     [[[(0, 0), (0, 1), (1, 2), (2, 3), (3, 4), (4, 5), (5, 6)],
       [(6, 0), (7, 1), (8, 2), (9, 3), (10, 4), (11, 5), (12, 6)],
       [(13, 0), (14, 1), (15, 2), (16, 3), (17, 4), (18, 5), (19, 6)],
       [(20, 0), (21, 1), (22, 2), (23, 3), (24, 4), (25, 5), (26, 6)],
       [(27, 0), (28, 1), (29, 2), (30, 3), (0, 4), (0, 5), (0, 6)]],
      [[(0, 0), (0, 1), (0, 2), (0, 3), (1, 4), (2, 5), (3, 6)],
       [(4, 0), (5, 1), (6, 2), (7, 3), (8, 4), (9, 5), (10, 6)],
       [(11, 0), (12, 1), (13, 2), (14, 3), (15, 4), (16, 5), (17, 6)],
       [(18, 0), (19, 1), (20, 2), (21, 3), (22, 4), (23, 5), (24, 6)],
       [(25, 0), (26, 1), (27, 2), (28, 3), (29, 4), (30, 5), (31, 6)]],
      [[(1, 0), (2, 1), (3, 2), (4, 3), (5, 4), (6, 5), (7, 6)],
       [(8, 0), (9, 1), (10, 2), (11, 3), (12, 4), (13, 5), (14, 6)],
       [(15, 0), (16, 1), (17, 2), (18, 3), (19, 4), (20, 5), (21, 6)],
       [(22, 0), (23, 1), (24, 2), (25, 3), (26, 4), (27, 5), (28, 6)],
       [(29, 0), (30, 1), (0, 2), (0, 3), (0, 4), (0, 5), (0, 6)]]],
     [[[(0, 0), (0, 1), (1, 2), (2, 3), (3, 4), (4, 5), (5, 6)],
       [(6, 0), (7, 1), (8, 2), (9, 3), (10, 4), (11, 5), (12, 6)],
       [(13, 0), (14, 1), (15, 2), (16, 3), (17, 4), (18, 5), (19, 6)],
       [(20, 0), (21, 1), (22, 2), (23, 3), (24, 4), (25, 5), (26, 6)],
       [(27, 0), (28, 1), (29, 2), (30, 3), (31, 4), (0, 5), (0, 6)]],
      [[(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (1, 5), (2, 6)],
       [(3, 0), (4, 1), (5, 2), (6, 3), (7, 4), (8, 5), (9, 6)],
       [(10, 0), (11, 1), (12, 2), (13, 3), (14, 4), (15, 5), (16, 6)],
       [(17, 0), (18, 1), (19, 2), (20, 3), (21, 4), (22, 5), (23, 6)],
       [(24, 0), (25, 1), (26, 2), (27, 3), (28, 4), (29, 5), (30, 6)],
       [(31, 0), (0, 1), (0, 2), (0, 3), (0, 4), (0, 5), (0, 6)]],
      [[(0, 0), (1, 1), (2, 2), (3, 3), (4, 4), (5, 5), (6, 6)],
       [(7, 0), (8, 1), (9, 2), (10, 3), (11, 4), (12, 5), (13, 6)],
       [(14, 0), (15, 1), (16, 2), (17, 3), (18, 4), (19, 5), (20, 6)],
       [(21, 0), (22, 1), (23, 2), (24, 3), (25, 4), (26, 5), (27, 6)],
       [(28, 0), (29, 1), (30, 2), (0, 3), (0, 4), (0, 5), (0, 6)]]],
     [[[(0, 0), (0, 1), (0, 2), (1, 3), (2, 4), (3, 5), (4, 6)],
       [(5, 0), (6, 1), (7, 2), (8, 3), (9, 4), (10, 5), (11, 6)],
       [(12, 0), (13, 1), (14, 2), (15, 3), (16, 4), (17, 5), (18, 6)],
       [(19, 0), (20, 1), (21, 2), (22, 3), (23, 4), (24, 5), (25, 6)],
       [(26, 0), (27, 1), (28, 2), (29, 3), (30, 4), (31, 5), (0, 6)]],
      [[(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (0, 5), (1, 6)],
       [(2, 0), (3, 1), (4, 2), (5, 3), (6, 4), (7, 5), (8, 6)],
       [(9, 0), (10, 1), (11, 2), (12, 3), (13, 4), (14, 5), (15, 6)],
       [(16, 0), (17, 1), (18, 2), (19, 3), (20, 4), (21, 5), (22, 6)],
       [(23, 0), (24, 1), (25, 2), (26, 3), (27, 4), (28, 5), (29, 6)],
       [(30, 0), (0, 1), (0, 2), (0, 3), (0, 4), (0, 5), (0, 6)]],
      [[(0, 0), (1, 1), (2, 2), (3, 3), (4, 4), (5, 5), (6, 6)],
       [(7, 0), (8, 1), (9, 2), (10, 3), (11, 4), (12, 5), (13, 6)],
       [(14, 0), (15, 1), (16, 2), (17, 3), (18, 4), (19, 5), (20, 6)],
       [(21, 0), (22, 1), (23, 2), (24, 3), (25, 4), (26, 5), (27, 6)],
       [(28, 0), (29, 1), (30, 2), (31, 3), (0, 4), (0, 5), (0, 6)]]]]



## datetime.dateのリスト


```python
import calendar

c = calendar.Calendar()
c.monthdatescalendar(2020, 12)
```




    [[datetime.date(2020, 11, 30),
      datetime.date(2020, 12, 1),
      datetime.date(2020, 12, 2),
      datetime.date(2020, 12, 3),
      datetime.date(2020, 12, 4),
      datetime.date(2020, 12, 5),
      datetime.date(2020, 12, 6)],
     [datetime.date(2020, 12, 7),
      datetime.date(2020, 12, 8),
      datetime.date(2020, 12, 9),
      datetime.date(2020, 12, 10),
      datetime.date(2020, 12, 11),
      datetime.date(2020, 12, 12),
      datetime.date(2020, 12, 13)],
     [datetime.date(2020, 12, 14),
      datetime.date(2020, 12, 15),
      datetime.date(2020, 12, 16),
      datetime.date(2020, 12, 17),
      datetime.date(2020, 12, 18),
      datetime.date(2020, 12, 19),
      datetime.date(2020, 12, 20)],
     [datetime.date(2020, 12, 21),
      datetime.date(2020, 12, 22),
      datetime.date(2020, 12, 23),
      datetime.date(2020, 12, 24),
      datetime.date(2020, 12, 25),
      datetime.date(2020, 12, 26),
      datetime.date(2020, 12, 27)],
     [datetime.date(2020, 12, 28),
      datetime.date(2020, 12, 29),
      datetime.date(2020, 12, 30),
      datetime.date(2020, 12, 31),
      datetime.date(2021, 1, 1),
      datetime.date(2021, 1, 2),
      datetime.date(2021, 1, 3)]]



## コマンドライン


```python
```python
>>> python3 -m calendar 2020 12
   December 2020
Mo Tu We Th Fr Sa Su
    1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30 31
```
```
