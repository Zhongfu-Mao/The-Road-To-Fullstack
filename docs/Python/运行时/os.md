# os


```python
import os

os.listdir()
path = os.getcwd()
os.path.split(path)
os.path.dirname(path)
os.path.basename(path)
os.path.splitext(path)
os.path.expanduser("~")
os.path.abspath(".")
os.path.abspath("..")
os.path.join(os.path.expanduser("~"), "GitHub")
os.path.isabs(".")
os.path.isdir(".")
os.path.isfile("my.cnf")
```


```python
import os
import sys

def main():
    sys.argv.append("")
    filename = sys.argv[1]
    if not os.path.isfile(filename):
        raise SystemExit(filename + " does not exists")
    elif not os.access(filename, os.R_OK):
        os.chmod(filename, 0777)
    else:
        with open(filename) as f:
            print(f.read())

if __name__ == "__main__":
    main()
```
