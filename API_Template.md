# HOMIES

<br>
#### Base Url: `https://homies-back-app.herokuapp.com/api`

<br>

<details> 
<summary><strong>User's Features *NEWS</strong></summary> 

<br>

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
<summary>Login *EDITED</summary>

NEW
```text
*The user id is now returned together with the token.
```

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

Info fields:
```html
username => username (Required, minLen = 4, maxLen = 100)
password => password (Required, minLen = 8, maxLen = 100)
id_token => token for user authenticate on all request
id       => id of user
```

Body Requireds:
```json
{
    "username": "nickName",
    "password": "12345678"
}
```

Return OK:
```java
HttpStatus.OK() "200"
```
```json
{
    "id_token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJlc3RoZXIxMyIsImF1dGgiOiJST0xFX1VTRVIiLCJleHAiOjE2NDg5NjY0NDN9.83t23mWPs0J2acZL88TxQCKd3uu-Tooi1T9_1-zCpE0FQ-mANWLVQBMovz1w5kotfvMFIO61zjHEA9rsaZFI6A",
    "id": 4
}
```

Return ERROR:
```java
HttpStatus.Unauthorized() "401"
HttpStatus.Bad_Request() "405"
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

<details>
<summary>View userData *EDITED</summary>

NEW
```text
*The groups to which the user belongs can now be retrieved.
```

REST access:
```java
@GetMapping
```

EndPoint:
```
/user-data
```

Header:
```java
null
```

Body Requireds:
```URL
/user-data/1 
```

Info fields:
```text
~/user-data/1 => example for displaying user 1 from the /user-data endpoint
- Here you can see information about which user this information is linked to, and which groups it belongs to with their corresponding objects.
```

Return OK:
```html
200
```
```JSON
{
    "id": 1,
    "photo": null,
    "photoContentType": null,
    "phone": null,
    "premium": false,
    "birthDate": null,
    "addDate": null,
    "user": {
        "id": 1,
        "login": "admin",
        "firstName": "Administrator",
        "lastName": "Administrator",
        "email": "homies_app@outlook.com",
        "activated": true,
        "langKey": "en",
        "imageUrl": "",
        "resetDate": null
    },
    "adminGroups": null,
    "taskAsigneds": [],
    "productCreateds": null,
    "groups": [
        {
            "id": 1,
            "groupKey": "jW63X27cAMnELzdNY1gr",
            "groupName": "grupoPrueba1",
            "groupRelationName": "esto es un grupo de prueba",
            "addGroupDate": "2022-04-01",
            "userAdmin": {
                "id": 1,
                "photo": null,
                "photoContentType": null,
                "phone": null,
                "premium": false,
                "birthDate": null,
                "addDate": null
            },
            "taskList": {
                "id": 1,
                "nameList": "TKLgrupoPrueba1"
            },
            "spendingList": {
                "id": 1,
                "total": 0.0,
                "nameSpendList": "SPL_grupoPrueba1"
            },
            "shoppingList": {
                "id": 1,
                "total": 0.0,
                "nameShopList": "SHLgrupoPrueba1"
            },
            "settingsList": {
                "id": 1,
                "settingOne": false,
                "settingTwo": false,
                "settingThree": false,
                "settingFour": false,
                "settingFive": false,
                "settingSix": false,
                "settingSeven": false
            },
            "userData": [
                {
                    "id": 1,
                    "photo": null,
                    "photoContentType": null,
                    "phone": null,
                    "premium": false,
                    "birthDate": null,
                    "addDate": null
                }
        }
    ]
}
```

Return Bad Request:
```html
404 title: NOT_FOUND
```

</details>

<details>
<summary>Delete User *NEW</summary>

REST access:
```java
@DeleteMapping
```

EndPoint:
```
/api/user-data/x
```

Header:
```java
null
```

Info fields:
```html
x  => x is the id of the user to delete
```

Body Requireds:
```java
null
```

Return OK:
```java
HttpStatus.No Content() "204"
```

Return ERROR:
```java
HttpStatus.Unauthorized() "401"
HttpStatus.Bad_Request() "405"
```
</details>

</details>

<br>

<details>
<summary><strong>Group's Features</strong></summary>

<br>

<details>
<summary>Create new Group *NEW & ERROR</summary>

ERROR
```text
Please, Do not use.
```

NEW
```text
Now all the lists of the group and the users that are part of it are returned (Only user who created the group).
```

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
    "id": 1,
    "groupKey": "Tunisian payment",
    "groupName": "South",
    "groupRelationName": "explicit white",
    "addGroupDate": "2022-03-07",
    "userAdmin": null,
    "taskList": {
        "id": 1,
        "nameList": "New"
    },
    "spendingList": {
        "id": 1,
        "total": 34472.0,
        "nameSpendList": "background"
    },
    "shoppingList": {
        "id": 1,
        "total": 90762.0,
        "nameShopList": "Towels Designer Jord"
    },
    "settingsList": {
        "id": 1,
        "settingOne": true,
        "settingTwo": false,
        "settingThree": false,
        "settingFour": false,
        "settingFive": true,
        "settingSix": false,
        "settingSeven": true
    },
    "userData": [
        {
            "id": 2,
            "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAAAADACAMAAABlApw1AAAC/VBMVEUAAA...",
            "photoContentType": "image/png",
            "phone": "1-555-408-2298 x3208",
            "premium": false,
            "birthDate": "2022-01-21",
            "addDate": "2022-01-21"
        }
    ]
}
```

Return Bad Request:
```java
HttpStatus.created() "400" //*por definir
```
</details>

<details>
<summary>Get all Groups *EDITED</summary>

NEW
```text
Now all the lists of the group and the users that are part of it are returned.
```

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
        "id": 1,
        "groupKey": "Tunisian payment",
        "groupName": "South",
        "groupRelationName": "explicit white",
        "addGroupDate": "2022-03-07",
        "userAdmin": null,
        "taskList": {
            "id": 1,
            "nameList": "New"
        },
        "spendingList": {
            "id": 1,
            "total": 34472.0,
            "nameSpendList": "background"
        },
        "shoppingList": {
            "id": 1,
            "total": 90762.0,
            "nameShopList": "Towels Designer Jord"
        },
        "settingsList": {
            "id": 1,
            "settingOne": true,
            "settingTwo": false,
            "settingThree": false,
            "settingFour": false,
            "settingFive": true,
            "settingSix": false,
            "settingSeven": true
        },
        "userData": [
            {
                "id": 2,
                "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAAAADACAMAAABlApw1AAAC/VBMVEUAAADLqqNLVm...",
                "photoContentType": "image/png",
                "phone": "1-555-408-2298 x3208",
                "premium": false,
                "birthDate": "2022-01-21",
                "addDate": "2022-01-21"
            }
        ]
    },
    {
        "id": 2,
        "groupKey": "info-mediaries matrix disintermediate",
        "groupName": "Savings Chair",
        "groupRelationName": "transmit",
        "addGroupDate": "2022-03-08",
        "userAdmin": null,
        "taskList": {
            "id": 2,
            "nameList": "analyzing"
        },
        "spendingList": {
            "id": 2,
            "total": 83853.0,
            "nameSpendList": "efficient XSS Soap"
        },
        "shoppingList": {
            "id": 2,
            "total": 53135.0,
            "nameShopList": "bypassing connect Mo"
        },
        "settingsList": {
            "id": 2,
            "settingOne": true,
            "settingTwo": false,
            "settingThree": false,
            "settingFour": true,
            "settingFive": true,
            "settingSix": true,
            "settingSeven": false
        },
        "userData": [
            {
                "id": 2,
                "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAAAADACAMAAABlApw1AAAC/VBMVEUAAADLqqNLVmy...",
                "photoContentType": "image/png",
                "phone": "1-555-408-2298 x3208",
                "premium": false,
                "birthDate": "2022-01-21",
                "addDate": "2022-01-21"
            }
        ]
    },
    {
        "id": 3,
        "groupKey": "Tasty client-driven Robust",
        "groupName": "Boliviano high-level moratorium",
        "groupRelationName": "orchid Car",
        "addGroupDate": "2022-03-08",
        "userAdmin": null,
        "taskList": {
            "id": 3,
            "nameList": "Berkshire Developer"
        } ...
```

Return Bad Request:
```java
HttpStatus.created() "400" //*por definir
```
</details>

</details>
