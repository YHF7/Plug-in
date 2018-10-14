# express 前端开发框架
1.安装
`
npm init -y //添加json初始化文件
npm install express --save//安装express
`
2.引包
`
const express = require('express');
`
3.创建服务
`
const app = express();
`
4.使用
`
app.get('/', function (req, res) {
  req.send('index.html')
})
`
# art-template 模版引擎 (配置在express中)
## 安装使用
1.安装
`
npm install --save art-template//express-art-templat依赖了art-template所以可以不用记载但是要安装
npm install --save express-art-template
`
2.配置
`
app.engine('art',require('express-art-template'))//art 可以替换成其他的标示 html 等
`
3.使用
`
app.get('/',function (req,res) {
    // 在 Express 中使用模板引擎有更好的方式：res.render('文件名， {模板对象})
  // 可以自己尝试去看 art-template 官方文档：如何让 art-template 结合 Express 来使用
    res.render('index.html',{
        title: 'hello world'
    });
});
`
4.如果希望修改默认的 views 视图渲染存储目录， 可以如下修改
`
// 第一个参数 views 不能写错
app.set('views', 目录路径)
`
# body-parser 中间件(解析表单 post 请求体)

1.安装
npm install --save body-parser
2.引包
`
const bodyParser = require('body-parser);
`
3.配置
`
// parse application/x-www-form-urlencoded 解析application
app.use(bodyParser.urlencoded({ extended: false }));
// parse application/json 解析
app.use(bodyParser.json());
`
4.使用
`
app.post('/post',function (req,res) {
    var myDate = new Date();
    var year = myDate.getFullYear(); //获取完整的年份(4位,1970-????)
    var month = myDate.getMonth() + 1; //获取当前月份(0-11,0代表1月)
    var date = myDate.getDate(); //获取当前日(1-31)
    let comment = req.body;
    comment.dateTime = year + "-" + month + "-" + date;
    comments.unshift(comment);
    res.redirect('/');
})
`

# mongoose （mongodb数据库链接插件）
1.安装
npm i -S mongoose
2.引包
const mongoose = require('mongoose');
3.配置
// 连接数据库
mongoose.connect('mongodb://localhost/test');

// 创建一个模型
// 就是在设计数据库
// MongoDB 是动态的，非常灵活，只需要在代码中设计你的数据库就可以了
// mongoose 这个包就可以让你的设计编写过程变的非常的简单
4.使用
const Cat = mongoose.model('Cat', {
    name: String
});

// 实例化一个 cat
const kitty = new Cat({
    name: 'yhf'
});
// 持久化保存 kitty 实例
kitty.save().then(() => console.log('meow'));