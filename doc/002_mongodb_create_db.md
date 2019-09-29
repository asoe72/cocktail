---
title: "MongoDB 데이터베이스 생성"
date: 2019-09-29 07:42:00 -0400
categories: MongoDB
---


# 데이터베이스(database) 생성, 사용자 추가

admin으로 로그인 한 상태에서, `cocktail` 이란 이름으로 데이터베이스를 만들고, 관리자 역할을 할 사용자를 추가해보자.

```
> use cocktail
switched to db cocktail
> db.createUser({
... user: "rainman",
... pwd: "rain123",
... roles: ["dbAdmin", "readWrite"]
... })

Successfully added user: { "user" : "rainman", "roles" : [ "dbAdmin", "readWrite" ] }
```

데이터베이스가 잘 만들어졌을까? 아래와 같이 확인해보면 `cocktail`이 보이지 않는다...??
```
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
```

좀 이상하지만, 컬렉션과 도큐먼트를 만들어야 보인다. 다음 섹션 설명을 보자.


# 컬렉션(collection)과 도큐먼트(document) 추가

`recipes`라는 컬렉션에 도큐먼트 하나를 추가해보자. 아래와 같이 도큐먼트를 삽입하면, 컬렉션도 자동으로 생성된다.

```
> db.recipes.insert({name: "Pina Colada", since: 1952})
WriteResult({ "nInserted" : 1 })
```

이제 데이터베이스 `cocktail`도 제대로 보인다.

```
> show dbs
admin     0.000GB
cocktail  0.000GB
config    0.000GB
local     0.000GB
```

MongoDB Compass Community를 실행하면 멋진 GUI로 데이터베이스들을 관리할 수 있다.

![compass_login](/doc/images/compass_login.png)

`connect` 버튼을 누르면, 좌측에 데이터베이스 `cocktail'이 보인다.

![compass_recipes](/doc/images/compass_recipes.png)
