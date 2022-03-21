# pytest

## 簡単な例

```shell
$ pytest test_one.py

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31
collected 1 item                                                               

test_one.py .                                                            [100%]

============================== 1 passed in 0.01s ===============================
```

!!!info

    `.`は一つのテストが実行され無事終了の意味  
    もっと詳しい情報欲しい場合は`-v`あるいは`-verbose`を追加

### `verbose`

```shell
$ pytest test_one.py -v

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1 -- /Library/Frameworks/Python.framework/Versions/3.8/bin/python3.8
cachedir: .pytest_cache
metadata: {'Python': '3.8.6', 'Platform': 'macOS-10.16-x86_64-i386-64bit', 'Packages': {'pytest': '6.2.1', 'py': '1.10.0', 'pluggy': '0.13.1'}, 'Plugins': {'html': '3.1.1', 'metadata': '1.11.0', 'allure-pytest': '2.8.31'}}
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31
collected 1 item                                                               

test_one.py::test_passing PASSED                                         [100%]

============================== 1 passed in 0.01s ===============================
```

### 失敗する場合

```shell
$ pytest test_two.py

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31
collected 1 item                                                               

test_two.py F                                                            [100%]

=================================== FAILURES ===================================
_________________________________ test_failing _________________________________

    def test_failing():
>       assert (1, 2, 3) == (3, 2, 1)
E       assert (1, 2, 3) == (3, 2, 1)
E         At index 0 diff: 1 != 3
E         Use -v to get the full diff

test_two.py:2: AssertionError
=========================== short test summary info ============================
FAILED test_two.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
============================== 1 failed in 0.13s ===============================
```

```shell
$ pytest test_two.py -v

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1 -- /Library/Frameworks/Python.framework/Versions/3.8/bin/python3.8
cachedir: .pytest_cache
metadata: {'Python': '3.8.6', 'Platform': 'macOS-10.16-x86_64-i386-64bit', 'Packages': {'pytest': '6.2.1', 'py': '1.10.0', 'pluggy': '0.13.1'}, 'Plugins': {'html': '3.1.1', 'metadata': '1.11.0', 'allure-pytest': '2.8.31'}}
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31
collected 1 item                                                               

test_two.py::test_failing FAILED                                         [100%]

=================================== FAILURES ===================================
_________________________________ test_failing _________________________________

    def test_failing():
>       assert (1, 2, 3) == (3, 2, 1)
E       assert (1, 2, 3) == (3, 2, 1)
E         At index 0 diff: 1 != 3
E         Full diff:
E         - (3, 2, 1)
E         ?  ^     ^
E         + (1, 2, 3)
E         ?  ^     ^

test_two.py:2: AssertionError
=========================== short test summary info ============================
FAILED test_two.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
============================== 1 failed in 0.11s ===============================
```

## 実行

```shell
$ pytest --help

Output exceeds the size limit. Open the full output data in a text editor
usage: pytest [options] [file_or_dir] [file_or_dir] [...]

positional arguments:
  file_or_dir

general:
  -k EXPRESSION         only run tests which match the given substring
                        expression. An expression is a python evaluatable
                        expression where all names are substring-matched against
                        test names and their parent classes. Example: -k
                        'test_method or test_other' matches all test functions
                        and classes whose name contains 'test_method' or
                        'test_other', while -k 'not test_method' matches those
                        that don't contain 'test_method' in their names. -k 'not
                        test_method and not test_other' will eliminate the
                        matches. Additionally keywords are matched to classes
                        and functions containing extra names in their
                        'extra_keyword_matches' set, as well as functions which
                        have names assigned directly to them. The matching is
                        case-insensitive.
  -m MARKEXPR           only run tests matching given mark expression.
                        For example: -m 'mark1 and not mark2'.
  --markers             show markers (builtin, plugin and per-project ones).
  -x, --exitfirst       exit instantly on first error or failed test.
  --fixtures, --funcargs
...

to see available markers type: pytest --markers
to see available fixtures type: pytest --fixtures
(shown according to specified file_or_dir or current dir if not specified; fixtures with leading '_' are only shown with the '-v' option
```

