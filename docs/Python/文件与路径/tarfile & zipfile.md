# tarfile & zipfile

## tarfile

```python
import tarfile

with tarfile.open(<file>) as t:
    for member_info in t.getmembers():
        print(member_info.name)
```

```python
with tarfile.open(<file>, mode="r:gz") as out:
    out.add("README.txt")
```

## zipfile

```python
import zipfile

foo = zipfile.ZipFile(<filename>)
foo.namelist()

new_zip = zipfile.ZipFile(<filename>, "w")
new_zip.write("spam.txt")
new_zip.close()
```
