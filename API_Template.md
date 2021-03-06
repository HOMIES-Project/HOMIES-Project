```text
  ██╗    ██╗ █████████╗ ███╗  ███╗ ████████╗ ████████╗  ██████╗
  ██║    ██║ ██║    ██║ █████████║ ╚══██╔══╝ ██╔═════╝ ██╔════╝
  █████████║ ██║    ██║ ██║ █║ ██║    ██║    ██████╗   ╚██████╗
  ██╔════██║ ██║    ██║ ██║ ╚╝ ██║    ██║    ██╔═══╝    ╚════██╗
  ██║    ██║ █████████║ ██║    ██║ ████████╗ ████████╗ ███████╔╝
  ╚═╝    ╚═╝ ╚════════╝ ╚═╝    ╚═╝ ╚═══════╝ ╚═══════╝ ╚══════╝
```

# HOMIES API

<p>✨ => NEW</p> 
<p>🛠️ => EDITED</p>
<p>❌ => ERROR</p>
<p>(❌🛠️) => REPAIRING </p>
<p>🗑️ => DELETE</p>

#### Base Url: `https://homies-back-app.herokuapp.com/api`

<br>
<!--
  ################################# USERS ###################################
-->
<details> 
<summary><strong>User's Features ✨🛠️❌</strong></summary>

<br>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ USERS/REGISTER @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
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
  "firstName": "myName",
  "lastName": "myLastName"
}
```

Return OK:

```java
HttpStatus.created() "201"
```

Email to return new user and activate url for this user:

```text
Dear user

Your Homies account has been created, please click on the URL below to activate it:

https://homies-1854.herokuapp.com//account/activate?key=N95gRmUHsiUSWVLahqqJ

Regards,
Homies Team.
```

Return Error:

```java
HttpStatus.Unauthorized() "401"
HttpStatus.Bad_Request() "405"
```

Info fields:

```text
login => username (Required, minLen = 4, maxLen = 50)
password => password (Required, minLen = 8, maxLen = 100)
email => email (Required, minLen = 8, maxLen = 100)
fistName => name of user (maxLen = 50)
lastName => last name of user (maxLen = 50)
langKey => laguagge of user (minLen = 2, maxLen = 10)
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ USERS/LOGIN @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
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

Info fields:

```text
username => username (Required, minLen = 4, maxLen = 100) password => password
(Required, minLen = 8, maxLen = 100) id_token => token for user authenticate on
all request id => id of user
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ USERS/CHANGE PASSWORD @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
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

Return OK:

```java
HttpStatus.OK() "200"
```

Return Bad Request:

```java
HttpStatus.BadRequest() "400" "Incorrect password"
```

Info fields:

```text
currentPassword => currentPassword (Required, minLen = 8, maxLen = 50)
newPassword => newPassword (Required, minLen = 8, maxLen = 100)
```

Info EndPoint:

```text
This request requires authentication need Authentication: "Bearer " + token
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ USERS/RESET PASSWORD @@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
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

Return OK:

```java
HttpStatus.OK() "200"
```

```JSON
{
    "ACCEPTED"
}
```

Return Bad Request:
Return Error:

```java
HttpStatus.Bad_Request() "400"
```

```text
400 title: Password reset requested for non existing mail!
```

Info fields:

```html
text: Encapsulated in JSON format
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ USERS/APLY RESET PASSWORD @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
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

Return OK:

```java
HttpStatus.OK() "200"
```

Return Bad Request:

```java
HttpStatus.BadRequest() "400" "Incorrect password"
```

Info fields:

```text
key => key retrieved in the endPoint /account/reset-password/init newPassword =>
newPassword (Required, minLen = 8, maxLen = 100)
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ USERS/VIEW USER DATA @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>View userData 🛠️</summary>

NEW

