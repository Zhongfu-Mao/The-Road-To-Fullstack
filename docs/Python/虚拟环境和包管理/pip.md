[ðpipå®æ¹ææ¡£](https://pip.pypa.io/en/stable/)


```python
from IPython.display import HTML
```


```python
HTML(
"""
<table style="border: 2px solid black;">
    <tr>
        <th style="text-align:center;">åé¡</th>
        <th style="text-align:center;">ã³ãã³ã</th>
        <th style="text-align:center;">èª¬æ</th>
    </tr>
    <tr>
        <td rowspan="4" style="text-align:center;">ãµã¼ã</td>
        <td style="text-align:left;">pip list</td>
        <td style="text-align:left;">ã¤ã³ã¹ãã¼ã«æ¸ã¿ããã±ã¼ã¸ä¸è¦§</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip search pkg</td>
        <td style="text-align:left;"><strong>pypi</strong>ã«ã¦ç¹å®ã®packageããµã¼ã</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip show pkd</td>
        <td style="text-align:left;">ããã±ã¼ã¸ã®è©³ç´°</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip listã--outdated</td>
        <td style="text-align:left;">ã¢ãããã¼ãã§ããããã±ã¼ã¸ä¸è¦§</td>
    </tr>
    <tr>
        <td rowspan="4">ãã¦ã³ã­ã¼ã</td>
        <td style="text-align:left;">pip download pkg</td>
        <td style="text-align:left;">ç¾å¨ã®ãã©ã«ãã¼ã«ä¿å­</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download pkg --destination-directory path</td>
        <td style="text-align:left;">ãã¹ãæå®</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download -r requirements.txt</td>
        <td style="text-align:left;">éç½®ãã¡ã¤ã«ãå©ç¨</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download --destination-directory path -r requirements.txt</td>
        <td style="text-align:left;">çµåãã¦å©ç¨</td>
    </tr>
    <tr>
        <td rowspan="11">ã¤ã³ã¹ãã¼ã«</td>
        <td style="text-align:left;">pip install pkg</td>
        <td style="text-align:left;">ææ°çãã¤ã³ã¹ãã¼ã«</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --no-index --find-links=path pkg</td>
        <td style="text-align:left;">ã­ã¼ã«ã«ããã¤ã³ã¹ãã¼ã«</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg==x.x.xx</td>
        <td style="text-align:left;">x.x.xxã®ãã¼ã¸ã§ã³ãæå®</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg>=x.x.xx</td>
        <td style="text-align:left;">x.x.xxä»¥ä¸ã®ãã¼ã¸ã§ã³ãæå®</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg<=x.x.xx</td>
        <td style="text-align:left;">x.x.xxä»¥ä¸ã®ãã¼ã¸ã§ã³ãæå®</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install -r requirement.txt</td>
        <td style="text-align:left;">éç½®ãã¡ã¤ã«ãå©ç¨</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg.zip</td>
        <td style="text-align:left;">wheelãä½¿ç¨ããªã</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --user pkg</td>
        <td style="text-align:left;">ç¾å¨ã®ã¦ã¼ã¶ã¼ã ãã®ããã«ã¤ã³ã¹ãã¼ã«</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --default-timeout=seconds pkg</td>
        <td style="text-align:left;">å¾ã¤æéãå»¶é·</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --proxy [user:passwd]@http_server_ip:port <pkg name></td>
        <td style="text-align:left;">ãã­ã­ã·</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install git+https://github.com/user-name/repository-name@branch-name</td>
        <td style="text-align:left;">GitHubãã</td>
    </tr>
    <tr>
        <td style="text-align:center;">ã¢ã³ã¤ã³ã¹ãã¼ã«</td>
        <td style="text-align:left;">pip uninstall pkg</td>
        <td style="text-align:left;"></td>
    </tr>
    <tr>
        <td style="text-align:center;">ã¢ããã°ã¬ã¼ã</td>
        <td style="text-align:left;">pip install --upgrade pkg</td>
        <td style="text-align:left;"></td>
    </tr>
</table>
"""
)
```





<table style="border: 2px solid black;">
    <tr>
        <th style="text-align:center;">åé¡</th>
        <th style="text-align:center;">ã³ãã³ã</th>
        <th style="text-align:center;">èª¬æ</th>
    </tr>
    <tr>
        <td rowspan="4" style="text-align:center;">ãµã¼ã</td>
        <td style="text-align:left;">pip list</td>
        <td style="text-align:left;">ã¤ã³ã¹ãã¼ã«æ¸ã¿ããã±ã¼ã¸ä¸è¦§</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip search pkg</td>
        <td style="text-align:left;"><strong>pypi</strong>ã«ã¦ç¹å®ã®packageããµã¼ã</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip show pkd</td>
        <td style="text-align:left;">ããã±ã¼ã¸ã®è©³ç´°</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip listã--outdated</td>
        <td style="text-align:left;">ã¢ãããã¼ãã§ããããã±ã¼ã¸ä¸è¦§</td>
    </tr>
    <tr>
        <td rowspan="4">ãã¦ã³ã­ã¼ã</td>
        <td style="text-align:left;">pip download pkg</td>
        <td style="text-align:left;">ç¾å¨ã®ãã©ã«ãã¼ã«ä¿å­</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download pkg --destination-directory path</td>
        <td style="text-align:left;">ãã¹ãæå®</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download -r requirements.txt</td>
        <td style="text-align:left;">éç½®ãã¡ã¤ã«ãå©ç¨</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip download --destination-directory path -r requirements.txt</td>
        <td style="text-align:left;">çµåãã¦å©ç¨</td>
    </tr>
    <tr>
        <td rowspan="11">ã¤ã³ã¹ãã¼ã«</td>
        <td style="text-align:left;">pip install pkg</td>
        <td style="text-align:left;">ææ°çãã¤ã³ã¹ãã¼ã«</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --no-index --find-links=path pkg</td>
        <td style="text-align:left;">ã­ã¼ã«ã«ããã¤ã³ã¹ãã¼ã«</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg==x.x.xx</td>
        <td style="text-align:left;">x.x.xxã®ãã¼ã¸ã§ã³ãæå®</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg>=x.x.xx</td>
        <td style="text-align:left;">x.x.xxä»¥ä¸ã®ãã¼ã¸ã§ã³ãæå®</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg<=x.x.xx</td>
        <td style="text-align:left;">x.x.xxä»¥ä¸ã®ãã¼ã¸ã§ã³ãæå®</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install -r requirement.txt</td>
        <td style="text-align:left;">éç½®ãã¡ã¤ã«ãå©ç¨</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install pkg.zip</td>
        <td style="text-align:left;">wheelãä½¿ç¨ããªã</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --user pkg</td>
        <td style="text-align:left;">ç¾å¨ã®ã¦ã¼ã¶ã¼ã ãã®ããã«ã¤ã³ã¹ãã¼ã«</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --default-timeout=seconds pkg</td>
        <td style="text-align:left;">å¾ã¤æéãå»¶é·</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install --proxy [user:passwd]@http_server_ip:port <pkg name></td>
        <td style="text-align:left;">ãã­ã­ã·</td>
    </tr>
    <tr>
        <td style="text-align:left;">pip install git+https://github.com/user-name/repository-name@branch-name</td>
        <td style="text-align:left;">GitHubãã</td>
    </tr>
    <tr>
        <td style="text-align:center;">ã¢ã³ã¤ã³ã¹ãã¼ã«</td>
        <td style="text-align:left;">pip uninstall pkg</td>
        <td style="text-align:left;"></td>
    </tr>
    <tr>
        <td style="text-align:center;">ã¢ããã°ã¬ã¼ã</td>
        <td style="text-align:left;">pip install --upgrade pkg</td>
        <td style="text-align:left;"></td>
    </tr>
</table>




## ã³ãã³ãä¸è¦§


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


## packageããµã¼ããã

### ç¾å¨ã®ç°å¢ã«ã¤ã³ã¹ãã¼ã«ãããpackageã®ä¸è¦§è¡¨
```python
pip list
```


```python
!pip list
```

### `pypi`ã«ã¦ç¹å®ã®packageããµã¼ããã
```python
pip search <pkg name>
```
[pypi](https://pypi.org)


```python
!pip search <pkg name>
```

### ç¾å¨ã®ç°å¢ã«ã¤ã³ã¹ãã¼ã«ãããpackageã®ä¸­ã¢ãããã¼ãã§ãããã®ã®ä¸è¦§
```python
pip list --out-dated
```


```python
!pip list --out-dated
```

### packageã®è©³ç´°ãç¢ºèªãã
```python
pip show <pkg name>
```


```python
!pip show <pkg name>
```

> `Location`ãå®éã«ããã±ã¼ã¸ãã¤ã³ã¹ãã¼ã«ããã¦ãããã¡ã¤ã«ã·ã¹ãã ä¸ã®å ´æï¼ãã¹ï¼

## packageããã¦ã³ã­ã¼ããã

### packageãã¤ã³ã¹ãã¼ã«ããã«ãã¦ã³ã­ã¼ããã
```python
pip download <pkg name> # ç¾å¨ã®ãã©ã«ãã¼ã«ä¿å­ãã
pip download <pkg name> --destination-directory <path> # æå®ã®ãã¹ã«ä¿å­ãã
pip download -r requirements.txt # éç½®ãã¡ã¤ã«ãå©ç¨ãã
pip download --destination-directory <path> -r requirements.txt # çµåãã¦å©ç¨ãã
```


```python
!pip download <pkg name>
```


```python
!pip download <pkg name> --destination-directory <path>
```


```python
%%writefile requirements.txt
pandas # ä¸ã¤ã®ä¾ã¨ãã¦
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

## [requirements.txtã®æ¸ãæ¹](https://note.nkmk.me/python-pip-install-requirements/)

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

* Pythonã®ã³ã¼ãã¨åãã#ä»¥éã¯ã³ã¡ã³ã
* ==ã>, >=, <, <=ãªã©ã§ãã¼ã¸ã§ã³ãæå®ã§ãã
* ãã¼ã¸ã§ã³æå®ãçç¥ããã¨ææ°çãã¤ã³ã¹ãã¼ã«ããã
* ã«ã³ã,ã§åºåãã¨äºã¤ã®æ¡ä»¶ãANDã§æå®ã§ãã

`pip freeze`ã³ãã³ãã§ç¾å¨ã®ç°å¢ã«ã¤ã³ã¹ãã¼ã«ãããããã±ã¼ã¸ã¨ãã¼ã¸ã§ã³ã`pip install -r`ã§ä½¿ããè¨­å®ãã¡ã¤ã«ã®å½¢å¼ã§åºå


```python
!pip freeze
```

ãããã£ã¦ã`pip freeze`ããªãã¤ã¬ã¯ã`>`ã§ãã¡ã¤ã«ã«åºåããã°ã  
ãã®ãã¡ã¤ã«ãä½¿ã£ã¦åã®ç°å¢ã¨åããã¼ã¸ã§ã³ã®ããã±ã¼ã¸ãå¥ç°å¢ã«ä¸æ¬ã§ã¤ã³ã¹ãã¼ã«ã§ãã


```python
!pip freeze > requirements.txt
```

## ã¤ã³ã¹ãã¼ã«

æ®æ®µã®å ´åã¯ã  `pip install <pkg name>`ã§`pypi`ãããµã¼ããã¦ã¤ã³ã¹ãã¼ã«ã§ãã

### ã­ã¼ã«ã«ãã
```python
pip install --no-index --find-links=<path> <pkg name>
```


```python
!pip install --no-index --find-links=<path> <pkg name>
```

### ãã¼ã¸ã§ã³ãæå®ããã®ã¯ä¸ã«`requirements.txtã®æ¸ãæ¹`ã®é¨åã¨åã

### ãã¤ããªãã¡ã¤ã«ãå©ç¨ããªã(OSã«ä¾å­ããªã)


æ®éãã¦ã³ã­ã¼ããã¤ã³ã¹ãã¼ã«ããæã`whl`ãã¡ã¤ã«ãå©ç¨  
`whl`ãã¡ã¤ã«ã®æ­£ä½ã¯`py`ãã¡ã¤ã«ã¨ã³ã³ãã¤ã«æ¸ã¿ã®`pyd`ãã¡ã¤ã«ã®**zip**ãã¡ã¤ã«ã§ãã  
[PEP427](https://www.python.org/dev/peps/pep-0427/)ã§å®ç¾©ããã  
ã³ã³ãã¤ã«æ¸ã¿ã®ããããã©ãããã©ã¼ã ã«ä¾å­ãã  
ããã§ãéãã¤ããªãã¡ã¤ã«ã®ç»å ´

ä¾ãã°ãèªåã¯*MacOS*ã*python3.8.6*ã§*numpy*ããã¦ã³ã­ã¼ãããã`pip download numpy`ãå®è¡å¾ã  
`numpy-1.19.3-cp38-cp38-macosx_10_9_x86_64.whl`ã¨ãããã¡ã¤ã«ãã²ãããã  
ãã®ãã¡ã¤ã«ã¯*Windows*ã*Linux*ã«ã¦ã¤ã³ã¹ãã¼ã«ã§ããªã

`pip download --no-binary=:all: numpy`ãå®è¡ããã¨ã
```python
Collecting numpy
  Downloading numpy-1.19.3.zip (7.3 MB)
     |ââââââââââââââââââââââââââââââââ| 7.3 MB 4.7 MB/s 
?25h  Installing build dependencies ... ?25ldone
?25h  Getting requirements to build wheel ... ?25ldone
?25h    Preparing wheel metadata ... ?25ldone
?25h  Saved ./numpy-1.19.3.zip
Successfully downloaded numpy
```
`num-1.19.3.zip`ãã¡ã¤ã«ããã¦ã³ã­ã¼ãããããè§£åããã¨ãä¸­èº«ã¯ä»¥ä¸ã¨ãªã
```bash
INSTALL.rst.txt       benchmarks            runtests.py
LICENSE.txt           doc                   setup.py
MANIFEST.in           doc_requirements.txt  site.cfg.example
PKG-INFO              numpy                 test_requirements.txt
README.md             pyproject.toml        tools
THANKS.txt            pytest.ini            tox.ini
```
ã¤ã³ã¹ãã¼ã«ããæã¯ã`pip install numpy-1.19.3.zip`ã®ããã«ãã¡ã¤ã«ãæå®ãã¦ã¤ã³ã¹ãã¼ã«
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
ãè¦§ã®éãã`Building wheels for collected packages: numpy`  
ã³ã³ãã¤ã«ãå¿è¦(å¤å°æéããã)


### ç¹å®ã®ã¦ã¼ã¶ã«å¯¾ãã¦ã¤ã³ã¹ãã¼ã«(ä»®æ³ç°å¢ã®ä½¿ç¨ãããããªããããã¯æ®æ®µä½¿ããªã)
```python
pip install --user <pkg name>
```


```python
!pip install --user <pkg name>
```

### å¾ã¤æéãå»¶é·(ãããã¯ã¼ã¯ãä¸å®å®ãªæä½¿ç¨)
```python
pip install --default-timeout=<seconds> <pkg name>
```


```python
!pip install --default-timeout=<seconds> <pkg name>
```

### ãã­ã­ã·ãä½¿ç¨(å¤é¨ã®ãããã¯ã¼ã¯ã«ã¢ã¯ã»ã¹ã§ããªãæã«ä½¿ç¨)
```python
pip install --proxy [user:passwd]@http_server_ip:port <pkg name>
```
`SSL`ã®ä½¿ç¨ã¨åã


```python
!pip install --proxy [user:passwd]@http_server_ip:port <pkg name>
```

### GitHubããã¤ã³ã¹ãã¼ã«
```python
pip install git+<repository-url>
pip install git+https://github.com/<user-name>/<repository-name><@branch-name>

```

* `git+`ãã¤ããã¤ã³ã¹ãã¼ã«ã¯ã`git clone`ãã¦ããã¤ã³ã¹ãã¼ã«ãããããã·ã¹ãã ã«gitãã¤ã³ã¹ãã¼ã«ããã¦ããå¿è¦ããã  
* GitHubã§ã¯ãªãªã¼ã¹ãã¼ã¸ããåãã¼ã¸ã§ã³ã®ãªãã¸ããªãzipã§ãã¦ã³ã­ã¼ãã§ããããã«ãªã£ã¦ããã®ã§ã  
  zipã®URLãç´æ¥æå®ãã¦ãOKããã®å ´åã¯gitãã¤ã³ã¹ãã¼ã«ããã¦ããªãã¦ãOK

## ã¢ã³ã¤ã³ã¹ãã¼ã«

```python
pip uninstall <pkg name>
```


```python
!pip uninstall <pkg name>
```

## ã¢ããã°ã¬ã¼ã

```python
pip install --upgrade <pkg name>
```


```python
!pip install --upgrade <pkg name>
```

ã¢ããã°ã¬ã¼ãã®æ¬è³ªã¯ã¢ã³ã¤ã³ã¹ãã¼ã«ãã¦ããææ°çãã¤ã³ã¹ãã¼ã«ã  
æã«ã³ãã³ãã¯`install`ã®ã¾ã¾ããã©ã¡ã¼ã¿ã¨ãã¦`--upgrade`ãè¿½å ãã  
ã¢ããã°ã¬ã¼ãããéã`--upgrade-strategy`ã¨ãããã©ã¡ã¼ã¿ããã  
é¸æè¢ã¯äºã¤
* `eager`ãä¾å­ããã±ã¼ã¸å¨é¨ã¢ããã°ã¬ã¼ã
* `only-if-need`(default)ãå¿è¦ãªæã ãä¾å­ããã±ã¼ã¸ãã¢ããã°ã¬ã¼ã

### ãããã¢ããã°ã¬ã¼ã


æ¹æ³ï¼ï¼`pip-review`ãä½¿ç¨

```bash
# ã¢ããã°ã¬ã¼ãã§ããããã±ã¼ã¸ä¸è¦§ãç¢ºèª
pip list  --outdated --format=columns
# ãããå¦ç
pip install pip-review
pip-review --local --interactive
```

æ¹æ³ï¼ï¼Pythonã¹ã¯ãªãããä½¿ç¨
```python
import pip
from subprocess import call
from pip._internal.utils.misc import get_installed_distributions

for dist in get_installed_distributions():
    call("pip install --upgrade " + dist.project_name, shell=True)
```


## `pip.ini`ãã¡ã¤ã«ãä½¿ç¨

æ¯åã³ãã³ããæã¤æã¯ããã©ã¡ã¼ã¿ãå¥åããå¿è¦(ä¾ãã°SSLå¯¾å¿ã®ããã®`--trusted-host`)ãé¢åè­ãã¨æããªã  
`pip.ini`ãå©ç¨ããã¨ä¾¿å©

æé ï¼
1. `win+r` -> `%APPDATA%`å®è¡(C:\Users\xx\AppData ãéã)
2. `pip`ã¨ãããã©ã«ãããªããªããä½ã
3. `pip`ãã©ã«ãã®ä¸­ã«ã`pip.ini`ã¨ãããã¡ã¤ã«ãä½ã
4. ç·¨éãã

```ini
[global]
index-url = <url> ã# pypiã«ã¢ã¯ã»ã¹ã¥ããæã«è¨­å®
proxy=<url> # å¤é¨ã®ãããã¯ã¼ã¯ã«ã¢ã¯ã»ã¹ã§ããªãæã«è¨­å®

[https]
verify=enable

[install]
trusted-host = pypi.python.org
               pypi.org
               files.pythonhosted.orgã# SSLå¯¾å¿
find-links = <path>
```


```python

```