```shell
$ pytest

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31
collected 6 items                                                              

test_four.py .F                                                          [ 33%]
test_one.py .                                                            [ 50%]
test_three.py ..                                                         [ 83%]
test_two.py F                                                            [100%]

=================================== FAILURES ===================================
_________________________________ test_replace _________________________________

    @pytest.mark.run_these_please
    def test_replace():
        t_before = Task('finish cooking', 'sanji', False)
        t_after = t_before._replace(id=10, done=True)
        t_expected = Task('finish cooking', 'sanji', True, 11)
>       assert t_after == t_expected
E       AssertionError: assert Task(summary=...e=True, id=10) == Task(summary=...e=True, id=11)
E         
E         Omitting 3 identical items, use -vv to show
E         Differing attributes:
E         ['id']
...
=========================== short test summary info ============================
FAILED test_four.py::test_replace - AssertionError: assert Task(summary=...e=...
FAILED test_two.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
========================= 2 failed, 4 passed in 0.16s ==========================
```

!!!info

    パラメータがない時、再帰的に現在のフォルダからテストケースを見つけ実行する

実行したいファイルを指定する：

```shell
$ pytest test_three.py test_four.py

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31
collected 4 items                                                              

test_three.py ..                                                         [ 50%]
test_four.py .F                                                          [100%]

=================================== FAILURES ===================================
_________________________________ test_replace _________________________________

    @pytest.mark.run_these_please
    def test_replace():
        t_before = Task('finish cooking', 'sanji', False)
        t_after = t_before._replace(id=10, done=True)
        t_expected = Task('finish cooking', 'sanji', True, 11)
>       assert t_after == t_expected
E       AssertionError: assert Task(summary=...e=True, id=10) == Task(summary=...e=True, id=11)
E         
E         Omitting 3 identical items, use -vv to show
E         Differing attributes:
E         ['id']
E         
E         Drill down into differing attribute id:
...

test_four.py:29: AssertionError
=========================== short test summary info ============================
FAILED test_four.py::test_replace - AssertionError: assert Task(summary=...e=...
========================= 1 failed, 3 passed in 0.12s ==========================
```

## 命名規則

+ ファイル: `test_<something>.py` or `<something>_test.py`
+ 関数、メソッド: `test_<something>`
+ クラス: `Test<something>`(`__init__`メソッドを定義しないように)

## テスト結果

+ PASSED(.): 成功
+ FAILED(F): 失敗
+ SKIPPED(s): スキップされた
+ xfail(x): 予想通り失敗した
+ XPASS(X):　予想外成功した(unexpectedly passing)
+ ERROR(E):　例外発生した

## ただ一つのテストを実行

`<module>::<test_name>`

```shell
$ pytest test_four.py::test_asdict

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31
collected 1 item                                                               

test_four.py .                                                           [100%]

============================== 1 passed in 0.01s ===============================
```

## Options

### `--collect-only`

> テストケースを集まるだけ

```shell
$ pytest --collect-only

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31
collected 6 items                                                              

<Module test_four.py>
  <Function test_asdict>
  <Function test_replace>
<Module test_one.py>
  <Function test_passing>
<Module test_three.py>
  <Function test_defaults>
  <Function test_member_access>
<Module test_two.py>
  <Function test_failing>

========================== 6 tests collected in 0.01s ==========================
```

### `-k EXPRESSION`

> 式を利用してテストケースを探す(k: keyword)

```shell
$ pytest -k "asdict or defaults" --collect-only

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31
collected 6 items / 4 deselected / 2 selected                                  

<Module test_four.py>
  <Function test_asdict>
<Module test_three.py>
  <Function test_defaults>

================= 2/6 tests collected (4 deselected) in 0.02s ==================
```

### `-m MARKEXPR`

> 関数をマックして一緒に実行する(m: marker)

```python
import pytest

@pytest.mark.run_these_please  # 任意な名前でいい
def test_member_access():
    ...
```

```shell
$ pytest -v -m run_these_please

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1 -- /Library/Frameworks/Python.framework/Versions/3.8/bin/python3.8
cachedir: .pytest_cache
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest/01.Getting Start
collected 6 items / 4 deselected / 2 selected                                  

test_four.py::test_replace PASSED                                        [ 50%]
test_three.py::test_member_access PASSED                                 [100%]

======================= 2 passed, 4 deselected in 0.03s ========================
```

