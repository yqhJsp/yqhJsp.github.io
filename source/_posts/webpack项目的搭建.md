---
title: webpack项目的搭建
date: 2019-02-15 10:10:48
tags:
---
### 搭建步骤:
1、新建个文件web-demo,初始化 npm init，该文件夹下会出现package.json文件

2、安装依赖包 npm install

3、安装webpack
```bash
npm  install webpack  --sava-dev
( 注：--sava-dev是开发环境)
```
4、新建一个webpack.config.js文件

5、新建一个src文件夹，并新建一个page的文件夹，里面新建index.html\index.css\indecx.js文件

6、为使webpack启动方便，我们在package，json的scripts里配置:
```bash
"scripts": {
    "webpack": "webpack --config webpack.config.js --progress --display-modules --colors --display-reason",
  }
```
7、安装插件启动webpack的插件
```bash
npm install webpack-cli --save-dev
npm install html-webpack-plugin --save-dev
```

 8、配置webpack.config.js如下：
 ```bash
  const HtmlWebpackPlugin = require('html-webpack-plugin')
// const CleanWebpackPlugin = require('clean-webpack-plugin'); //每次构建前清理 /dist 文件夹
const path = require('path')
module.exports = {
  entry: {
    page1: __dirname + '/src/page1/index.js',// page1的入口文件，webpack是以js为入口文件的
    page2: __dirname + '/src/page2/index.js',

    //把为入口文件放在dist目录的js文件夹下，
    //name是文件名，chunkhash是每次打包文件的hash值，
    //目的是如果哪个文件修改，chunkhash会改变，可以只上线修改过的文件
    // publicPath: 'http://cdn.com/' //如果上线，可以改为线上地址
  },
  output: {
    path: __dirname + '/dist',//产出路径，一般放在dist目录下
    filename: 'js/[name]-[chunkhash].js'
  },

  //配置本地服务器
  devServer: {
    host: '127.0.0.1',
    port: 8088,
    inline: true,
    open: true,  //自动打开浏览器
    hot: false,  //慎用，打开热更新，会导致修改样式可能不支持。关闭热更新，页面会强刷
    contentBase: path.join(__dirname, "dist")
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'style-loader',
          {
            loader: 'css-loader',
            options: {
              importLoaders: 1
            }
          },
          {
            loader: 'postcss-loader',
            options: {
              plugins: function () {
                return [
                  require('autoprefixer')({
                    browsers: ["last 5 versions"]
                  }), //添加浏览器前缀
                ];
              }
            }
          },
        ],
        exclude: /node_modules/
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      filename: 'page1.html',//入口html
      template: './src/page1/index.html',
      minify: {
        // removeComments:true,   //删除注释
        // collapseWhitespace: true      //删除空格，压缩
      },
      chunks: ['page1']
    }),
    new HtmlWebpackPlugin({
      filename: 'page2.html',//入口html
      template: './src/page2/index.html',
      minify: {
        // removeComments:true,   //删除注释
        // collapseWhitespace: true      //删除空格，压缩
      },
      chunks: ['page2']
    }),
    // new CleanWebpackPlugin(['dist']),
  ]
}
```

9、运行npm run webpack打包，便可以看到项目目录出现dist文件夹，该文件夹里的文件就是打包过后的文件

10、配置本地启动的服务器localhost，处理scss，css，图片等资源

10.1、配置本地服务器：

10.2. 在 package.json 下面配置如下代码
```bash
"scripts": {
"start": "node_modules/.bin/webpack-dev-server",
"dev": "webpack --mode development"
}
```
10.3、在 webpack.config.js 引入 path
```bash 
const path = require('path');
```
10.4、在  webpack.config.js 配置 devServer
```bash
//配置本地服务器
  devServer: {
    host: '127.0.0.1',
    port: 8088,
    inline: true,
    open: true,  //自动打开浏览器
    hot: false,  //慎用，打开热更新，会导致修改样式可能不支持。关闭热更新，页面会强刷
    contentBase: path.join(__dirname, "dist")
  },
``` 
10.5、运行npm run dev然后在运行npm run start

10.6、处理CSS,SCSS文件类型：

在 index.css 下面给 body 添加背景颜色：
```bash
body{
    background-color:red
}
```
在 index.js 引入这两个 css 文件

10.6、安装处理css的插件
```bash
npm install --save-dev css-loader style-loader
 
npm install sass-loader node-sass --save-dev
 
npm install postcss-cli autoprefixer

```
然后在运行npm run start