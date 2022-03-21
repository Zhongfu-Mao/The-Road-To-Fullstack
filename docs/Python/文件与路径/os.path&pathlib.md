|処理内容| os及びos.path | pathlib | 
| :-- | :-- | :-- | 
|絶対パスへ変換| os.path.abspath() | Path.resolve() |
|絶対パスか判定| os.path.isabs() | PurePath.is_absolute() |
|権限を変えkる| os.chmod() | Path.chmod() |
|フォルダを作成| os.mkdir(), os.makedirs() | Path.mkdir() |
|フォルダを削除| os.rmdir() | Path.rmdir() |
|名前を変更| os.rename() | Path.rename() |
|ファイルまたはディレクトリ名前変更| os.replace() | Path.replace() |
|ファイルを削除| os.remove(), os.unlink() | Path.unlink() |
|カレントディレクトリ取得| os.getcwd() | Path.cwd() |
|パスの存在確認| os.path.exists() | Path.exists() |
|先頭の`~`をホームディレクトリに置換| os.path.expanduser() | Path.expanduser(), Path.home() |
|ディレクトリか判定| os.path.isdir() | Path.is_dir() |
|ファイルか判定| os.path.isfile() | Path.is_file() |
|シンボリックリンクか判定| os.path.islink() | Path.is_symlink() |
|ステータス取得| os.stat() | Path.stat(), Path.owner(), Path.group() |
|パスを結合| os.path.join() | PurePath.joinpath() |
|ファイル名を取得| os.path.basename() | PurePath.name |
|親ディレクトリを取得| os.path.dirname() | PurePath.parent |
|同じファイルか判定| os.path.samefile() | Path.samefile() |
|拡張子を取得| os.path.splitext() | PurePath.suffix |

# os.path

パスの解析は以下の変数に依存する
* `os.sep`: パスの各部分を分離する記号
* `os.extsep`: ファイル名と拡張子を結合する記号
* `os.pardir`: 上の階層を表す記号
* `os.curdir`: 現在の階層を表す記号



```python
import os
print(f"{os.sep=}") # windowsの場合は"\"
print(f"{os.extsep=}")
print(f"{os.pardir=}")
print(f"{os.curdir=}")
```

    os.sep='/'
    os.extsep='.'
    os.pardir='..'
    os.curdir='.'


## split()


```python
import os.path

PATHS = [
    '/one/two/three',
    '/one/two/three',
    '/',
    '.',
    ''
]

for path in PATHS:
    print(f"{path!r:>17} : {os.path.split(path)}")
```

     '/one/two/three' : ('/one/two', 'three')
     '/one/two/three' : ('/one/two', 'three')
                  '/' : ('/', '')
                  '.' : ('', '.')
                   '' : ('', '')


戻り値はtuple, 二番目の要素はパスの最後の部分、そして一番目の要素は残りの部分

## basename()


```python
import os.path

PATHS = [
    '/one/two/three',
    '/one/two/three',
    '/',
    '.',
    ''
]

for path in PATHS:
    print(f"{path!r:>17} : {os.path.basename(path)!r}")
```

     '/one/two/three' : 'three'
     '/one/two/three' : 'three'
                  '/' : ''
                  '.' : '.'
                   '' : ''


`split()[1]`に相当

## dirname()


```python
import os.path

PATHS = [
    '/one/two/three',
    '/one/two/three',
    '/',
    '.',
    ''
]

for path in PATHS:
    print(f"{path!r:>17} : {os.path.dirname(path)!r}")
```

     '/one/two/three' : '/one/two'
     '/one/two/three' : '/one/two'
                  '/' : '/'
                  '.' : ''
                   '' : ''


`split()[0]`に相当

## splittext()


```python
import os.path

PATHS = [
    'filename.txt',
    'filename',
    '/path/to/filename.txt',
    '/',
    '',
    'my-archive.tar.gz',
    'no-extension.',
]

for path in PATHS:
    print(f'{path!r:>25} : {os.path.splitext(path)!r}')
```

               'filename.txt' : ('filename', '.txt')
                   'filename' : ('filename', '')
      '/path/to/filename.txt' : ('/path/to/filename', '.txt')
                          '/' : ('/', '')
                           '' : ('', '')
          'my-archive.tar.gz' : ('my-archive.tar', '.gz')
              'no-extension.' : ('no-extension', '.')


`split`は`os.sep`で分離する、`splitext`は`os.extsep`を利用する

