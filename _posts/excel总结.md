# excel 总结

 - mongoDB

MongoDB教程是为初学者和专业人士设计的，在本系列教程中提供了SQL的基本和高级概念。MongoDB是一个NoSQL数据库。 它是一个使用C++编写的开源，跨平台，面向文档的数据。

用法：

    // 进入 /usr/local
    cd /usr/local

    // 下载
    sudo curl -O https://fastdl.mongodb.org/osx/mongodb-osx-x86_64-3.4.2.tgz

    // 解压
    sudo tar -zxvf mongodb-osx-x86_64-3.4.2.tgz

    // 重命名为 mongodb 目录

    sudo mv mongodb-osx-x86_64-3.4.2 mongodb

    // 设置全局变量
    export PATH=/usr/local/mongodb/bin:$PATH

    // 启动本地mongodb数据库
    sudo mongod

    // 连接本地mongodb数据库
    mongo

    // 标准连接语法
    mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]

    #// 在连接成功的情况系
    // 查看数据库
    show dbs

    // 新建 选择数据库
    use dbName

    // 删除数据库
    db.dropDatabase()

    // 创建集合
    db.createCollection(name, options)

    // 删除集合
    db.collectionName.drop()

    // 查询
    db.collectionName.find(where);
    db.collectionName.count();

    // 索引
    db.collectionName.createIndex(key, options)
    db.col.getIndexes()

 - NoSQL数据库
 
泛指非关系型的数据库。产生就是为了解决大规模数据集合多重数据种类带来的挑战，尤其是大数据应用难题。

 - 关系型数据库

在关系型数据库当中一个表就是一个关系，一个关系数据库可以包含多个表。

[mongoDB参考资料][1]

 [1]: https://www.cnblogs.com/clsn/p/8214194.html#auto_id_28