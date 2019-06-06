---
title: Mongodb
categories: ['数据库']
tags: ['Mongodb'] 
---

### 一、 基础Shell命令。
- show dbs :显示已有数据库，如果你刚安装好，会默认有local、admin(config)，这是MongoDB的默认数据库，我们在新建库时是不允许起这些名称的。
- use admin： 进入数据，也可以理解成为使用数据库。成功会显示：switched to db admin。9（如果当前数据库名字不存在则建立该名字的数据库，但是在没有集合前，它还是默认为空。）
- show collections: 显示数据库中的集合（关系型中叫表，我们要逐渐熟悉）。
- db:显示当前位置，也就是你当前使用的数据库名称，这个命令算是最常用的，因为你在作任何操作的时候都要先查看一下自己所在的库，以免造成操作错误。
### 二、 数据操作基础命令：

- use db（建立数据库）：use不仅可以进入一个数据库，如果你敲入的库不存在，它还可以帮你建立一个库。但是在没有集合前，它还是默认为空。
- db.集合.insert( ):新建数据集合和插入文件（数据），当集合没有时，这时候就可以新建一个集合，并向里边插入数据。Demo：db.user.insert({“name”:”jspang”})
- db.集合.find( ):查询所有数据，这条命令会列出集合下的所有数据，可以看到MongoDB是自动给我们加入了索引值的。Demo：db.user.find()
- db.集合.findOne( ):查询第一个文件数据，这里需要注意的，所有MongoDB的组合单词都使用首字母小写的驼峰式写法。
- db.集合.update({查询},{修改}):修改文件数据，第一个是查询条件，第二个是要修改成的值。这里注意的是可以多加文件数据项的，比如下面的例子。
```
db.jspang.update({"name":"jspang"},{"name":"jspang","age":"32"})
```
- db.集合.remove(条件)：删除文件数据，注意的是要跟一个条件。Demo:db.user.remove({“name”:”jspang”})
- db.集合.drop( ):删除整个集合，这个在实际工作中一定要谨慎使用，如果是程序，一定要二次确认。
- db.dropDatabase( ):删除整个数据库，在删除库时，一定要先进入数据库，然后再删除。实际工作中这个基本不用，实际工作可定需要保留数据和痕迹的。
### 三、在操作数据库时要注意两个能力：

1. 第一个是快速存储能力。
2. 第二个是方便迅速查询能力。
### 四、 批量插入
```
db.test.insert([
    {"_id":1},
    {"_id":2},
    {"_id":3}
])
```
> 1. 注意一次插入不要超过48M，向.zip和大图片什么的尽量用静态存储，MongoDB存储静态路径就好，这也算是一个规则。 
> 2. 数据插入选用批量插入性能远远大于循环插入。
### 五、 update修改器
1. 修改非嵌入文档
```
dbd .workmate.update({"name":"MinJie"},{"$set":{sex:2,age:21}})
```
2. 修改嵌入文档
```
db.workmate.update({"name":"MinJie"},{"$set":{"skill.skillThree":'word'}})
```
3. $unset用于将key删除
```
db.workmate.update({"name":"MinJie"},{$unset:{"age":''}})
```
4. $inc对数字进行计算
```
db.workmate.update({"name":"MinJie"},{$inc:{"age":-2}})
```
5. multi选项
```
db.workmate.update({},{$set:{interset:[]}})
```
> 只改变了第一个数据
```
db.workmate.update({},{$set:{interset:[]}},{multi:true})
```
> 每个数据都发生了改变，multi是有ture和false两个值，true代表全部修改，false代表只修改一个（默认值）
6. upsert选项
```
db.workmate.update({name:'xiaoWang'},{$set:{age:20}},{upsert:true})
```
> upsert是在找不到值的情况下，直接插入这条数据。upsert也有两个值：true代表没有就添加，false代表没有不添加(默认值)。
### 六. update数组修改器
1. $push追加数组/内嵌文档值
```
db.workmate.update({name:'xiaoWang'},{$push:{interest:'draw'}})
```
> $push的功能是追加数组中的值
```
db.workmate.update({name:'MinJie'},{$push:{"skill.skillFour":'draw'}})
```
> $push修饰符内嵌文档增加值
2. $ne查找是否存在
```
db.workmate.update({name:'xiaoWang',"interest":{$ne:'playGame'}},{$push:{interest:'Game'}})
```
> 如果xiaoWang的爱好（interest）里没有palyGame这个值，我们就加入Game这个爱好。总结：没有则修改，有则不修改。
3. \$addToSet 升级版的\$ne
```
db.workmate.update({name:"xiaoWang"},{$addToSet:{interest:"readBook"}})
```
> 我们现在要查看小王(xiaoWang)兴趣(interest)中有没有阅读（readBook）这项，没有则加入读书(readBook)的兴趣.
4. $each 批量追加
```
var newInterset=["Sing","Dance","Code"];
db.workmate.update({name:"xiaoWang"},{$addToSet:{interest:{$each:newInterset}}})
````
> 它可以传入一个数组，一次增加多个值进去，相当于批量操作，性能同样比循环操作要好很多，这个是需要我们注意的，工作中也要先组合成数组，然后用批量的形式进行操作.
5. $pop 删除数组值
```
db.workmate.update({name:'xiaoWang'},{$pop:{interest:1}})
```
> $pop只删除一次，并不是删除所有数组中的值。而且它有两个选项，一个是1和-1。

> 1：从数组末端进行删除,
> -1：从数组开端进行删除
6. 数组定位修改
```
db.workmate.update({name:'xiaoWang'},{$set:{"interest.2":"Code"}})
```
### 七、修改：状态返回与安全


