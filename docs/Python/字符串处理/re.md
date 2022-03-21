参考資料
* [PyMOTW](https://pymotw.com/3/re/index.html)
* [正規表現HOWTO](https://docs.python.org/ja/3/howto/regex.html)
* [re](https://docs.python.org/ja/3/library/re.html)
* [Pythonの正規表現モジュールreの使い方](https://note.nkmk.me/python-re-match-search-findall-etc/)
* [前提知識](https://github.com/ziishaned/learn-regex/blob/master/translations/README-ja.md)

## search()


```python
import re

pattern = 'this'
text = 'Does this text match the pattern?'

match = re.search(pattern, text) # 見つからない場合は、Noneを戻す

s = match.start()
e = match.end()

print(f'Found "{match.re.pattern}"\n',
      f'in "{match.string}"\n', # 元の情報を持っている
      f'from {s} to {e} ("{text[s:e]}")')
```

    Found "this"
     in "Does this text match the pattern?"
     from 5 to 9 ("this")


## compile()


```python
import re

# パターンを事前にコンパイルする
regexes = [
    re.compile(p) # RegexObject
    for p in ['this', 'that']
]
text = 'Does this text match the pattern?'

print(f'Text: {text!r}\n')

for regex in regexes:
    print(f'Seeking "{regex.pattern}" ->', end=' ')

    if regex.search(text):
        print('match!')
    else:
        print('no match')
```

    Text: 'Does this text match the pattern?'
    
    Seeking "this" -> match!
    Seeking "that" -> no match


## findall()


```python
import re

text = 'abbaaabbbbaaaaa'

pattern = 'ab'

for match in re.findall(pattern, text):
    print(f'Found {match!r}')
```

    Found 'ab'
    Found 'ab'


## finditer()


```python
import re

text = 'abbaaabbbbaaaaa'

pattern = 'ab'

for match in re.finditer(pattern, text):
    s = match.start()
    e = match.end()
    print(f'Found {text[s:e]!r} at {s}:{e}')
```

    Found 'ab' at 0:2
    Found 'ab' at 5:7


## パターンの文法

### 重複


```python
def test_patterns(text, patterns):
    """テキストからパターンに合わせるものをサーチして出力する"""
    for pattern, desc in patterns:
        print(f"'{pattern}' ({desc})\n")
        print(f"  '{text}'")
        for match in re.finditer(pattern, text):
            s = match.start()
            e = match.end()
            substr = text[s:e]
            n_backslashes = text[:s].count('\\')
            prefix = '.' * (s + n_backslashes)
            print(f"  {prefix}'{substr}'")
        print()
    return


test_patterns(
    'abbaabbba',
    [('ab*', 'a followed by zero or more b'),
     ('ab+', 'a followed by one or more b'),
     ('ab?', 'a followed by zero or one b'),
     ('ab{3}', 'a followed by three b'),
     ('ab{2,3}', 'a followed by two to three b')],
)
```

    'ab*' (a followed by zero or more b)
    
      'abbaabbba'
      'abb'
      ...'a'
      ....'abbb'
      ........'a'
    
    'ab+' (a followed by one or more b)
    
      'abbaabbba'
      'abb'
      ....'abbb'
    
    'ab?' (a followed by zero or one b)
    
      'abbaabbba'
      'ab'
      ...'a'
      ....'ab'
      ........'a'
    
    'ab{3}' (a followed by three b)
    
      'abbaabbba'
      ....'abbb'
    
    'ab{2,3}' (a followed by two to three b)
    
      'abbaabbba'
      'abb'
      ....'abbb'
    



```python
# 非貪欲版
test_patterns(
    'abbaabbba',
    [('ab*?', 'a followed by zero or more b'),
     ('ab+?', 'a followed by one or more b'),
     ('ab??', 'a followed by zero or one b'),
     ('ab{3}?', 'a followed by three b'),
     ('ab{2,3}?', 'a followed by two to three b')],
)
```

    'ab*?' (a followed by zero or more b)
    
      'abbaabbba'
      'a'
      ...'a'
      ....'a'
      ........'a'
    
    'ab+?' (a followed by one or more b)
    
      'abbaabbba'
      'ab'
      ....'ab'
    
    'ab??' (a followed by zero or one b)
    
      'abbaabbba'
      'a'
      ...'a'
      ....'a'
      ........'a'
    
    'ab{3}?' (a followed by three b)
    
      'abbaabbba'
      ....'abbb'
    
    'ab{2,3}?' (a followed by two to three b)
    
      'abbaabbba'
      'abb'
      ....'abb'
    


### 文字セット


```python
test_patterns(
    'abbaabbba',
    [('[ab]', 'either a or b'),
     ('a[ab]+', 'a followed by 1 or more a or b'),
     ('a[ab]+?', 'a followed by 1 or more a or b, not greedy')],
)
```

    '[ab]' (either a or b)
    
      'abbaabbba'
      'a'
      .'b'
      ..'b'
      ...'a'
      ....'a'
      .....'b'
      ......'b'
      .......'b'
      ........'a'
    
    'a[ab]+' (a followed by 1 or more a or b)
    
      'abbaabbba'
      'abbaabbba'
    
    'a[ab]+?' (a followed by 1 or more a or b, not greedy)
    
      'abbaabbba'
      'ab'
      ...'aa'
    



```python
test_patterns(
    'This is some text -- with punctuation.',
    [('[^-. ]+', 'sequences without -, ., or space')],
)
```

    '[^-. ]+' (sequences without -, ., or space)
    
      'This is some text -- with punctuation.'
      'This'
      .....'is'
      ........'some'
      .............'text'
      .....................'with'
      ..........................'punctuation'
    



```python
test_patterns(
    'This is some text -- with punctuation.',
    [('[a-z]+', 'sequences of lowercase letters'),
     ('[A-Z]+', 'sequences of uppercase letters'),
     ('[a-zA-Z]+', 'sequences of letters of either case'),
     ('[A-Z][a-z]+', 'one uppercase followed by lowercase')],
)
```

    '[a-z]+' (sequences of lowercase letters)
    
      'This is some text -- with punctuation.'
      .'his'
      .....'is'
      ........'some'
      .............'text'
      .....................'with'
      ..........................'punctuation'
    
    '[A-Z]+' (sequences of uppercase letters)
    
      'This is some text -- with punctuation.'
      'T'
    
    '[a-zA-Z]+' (sequences of letters of either case)
    
      'This is some text -- with punctuation.'
      'This'
      .....'is'
      ........'some'
      .............'text'
      .....................'with'
      ..........................'punctuation'
    
    '[A-Z][a-z]+' (one uppercase followed by lowercase)
    
      'This is some text -- with punctuation.'
      'This'
    



```python
test_patterns(
    'abbaabbba',
    [('a.', 'a followed by any one character'),
     ('b.', 'b followed by any one character'),
     ('a.*b', 'a followed by anything, ending in b'),
     ('a.*?b', 'a followed by anything, ending in b')],
)
```

    'a.' (a followed by any one character)
    
      'abbaabbba'
      'ab'
      ...'aa'
    
    'b.' (b followed by any one character)
    
      'abbaabbba'
      .'bb'
      .....'bb'
      .......'ba'
    
    'a.*b' (a followed by anything, ending in b)
    
      'abbaabbba'
      'abbaabbb'
    
    'a.*?b' (a followed by anything, ending in b)
    
      'abbaabbba'
      'ab'
      ...'aab'
    


### エスケープコード

|コード|意味|
| --- | --- |
|\d|数字|
|\D|数字以外|
|\s|ホワイトスペース|
|\S|ホワイトスペース以外|
|\w|アルファベットと数字|
|\W|アルファベットと数字以外|


```python
test_patterns(
    'A prime #1 example!',
    [(r'\d+', 'sequence of digits'),
     (r'\D+', 'sequence of non-digits'),
     (r'\s+', 'sequence of whitespace'),
     (r'\S+', 'sequence of non-whitespace'),
     (r'\w+', 'alphanumeric characters'),
     (r'\W+', 'non-alphanumeric')],
)
```

    '\d+' (sequence of digits)
    
      'A prime #1 example!'
      .........'1'
    
    '\D+' (sequence of non-digits)
    
      'A prime #1 example!'
      'A prime #'
      ..........' example!'
    
    '\s+' (sequence of whitespace)
    
      'A prime #1 example!'
      .' '
      .......' '
      ..........' '
    
    '\S+' (sequence of non-whitespace)
    
      'A prime #1 example!'
      'A'
      ..'prime'
      ........'#1'
      ...........'example!'
    
    '\w+' (alphanumeric characters)
    
      'A prime #1 example!'
      'A'
      ..'prime'
      .........'1'
      ...........'example'
    
    '\W+' (non-alphanumeric)
    
      'A prime #1 example!'
      .' '
      .......' #'
      ..........' '
      ..................'!'
    



```python
test_patterns(
    r'\d+ \D+ \s+',
    [(r'\\.\+', 'escape code')],
)
```

    '\\.\+' (escape code)
    
      '\d+ \D+ \s+'
      '\d+'
      .....'\D+'
      ..........'\s+'
    


### 定着

|コード|意味|
| --- | --- |
| ^ | 文字列や一行のスタート |
| $ | 文字列や一行のエンド |
| \A | 文字列のスタート |
| \Z | 文字列のエンド |
| \b | 単語の先頭か末尾の空文字列 |
| \B | 単語の先頭か末尾以外の空文字列 |


```python
test_patterns(
    'This is some text -- with punctuation.',
    [(r'^\w+', 'word at start of string'),
     (r'\A\w+', 'word at start of string'),
     (r'\w+\S*$', 'word near end of string'),
     (r'\w+\S*\Z', 'word near end of string'),
     (r'\w*t\w*', 'word containing t'),
     (r'\bt\w+', 't at start of word'),
     (r'\w+t\b', 't at end of word'),
     (r'\Bt\B', 't, not start or end of word')],
)
```

    '^\w+' (word at start of string)
    
      'This is some text -- with punctuation.'
      'This'
    
    '\A\w+' (word at start of string)
    
      'This is some text -- with punctuation.'
      'This'
    
    '\w+\S*$' (word near end of string)
    
      'This is some text -- with punctuation.'
      ..........................'punctuation.'
    
    '\w+\S*\Z' (word near end of string)
    
      'This is some text -- with punctuation.'
      ..........................'punctuation.'
    
    '\w*t\w*' (word containing t)
    
      'This is some text -- with punctuation.'
      .............'text'
      .....................'with'
      ..........................'punctuation'
    
    '\bt\w+' (t at start of word)
    
      'This is some text -- with punctuation.'
      .............'text'
    
    '\w+t\b' (t at end of word)
    
      'This is some text -- with punctuation.'
      .............'text'
    
    '\Bt\B' (t, not start or end of word)
    
      'This is some text -- with punctuation.'
      .......................'t'
      ..............................'t'
      .................................'t'
    


## Groups


```python
test_patterns(
    'abbaaabbbbaaaaa',
    [('a(ab)', 'a followed by literal ab'),
     ('a(a*b*)', 'a followed by 0-n a and 0-n b'),
     ('a(ab)*', 'a followed by 0-n ab'),
     ('a(ab)+', 'a followed by 1-n ab')],
)
```

    'a(ab)' (a followed by literal ab)
    
      'abbaaabbbbaaaaa'
      ....'aab'
    
    'a(a*b*)' (a followed by 0-n a and 0-n b)
    
      'abbaaabbbbaaaaa'
      'abb'
      ...'aaabbbb'
      ..........'aaaaa'
    
    'a(ab)*' (a followed by 0-n ab)
    
      'abbaaabbbbaaaaa'
      'a'
      ...'a'
      ....'aab'
      ..........'a'
      ...........'a'
      ............'a'
      .............'a'
      ..............'a'
    
    'a(ab)+' (a followed by 1-n ab)
    
      'abbaaabbbbaaaaa'
      ....'aab'
    



```python
import re

text = 'This is some text -- with punctuation.'

print(text)
print()

patterns = [
    (r'^(\w+)', 'word at start of string'),
    (r'(\w+)\S*$', 'word at end, with optional punctuation'),
    (r'(\bt\w+)\W+(\w+)', 'word starting with t, another word'),
    (r'(\w+t)\b', 'word ending with t'),
]

for pattern, desc in patterns:
    regex = re.compile(pattern)
    match = regex.search(text)
    print(f"'{pattern}' ({desc})\n")
    print('  ', match.groups())
    print()
```

    This is some text -- with punctuation.
    
    '^(\w+)' (word at start of string)
    
       ('This',)
    
    '(\w+)\S*$' (word at end, with optional punctuation)
    
       ('punctuation',)
    
    '(\bt\w+)\W+(\w+)' (word starting with t, another word)
    
       ('text', 'with')
    
    '(\w+t)\b' (word ending with t)
    
       ('text',)
    



```python
import re

text = 'This is some text -- with punctuation.'

print('Input text            :', text)

regex = re.compile(r'(\bt\w+)\W+(\w+)')
print('Pattern               :', regex.pattern)

match = regex.search(text)
print('Entire match          :', match.group(0))
print('Word starting with "t":', match.group(1))
print('Word after "t" word   :', match.group(2))
```

    Input text            : This is some text -- with punctuation.
    Pattern               : (\bt\w+)\W+(\w+)
    Entire match          : text -- with
    Word starting with "t": text
    Word after "t" word   : with



```python
import re

text = 'This is some text -- with punctuation.'

print(text)
print()

patterns = [
    r'^(?P<first_word>\w+)',
    r'(?P<last_word>\w+)\S*$',
    r'(?P<t_word>\bt\w+)\W+(?P<other_word>\w+)',
    r'(?P<ends_with_t>\w+t)\b',
]

for pattern in patterns:
    regex = re.compile(pattern)
    match = regex.search(text)
    print(f"'{pattern}'")
    print('  ', match.groups())
    print('  ', match.groupdict())
    print()
```

    This is some text -- with punctuation.
    
    '^(?P<first_word>\w+)'
       ('This',)
       {'first_word': 'This'}
    
    '(?P<last_word>\w+)\S*$'
       ('punctuation',)
       {'last_word': 'punctuation'}
    
    '(?P<t_word>\bt\w+)\W+(?P<other_word>\w+)'
       ('text', 'with')
       {'t_word': 'text', 'other_word': 'with'}
    
    '(?P<ends_with_t>\w+t)\b'
       ('text',)
       {'ends_with_t': 'text'}
    



```python
def test_patterns(text, patterns):
    """テキストからパターンに合わせるものをサーチして出力する"""
    for pattern, desc in patterns:
        print(f'{pattern!r} ({desc})\n')
        print(f'  {text!r}')
        for match in re.finditer(pattern, text):
            s = match.start()
            e = match.end()
            prefix = ' ' * (s)
            print(
                f'  {prefix}{text[s:e]!r}{" " * (len(text) - e)} ',
                end=' ',
            )
            print(match.groups())
            if match.groupdict():
                print(f'{" " * (len(text) - s)}{match.groupdict()}')
        print()
    return
```


```python
test_patterns(
    'abbaabbba',
    [(r'a((a*)(b*))', 'a followed by 0-n a and 0-n b')],
)
```

    'a((a*)(b*))' (a followed by 0-n a and 0-n b)
    
      'abbaabbba'
      'abb'        ('bb', '', 'bb')
         'aabbb'   ('abbb', 'a', 'bbb')
              'a'  ('', '', '')
    



```python
test_patterns(
    'abbaabbba',
    [(r'a((a+)|(b+))', 'a then seq. of a or seq. of b'),
     (r'a((a|b)+)', 'a then seq. of [ab]')],
)
```

    'a((a+)|(b+))' (a then seq. of a or seq. of b)
    
      'abbaabbba'
      'abb'        ('bb', None, 'bb')
         'aa'      ('a', 'a', None)
    
    'a((a|b)+)' (a then seq. of [ab])
    
      'abbaabbba'
      'abbaabbba'  ('bbaabbba', 'a')
    



```python
test_patterns(
    'abbaabbba',
    [(r'a((a+)|(b+))', 'capturing form'),
     (r'a((?:a+)|(?:b+))', 'noncapturing')],
)
```

    'a((a+)|(b+))' (capturing form)
    
      'abbaabbba'
      'abb'        ('bb', None, 'bb')
         'aa'      ('a', 'a', None)
    
    'a((?:a+)|(?:b+))' (noncapturing)
    
      'abbaabbba'
      'abb'        ('bb',)
         'aa'      ('a',)
    


## サーチの選択肢

### 大文字小文字非敏感


```python
import re

text = 'This is some text -- with punctuation.'
pattern = r'\bT\w+'
with_case = re.compile(pattern)
without_case = re.compile(pattern, re.IGNORECASE)

print(f'Text:\n  {text!r}')
print(f'Pattern:\n  {pattern}')
print('Case-sensitive:')
for match in with_case.findall(text):
    print(f'  {match!r}')
print('Case-insensitive:')
for match in without_case.findall(text):
    print(f'  {match!r}')
```

    Text:
      'This is some text -- with punctuation.'
    Pattern:
      \bT\w+
    Case-sensitive:
      'This'
    Case-insensitive:
      'This'
      'text'


### 複数行


```python
import re

text = 'This is some text -- with punctuation.\nA second line.'
pattern = r'(^\w+)|(\w+\S*$)'
single_line = re.compile(pattern)
multiline = re.compile(pattern, re.MULTILINE)

print(f'Text:\n  {text!r}')
print(f'Pattern:\n  {pattern}')
print('Single Line :')
for match in single_line.findall(text):
    print(f'  {match!r}')
print('Multline    :')
for match in multiline.findall(text):
    print(f'  {match!r}')
```

    Text:
      'This is some text -- with punctuation.\nA second line.'
    Pattern:
      (^\w+)|(\w+\S*$)
    Single Line :
      ('This', '')
      ('', 'line.')
    Multline    :
      ('This', '')
      ('', 'punctuation.')
      ('A', '')
      ('', 'line.')



```python
import re

text = 'This is some text -- with punctuation.\nA second line.'
pattern = r'.+'
no_newlines = re.compile(pattern)
dotall = re.compile(pattern, re.DOTALL)

print(f'Text:\n  {text!r}')
print(f'Pattern:\n  {pattern}')
print('No newlines :')
for match in no_newlines.findall(text):
    print(f'  {match!r}')
print('Dotall      :')
for match in dotall.findall(text):
    print(f'  {match!r}')
```

    Text:
      'This is some text -- with punctuation.\nA second line.'
    Pattern:
      .+
    No newlines :
      'This is some text -- with punctuation.'
      'A second line.'
    Dotall      :
      'This is some text -- with punctuation.\nA second line.'


### Unicode


```python
import re

text = u'Français złoty Österreich'
pattern = r'\w+'
ascii_pattern = re.compile(pattern, re.ASCII)
unicode_pattern = re.compile(pattern)

print('Text    :', text)
print('Pattern :', pattern)
print('ASCII   :', list(ascii_pattern.findall(text)))
print('Unicode :', list(unicode_pattern.findall(text)))
```

    Text    : Français złoty Österreich
    Pattern : \w+
    ASCII   : ['Fran', 'ais', 'z', 'oty', 'sterreich']
    Unicode : ['Français', 'złoty', 'Österreich']


### 冗長な表現


```python
import re

address = re.compile('[\w\d.+-]+@([\w\d.]+\.)+(com|org|edu)')

candidates = [
    'first.last@example.com',
    'first.last+category@gmail.com',
    'valid-address@mail.example.com',
    'not-valid@example.foo',
]

for candidate in candidates:
    match = address.search(candidate)
    print(f"{candidate:<30}  {'Matches' if match else 'No match'}")
```

    first.last@example.com          Matches
    first.last+category@gmail.com   Matches
    valid-address@mail.example.com  Matches
    not-valid@example.foo           No match



```python
import re

address = re.compile(
    '''
    [\w\d.+-]+       # username
    @
    ([\w\d.]+\.)+    # domain name prefix
    (com|org|edu)    # TODO: support more top-level domains
    ''',
    re.VERBOSE)

candidates = [
    'first.last@example.com',
    'first.last+category@gmail.com',
    'valid-address@mail.example.com',
    'not-valid@example.foo',
]

for candidate in candidates:
    match = address.search(candidate)
    print(f"{candidate:<30}  {'Matches' if match else 'No match'}")
```

    first.last@example.com          Matches
    first.last+category@gmail.com   Matches
    valid-address@mail.example.com  Matches
    not-valid@example.foo           No match



```python
import re

address = re.compile(
    '''

    # A name is made up of letters, and may include "."
    # for title abbreviations and middle initials.
    ((?P<name>
       ([\w.,]+\s+)*[\w.,]+)
       \s*
       # Email addresses are wrapped in angle
       # brackets < >, but only if a name is
       # found, so keep the start bracket in this
       # group.
       <
    )? # the entire name is optional

    # The address itself: username@domain.tld
    (?P<email>
      [\w\d.+-]+       # username
      @
      ([\w\d.]+\.)+    # domain name prefix
      (com|org|edu)    # limit the allowed top-level domains
    )

    >? # optional closing angle bracket
    ''',
    re.VERBOSE)

candidates = [
    'first.last@example.com',
    'first.last+category@gmail.com',
    'valid-address@mail.example.com',
    'not-valid@example.foo',
    'First Last <first.last@example.com>',
    'No Brackets first.last@example.com',
    'First Last',
    'First Middle Last <first.last@example.com>',
    'First M. Last <first.last@example.com>',
    '<first.last@example.com>',
]

for candidate in candidates:
    print('Candidate:', candidate)
    match = address.search(candidate)
    if match:
        print('  Name :', match.groupdict()['name'])
        print('  Email:', match.groupdict()['email'])
    else:
        print('  No match')
```

    Candidate: first.last@example.com
      Name : None
      Email: first.last@example.com
    Candidate: first.last+category@gmail.com
      Name : None
      Email: first.last+category@gmail.com
    Candidate: valid-address@mail.example.com
      Name : None
      Email: valid-address@mail.example.com
    Candidate: not-valid@example.foo
      No match
    Candidate: First Last <first.last@example.com>
      Name : First Last
      Email: first.last@example.com
    Candidate: No Brackets first.last@example.com
      Name : None
      Email: first.last@example.com
    Candidate: First Last
      No match
    Candidate: First Middle Last <first.last@example.com>
      Name : First Middle Last
      Email: first.last@example.com
    Candidate: First M. Last <first.last@example.com>
      Name : First M. Last
      Email: first.last@example.com
    Candidate: <first.last@example.com>
      Name : None
      Email: first.last@example.com


### フラグを埋める


```python
import re

text = 'This is some text -- with punctuation.'
pattern = r'(?i)\bT\w+'
regex = re.compile(pattern)

print('Text      :', text)
print('Pattern   :', pattern)
print('Matches   :', regex.findall(text))
```

    Text      : This is some text -- with punctuation.
    Pattern   : (?i)\bT\w+
    Matches   : ['This', 'text']


|フラグ|略称|
| --- | --- |
| ASCII | a |
| IGNORECASE | i |
| MULTILINE | m |
| DOTALL | s |
| VERBOSE | x |

## 自己言及


```python
import re

address = re.compile(
    r'''

    # The regular name
    (\w+)               # first name
    \s+
    (([\w.]+)\s+)?      # optional middle name or initial
    (\w+)               # last name

    \s+

    <

    # The address: first_name.last_name@domain.tld
    (?P<email>
      \1               # first name
      \.
      \4               # last name
      @
      ([\w\d.]+\.)+    # domain name prefix
      (com|org|edu)    # limit the allowed top-level domains
    )

    >
    ''',
    re.VERBOSE | re.IGNORECASE)

candidates = [
    'First Last <first.last@example.com>',
    'Different Name <first.last@example.com>',
    'First Middle Last <first.last@example.com>',
    'First M. Last <first.last@example.com>',
]

for candidate in candidates:
    print('Candidate:', candidate)
    match = address.search(candidate)
    if match:
        print('  Match name :', match.group(1), match.group(4))
        print('  Match email:', match.group(5))
    else:
        print('  No match')
```

    Candidate: First Last <first.last@example.com>
      Match name : First Last
      Match email: first.last@example.com
    Candidate: Different Name <first.last@example.com>
      No match
    Candidate: First Middle Last <first.last@example.com>
      Match name : First Last
      Match email: first.last@example.com
    Candidate: First M. Last <first.last@example.com>
      Match name : First Last
      Match email: first.last@example.com


## 文字列を修正


```python
import re

bold = re.compile(r'\*{2}(.*?)\*{2}')

text = 'Make this **bold**.  This **too**.'

print('Text:', text)
print('Bold:', bold.sub(r'<b>\1</b>', text))
```

    Text: Make this **bold**.  This **too**.
    Bold: Make this <b>bold</b>.  This <b>too</b>.



```python
import re

bold = re.compile(r'\*{2}(?P<bold_text>.*?)\*{2}')

text = 'Make this **bold**.  This **too**.'

print('Text:', text)
print('Bold:', bold.sub(r'<b>\g<bold_text></b>', text))
```

    Text: Make this **bold**.  This **too**.
    Bold: Make this <b>bold</b>.  This <b>too</b>.



```python
import re

bold = re.compile(r'\*{2}(.*?)\*{2}')

text = 'Make this **bold**.  This **too**.'

print('Text:', text)
print('Bold:', bold.sub(r'<b>\1</b>', text, count=1))
```

    Text: Make this **bold**.  This **too**.
    Bold: Make this <b>bold</b>.  This **too**.



```python
import re

bold = re.compile(r'\*{2}(.*?)\*{2}')

text = 'Make this **bold**.  This **too**.'

print('Text:', text)
print('Bold:', bold.subn(r'<b>\1</b>', text))
```

    Text: Make this **bold**.  This **too**.
    Bold: ('Make this <b>bold</b>.  This <b>too</b>.', 2)


## splitting


```python
import re

text = '''Paragraph one
on two lines.

Paragraph two.


Paragraph three.'''

for num, para in enumerate(re.findall(r'(.+?)\n{2,}',
                                      text,
                                      flags=re.DOTALL)
                           ):
    print(num, repr(para))
    print()
```

    0 'Paragraph one\non two lines.'
    
    1 'Paragraph two.'
    



```python
import re

text = '''Paragraph one
on two lines.

Paragraph two.


Paragraph three.'''

print('With findall:')
for num, para in enumerate(re.findall(r'(.+?)(\n{2,}|$)',
                                      text,
                                      flags=re.DOTALL)):
    print(num, repr(para))
    print()

print()
print('With split:')
for num, para in enumerate(re.split(r'\n{2,}', text)):
    print(num, repr(para))
    print()
```

    With findall:
    0 ('Paragraph one\non two lines.', '\n\n')
    
    1 ('Paragraph two.', '\n\n\n')
    
    2 ('Paragraph three.', '')
    
    
    With split:
    0 'Paragraph one\non two lines.'
    
    1 'Paragraph two.'
    
    2 'Paragraph three.'
    



```python
import re

text = '''Paragraph one
on two lines.

Paragraph two.


Paragraph three.'''

print('With split:')
for num, para in enumerate(re.split(r'(\n{2,})', text)):
    print(num, repr(para))
    print()

```

    With split:
    0 'Paragraph one\non two lines.'
    
    1 '\n\n'
    
    2 'Paragraph two.'
    
    3 '\n\n\n'
    
    4 'Paragraph three.'
    



```python

```