### `-x, --exitfirst`

> 失敗する場合は継続ではなく停止する

```shell
$ pytest -x

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest/01.Getting Start
collected 6 items                                                              

test_four.py ..                                                          [ 33%]
test_one.py .                                                            [ 50%]
test_three.py ..                                                         [ 83%]
test_two.py F                                                            [100%]

=================================== FAILURES ===================================
_________________________________ test_failing _________________________________

    def test_failing():
>       assert (1, 2, 3) == (3, 2, 1)
E       assert (1, 2, 3) == (3, 2, 1)
E         At index 0 diff: 1 != 3
E         Use -v to get the full diff

test_two.py:2: AssertionError
=========================== short test summary info ============================
FAILED test_two.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
!!!!!!!!!!!!!!!!!!!!!!!!!! stopping after 1 failures !!!!!!!!!!!!!!!!!!!!!!!!!!!
========================= 1 failed, 5 passed in 0.28s ==========================
```

```shell
# tb -> traceback
$ pytest --tb=no

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest/01.Getting Start
collected 6 items                                                              

test_four.py ..                                                          [ 33%]
test_one.py .                                                            [ 50%]
test_three.py ..                                                         [ 83%]
test_two.py F                                                            [100%]

=========================== short test summary info ============================
FAILED test_two.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
========================= 1 failed, 5 passed in 0.03s ==========================
```

### `--maxfail=num`

> 失敗の数が`num`に達したら停止する
> `num`が`1`の場合は`-x`と同じ

### `--lf, --last-failed`

> 最後の失敗を示す

```shell
$ pytest --lf

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest/01.Getting Start
collected 1 item                                                               
run-last-failure: rerun previous 1 failure (skipped 3 files)

test_two.py F                                                            [100%]

=================================== FAILURES ===================================
_________________________________ test_failing _________________________________

    def test_failing():
>       assert (1, 2, 3) == (3, 2, 1)
E       assert (1, 2, 3) == (3, 2, 1)
E         At index 0 diff: 1 != 3
E         Use -v to get the full diff

test_two.py:2: AssertionError
=========================== short test summary info ============================
FAILED test_two.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
============================== 1 failed in 0.19s ===============================
```

### `--ff, --failed-first`

> 先に失敗のケースを実行、その後残りのケースを実行する

```shell
$ pytest --ff --tb=no

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest/01.Getting Start
collected 6 items                                                              
run-last-failure: rerun previous 1 failure first

test_two.py F                                                            [ 16%]
test_four.py ..                                                          [ 50%]
test_one.py .                                                            [ 66%]
test_three.py ..                                                         [100%]

=========================== short test summary info ============================
FAILED test_two.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
========================= 1 failed, 5 passed in 0.03s ==========================
```

### `-v, --verbose`

> 詳細表示

### `-q, --quiet`

> `-v, --verbose`の反対

```shell
$ pytest -q

.....F                                                                   [100%]
=================================== FAILURES ===================================
_________________________________ test_failing _________________________________

    def test_failing():
>       assert (1, 2, 3) == (3, 2, 1)
E       assert (1, 2, 3) == (3, 2, 1)
E         At index 0 diff: 1 != 3
E         Full diff:
E         - (3, 2, 1)
E         ?  ^     ^
E         + (1, 2, 3)
E         ?  ^     ^

test_two.py:2: AssertionError
=========================== short test summary info ============================
FAILED test_two.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
1 failed, 5 passed in 0.17s
```

### `-l, --showlocals`

> トラックバックにローカル変数と値を出力

```python
# test_four.py
t_expected = Task('finish cooking', 'sanji', True, 11)  # 10 -> 11
```

