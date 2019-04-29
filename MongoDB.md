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







### mongoose 模块

​	**安装**:   `npm install mongoose`

​	**连接数据库**

​			1, 确保mongodb数据库的正常运行

​			2, 引入mongoose模块

​			3, 连接数据库:  

​	**`mongoose.connect("mongodb:127.0.0.1:27017/数据库名")`**

步骤:

​	// **安装mongoose**

​		`npm install mongoose`

​	// **导入**

​		`const mongoose = require("mongoose");`

​	// **连接数据库**

​		`mongoose.connect("mongodb://主机名:端口/数据库名称")`

​		// **举例**

​		`mongoose.connect("mongodb://127.0.0.1:27017/test", (err) => {`

`if(!err){`

​	`console.log("服务器连接成功")`

`}elsr{`

​	`throw err`

}

`})	`



### 新增数据  

​	**Schema**骨架 :    

​		 一种以文件形式存储的数据库模型骨架, 不具备数据库的操作能力



​	**Model** 模型 :  

​		  由**`Schema`**发布生成的模型, 具有抽象属性和行为的数据库操作对



​	**Entity**  实体 :    

​		  由**`Model`**创建的实体, 他的操作也会影响数据库

​		

###**存储数据的步骤**:

​	定义**Schema**(骨架)  ==>  创建**`model`**(模型)  ==> **`Entity`**(实例化方法)



#### **定义骨架**

```
	const mongoose = require("mongoose");
	const Schema = mongoose.Schema;
	
	const teacherSchema = new Schema( options ) 
	
	/*
		options = {
            key : key 的数据类型
		}
	*/
	
	完善:
		const teacherSchema = new Schema({
            id : Number,
            name : String,
            age : Number
		})
	
	
```

#### **创建模型**                      ----- 创建集合

​	

```
const teacherModel = mongoose.model("集合的名称", "定义好的骨架")
```



#### 创建实例                     -----  创建文档



```
const  teacherEnitity = new teacherModel()
```





#### 数据的存储      实例.save( (err, user) => {  *** } )

​	

```
teacherEnitity.id = 5

	teacherEnitity.name = "jack"

	teacherEnitity.age = 16



teacherEnitity.save( (err,  data) => {

	if(err) {

		console.log(err)

	}elsr{
	
        console.log(data)
        
	}

} )


```

#### 数据的查询  



+ **teacherModel.find( {name: }, (err, users) => { } )**

+ **teacherModel.findByid(id, (err, doc) => {  } )**

+ 

```
teacherModel.find({age: 10}, (err, result) => {
   
   if(!err){
       
       console.log(result)
       
       const id = result[0]._id
       
       // 根据查找的第一个实例的id再进行精确查找
       teacherModel.findByid(id, (err, doc) => {
       
       	 //删除查找到的文档
       doc.remove( ()=> console.log("delete data success ~") )
       
       })
      
   }else{
   
       console.log(err)
       
   }
   
})
```



#### 数据的修改

​	

```
teacherModel.find( {name:"yanyabing"}, (err, res)=>{
    if(!err){
        
        const id = res[0]._id;
        teacherModel.findByid(id, (err, doc)=>{
            doc.age = 18,
            doc.save( (err)=>{
                if(!err){
                    console.log("data updata success~~")
                }else{
                    throw "data updata error"
                }
            } )
            
        })
        
    }else{
    
    
    }
} )
```

​    

数据库名称: maoyan

​	大写: 

​		1, 稳定性高,

​		2, 辨识度高

