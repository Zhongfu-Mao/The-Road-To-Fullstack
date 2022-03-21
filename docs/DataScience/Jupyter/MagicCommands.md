# MagicCommands

* Line Magic: `%`で始まる
* Cell Magic: `%%`で始まる

> Line Magicは自動的に認識されるが、Cell Magicは`%%`を付けらないといけない

## Line Magic

### %alias

> システムコマンドの別名を定義する  
> `%alias alias_name cmd`で`cmd`を`alias_name`という別名を作り出す  
> そこで、`alias_name params`を実行したら`cmd params`と同じ効果

### %unalias

> 別名を削除する

### %alias_magic

> line magic もしくは　cell magic　に別名を定義する

`%alias_magic [-l] [-c] [-p PARAMS] name target`

* -l, --line: line magic別名
* -c, --cell: cell magic別名
* -p PARAMS, --params PARAMS: magic関数に渡るパラメータ

```python
```python
In [1]: %alias_magic t timeit  # `timeit`というcell magicとline magic両方あるので、同時に別名を作った
Created `%t` as an alias for `%timeit`.
Created `%%t` as an alias for `%%timeit`.

In [2]: %t -n1 pass
1 loops, best of 3: 954 ns per loop

In [3]: %%t -n1
   ...: pass
   ...:
1 loops, best of 3: 954 ns per loop

In [4]: %alias_magic --cell whereami pwd
UsageError: Cell magic function `%%pwd` not found.  # ないの場合は、エラーが起こる
In [5]: %alias_magic --line whereami pwd
Created `%whereami` as an alias for `%pwd`.

In [6]: %whereami
Out[6]: '/home/testuser'

In [7]: %alias_magic h history "-p -l 30" --line
Created `%h` as an alias for `%history -l 30`.
```

### %autoawait

> 非同期処理統合に対して調節する  
> パラメータないなら、機能のON,OFF状態と利用するライブラリーを示す
>> `asyncio`(default値),`curio`と `trio`のいずれかをインポートする  
> False/false/off は非活性化にする  
> True/true/on は活性化にする  
> asyncio/curio/trio は利用するライブラリーを選択する

### %autocall

```python
> 関数を呼び出すときに、括弧を書かなくてもいい様に