```text
🛠️ *access only to backend administrator users
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

```
/user-data/1
```

Return OK:

```java
HttpStatus.OK() "200"
```

```JSON
{
    "id": 4,
    "photo": "iVBORw0KGgoAAAANSUhEUgAAAMA...",
    "photoContentType": "image/png",
    "phone": "999888777",
    "premium": false,
    "birthDate": null,
    "addDate": null,
    "user": {
        "id": 4,
        "login": "yorch7777",
        "firstName": "Agulló",
        "lastName": "Agulló",
        "email": "re227editado@hotmail.com",
        "activated": true,
        "langKey": "en",
        "imageUrl": null,
        "resetDate": "2022-04-05T05:50:48Z"
    },
    "adminGroups": [],
    "taskAsigneds": [],
    "productCreateds": [],
    "groups": [
        {
            "id": 1,
            "groupKey": "Tunisian payment",
            "groupName": "South",
            "groupRelationName": "explicit white",
            "addGroupDate": "2022-03-07",
            "userAdmin": {
                "id": 2,
                "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAA...",
                "photoContentType": "image/png",
                "phone": "1-555-408-2298 x3208",
                "premium": false,
                "birthDate": "2022-01-21",
                "addDate": "2022-01-21"
            },
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
                    "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAAAADACAMA...",
                    "photoContentType": "image/png",
                    "phone": "999888777",
                    "premium": false,
                    "birthDate": null,
                    "addDate": null
                },
                {
                    "id": 5,
                    "photo": null,
                    "photoContentType": null,
                    "phone": null,
                    "premium": false,
                    "birthDate": null,
                    "addDate": "2022-04-05"
                }
            ]
        }
    ]
}
```

Return Bad Request:

```text
404 title: NOT_FOUND
```

Info fields:

```text
/user-data/1 => example for displaying user 1 from the /user-data endpoint
- Here you can see information about which user this information is linked to, and which groups it belongs to with their corresponding objects.
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ USERS/DELETE USER @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Delete User ✨🛠️</summary>

NEW:

```text
✨ It is now possible to delete a user account
```

REST access:

```java
@DeleteMapping
```

EndPoint:

```
/user-data/x
```

Header:

```java
null
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

Info fields:

```text
x => x is the id of the user to delete
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ USERS/RE-SEND ACTIVATION EMAIL @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Re-send activation email ❌</summary>

ERROR:

```text
❌ Only allows forwarding if you are logged in, so it does not work properly.
```

REST access:

```java
@PostMapping
```

EndPoint:

```
/account/reset-password/email
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

Return OK:

```java
HttpStatus.ResetContent() "205"
```

Return Bad Request:
Return Error:

```java
HttpStatus.Bad_Request() "500"
```

```text
500 "detail": "No value present"
```

Info fields:

```text
text: Encapsulated in JSON format
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ USERS/EDIT USER DATA @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Edit user data✨</summary>

NEW:✨

```text
- ❗ When the user changes their email when editing their user, the user will be deactivated, so they will lose their login, and they will be sent the activation email again.
  - ❗❗❗❗❗ This should be pointed out to the user so that they do not enter the wrong email address and lose their account.
```

REST access:

```java
@PostMapping
```

EndPoint:

```TEXT
/account/reset-password/user-data/x
```

Header:

```java
null
```

Body Requireds:

```JSON
{
    "login": "Yorch7",
    "firstName": "Jorge",
    "lastName": "Agulló",
    "email": "re227editado@hotmail.com",
    "langKey": "en",
    "phone": 999888777,
    "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAA...",
    "photoContentType": "image/png",
    "birthDate": "1985-11-16T05:50:48Z"
}
```

Return OK:

```java
HttpStatus.Ok() "200"
```

