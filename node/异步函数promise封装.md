# 异步函数顺序控制 Promise 封装

``` JavaScript
// 获取读取文件函数
const fs = require('fs');

// 封装一个异步函数
function pReadFile(filePath) {
    return new Promise(function (resolve, reject) {
        fs.readFile(filePath, 'utf8', function (err, data) {
            if (err) {
                reject(err);
            } else {
                resolve(data)
            }
        })
    })
}

// 启动行数传入地址值 .then 获取返回多函数
pReadFile('./data/a.txt').then(function (data) {
    console.log(data);
    // 当 p1 读取成功的时候
    // 当前函数中 return 的结果就可以在后面的 then 中 function 接收到
    // 当你 return 123 后面就接收到 123
    //      return 'hello' 后面就接收到 'hello'
    //      没有 return 后面收到的就是 undefined
    // 上面那些 return 的数据没什么卵用
    // 真正有用的是：我们可以 return 一个 Promise 对象
    // 当 return 一个 Promise 对象的时候，后续的 then 中的 方法的第一个参数会作为 pReadFile('./data/b.txt') 的 resolve
    // 传入地址进行异步函数操作
    // return 执行第二个回调函数
    return pReadFile('./data/b.txt')
}).then(function (data) {
    console.log(data);
    return pReadFile('./data/c.txt')
}).then(function (data) {
    console.log(data);
})
```