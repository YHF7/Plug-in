# node连接mysql

## 安装
``` bash
npm i -S mysql
```

## 使用
``` JavaScript
// 加载mysql
var mysql = require('mysql');
// 1.创建连接
var connection = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: '',
    database: 'users'
});
// 2.连接数据库
connection.connect();
// 3.执行数据操作
// 查询数据
connection.query('SELECT * FROM `users`', function (error, results, fields) {
    if (error) throw error;
    console.log('The solution is: ', results);
});

// 添加数据
// connection.query('INSERT INTO users VALUES(null,"admin","123456")', function (error, results, fields) {
//     if (error) throw error;
//     console.log('The solution is: ', results);
// });

// 4.关闭连接
connection.end();
```