# imooc-music

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).


## Vue-开发移动端音乐WebApp
[](https://c.y.qq.com/musichall/fcgi-bin/fcg_yqqhomepagerecommend.fcg)
[](https://c.y.qq.com/v8/fcg-bin/fcg_v8_singer_track_cp.fcg?g_tk=5381&inCharset=utf-8&outCharset=utf-8&notice=0&format=jsonp&hostUin=0&needNewCode=0&platform=yqq&order=listen&begin=0&num=80&songstatus=1&singermid=0025NhlN2yWrP4&jsonpCallback=__jp1)
[](https://c.y.qq.com/v8/fcg-bin/v8.fcg?g_tk=5381&inCharset=utf-8&outCharset=utf-8&notice=0&format=jsonp&channel=singer&page=list&key=all_all_all&pagesize=100&pagenum=1&hostUin=0&needNewCode=0&platform=yqq&jsonpCallback=__jp0)


## 2-2: 项目安装
```
vue init webpack imooc-music
```
##### 'RunTime-only' 更加轻量
##### vue-router 'Y' vue路由
##### ESLint 'Y' ES6风格代码检查器
##### Standard
##### karma, e2e test 'N' 测试相关
##### npm install 安装依赖
##### 运行项目
```
npm run dev
```


## 2-3: 项目目录介绍
*(build/webpack.base.config)*
##### api: (后端请求, jsonp 请求, AJAX 请求)
##### common: (共用的静态资源: img, common js, style file)
##### components: (组件)
##### base: (共用组件)
##### router: (路由)
##### store: (Vuex相关)
##### main.js (入口)
##### npm install (scss依赖)
```
"sass-loader": "^6.0.7",
"node-sass": "^4.7.2",
```
##### (webpack.base.conf.js) 别名配置, 使用后直接在 main.js 中引入相应的文件。
import 'common/scss/index.scss'
```
context: path.resolve(__dirname, '..', dir),
resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      'src': resolve('src'),
      'api': resolve('src/api'),
      'base': resolve('src/base'),
      'common': resolve('src/common'),
      'components': resolve('src/components'),
      'router': resolve('src/router'),
      'store': resolve('src/store')
    }
  },
```


## 3-1: npm 依赖
*(App.vue)*
*(build/webpack.base.config)*
##### es6 编译辅助操作
```
npm install babel-runtime --save
```
##### 移动端点击300MS延迟。
```
cnpm install fastclick --save
```
##### es6 api 转义
```
cnpm install babel-polyfill --save-dev
```
##### (build/webpack.base.config)
> 别名配置，缩写的应用程序文件路径。


## 3-2: 路由切换基础界面
*(tab.vue)*
*(App.vue)*
*(route.vue)*
##### Navigation switch


## 4-1: 如何使用chrome操作查看qq音乐后台数据
##### chrome use (static/jsonp1.png)
##### data source
```
https://m.y.qq.com/
https://c.y.qq.com/musichall/fcgi-bin/fcg_yqqhomepagerecommend.fcg
```


## 4-2: jsonp讲解
*(common/js/jsonp.js)*
##### Promise:
> 是一个用于传递异步消息的对象。
> 表示将来会知道结果的事件(通常是异步操作)。
> 和这个事件为进一步处理提供了统一的API。
##### jsonp: 
> 解决跨域问题
> 动态地创建一个脚本标记，没有同源限制，它可以是跨域的，
> 和脚本SRC地址指向第三方API url。
> 提供一个回调函数来接收数据，而第三方生成响应作为json数据的包装器。
> 浏览器调用回调函数，并将解析过的json对象作为参数传递。
> 这个站点脚本可以处理回调函数中的传入数据。
##### install jsonp
```
cnpm install jsonp --save
```


## 4-3: jsonp应用, 轮播图数据抓取
*(api/config)*
*(api/recommend.js)*


## 4-4: 轮播图组件, better-scroll
*(recommend.vue)*
*(slider.vue)*
*(common/js/dom.js)*
##### 推荐界面: carousel component
##### better-scroll
```
cnpm install better-scroll@0.1.15 --save
```


## 4-5: 小点控制轮播图播放
*(slider.vue)*
##### 推荐界面: carousel component indicating


## 4-6: 当窗口大小改变时, 当手动拖动轮播图时
*(slider.vue)*
##### 推荐界面: carousel component fix bug
##### Window changes.


## 4-7: 获取qq音乐 热门歌单推荐 数据, 还要绕过接口限制
*(App.vue)*
*(recommend.js)*
*(recommend.vue)*
##### 推荐界面: 热门歌单推荐 
##### Grab the song single data interface.
##### <keep-alive> dom缓存在内存中，防止返回到推荐界面，界面闪烁
##### 500 server error, host problem. 要绕过接口限制


## 4-8: 获取qq音乐 热门歌单推荐 数据, 绕过接口限制
*(build/webpack.dev.conf.js)*
*(config/index.js)*
> 前端请求我们的后端地址，后端请求qq服务器，
> 后端接口代理绕过了qq检查请求数据。
##### ajax 库 axios, 发起HTTPRequest, 修改 headers
```
cnpm install axios --save
```
##### 1.修改config目录下的index.js文件
##### 修改host *(config/index.js)*
```
host: '0.0.0.0',
```
##### 2.修改/build/webpack.dev.conf.js
> 异步定义后端接口
##### 3. api/recommend.js/getDiscList 调用后端接口 *(build/webpack.dev.conf.js)*


## 4-9: 使用热门歌单推荐数据, 渲染界面
*(recommend.vue)*
##### 推荐界面: 热门歌单推荐 
##### chrome 访问 /api/getDiscList 来查看从qq音乐抓取的数据 ?


## 4-10: scroll组件
*(scroll.vue)* [官方文档](https://ustbhuangyi.github.io/better-scroll/doc/zh-hans/#better-scroll%20%E6%98%AF%E4%BB%80%E4%B9%88)
##### scroll组件


## 4-11: 防止轮播图延迟加载, 造成高度计算错误
*(recommend.vue)*
##### 调用better-scroll要保证dom已经渲染,数据变化或者dom变化,better-scroll要调用refresh


## 4-12: 图片懒加载, fastclick优化
*(recommend.vue)*
*(main.js)*
##### 图片懒加载: 仅在滚动时加载
```
cnpm install vue-lazyload --save
```
##### class="needsclick" : fastclick 不拦截单击过程


## 4-13: loading组件
*(loading.vue)*
*(recommend.vue)*
##### 推荐界面: loading


## 5-1: 歌手界面介绍


## 5-2: 抓取qq音乐, 歌手数据
*(api/singer.js)* 
*(singer.vue)*
[歌手数据](https://c.y.qq.com/v8/fcg-bin/v8.fcg?g_tk=5381&inCharset=utf-8&outCharset=utf-8&notice=0&format=jsonp&channel=singer&page=list&key=all_all_all&pagesize=100&pagenum=1&hostUin=0&needNewCode=0&platform=yqq&jsonpCallback=__jp0)


## 5-3: 歌手数据处理
*(singer.vue)* 
*(common/js/singer.js)*


## 5-4: 用歌手数据渲染歌手界面, 歌手界面listview列表
*(listview.vue)歌手列表* 
*(singer.vue)数据处理*


## 5-5: 歌手界面右侧索引滚动组件
*(listview.vue)* 
*(scroll.vue)*
*(common/dom.js)*


## 5-6: 歌手界面右侧索引滚动, 对应歌手列表也要滚动
*(listview.vue)* 
*(scroll.vue)*


## 5-7: 歌手界面右侧索引修改bug
*(listview.vue)* 
*(scroll.vue)*


## 5-8: 歌手界面右侧索引点击最上边和最下边空白部分
*(listview.vue)* 
*(scroll.vue)*


## 5-9: 歌手界面 fixtitle
*(listview.vue)* 


## 5-10: 歌手界面 fixtitle animate, loading
*(listview.vue)* 
*(loading.vue)* 


## 6-1: 歌手详情页: introduce


## 6-2: 点击歌手界面里的歌手, 跳转到歌手详情界面
*(route.js)*
*(listview.vue)*
*(singer.vue)*
*(singer-detail.vue)*


## 6-3: Vuex: 状态管理方式, 管理组件状态
*(static/vuex.png)*
```
cnpm install vuex --save 
```


## 6-4: Vuex配置
##### (store/vuex.js) 项目里使用vuex
##### (store/state.js) 定义基础数据
##### (store/getters.js) 映射state数据, 取数据到组件中
##### (store/mutation-types.js) 操作修改数据的动作名称
##### (store/mutations.js) 修改数据操作
##### (store/action.js) 异步修改, mutation封装
```
  // 调用 mutation，使用 mutation 类型常量。设置 state
        ...mapMutations({
          setSinger: 'SET_SINGER'
        })
  
  // 对应 getters, 获取 state 数据
        ...mapGetters([
          'singer'
        ])
```


## 6-5: 歌手详情页, 抓取歌手详情页数据
*(singer-detail.vue)*
*(api/singer.js)*


## 6-6, 6-7: ? 歌手详情页: 歌曲列表数据处理
*(singer-detail.vue)*
*(common/js/song.js)难度高*
##### 歌手详情页: 歌曲列表数据处理
##### song类封装


## 6-8: 歌手详情页: 使用数据渲染界面
*(music-list.vue)*
##### singer-detail处理歌手详情页数据, music-list渲染歌手详情页


## 6-9: 歌手详情页: 使用数据渲染歌曲列表
*(music-list.vue)*
*(song-list.vue)*


## 6-10, 6-11, 6-12: 歌手详情页, 歌曲列表滚动动画效果
*(song-list.vue)*
*(music-list.vue)*


## 6-13: 歌手详情页: 不同浏览器css的配置
*(common/js/dom.js)*
*(music-list.vue)*


## 6-14: 歌手详情页: 返回按钮, loading加载效果
*(music-list.vue)*


## 7-1: 音乐播放界面 introduce


## 7-2: 音乐播放界面: 播放器 vuex 数据定义
*(store/state.js)*


## 7-3: 音乐播放界面: vuex的具体使用
*(player.vue)*
*(song-list.vue)*
*(music-list.vue)*
*(store/actions.js)*
```
// 传入 vuex 的 actions.js
      ...mapActions([
        'selectPlay',
        'randomPlay'
      ])
```


## 7-4: 音乐播放界面: 全屏按钮, vuex控制
*(player.vue)*


## 7-5: 音乐播放界面: 全屏按钮动画效果, css 实现
*(player.vue)*


## 7-6, 7-7: 音乐播放界面: 大唱片和小唱片缩放的 css3 动画效果
*(player.vue)*
##### transition 的事件监听处理
##### 不同浏览器css的配置
```
cnpm install create-keyframe-animation --save
```


## 7-8: 音乐播放界面: 歌曲控件 播放按钮
*(player.vue)*


## 7-9: 音乐播放界面: 歌曲控件 前进后退, 防止极限点击
*(player.vue)*


## 7-10: 音乐播放界面: 歌曲控件防止极限点击, 组件变灰
*(player.vue)*


## 7-11: 音乐播放界面: 获取歌曲播放时间
*(player.vue)*


## 7-12: 音乐播放界面: 歌曲控件歌曲进度条随歌曲播放而增长
*(progress-bar.vue)*
*(player.vue)*


## 7-13: 音乐播放界面: 歌曲控件歌曲进度条能手动拖动
*(progress-bar.vue)*
*(player.vue)*


## 7-14: 音乐播放界面: 歌曲控件歌曲进度条能点击某个位置播放
*(progress-bar.vue)*
*(player.vue)*


## 7-15: 音乐播放界面: mini播放器环形进度条 SVG
*(progress-circle.vue)*


## 7-16: 音乐播放界面: 歌曲控件播放模式样式改变
*(player.vue)*
*(common/js/mixin.js)*


## 7-17: 音乐播放界面: 各种播放模式情况处理
*(player.vue)*
*(common/js/util.js)*
*(common/js/mixin.js)*


## 7-18: 音乐播放界面: 歌曲控件播放模式改变 fix bug
*(player.vue)*
*(store/actions)*


## 7-19: 抓取歌词数据
*(api/song.js)前端调用,前台定义代理地址给后台*
*(webpack.dev.conf.js)后端绕过qq音乐限制,输出请求内容出去,正则表达式*
*(common/js/song.js)前端调用后端的输出内容*
*(player.vue)组件里面使用输出内容*
##### qq音乐播放歌曲界面 -> chrome network -> js fcg preview
##### 点击fcg就可以在chrome里显示url


## 7-20: 播放器歌词数据解析
*(player.vue)*
*(common/js/song.js)*
##### base64解码和编码
```
cnpm install js-base64 --save
```
##### 视频作者编写, 歌词解析, 每执行到时间点时都执行回调函数
```
cnpm install lyric-parser
```


## 7-21: 音乐播放界面: 歌词滚动
*(player.vue)*


## 7-22, 7-23: 音乐播放界面: 歌词界面和唱片界面之间切换
*(player.vue)*


## 7-24: 音乐播放界面: fix bug
*(player.vue)*


## 7-25: 音乐播放界面: 设置mini播放器的正确位置显示
*(player.vue)*
*(common/js/mixin.js)公共代码*


## 8-1: 热门歌单: Vuex数据通讯
*(route.js)*
*(recommend.vue)* 
*(recommend.js)* 
*(mutations.js)* 
*(getter.js)* 
*(disc.vue)*


## 8-2: 热门歌单: 数据抓取
*(disc.vue)*
*(api/recommend.js)抓取失败*


## 8-3: 热门歌单: 数据应用
*(disc.vue)*


## 9-1: 排行榜界面: 抓取数据
*(rank.vue)*


## 9-2: 排行榜界面: 数据应用
*(rank.vue)*


## 9-3: 排行榜详情界面: Vuex数据通讯
*(top-list.vue)*


## 9-4: 排行榜详情界面: 抓取数据和应用
*(top-list.vue)*
*(api/rank.js)*


## 9-5: 排行榜详情界面: 组件扩展, 前三排行奖杯
*(top-list.vue)*
*(song-list.vue)*


## 10-1: 搜索界面---介绍搜索界面
- ✨


## 10-2: 搜索界面---搜索框组件
*(search.vue)* 
*(search-box.vue)*
- ✨✨
1. 派发query值给外面


## 10-3: 搜索界面---抓取数据, 热门搜索
*(api/search.js)*
*(search-box.vue)*
- ✨✨✨
1. jsonp请求


## 10-4: 搜索界面--搜索功能
*(suggest.vue)* 
*(api/search.js)*
- ✨✨✨
1. ES6
2. jsonp请求


## 10-5: 搜索界面---下拉加载
*(suggest.vue)*
*(scroll.vue)*
*(loading.vue)*
- ✨✨✨

 
## 10-6, 10-7, 10-8, 10-9: 搜索界面---点击搜索界面的歌曲, 插入到播放列表里面
*(store/action.js)*
*(suggest.vue)*
- ✨✨✨✨✨


## 10-10: 搜索界面---优化
*(suggest.vue)* 
*(no-result.vue)*
*(common/js/util)*
- ✨✨✨
1. 当没有搜索结果时返回404
2. 优化请求: 节流函数, 处理搜索框输入字符时, 搜索结果不是输入一个字符出来结果, 输入一定时间后再去请求
3. 滚动时失去焦点, 移动端输入键盘不会挡住界面


## 10-11: 搜索界面---搜索历史数据缓存到localStorage, vuex数据储存
*(search.vue)* 
- ✨✨


## 10-12: 搜索界面---搜索历史数据缓存到localStorage
*(common/js/cache.js)*
*(store/actions.js)*
- ✨✨✨✨✨
1. localStorage封装: 
storage.set(key, val)
storage.get(key, def)
storage.remove(key)
2. sessionStorage封装: 
storage.session.set(key, val)
storage.session.get(key, def)
```
npm install good-storage --save
```


## 10-13: 搜索界面---读取搜索历史数据localStorage
*(common/js/cache.js)*
- ✨✨


## 10-14: 搜索界面---搜索历史列表vuex数据渲染
*(search-list.vue)* 
*(search.vue)* 
- ✨✨


## 10-15: 搜索界面---搜索历史记录储存缓存, 删除缓存
*(common/js/cache.js)*
*(search.vue)* 
- ✨✨✨✨


## 10-16: 搜索界面---确定提示框
*(confirm.js)*
- ✨✨


## 10-17: 搜索界面---搜索歌曲滚动设置
*(search.vue)*
- ✨✨✨


## 10-18: 搜索界面---设置mini播放器的位置显示
*(search.vue)*
- ✨✨


## 11-1: mini歌曲列表---布局和功能介绍
*(playlist.vue)*
- ✨


## 11-2:  mini歌曲列表---显示和隐藏的控制
*(playlist.vue)*
*(player.vue)*
- ✨✨
1. 防止冒泡


## 11-3:  mini歌曲列表---vuex数据渲染
*(playlist.vue)*
- ✨✨✨


## 11-4:  mini歌曲列表---滚动到当前播放歌曲位置
*(playlist.vue)*
- ✨✨✨


## 11-5, 11-6:  mini歌曲列表---删除一首歌曲
*(store/actions.js)*
*(playlist.vue)*
- ✨✨✨✨


## 11-7:  mini歌曲列表---删除一首歌曲的动画
*(playlist.vue)*
*(confirm.vue)*
- ✨✨✨
1. transition-group


## 11-8, 11-9: mini歌曲列表---mixin公共js
*(common/js/mixin.js)*
- ✨✨


## 11-10:  mini歌曲列表---'添加歌曲到列表'的显示和隐藏
*(add-song.vue)*
- ✨✨


## 11-11: 添加歌曲到列表---点击搜索结果歌曲, 保存歌曲到localStorage
*(add-song.vue)*
*(common/js/mixin.js)*
- ✨✨✨


## 11-12: 添加歌曲到列表---切换歌曲列表组件的两个按钮
*(switches.vue)*
- ✨✨


## 11-13, 11-14: 添加歌曲到列表---最近播放列表
*(add-song.vue)*
*(common/js/cache.js)*
- ✨✨✨✨✨


## 11-15: 添加歌曲到列表---搜索历史
*(add-song.vue)*
*(common/js/mixin.js)*
- ✨✨✨


## 11-16: 添加歌曲到列表---顶部提示
*(top-tip.vue)*
- ✨✨


## 11-17: 添加歌曲到列表---fix-bug
*(add-song.vue)*
- ✨✨


## 12-1: 用户中心页---切换 '我喜欢的' '最近听的'
*(user-center.vue)*
*(m-header.vue)*
- ✨✨
1. 点击❤️按钮跳转到用户中心


## 12-2: 用户中心页---vuex数据通讯
*(store/actions.js)* 
*(common/js/cache.js)*
- ✨✨✨✨


## 12-3: 用户中心页---收藏功能处理
*(user-center.vue)*
*(common/js/mixin.js)*
- ✨✨✨


## 12-4: 用户中心页---添加歌曲到列表
*(user-center.vue)*
*(playlist.vue)*
- ✨✨✨


## 12-5: 用户中心页---随机播放
*(user-center.vue)*
- ✨✨✨
1. 回退按钮功能
2. 随机播放按钮功能


## 12-6: 用户中心页---设置高度, 404界面
*(user-center.vue)*
- ✨✨✨
1. 设置高度
2. 404界面


## 13-1: fix-bug
*(player.vue)*
- ✨✨✨✨


## 13-2: 编译打包
- ✨✨✨✨
1. 编译打包, 后端调用
```
npm run build
```
2. *(config/index.js)*
```
build(){port: 9000}
```
3. *(prod.server.js)*
##### 从 dev.conf.js copy
```
node prod.server.js
```
##### chrome -> localhost:9000


## 13-3: 优化
*(router/index.js)*
- ✨✨✨
1. 路由懒加载
*(router/route.js)*


## 13-4
##### (package.json)
##### vue升级, 修改package.json版本号
> "vue"版本号和"vue-template-compiler"要相等


## 14-1
##### (main.js)
##### 移动端调试, 界面多了一个绿色的按钮vConsole
<https://github.com/Tencent/vConsole>
```
cnpm install vconsole
```
##### 抓包工具charies(Mac) , Fiddler(Win)
##### 默认有个8888端口
##### 电脑IP
```
ifconfig
```
##### iphone代理, 无线局域网, 配置代理, 代理IP手动, 电脑IP, 8888端口。 实现代理到charies
##### android 局域网, 修改网络, 配置http代理, 服务器电脑IP, 8888端口。 实现代理到charies
