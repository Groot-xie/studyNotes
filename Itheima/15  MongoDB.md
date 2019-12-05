# 一、数据库分类

+ 关系型数据库 ---> 表(table) ---> 记录/行(record) ---> 字段

  `mysql` / `oracle` / `sql` / `server` / `db2`

+ 非关系型数据库 ---> 集合(collection) ---> 文档(document) ---> 字段

  `MongoDB` / `redis` / `memcache`



# 二、简介

+ MongoDB 是一个非关系型数据库，属于文档型数据库(NoSql ---> Not Only Sql)
+ 对 JS 兼容好，和 node 结合最好
+ MEAN
  1. M：MongoDB
  2. E：express
  3. A：angular(vue、react)
  4. N：nodeJS



# 三、MongoDB 启动与连接

+ 通过命令 `mongod` 启动 mongodb 数据库服务
+ 重新开启一个 cmd ，输入命令 `mongo` 就可以连接到 mongod 服务了
+ 端口：27017



# 四、数据库存储路径说明

+ MongoDB 会在执行命令的磁盘根目录中查找 `data/db` 目录作为数据库文件存储路径

+ 通过命令 `mongod --dbpath` 路径修改默认配置

  #64

  `mongod --dbpath c:\data\db`

  #32

  `mongod --journal --storageEngine=mmapv1`

  `mongod --dbpath c:\data\db --journal --storageEngine=mmapv1`

+ 连接服务器说明

  + mongo 命令默认连接 MongoDB 服务：127.0.0.1:27017

  + 可以通过下面命令指定连接的主机名和端口号

    `mongo --host 127.0.0.1 --port 27017`



# 五、数据库操作

+ 查看数据库(所有数据库， 如数据库没有数据则不显示)

  `show dbs`

+ 切换(创建)数据库

  `use 数据库名`

+ 查看当前正在使用的数据库

  `db`

+ 查看当前数据库的集合

  `show collections`

+ 删除数据库

  `db.dropDatabase()`

+ 插入数据(<font color=red> **增** </font>)

  + 语法

    `db.集合名.insert({})`

    `db.集合名.insertMay([])`

  + 说明

    在 MongoDB 中不需要提前创建 ’表‘，直接通过 `db.表名.insert()` 就可以往表里添加数据

+ 查询数据( <font color=red> **查** </font> )

  + `db.collection.find().pretty()` ---> 查询所有数据 ---> .pretty() ---> 美化代码
  + `db.collection.find(name: 'jack')` ---> 指定查询条件
  + `db.collection.find(age: { $gt: 18 })`

+ 修改数据( <font color=red> **改** </font> )

  + `db.集合名.updateOne(条件, 更新后的数据)` 

    参数1：表示要修改哪条数据

    参数2：表示修改后的数据

  + `db.users.updateOne({ name: 'jack' }, { $set: { age: 20 } })`

  + `db.users.updateMany({ age: { $gt: 19 } }, { $set: { name: '中年人' } })`

+ 删除数据( <font color=red> **删** </font> )

  + `db.集合名称.deleteOne(条件)`
  + `db.users.deleteOne({ age: 18 })`
  + `db.users.deleteMany({ age: { $gte: 30 } })`

+ MongoDB 查询语句

  | 操作       | 格式                                          |
  | ---------- | --------------------------------------------- |
  | 等于       | {}                                            |
  | 小于       | `$lt` | `db.col.find({ age: { $lt: 18 } })`   |
  | 小于或等于 | `$lte` | `db.col.find({ age: { $lte: 18 } })` |
  | 大于       | `$gt` | `db.col.find({ age: { $gt: 18 } })`   |
  | 大于或等于 | `$gte` | `db.col.find({ age: { $gte: 18 } })` |
  | 不等于     | `$ne` | `db.col.find({ age: { $ne: 18 } })`   |



# 六、node 操作 MongoDB

node 通过 mongodb 模块连接 MongoDB 数据库

安装：`npm i mongodb`

+ 连接 MongoDB (保证 MongoDB 的服务是启动着的)

  ```js
  // 导入
  const mongodb = require('mongodb')
  // 专门用于连接 MongoDB 服务器的( MongoDB 客户端 )
  const MongoClient = mongodb.MongoClient
  // 连接 MongoDB 服务器
  // 参数1：数据库地址
  // 参数2：回调函数：err ---> 连接失败时的错误对象 client ---> 连接成功，client 对象用于操作数据库
  MongoClient.connect('mongodb://localhost:20717', (err, client) => {
      if (err) {}	// 失败时处理
      // 成功后通过 client 操作数据库
      // 取得数据库
      const db = client.db('itcast')
      // 获取操作的集合(表)
      const index = db.collection('index')
      // client 一定需要关闭连接
      client.close()
  })
  ```

+ 查询数据库

  ```js
  const db = client.db('itcast')
  const index = db.collection('index')
  // 多条
  index.find().toArray((err, data) => {})
  // 单条 index.findOne(条件, 回调)
  index.findOne({ name: '春春' }, (err, data) => {})
  ```

+ 插入数据库

  ```js
  // 单条插入 index.insertOne(数据， 结果(回调))
  index.insertOne({ name: 'xxh', age: 18 }, (err, result) => {
      if (err) {}
      // result 对象下有多个属性，ok表示成功
      if (result.result.ok === 1) {}
  })
  
  // 插入多条 index.insertMany(对象或数组, callback)
  index.insertMany([多个对象], (err, result) => {})
  ```

+ 删除数据

  ```js
  // 多条 index.deleteMany(条件, 回调)
  index.deleteMany({ name: '小马哥' }, (err, result) => {})
  // 单条 index.deleteOne(条件, 回调)
  ```

+ 修改操作

  ```js
  // 修改多条 index.updateMany(条件, 更新后的数据, 回调)
  index.updateMany(
      { age: { $gt: 18 } }, 
      { $set: { desc: '未成年' } }, 
      (err, result) => {}
  )
  // 修改单条
  index.updateOne()
  ```

  

# 七、前后端分离思想

一般项目中，首屏采用后端渲染，页面下面的内容采用前端渲染，需要的时候才会发送请求渲染数据

+ 后端渲染

  在服务端读取模块页面和数据，渲染成 html 返回给浏览器

+ 前端渲染

  服务端提供接口，前端调用端口获取数据，在页面中完成模板渲染



# 八、CORS 跨域资源共享

如果使用 CORS 处理跨域的问题，只需要服务器设置响应头即可

`res.set('Access-Control-Allow-Origin', '*')`

