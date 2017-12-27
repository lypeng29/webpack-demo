# webpack-demo

最新版webpack3.8.1的一个最基础的demo

参见网址：https://webpack.js.org/guides/getting-started/

教你一步步了解使用webpack

本实例根据上面网址做的最基础的配置，你可以按下面步骤体验：

1. clone代码
git clone https://github.com/lypeng29/webpack-demo.git
2. 进入webpack-demo目录，执行npm install安装package.json中的依赖库
npm install
3. 打包js到build.js
npm run build（等价于：webpack --config webpack.config.js）
4. 访问
浏览器访问：dist/index.html，即可看到：Hello webpack

2017-11-21
npm install --save-dev something...
--save-dev会自动将安装的包，写入到package.json文件

静态资源文件导入，打包！包括css image font data等，完整配置如下：

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
  entry: {
  	app: './src/index.js',
  	print: './src/print.js',
  },
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
   module: {
     rules: [
       {
         test: /\.css$/,
         use: [
           'style-loader',
           'css-loader'
         ]
       },
		{
         test: /\.(png|svg|jpg|gif)$/,
         use: [
           'file-loader'
         ]
       },
		{
         test: /\.(woff|woff2|eot|ttf|otf)$/,
         use: [
           'file-loader'
         ]
       }              
     ]
   }
};
```


### HtmlWebpackPlugin

打包所有文件到dist，包括index.html，不用事先写好index.html

### CleanWebpackPlugin

创建所有文件之前清空dist目录
npm install --save-dev clean-webpack-plugin


### watch

在package.json中增加`"watch": "webpack --watch"`，然后运行npm run watch，将监视目录，修改保存后自动生成文件，不用再执行一次npm run build！


### webpack-dev-server

1. npm install --save-dev webpack-dev-server
2. 修改webpack.config.js   
  devtool: 'inline-source-map',
  devServer: {
  	contentBase: './dist'
  },
3. 修改package.json，新增："start": "webpack-dev-server --open"
4. 运行npm run start，浏览器将打开localhost:8080地址
5. 修改src中的文件保存后，重新打包生成dist，浏览器页面自动刷新


### webpack-dev-middleware

webpack-dev-middleware与webpack-dev-server，感觉不出有多大差异，备注唯一点：middleware不会自动刷新~
1. npm install --save-dev express webpack-dev-middleware
2. 新增server.js，内容如下：

```
const express = require('express');
const webpack = require('webpack');
const webpackDevMiddleware = require('webpack-dev-middleware');

const app = express();
const config = require('./webpack.config.js');
const compiler = webpack(config);

// Tell express to use the webpack-dev-middleware and use the webpack.config.js
// configuration file as a base.
app.use(webpackDevMiddleware(compiler, {
  publicPath: config.output.publicPath
}));

// Serve the files on port 3000.
app.listen(3000, function () {
  console.log('Example app listening on port 3000!\n');
});
```
3. webpack.config.js在output中新增：publicPath: '/'
4. package.json新增："server": "node server.js"
5. 执行npm run server


### Hot Module Replacement

### 两种服务器server
- node server.js 启用dev-middleware
- node dev-server.js 启用 dev-server