## commonprefix()


```python
import os.path

paths = ['/one/two/three/four',
         '/one/two/threefold',
         '/one/two/three/',
         ]
for path in paths:
    print('PATH:', path)

print()
print('PREFIX:', os.path.commonprefix(paths))
```

    PATH: /one/two/three/four
    PATH: /one/two/threefold
    PATH: /one/two/three/
    
    PREFIX: /one/two/three


パス分離記号を考慮していないので実際存在しない結果になるかもしれない

## commonpath()


```python
import os.path

paths = ['/one/two/three/four',
         '/one/two/threefold',
         '/one/two/three/',
         ]
for path in paths:
    print('PATH:', path)

print()
print('PREFIX:', os.path.commonpath(paths))
```

    PATH: /one/two/three/four
    PATH: /one/two/threefold
    PATH: /one/two/three/
    
    PREFIX: /one/two


この関数は考慮している

## join()


```python
import os.path

PATHS = [
    ('one', 'two', 'three'),
    ('/', 'one', 'two', 'three'),
    ('/one', '/two', '/three'),
]

for parts in PATHS:
    print(f'{parts} : {os.path.join(*parts)!r}')
```

    ('one', 'two', 'three') : 'one/two/three'
    ('/', 'one', 'two', 'three') : '/one/two/three'
    ('/one', '/two', '/three') : '/three'


頭文字は`os.sep`のパラメータがあったら、その前のパラメータは捨てられる

## expanduser()


```python
import os.path

for user in ['', 'maozhongfu', 'nosuchuser']:
    lookup = '~' + user
    print(f'{lookup!r:>15} : {os.path.expanduser(lookup)!r}')
```

                '~' : '/Users/maozhongfu'
      '~maozhongfu' : '/Users/maozhongfu'
      '~nosuchuser' : '~nosuchuser'


`~`はユーザのディレクトリに変換される、見つからない場合はそのまま戻る

## expandvars()


```python
import os.path
import os

os.environ['MYVAR'] = 'VALUE'

print(os.path.expandvars('/path/to/$MYVAR'))
```

    /path/to/VALUE


shellの中の環境変数を解析する

## normpath()


```python
import os.path

PATHS = [
    'one//two//three',
    'one/./two/./three',
    'one/../alt/two/three',
]

for path in PATHS:
    print(f'{path!r:>22} : {os.path.normpath(path)!r}')
```

         'one//two//three' : 'one/two/three'
       'one/./two/./three' : 'one/two/three'
    'one/../alt/two/three' : 'alt/two/three'


`os.curdir`,`os.pardir`は解析され展開する

## normcase()


```python
import os.path 
  
path_1 = r'C:\User\admin\Documents'
# 大文字は小文字に変更される
print(f"{path_1!r:20} -> {os.path.normcase(path_1)}") 
  
path_2 = '/hoMe/UseR/'
# slashはbackslashになる
print(f"{path_2!r:20} -> {os.path.normcase(path_2)}") 
  
path_3 = r'C:\Users/Desktop'
# 統一される
print(f"{path_3!r:20} -> {os.path.normcase(path_3)}") 
```

    'C:\\User\\admin\\Documents' -> c:\user\admin\documents
    '/hoMe/UseR/'        -> \home\user\
    'C:\\Users/Desktop'  -> c:\users\desktop


## abspath()


```python
import os
import os.path

os.chdir('/usr')

PATHS = [
    '.',
    '..',
    './one/two/three',
    '../one/two/three',
]

for path in PATHS:
    print(f'{path!r:>21} : {os.path.abspath(path)!r}')
```

                      '.' : '/usr'
                     '..' : '/'
        './one/two/three' : '/usr/one/two/three'
       '../one/two/three' : '/one/two/three'


## getatime(), getmtime(), getctime(), getsize()


```python
%%writefile foo.py

import os.path
import time

print('File         :', __file__)
print('Access time  :', time.ctime(os.path.getatime(__file__)))
print('Modified time:', time.ctime(os.path.getmtime(__file__)))
print('Change time  :', time.ctime(os.path.getctime(__file__)))
print('Size         :', os.path.getsize(__file__))
```

    Writing foo.py



```python
%run foo.py
```

    File         : /Users/maozhongfu/GitHub/Python/ファイルとディレクトリ/foo.py
    Access time  : Thu Nov  5 02:07:33 2020
    Modified time: Thu Nov  5 02:07:31 2020
    Change time  : Thu Nov  5 02:07:31 2020
    Size         : 306



