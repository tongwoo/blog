---
layout: post
title: '使用PDO开启事务无法执行SAVEPOINT'
date: 2018-04-02
author: wutong
tags:  php mysql pdo
---

在使用Yii框架事务嵌套的时候出现了错误 `SQLSTATE[HY000]: General error: 2014 Cannot execute queries while other unbuffered queries are active. Consider using PDOStatement::fetchAll(). Alternatively, if your code is only ever going to run against mysql, you may enable query buffering by setting the PDO::MYSQL_ATTR_USE_BUFFERED_QUERY attribute.`  

### 问题呈现

代码中不同位置多次调用了 `Yii:$app->db->beginTransaction()` 方法，Yii创建了 `SAVEPOINT LEVEL1` 的SQL语句，但是执行的时候报错，具体错误信息见上方。

### 解决过程

按照文档上提示的方法 `closeCursor()` 和 连接属性 `PDO::MYSQL_ATTR_USE_BUFFERED_QUERY` 都没有解决。

尝试自己写PDO操作代码，运行成功。

经过长时间的检查找到在PDO连接数据库的配置中，Yii配置中我多加了一个选项 `PDO::ATTR_EMULATE_PREPARES`

```php
'db' => [
    'class' => 'yii\db\Connection',
    'charset' => 'utf8',
    ........
    'attributes'=>[
        PDO::ATTR_EMULATE_PREPARES => false,
    ],
],
```

将其改为 `true` 或者删除即可，但是带来的另外一个问题就是查询返回的数据都是字符串了，所以在需要在合适的地方去手动执行这个参数设置，比如在需要 `SAVEPOINT` 的地方前面加上 `PDO::setAttribute(PDO::ATTR_EMULATE_PREPARES,0); `，执行完毕后再改回来