`%autocall [mode]`
* 0: Off(無効)
* 1: Smart(パラメータがあるなら有効)
* 2: Full(常に有効)
```

```python
%autocall 0
```

    Automatic calling is: OFF

```python
int 1.23
```

      File "<ipython-input-5-7c131faad543>", line 1
        int 1.23
            ^
    SyntaxError: invalid syntax

```python
%autocall 1
```

    Automatic calling is: Smart

```python
int 1.23
```

    ------> int(1.23)
    ------> int(1.23)





    1

```python
int
```

    int

```python
%autocall 2
```

    Automatic calling is: Full

```python
int
```

    ------> int()
    ------> int()





    0

### %automagic

> magic関数を利用する際に、`%`を書かなくてもいい様に

* パラメータがないなら、ON,OFFをスイッチ
* on, 1, True: 有効
* off, 0, False: 無効

### %bookmark

> bookmarkシステムを管理

* `%bookmark <name>`: 現在のディレクトリをbookmarkに追加
* `%bookmark <name> <dir>`: 指定するディレクトリをbookmarkに追加
* `%bookmark -l`: bookmark一覧
* `%bookmark -d <name>`: `name`のbookmarkを削除
* `%bookmark -r`: 全てのbookmarkを削除

### %cd

> 現在のディレクトリを変える  
> このコマンドは自動的にアクセスしたディレクトリを`_dh`に保存させる  

* `cd 'dir'`: `dir`へ移動
* `cd -`: 前回アクセスしたディレクトリへ移動
* `cd -<n>`: アクセス履歴のn番目へ移動
* `cd -foo`: 履歴の中に`foo`と一致するものへ移動
* `cd -b <bookmark name>`:　bookmarkした所へ移動
* `cd -q`: コマンドを実行後ディレクトリを出力しないように

### %colors

> prompts, info system, exception handlersの色体系を設定する

利用可能値:

* NoColor
* Linux
* LightBG

※大文字小文字敏感ではない

### %conda

> **conda**パッケージマネジャーを召喚

`%conda install [package]`

### %config

> IPython設定値を変える

`%config Class[.trait=value]`

```python
# パラメータ無しでクラスの一覧を確認
%config
```

    Available objects for config:
         AliasManager
         DisplayFormatter
         HistoryManager
         IPCompleter
         IPKernelApp
         LoggingMagics
         MagicsManager
         OSMagics
         PrefilterManager
         ScriptMagics
         StoreMagics
         ZMQInteractiveShell

```python
# 設定できる値を見たい時、クラス名だけ
# 例として
%config IPCompleter
```

    IPCompleter(Completer) options
    ----------------------------
    IPCompleter.backslash_combining_completions=<Bool>
        Enable unicode completions, e.g. \alpha<tab> . Includes completion of latex
        commands, unicode names, and expanding unicode characters back to latex
        commands.
        Current: True
    IPCompleter.debug=<Bool>
        Enable debug for the Completer. Mostly print extra information for
        experimental jedi integration.
        Current: False
    IPCompleter.greedy=<Bool>
        Activate greedy completion PENDING DEPRECTION. this is now mostly taken care
        of with Jedi.
        This will enable completion on elements of lists, results of function calls,
        etc., but can be unsafe because the code is actually evaluated on TAB.
        Current: False
    IPCompleter.jedi_compute_type_timeout=<Int>
        Experimental: restrict time (in milliseconds) during which Jedi can compute
        types. Set to 0 to stop computing types. Non-zero value lower than 100ms may
        hurt performance by preventing jedi to build its cache.
        Current: 400
    IPCompleter.limit_to__all__=<Bool>
        DEPRECATED as of version 5.0.
        Instruct the completer to use __all__ for the completion
        Specifically, when completing on ``object.<tab>``.
        When True: only those names in obj.__all__ will be included.
        When False [default]: the __all__ attribute is ignored
        Current: False
    IPCompleter.merge_completions=<Bool>
        Whether to merge completion results into a single list
        If False, only the completion results from the first non-empty completer
        will be returned.
        Current: True
    IPCompleter.omit__names=<Enum>
        Instruct the completer to omit private method names
        Specifically, when completing on ``object.<tab>``.
        When 2 [default]: all names that start with '_' will be excluded.
        When 1: all 'magic' names (``__foo__``) will be excluded.
        When 0: nothing will be excluded.
        Choices: any of [0, 1, 2]
        Current: 2
    IPCompleter.use_jedi=<Bool>
        Experimental: Use Jedi to generate autocompletions. Default to True if jedi
        is installed.
        Current: True

### %debug

> IPythonのdebugシステムを利用

### %dhist

```python
> アクセスしたディレクトリを綺麗な形で表す
```

```python
%dhist
```

    Directory history (kept in _dh)
    0: /
    1: /Users/maozhongfu/GitHub/DataScience/Jupyter
    2: /Users/maozhongfu/GitHub/DataScience
    3: /Users/maozhongfu/GitHub
    4: /Users/maozhongfu
    5: /Users

### %pushd

> 現在のディレクトリをstackへ追加後ディレクトリを変更

`%pushd ["dirname"]`

### %dirs

> ディレクトリstackを表示

### %popd

> ディレクトリstackをpopし、ディレクトリを変換

### %doctest_mode

> doctestモードを有効するスイッチ

有効の場合、以下の様な変更点がある

* `In []`, `Out []`から`>>>`になる
* pretty-printingをOFFにする
* エラーの出力が地味になる

一言で言うと、IPythonのスタイルからPythonスタイルへ変換

```python
```python
In [1]: %doctest_mode
Exception reporting mode: Plain
Doctest mode is: ON
>>> 1 + "1"
Traceback (most recent call last):
  File "<ipython-input-2-b780703cc5f9>", line 1, in <module>
    1 + "1"
TypeError: unsupported operand type(s) for +: 'int' and 'str'

>>> %doctest_mode
Exception reporting mode: Context
Doctest mode is: OFF

In [4]: 1 + "1"
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-4-b780703cc5f9> in <module>
----> 1 1 + "1"

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

### %edit

> 環境変数に定義された｀$EDITOR`を起動して入力したコードを実行する  
> 定義されていないなら、Linux/Macの場合`vi`、Windowsの場合`notepad`

