## ✔️ Migration
Database Migration(또는 Schema Migration)은 관계형 데이터베이스에서 Schema, 즉 테이블의 정의와 테이블 간 관계 구조를 Version Control을 통해서 점진적으로 관리하는 방법이다. 간단하게 설명하자면, Database를 위한 Git 이라고 생각할 수 있다. 우리가 Git과 GitHub를 통해서 코드의 변경이력을 추적하고, 때때로 에러 등의 이유로 다시 commit을 되돌리듯이 Database의 변화를 점진적으로 기록하고, 또 이 변화를 복원할 수 있도록 만들게 된다.   

---

## ✔️ Sequelize
시퀄라이즈는 DB 작업을 쉽게 할 수 있도록 도와주는 ORM 라이브러리이다.   

---

## ✔️ ORM(Object-relational Mapping)   
OOP 간의 호환되지 않는 데이터를 변환하는 프로그래밍 기법으로 쉽게 말해 객체로 관계형 데이터베이스를 관리하는 기술이다. 대부분의 개발 언어 platform마다 제공되고 있으며, 대표적으로 spring에는 JPA가, node의 sequalize, 또 Django에는 orm이 내장되어있다.

---

### 설치
sequelize와 sequelize-cli 그리고 mysql2를 설치한다. (mysql 데이터베이스에서 사용해보겠다.)
```
npm install sequelize sequelize-cli mysql2
```

`sequelize-cli`는 시퀄라이즈 명령어를 실행하기 위한 패키지 라이브러리이다. Global 설치해도 상관이 없다.   

`mysql2`는 MySQL과 연결해주는 드라이버이다.   

설치를 완료 후 sequelize init 명령어를 실행한다.   
```
npx sequelize init
```
해당 명령어를 실행하면 아래와 같이 디렉토리와 파일이 생성이 된다.   
![스크린샷 2022-05-10 오전 2 41 17](https://user-images.githubusercontent.com/85857465/167466592-79ffd673-d9fe-4eb4-a26d-cafcdf0d00a0.png)   

**config/config.json**   
📌 여기서 config.json에 중요정보들이 많으므로 .gitignore 폴더를 하나 생성한 후 config.json 파일을 .gitignore에 넣어주면 된다.(그러면 config.json파일은 깃으로 올릴때 업로드가 안된다.)  
```javascript
{
  "development": {  //개발모드
    "username": "root", //DB와 연결할 유저 "이름"
    "password": null, //DB와 연결할 유저 "비밀번호"
    "database": "migration test", //사용할 Database 이름
    "host": "127.0.0.1", //DB 서버 호스트
    "dialect": "mysql" //DB 타입 설정 (mysql이 아니면 다른 DB 설정)
  },
  "test": {  //테스트모드
    "username": "root",
    "password": null,
    "database": "database_test",
    "host": "127.0.0.1",
    "dialect": "mysql"
  },
  "production": {  //배포모드
    "username": "root",
    "password": null,
    "database": "database_production",
    "host": "127.0.0.1",
    "dialect": "mysql"
  }
}
```

**models/index.js**   
📌 데이터베이스에서 테이블이랑 sequelize에서 model이랑 같다고 생각하면 편하다.   
models는 model(데이터베이스 테이블)들이 들어 있는 폴더이다.   
(models 안에는 기본적으로 index.js 파일이 있다. 각 폴더에서 중요한 파일을 index.js 파일이라고 생각하면 된다.)
```javascript
'use strict';

const fs = require('fs');
const path = require('path');
const Sequelize = require('sequelize');
const basename = path.basename(__filename);
const env = process.env.NODE_ENV || 'development';
const config = require(__dirname + '/../config/config.json')[env];
const db = {};

let sequelize;

//config/config.js 파일에 있는 정보를 가져와 sequelize 객체를 생성한다.
if (config.use_env_variable) {
  sequelize = new Sequelize(process.env[config.use_env_variable], config);
} else {
  sequelize = new Sequelize(config.database, config.username, config.password, config);
}

// 우리가 작성한 Table파일을 찾아온다.
fs
  .readdirSync(__dirname)
  .filter(file => {
    return (file.indexOf('.') !== 0) && (file !== basename) && (file.slice(-3) === '.js');
  })
  .forEach(file => {
    const model = require(path.join(__dirname, file))(sequelize, Sequelize.DataTypes);
    db[model.name] = model;
  });

//DB에 모델이름을 연결한다.
Object.keys(db).forEach(modelName => {
  if (db[modelName].associate) {
    db[modelName].associate(db);
  }
});

db.sequelize = sequelize;
db.Sequelize = Sequelize;

module.exports = db;
```

**migrations**   
우리가 데이터베이스에 테이블에 칼럼 정보가 변경되서나 이런 특수한 상황을 변경할 때 사용된다.   

**seeders**   
서버를 실행하거나 아니면 콘솔 창 명령어를 실행했을 때 sequelize를 통해 DB에 데이터를 생성할 때 사용된다.   

---
## ✔️ DB 생성
sequelize에서 DB를 생성하는 방법은 터미널에 명령어를 통해 사용 가능하다.   
```
npx sequelize db:create
```
위 명령어를 통해 config/config.json 파일을 읽은 후, develpment 모드에 작성되어 있는 migration test가 생성이 된다.   
![스크린샷 2022-05-10 오전 2 59 19](https://user-images.githubusercontent.com/85857465/167469577-9a58ffbe-7fe9-4866-a5d8-c6cd58a982fe.png)   