```shell
$ pytest -l

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31
collected 6 items                                                              

test_four.py .F                                                          [ 33%]
test_one.py .                                                            [ 50%]
test_three.py ..                                                         [ 83%]
test_two.py F                                                            [100%]

=================================== FAILURES ===================================
_________________________________ test_replace _________________________________

    @pytest.mark.run_these_please
    def test_replace():
        t_before = Task('finish cooking', 'sanji', False)
        t_after = t_before._replace(id=10, done=True)
        t_expected = Task('finish cooking', 'sanji', True, 11)
>       assert t_after == t_expected
E       AssertionError: assert Task(summary=...e=True, id=10) == Task(summary=...e=True, id=11)
E         
E         Omitting 3 identical items, use -vv to show
E         Differing attributes:
E         ['id']
...

=========================== short test summary info ============================
FAILED test_four.py::test_replace - AssertionError: assert Task(summary=...e=...
FAILED test_two.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
========================= 2 failed, 4 passed in 0.19s ==========================
```

### `-r`: 短なレポートを出す(r: report)

使用する際に、出力の形を選択可能：

+ `f` -> failed
+ `E` -> error
+ `s` -> skipped
+ `x` -> xfailed
+ `X` -> xpassed
+ `p` -> passed
+ `P` -> passed with output
+ `a` -> all except pP
+ `A` -> all
+ `N` -> none

```shell
!pytest -ra
============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31
collected 6 items                                                              

test_four.py .F                                                          [ 33%]
test_one.py .                                                            [ 50%]
test_three.py ..                                                         [ 83%]
test_two.py F                                                            [100%]

=================================== FAILURES ===================================
_________________________________ test_replace _________________________________

    @pytest.mark.run_these_please
    def test_replace():
        t_before = Task('finish cooking', 'sanji', False)
        t_after = t_before._replace(id=10, done=True)
        t_expected = Task('finish cooking', 'sanji', True, 11)
>       assert t_after == t_expected
E       AssertionError: assert Task(summary=...e=True, id=10) == Task(summary=...e=True, id=11)
E         
E         Omitting 3 identical items, use -vv to show
E         Differing attributes:
E         ['id']
...
=========================== short test summary info ============================
FAILED test_four.py::test_replace - AssertionError: assert Task(summary=...e=...
FAILED test_two.py::test_failing - assert (1, 2, 3) == (3, 2, 1)
========================= 2 failed, 4 passed in 0.15s ==========================
```

### `--tb=style`: 失敗する際のトランスバックを変更する

+ `no`: 完全に表示しない
+ `line`: 一行で納める
+ `short`: `assert`のところだけを出力
+ `long`: 一番詳しい出力
+ `auto`: デフォルト値、最初と最後の失敗だけを出力
+ `native`: pythonの標準ライブラリの出力だけを出力

### `--durations=N`: もっとも遅いの`tests/setups/teardowns`N個を出力

> Nが`0`の場合、遅い順で全てを出力

### `--version`

> `pytest`をバージョンを出力

### `-h, --help`

## setup&teardown

+ module level: `setup_module`, `teardown_module`
+ function level: `setup_function`, `teardown_function`
+ class level: `setup_class`, `teardown_class`
+ method level: `setup_method`, `teardown_method`
+ inner class level: `setup`, `teardown`

```shell
$ pytest -s "test/Getting Start/test_setup_teardown.py"

============================= test session starts ==============================
platform darwin -- Python 3.8.6, pytest-6.2.1, py-1.10.0, pluggy-0.13.1
rootdir: /Users/maozhongfu/GitHub/自動化/テスト/pytest
plugins: html-3.1.1, metadata-1.11.0, allure-pytest-2.8.31, ordering-0.6
collected 4 items                                                              

test/Getting Start/test_setup_teardown.py 
setup_module: *.pyモジュールの前に実行される

setup_function: テストケースの前に実行される
test_oneを実行中
.
teardown_function: テストケースの後に実行される

setup_function: テストケースの前に実行される
test_twoを実行中
F
teardown_function: テストケースの後に実行される

setup_class：全てのクラスケースの前に実行される

setup_method:  クラスケースごとの前に実行される

setup: クラスケースごとの前に実行される
test_threeを実行中
...
=========================== short test summary info ============================
FAILED test/Getting Start/test_setup_teardown.py::test_two - AssertionError: ...
FAILED test/Getting Start/test_setup_teardown.py::TestCase::test_four - Asser...
========================= 2 failed, 2 passed in 0.12s ==========================
```

## plug-in

### HTML 出力

```shell
pip install pytest-html
pytest --html=report.html
```

### allure(美しいレポート)

```shell
pip install allure-pytest
```
