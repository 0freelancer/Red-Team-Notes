
There is lot of different 2FA Bypass Techniques given below. Check it.
## Bypass 2FA with null or 000000
 ## 1. Manipulation
   
   ### Response Manipulation
    1. Check Response of the 2FA Request.
    2. If you Observe “Success”:false
    3. Change this to “Success”:true and see if it bypass the 2FA
    or
    See the Response of this request and analyze if the 2FA Code is leaked.
   
   ### Status code Manipulation
    1. If the Response Status Code is 4XX like 401, 402, etc.
    2. Change the Response Status Code to “200 OK” and see if it bypass the 2FA
 
## Ignoring 2FA under certain circumstances.

    ### 2FA ignoring when recovering a password
    ### Ignoring 2FA when entering through a social network
    ### Ignoring 2FA in an older version of the application
        *Subdomains: If you can find some "testing" subdomains with the login functionality, they could be using old versions that don't support 2FA (so it is                         directly bypassed) or those endpoints could support a vulnerable version of the 2FA.
                    https://www.freecodecamp.org/news/responsible-disclosure-how-i-could-have-hacked-all-facebook-accounts-f47c0252ae4d/
        *Apis:    If you find that the 2FA is using an API located under a /v*/ directory (like "/v3/"), this probably means that there are older API endpoints                      that could be vulnerable to some kind of 2FA bypass. 
    ### Ignoring 2FA in case of cross-platforming

## 3. 2FA Refer Check Bypass

    1. Directly Navigate to the page which comes after 2FA or any other authenticated page of the application.
    2. If there is no success, change the refer header to the 2FA page URL. This may fool application to pretend as if the request came after satisfying 2FA           Condition.
 
## 4. 2FA Code Reusability

    1. Request a 2FA code and use it
    2. Now, Re-use the 2FA code and if it is used successfully that’s an issue.
    3. Also, try requesting multiple 2FA codes and see if previously requested Codes expire or not when a new code is requested
    4. Also, try to re-use the previously used code after long time duration say 1 day or more. That will be an potential issue as 1 day is enough duration to         crack and guess a 6-digit 2FA code.

## Bypass using the "Remember Me" functionality
    # If 2FA is attached using a cookie, the cookie value must be unguessable
    # If 2FA is attached to an IP address, you can try to figure out the IP address of the victim and impersonate it using the X-Forwarded-For header.

 ## 5.Enabling 2FA Doesn’t Expire Previous Session

    1. Login to the application in two different browsers and enable 2FA from 1st session.
    2. Use 2nd session and if it is not expired, it could be an issue if there is an insufficient session expiration issue. In this scenario if an attacker           hijacks an active session before 2FA, it is possible to carry out all functions without a need for 2FA

## 7.Missing 2FA Code IntegrityValidation

    Code for any user acc can be used to bypass the 2FA
    Request a 2FA code from Attacker Account.
    # Bypass replacing part of the request from the session

    If a parameter with a specific value is sent to verify the code in the request, try sending the value from the request of another account.
    For example, when sending an OTP code, the form ID/user ID or cookie is checked, which is associated with sending the code. If we apply the data from the         parameters of the account on which you want to bypass code verification (Account 1) to a session of a completely different account (Account 2), receive the       code and enter it on the second account, then we can bypass the protection on the first account. After reloading the page, 2FA should disappear.


## Improper access control bug on the 2FA dialog page
   
    Sometimes a dialog page for entering 2FA is presented as a URL with parameters. Access to such a page with parameters in the URL with cookies that do not         match those used to generate the page or without cookies at all is not safe. But if the developers decided to accept the risks, then you need to go through       a few  important points:
        1) Does the link for 2FA dialog page expire;
        2) Whether the link is indexed in search engines.
    If the link has a long period of existence and/or the search engines contain working links for 2FA input/links can be indexed (there are no rules in               robots.txt   / meta tags), then there is a possibility of using a 2FA bypass mechanism on the 2FA input page, in which you can completely bypass entering         login and password,   and gain access to someone else’s account

## Brute force
  ### Lack of rate limit
    - Exploit:
    1. Request 2FA code and capture this request.
    2. Repeat this request for 100–200 times and if there is no limitation set, that’s a rate limit issue.
    3. At 2FA Code Verification page, try to brute-force for valid 2FA and see if there is any success.
    4. You can also try to initiate, requesting OTPs at one side and brute-forcing at another side. Somewhere the OTP will match in middle and may give you a         quick result.

  ### Rate limit bypass
     Limiting the flow rate with the absence of blocking after reaching a certain flow rate
    In this case there is a flow rate limit (you have to brute force it very slowly: 1 thread and some sleep before 2 tries) but no rate limit. So with enough         time you can be able to find the valid code.
    
  ### Generated OTP code doesn’t change
        https://hackerone.com/reports/420163
    
  ### Rate-limit resetting when updating the code. 
      https://hackerone.com/reports/149598, — theory;
      https://hackerone.com/reports/205000, — a practical exploit based on a previous report.
  
  ### Client side rate limit bypass
 
  ###  Lack of Rate-limit in the user’s account
  
  ### Lack of rate limit re-sending the code via SMS
      You want be able to bypass the 2FA but you will be able to waste money of the company.
      
  ### Infinite OTP regeneration
      If you can generate a new OTP infinite times, the OTP is simple enough (4 numbers), and you can try up to 4 or 5 tokens per generated OTP, you can just try       the same 4 or 5 tokens every time and generate OTPs until it matches the ones you are using.
      
## 6. insufficient censorship of personal data on the 2FA page.

## Backup Code Abuse

Bypassing 2FA by abusing the Backup code feature
Use the above mentioned techniques to bypass Backup Code to remove/reset 2FA restrictions

## 7. When disabling 2FA, the current code or password is not requested.
    Check if there is a CSRF or a Clickjacking vulnerability to disable the 2FA.
     1. Assuming that you are able to perform email change or password reset for the victim user or make victim user do it by any means possible.
     2. 2FA is disabled after the email is changed or password is reset. This could
    be an issue for some organizations. However, depends on case by case basis.
  Use this valid 2FA code in the victim 2FA Request and see if it bypass the 2FA Protection.










### References
https://medium.com/@iSecMax/two-factor-authentication-security-testing-and-possible-bypasses-f65650412b35
https://aswingovind.medium.com/2-factor-authentication-bypass-3b2bbd907718