```json
{
  "id": 4,
  "photo": null,
  "photoContentType": "image/png",
  "phone": "999888777",
  "premium": false,
  "birthDate": null,
  "addDate": null,
  "user": {
    "id": 4,
    "login": "yorch27",
    "firstName": "Jorge",
    "lastName": "Agulló",
    "email": "re22788editado@hotmail.com",
    "activated": true,
    "langKey": "en",
    "imageUrl": null,
    "resetDate": "2022-04-05T05:50:48Z"
  },
  "adminGroups": [],
  "taskAsigneds": [],
  "productCreateds": [],
  "groups": [
    {
      "id": 1,
      "groupKey": "Tunisian payment",
      "groupName": "South",
      "groupRelationName": "explicit white",
      "addGroupDate": "2022-03-07",
      "userAdmin": {
        "id": 2,
        "photo": "iVBORw0KGgoAAAANSUhEUgAAA...",
        "photoContentType": "image/png",
        "phone": "1-555-408-2298 x3208",
        "premium": false,
        "birthDate": "2022-01-21",
        "addDate": "2022-01-21"
      },
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
          "photo": "iVBORw0KGgoAAAANSUhEUgAAA...",
          "photoContentType": "image/png",
          "phone": "1-555-408-2298 x3208",
          "premium": false,
          "birthDate": "2022-01-21",
          "addDate": "2022-01-21"
        },
        {
          "id": 4,
          "photo": null,
          "photoContentType": "image/png",
          "phone": "999888777",
          "premium": false,
          "birthDate": null,
          "addDate": null
        }
      ]
    }
  ]
}
```

Return Bad Request:
Return Error:

```java
HttpStatus.Bad_Request() "500"
```

```text
500 "detail": "No value present"
```

Info fields:

```html
x => user's id login => user's name firstName => real user's name lastName =>
real user's lastName email => user's email langKey => user's language phone =>
user's phone photo => user's photo photoContentType => photo's format birthDate
=> user's birth day
```

</details>
</details>
<br>
<!--
  ############################### GROUPS ##############################
-->
<details>
<summary><strong>Group's Features✨🛠️</strong></summary>
<br>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ GROUPS/CREATE NEW GROUPS @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
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

Info fields:

```Text
Request:
user => userData.id (Require, Int) only need id of user login in app or web *For now only userData 1 can be used
groupName => name of group (Require, unique, lenMin = 3, lenMax = 50, text)
groupRelation => reason why the group exist (Require, unique, lenMin = 3, lenMax = 100, text)

Info Response:
id => id's group (Autoasigned)
groupKey => key/password group (Autoasigned)
groupName => name of group
groupRelation => reason why the group exist
userData => extension of "user" for save extra data of users
userAdmin => user who created the group
taskList => group's task list (Autoasigned)
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ GROUPS/GET ALL GROUPS @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Get all Groups 🛠️</summary>

NEW:

```text
Only allows queries to backend administrators.
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

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ GROUPS/ADD USER TO THE GROUP @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Add user to the group</summary>

❗ It can only be exercised by the owner of the group

REST access:

```java
@PostMapping
```

EndPoint:

```
/groups/add-user
```

Header:

```java
null
```

Body Requireds:

```json
{
  "idAdminGroup": "8",
  "login": "newUserName",
  "idGroup": "1"
}
```

Return OK:

```java
HttpStatus.Ok() "200"
```

```json
{
  "id": 1,
  "groupKey": "Tunisian payment",
  "groupName": "South",
  "groupRelationName": "explicit white",
  "addGroupDate": "2022-03-07",
  "userAdmin": {
    "id": 2,
    "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAAAAD...",
    "photoContentType": "image/png",
    "phone": "1-555-408-2298 x3208",
    "premium": false,
    "birthDate": "2022-01-21",
    "addDate": "2022-01-21"
  },
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
      "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAA...",
      "photoContentType": "image/png",
      "phone": "999888777",
      "premium": false,
      "birthDate": null,
      "addDate": null
    },
    {
      "id": 5,
      "photo": null,
      "photoContentType": null,
      "phone": null,
      "premium": false,
      "birthDate": null,
      "addDate": "2022-04-05"
    }
  ]
}
```

Return ERROR:

```java
HttpStatus.Unauthorized() "401"
HttpStatus.Bad_Request() "405"
```

Info fields:

