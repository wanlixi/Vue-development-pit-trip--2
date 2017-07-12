# Vue-development-pit-trip--2
Webpack package Vue project out of the static font resource path error problems



### 出现的场景：
vue-cli构建的项目（vue2.x+webpack2.x），引入第三方的字体图标库，开发环境下一丝问题都没有，iconfont完美显示，
而在生产环境下，你在页面上只能看到千篇一律的“口”，what？美美的矢量图标全变成“口”了，打开控制台才发现：
```
GET file:///C:/static/fonts/ionicons.24712f6.ttf net::ERR_FILE_NOT_FOUND
/C:/static/fonts/ionicons.05acfdb.woff
```
打包出来的静态资源引入字体文件发生路径错误

### 解决办法
通常在webpack.base.conf.js里面找到关于font的配置
for example:
```
{
  test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
  loader: 'url-loader',
  options: {
    limit: 10000,
    name: utils.assetsPath('fonts/[name].[hash:7].[ext]')
  }
}
```
在options里面配置一个
* publicPath：'/' *
就可以解决
