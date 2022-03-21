参考資料
* [標準ライブラリ](https://docs.python.org/ja/3/library/sys.html)
* [PyMOTW-3](https://pymotw.com/3/sys/index.html)

> このモジュールでは、インタプリタで使用・管理している変数や、インタプリタの動作に深く関連する関数を定義しています。  
> このモジュールは常に利用可能です。

## インタプリタ設定

### バージョン情報


```python
import sys

print('Version info:')
print()
print('sys.version      =', repr(sys.version))
print('sys.version_info =', sys.version_info)
print('sys.hexversion   =', hex(sys.hexversion)) # 単精度整数にエンコードされたバージョン番号
print('sys.api_version  =', sys.api_version) # C API バージョン
```

    Version info:
    
    sys.version      = '3.8.6 (v3.8.6:db455296be, Sep 23 2020, 13:31:39) \n[Clang 6.0 (clang-600.0.57)]'
    sys.version_info = sys.version_info(major=3, minor=8, micro=6, releaselevel='final', serial=0)
    sys.hexversion   = 0x30806f0
    sys.api_version  = 1013


```bash
Python 3.8.6 (v3.8.6:db455296be, Sep 23 2020, 13:31:39) 
[Clang 6.0 (clang-600.0.57)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```
pythonを起動する時、表示するバーション情報は`sys.version`

sys.version_info
* major
* minor
* micro(patchと呼ばれる場合もある)
* releaselevel
* serial

`major.minor.micro`はPythonのバーションを示す  
`releaselevel`は'alpha', 'beta', 'candidate', 'final'の一つ


```python
import sys

print('This interpreter was built for:', sys.platform)
```

    This interpreter was built for: darwin


|システム|platform の値|
|:-:|:-:|
|Linux|'linux'|
|MacOS|'darwin'|
|Windows|'win32'|

### インタプリタ実装


```python
import sys


print('Name:', sys.implementation.name)
print('Version:', sys.implementation.version) # CPython以外の場合は"sys.version_info"と違う
print('Cache tag:', sys.implementation.cache_tag)
```

    Name: cpython
    Version: sys.version_info(major=3, minor=8, micro=6, releaselevel='final', serial=0)
    Cache tag: cpython-38


### コマンドライン選択肢


```python
!python3 -h
```

    usage: /Library/Frameworks/Python.framework/Versions/3.8/bin/python3 [option] ... [-c cmd | -m mod | file | -] [arg] ...
    Options and arguments (and corresponding environment variables):
    -b     : issue warnings about str(bytes_instance), str(bytearray_instance)
             and comparing bytes/bytearray with str. (-bb: issue errors)
    -B     : don't write .pyc files on import; also PYTHONDONTWRITEBYTECODE=x
    -c cmd : program passed in as string (terminates option list)
    -d     : debug output from parser; also PYTHONDEBUG=x
    -E     : ignore PYTHON* environment variables (such as PYTHONPATH)
    -h     : print this help message and exit (also --help)
    -i     : inspect interactively after running script; forces a prompt even
             if stdin does not appear to be a terminal; also PYTHONINSPECT=x
    -I     : isolate Python from the user's environment (implies -E and -s)
    -m mod : run library module as a script (terminates option list)
    -O     : remove assert and __debug__-dependent statements; add .opt-1 before
             .pyc extension; also PYTHONOPTIMIZE=x
    -OO    : do -O changes and also discard docstrings; add .opt-2 before
             .pyc extension
    -q     : don't print version and copyright messages on interactive startup
    -s     : don't add user site directory to sys.path; also PYTHONNOUSERSITE
    -S     : don't imply 'import site' on initialization
    -u     : force the stdout and stderr streams to be unbuffered;
             this option has no effect on stdin; also PYTHONUNBUFFERED=x
    -v     : verbose (trace import statements); also PYTHONVERBOSE=x
             can be supplied multiple times to increase verbosity
    -V     : print the Python version number and exit (also --version)
             when given twice, print more information about the build
    -W arg : warning control; arg is action:message:category:module:lineno
             also PYTHONWARNINGS=arg
    -x     : skip first line of source, allowing use of non-Unix forms of #!cmd
    -X opt : set implementation-specific option. The following options are available:
    
             -X faulthandler: enable faulthandler
             -X showrefcount: output the total reference count and number of used
                 memory blocks when the program finishes or after each statement in the
                 interactive interpreter. This only works on debug builds
             -X tracemalloc: start tracing Python memory allocations using the
                 tracemalloc module. By default, only the most recent frame is stored in a
                 traceback of a trace. Use -X tracemalloc=NFRAME to start tracing with a
                 traceback limit of NFRAME frames
             -X showalloccount: output the total count of allocated objects for each
                 type when the program finishes. This only works when Python was built with
                 COUNT_ALLOCS defined
             -X importtime: show how long each import takes. It shows module name,
                 cumulative time (including nested imports) and self time (excluding
                 nested imports). Note that its output may be broken in multi-threaded
                 application. Typical usage is python3 -X importtime -c 'import asyncio'
             -X dev: enable CPython's "development mode", introducing additional runtime
                 checks which are too expensive to be enabled by default. Effect of the
                 developer mode:
                    * Add default warning filter, as -W default
                    * Install debug hooks on memory allocators: see the PyMem_SetupDebugHooks() C function
                    * Enable the faulthandler module to dump the Python traceback on a crash
                    * Enable asyncio debug mode
                    * Set the dev_mode attribute of sys.flags to True
                    * io.IOBase destructor logs close() exceptions
             -X utf8: enable UTF-8 mode for operating system interfaces, overriding the default
                 locale-aware mode. -X utf8=0 explicitly disables UTF-8 mode (even when it would
                 otherwise activate automatically)
             -X pycache_prefix=PATH: enable writing .pyc files to a parallel tree rooted at the
                 given directory instead of to the code tree
    
    --check-hash-based-pycs always|default|never:
        control how Python invalidates hash-based .pyc files
    file   : program read from script file
    -      : program read from stdin (default; interactive mode if a tty)
    arg ...: arguments passed to program in sys.argv[1:]
    
    Other environment variables:
    PYTHONSTARTUP: file executed on interactive startup (no default)
    PYTHONPATH   : ':'-separated list of directories prefixed to the
                   default module search path.  The result is sys.path.
    PYTHONHOME   : alternate <prefix> directory (or <prefix>:<exec_prefix>).
                   The default module search path uses <prefix>/lib/pythonX.X.
    PYTHONCASEOK : ignore case in 'import' statements (Windows).
    PYTHONUTF8: if set to 1, enable the UTF-8 mode.
    PYTHONIOENCODING: Encoding[:errors] used for stdin/stdout/stderr.
    PYTHONFAULTHANDLER: dump the Python traceback on fatal errors.
    PYTHONHASHSEED: if this variable is set to 'random', a random value is used
       to seed the hashes of str and bytes objects.  It can also be set to an
       integer in the range [0,4294967295] to get hash values with a
       predictable seed.
    PYTHONMALLOC: set the Python memory allocators and/or install debug hooks
       on Python memory allocators. Use PYTHONMALLOC=debug to install debug
       hooks.
    PYTHONCOERCECLOCALE: if this variable is set to 0, it disables the locale
       coercion behavior. Use PYTHONCOERCECLOCALE=warn to request display of
       locale coercion and locale compatibility warnings on stderr.
    PYTHONBREAKPOINT: if this variable is set to 0, it disables the default
       debugger. It can be set to the callable of your debugger of choice.
    PYTHONDEVMODE: enable the development mode.
    PYTHONPYCACHEPREFIX: root directory for bytecode cache (pyc) files.


### Unicodeデフォルト


```python
import sys

print('Default encoding     :', sys.getdefaultencoding())
print('File system encoding :', sys.getfilesystemencoding())
```

    Default encoding     : utf-8
    File system encoding : utf-8


### 対話的プロンプト


```python
```python
>>> import sys
>>> sys.ps1
'>>> '
>>> sys.ps2
'... '
```
```

> 任意の`__str__`を定義したオブジェクトはプロンプトに利用できる


```python
```python
>>> import sys
>>> class IPythonStyle:
...     def __init__(self):
...         self.count = 0
...     
...     def __str__(self):
...         self.count += 1
...         return f"In [{self.count}]:"
... 
>>> sys.ps1=IPythonStyle()
In [1]:
In [2]:
In [3]:
```
```

### Install Location


```python
import sys

print('Interpreter executable:')
# プロンプトの場所、特に仮想環境を利用する際正しいプロンプトを利用しているかどうか確認できる
print(sys.executable)
print('\nInstallation prefix:')
# プロンプトがインストールされる場所
print(sys.prefix)
```

    Interpreter executable:
    /Library/Frameworks/Python.framework/Versions/3.8/bin/python3
    
    Installation prefix:
    /Library/Frameworks/Python.framework/Versions/3.8


## Runtime Environment

### コマンドラインパラメータ


```python
%%writefile foo.py

import sys

print("Arguments: ", sys.argv)
```

    Writing foo.py



```python
%run foo.py
```

    Arguments:  ['foo.py']



```python
%run foo.py -v foo blabababa
```

    Arguments:  ['foo.py', '-v', 'foo', 'blabababa']



```python
!rm foo.py
```

### Input and Output Streams


```python
%%writefile foo.py

import sys

print('STATUS: Reading from stdin', file=sys.stderr)
 # stdinは普通input,でもpipelineを経由で他のプログラムから取得できる
data = sys.stdin.read()

print('STATUS: Writing data to stdout', file=sys.stderr)

sys.stdout.write(data)　# pipelineへ渡ることができる
sys.stdout.flush()

print('STATUS: Done', file=sys.stderr)
```

    Writing foo.py



```python
!cat foo.py | python3 -u foo.py
```

    STATUS: Reading from stdin
    STATUS: Writing data to stdout
    
    import sys
    
    print('STATUS: Reading from stdin', file=sys.stderr)
    
    data = sys.stdin.read()
    
    print('STATUS: Writing data to stdout', file=sys.stderr)
    
    sys.stdout.write(data)
    sys.stdout.flush()
    
    print('STATUS: Done', file=sys.stderr)
    STATUS: Done



```python
!rm foo.py
```

### Returning Status


```python
%%writefile foo.py

import sys

exit_code = int(sys.argv[1])
sys.exit(exit_code)
```

    Writing foo.py



```python
!python3 foo.py 0; echo "Exited $?"
```

    Exited 0



```python
!python3 foo.py 1; echo "Exited $?"
```

    Exited 1



```python
!rm foo.py
```

## メモリ管理と限界値

### 参照カウント


```python
import sys

one = []
print('At start         :', sys.getrefcount(one))

two = one

print('Second reference :', sys.getrefcount(one))

del two

print('After del        :', sys.getrefcount(one))
```

    At start         : 2
    Second reference : 3
    After del        : 2


> 0になったら`garbage collector(gc)`によりメモリから削除される

### オブジェクト大きさ


```python
import sys


class MyClass:
    pass


objects = [
    [], (), {}, 'c', 'string', b'bytes', 1, 2.3,
    MyClass, MyClass(),
]

for obj in objects:
    print(f'{type(obj).__name__:>10} : {sys.getsizeof(obj)}') # 単位: Bytes
```

          list : 56
         tuple : 40
          dict : 64
           str : 50
           str : 55
         bytes : 38
           int : 28
         float : 24
          type : 1064
       MyClass : 48



```python
import sys


class WithoutAttributes:
    pass


class WithAttributes:
    def __init__(self):
        self.a = 'a'
        self.b = 'b'
        return


without_attrs = WithoutAttributes()
print('WithoutAttributes:', sys.getsizeof(without_attrs))

with_attrs = WithAttributes()
print('WithAttributes:', sys.getsizeof(with_attrs))
```

    WithoutAttributes: 48
    WithAttributes: 48


> 属性は計算されていないのため間違った結果となる


```python
import sys


class WithAttributes:
    def __init__(self):
        self.a = 'a'
        self.b = 'b'
        return

    def __sizeof__(self):
        return object.__sizeof__(self) + \
            sum(sys.getsizeof(v) for v in self.__dict__.values())

my_inst = WithAttributes()
print(sys.getsizeof(my_inst))
```

    148


### 再帰


```python
import sys

print('Initial limit:', sys.getrecursionlimit())

sys.setrecursionlimit(56)

print('Modified limit:', sys.getrecursionlimit())


def generate_recursion_error(i):
    print(f'generate_recursion_error({i})')
    generate_recursion_error(i + 1)


try:
    generate_recursion_error(1)
except RuntimeError as err:
    print('Caught exception:', err)
```

    Initial limit: 3000
    Modified limit: 56
    generate_recursion_error(1)
    generate_recursion_error(2)
    generate_recursion_error(3)
    generate_recursion_error(4)
    generate_recursion_error(5)
    generate_recursion_error(6)
    generate_recursion_error(7)
    generate_recursion_error(8)
    generate_recursion_error(9)
    generate_recursion_error(10)
    generate_recursion_error(11)
    generate_recursion_error(12)
    generate_recursion_error(13)
    Caught exception: maximum recursion depth exceeded while calling a Python object


### 最大値


```python
import sys
import math

print('maxsize   :', math.log(sys.maxsize, 2))
print('maxunicode:', sys.maxunicode)
print('int_info  :', sys.int_info)
```

    maxsize   : 63.0
    maxunicode: 1114111
    int_info  : sys.int_info(bits_per_digit=30, sizeof_digit=4)


### Floating Point Values


```python
import sys

print('Smallest difference (epsilon):', sys.float_info.epsilon)
print()
print('Digits (dig)              :', sys.float_info.dig)
print('Mantissa digits (mant_dig):', sys.float_info.mant_dig)
print()
print('Maximum (max):', sys.float_info.max)
print('Minimum (min):', sys.float_info.min)
print()
print('Radix of exponents (radix):', sys.float_info.radix)
print()
print('Maximum exponent for radix (max_exp):',
      sys.float_info.max_exp)
print('Minimum exponent for radix (min_exp):',
      sys.float_info.min_exp)
print()
print('Max. exponent power of 10 (max_10_exp):',
      sys.float_info.max_10_exp)
print('Min. exponent power of 10 (min_10_exp):',
      sys.float_info.min_10_exp)
print()
print('Rounding for addition (rounds):', sys.float_info.rounds)
```

    Smallest difference (epsilon): 2.220446049250313e-16
    
    Digits (dig)              : 15
    Mantissa digits (mant_dig): 53
    
    Maximum (max): 1.7976931348623157e+308
    Minimum (min): 2.2250738585072014e-308
    
    Radix of exponents (radix): 2
    
    Maximum exponent for radix (max_exp): 1024
    Minimum exponent for radix (min_exp): -1021
    
    Max. exponent power of 10 (max_10_exp): 308
    Min. exponent power of 10 (min_10_exp): -307
    
    Rounding for addition (rounds): 1


### 整数値


```python
import sys

print('Number of bits used to hold each digit:',
      sys.int_info.bits_per_digit)
print('Size in bytes of C type used to hold each digit:',
      sys.int_info.sizeof_digit)
```

    Number of bits used to hold each digit: 30
    Size in bytes of C type used to hold each digit: 4


## Modules and Imports

### Imported Modules


```python
import sys
import textwrap

names = sorted(sys.modules.keys())
name_text = ', '.join(names)

print(textwrap.fill(name_text, width=64))
```

    IPython, IPython.core, IPython.core.alias,
    IPython.core.application, IPython.core.async_helpers,
    IPython.core.autocall, IPython.core.builtin_trap,
    IPython.core.compilerop, IPython.core.completer,
    IPython.core.completerlib, IPython.core.crashhandler,
    IPython.core.debugger, IPython.core.display,
    IPython.core.display_trap, IPython.core.displayhook,
    IPython.core.displaypub, IPython.core.error,
    IPython.core.events, IPython.core.excolors,
    IPython.core.extensions, IPython.core.formatters,
    IPython.core.getipython, IPython.core.history,
    IPython.core.hooks, IPython.core.inputtransformer2,
    IPython.core.interactiveshell, IPython.core.latex_symbols,
    IPython.core.logger, IPython.core.macro, IPython.core.magic,
    IPython.core.magic_arguments, IPython.core.magics,
    IPython.core.magics.auto, IPython.core.magics.basic,
    IPython.core.magics.code, IPython.core.magics.config,
    IPython.core.magics.display, IPython.core.magics.execution,
    IPython.core.magics.extension, IPython.core.magics.history,
    IPython.core.magics.logging, IPython.core.magics.namespace,
    IPython.core.magics.osm, IPython.core.magics.packaging,
    IPython.core.magics.pylab, IPython.core.magics.script,
    IPython.core.oinspect, IPython.core.page, IPython.core.payload,
    IPython.core.payloadpage, IPython.core.prefilter,
    IPython.core.profiledir, IPython.core.pylabtools,
    IPython.core.release, IPython.core.shellapp,
    IPython.core.splitinput, IPython.core.ultratb,
    IPython.core.usage, IPython.display, IPython.extensions,
    IPython.extensions.storemagic, IPython.lib,
    IPython.lib.backgroundjobs, IPython.lib.clipboard,
    IPython.lib.display, IPython.lib.pretty, IPython.lib.security,
    IPython.paths, IPython.terminal, IPython.terminal.debugger,
    IPython.terminal.embed, IPython.terminal.interactiveshell,
    IPython.terminal.ipapp, IPython.terminal.magics,
    IPython.terminal.prompts, IPython.terminal.pt_inputhooks,
    IPython.terminal.ptutils, IPython.terminal.shortcuts,
    IPython.testing, IPython.testing.skipdoctest, IPython.utils,
    IPython.utils.PyColorize, IPython.utils._process_common,
    IPython.utils._process_posix, IPython.utils._sysinfo,
    IPython.utils.capture, IPython.utils.colorable,
    IPython.utils.coloransi, IPython.utils.contexts,
    IPython.utils.data, IPython.utils.decorators,
    IPython.utils.dir2, IPython.utils.encoding, IPython.utils.frame,
    IPython.utils.generics, IPython.utils.importstring,
    IPython.utils.io, IPython.utils.ipstruct,
    IPython.utils.module_paths, IPython.utils.openpy,
    IPython.utils.path, IPython.utils.process,
    IPython.utils.py3compat, IPython.utils.sentinel,
    IPython.utils.strdispatch, IPython.utils.sysinfo,
    IPython.utils.syspathcontext, IPython.utils.tempdir,
    IPython.utils.terminal, IPython.utils.text,
    IPython.utils.timing, IPython.utils.tokenutil,
    IPython.utils.wildcard, __future__, __main__, _abc, _ast,
    _asyncio, _bisect, _blake2, _bootlocale, _bz2, _codecs,
    _collections, _collections_abc, _compat_pickle, _compression,
    _contextvars, _ctypes, _curses, _cython_0_29_21, _datetime,
    _decimal, _frozen_importlib, _frozen_importlib_external,
    _functools, _hashlib, _heapq, _imp, _io, _json, _locale,
    _lsprof, _lzma, _opcode, _operator, _osx_support, _pickle,
    _posixsubprocess, _queue, _random, _scproxy, _sha3, _sha512,
    _signal, _sitebuiltins, _socket, _sqlite3, _sre, _ssl, _stat,
    _string, _strptime, _struct, _sysconfigdata__darwin_darwin,
    _thread, _uuid, _warnings, _weakref, _weakrefset, abc, appnope,
    appnope._nope, argparse, array, ast, asyncio,
    asyncio.base_events, asyncio.base_futures,
    asyncio.base_subprocess, asyncio.base_tasks, asyncio.constants,
    asyncio.coroutines, asyncio.events, asyncio.exceptions,
    asyncio.format_helpers, asyncio.futures, asyncio.locks,
    asyncio.log, asyncio.protocols, asyncio.queues, asyncio.runners,
    asyncio.selector_events, asyncio.sslproto, asyncio.staggered,
    asyncio.streams, asyncio.subprocess, asyncio.tasks,
    asyncio.transports, asyncio.trsock, asyncio.unix_events, atexit,
    backcall, backcall.backcall, base64, bdb, binascii, bisect,
    builtins, bz2, cProfile, calendar, cmd, code, codecs, codeop,
    collections, collections.abc, colorsys, concurrent,
    concurrent.futures, concurrent.futures._base, contextlib,
    contextvars, copy, copyreg, ctypes, ctypes._endian,
    ctypes.macholib, ctypes.macholib.dyld, ctypes.macholib.dylib,
    ctypes.macholib.framework, ctypes.util, curses, cython_runtime,
    datetime, dateutil, dateutil._common, dateutil._version,
    dateutil.parser, dateutil.parser._parser,
    dateutil.parser.isoparser, dateutil.relativedelta, dateutil.tz,
    dateutil.tz._common, dateutil.tz._factories, dateutil.tz.tz,
    decimal, decorator, difflib, dis, distutils, distutils.debug,
    distutils.dep_util, distutils.errors, distutils.log,
    distutils.spawn, distutils.util, distutils.version, email,
    email._encoded_words, email._parseaddr, email._policybase,
    email.base64mime, email.charset, email.encoders, email.errors,
    email.feedparser, email.header, email.iterators, email.message,
    email.parser, email.quoprimime, email.utils, encodings,
    encodings.aliases, encodings.latin_1, encodings.utf_8, enum,
    errno, faulthandler, fcntl, filecmp, fnmatch, functools, gc,
    genericpath, getopt, getpass, gettext, glob, grp, hashlib,
    heapq, hmac, html, html.entities, http, http.client, imp,
    importlib, importlib._bootstrap, importlib._bootstrap_external,
    importlib.abc, importlib.machinery, importlib.util, inspect, io,
    ipykernel, ipykernel._version, ipykernel.codeutil,
    ipykernel.comm, ipykernel.comm.comm, ipykernel.comm.manager,
    ipykernel.connect, ipykernel.datapub, ipykernel.displayhook,
    ipykernel.eventloops, ipykernel.heartbeat, ipykernel.iostream,
    ipykernel.ipkernel, ipykernel.jsonutil, ipykernel.kernelapp,
    ipykernel.kernelbase, ipykernel.parentpoller,
    ipykernel.pickleutil, ipykernel.serialize, ipykernel.zmqshell,
    ipython_genutils, ipython_genutils._version,
    ipython_genutils.encoding, ipython_genutils.importstring,
    ipython_genutils.path, ipython_genutils.py3compat,
    ipython_genutils.text, itertools, jedi, jedi._compatibility,
    jedi.api, jedi.api.classes, jedi.api.completion,
    jedi.api.completion_cache, jedi.api.environment,
    jedi.api.errors, jedi.api.exceptions, jedi.api.file_name,
    jedi.api.helpers, jedi.api.interpreter, jedi.api.keywords,
    jedi.api.project, jedi.api.refactoring,
    jedi.api.refactoring.extract, jedi.api.strings, jedi.cache,
    jedi.common, jedi.debug, jedi.file_io, jedi.inference,
    jedi.inference.analysis, jedi.inference.arguments,
    jedi.inference.base_value, jedi.inference.cache,
    jedi.inference.compiled, jedi.inference.compiled.access,
    jedi.inference.compiled.getattr_static,
    jedi.inference.compiled.mixed,
    jedi.inference.compiled.subprocess,
    jedi.inference.compiled.subprocess.functions,
    jedi.inference.compiled.value, jedi.inference.context,
    jedi.inference.docstrings, jedi.inference.filters,
    jedi.inference.flow_analysis, jedi.inference.gradual,
    jedi.inference.gradual.annotation, jedi.inference.gradual.base,
    jedi.inference.gradual.conversion,
    jedi.inference.gradual.generics,
    jedi.inference.gradual.stub_value,
    jedi.inference.gradual.type_var,
    jedi.inference.gradual.typeshed, jedi.inference.gradual.typing,
    jedi.inference.gradual.utils, jedi.inference.helpers,
    jedi.inference.imports, jedi.inference.lazy_value,
    jedi.inference.names, jedi.inference.param,
    jedi.inference.parser_cache, jedi.inference.recursion,
    jedi.inference.references, jedi.inference.signature,
    jedi.inference.syntax_tree, jedi.inference.sys_path,
    jedi.inference.utils, jedi.inference.value,
    jedi.inference.value.decorator,
    jedi.inference.value.dynamic_arrays,
    jedi.inference.value.function, jedi.inference.value.instance,
    jedi.inference.value.iterable, jedi.inference.value.klass,
    jedi.inference.value.module, jedi.parser_utils, jedi.plugins,
    jedi.plugins.django, jedi.plugins.flask, jedi.plugins.pytest,
    jedi.plugins.registry, jedi.plugins.stdlib, jedi.settings, json,
    json.decoder, json.encoder, json.scanner, jupyter_client,
    jupyter_client._version, jupyter_client.adapter,
    jupyter_client.asynchronous,
    jupyter_client.asynchronous.channels,
    jupyter_client.asynchronous.client, jupyter_client.blocking,
    jupyter_client.blocking.channels,
    jupyter_client.blocking.client, jupyter_client.channels,
    jupyter_client.channelsabc, jupyter_client.client,
    jupyter_client.clientabc, jupyter_client.connect,
    jupyter_client.jsonutil, jupyter_client.kernelspec,
    jupyter_client.launcher, jupyter_client.localinterfaces,
    jupyter_client.manager, jupyter_client.managerabc,
    jupyter_client.multikernelmanager, jupyter_client.session,
    jupyter_core, jupyter_core.paths, jupyter_core.version, keyword,
    linecache, locale, logging, logging.handlers, lzma, marshal,
    math, mimetypes, mpl_toolkits, ntpath, numbers, opcode,
    operator, os, os.path, parso, parso._compatibility, parso.cache,
    parso.file_io, parso.grammar, parso.normalizer, parso.parser,
    parso.pgen2, parso.pgen2.generator, parso.pgen2.grammar_parser,
    parso.python, parso.python.diff, parso.python.errors,
    parso.python.parser, parso.python.pep8, parso.python.prefix,
    parso.python.token, parso.python.tokenize, parso.python.tree,
    parso.tree, parso.utils, pathlib, pdb, pexpect,
    pexpect.exceptions, pexpect.expect, pexpect.pty_spawn,
    pexpect.run, pexpect.spawnbase, pexpect.utils, pickle,
    pickleshare, pkgutil, platform, plistlib, posix, posixpath,
    pprint, profile, prompt_toolkit, prompt_toolkit.application,
    prompt_toolkit.application.application,
    prompt_toolkit.application.current,
    prompt_toolkit.application.dummy,
    prompt_toolkit.application.run_in_terminal,
    prompt_toolkit.auto_suggest, prompt_toolkit.buffer,
    prompt_toolkit.cache, prompt_toolkit.clipboard,
    prompt_toolkit.clipboard.base,
    prompt_toolkit.clipboard.in_memory, prompt_toolkit.completion,
    prompt_toolkit.completion.base,
    prompt_toolkit.completion.filesystem,
    prompt_toolkit.completion.fuzzy_completer,
    prompt_toolkit.completion.nested,
    prompt_toolkit.completion.word_completer,
    prompt_toolkit.data_structures, prompt_toolkit.document,
    prompt_toolkit.enums, prompt_toolkit.eventloop,
    prompt_toolkit.eventloop.async_generator,
    prompt_toolkit.eventloop.inputhook,
    prompt_toolkit.eventloop.utils, prompt_toolkit.filters,
    prompt_toolkit.filters.app, prompt_toolkit.filters.base,
    prompt_toolkit.filters.cli, prompt_toolkit.filters.utils,
    prompt_toolkit.formatted_text,
    prompt_toolkit.formatted_text.ansi,
    prompt_toolkit.formatted_text.base,
    prompt_toolkit.formatted_text.html,
    prompt_toolkit.formatted_text.pygments,
    prompt_toolkit.formatted_text.utils, prompt_toolkit.history,
    prompt_toolkit.input,
    prompt_toolkit.input.ansi_escape_sequences,
    prompt_toolkit.input.base, prompt_toolkit.input.defaults,
    prompt_toolkit.input.typeahead,
    prompt_toolkit.input.vt100_parser, prompt_toolkit.key_binding,
    prompt_toolkit.key_binding.bindings,
    prompt_toolkit.key_binding.bindings.auto_suggest,
    prompt_toolkit.key_binding.bindings.basic,
    prompt_toolkit.key_binding.bindings.completion,
    prompt_toolkit.key_binding.bindings.cpr,
    prompt_toolkit.key_binding.bindings.emacs,
    prompt_toolkit.key_binding.bindings.focus,
    prompt_toolkit.key_binding.bindings.mouse,
    prompt_toolkit.key_binding.bindings.named_commands,
    prompt_toolkit.key_binding.bindings.open_in_editor,
    prompt_toolkit.key_binding.bindings.page_navigation,
    prompt_toolkit.key_binding.bindings.scroll,
    prompt_toolkit.key_binding.bindings.vi,
    prompt_toolkit.key_binding.defaults,
    prompt_toolkit.key_binding.digraphs,
    prompt_toolkit.key_binding.emacs_state,
    prompt_toolkit.key_binding.key_bindings,
    prompt_toolkit.key_binding.key_processor,
    prompt_toolkit.key_binding.vi_state, prompt_toolkit.keys,
    prompt_toolkit.layout, prompt_toolkit.layout.containers,
    prompt_toolkit.layout.controls, prompt_toolkit.layout.dimension,
    prompt_toolkit.layout.dummy, prompt_toolkit.layout.layout,
    prompt_toolkit.layout.margins, prompt_toolkit.layout.menus,
    prompt_toolkit.layout.mouse_handlers,
    prompt_toolkit.layout.processors, prompt_toolkit.layout.screen,
    prompt_toolkit.layout.utils, prompt_toolkit.lexers,
    prompt_toolkit.lexers.base, prompt_toolkit.lexers.pygments,
    prompt_toolkit.mouse_events, prompt_toolkit.output,
    prompt_toolkit.output.base, prompt_toolkit.output.color_depth,
    prompt_toolkit.output.defaults, prompt_toolkit.output.vt100,
    prompt_toolkit.patch_stdout, prompt_toolkit.renderer,
    prompt_toolkit.search, prompt_toolkit.selection,
    prompt_toolkit.shortcuts, prompt_toolkit.shortcuts.dialogs,
    prompt_toolkit.shortcuts.progress_bar,
    prompt_toolkit.shortcuts.progress_bar.base,
    prompt_toolkit.shortcuts.progress_bar.formatters,
    prompt_toolkit.shortcuts.prompt, prompt_toolkit.shortcuts.utils,
    prompt_toolkit.styles, prompt_toolkit.styles.base,
    prompt_toolkit.styles.defaults,
    prompt_toolkit.styles.named_colors,
    prompt_toolkit.styles.pygments, prompt_toolkit.styles.style,
    prompt_toolkit.styles.style_transformation,
    prompt_toolkit.utils, prompt_toolkit.validation,
    prompt_toolkit.widgets, prompt_toolkit.widgets.base,
    prompt_toolkit.widgets.dialogs, prompt_toolkit.widgets.menus,
    prompt_toolkit.widgets.toolbars, pstats, pty, ptyprocess,
    ptyprocess.ptyprocess, ptyprocess.util, pwd, pydoc, pydoc_data,
    pydoc_data.topics, pyexpat, pyexpat.errors, pyexpat.model,
    pygments, pygments.filter, pygments.filters, pygments.formatter,
    pygments.formatters, pygments.formatters._mapping,
    pygments.formatters.html, pygments.lexer, pygments.lexers,
    pygments.lexers._mapping, pygments.lexers.python,
    pygments.modeline, pygments.plugin, pygments.regexopt,
    pygments.style, pygments.styles, pygments.token,
    pygments.unistring, pygments.util, queue, quopri, random, re,
    reprlib, resource, runpy, select, selectors, shlex, shutil,
    signal, site, six, six.moves, socket, sqlite3, sqlite3.dbapi2,
    sre_compile, sre_constants, sre_parse, ssl, stat, storemagic,
    string, struct, subprocess, sys, sysconfig, tempfile, termios,
    textwrap, threading, time, timeit, token, tokenize, tornado,
    tornado.concurrent, tornado.escape, tornado.gen, tornado.ioloop,
    tornado.locks, tornado.log, tornado.platform,
    tornado.platform.asyncio, tornado.queues, tornado.speedups,
    tornado.util, traceback, traitlets, traitlets._version,
    traitlets.config, traitlets.config.application,
    traitlets.config.configurable, traitlets.config.loader,
    traitlets.log, traitlets.traitlets, traitlets.utils,
    traitlets.utils.bunch, traitlets.utils.decorators,
    traitlets.utils.descriptions, traitlets.utils.getargspec,
    traitlets.utils.importstring, traitlets.utils.sentinel, tty,
    types, typing, typing.io, typing.re, unicodedata, urllib,
    urllib.error, urllib.parse, urllib.request, urllib.response, uu,
    uuid, warnings, wcwidth, wcwidth.table_wide, wcwidth.table_zero,
    wcwidth.unicode_versions, wcwidth.wcwidth, weakref, xml,
    xml.dom, xml.dom.NodeFilter, xml.dom.domreg, xml.dom.minicompat,
    xml.dom.minidom, xml.dom.xmlbuilder, xml.parsers,
    xml.parsers.expat, xml.parsers.expat.errors,
    xml.parsers.expat.model, zipimport, zlib, zmq, zmq._future,
    zmq.asyncio, zmq.backend, zmq.backend.cython,
    zmq.backend.cython._device, zmq.backend.cython._poll,
    zmq.backend.cython._proxy_steerable,
    zmq.backend.cython._version, zmq.backend.cython.constants,
    zmq.backend.cython.context, zmq.backend.cython.error,
    zmq.backend.cython.message, zmq.backend.cython.socket,
    zmq.backend.cython.utils, zmq.backend.select, zmq.error,
    zmq.eventloop, zmq.eventloop.ioloop, zmq.eventloop.zmqstream,
    zmq.libzmq, zmq.sugar, zmq.sugar.attrsettr, zmq.sugar.constants,
    zmq.sugar.context, zmq.sugar.frame, zmq.sugar.poll,
    zmq.sugar.socket, zmq.sugar.stopwatch, zmq.sugar.tracker,
    zmq.sugar.version, zmq.utils, zmq.utils.constant_names,
    zmq.utils.jsonapi, zmq.utils.strtypes


### Built-in Modules


```python
import sys
import textwrap

name_text = ', '.join(sorted(sys.builtin_module_names))

print(textwrap.fill(name_text, width=64))
```

    _abc, _ast, _codecs, _collections, _functools, _imp, _io,
    _locale, _operator, _signal, _sre, _stat, _string, _symtable,
    _thread, _tracemalloc, _warnings, _weakref, atexit, builtins,
    errno, faulthandler, gc, itertools, marshal, posix, pwd, sys,
    time, xxsubtype


### Import Path


```python
import sys

for d in sys.path:
    print(d)
```

    /Users/maozhongfu/GitHub/Python/Runtime Features
    /Users/maozhongfu/.vscode/extensions/ms-python.python-2020.10.332292344/pythonFiles
    /Users/maozhongfu/.vscode/extensions/ms-python.python-2020.10.332292344/pythonFiles/lib/python
    /Library/Frameworks/Python.framework/Versions/3.8/lib/python38.zip
    /Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8
    /Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8/lib-dynload
    
    /Users/maozhongfu/Library/Python/3.8/lib/python/site-packages
    /Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8/site-packages
    /Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8/site-packages/aeosa
    /Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8/site-packages/IPython/extensions
    /Users/maozhongfu/.ipython



```python

```