```text
idAdminGroup => userAdmin's id, owner of group login => userName of new user to
be added (it is possible to change it to use the id, ¿yes?) idGroup => group's
id
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ GROUPS/DELETE USER OF GROUP @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Delete user of group ✨ (Allows the administrator to exit from himself/herself)</summary>

- ❗ It can only be exercised by the owner of the group.
- ❗ Remove the user from the group, and allow the administrator to leave the group by passing ownership to another user in teh group, if any.
- ❗ It can be used to make a user leave the group, just send the request without an administrator user.

REST access:

```java
@PostMapping
```

EndPoint:

```
/groups/delete-user
```

Header:

```java
null
```

Body Requireds:

```json
{
  "idAdminGroup": "8",
  "login": "newUserName",
  "idGroup": "1"
}
```

❗❗❗❗❗❗ Body Requireds: (only for a user to leave the group)✨

```json
{
  "login": "newUserName",
  "idGroup": "1"
}
```

Return OK:

```java
HttpStatus.No Content() "204"
```

```json
{
  "id": 1,
  "groupKey": "Tunisian payment",
  "groupName": "South",
  "groupRelationName": "explicit white",
  "addGroupDate": "2022-03-07",
  "userAdmin": {
    "id": 2,
    "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAAAAD...",
    "photoContentType": "image/png",
    "phone": "1-555-408-2298 x3208",
    "premium": false,
    "birthDate": "2022-01-21",
    "addDate": "2022-01-21"
  },
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
      "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAA...",
      "photoContentType": "image/png",
      "phone": "999888777",
      "premium": false,
      "birthDate": null,
      "addDate": null
    },
    {
      "id": 5,
      "photo": null,
      "photoContentType": null,
      "phone": null,
      "premium": false,
      "birthDate": null,
      "addDate": "2022-04-05"
    }
  ]
}
```

Return ERROR:

```java
HttpStatus.Unauthorized() "401"
HttpStatus.Bad_Request() "405"
```

Info fields:

```text
idAdminGroup => userAdmin's id, owner of group login => userName of new user to
be added (it is possible to change it to use the id, ¿yes?) idGroup => group's
id
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ GROUPS/CHANGE GROUP ADMIN @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Change group administrator</summary>

❗ It can only be exercised by the owner of the group

REST access:

```java
@PostMapping
```

EndPoint:

```
/groups/change-admin
```

Header:

```java
null
```

Body Requireds:

```json
{
  "idAdminGroup": "8",
  "login": "newUserName",
  "idGroup": "1"
}
```

Return OK:

```java
HttpStatus.Ok() "200"
```

```json
{
  "id": 1,
  "groupKey": "Tunisian payment",
  "groupName": "South",
  "groupRelationName": "explicit white",
  "addGroupDate": "2022-03-07",
  "userAdmin": {
    "id": 2,
    "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAAAAD...",
    "photoContentType": "image/png",
    "phone": "1-555-408-2298 x3208",
    "premium": false,
    "birthDate": "2022-01-21",
    "addDate": "2022-01-21"
  },
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
      "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAA...",
      "photoContentType": "image/png",
      "phone": "999888777",
      "premium": false,
      "birthDate": null,
      "addDate": null
    },
    {
      "id": 5,
      "photo": null,
      "photoContentType": null,
      "phone": null,
      "premium": false,
      "birthDate": null,
      "addDate": "2022-04-05"
    }
  ]
}
```

Return ERROR:

```java
HttpStatus.Unauthorized() "401"
HttpStatus.Bad_Request() "405"
```

Info fields:

