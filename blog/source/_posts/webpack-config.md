---
title: webpack-config
date: 2022-4-23 18:57:55
tags:
---
# webpack + react + ts + scss hello
 1.进入对应的文件夹，初始化项目 npm init -y 安装webpack webpack-cli

2.创建src文件夹,添加index.js

3.安装babel-loader,建立webpack.config.js文件并配置入口,出口,等例如
```
import path from "path";
 const config = {
        entry:  "./src/index.js",
        output: {
          path: path.resolve(__dirname, "dist"),
          filename: "main.js",
         },
        mode: "production",
         module: {
    rules: [
      {
        test: /\.js$/,
        use: {
          loader: "babel-loader"
        },
      },
    ],
  },
```
4.在package.json 配置webpack打包命令
```
“scripts”: {
“test”: “echo "Error: no test specified" && exit 1”,
“build”: “webpack”
},
```
5.安装webpack-dev-server,配置启动命令,运行npm run dev查看页面
```
“scripts”: {
“test”: “echo "Error: no test specified" && exit 1”,
“build”: “webpack”,
“dev”: “webpack server –open”
},
```

6.配置渲染的html模板,在src下建一个index.html,安装html-webpack-plugin，并在webpack.config.js进行配置
```
-webpack.config.js- import WebpackHtmlPlugin from "html-webpack-plugin" plugins: [new WebpackHtmlPlugin({ template: "./src/index.html" })],`

```
7.安装react react-dom,向项目中集成react(react 18.0版本的写法),安装@babel/preset-env, @babel/preset-react,将index.js文件改为在index.jsx,入口也要记得改为jsx,在index.jsx中写入如下代码,在webpack.config.js中添加jsx的配置,打包后运行会在页面上展示hello world
```
-index.jsx- let root = document.getElementById("root"); ReactDOM.createRoot(root).render(
hello world
); -webpack.config.js- entry: "./src/index.jsx", -module use添加- { test: /\.jsx?$/, use: [ { loader: "babel-loader", options: { presets: ["@babel/preset-env", "@babel/preset-react"], }, }, ], },
```
8.集成ts,需要安装typescript ,ts-loader,将jsx改为tsx,入口要要改为tsx,webpack.config.js添加配置
```
entry: "./src/index.tsx", { test: /\.tsx?$/, use: ["ts-loader"], }, resolve: { extensions: [".ts", ".tsx", ".js", ".jsx"], },
```
9.集成scss,除了要安装css-loader style-loader还需要安装sass-loader sass,在webpack.config.js添加配置

```
{ test: /\.scss$/i, exclude: /\.module\.scss$/i, use: [ { loader: "style-loader", }, { loader: "css-loader", }, { loader: "sass-loader", }, ], }
```
配置好之后,在引入scss文件的时候可能会出现找不到模块,此时要添加对应的文件index.d.ts,typings.d.ts
```
-index.d.ts- declare module '*.scss' { const content: { [key: string]: any } export = content } -typings.d.ts- declare module '*.scss';
```
在配置的过程中遇到,className配置未生效,需要配置css-loader的扩展 ,此外配置的顺序也不能乱，依次是style-loader css-loader sass-loader
```
{ loader: "css-loader", options: { modules: true, esModule: true } }

```
10.将webpack.config.js改为webpack.config.ts(参考 https://webpack.docschina.org/configuration/configuration-languages/#typescript)
 10-1.安装 npm install --save-dev typescript ts-node @types/node @types/webpack  
 10-2. 给config添加类型
```
const config: webpack.Configuration = { mode: 'production', entry: './foo.js', output: { path: path.resolve(__dirname, 'dist'), filename: 'foo.bundle.js', }, };
export default config;
```