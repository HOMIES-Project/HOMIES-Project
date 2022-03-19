# HOMIES
Base Url: `https://homies-java-16.herokuapp.com/api`


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
    "email": "mymail@domain.com"
}
```

Body complete:
```json
{
    "login": "nickName",
    "password": "12345678",
    "email": "mymail@domain.com",
    "firstName":"myName",
    "lastName":"myLastName",
    "langKey":"en"
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
```
username => username (Required, minLen = 1, maxLen = 50)
password => password (Required, minLen = 8, maxLen = 100)
```

Return OK:
```json
{
    "id_token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhZG1pbiIsImF1dGgiOiJST0xFX0FETUlOLFJPTEVfVVNFUiIsImV4cCI6MTY0NzcxNTU1N30.rCu8qK61uRQvJVJpZ2RRe_3Qizdjr9DL4EBMQnYaD-np94qEFV5rcNV0Q0279xMkLZq86w5k_GqJbhC1C_NKmA"
}
```

</details>
