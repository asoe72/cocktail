---
title: "MongoDB 설치와 실행, admin 계정 생성과 접속"
date: 2019-09-28 09:54:00 -0400
categories: MongoDB
---

# MongoDB 설치

MongoDB를 설치한다. 운영체계와 설치한 MongoDB 버전은 각기 아래와 같다.

    Windows 10 Home 64bit

    MongoDB Server
    Version 3.6.13

윈도우의 `환경변수 - 시스템 변수`에 아래를 추가한다.

```
C:\Program Files\MongoDB\Server\3.6\bin
```

데이터베이스들을 보관할 폴더 `mongo_db/`를 생성한다. 서브 폴더로 `mongo_db/local/`을 만든다.

이제 `mongo_db/`에 아래와 같이 daemon(서버)을 실행할 배치파일 `mongodb_start.bat`을 만든다.

```
mongod --auth --dbpath e:/mongo_db/local
```

`mongodb_start.bat`을 실행하면, port 27017에서 connection을 대기한다는 메시지가 나온다.

이제, 명령 프롬프트를 열고 mongoDB shell을 실행한다.

```
C:\Users\...>mongo
```

# admin 계정 생성

admin db를 선택하고 admin 계정을 추가한다.

```
> use admin
switched to db admin
> db.createUser({
... user: "admin",
... pwd: "p1234",
... roles:["userAdminAnyDatabase",
... "userAdmin",
... "readWrite",
... "dbAdmin",
... "clusterAdmin",
... "readWriteAnyDatabase",
... "dbAdminAnyDatabase"]});

Successfully added user: {
        "user" : "admin",
        "roles" : [
                "userAdminAnyDatabase",
                "userAdmin",
                "readWrite",
                "dbAdmin",
                "clusterAdmin",
                "readWriteAnyDatabase",
                "dbAdminAnyDatabase"
        ]
}
```

mongoDB shell을 빠져나간다.

```
> exit
bye
```

mongoDB shell을 다시 실행해서, admin으로 로그인해본다.

```
C:\Users\...>mongo admin -uadmin
MongoDB shell version v3.6.13
Enter password:
connecting to: mongodb://127.0.0.1:27017/admin?gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("3098a815-aed8-4537-a922-5d0bbf7460ba") }
MongoDB server version: 3.6.13
>
```

혹은, shell 실행 후 admin db 선택하고 auth로 로그인한다.
결과가 1로 나오면 성공한 것이다.

```
C:\Users\...>mongo
MongoDB shell version v3.6.13
> use admin
switched to db admin
> db.auth("admin", "p1234")
1
```

# 참고자료
- [Do it! Node.js 프로그래밍](http://www.yes24.com/Product/Goods/36886447)
- https://ijeee.tistory.com/12
- http://blog.naver.com/PostView.nhn?blogId=oidoman&logNo=221238334996&parentCategoryNo=&categoryNo=&viewDate=&isShowPopularPosts=false&from=postView
- https://stackoverflow.com/questions/27784956/error-couldnt-add-user-not-authorized-on-test-to-execute-command-createuser
