## Account Takeover

### 1. Using OAuth Misconfiguration
   - Victim has a account in evil.com
   - Attacker creates an account on evil.com using OAuth. For example the attacker have a facebook with a registered victim email
   - Attacker changed his/her email to victim email.
   - When the victim try to create an account on evil.com, it says the email already exists.

### 2. Try re-sign up using same email
```
POST /newaccount
[...]
email=victim@mail.com&password=1234
/////////
POST /newaccount
[...]
email=victim@mail.com&password=hacked
```
### 3.Token Leaks In Response
   Check response for Endpoints:(Register,Forget Password) if contains any link,any token or otp
   
### 4.Password Reset Poisioning Leads To Token Theft

### 5.Chaining Session Hijacking with XSS
  1.I have add a session hijacking method in broken auth and session managment. 
  2.If you find that on target.
  3.Try anyway to steal cookies on that target.
  4.Here I am saying look for xss .
  5.If you find xss you can stole the cookies of victim and using session hijacking you can takeover the account of victim.
  
  
