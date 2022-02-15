

**使用sass的时候，导入依赖node-sass、sass-loader，存在两者版本不兼容的情况，需要卸载sass-loader后，安装旧版本的sass-loader**

  "node-sass": "^4.14.1"

  "sass-loader": "^7.1.0`"

**node-sass 4.14.1 配套的sass-loader版本为7.1.0**

版本问题: 

- `npm install --save-dev sass-loader`

- `npm install --save-dev node-sass`

卸载高版本sass-loader

- `npm unstall sass-loader ` 

安装指定版本的sass-loader

- ` npm install sass-loader@7.1.0`

