# shutil

os模块是对操作系统的接口进行封装，主要作用是跨平台。  
shutil模块包含复制、移动、重命名和删除文件及目录的函数，主要作用是管理文件和目录。


```python
import shutil

shutil.get_archive_formats()
shutil.make_archive("backup", "gztar")

import tarfile

f = tarfile.open("backup.tar.gz", "r:gz")
f.getnames()

shutil.unpack_archive("backup.tar.gz")
```
