# ORM

>  ORM ( Object Relational Mapping )은 어플리케이션과 데이터베이스 사이를 맵핑시켜주는 도구이다. 데이터베이스에서  row 쿼리문을 작성하지 않고도 데이터베이스를 다룰 수 있다. ORM은 특정 DB에 종속되지 않고, 가독성 높은 코드를 작성할 수 있게 해준다. 



## Sequelize

> ORM은 많은 종류가 있지만 Node에서 가장 많이 사용되는 ORM은 Sequelize이다. Sequelize의 가장 큰 특징은 Promise를 기반으로 동작한다는 것이다.



#### Install Sequelize

```
npm install --save sequelize

npm install -g sequelize-cli
```



#### Init Sequelize

```js
/* config/config.json 파일이 생성된다 */
$ sequelize init:config

/* models/index.js 파일이 생성된다. */
$ sequelize init:medels
```



#### config Sequelize

> 데이터베이스와 관련된 설정값을 입력한다. `NODE_ENV` 에 따라 다른 값을 사용하기 때문에 사용할 `NODE_ENV` 를 꼭 확인한다.

```
{
  "development": {
    "username": "testUser",
    "password": "1234567",
    "database": "testDB",
    "host": "SOMEWHERE",
    "dialect": "mysql",
    "port": "3306"
  },
  "test": {
    "username": "root",
    "password": null,
    "database": "database_test",
    "host": "127.0.0.1",
    "dialect": "mysql"
  },
  "production": {
    "username": "root",
    "password": null,
    "database": "database_production",
    "host": "127.0.0.1",
    "dialect": "mysql"
  }
}

```



#### define Model

> 데이터베이스의 스키마를 설정해주는것과 비슷한 작업이다. 

```js
'use strict';

require('dotenv').config();

const Sequelize = require('sequelize');

const env = process.env.NODE_ENV || 'development';
const config = require('../../config/sequelize.json')[env];

const db = {};

const sequelize = new Sequelize(
  config.database,
  config.username,
  config.password,
  config,
);

db.sequelize = sequelize;
db.Sequelize = Sequelize;

//모델정보를 읽어온다.
db.Users = require('./users')(sequelize, Sequelize);

//모델간의 관계를 설정.
db.Users.hasMany(db.Challenges, { foreignKey: 'challenger', sourceKey: 'id' });
db.Challenges.belongsTo(db.Users, {
  foreignKey: 'challenger',
  targetKey: 'id',
});

module.exports = db;
```

```js
//define model
module.exports = (sequelize, DataTypes) => sequelize.define('users', {
  id: {
    type: DataTypes.INTEGER,
    primaryKey: true,
    autoIncrement: true,
    unique: true,
  },
  email: {
    field: 'email',
    type: DataTypes.STRING(50),
    unique: true,
    allowNull: false,
  },
    ...
});
```



#### example INSERT

```js
models.<table_name>.create({
    col_one : 'value_one',
    col_two : 'value_two',
    ...
}).then( result => {
    res.json(result); 
}).catch( err => {
    throw err;
})
```



#### example UPDATE

```js
models.<table_name>.update({ target_col : 'new_value'},
                           { where : { col_one : 'value }
}).then( result => {
     res.json(result);
}).catch( err => {
    throw err;
})
```



#### example DELETE

```js
models.<table_name>.destroy({where : { col_name : 'value' }
}).then( result => {
    res.json(result);
}).catch( err => {
    throw err
})
```