```text
idAdminGroup => userAdmin's id, owner of group login => administrator's userName
of new group (it is possible to change it to use the id, ¿yes?) idGroup =>
group's id
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ GROUPS/DELETE GROUP @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Delete group ✨</summary>

❗ It can only be exercised by the owner of the group

REST access:

```java
@DeleteMapping
```

EndPoint:

```
/groups/x
```

Header:

```java
null
```

Body Requireds:

```java
null
```

Return OK:

```java
HttpStatus.NoContent() "204"
```

Return ERROR:

```java
HttpStatus.Unauthorized() "401"
HttpStatus.Bad_Request() "405"
```

Info fields:

```text
x => group`s id to delete
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ GROUPS/EDITE GROUP @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Edit group ✨</summary>

❗ It can only be exercised by the owner of the group

REST access:

```java
@PutMapping
```

EndPoint:

```
/groups/x
```

Header:

```java
null
```

Body Requireds:

```json
{
  "groupName": "newNameGroup",
  "groupRelation": "newDescriptionGroup"
}
```

Return OK:

```java
HttpStatus.Ok() "200"
```

Body Response:

```json
{
  "id": 45,
  "groupKey": "IoLBKbR7sI2YTimCsbQq",
  "groupName": "nombre editado2",
  "groupRelationName": "editando la descripción del grupo 2",
  "addGroupDate": "2022-04-24",
  "userAdmin": {
    "id": 8,
    "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAAAADACAMAAABlA...",
    "photoContentType": "image/png",
    "phone": "999888777",
    "premium": false,
    "birthDate": null,
    "addDate": "2022-04-21",
    "user": {
      "id": 8,
      "login": "yorch",
      "firstName": "Jorge",
      "lastName": "Agulló",
      "email": "agullojorge2@hotmail.com",
      "activated": true,
      "langKey": "en",
      "imageUrl": null,
      "resetDate": null
    }
  },
  "taskList": {
    "id": 45,
    "nameList": "TKLhomies1"
  },
  "spendingList": {
    "id": 45,
    "total": 0.0,
    "nameSpendList": "SPL_homies1"
  },
  "shoppingList": {
    "id": 45,
    "total": 0.0,
    "nameShopList": "SHLhomies1"
  },
  "settingsList": {
    "id": 45,
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
      "id": 2,
      "photo": "iVBORw0KGgoAAAANSUhEUgAAAMAAAADACAMAAABlApw1...",
      "photoContentType": "image/png",
      "phone": "999888777",
      "premium": false,
      "birthDate": null,
      "addDate": "2022-04-21",
      "user": {
        "id": 2,
        "login": "user",
        "firstName": "User",
        "lastName": "User",
        "email": "agullojorge@gmail.com",
        "activated": true,
        "langKey": "en",
        "imageUrl": "",
        "resetDate": null
      }
    }
  ]
}
```

Return ERROR:

```java
HttpStatus.Unauthorized() "401"
HttpStatus.Bad_Request() "405"
```

Info fields:

```text
groupName => The new name of the group (NonRequire, minLen = 3, maxLen = 50)
groupRelation => The new description of the group (NonRequire, minLen = 3, maxLen = 100)
```

</details>
</details>
<br>
<!--
  ################################ TASK ################################
-->
<details>
<summary><strong>Task Features✨</strong></summary>
<br>

<!--
  ################################ TASK ENTITY ################################
-->
<details>
<summary>Entity</summary>

Info variables:

```text
Response:
id => id task
task_name => name task
data_create => date on which the task is created
data_end => date on which the task is finish
description => description task
cancel => boolean variable used to cross out the task if it has been completed
photo => photo task
puntuacion => for the time being it will not be used

```

</details>

<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ TASK/CREATE NEW TASK @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Create new Task ✨</summary>

REST access:

```java
@PostMapping
```

EndPoint:

```
/tasks
```

Header:

```java
null
```

Body Requireds:

```json
{
  "user": 1,
  "idGroup": "1",
  "taskName": "Lavar platos",
  "description": "Lava también la taza de mi cuarto"
}
```

Return OK:

```java
HttpStatus.created() "201"
```

Body response:

```json
{
  "id": 3,
  "taskName": "Lavar platos",
  "dataCreate": "2022-04-20",
  "dataEnd": null,
  "description": "Lava también la taza de mi cuarto",
  "cancel": null,
  "photo": null,
  "photoContentType": null,
  "puntuacion": null,
  "taskList": {
    "id": 1,
    "nameList": "TKLMyHome"
  },
  "userData": {
    "id": 1,
    "photo": "/9j/4AAQSkZJRgABAQEASABIAAD/....",
    "photoContentType": "image/jpeg",
    "phone": "999999999",
    "premium": true,
    "birthDate": "2022-03-01",
    "addDate": "2022-04-30"
  },
  "userCreator": null,
  "userAssigneds": []
}
```

Return Bad Request:

```java
HttpStatus.created() "400" //*por definir
```

Info fields:

```Text
Request:
user => userData.id (Require, Int) only need id of user login in app or web
idGroup => It is generated only when the group is created
taskName => (name = "task_name", length = 50, nullable = false)
description => (name = "description", length = 100, nullable = false)

