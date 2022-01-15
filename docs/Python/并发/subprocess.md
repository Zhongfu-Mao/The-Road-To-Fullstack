# subprocess

```python
import subprocess

subprocess.call(["ls", "-l"])
subprocess.call("exit 1", shell=True)

output = subprocess.check_output(["df", "-h"])
print(output)

def execute_cmd(cmd):
    p = subprocess.Popen(
        cmd,
        stdin=subprocess.PIPE,
        stdout=subprocess.PIPE,
        stderr=subprocess.PIPE
    )
    stdout, stderr = p.communicate()
    if p.returncode != 0:
        return p.returncode, stderr
    return p.returncode, stdout
```
