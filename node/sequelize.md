# Sequelize

자바스크립트 객체와 관계형 데이터베이스를 연결해 주는 ORM 패키지.  
자바스크립트로 SQL을 다룰 수 있다.

## 설치

```bash
$ npm i sequelize sequelize-cli
# 아래 중 환경에 맞는 DB 드라이버 선택해서 패키지 설치
$ npm i pg pg-hstore        # postgresql
$ npm i mysql2              # mysql
$ npm i mariadb             # mariadb
$ npm i sqlite3             # sqlite
$ npm i oracledb            # oracle

# sequelize 적용
$ npx sequelize init
```

*`sequelize-cli`는 CLI에서 sequelize를 사용할 수 있게 하는 모듈이다.*  
*`npx sequelize init`으로 config, models, migrations, seeders 디렉토리 자동 생성된다.*

## 사용

### 1. 설정 파일

```json
// config/config.json
{
    "development": {
        "username": "root",
        "password": "mysql",
        "database": "test",
        "host": "127.0.0.1",
        "dialect": "mysql"
    },
    "production": {
        "username": "postgres",
        "password": "postgres",
        "database": "vm",
        "host": "localhost",
        "dialect": "postgres"
    }
}
```

**config 호출**  
dev: `const config = require('config/config')["development"]`  
prod: `const config = require('config/config')["production"]`

### 2. DB 연결

``` javascript
// models/index.js
const Sequelize = require('sequelize');
const env = process.env.NODE_ENV || "development";
const config = require('config/config')[env];
const User = require('models/User');

//new Sequelize('database', 'username', 'password', { host: "IP", dialect: "postgres" })
const sequelize = new Sequelize(config.database, config.username, config.password, config);

const db = {};
db.sequelize = sequelize;
db.User = User;

User.init(sequelize);
User.associate(db);

module.exports = db;
```

### 3. 모델 생성

`sequelize.define`로 모델 생성

```javascript
// models/User.js
const { Sequelize, DataTypes } = require('sequelize');
const sequelize = new Sequelize('');

const User = sequelize.define('User', {
    username: {
        type: DataTypes.STRING(20),
        allowNull: false
    },
    password: {
        type: DataTypes.STRING(200),
    }
}, {
    // Model Options
    timestamp: true,
    paranoid: false,
    underscored: false,
    modelName: "User",
    tableName: "users",
    charset: "utf8mb4",
    collate: "utf8mb4_general_ci"
});

module.exports = User;
```

`Model` 상속으로 모델 생성

```javascript
// models/User.js
const Sequelize = require('sequelize');

module.exports = class User extends Sequelize.Model {
    static init(sequelize) {
        return super.init({
            username: {
                type: Sequelize.STRING(20),
                allowNull: false,
            },
            password: {
                type: Sequelize.STRING(200),
                allowNull: false,
            },

        }, {
            // Model Options
            sequelize,
            timestamp: true,
            paranoid: false,
            underscored: false,
            modelName: "User",
            tableName: "users",
            charset: "utf8mb4",
            collate: "utf8mb4_general_ci"
        });
    }

    // 모델 간 관계 
    static associate(db) {
        // 1:N 관계 정의
        db.User.hasMany(db.Post);
        // 같은 테이블 간 N:M 관계 정의
        // User(Follower) - Follow - User(Following)
        db.User.belongsToMany(db.User, {
            foreignKey: 'followingId',      // 컬럼명
            as: 'Followers',                // foreignKey와 반대되는 모델 - 같은 테이블 간 N:M 관계 정의할 때만 사용
            through: 'Follow'               // 모델명
        });
        db.User.belongsToMany(db.User, {
            foreignKey: 'followerId',
            as: 'Followings',
            through: 'Follow'
        })
    }
}
```

### 4. DB 생성

```bash
$ npx sequelize db:create
Sequelize CLI [Node: , CLI: , ORM: ]

Loaded configuration file "config/config.json".
Using environment "development".
Database vm created.
```

## CRUD