### %env

```python
> 環境変数を取得、設定、列挙する

* `%env`: 一覧を列挙する
* `%env var`: `var`の値を取得
* `%env var val`、`%env var=val`: `var`の値の`val`に設定する
* `%env var=$val`: pythonの変数を利用して設定する
```

### %gui

> IPythonの内蔵されているGUIイベントループを有効するかどうか

### %history

> 入力の履歴を出力する

### %killbgscripts

> `%%script`で実行したスクリプトを全部閉じる

### %load

> 指定したファイルを読み込んでIPython上で実行する

```python
* `%load myscript.py`: pythonファイルを実行
* `%load http:www.example.com/myscript.py`:　URLからファイルを実行
* `%load -r 5-10 myscript.py`: 範囲を指定
* `%load -r 12: myscript.py`: pythonのスライス文法で範囲を指定
* `%load -s MyClass, wonder_function myscript.py`: ファイルから特定のクラスや関数を指定してload
* `%load -n my_module.wonder_function`: ユーザの名前空間からload
```

### %load_ext

> IPythonのextensionをload

### %loadpy

> `%load`の別名

### %logstart

> logging開始

### %logoff

> logging一時的に停止

### %logon

> logging再開

### %logstop

> logging中止

### %logstate

> loggingの状態を出力

```python
# 例として
```python
In [26]: logstate
Filename       : ipython_log.py
Mode           : rotate
Output logging : True
Raw input log  : False
Timestamping   : False
State          : active
```

### %lsmagic

> 利用可能のmagic関数一覧

Notes: VSCode上のjupyter notebookには出力無し

```python
In [28]: lsmagic
Out[28]: 
Available line magics:
%alias  %alias_magic  %autoawait  %autocall  %autoindent  %automagic  %bookmark  %cat  %cd  %clear  %colors  %conda  %config  %cp  %cpaste  %debug  %dhist  %dirs  %doctest_mode  %ed  %edit  %env  %gui  %hist  %history  %killbgscripts  %ldir  %less  %lf  %lk  %ll  %load  %load_ext  %loadpy  %logoff  %logon  %logstart  %logstate  %logstop  %ls  %lsmagic  %lx  %macro  %magic  %man  %matplotlib  %mkdir  %more  %mv  %notebook  %page  %paste  %pastebin  %pdb  %pdef  %pdoc  %pfile  %pinfo  %pinfo2  %pip  %popd  %pprint  %precision  %prun  %psearch  %psource  %pushd  %pwd  %pycat  %pylab  %quickref  %recall  %rehashx  %reload_ext  %rep  %rerun  %reset  %reset_selective  %rm  %rmdir  %run  %save  %sc  %set_env  %store  %sx  %system  %tb  %time  %timeit  %unalias  %unload_ext  %who  %who_ls  %whos  %xdel  %xmode

Available cell magics:
%%!  %%HTML  %%SVG  %%bash  %%capture  %%debug  %%file  %%html  %%javascript  %%js  %%latex  %%markdown  %%perl  %%prun  %%pypy  %%python  %%python2  %%python3  %%ruby  %%script  %%sh  %%svg  %%sx  %%system  %%time  %%timeit  %%writefile

Automagic is ON, % prefix IS NOT needed for line magics.
```

```

### %macro

> macroを定義する

### %magic

> magic関数システムの情報を出力する

### %matplotlib

> `matplotlib`を立ち上げる

`%matplotlib [-l] [gui]`


```python
%matplotlib -l
```

    Available matplotlib backends: ['tk', 'gtk', 'gtk3', 'wx', 'qt4', 'qt5', 'qt', 'osx', 'nbagg', 'notebook', 'agg', 'svg', 'pdf', 'ps', 'inline', 'ipympl', 'widget']

一番よく使う`inline`はbackendsの一つ

### %notebook

> notebookの形で出力する

### %page

> pagerを利用してオブジェクトを綺麗に出力する

### %pastebin

