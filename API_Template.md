# HOMIES
Base Url: `https://homies-back-app.herokuapp.com/api`


<details>
<summary>User's Features</summary>

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
login => username (Required, minLen = 4, maxLen = 50)
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
username => username (Required, minLen = 4, maxLen = 100)
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
```JSON
{
    "email": "email@domain.com"    
}    
```

Info fields:
```html
text: Encapsulated in JSON format
```

Return OK:
```html
200
```
```JSON
{
    "ACCEPTED"
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

</details>

##

<details>
<summary>Group's Features</summary>

<details>
<summary>Create new Group</summary>

REST access:
```java
@PostMapping
```

EndPoint:
```
/groups
```

Header:
```java
null
```

Body Requireds:
```json
{
    "user": 1,
    "groupName": "grupoPrueba1",
    "groupRelation": "esto es un grupo de prueba"
}
```

Info fields:
```Text
Request:
user => userData.id (Require, Int) only need id of user login in app or web *For now only userData 1 can be used
groupName => name of group (Require, unique, lenMin = 3, lenMax = 50, text)
groupRelation => reason why the group exist (Require, unique, lenMin = 3, lenMax = 100, text)

Response:
id => id's group (Autoasigned)
groupKey => key/password group (Autoasigned)
groupName => name of group
groupRelation => reason why the group exist
userData => extension of "user" for save extra data of users
userAdmin => user who created the group
taskList => group's task list (Autoasigned)
```

Return OK:
```java
HttpStatus.created() "201"
```
Body response:
```json
{
    "id": 31,
    "groupKey": "DdsiB9XTHSnpEQyfkFNV",
    "groupName": "grupoPrueba7",
    "groupRelationName": "esto es un grupo de prueba",
    "addGroupDate": "2022-03-31",
    "userAdmin": {
        "id": 1,
        "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAAAADACAMAAABlApw1AAAC/VBMVEUAAADLqqNL...",
        "photoContentType": "image/png",
        "phone": "735-497-3310",
        "premium": false,
        "birthDate": "2022-01-20",
        "addDate": "2022-01-21"
    },
    "taskList": {
        "id": 31,
        "nameList": "TKLgrupoPrueba7"
    },
    "spendingList": {
        "id": 31,
        "total": 0.0,
        "nameSpendList": "SPL_grupoPrueba7"
    },
    "shoppingList": {
        "id": 31,
        "total": 0.0,
        "nameShopList": "SHLgrupoPrueba7"
    },
    "settingsList": {
        "id": 31,
        "settingOne": false,
        "settingTwo": false,
        "settingThree": false,
        "settingFour": false,
        "settingFive": false,
        "settingSix": false,
        "settingSeven": false
    },
    "userData": null
}
```

Return Bad Request:
```java
HttpStatus.created() "400" //*por definir
```
</details>

<details>
<summary>Get all Groups</summary>

REST access:
```java
@GetMapping
```

EndPoint:
```
/groups
```

Header:
```java
null
```

Body Requireds:
```java
null
```

Info fields:
```text
Response:
id => id's group (Autoasigned)
groupKey => key/password group (Autoasigned)
groupName => name of group
groupRelation => reason why the group exist
userData => extension of "user" for save extra data of users
userAdmin => user who created the group
taskList => group's task list (Autoasigned)
```

Return OK:
```java
HttpStatus.ok() "200"
```
Body response:
```json
[
    {
        "id": 31,
        "groupKey": "DdsiB9XTHSnpEQyfkFNV",
        "groupName": "grupoPrueba7",
        "groupRelationName": "esto es un grupo de prueba",
        "addGroupDate": "2022-03-31",
        "userAdmin": {
            "id": 1,
            "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAAAADACAMAAABlApw1AAAC/VBMVEUAAADLqqNL...",
            "photoContentType": "image/png",
            "phone": "735-497-3310",
            "premium": false,
            "birthDate": "2022-01-20",
            "addDate": "2022-01-21"
        },
        "taskList": {
            "id": 31,
            "nameList": "TKLgrupoPrueba7"
        },
        "spendingList": {
            "id": 31,
            "total": 0.0,
            "nameSpendList": "SPL_grupoPrueba7"
        },
        "shoppingList": {
            "id": 31,
            "total": 0.0,
            "nameShopList": "SHLgrupoPrueba7"
        },
        "settingsList": {
            "id": 31,
            "settingOne": false,
            "settingTwo": false,
            "settingThree": false,
            "settingFour": false,
            "settingFive": false,
            "settingSix": false,
            "settingSeven": false
        },
        "userData": null
    }
]
```

Return Bad Request:
```java
HttpStatus.created() "400" //*por definir
```
</details>

</details>
