```python
foo = "hello, world"
```


```python
[ e for e in dir(foo) if not e.startswith('_')]
```




    ['capitalize',
     'casefold',
     'center',
     'count',
     'encode',
     'endswith',
     'expandtabs',
     'find',
     'format',
     'format_map',
     'index',
     'isalnum',
     'isalpha',
     'isascii',
     'isdecimal',
     'isdigit',
     'isidentifier',
     'islower',
     'isnumeric',
     'isprintable',
     'isspace',
     'istitle',
     'isupper',
     'join',
     'ljust',
     'lower',
     'lstrip',
     'maketrans',
     'partition',
     'replace',
     'rfind',
     'rindex',
     'rjust',
     'rpartition',
     'rsplit',
     'rstrip',
     'split',
     'splitlines',
     'startswith',
     'strip',
     'swapcase',
     'title',
     'translate',
     'upper',
     'zfill']



[公式ドキュメント: string methods](https://docs.python.org/ja/3/library/stdtypes.html#string-methods)

## 大文字小文字変換


```python
print(f"{'abc XYZ'.lower()=}")
print(f"{'abc XYZ'.upper()=}")
print(f"{'abc XYZ'.title()=}")
print(f"{'abc XYZ'.capitalize()=}")
print(f"{'abc XYZ'.swapcase()=}")
print(f"{'abc XYZ'.casefold()=}")
```

    'abc XYZ'.lower()='abc xyz'
    'abc XYZ'.upper()='ABC XYZ'
    'abc XYZ'.title()='Abc Xyz'
    'abc XYZ'.capitalize()='Abc xyz'
    'abc XYZ'.swapcase()='ABC xyz'
    'abc XYZ'.casefold()='abc xyz'


## isXXX判断


```python
print(f"{'42xyz'.isalnum()=}")
print(f"{'google.com'.isalnum()=}")
```

    '42xyz'.isalnum()=True
    'google.com'.isalnum()=False



```python
print(f"{'abc'.isalpha()=}")
print(f"{'42'.isalpha()=}")
```

    'abc'.isalpha()=True
    '42'.isalpha()=False



```python
import string

print(f"{string.ascii_letters.isascii()=}")
print(f"{'うずまきナルト'.isascii()=}")
```

    string.ascii_letters.isascii()=True
    'うずまきナルト'.isascii()=False



```python
print(f"{'1234567890'.isdecimal()=}")
'\u00B2'.isdecimal() # ²
```

    '1234567890'.isdecimal()=True





    False




```python
print(f"{'1234567890ABCDEF'.isdigit()=}")
'\u00B2'.isdigit()
```

    '1234567890ABCDEF'.isdigit()=False





    True




```python
print(f"{'hello'.isidentifier()=}")
print(f"{'123hao'.isidentifier()=}")
```

    'hello'.isidentifier()=True
    '123hao'.isidentifier()=False



```python
print(f"{'普通の文字列の間にアルファベットがあったらislowerが認識する'.islower()=}")
print(f"{'この場合はFalseね'.islower()=}")
print(f"{'同じくISUPPERメソッドも'.isupper()=}")
print(f"{'これはFalseになる'.isupper()=}")
print(f"{'istitleをテストしてみよう'.istitle()=}")
print(f"{'Falseちょうどタイトルの形'.istitle()=}")

```

    '普通の文字列の間にアルファベットがあったらislowerが認識する'.islower()=True
    'この場合はFalseね'.islower()=False
    '同じくISUPPERメソッドも'.isupper()=True
    'これはFalseになる'.isupper()=False
    'istitleをテストしてみよう'.istitle()=False
    'Falseちょうどタイトルの形'.istitle()=True



```python
#s = '²3455'
s = '\u00B23455'
print(s.isnumeric())
# s = '½'
s = '\u00BD'
print(s.isnumeric())

a = "\u0030" #unicode for 0
print(a.isnumeric())

b = "\u00B2" #unicode for ²
print(b.isnumeric())

c = "10km2"
print(c.isnumeric())
```

    True
    True
    True
    True
    False


### s.isdigit、isdecimal と s.isnumeric の違い

* `isdigit()`

    - True: Unicode数字，byte数字（1 Byte），全角数字（2 Bytes）
    - False: 漢字の数字，ローマ数字，小数
    - Error: 無し

* `isdecimal()`

    - True: Unicode数字，，全角数字（2 Bytes）
    - False: ローマ数字，漢字の数字，小数
    - Error: byte数字（1 Byte）

* `isnumeric()`

    - True: Unicode 数字，全角数字（2 Bytes），漢字の数字
    - False: 小数，ローマ数字
    - Error: byte数字（1 Byte）


```python
num = "\u00BD"  #unicode
print(f"{num=}")
print(f"{num.isdigit()=}")   # True
print(f"{num.isdecimal()=}") # True
print(f"{num.isnumeric()=}") # True

num = "1" # 全角
print(f"{num=}")
print(f"{num.isdigit()=}")   # True
print(f"{num.isdecimal()=}") # True
print(f"{num.isnumeric()=}") # True

num = b"1" # byte
print(f"{num=}")
print(f"{num.isdigit()=}")   # True
# num.isdecimal() # AttributeError 'bytes' object has no attribute 'isdecimal'
# num.isnumeric() # AttributeError 'bytes' object has no attribute 'isnumeric'

num = "IV" # ローマ数字
print(f"{num=}")
print(f"{num.isdigit()=}")   # False
print(f"{num.isdecimal()=}") # False
print(f"{num.isnumeric()=}") # False

num = "四" # 漢字
print(f"{num=}")
print(f"{num.isdigit()=}")   # False
print(f"{num.isdecimal()=}") # False
print(f"{num.isnumeric()=}") # True
```

    num='½'
    num.isdigit()=False
    num.isdecimal()=False
    num.isnumeric()=True
    num='1'
    num.isdigit()=True
    num.isdecimal()=True
    num.isnumeric()=True
    num=b'1'
    num.isdigit()=True
    num='IV'
    num.isdigit()=False
    num.isdecimal()=False
    num.isnumeric()=False
    num='四'
    num.isdigit()=False
    num.isdecimal()=False
    num.isnumeric()=True


[Unicode Separator](https://www.compart.com/en/unicode/category/Zs)


```python
'\u2028'.isprintable()
```




    False




```python
'   '.isspace()
```




    True



## 分割


```python
print('Hello, world!'.partition('w'))
print('Hello, world!'.partition('world'))
print('Hello, world!'.partition('o'))
print('Hello, world!'.rpartition('o'))
print('Hello, world!'.partition('XYZ'))
```

    ('Hello, ', 'w', 'orld!')
    ('Hello, ', 'world', '!')
    ('Hell', 'o', ', world!')
    ('Hello, w', 'o', 'rld!')
    ('Hello, world!', '', '')



```python
before, sep, after = 'Hello, world!'.partition(' ')
print(f'{before=} {sep=} {after=}')
```

    before='Hello,' sep=' ' after='world!'



```python
print(f"{'月,火,水,木,金,土,日'.split(',')=}")
print(f"{'月,火,水,木,金,土,日'.split(',', 1)=}")
```

    '月,火,水,木,金,土,日'.split(',')=['月', '火', '水', '木', '金', '土', '日']
    '月,火,水,木,金,土,日'.split(',', 1)=['月', '火,水,木,金,土,日']



```python
"<hello><><world>".split("<>")
```




    ['<hello>', '<world>']




```python
"ab c\n\nde fg\rkl\r\n".splitlines()
```




    ['ab c', '', 'de fg', 'kl']




```python
"ab c\n\nde fg\rkl\r\n".splitlines(keepends=True)
```




    ['ab c\n', '\n', 'de fg\r', 'kl\r\n']



## 組み合わせ


```python
print(f"{'_'.join('python')=}")
print(f"{'_'.join(('1', '2' ,'3'))=}")
print(f"{'_'.join(set('python'))=}")
print(f"{'_'.join(['py', 't', 'h', 'on'])=}")
print(f"{'_'.join({'name': 'python', 'age': 29})=}")
```

    '_'.join('python')='p_y_t_h_o_n'
    '_'.join(('1', '2' ,'3'))='1_2_3'
    '_'.join(set('python'))='o_n_h_p_t_y'
    '_'.join(['py', 't', 'h', 'on'])='py_t_h_on'
    '_'.join({'name': 'python', 'age': 29})='name_age'



```python
# joinのパラメータは文字列が必要
"_".join((1, 2, 3))
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-22-2b5a4c7dccb5> in <module>
          1 # joinのパラメータは文字列が必要
    ----> 2 "_".join((1, 2, 3))
    

    TypeError: sequence item 0: expected str instance, int found


## padding


```python
print(f"{'Hello'.ljust(20, '*')=}")
print(f"{'Hello'.rjust(20, '-')=}")
print(f"{'Hello'.center(20, '=')=}")
```

    'Hello'.ljust(20, '*')='Hello***************'
    'Hello'.rjust(20, '-')='---------------Hello'
    'Hello'.center(20, '=')='=======Hello========'



```python
print(f"{'Hello'.ljust(3, '*')=}")
print(f"{'Hello'.rjust(3, '-')=}")
print(f"{'Hello'.center(3, '=')=}")
```

    'Hello'.ljust(3, '*')='Hello'
    'Hello'.rjust(3, '-')='Hello'
    'Hello'.center(3, '=')='Hello'



```python
print(f"{'abc'.zfill(5)=}")
print(f"{'-abc'.zfill(5)=}")
print(f"{'+abc'.zfill(5)=}")
print(f"{'42'.zfill(5)=}")
print(f"{'-42'.zfill(5)=}")
print(f"{'+42'.zfill(5)=}")
```

    'abc'.zfill(5)='00abc'
    '-abc'.zfill(5)='-0abc'
    '+abc'.zfill(5)='+0abc'
    '42'.zfill(5)='00042'
    '-42'.zfill(5)='-0042'
    '+42'.zfill(5)='+0042'


## 刈り込む


```python
spam = '  Hello, World  '
print(f'{spam.strip()=}')
print(f'{spam.lstrip()=}')
print(f'{spam.rstrip()=}')
```

    spam.strip()='Hello, World'
    spam.lstrip()='Hello, World  '
    spam.rstrip()='  Hello, World'



```python
spam = 'SpamSpamBaconSpamEggsSpamSpam'
spam.strip('ampS')
```




    'BaconSpamEggs'



## 探索


```python
print(f"{'abcxyz'.endswith('xyz')=}")
print(f"{'abcxyz'.endswith('xyz', 4)=}")
print(f"{'abcxyz'.endswith('xyz', 0, 5)=}")
print(f"{'abcxyz'.endswith('xyz', 0, 6)=}")
```

    'abcxyz'.endswith('xyz')=True
    'abcxyz'.endswith('xyz', 4)=False
    'abcxyz'.endswith('xyz', 0, 5)=False
    'abcxyz'.endswith('xyz', 0, 6)=True



```python
print(f"{'abcxyz'.startswith(('xyz', 'abc'))=}")

```

    'abcxyz'.startswith(('xyz', 'abc'))=True



```python
print(f"{'xy' in 'abxycd'=}")
```

    'xy' in 'abxycd'=True



```python
print(f"{'abcxyzXY'.find('xy')=}")
print(f"{'abcxyzXY'.find('xy', 4)=}")
print(f"{'abcxyzXY'.find('Xy')=}")
```

    'abcxyzXY'.find('xy')=3
    'abcxyzXY'.find('xy', 4)=-1
    'abcxyzXY'.find('Xy')=-1



```python
print(f"{'abcxyzabc'.find('abc')=}")
print(f"{'abcxyzabc'.rfind('abc')=}")

```

    'abcxyzabc'.find('abc')=0
    'abcxyzabc'.rfind('abc')=6


## 入れ替え


```python
print(f"{'abcxyzoxy'.replace('xy', 'XY')=}")
print(f"{'abcxyzoxy'.replace('xy', 'XY', 1)=}")
print(f"{'abcxyzoxy'.replace('mn', 'XY', 1)=}")
```

    'abcxyzoxy'.replace('xy', 'XY')='abcXYzoXY'
    'abcxyzoxy'.replace('xy', 'XY', 1)='abcXYzoxy'
    'abcxyzoxy'.replace('mn', 'XY', 1)='abcxyzoxy'



```python
'01\t012\t0123\t01234'.expandtabs(4) # 2 1 4
```




    '01  012 0123    01234'




```python
'01\t012\t0123\t01234'.expandtabs(8) # 6 5 4
```




    '01      012     0123    01234'




```python
input = string.ascii_letters
output = input[5:] + input[:5]

map_table = str.maketrans(input, output)

'I love You'.translate(map_table)
```




    'N qtAj dtz'



## Format


```python
"The sum of 1 + 2 is {0}".format(1 + 2)
```




    'The sum of 1 + 2 is 3'



[書式指定文字列の文法](https://docs.python.org/ja/3/library/string.html#formatstrings)


```python
format_spec     ::=  [[fill]align][sign][#][0][width][grouping_option][.precision][type]
fill            ::=  <any character>
align           ::=  "<" | ">" | "=" | "^"
sign            ::=  "+" | "-" | " "
width           ::=  digit+
grouping_option ::=  "_" | ","
precision       ::=  digit+
type            ::=  "b" | "c" | "d" | "e" | "E" | "f" | "F" | "g" | "G" | "n" | "o" | "s" | "x" | "X" | "%"
```


```python
ip_address = [int(x) for x in "178.124.155.13".split(".")]
"{:02X} {:02X} {:02X} {:02X}".format(*ip_address)
```




    'B2 7C 9B 0D'



## ClipBoard

pip install pyperclip


```python
import pyperclip

```


```python
pyperclip.copy('Hello, World')
pyperclip.paste()
```




    'Hello, World'




```python

```