> 文字列あるいはmacroを[dpaste](https://dpaste.com)へアプロッドしURLを戻る

### %pdb

> `pdb`debuggerの自動呼び出しをコントロールする

### %pdef

> (print definition)クラスのコンストラクターあるいはオブジェクトの定義を出力

### %pdoc

> (print docstring)オブジェクトのdocstringを出力する

### %pfile

> (print file)オブジェクトが定義されるファイルを出力する

### %psource

> (print source code)オブジェクトのsource codeを出力する

### %pinfo

> `object?`や`?object`と同じ

### %pinfo2

> `object??`や``??object`と同じ

### %pip

> `pip`パッケージマネージャーを召喚

`%pip install [pkg name]`

### %pprint

> pprintの利用をコントロール

### %precision

> [表示桁数（精度）を設定する](https://note.nkmk.me/jupyter-notebook-ipython-precision/)

### %prun

> python code profilerを利用してstatementを実行する

### %psearch

> wildcardを利用して名前空間からオブジェクトを探す

### %pwd

> (print working directory)shellコマンドと同じ

### %pycat

> `cat`コマンドと同じ(pythonファイルならsyntax highlighting)

### %pylab

```python
> `numpy`,`matplotlib`をloadする
```

`%pylab [--no-import-all] [gui]`

```python
以下と同じ
```python
import numpy
import matplotlib
from matplotlib import pylab, mlab, pyplot
np = numpy
plt = pyplot

from IPython.display import display
from IPython.core.pylabtools import figsize, getfigs
### --no-import-allを指定する場合、以下の二行は実行されない
from pylab import *
from numpy import *
```

```

### %quickref


```python
%quickref
```

    IPython -- An enhanced Interactive Python - Quick Reference Card
    ================================================================
    
    obj?, obj??      : Get help, or more help for object (also works as
                       ?obj, ??obj).
    ?foo.*abc*       : List names in 'foo' containing 'abc' in them.
    %magic           : Information about IPython's 'magic' % functions.
    
    Magic functions are prefixed by % or %%, and typically take their arguments
    without parentheses, quotes or even commas for convenience.  Line magics take a
    single % and cell magics are prefixed with two %%.
    
    Example magic function calls:
    
    %alias d ls -F   : 'd' is now an alias for 'ls -F'
    alias d ls -F    : Works if 'alias' not a python name
    alist = %alias   : Get list of aliases to 'alist'
    cd /usr/share    : Obvious. cd -<tab> to choose from visited dirs.
    %cd??            : See help AND source for magic %cd
    %timeit x=10     : time the 'x=10' statement with high precision.
    %%timeit x=2**100
    x**100           : time 'x**100' with a setup of 'x=2**100'; setup code is not
                       counted.  This is an example of a cell magic.
    
    System commands:
    
    !cp a.txt b/     : System command escape, calls os.system()
    cp a.txt b/      : after %rehashx, most system commands work without !
    cp ${f}.txt $bar : Variable expansion in magics and system commands
    files = !ls /usr : Capture system command output
    files.s, files.l, files.n: "a b c", ['a','b','c'], 'a\nb\nc'
    
    History:
    
    _i, _ii, _iii    : Previous, next previous, next next previous input
    _i4, _ih[2:5]    : Input history line 4, lines 2-4
    exec _i81        : Execute input history line #81 again
    %rep 81          : Edit input history line #81
    _, __, ___       : previous, next previous, next next previous output
    _dh              : Directory history
    _oh              : Output history
    %hist            : Command history of current session.
    %hist -g foo     : Search command history of (almost) all sessions for 'foo'.
    %hist -g         : Command history of (almost) all sessions.
    %hist 1/2-8      : Command history containing lines 2-8 of session 1.
    %hist 1/ ~2/     : Command history of session 1 and 2 sessions before current.
    %hist ~8/1-~6/5  : Command history from line 1 of 8 sessions ago to
                       line 5 of 6 sessions ago.
    %edit 0/         : Open editor to execute code with history of current session.
    
    Autocall:
    
    f 1,2            : f(1,2)  # Off by default, enable with %autocall magic.
    /f 1,2           : f(1,2) (forced autoparen)
    ,f 1 2           : f("1","2")
    ;f 1 2           : f("1 2")
    
    Remember: TAB completion works in many contexts, not just file names
    or python names.
    
    The following magic functions are currently available:
    
    %alias:
        Define an alias for a system command.
    %alias_magic:
        ::
    %autoawait:
        
    %autocall:
        Make functions callable without having to type parentheses.
    %automagic:
        Make magic functions callable without having to type the initial %.
    %autosave:
        Set the autosave interval in the notebook (in seconds).
    %bookmark:
        Manage IPython's bookmark system.
    %cat:
        Alias for `!cat`
    %cd:
        Change the current working directory.
    %clear:
        Clear the terminal.
    %colors:
        Switch color scheme for prompts, info system and exception handlers.
    %conda:
        Run the conda package manager within the current kernel.
    %config:
        configure IPython
    %connect_info:
        Print information for connecting other clients to this kernel
    %cp:
        Alias for `!cp`
    %debug:
        ::
    %dhist:
        Print your history of visited directories.
    %dirs:
        Return the current directory stack.
    %doctest_mode:
        Toggle doctest mode on and off.
    %ed:
        Alias for `%edit`.
    %edit:
        Bring up an editor and execute the resulting code.
    %env:
        Get, set, or list environment variables.
    %gui:
        Enable or disable IPython GUI event loop integration.
    %hist:
        Alias for `%history`.
    %history:
        ::
    %killbgscripts:
        Kill all BG processes started by %%script and its family.
    %ldir:
        Alias for `!ls -F -G -l %l | grep /$`
    %less:
        Show a file through the pager.
    %lf:
        Alias for `!ls -F -l -G %l | grep ^-`
    %lk:
        Alias for `!ls -F -l -G %l | grep ^l`
    %ll:
        Alias for `!ls -F -l -G`
    %load:
        Load code into the current frontend.
    %load_ext:
        Load an IPython extension by its module name.
    %loadpy:
        Alias of `%load`
    %logoff:
        Temporarily stop logging.
    %logon:
        Restart logging.
    %logstart:
        Start logging anywhere in a session.
    %logstate:
        Print the status of the logging system.
    %logstop:
        Fully stop logging and close log file.
    %ls:
        Alias for `!ls -F -G`
    %lsmagic:
        List currently available magic functions.
    %lx:
        Alias for `!ls -F -l -G %l | grep ^-..x`
    %macro:
        Define a macro for future re-execution. It accepts ranges of history,
    %magic:
        Print information about the magic function system.
    %man:
        Find the man page for the given command and display in pager.
    %matplotlib:
        ::
    %mkdir:
        Alias for `!mkdir`
    %more:
        Show a file through the pager.
    %mv:
        Alias for `!mv`
    %notebook:
        ::
    %page:
        Pretty print the object and display it through a pager.
    %pastebin:
        Upload code to dpaste's paste bin, returning the URL.
    %pdb:
        Control the automatic calling of the pdb interactive debugger.
    %pdef:
        Print the call signature for any callable object.
    %pdoc:
        Print the docstring for an object.
    %pfile:
        Print (or run through pager) the file where an object is defined.
    %pinfo:
        Provide detailed information about an object.
    %pinfo2:
        Provide extra detailed information about an object.
    %pip:
        Run the pip package manager within the current kernel.
    %popd:
        Change to directory popped off the top of the stack.
    %pprint:
        Toggle pretty printing on/off.
    %precision:
        Set floating point precision for pretty printing.
    %prun:
        Run a statement through the python code profiler.
    %psearch:
        Search for object in namespaces by wildcard.
    %psource:
        Print (or run through pager) the source code for an object.
    %pushd:
        Place the current dir on stack and change directory.
    %pwd:
        Return the current working directory path.
    %pycat:
        Show a syntax-highlighted file through a pager.
    %pylab:
        ::
    %qtconsole:
        Open a qtconsole connected to this kernel.
    %quickref:
        Show a quick reference sheet 
    %recall:
        Repeat a command, or get command to input line for editing.
    %rehashx:
        Update the alias table with all executable files in $PATH.
    %reload_ext:
        Reload an IPython extension by its module name.
    %rep:
        Alias for `%recall`.
    %rerun:
        Re-run previous input
    %reset:
        Resets the namespace by removing all names defined by the user, if
    %reset_selective:
        Resets the namespace by removing names defined by the user.
    %rm:
        Alias for `!rm`
    %rmdir:
        Alias for `!rmdir`
    %run:
        Run the named file inside IPython as a program.
    %save:
        Save a set of lines or a macro to a given filename.
    %sc:
        Shell capture - run shell command and capture output (DEPRECATED use !).
    %set_env:
        Set environment variables.  Assumptions are that either "val" is a
    %store:
        Lightweight persistence for python variables.
    %sx:
        Shell execute - run shell command and capture output (!! is short-hand).
    %system:
        Shell execute - run shell command and capture output (!! is short-hand).
    %tb:
        Print the last traceback.
    %time:
        Time execution of a Python statement or expression.
    %timeit:
        Time execution of a Python statement or expression
    %unalias:
        Remove an alias
    %unload_ext:
        Unload an IPython extension by its module name.
    %who:
        Print all interactive variables, with some minimal formatting.
    %who_ls:
        Return a sorted list of all interactive variables.
    %whos:
        Like %who, but gives some extra information about each variable.
    %xdel:
        Delete a variable, trying to clear it from anywhere that
    %xmode:
        Switch modes for the exception handlers.
    %%!:
        Shell execute - run shell command and capture output (!! is short-hand).
    %%HTML:
        Alias for `%%html`.
    %%SVG:
        Alias for `%%svg`.
    %%bash:
        %%bash script magic
    %%capture:
        ::
    %%debug:
        ::
    %%file:
        Alias for `%%writefile`.
    %%html:
        ::
    %%javascript:
        Run the cell block of Javascript code
    %%js:
        Run the cell block of Javascript code
    %%latex:
        Render the cell as a block of latex
    %%markdown:
        Render the cell as Markdown text block
    %%perl:
        %%perl script magic
    %%prun:
        Run a statement through the python code profiler.
    %%pypy:
        %%pypy script magic
    %%python:
        %%python script magic
    %%python2:
        %%python2 script magic
    %%python3:
        %%python3 script magic
    %%ruby:
        %%ruby script magic
    %%script:
        ::
    %%sh:
        %%sh script magic
    %%svg:
        Render the cell as an SVG literal
    %%sx:
        Shell execute - run shell command and capture output (!! is short-hand).
    %%system:
        Shell execute - run shell command and capture output (!! is short-hand).
    %%time:
        Time execution of a Python statement or expression.
    %%timeit:
        Time execution of a Python statement or expression
    %%writefile:
        ::

### %recall

> コマンドを重複する、あるいは出力を入力欄に入れる

### %rehashx

> `$PATH`中の全ての実行可能のファイルの別名テーブルを更新する

### %reload_ext

> IPythonのextensionをreloadする

### %unload_ext

> extensionをunloadする

### %rerun

> 前の入力内容をもう一度実行する

### %reset

> 名前空間の中にユーザーが定義する名前を全てリセットする

`%reset`\[in | out | dhist | array] \[-f | s]`

* in: 入力履歴
* out: 出力履歴
* dhist: ディレクトリ履歴
* array: NumPy array履歴
* -f: 確認せずに(soft)
* -s: 名前空間だけをクリアして履歴はそのまま

### %reset_selective

> 正規表現に満たすものをリセットする

`%reset_selective [-f] regex`

### %run

> IPythonの中でファイルを実行する  
> `python file args`と似てるが良い所としてIPythonのトレースバック情報、  
> そして全ての変数は名前空間に導入される  
> Jupyter Notebookもファイルに属する

[IPython における「%run hoge.py」と「!python hoge.py」の違い](https://qiita.com/2-propanol/items/f6f63c3f20981df2c844)

### %save

> 一部の入力やmacroをPythonファイルに保存

`%save [options] filename n1-n2 n3-n4..n5`

> ファイルに拡張子を追加しても`.py`になる

* -r: raw input、拡張子は`.ipy`になる
* -f: 強制的に上書き
* -a: 追記モード

### %sc

> `!`前のshellへアクセル方法、推奨されない

### %set_env

> 環境変数をセットする

### %sx

> `%sc -l`と同じ効果、パラメータをリストとしてshellへ渡して結果をcaptureする

### %system

> `%sx`と同じ

### %tb

> 最後のtrackbackを出力する

### %time

> Python statementやexpressionの実行で掛かる時間測る  
> CPU time とwall timeが出力される

[real time/user CPU time/system CPU timeの違いをメモ](https://siguniang.wordpress.com/2015/08/30/what-is-wall-clock-time-and-cpu-time/)

### %timeit

> `timeit`モジュールで時間を測る

`%timeit [-n<N> -r<R> [-t|-c] -q -p<P> -o] statement`

* `-n<N>`: 一つのループでN回実行するかを設定、指定しない場合自動的に設定される
* `-r<R>`: 重複回数を指定、デフォルト７
* `-t`: wall time(time.time利用)
* `-c`: CPU time(time.clock利用)
* `-p<P>: 結果時間出力の精度を設定、デフォルト３
* `-q`: 出力しない
* `-o`: `TimeitResult`オブジェクトを戻る

### %who

> 変数一覧出力

### %who_ls

> 変数一覧をリストとして戻る

### %whos

> `%who`より多くの情報を提供する

### %xdel

> 変数を削除する

### %xmode

> Exception　handlerを設定する

## Cell Magics

### %%bash

> bash scriptを実行する

### %%capture

> cellを実行して、stdout, stderr, IPythonのdisplayを出力する

### %%html

> HTMLとしてcellを解析する

### %%javascript

> Javascriptとしてcellを解析する

### %%js

> `%%javascript`の別名

### %%latex

> [latex](https://ja.wikipedia.org/wiki/LaTeX)としてcellを解析する

### %%markdown

>　markdownとしてcellを解析する

### %%perl

> perl scriptとしてcellを解析する

### %%prun

```python
import numpy as np

def step(*shape):
    return 2 * (np.random.random_sample(shape)<.5) - 1
```

```python
%%prun -s cumulative -q -l 10 -T prun0
# We profile the cell, sort the report by "cumulative
# time", limit it to 10 lines, and save it to a file
# named "prun0".

n = 10000
iterations = 50
x = np.cumsum(step(iterations, n), axis=0)
bins = np.arange(-30, 30, 1)
y = np.vstack([np.histogram(x[i,:], bins)[0]
               for i in range(iterations)])
```

```python
print(open('prun0', 'r').read())
```

### %%pypy

> pypy scriptとしてcellを実行する

### %%python

> subprocessでPython codeを実行する

### %%python2

> subprocessでPython2 codeを実行する

### %%python3

> subprocessでPython3 codeを実行する

### %%ruby

> ruby scriptとしてcellを実行する

### %%script

> shellを選択してcellを実行する

### %%sh

>　subprocessでsh scriptを実行する

### %%svg

> SVGとしてcellを解析する

### %%writefile

>　cellの内容をファイルへ出力する

`%%writefile [-a] filename`

* `-a`: 追記モード

## [自分で定義する](https://ipython.readthedocs.io/en/stable/config/custommagics.html)

```python
from IPython.core.magic import (register_line_magic,
                                register_cell_magic)
```

```python
@register_line_magic
def hello(language):
    if language == 'Japanese':
        print("こんにちは!")
    elif language == "Chinese":
        print("你好!")
    else:
        print("Hi!")
```

```python
%hello
```

    Hi!

```python
%hello Japanese
```

    こんにちは!

```python
import pandas as pd
from io import StringIO

@register_cell_magic
def csv(line, cell):
    sio = StringIO(cell)
    return pd.read_csv(sio)
```

```python
%%csv
col1,col2,col3
0,1,2
3,4,5
7,8,9
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>

```python
df = _
df.describe()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>3.333333</td>
      <td>4.333333</td>
      <td>5.333333</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.511885</td>
      <td>3.511885</td>
      <td>3.511885</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.500000</td>
      <td>2.500000</td>
      <td>3.500000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>3.000000</td>
      <td>4.000000</td>
      <td>5.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>5.000000</td>
      <td>6.000000</td>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>7.000000</td>
      <td>8.000000</td>
      <td>9.000000</td>
    </tr>
  </tbody>
</table>
</div>

```python
%%writefile csvmagic.py

import pandas as pd
from io import StringIO

def csv(line, cell):
    sio = StringIO(cell)
    return pd.read_csv(sio)

def load_ipython_extension(ipython):
    ipython.register_magic_function(csv, 'cell')
```

    Writing csvmagic.py

```python
%load_ext csvmagic

```

```python
%%csv
col1,col2,col3
0,1,2
3,4,5
7,8,9
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>

```python
!rm csvmagic.py
```

```python
!rm -rf __pycache__/
```

```python

```