Response:
id => id's group (Autoasigned)
groupKey => key/password group (Autoasigned)
groupName => name of group
groupRelation => reason why the group exist
userData => extension of "user" for save extra data of users
userAdmin => user who created the group
taskList => group's task list (Autoasigned)
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ TASK/ADD USET TO TASK @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Add User Task ✨</summary>

REST access:

```java
@PostMapping
```

EndPoint:

```
/tasks/add-user
```

Header:

```java
null
```

Body Requireds:

```Json
{
    "idTask": "2",
    "login": "user",
    "idList": "1"
}
```

Return OK:

```java
HttpStatus.ok() "200"
```

Body response:

```json
[
   {
    "id": 2,
    "taskName": "Lavar platos",
    "dataCreate": "2022-04-18",
    "dataEnd": null,
    "description": "Lava también la taza de mi cuarto",
    "cancel": null,
    "photo": null,
    "photoContentType": null,
    "puntuacion": null,
    "taskList": {
        "id": 1,
        "nameList": "TKLMyHome"
    },
    "userData": {
        "id": 1,
        "photo": "/9j/4AAQSkZJRgABAQEASABIAAD/...",
        "photoContentType": "image/jpeg",
        "phone": "999999999",
        "premium": true,
        "birthDate": "2022-03-01",
        "addDate": "2022-04-30"
    },
    "userCreator": null,
    "userAssigneds": [
        {
            "id": 2,
            "photo": "iVBORw0KGgoAAAANSUhEUgAAAEo....",
            "photoContentType": "image/png",
            "phone": "666666666",
            "premium": true,
            "birthDate": "2022-04-01",
            "addDate": "2022-04-08"
        }
    ]
} ...
```

Return Bad Request:

```java
HttpStatus.created() "400" //*por definir
```

Info fields:

