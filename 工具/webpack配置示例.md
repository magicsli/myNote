```javascript
/*  webpack 是一个Node.js的模块化性文件 */

const path = require('path')
const HtmlwebpackPlugin = require('html-webpack-plugin')

module.exports = {
//   entry  入口文件的相对路径 或者 ( 网络路径   )
    entry: './src/index.js',     // 单文件

// output 出口文件 有两个参数 ( path,  filename )
    output:{
        path:path.join(__dirname, 'dist'),  // 出口目录的磁盘路径
        filename:'main.js'                  // 出口目录中的文件名称
    }, 
    mode: 'development',  // ( 开发环境 )  或者 production ( 生产环境 )
    module:{
        rules:[
                {  
                    test:/\.css$/,
                    use: ['style-loader', 'css-loader']
                }
            ]
    },
    // 前端服务器配置
    devServer:{
        open:true
    },
    // 插件
    plugins:[
        new HtmlwebpackPlugin({
            filename:'index.html',
            template:'./index.html'
        })
    ],
    // 文件后缀可以省略
    resolve:{
        extensions:['.css', '.js', '.jsx']
    }
}
```

