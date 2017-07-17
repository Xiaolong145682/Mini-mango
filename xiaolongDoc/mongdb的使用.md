##  安装mongodb(ubuntu系统下的安装)
* 添加公共keyserver
```
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
```
* 在本地包数据库添加版本号:
```
$ echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
```
* 重新加载本地包数据库并进行更新：
```
$ sudo apt-get update
```
* Issue the following command:
```
sudo apt-get install -y mongodb-org
```
## 数据库的创建
* 使用use dbname 命令创建新数据库，如果dbname已经存在，那么就切换到数据库
```
> use stu
switched to db stu
> db
stu
```
* 查看数据库，需要先往数据库里写入一些数据后才能查看
```
> db.firstclass.insert({"name":"lisi", "age":12})
WriteResult({ "nInserted" : 1 })
> show dbs
local  0.000GB
stu    0.000GB
```
## 数据库的删除
* 使用db.dropDatabase() 来删除数据库
```
> use dbname //先要进入该数据库
> db //查看当前所在数据库
dbname
> db.dropDatabase() //删除当前数据库
> show dbs //查看当前所有的数据库

```
## MongoDB集合的创建和删除
### 集合的创建
```
> db.one.insert({"name":"lisi", "age":12})
WriteResult({ "nInserted" : 1 })
```
### 集合的删除
```
> db.one.drop()
true
```
## MongoDB文档操作
### 插入文档,db.collectionname.insert(doc)
```
直接插入：
> db.one.insert({"name":"lisi", "age":12})
WriteResult({ "nInserted" : 1 })
> db.one.find()
{ "_id" : ObjectId("578b4fc554ec6d203080b398"), "name" : "lisi", "age" : 12 }
>

先保存于变量中：
> doc = {"name":"zhangsan", "age":13};
{ "name" : "zhangsan", "age" : 13 }
> db.one.insert(doc);
WriteResult({ "nInserted" : 1 })
>
```
### 更新文档
* 更新方法：db.collectionName.update()
```
db.collectionName.update(
   { query},
   {update},
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
)
参数说明：
query : update的查询条件。
update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
writeConcern :可选，抛出异常的级别       
```






