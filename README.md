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

HtmlWebpackPlugin
打包所有文件到dist，包括index.html，不用事先写好index.html

CleanWebpackPlugin
创建所有文件之前清空dist目录
npm install --save-dev clean-webpack-plugin


