# HOMIES
Base Url: `https://homies-1854.herokuapp.com/api`


<details>
<summary>Register</summary>

REST access:
```java
@PostMapping
```

EndPoint:
```
/register
```

Header:
```java
null
```

Body Requireds:
```json
{
    "login": "nickName",
    "password": "12345678",
    "email": "mymail@domain.com",
    "langKey": "es"
}
```

Body complete:
```json
{
    "login": "nickName",
    "password": "12345678",
    "email": "mymail@domain.com",
    "langKey": "es",
    "firstName":"myName",
    "lastName":"myLastName"
}
```

Info fields:
```
login => username (Required, minLen = 1, maxLen = 50)
password => password (Required, minLen = 8, maxLen = 100)
email => email (Required, minLen = 8, maxLen = 100)
fistName => name of user (maxLen = 50)
lastName => last name of user (maxLen = 50)
langKey => laguagge of user (minLen = 2, maxLen = 10)
```

Return OK:
```java
HttpStatus.created() "201"
```

Email to return new user and activate url for this user:
```
Dear user

Your Homies account has been created, please click on the URL below to activate it:

https://homies-1854.herokuapp.com//account/activate?key=N95gRmUHsiUSWVLahqqJ

Regards,
Homies Team.
```

</details>


<details>
<summary>Login</summary>

REST access:
```java
@PostMapping
```

EndPoint:
```
/authenticate
```

Header:
```java
null
```

Body Requireds:
```json
{
    "username": "nickName",
    "password": "12345678"
}
```

Info fields:
```html
username => username (Required, minLen = 1, maxLen = 100)
password => password (Required, minLen = 8, maxLen = 100)
```

Return OK:
```json
{
    "id_token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhZG1pbiIsImF1dGgiOiJST0xFX0FETUlOLFJPTEVfVVNFUiIsImV4cCI6MTY0NzcxNTU1N30.rCu8qK61uRQvJVJpZ2RRe_3Qizdjr9DL4EBMQnYaD-np94qEFV5rcNV0Q0279xMkLZq86w5k_GqJbhC1C_NKmA"
}
```

</details>

<details>
<summary>Change Password</summary>

REST access:
```java
@PostMapping
```

EndPoint:
```
/account/change-password
```

Header:
```java
null
```

Body Requireds:
```json
{
    "currentPassword": "actualPass",
    "newPassword": "newPassword"
}
```

Info fields:
```html
currentPassword => currentPassword (Required, minLen = 8, maxLen = 50)
newPassword => newPassword (Required, minLen = 8, maxLen = 100)
```

Info EndPoint:
```html
This request requires authentication
need Authentication: "Bearer " + token
```

Return OK:
```html
200
```

Return Bad Request:
```html
400 title: Incorrect password
```

</details>

<details>
<summary>Reset password</summary>

REST access:
```java
@PostMapping
```

EndPoint:
```
/account/reset-password/init
```

Header:
```java
null
```

Body Requireds:
```text
email@domain.com
```

Info fields:
```html
text: needed text format, ¡¡¡NOT JSON format!!!
```

Return OK:
```html
200
```
```JSON
{
    "key": "Qal1LtXREXjj4hnkH1ZX"
}
```

Return Bad Request:
```html
400 title: Password reset requested for non existing mail!
```

</details>

<details>
<summary>Aply Reset password</summary>

REST access:
```java
@PostMapping
```

EndPoint:
```
/account/reset-password/finish
```

Header:
```java
null
```

Body Requireds:
```JSON
{
    "key": "Rkbx5WPUs5W1JaPY7BcA",
    "newPassword": "0987654321"
}
```

Info fields:
```html
key => key retrieved in the endPoint /account/reset-password/init
newPassword => newPassword (Required, minLen = 8, maxLen = 100)
```

Return OK:
```html
200
```

Return Bad Request:
```html
400 title: Incorrect password
```

</details>
