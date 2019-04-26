---
title: npm browser gulp使用
categories: ['前端']
tags: ['工具']
---
# 流行框架第2天




### sourceTree , tortoiseGit


### npm
  - 官网[https://www.npmjs.com]
  - node package manager
  - 命令:
    + 初始化:`npm init`
    + 安装指定包:`npm install jquery --save`
    + 安装指定包:`npm install jquery@版本号 --save`
    + 删除指定包:`npm remove jquery --save`
    + 下载安装package.json中dependencies属性对的文件:`npm install --production`

### browser-sync
  - 更改代码之后自动刷新浏览器
  - 需要使用npm进行全局安装:`npm install browser-sync -g`,-g表示安装到全局
  - 使用:`browser-sync start --server --files "./index.html,app.css,./css/*.css,*.*" ``z注意这里父文件和子文件都不要用中文  后面指定文件用双引号`
  - --files参数指定要监视的文件，后面跟要监视的文件的文件路径以逗号分隔。

## gulp
  [官网](http://www.gulpjs.com)
  [中文网](http://www.gulpjs.com.cn)

- 前端自动化构建工具
  js压缩,var x,xname，混淆
  合并.
  css压缩
  html压压缩

- grunt ,webpack...


### 核心就5个方法
  - task,gulp中是一个个任务的形式来实现功能。
    + task('任务名',function(){
      .....
    });
  - src
    + src('./*.js')
  - dest('./minjs/')// 指定处理后的文件的输出路径.
  - watch('./*.js',['任务名1','任务名2']);
  - run('任务名');//执行指定的任务.

### gulp的安装
  - 使用npm 进行安装
  - `npm install gulp-cli -g`;

### gulp 使用

#### 使用时还需要在项目中通过npm非全局安装gulp
  - `npm install gulp --save-dev`


#### 还需要在当前项目根目录添加一个gulpfile.js文件来写具体的任务代码.

### gulp的一些插件
  - 也是使用npm安装
  - 对js代码进行压缩 gulp-uglify
  - 对代码进行合并 gulp-concat
  - 对css进行压缩 gulp-cssnano
  - 对html进行压缩 gulp-htmlmin