```python
!rm foo.py
```

* `os.path.getatime()`: ファイルの最後のアクセル時間(access)
* `os.path.getmtime()`: ファイルの最後の変更時間(modify)
* `os.path.getctime()`: ファイルの作られる時間(create)
* `os.path.getsize()`: ファイルの大きさ(Bytes)

## isX(), exists(), lexists()


```python
%%writefile foo.py

import os.path

FILENAMES = [
    __file__,
    os.path.dirname(__file__),
    '/',
    './broken_link',
]

for file in FILENAMES:
    print('File        : {!r}'.format(file))
    print('Absolute    :', os.path.isabs(file))
    print('Is File?    :', os.path.isfile(file))
    print('Is Dir?     :', os.path.isdir(file))
    print('Is Link?    :', os.path.islink(file))
    print('Mountpoint? :', os.path.ismount(file))
    print('Exists?     :', os.path.exists(file))
    print('Link Exists?:', os.path.lexists(file))
    print()
```

    Writing foo.py


[mount point](https://en.wikipedia.org/wiki/Mount_(computing))


```python
%run foo.py
```

    File        : '/Users/maozhongfu/GitHub/Python/ファイルとディレクトリ/foo.py'
    Absolute    : True
    Is File?    : True
    Is Dir?     : False
    Is Link?    : False
    Mountpoint? : False
    Exists?     : True
    Link Exists?: True
    
    File        : '/Users/maozhongfu/GitHub/Python/ファイルとディレクトリ'
    Absolute    : True
    Is File?    : False
    Is Dir?     : True
    Is Link?    : False
    Mountpoint? : False
    Exists?     : True
    Link Exists?: True
    
    File        : '/'
    Absolute    : True
    Is File?    : False
    Is Dir?     : True
    Is Link?    : False
    Mountpoint? : True
    Exists?     : True
    Link Exists?: True
    
    File        : './broken_link'
    Absolute    : False
    Is File?    : False
    Is Dir?     : False
    Is Link?    : False
    Mountpoint? : False
    Exists?     : False
    Link Exists?: False
    



```python
!rm foo.py
```

# pathlib

参考文档：[pathlib cookbook](https://miguendes.me/python-pathlib)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1635494392030/uomUWH2vC.png?auto=compress,format&format=webp)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1635494412217/w8PsZFUD-.png?auto=compress,format&format=webp)

**OOP**の考え方でAPIを構築、解析; 文字列の処理よりレベル高い


```python
import pathlib
```


```python
pathlib.*Path?
```

    pathlib.Path
    pathlib.PosixPath
    pathlib.PurePath
    pathlib.PurePosixPath
    pathlib.PureWindowsPath
    pathlib.WindowsPath

`PurePosixPath`と`PureWindowsPath`はただ文字列を処理するだけでファイルシステムと関わらない  
一方、実際のファイルシステムを操作する際、`Path`を利用すべき  
基本OSによって`PosixPath`や`WindowsPath`のインスタンスを作成する

## 汎用プロパティ

> パスは変更不可(immutable)でハッシュ可能(hashable)  
> 基本OS同じの場合は比較などできる


```python
from pathlib import PurePosixPath, PureWindowsPath

print(PurePosixPath('foo') == PurePosixPath('FOO'))
print(PureWindowsPath('foo') == PureWindowsPath('FOO'))
print(PureWindowsPath('FOO') in { PureWindowsPath('foo') })
print(PureWindowsPath('C:') < PureWindowsPath('d:'))
print(PureWindowsPath('foo') == PurePosixPath('foo'))
# print(PureWindowsPath('foo') < PurePosixPath('foo')) # エラーが起こる
```

    False
    True
    True
    True
    False


## "/"演算子


```python
import pathlib

usr = pathlib.PurePosixPath('/usr')
print(usr)

usr_local = usr / 'local'  # os.path.join()と同じ
print(usr_local)

usr_share = usr / pathlib.PurePosixPath('share')
print(usr_share)

root = usr / '..'
print(root)

etc = root / '/etc/'
print(etc)

# Windowsの場合は、ローカルルータを変えても前のドライバーが残る
print(pathlib.PureWindowsPath('c:/Windows') / '/Program Files')
```

    /usr
    /usr/local
    /usr/share
    /usr/..
    /etc


## resolve()


```python
import pathlib

usr_local = pathlib.Path('/usr/local')
share = usr_local / '..' / 'share'
print(share.resolve())  # 解析される
```

    /usr/share


## joinpath()


```python
import pathlib

root = pathlib.PurePosixPath('/')
subdirs = ['usr', 'local']
usr_local = root.joinpath(*subdirs)
print(usr_local)
```

    /usr/local


## with_name(), with_suffix()


```python
import pathlib

ind = pathlib.PurePosixPath('source/pathlib/index.rst')
print(ind)

py = ind.with_name('pathlib_from_existing.py')
# os.path.join(os.path.dirname(ind), 'pathlib_from_existing.py')と同じ
print(py)

pyc = py.with_suffix('.pyc')
# os.path.splitext(py)[0] + ".pyc"と同じ
print(pyc)
```

    source/pathlib/index.rst
    source/pathlib/pathlib_from_existing.py
    source/pathlib/pathlib_from_existing.pyc


## parts


```python
import pathlib

p = pathlib.PurePosixPath('/usr/local')
print(p.parts)
```

    ('/', 'usr', 'local')


## parent, parents


```python
import pathlib

p = pathlib.PurePosixPath('/usr/local/lib')

print(f'{p.parent}')

print('\nhierarchy:')
for up in p.parents:
    print(up)
```

    /usr/local
    
    hierarchy:
    /usr/local
    /usr
    /


## name, suffix, suffixes, stem


```python
import pathlib

p = pathlib.PurePosixPath('./source/pathlib/pathlib_name.tar.gz')
print(f'path  : {p}')
print(f'name  : {p.name}')
print(f'suffix: {p.suffix}')
print(f'suffixes: {p.suffixes}')
print(f'stem  : {p.stem}')
```

    path  : source/pathlib/pathlib_name.tar.gz
    name  : pathlib_name.tar.gz
    suffix: .gz
    suffixs: ['.tar', '.gz']
    stem  : pathlib_name.tar


## home(), cwd()


```python
import pathlib

home = pathlib.Path.home()
print('home: ', home)

cwd = pathlib.Path.cwd()
print('cwd : ', cwd)
```

    home:  /Users/maozhongfu
    cwd :  /Users/maozhongfu/GitHub/Python/ファイルとディレクトリ


## iterdir()


```python
import pathlib

p = pathlib.Path('.')

for f in p.iterdir():
    print(f)
```

    codecs.ipynb
    os.path&pathlib.ipynb
    io.ipynb
    glob.ipynb
    shutil.ipynb


## glob()

如果要递归的检索所有子目录,使用`rglob()`方法


```python
import pathlib

p = pathlib.Path('..')

# glob("**/*.ipynb")と同じ
for f in p.glob('*.ipynb'):
    print(f)
```

    ../pip.ipynb
    ../typing.ipynb


## read_bytes(), read_text(), write_bytes(), write_text()


```python
import pathlib

f = pathlib.Path('example.txt')

f.write_bytes('This is the content'.encode('utf-8'))

with f.open('r', encoding='utf-8') as handle:
    print(f'read from open(): {handle.read()!r}')

print(f'read_text(): {f.read_text("utf-8")!r}')
```

    read from open(): 'This is the content'
    read_text(): 'This is the content'



```python
!rm example.txt
```

## mkdir(), rmdir()


```python
import pathlib

p = pathlib.Path('example_dir')

print(f'Creating {p}')
p.mkdir(exist_ok=True)  # os.makedirs(p, exist_ok=True)と同じ

print(f'Removing {p}')
p.rmdir()
```

    Creating example_dir


## symlink_to()


```python
import pathlib

p = pathlib.Path('example_link')

p.symlink_to('glob.ipynb')

print(p)
print(p.resolve().name)
```

    example_link
    glob.ipynb



```python
!rm example_link
```

## as_posix(), as_uri()


```python
from pathlib import PurePosixPath, PureWindowsPath

p = PureWindowsPath('c:\\windows')
print(f"{p!r:25} -> {p.as_posix()}")

p = PurePosixPath('/etc/passwd')
print(f"{p!r:25} -> {p.as_uri()}")

p = PureWindowsPath('c:/Windows')
print(f"{p!r:25} -> {p.as_uri()}")
```

    PureWindowsPath('c:/windows') -> c:/windows
    PurePosixPath('/etc/passwd') -> file:///etc/passwd
    PureWindowsPath('c:/Windows') -> file:///c:/Windows


## isX()


```python
import itertools
import os
import pathlib

root = pathlib.Path('test_files')

# 前の結果を消す
if root.exists():
    for f in root.iterdir():
        f.unlink()
else:
    root.mkdir()

# テストファイルを作る
(root / 'file').write_text('This is a regular file', encoding='utf-8')
(root / 'symlink').symlink_to('file')
os.mkfifo(str(root / 'fifo'))

to_scan = itertools.chain(
    root.iterdir(),
    [pathlib.Path('/dev/disk0'),
     pathlib.Path('/dev/console')],
)
hfmt = '{:18s}' + ('  {:>5}' * 6)
print(hfmt.format('Name', 'File', 'Dir', 'Link', 'FIFO', 'Block',
                  'Character'))
print()

fmt = '{:20s}  ' + ('{!r:>5}  ' * 6)
for f in to_scan:
    print(fmt.format(
        str(f),
        f.is_file(),
        f.is_dir(),
        f.is_symlink(),
        f.is_fifo(),
        f.is_block_device(),
        f.is_char_device(),
    ))
```

    Name                 File    Dir   Link   FIFO  Block  Character
    
    test_files/symlink     True  False   True  False  False  False  
    test_files/file        True  False  False  False  False  False  
    test_files/fifo       False  False  False   True  False  False  
    /dev/disk0            False  False  False  False   True  False  
    /dev/console          False  False  False  False  False   True  



```python
!rm -rf test_files
```

## stat(), lstat()


```python
%%writefile foo.py

import pathlib
import sys
import time

if len(sys.argv) == 1:
    filename = __file__
else:
    filename = sys.argv[1]

p = pathlib.Path(filename)
stat_info = p.stat()

print(f'{filename}:')
print('  Size:', stat_info.st_size)
print('  Permissions:', oct(stat_info.st_mode))
print('  Owner:', stat_info.st_uid)
print('  Device:', stat_info.st_dev)
print('  Created      :', time.ctime(stat_info.st_ctime))
print('  Last modified:', time.ctime(stat_info.st_mtime))
print('  Last accessed:', time.ctime(stat_info.st_atime))
```

    Writing foo.py



```python
%run foo.py
```

    /Users/maozhongfu/GitHub/Python/ファイルとディレクトリ/foo.py:
      Size: 531
      Permissions: 0o100644
      Owner: 501
      Device: 16777220
      Created      : Thu Nov  5 03:23:05 2020
      Last modified: Thu Nov  5 03:23:05 2020
      Last accessed: Thu Nov  5 03:23:07 2020



```python
!rm foo.py
```

## owner(), group()


```python
%%writefile bar.py

import pathlib

p = pathlib.Path(__file__)

print(f'{p} is owned by {p.owner()}/{p.group()}')
```

    Writing bar.py



```python
%run bar.py
```

    /Users/maozhongfu/GitHub/Python/ファイルとディレクトリ/bar.py is owned by maozhongfu/staff



```python
!rm bar.py
```

## touch()


```python
import pathlib
import time

p = pathlib.Path('touched')
if p.exists():
    print('already exists')
else:
    print('creating new')

p.touch()
start = p.stat()

time.sleep(1)

p.touch()
end = p.stat()

print('Start:', time.ctime(start.st_mtime))
print('End  :', time.ctime(end.st_mtime))
```

    creating new
    Start: Thu Nov  5 03:27:34 2020
    End  : Thu Nov  5 03:27:35 2020



```python
!rm touched
```

## chmod()


```python
import os
import pathlib
import stat

# 新しいテストファイルを作る
f = pathlib.Path('pathlib_chmod_example.txt')
if f.exists():
    f.unlink()
f.write_text('contents')

# statでファイルの権限を確認する
existing_permissions = stat.S_IMODE(f.stat().st_mode)
print('Before: {:o}'.format(existing_permissions))

if not (existing_permissions & os.X_OK):
    print('Adding execute permission')
    new_permissions = existing_permissions | stat.S_IXUSR
else:
    print('Removing execute permission')
    # xor でexe権限を消す
    new_permissions = existing_permissions ^ stat.S_IXUSR

# 権限を修正する
f.chmod(new_permissions)
after_permissions = stat.S_IMODE(f.stat().st_mode)
print('After: {:o}'.format(after_permissions))
```

    Before: 644
    Adding execute permission
    After: 744



```python
!rm pathlib_chmod_example.txt
```
