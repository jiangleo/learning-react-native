### React Native ESLint & Airbnb 配置

```diff
- 欢迎您帮忙纠错, 一起帮助更多的人。 一起来学习交流React, QQ群：413381701
```

我在配置的时候也遇坑无数，差不多搞了半天才配置完毕，现记录下来，供以后参考。

#### 0.遇坑环境
```js
{ npm: '2.15.9',
  ares: '1.10.1-DEV',
  http_parser: '2.7.0',
  icu: '56.1',
  modules: '46',
  node: '4.6.0',
  openssl: '1.0.2j',
  uv: '1.9.1',
  v8: '4.5.103.37',
  zlib: '1.2.8' }
```
按着网上的教程，一步一步来。补充一句：-d 是 detail 的意思，可以看安装的细节。

Step 0-1 `npm install -g eslint`

Step 0-2 `npm install --save-dev -d eslint-plugin-react`

Step 0-3 `npm install --save-dev -d eslint-plugin-react-native`

Step 0-4 `npm install --save-dev -d eslint-config-airbnb`

错误来了，airbnb 死活安装不上，报如下错误

![airbnb can not install](http://ww4.sinaimg.cn/mw690/77c29b23jw1f94nlzi8dtj20i90attbn.jpg)

满世界找资料，https://www.google.com/search?q=The+package+eslint-plugin-import%402.0.1+does+not+satisfy+its+siblings%27+peerDependencies+requirements!&oq=The+package+eslint-plugin-import%402.0.1+does+not+satisfy+its+siblings%27+peerDependencies+requirements!&aqs=chrome..69i57.1296j0j7&sourceid=chrome&ie=UTF-8

唯一一个看起来比较靠谱的，https://github.com/airbnb/javascript/issues/956#issuecomment-233696181

`npm install --save-dev eslint-config-airbnb eslint-plugin-import@^1.8.0 eslint-plugin-react@^5.1.1 eslint-plugin-jsx-a11y@^1.2.2 eslint@^2.10.2`

最后结论：网上的解决方案没有一个是可用的（_后来才发现其实是我的姿势不对，请接着看_）。

后来问群里好友，告诉我用 cnpm 试试，结果神奇的一幕出现了。

![airbnb installed successful with cnpm](http://ww4.sinaimg.cn/mw1024/77c29b23jw1f94o1ri873j20i805ndhp.jpg)

Step 0-5 在 React Native 项目中，找到 package.json，添加下面这行
```diff
"scripts": {
  "start": "node node_modules/react-native/local-cli/cli.js start",
+  "lint":"eslint --ext .js ./src"
}
```

Step 0-6 在命令行下执行，`npm run lint`, 

Step 0-7 如果项目大的话，会有上千条 errors，慢慢改代码吧！ ：D


