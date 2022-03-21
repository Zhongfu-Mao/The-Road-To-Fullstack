[🔗pip官方文档](https://pip.pypa.io/en/stable/)


```python
from IPython.display import HTML
```


```python
HTML(
"""
<table style="border: 2px solid black;">
    <tr>
        <th style="text-align:center;">分類</th>
        <th style="text-align:center;">コマンド</th>
        <th style="text-align:center;">説明</th>
    </tr>
    <tr>
        <td rowspan="4" style="text-align:center;">サーチ</td>
        <td style="text-align:left;">pip list</td>
        <td style="text-align:left;">インストール済みパッケージ一覧</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip search pkg</td>
        <td style="text-align:left;"><strong>pypi</strong>にて特定のpackageをサーチ</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip show pkd</td>
        <td style="text-align:left;">パッケージの詳細</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip list　--outdated</td>
        <td style="text-align:left;">アップデートできるパッケージ一覧</td>
    </tr>
    <tr>
        <td rowspan="4">ダウンロード</td>
        <td style="text-align:left;">pip download pkg</td>
        <td style="text-align:left;">現在のフォルダーに保存</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download pkg --destination-directory path</td>
        <td style="text-align:left;">パスを指定</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download -r requirements.txt</td>
        <td style="text-align:left;">配置ファイルを利用</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download --destination-directory path -r requirements.txt</td>
        <td style="text-align:left;">結合して利用</td>
    </tr>
    <tr>
        <td rowspan="11">インストール</td>
        <td style="text-align:left;">pip install pkg</td>
        <td style="text-align:left;">最新版をインストール</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --no-index --find-links=path pkg</td>
        <td style="text-align:left;">ローカルからインストール</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg==x.x.xx</td>
        <td style="text-align:left;">x.x.xxのバージョンを指定</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg>=x.x.xx</td>
        <td style="text-align:left;">x.x.xx以上のバージョンを指定</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg<=x.x.xx</td>
        <td style="text-align:left;">x.x.xx以下のバージョンを指定</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install -r requirement.txt</td>
        <td style="text-align:left;">配置ファイルを利用</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg.zip</td>
        <td style="text-align:left;">wheelを使用しない</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --user pkg</td>
        <td style="text-align:left;">現在のユーザーだけのためにインストール</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --default-timeout=seconds pkg</td>
        <td style="text-align:left;">待つ時間を延長</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --proxy [user:passwd]@http_server_ip:port <pkg name></td>
        <td style="text-align:left;">プロキシ</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install git+https://github.com/user-name/repository-name@branch-name</td>
        <td style="text-align:left;">GitHubから</td>
    </tr>
    <tr>
        <td style="text-align:center;">アンインストール</td>
        <td style="text-align:left;">pip uninstall pkg</td>
        <td style="text-align:left;"></td>
    </tr>
    <tr>
        <td style="text-align:center;">アップグレード</td>
        <td style="text-align:left;">pip install --upgrade pkg</td>
        <td style="text-align:left;"></td>
    </tr>
</table>
"""
)
```





<table style="border: 2px solid black;">
    <tr>
        <th style="text-align:center;">分類</th>
        <th style="text-align:center;">コマンド</th>
        <th style="text-align:center;">説明</th>
    </tr>
    <tr>
        <td rowspan="4" style="text-align:center;">サーチ</td>
        <td style="text-align:left;">pip list</td>
        <td style="text-align:left;">インストール済みパッケージ一覧</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip search pkg</td>
        <td style="text-align:left;"><strong>pypi</strong>にて特定のpackageをサーチ</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip show pkd</td>
        <td style="text-align:left;">パッケージの詳細</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip list　--outdated</td>
        <td style="text-align:left;">アップデートできるパッケージ一覧</td>
    </tr>
    <tr>
        <td rowspan="4">ダウンロード</td>
        <td style="text-align:left;">pip download pkg</td>
        <td style="text-align:left;">現在のフォルダーに保存</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download pkg --destination-directory path</td>
        <td style="text-align:left;">パスを指定</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download -r requirements.txt</td>
        <td style="text-align:left;">配置ファイルを利用</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download --destination-directory path -r requirements.txt</td>
        <td style="text-align:left;">結合して利用</td>
    </tr>
    <tr>
        <td rowspan="11">インストール</td>
        <td style="text-align:left;">pip install pkg</td>
        <td style="text-align:left;">最新版をインストール</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --no-index --find-links=path pkg</td>
        <td style="text-align:left;">ローカルからインストール</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg==x.x.xx</td>
        <td style="text-align:left;">x.x.xxのバージョンを指定</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg>=x.x.xx</td>
        <td style="text-align:left;">x.x.xx以上のバージョンを指定</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg<=x.x.xx</td>
        <td style="text-align:left;">x.x.xx以下のバージョンを指定</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install -r requirement.txt</td>
        <td style="text-align:left;">配置ファイルを利用</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg.zip</td>
        <td style="text-align:left;">wheelを使用しない</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --user pkg</td>
        <td style="text-align:left;">現在のユーザーだけのためにインストール</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --default-timeout=seconds pkg</td>
        <td style="text-align:left;">待つ時間を延長</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --proxy [user:passwd]@http_server_ip:port <pkg name></td>
        <td style="text-align:left;">プロキシ</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install git+https://github.com/user-name/repository-name@branch-name</td>
        <td style="text-align:left;">GitHubから</td>
    </tr>
    <tr>
        <td style="text-align:center;">アンインストール</td>
        <td style="text-align:left;">pip uninstall pkg</td>
        <td style="text-align:left;"></td>
    </tr>
    <tr>
        <td style="text-align:center;">アップグレード</td>
        <td style="text-align:left;">pip install --upgrade pkg</td>
        <td style="text-align:left;"></td>
    </tr>
</table>




## コマンド一覧


```python
!pip
```

    
    Usage:   
      pip <command> [options]
    
    Commands:
      install                     Install packages.
      download                    Download packages.
      uninstall                   Uninstall packages.
      freeze                      Output installed packages in requirements format.
      list                        List installed packages.
      show                        Show information about installed packages.
      check                       Verify installed packages have compatible dependencies.
      config                      Manage local and global configuration.
      search                      Search PyPI for packages.
      cache                       Inspect and manage pip's wheel cache.
      wheel                       Build wheels from your requirements.
      hash                        Compute hashes of package archives.
      completion                  A helper command used for command completion.
      debug                       Show information useful for debugging.
      help                        Show help for commands.
    
    General Options:
      -h, --help                  Show help.
      --isolated                  Run pip in an isolated mode, ignoring
                                  environment variables and user configuration.
      -v, --verbose               Give more output. Option is additive, and can be
                                  used up to 3 times.
      -V, --version               Show version and exit.
      -q, --quiet                 Give less output. Option is additive, and can be
                                  used up to 3 times (corresponding to WARNING,
                                  ERROR, and CRITICAL logging levels).
      --log <path>                Path to a verbose appending log.
      --no-input                  Disable prompting for input.
      --proxy <proxy>             Specify a proxy in the form
                                  [user:passwd@]proxy.server:port.
      --retries <retries>         Maximum number of retries each connection should
                                  attempt (default 5 times).
      --timeout <sec>             Set the socket timeout (default 15 seconds).
      --exists-action <action>    Default action when a path already exists:
                                  (s)witch, (i)gnore, (w)ipe, (b)ackup, (a)bort.
      --trusted-host <hostname>   Mark this host or host:port pair as trusted,
                                  even though it does not have valid or any HTTPS.
      --cert <path>               Path to alternate CA bundle.
      --client-cert <path>        Path to SSL client certificate, a single file
                                  containing the private key and the certificate
                                  in PEM format.
      --cache-dir <dir>           Store the cache data in <dir>.
      --no-cache-dir              Disable the cache.
      --disable-pip-version-check
                                  Don't periodically check PyPI to determine
                                  whether a new version of pip is available for
                                  download. Implied with --no-index.
      --no-color                  Suppress colored output
      --no-python-version-warning
                                  Silence deprecation warnings for upcoming
                                  unsupported Pythons.
      --use-feature <feature>     Enable new functionality, that may be backward
                                  incompatible.
      --use-deprecated <feature>  Enable deprecated functionality, that will be
                                  removed in the future.


## packageをサーチする

### 現在の環境にインストールされるpackageの一覧表
```python
pip list
```


```python
!pip list
```

### `pypi`にて特定のpackageをサーチする
```python
pip search <pkg name>
```
[pypi](https://pypi.org)


```python
!pip search <pkg name>
```

### 現在の環境にインストールされるpackageの中アップデートできるものの一覧
```python
pip list --out-dated
```


```python
!pip list --out-dated
```

### packageの詳細を確認する
```python
pip show <pkg name>
```


```python
!pip show <pkg name>
```

> `Location`が実際にパッケージがインストールされているファイルシステム上の場所（パス）

## packageをダウンロードする

### packageをインストールせずにダウンロードする
```python
pip download <pkg name> # 現在のフォルダーに保存する
pip download <pkg name> --destination-directory <path> # 指定のパスに保存する
pip download -r requirements.txt # 配置ファイルを利用する
pip download --destination-directory <path> -r requirements.txt # 結合して利用する
```


```python
!pip download <pkg name>
```


```python
!pip download <pkg name> --destination-directory <path>
```


```python
%%writefile requirements.txt
pandas # 一つの例として
```


```python
!pip download -r requirements.txt
```


```python
!pip download <pkg name> --destination-directory <path> -r requirements.txt
```


```python
!rm requirements.txt *.whl
```

## [requirements.txtの書き方](https://note.nkmk.me/python-pip-install-requirements/)

[pip install - Example Requirements File](https://pip.pypa.io/en/latest/reference/pip_install/#example-requirements-file)

```python
####### example-requirements.txt #######
#
###### Requirements without Version Specifiers ######
nose
nose-cov
beautifulsoup4
#
###### Requirements with Version Specifiers ######
#   See https://www.python.org/dev/peps/pep-0440/#version-specifiers
docopt == 0.6.1             # Version Matching. Must be version 0.6.1
keyring >= 4.1.1            # Minimum version 4.1.1
coverage != 3.5             # Version Exclusion. Anything except version 3.5
Mopidy-Dirble ~= 1.1        # Compatible release. Same as >= 1.1, == 1.*
```

* Pythonのコードと同じく#以降はコメント
* ==や>, >=, <, <=などでバージョンを指定できる
* バージョン指定を省略すると最新版がインストールされる
* カンマ,で区切ると二つの条件をANDで指定できる

`pip freeze`コマンドで現在の環境にインストールされたパッケージとバージョンが`pip install -r`で使える設定ファイルの形式で出力


```python
!pip freeze
```

したがって、`pip freeze`をリダイレクト`>`でファイルに出力すれば、  
そのファイルを使って元の環境と同じバージョンのパッケージを別環境に一括でインストールできる


```python
!pip freeze > requirements.txt
```

## インストール

普段の場合は、  `pip install <pkg name>`で`pypi`からサーチしてインストールできる

### ローカルから
```python
pip install --no-index --find-links=<path> <pkg name>
```


```python
!pip install --no-index --find-links=<path> <pkg name>
```

### バージョンを指定するのは上に`requirements.txtの書き方`の部分と同じ

### バイナリファイルを利用しない(OSに依存しない)


普通ダウンロードやインストールする時、`whl`ファイルを利用  
`whl`ファイルの正体は`py`ファイルとコンパイル済みの`pyd`ファイルの**zip**ファイルである  
[PEP427](https://www.python.org/dev/peps/pep-0427/)で定義された  
コンパイル済みのため、プラットフォームに依存する  
そこで、非バイナリファイルの登場

例えば、自分は*MacOS*、*python3.8.6*で*numpy*をダウンロードしたら`pip download numpy`を実行後、  
`numpy-1.19.3-cp38-cp38-macosx_10_9_x86_64.whl`というファイルをゲットする  
このファイルは*Windows*や*Linux*にてインストールできない

`pip download --no-binary=:all: numpy`を実行すると、
```python
Collecting numpy
  Downloading numpy-1.19.3.zip (7.3 MB)
     |████████████████████████████████| 7.3 MB 4.7 MB/s 
?25h  Installing build dependencies ... ?25ldone
?25h  Getting requirements to build wheel ... ?25ldone
?25h    Preparing wheel metadata ... ?25ldone
?25h  Saved ./numpy-1.19.3.zip
Successfully downloaded numpy
```
`num-1.19.3.zip`ファイルがダウンロードされる、解凍すると、中身は以下となる
```bash
INSTALL.rst.txt       benchmarks            runtests.py
LICENSE.txt           doc                   setup.py
MANIFEST.in           doc_requirements.txt  site.cfg.example
PKG-INFO              numpy                 test_requirements.txt
README.md             pyproject.toml        tools
THANKS.txt            pytest.ini            tox.ini
```
インストールする時は、`pip install numpy-1.19.3.zip`のようにファイルを指定してインストール
```python
Processing ./numpy-1.19.3.zip
  Installing build dependencies ... ?25ldone
?25h  Getting requirements to build wheel ... ?25ldone
?25h    Preparing wheel metadata ... ?25ldone
?25hBuilding wheels for collected packages: numpy
  Building wheel for numpy (PEP 517) ... ?25ldone
?25h  Created wheel for numpy: filename=numpy-1.19.3-cp38-cp38-macosx_10_15_x86_64.whl size=4586582 sha256=e4e55141a3d91c9d00be8fe47493b9f1618c4445f0d02e9740c7ef148821f559
  Stored in directory: /Users/maozhongfu/Library/Caches/pip/wheels/ba/78/20/049274e9c87361903181a8e143ab946747bb34f4b6fc63544a
Successfully built numpy
Installing collected packages: numpy
  Attempting uninstall: numpy
    Found existing installation: numpy 1.19.2
    Uninstalling numpy-1.19.2:
      Successfully uninstalled numpy-1.19.2
ERROR: After October 2020 you may experience errors when installing or updating packages. This is because pip will change the way that it resolves dependency conflicts.

We recommend you use --use-feature=2020-resolver to test your packages with the new resolver before it becomes the default.

robotframework-ride 1.7.4.2 requires wxPython<=4.0.7.post2, but you'll have wxpython 4.1.0 which is incompatible.
Successfully installed numpy-1.19.3
```
ご覧の通り、`Building wheels for collected packages: numpy`  
コンパイルが必要(多少時間かかる)


### 特定のユーザに対してインストール(仮想環境の使用するいらない、これは普段使わない)
```python
pip install --user <pkg name>
```


```python
!pip install --user <pkg name>
```

### 待つ時間を延長(ネットワークが不安定な時使用)
```python
pip install --default-timeout=<seconds> <pkg name>
```


```python
!pip install --default-timeout=<seconds> <pkg name>
```

### プロキシを使用(外部のネットワークにアクセスできない時に使用)
```python
pip install --proxy [user:passwd]@http_server_ip:port <pkg name>
```
`SSL`の使用と同じ


```python
!pip install --proxy [user:passwd]@http_server_ip:port <pkg name>
```

### GitHubからインストール
```python
pip install git+<repository-url>
pip install git+https://github.com/<user-name>/<repository-name><@branch-name>

```

* `git+`をつけたインストールは、`git clone`してからインストールするため、システムにgitがインストールされている必要がある  
* GitHubではリリースページから各バージョンのリポジトリをzipでダウンロードできるようになっているので、  
  zipのURLを直接指定してもOK。この場合はgitがインストールされていなくてもOK

## アンインストール

```python
pip uninstall <pkg name>
```


```python
!pip uninstall <pkg name>
```

## アップグレード

```python
pip install --upgrade <pkg name>
```


```python
!pip install --upgrade <pkg name>
```

アップグレードの本質はアンインストールしてから最新版をインストール、  
故にコマンドは`install`のまま、パラメータとして`--upgrade`を追加した  
アップグレードする際、`--upgrade-strategy`というパラメータがある  
選択肢は二つ
* `eager`　依存パッケージ全部アップグレード
* `only-if-need`(default)　必要な時だけ依存パッケージをアップグレード

### バッチアップグレード


方法１：`pip-review`を使用

```bash
# アップグレードできるパッケージ一覧を確認
pip list  --outdated --format=columns
# バッチ処理
pip install pip-review
pip-review --local --interactive
```

方法２：Pythonスクリプトを使用
```python
import pip
from subprocess import call
from pip._internal.utils.misc import get_installed_distributions

for dist in get_installed_distributions():
    call("pip install --upgrade " + dist.project_name, shell=True)
```


## `pip.ini`ファイルを使用

毎回コマンドを打つ時は、パラメータを入力する必要(例えばSSL対応のための`--trusted-host`)が面倒臭いと思うなら  
`pip.ini`を利用すると便利

手順：
1. `win+r` -> `%APPDATA%`実行(C:\Users\xx\AppData を開く)
2. `pip`というフォルダがないなら、作る
3. `pip`フォルダの中に、`pip.ini`というファイルを作る
4. 編集する

```ini
[global]
index-url = <url> 　# pypiにアクセスづらい時に設定
proxy=<url> # 外部のネットワークにアクセスできない時に設定

[https]
verify=enable

[install]
trusted-host = pypi.python.org
               pypi.org
               files.pythonhosted.org　# SSL対応
find-links = <path>
```


```python

```
