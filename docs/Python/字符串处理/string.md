```python
import string
```

## 字符串常量


```python
string.ascii_letters
```




    'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'




```python
string.punctuation
```




    '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'




```python
string.printable
```




    '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ \t\n\r\x0b\x0c'




```python
string.whitespace
```




    ' \t\n\r\x0b\x0c'



## 模版字符串


```python
from string import Template
s = Template("$I love $U")
s.substitute(I="mao", U="Ms.Right")
```


```python
d = dict(I="mao")
s.safe_substitute(d)
```

## 辅助函数
```python
string.capwords(s, sep=None) # 等价与 sep.join([x.capitalize() for x in str.split()])
```


```python
Zen = """
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
"""
```


```python
string.capwords(Zen)
```


```python
" ".join([ x.capitalize() for x in Zen.split("\n")])
```


```python

```
