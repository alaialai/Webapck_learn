<!--
 * @Author: xiangly
 * @Date: 2020-04-19 14:40:53
 * @LastEditTime: 2020-04-19 14:49:41
 * @LastEditors: Please set LastEditors
 * @Description: webpack外置文件写入
 * @FilePath: \Webapck_learn\generate-asset-webpack-plugin.md
 -->

## generate-asset-webpack-plugin 外置文件

因为工作需要，项目需要有配置文件，且配置文件需与 static 文件夹（打包后的文件）同级。

### 详细步骤

1. 下载插件

```js
npm install --save-dev generate-asset-webpack-plugin
```

2. webpack.prod.confug.js

```js
const GeneraterAssetPlugin = require("generate-asset-webpack-plugin");

//引入配置文件
const serverConfig = require("../serverConfig.json"); //这个json文件可以随意起名除了config.json

//将json中的配置项返回
const createJson = function (compilation) {
  return JSON.stringify(serverConfig);
};

//webpackConfig -> plugin中写入
new GeneraterAssetPlugin({
  filename: "serverConfig.json", //输出到dist根目录下的serverConfig.json文件,名字可以按需改
  fn: (compilation, cb) => {
    cb(null, createJson(compilation));
  },
});
```
