```javascript
/* 
  webpack是一个Node.js的模块化性文件
*/
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const ExtractTextWebpackplugin = require('extract-text-webpack-plugin')
const CopyWebpackPlugin = require('copy-webpack-plugin')
module.exports = {
  // 入口文件
      //entry: 入口文件的相对路径（网络路径）
      entry: {//多页面
        // key: value   key就是入口文件的名称， 值就是入口文件的路径
        index: path.resolve(__dirname,'../src/index.js'),
        app: path.resolve(__dirname,'../src/app.js')
      },   
  // 出口文件
      // output: {path,filename} path是出口目录的磁盘路径 ， filename指的是出口目录中文件的名称
      output: {
        path: path.resolve(__dirname,'../dist'),
        // filename: `js/app_[hash:6].js`
        filename: 'js/[name]_[hash:6].js'
      },
  // 转换器
  module: {
    rules: [
      // 优雅降级
          {
            test: /\.js$/,
            exclude: /node_modules/,
            use: [{
              loader: 'babel-loader',
              options: {
                presets: ['@babel/preset-env']
              }
            }]
          },
      // css解析
          {
            test: /\.css$/,
            use: ExtractTextWebpackplugin.extract({
              use: 'css-loader'
            })
          },
      // 图片打包   5000kb 以上直接拷贝到dist目录， 5000以下将图片转成base64
          {
            test: /\.(png|jpg|gif|svg)/,
            use: [
              {
                loader: 'url-loader',
                options: {
                  limit: 5000,
                  outputPath: 'img/'
                }
              }
            ]
          }
        ]
      }, 
      

  // 插件
      plugins: [
        new HtmlWebpackPlugin({  // Also generate a test.html
          filename: 'index.html',
          template: path.resolve(__dirname,'../index.html')
        }),

        //css代码抽离的插件实例化
        new ExtractTextWebpackplugin('css/[name]_[hash:6].css'),
        new CopyWebpackPlugin([
          {
            from: path.resolve(__dirname,'../src/static'),
            to: path.resolve(__dirname,'../dist/static')
          }
        ])
      ],
  // 环境配置
      mode: 'development', // production
  // 前端服务器配置
      devServer: {
        open: true,
        port: 8000,
        hot: true // 【HMR】 hot module replacement
      },
  // 文件后缀可以省略
      resolve: {
        extensions: ['.js','.css','.vue']
      },
      
}
```