```text
Response:
idTask => id task
login => name user
idList => id list
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ TASK/DELETE USER TASK @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Delete user task ✨</summary>

REST access:

```java
@PostMapping
```

EndPoint:

```
/task/delete-user
```

Header:

```java
null
```

Body Requireds:

```Json
{
    "idTask": "2",
    "login": "admin",
    "idList": "1"
}
```

Return OK:

```java
HttpStatus.ok() "200"
```

Body response:

```json
[
  {
    "id": 2,
    "taskName": "Lavar platos",
    "dataCreate": "2022-04-18",
    "dataEnd": null,
    "description": "Lava también la taza de mi cuarto",
    "cancel": null,
    "photo": null,
    "photoContentType": null,
    "puntuacion": null,
    "taskList": {
        "id": 1,
        "nameList": "TKLMyHome"
    },
    "userData": {
        "id": 1,
        "photo": "/9j/4A...",
        "photoContentType": "image/jpeg",
        "phone": "999999999",
        "premium": true,
        "birthDate": "2022-03-01",
        "addDate": "2022-04-30"
    },
    "userCreator": null,
    "userAssigneds": [
        {
            "id": 2,
            "photo": "iVBORw0KGgoA....",
            "photoContentType": "image/png",
            "phone": "666666666",
            "premium": true,
            "birthDate": "2022-04-01",
            "addDate": "2022-04-08"
        }
    ]
} ...
```

Return Bad Request:

```java
HttpStatus.created() "400" //*por definir
```

Info fields:

```text
Response:
idTask => id task
login => name user
idList => id list
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ TASK/DELETE TASK @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Detelete task✨</summary>

REST access:

```java
@PostMapping
```

EndPoint:

```
/task/delete-task/{id}
```

Header:

```java
null
```

Body Requireds:

```Java

```

Return OK:

```java
HttpStatus.ok() "204"
```

Body response:
Return Bad Request:

```java
HttpStatus.created() "400" //*por definir
```

</details>

<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ GET/ALLTASK @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Get/ All tasks ✨</summary>

REST access:

```java
@GetMapping
```

EndPoint:

```
/task-lists
```

Header:

```java
null
```

Body Requireds:

```Json
null
```

Return OK:

```java
HttpStatus.ok() "200"
```

Body response:

```json
[
  [
    {
        "id": 1,
        "nameList": "New",
        "group": {
            "id": 1,
            "groupKey": "Tunisian payment",
            "groupName": "South",
            "groupRelationName": "explicit white",
            "addGroupDate": "2022-03-07"
        },
        "tasks": [
            {
                "id": 11,
                "taskName": "Alex",
                "dataCreate": "2022-04-24",
                "dataEnd": null,
                "description": "JORGE",
                "cancel": null,
                "photo": null,
                "photoContentType": null,
                "puntuacion": null
            }
    ]
} ...
```

Return Bad Request:

```java
HttpStatus.created() "400" //*por definir
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ Get-TaskList-Task-User@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Get/ All task for one user✨</summary>

REST access:

```java
@GetMapping
```

EndPoint:

```
/task-lists-user/{id}/{login}
```

Header:

```java
null
```

Body Requireds:

```Json
null
```

Return OK:

```java
HttpStatus.ok() "200"
```

Body response:

```json
[
  [
     {
        "id": 12,
        "taskName": "Alex",
        "dataCreate": "2022-04-24",
        "dataEnd": null,
        "description": "JORGE",
        "cancel": null,
        "photo": null,
        "photoContentType": null,
        "puntuacion": null,
        "taskList": {
            "id": 1,
            "nameList": "New"
        },
        "userData": {
            "id": 1,
            "photo": "i..",
            "photoContentType": "image/png",
            "phone": "735-497-3310",
            "premium": false,
            "birthDate": "2022-01-20",
            "addDate": "2022-01-21"
        },
        "userAssigneds": [
            {
                "id": 1,
                "photo": "iVBO...",
                "photoContentType": "image/png",
                "phone": "735-497-3310",
                "premium": false,
                "birthDate": "2022-01-20",
                "addDate": "2022-01-21"
            }
    ]
}
    ]
} ...
```

Return Bad Request:

```java
HttpStatus.created() "400" //*por definir
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ GET/ONETASK @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Get/ One task ✨</summary>

REST access:

```java
@GetMapping
```

EndPoint:

```
/task-lists/{id}
```

Header:

```java
null
```

Body Requireds:

```Json
null
```

Return OK:

```java
HttpStatus.ok() "200"
```

Body response:

```json
[
  [
    {
    "id": 1,
    "nameList": "New",
    "group": {
        "id": 1,
        "groupKey": "Tunisian payment",
        "groupName": "South",
        "groupRelationName": "explicit white",
        "addGroupDate": "2022-03-07"
    },
    "tasks": [
        {
            "id": 12,
            "taskName": "Alex",
            "dataCreate": "2022-04-24",
            "dataEnd": null,
            "description": "JORGE",
            "cancel": null,
            "photo": null,
            "photoContentType": null,
            "puntuacion": null
        },
        {
            "id": 11,
            "taskName": "Alex",
            "dataCreate": "2022-04-24",
            "dataEnd": null,
            "description": "JORGE",
            "cancel": null,
            "photo": null,
            "photoContentType": null,
            "puntuacion": null
        },
  ]
}
    ]
} ...
```

Return Bad Request:

```java
HttpStatus.created() "400" //*por definir
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ Put-UpdateTask@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Update Task✨</summary>

REST access:

```java
@PutMapping
```

EndPoint:

```
/tasks/update-tasks
```

Header:

```java
null
```

Body Requireds:

```Json
{
    "idTask": 22,
    "idGroup": 11,
    "login": "admin",
    "taskName": "Jorgeeasss",
    "description": "YA tu sabessasdsaaasasda"
}
```

Return OK:

```java
HttpStatus.ok() "200"
```

Body response:

```json
[
  [
     {
    "id": 22,
    "taskName": "Jorgeeasss",
    "dataCreate": "2022-04-25",
    "dataEnd": null,
    "description": "YA tu sabessasdsaaasasda",
    "cancel": null,
    "photo": null,
    "photoContentType": null,
    "puntuacion": null,
    "taskList": {
        "id": 11,
        "nameList": "TKLhomies22"
    },
    "userData": {
        "id": 1,
        "photo": "iVBOR..",
        "photoContentType": "image/png",
        "phone": "735-497-3310",
        "premium": false,
        "birthDate": "2022-01-20",
        "addDate": "2022-01-21"
    },
    "userAssigneds": []
}
    ]
    ]
} ...
```

Return Bad Request:

```java
HttpStatus.created() "400" //*por definir
```

</details>
</details>
<br>
<!--
  ################################ Product ################################
-->
<details>
<summary><strong>Product Features✨</strong></summary>
<br>

<!--
  ################################ Product ENTITY ################################
-->
<details>
<summary>Entity</summary>

Info variables:

```text
Response:
id => id Product
name => name Product
photo => photo Product
units => units Product
typeUnit => type Unit
note => note Product
dataCreated => date that is created by default when creating a product
shoppingDate => date that is created by default put that a product has been purchased
purchased => section to cross a product off the list when buying
user_created => User who creates a product

