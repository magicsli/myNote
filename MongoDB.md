### MongoDB数据库 ( 存储格式为bson )

​	

- 分类:
  - 关系型数据库:  MySQL
  - 非关系型数据库: MOngoDB
- 差异:
  - 关系型数据库是有表和表之间的关系组成的, `nosql`是由集合组成的, 集合下面是很多的文档
  - 非关系型数据库文件存储格式为`bson`(一种`json`的扩展)

MongoDB安装

- 1,  环境变量设置
- 2,   系统服务添加有问题

**MongoDB的存储数据形式 bson** (可以存储二进制)

​	bson 是一种类似json的二级制形式的存储格式, 支持文档对象和数组对象







### MOngoDB的操作命令

​	MongoDB的连接地址  ==>    `mongodb://127.0.0.1:27017`







**MongoDB**

​	数据库  ==>   集合  ==>  文档









#### 针对数据库的操作





**创建 / 切换数据库       `use  db_name`**

​	如果没有我们要切换的数据库, 那么就会新建一个

​	如果已存在, 那么就切换到那个数据库



**查询所有数据库   `show  dbs`**

​	将我们本地的所有的数据库列出来



**查看当前使用的数据库     ` db / db.getName() `**

​	

**显示当前数据库的状态     `db.states()`**



**查看当前数据库的版本     `db.version()`  **



**查看当前数据库的连接地址    `db.getMongo()`** 



**删除数据库   	`db.dropDatabase()`**







#### 针对集合的操作



​	**创建一个集合**

​		`db.createCollection("collName", {size:20, capped:true, max:100})`



​	**判断集合是否为定容量** 

​       	 `db.collName.isCapped()`



​	**得到指定名称的集合**

​		`db.getCollection("account");`



​	**得到当前db的所有集合**

​		`db.getCollectionNames();`



​	**显示当前db所有集合的状态**

​		`db.printCollectionStats()`





#### 针对文档(document)的操作



​	**查询数据**        `db.users.find()`  // 查看所有文档

​			      `db.users.findOne()` 	// 查看一个文档



​	**添加文档**       `db.users.save({name:"zhangsan", age:"25"})`

​			     `db.users.insert({name:"zhangsan", age:"25"})`

​			     `db.users.insertOne({name:"zsan", age:"25"})`



​	**修改文档**       db.users.updata({name:"tom"},{ age:"89" })

​	`db.users.update({age:25}, {$set:{name:"changeName"}}, false, true)`





**db.coll_name.update(arg1, arg2, arg3, arg4) 参数解释** 

​	1, arg1:  **匹配条件**

​	2, arg2:  **修改的具体内容**

​			`{$set:{name:"吴亦凡"}} `        **修改这一条**

​			`{$inc:{name:"吴亦凡"}}` 	**增加这一条**

​			

​	3, arg3:      **匹配几条**

​			1, false: **修改一条**

​			2, true:   **全部修改**

​	4,arg4       **false /  true**     **修改几条**

​		









​	**删除文档**       `db.users.remove({name:"zhangsan"})`



​	



###多重查询:

​		**查询所有记录**

​			`db.userlnfo.find()`

​		**查询去重后数据**

​			`db.userlnfo,distince("name")`

​		**查询age = 22的记录**

​			`db.userlnfo.find("age":22)`

​		**查询age>22的记录**

​			`db.userlnfo.find({age:{$gt:22}})`

​		**查询age<22的记录**

​			`db.userlnfo.find({age:{$lt:22}})`

​		**查询age>=25的记录**

​			`db.uderlnfo.find({age:{$gte:25}})`

​		**查询age<=25的记录**

​			`db.userlnfo.find({age:{$lte:25}})`

​		**查询age>=23并且age<=26的记录**

​			`db.userlnfo.find((age:{$gte:23,  ​$lte:26}})`

​		**查询name中包含Mongo的数据**

​			`db.userlnfo.find({name:/mongo/})`

​		**查询name中以Mongo开头的**

​			`db.userlnfo.find({name:/^mongo/})`



**db,coll_name.find(arg1, arg2) 所有的**

 	参数解释:

​	arg1: 表示的是匹配条件

​	arg2: 表示将来输出的内容匹配,  **0 表示不予**,  **1 表示要**



例子 

​	

```
db.movies.find({year:'1993'}, {_id:0, title:1})
```



**排序 > skip > limit**   权重等级



**升序**

​	 

```
db.movies.find({year:'1993'}, {_id:0, title:1}).sort({year:1})
```





**降序**



```
db.movies.find({year:'1993'}, {_id:0, title:1}).sort({year:-1})
```





**截取    `limit`**



```
db.movies.find({year:'1993'}, {_id:0, title:1}).limit(5)
```





**`skip`从哪一条开始查**  



```
db.movies.find({year:'1993'},{_id:0, title:1}).skip(5).limit(3)          // 从第五条开始, 截取两条                                    
```



**`$or` 表示或者**  可以匹配多个条件

```
db.coll_name.find({$or:[{age:10}, {age:40}]})
```



**.count()** 查询到的文档有多少条

​	db.coll_name.find({$or:[{age:10}, {age:40}]}).count()