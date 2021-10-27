# 2FA

## Common flaws

---------------------------### Brute force--------------------------------------------------------
# Bypass replacing part of the request from the session
If a parameter with a specific value is sent to verify the code in the request, try sending the value from the request of another account.
For example, when sending an OTP code, the form ID/user ID or cookie is checked, which is associated with sending the code. If we apply the data from the parameters of the account on which you want to bypass code verification (Account 1) to a session of a completely different account (Account 2), receive the code and enter it on the second account, then we can bypass the protection on the first account. After reloading the page, 2FA should disappear.

# Ignoring 2FA under certain circumstances.

    # 2FA ignoring when recovering a password
    # Ignoring 2FA when entering through a social network
    # Ignoring 2FA in an older version of the application
        *Subdomains: If you can find some "testing" subdomains with the login functionality, they could be using old versions that don't support 2FA (so it is                         directly bypassed) or those endpoints could support a vulnerable version of the 2FA.
                    https://www.freecodecamp.org/news/responsible-disclosure-how-i-could-have-hacked-all-facebook-accounts-f47c0252ae4d/
        *Apis:    If you find that the 2FA is using an API located under a /v*/ directory (like "/v3/"), this probably means that there are older API endpoints                      that could be vulnerable to some kind of 2FA bypass. 
    
    # Ignoring 2FA in case of cross-platforming

# 7. When disabling 2FA, the current code or password is not requested.

# Bypass using the "Remember Me" functionality
    # If 2FA is attached using a cookie, the cookie value must be unguessable
    # If 2FA is attached to an IP address, you can try to figure out the IP address of the victim and impersonate it using the X-Forwarded-For header.

# Improper access control bug on the 2FA dialog page
   Sometimes a dialog page for entering 2FA is presented as a URL with parameters. Access to such a page with parameters in the URL with cookies that do not match    those used to generate the page or without cookies at all is not safe. But if the developers decided to accept the risks, then you need to go through a few       important points:
  1) Does the link for 2FA dialog page expire;
  2) Whether the link is indexed in search engines.
  If the link has a long period of existence and/or the search engines contain working links for 2FA input/links can be indexed (there are no rules in robots.txt   / meta tags), then there is a possibility of using a 2FA bypass mechanism on the 2FA input page, in which you can completely bypass entering login and password,   and gain access to someone else’s account





# Lack of rate limit
    - Exploit:
    1. Request 2FA code and capture this request.
    2. Repeat this request for 100–200 times and if there is no limitation set, that’s a rate limit issue.
    3. At 2FA Code Verification page, try to brute-force for valid 2FA and see if there is any success.
    4. You can also try to initiate, requesting OTPs at one side and brute-forcing at another side. Somewhere the OTP will match in middle and may give you a quick result.

## Rate limit bypass
    # Limiting the flow rate with the absence of blocking after reaching a certain flow rate
    In this case there is a flow rate limit (you have to brute force it very slowly: 1 thread and some sleep before 2 tries) but no rate limit. So with enough         time you can be able to find the valid code.
    
    # Generated OTP code doesn’t change
        https://hackerone.com/reports/420163
    
    # Rate-limit resetting when updating the code. 
    
       https://hackerone.com/reports/149598, — theory;
       https://hackerone.com/reports/205000, — a practical exploit based on a previous report.
    # Client side rate limit bypass
 # Lack of Rate-limit in the user’s account






# Improper Access Control in the backup codes request
```

## Mindmaps

![](../../.gitbook/assets/image%20%289%29.png)

![](../../.gitbook/assets/image%20%288%29.png)



```text
https://medium.com/@iSecMax/two-factor-authentication-security-testing-and-possible-bypasses-f65650412b35
```



