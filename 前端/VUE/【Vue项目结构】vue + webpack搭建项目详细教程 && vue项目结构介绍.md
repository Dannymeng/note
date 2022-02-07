## vue + webpack搭建项目详细教程 && vue项目结构介绍



## 安装vue-cli脚手架

`npm install vue-cli -g`

安装成功验证方法：

`vue -V` 查看vue版本号



## 创建vue-cli项目

`vue init webpack projectname(项目名)`

注意： 项目名不能大写，不能使用中文

后面的会出现几个提示，正常回车即可。



## 启动项目

`npm run dev`

浏览器访问： http://localhost:8080



## 项目总体框架

 一个vue-cli的项目结构如下，其中src文件夹是需要掌握的，所以本文也重点讲解其中的文件，至于其他相关文件，了解一下即可。 

![Vue+Webpack项目框架](https://github.com/Dannymeng/note/blob/master/%E5%89%8D%E7%AB%AF/VUE/%E3%80%90Vue%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84%E3%80%91vue%20%2B%20webpack%E6%90%AD%E5%BB%BA%E9%A1%B9%E7%9B%AE%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B%20%26%26%20vue%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84%E4%BB%8B%E7%BB%8D/Vue%2BWebpack%E9%A1%B9%E7%9B%AE%E6%A1%86%E6%9E%B6.png)



 文件结构细分 

### 1、build文件夹 - webpack配置

build文件夹主要为webpack的配置，当启动程序时，会检查npm版本，加载配置文件，启动项目

![build文件夹](https://github.com/Dannymeng/note/blob/master/%E5%89%8D%E7%AB%AF/VUE/%E3%80%90Vue%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84%E3%80%91vue%20%2B%20webpack%E6%90%AD%E5%BB%BA%E9%A1%B9%E7%9B%AE%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B%20%26%26%20vue%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84%E4%BB%8B%E7%BB%8D/build%E6%96%87%E4%BB%B6%E5%A4%B9.png)



### 2、config - vue项目配置

 config文件主要是项目相关配置，我们常用的就是当端口冲突时配置监听端口，打包输出路径及命名等 

![config文件夹](https://github.com/Dannymeng/note/blob/master/%E5%89%8D%E7%AB%AF/VUE/%E3%80%90Vue%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84%E3%80%91vue%20%2B%20webpack%E6%90%AD%E5%BB%BA%E9%A1%B9%E7%9B%AE%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B%20%26%26%20vue%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84%E4%BB%8B%E7%BB%8D/config%E6%96%87%E4%BB%B6%E5%A4%B9.png)



[参考资料](https://blog.csdn.net/weixin_45627031/article/details/107846016)