```

</details>

<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ TASK/CREATE NEW Product @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Create new Product ✨</summary>

REST access:

```java
@PostMapping
```

EndPoint:

```
/products
```

Header:

```java
null
```

Body Requireds:

```json
{
  "idGroup": 15,
  "idUserData": "1",
  "nameProduct": "patatas",
  "units": "2",
  "typeUnit": "kg"
}
```

Return OK:

```java
HttpStatus.created() "201"
```

Body response:

```json
{
  "id": 14,
  "name": "patatas",
  "price": null,
  "photo": null,
  "photoContentType": null,
  "units": 2.0,
  "typeUnit": "kg",
  "note": null,
  "dataCreated": null,
  "shoppingDate": null,
  "purchased": null,
  "userCreated": null,
  "userCreator": null,
  "shoppingList": {
    "id": 15,
    "total": 0.0,
    "nameShopList": "SHLPrueba 1"
  }
}
```

Return Bad Request:

```java
HttpStatus.created() "400" //*por definir
```

Info fields:

```Text
Request:
user => userData.id (Require, Int) only need id of user login in app or web
idGroup => It is generated only when the group is created
taskName => (name = "task_name", length = 50, nullable = false)
description => (name = "description", length = 100, nullable = false)

Response:
id => id's group (Autoasigned)
groupKey => key/password group (Autoasigned)
groupName => name of group
groupRelation => reason why the group exist
userData => extension of "user" for save extra data of users
userAdmin => user who created the group
taskList => group's task list (Autoasigned)
```

</details>
<!--
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@ Put-UpdateProduct @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
-->
<details>
<summary>Update Product✨</summary>

REST access:

```java
@PutMapping
```

EndPoint:

```
/products/update-products
```

Header:

```java
null
```

Body Requireds:

```Json
{
    "login": "user",
    "idGroup": "15",
    "idProduct": "14",
    "typeUnit": "Cajas",
    "name": "Patatas con sad",
    "units": "5"
}
```

Return OK:

```java
HttpStatus.ok() "200"
```

Body response:

```json
{
  "id": 14,
  "name": "Patatas con sad",
  "price": null,
  "photo": null,
  "photoContentType": null,
  "units": 5.0,
  "typeUnit": "Cajas",
  "note": null,
  "dataCreated": null,
  "shoppingDate": null,
  "purchased": null,
  "userCreated": null,
  "userCreator": null,
  "shoppingList": {
    "id": 15,
    "total": 0.0,
    "nameShopList": "SHLPrueba 1"
  }
}
```

Return Bad Request:

```java
HttpStatus.created() "400" //*por definir
```

</details>
