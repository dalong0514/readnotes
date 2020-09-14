## 记忆时间

## 0301. 带你用vue撸后台——基础篇.md

### 1.1 前言

第一篇文章主要来说一说在开始写实际业务代码之前的一些准备工作吧，但这里不会教你 webpack 的基础配置，热更新原理是什么，webpack 速度优化等等，有需求的请自行 google，相关文章已经很多了。

### 1.2 目录结构

```
├── build                      // 构建相关  
├── config                     // 配置相关
├── src                        // 源代码
│   ├── api                    // 所有请求
│   ├── assets                 // 主题 字体等静态资源
│   ├── components             // 全局公用组件
│   ├── directive              // 全局指令
│   ├── filtres                // 全局 filter
│   ├── icons                  // 项目所有 svg icons
│   ├── lang                   // 国际化 language
│   ├── mock                   // 项目mock 模拟数据
│   ├── router                 // 路由
│   ├── store                  // 全局 store管理
│   ├── styles                 // 全局样式
│   ├── utils                  // 全局公用方法
│   ├── vendor                 // 公用vendor
│   ├── views                   // view
│   ├── App.vue                // 入口页面
│   ├── main.js                // 入口 加载组件 初始化等
│   └── permission.js          // 权限管理
├── static                     // 第三方不打包资源
│   └── Tinymce                // 富文本
├── .babelrc                   // babel-loader 配置
├── eslintrc.js                // eslint 配置项
├── .gitignore                 // git 忽略项
├── favicon.ico                // favicon图标
├── index.html                 // html模板
└── package.json               // package.json
```

这里来简单讲一下 src 文件。

#### 1.2.1 api 和 views

简单截取一下公司后台项目，现在后台大概有四五十个 api 模块。如图可见模块有很多，而且随着业务的迭代，模块还会会越来越多。 所以这里建议根据业务模块来划分 views，并且将 views 和 api 两个模块一一对应，从而方便维护。如下图：

如 article 模块下放的都是文章相关的 api，这样不管项目怎么累加，api 和 views 的维护还是清晰的，当然也有一些全区公用的 api 模块，如七牛 upload，remoteSearch 等等，这些单独放置就行。

1『比如数据流里，提条件的视图是 views 文件夹下的「requires」文件夹，那么建一个「requires.js」api 与之对应。』

#### 1.2.2 components

这里的 components 放置的都是全局公用的一些组件，如上传组件，富文本等等。一些页面级的组件建议还是放在各自 views 文件下，方便管理。如图：

#### 1.2.3 store

这里我个人建议不要为了用 vuex 而用 vuex。就拿我司的后台项目来说，它虽然比较庞大，几十个业务模块，几十种权限，但业务之间的耦合度是很低的，文章模块和评论模块几乎是两个独立的东西，所以根本没有必要使用 vuex 来存储 data，每个页面里存放自己的 data 就行。当然有些数据还是需要用 vuex 来统一管理的，如登录 token，用户信息，或者是一些全局个人偏好设置等，还是用 vuex 管理更加的方便，具体当然还是要结合自己的业务场景的。总之还是那句话，不要为了用 vuex 而用 vuex！

1『两个页面共用数据，这种数据交互耦合度高的才使用 vuex。』

### 1.3 webpack

这里是用 vue-cli 的 webpack-template 为基础模板构建的，如果你对这个有什么疑惑请自行 google，相关的配置绍其它的文章已经介详细了，这里就不再展开了。简单说一些需要注意到地方。

#### 1.3.1 jquery（本项目已移除）

管理后台不同于前台项目，会经常用到一些第三方插件，但有些插件是不得不依赖 jquery 的，如市面很多富文本基都是依赖 jquery 的，所以干脆就直接引入到项目中省事（gzip 之后只有 34kb，而且常年 from cache，不要考虑那些吹毛求疵的大小问题，这几 kb 和提高的开发效率根本不能比）。但是如果第三方库的代码中出现 .xxx 或 jQuery.xxx 或 window.jQuery 或 window，则会直接报错。要达到类似的效果，则需要使用 webpack 内置的 ProvidePlugin 插件，配置很简单，只需要：

```js
new webpack.ProvidePlugin({
  $: 'jquery' ,
  'jQuery': 'jquery'
})
```

这样当 webpack 碰到 require 的第三方库中出现全局的\$、jQeury 和 window.jQuery 时，就会使用 node\_module 下 jquery 包 export 出来的东西了。

#### 1.3.2 alias

当项目逐渐变大之后，文件与文件直接的引用关系会很复杂，这时候就需要使用 alias 了。 有的人喜欢 alias 指向 src 目录下，再使用相对路径找文件。

```js
resolve: {
  alias: {
    '~': resolve(__dirname, 'src')
  }
}

//使用
import stickTop from '~/components/stickTop'
```

或者也可以：

```js
alias: {
  'src': path.resolve(__dirname, '../src'),
  'components': path.resolve(__dirname, '../src/components'),
  'api': path.resolve(__dirname, '../src/api'),
  'utils': path.resolve(__dirname, '../src/utils'),
  'store': path.resolve(__dirname, '../src/store'),
  'router': path.resolve(__dirname, '../src/router')
}

//使用
import stickTop from 'components/stickTop'
import getArticle from 'api/article'
```

没有好与坏对与错，纯看个人喜好和团队规范。

#### 1.3.3 ESLint

不管是多人合作还是个人项目，代码规范是很重要的。这样做不仅可以很大程度地避免基本语法错误，也保证了代码的可读性。这所谓工欲善其事，必先利其器，个人推荐 eslint+vscode 来写 vue，绝对有种飞一般的感觉。效果如图：

每次保存，vscode 就能标红不符合 eslint 规则的地方，同时还会做一些简单的自我修正。安装步骤如下：

1、首先安装 eslint 插件。安装并配置完成 ESLint 后，我们继续回到 VSCode 进行扩展设置，依次点击 文件 > 首选项 > 设置，打开 VSCode 配置文件，添加如下配置：

```json
"files.autoSave":"off",
"eslint.validate": [
   "javascript",
   "javascriptreact",
   "html",
   { "language": "vue", "autoFix": true }
 ],
 "eslint.options": {
    "plugins": ["html"]
 }
```

这样每次保存的时候就可以根据根目录下 .eslintrc.js 你配置的 eslint 规则来检查和做一些简单的 fix。这里提供了一份我平时的 eslint 规则地址「[vue-element-admin/.eslintrc.js at master · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/blob/master/.eslintrc.js)」，都简单写上了注释。每个人和团队都有自己的代码规范，统一就好了，去打造一份属于自己的 eslint  规则上传到 npm 吧，如饿了么团队的 config「[eslint-config-elemefe - npm](https://www.npmjs.com/package/eslint-config-elemefe)」，vue 的 config「[vuejs/eslint-config-vue](https://github.com/vuejs/eslint-config-vue)」。

[VSCode 拓展推荐（前端开发）](https://github.com/varHarrie/varharrie.github.io/issues/10)。

### 1.4 封装 axios

我们经常遇到一些线上的 bug，但测试环境很难模拟。其实可以通过简单的配置就可以在本地调试线上环境。 这里结合业务封装了 axios ，线上代码「[vue-element-admin/request.js at master · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/blob/master/src/utils/request.js)」。

```js
import axios from 'axios'
import { Message } from 'element-ui'
import store from '@/store'
import { getToken } from '@/utils/auth'

// 创建axios实例
const service = axios.create({
  baseURL: process.env.BASE_API, // api的base_url
  timeout: 5000 // 请求超时时间
})

// request拦截器
service.interceptors.request.use(config => {
  // Do something before request is sent
  if (store.getters.token) {
    config.headers['X-Token'] = getToken() // 让每个请求携带token--['X-Token']为自定义key 请根据实际情况自行修改
  }
  return config
}, error => {
  // Do something with request error
  console.log(error) // for debug
  Promise.reject(error)
})

// respone拦截器
service.interceptors.response.use(
  response => response,
  /**
  * 下面的注释为通过response自定义code来标示请求状态，当code返回如下情况为权限有问题，登出并返回到登录页
  * 如通过xmlhttprequest 状态码标识 逻辑可写在下面error中
  */
  //  const res = response.data;
  //     if (res.code !== 20000) {
  //       Message({
  //         message: res.message,
  //         type: 'error',
  //         duration: 5 * 1000
  //       });
  //       // 50008:非法的token; 50012:其他客户端登录了;  50014:Token 过期了;
  //       if (res.code === 50008 || res.code === 50012 || res.code === 50014) {
  //         MessageBox.confirm('你已被登出，可以取消继续留在该页面，或者重新登录', '确定登出', {
  //           confirmButtonText: '重新登录',
  //           cancelButtonText: '取消',
  //           type: 'warning'
  //         }).then(() => {
  //           store.dispatch('FedLogOut').then(() => {
  //             location.reload();// 为了重新实例化vue-router对象 避免bug
  //           });
  //         })
  //       }
  //       return Promise.reject('error');
  //     } else {
  //       return response.data;
  //     }
  error => {
    console.log('err' + error)// for debug
    Message({
      message: error.message,
      type: 'error',
      duration: 5 * 1000
    })
    return Promise.reject(error)
  })

export default service
```

```js
import request from '@/utils/request'

//使用
export function getInfo(params) {
  return request({
    url: '/user/info',
    method: 'get',
    params
  });
}
```

1『

后台编译「npm run dev」是跑开发环境，「npm run pro」是跑生产环境，其配置文件一个对应于「.env.development」，一个对应于「.env.production」，需要在这个配置文件里设置整个前端的基础 url。试了下设置成本地 url，但发现后端 laravel 默认跑在 8000 接口上，而前端默认跑在 9527 接口上，不一致的话登录不了。接着尝试把 laravel 的启动端口更改，用命令「php artisan serve --host=127.0.0.1 --port=9527」。但发现前端的端口又自动更改为 9528。

配置文件里设置为「VUE_APP_BASE_API = '/dev-api'」，登录界面请求的 URL 是「Request URL: http://localhost:9527/dev-api/vue-element-admin/user/login」，说明请求头「http://localhost:9527」是自动加的。目前测试的折中办法是在请求数据的 api 方法里要求 url 填全称。（2020-05-20）

』

比如后台项目，每一个请求都是要带 token 来验证权限的，这样封装一下的话我们就不用每个请求都手动来塞 token，或者来做一些统一的异常处理，一劳永逸。 而且因为我们的 api 是根据 env 环境变量动态切换的，如果以后线上出现了 bug，我们只需配置一下 @/config/dev.env.js 再重启一下服务，就能在本地模拟线上的环境了。

```js
module.exports = {
    NODE_ENV: '"development"',
    BASE_API: '"https://api-dev"', //修改为'"https://api-prod"'就行了
    APP_ORIGIN: '"https://wallstreetcn.com"' //为公司打个广告 pc站为vue+ssr
}
```

妈妈再也不用担心我调试线上 bug 了。 当然这里只是简单举了个例子，axios 还可以执行多个并发请求，拦截器什么的，大家自行去研究吧。

### 1.5 多环境

vue-cli 默认只提供了 dev 和 prod 两种环境。但其实正真的开发流程可能还会多一个 sit 或者 stage 环境，就是所谓的测试环境和预发布环境。所以我们就要简单的修改一下代码。其实很简单就是设置不同的环境变量。

```json
"build:prod": "NODE_ENV=production node build/build.js",
"build:sit": "NODE_ENV=sit node build/build.js",
```

之后在代码里自行判断，想干就干啥。

```js
var env = process.env.NODE_ENV === 'production' ? config.build.prodEnv : config.build.sitEnv
```

新版的 vue-cli 也内置了 webpack-bundle-analyzer 一个模块分析的东西，相当的好用。使用方法也很简单，和之前一样封装一个 npm script 就可以。

```json
//package.json
 "build:sit-preview": "cross-env NODE_ENV=production env_config=sit npm_config_preview=true  npm_config_report=true node build/build.js"

//之后通过process.env.npm_config_report来判断是否来启用webpack-bundle-analyzer

var BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin
webpackConfig.plugins.push(new BundleAnalyzerPlugin())
```

webpack-bundle-analyzer 这个插件还是很有用的，对后期的代码优化什么的，最重要的是它够装逼。

### 1.6 前后端交互

每个公司都有自己一套的开发流程，没有绝对的好与坏。这里我来讲讲我司的前后端交互流程。

#### 1.6.1 跨域问题

首先前后端交互不可避免的就会遇到跨域问题，我司现在全是用 cors 来解决的，如果你司后端嫌麻烦不肯配置的话，dev 环境也可以通过 webpack-dev-server 的 proxy 来解决，开发环境用 nginx 反代理一下就好了，具体配置这里就不展开了。

#### 1.6.2 前后端的交互问题

其实大家也知道，平时的开发中交流成本占据了我们很大一部分时间，但前后端如果有一个好的协作方式的话能解决很多时间。我司开发流程都是前后端和产品一起开会讨论项目，之后后端根据需求，首先定义数据格式和 api，然后 mock api 生成好文档，我们前端才是对接接口的。这里推荐一个文档生成器 swagger「[API Documentation & Design Tools for Teams | Swagger | Swagger](https://swagger.io/)」。 swagger 是一个 REST APIs 文档生成工具，可以在许多不同的平台上从代码注释中自动生成，开源，支持大部分语言，社区好，总之就是一个强大，如下图的 api 文档（swagger 自动生成，ui 忽略）。

api 地址，需要传是没参数，需要的传参类型，返回的数据格式什么都一清二楚了。

1『目前自己用的是 postman，也很棒。laravel 里也有模拟的工具，好像是 seed、factory 之类的，遇到需要的场景时研究一下。』

#### 1.6.3 前端自行 mock

如果后端不肯来帮你 mock 数据的话，前端自己来 mock 也是很简单的。你可以使用 mock server 或者使用 mockjs + rap 也是很方便的。 不久前出的 easy-mock 也相当的不错，还能结合 swagger。 我们大前端终于不用再看后端的脸色了。

#### 1.6.4 iconfont

element-ui 默认的 icon 不是很多，这里要安利一波阿里的 iconfont 简直是神器，不管是公司项目还是个人项目都在使用。它提供了 png、ai、svg 三种格式，同时使用也支持 unicode，font-class，symbol 三种方式。由于是管理后台对兼容性要求不高，楼主平时都喜欢用 symbol，晒一波我司后台的图标（都是楼主自己发挥的）。

详细具体的使用可以见文章「[手摸手，带你优雅的使用 icon - 掘金](https://juejin.im/post/59bb864b5188257e7a427c09)」。

### 1.7 router-view

different router the same component vue。真实的业务场景中，这种情况很多。比如：

```json
{ path: 'create', component: PostCreate, name: '发表文章' },
{ path: 'edit/:id(\\d+)', componet: PostCreate, name: '编辑文章' }
```

我创建和编辑的页面使用的是同一个 component，默认情况下当这两个页面切换时并不会触发 vue 的 created 或者 mounted 钩子，官方说你可以通过 watch \$route 的变化来做处理，但其实说真的还是蛮麻烦的。后来发现其实可以简单的在 router-view上加上一个唯一的 key，来保证路由切换时都会重新渲染触发钩子了。这样简单的多了。

```js
<router-view :key="key"></router-view>

computed: {
    key() {
        return this.$route.name !== undefined? this.$route.name + +new Date(): this.$route + +new Date()
    }
 }
 ```
 
### 1.8 优化

有些人会觉得现在构建是不是有点慢，我司现在技术栈是容器服务，后台项目会把 dist 文件夹里的东西都会打包成一个 docker 镜像，基本步骤为：

```
npm install
npm run build:prod
加打包镜像，一共是耗时如下
```

还是属于能接受时间的范围。 主站 PC 站基于 nodejs、Vue 实现服务端渲染，所以不仅需要依赖 nodejs，而且需要利用 pm2 进行 nodejs 生命周期的管理。为了加速线上镜像构建的速度，我们利用 taobao 源 registry.npm.taobao.org 进行加速, 并且将一些常见的 npm 依赖打入了基础镜像，避免每次都需要重新下载。 这里注意下建议不要使用 cnpm install 或者 update，它的包都是一个link，反正会有各种诡异的 bug，这里建议这样使用：

```
npm install --registry=https://registry.npm.taobao.org
```

如果你觉得慢还是有可优化的空间如使用 webpack dll 或者把那些第三方 vendor 单独打包 external 出去，或者我司现在用的是 http2 可以使用 AggressiveSplittingPlugin 等等，这里有需求的可以自行优化。

## 0303. 手摸手，带你用 vue 撸后台 —— 实战篇

[手摸手，带你用vue撸后台 系列三(实战篇) - 掘金](https://juejin.im/post/593121aa0ce4630057f70d35)

在前面两篇文章中已经把基础工作环境构建完成，也已经把后台核心的登录和权限问题完成了，现在手摸手，一起进入实操。

### 3.1 Element

去年十月份开始用 vue 做管理后台的时候毫不犹豫的就选择了 element-ui，那时候 vue2.0 刚发布也没多久，市面上也没有很多其它的 vue2.0 的 ui 框架可供选择。虽然 element-ui 也有很多的不足，前期的 bug 也不少，但我还是选择了它，简单说一下我选择 element-ui 的原因吧：

1、有大厂背书：虽然核心开发只有两三个人，但至少不用担心哪天就不维护，带着小姨子跑路了。

2、持续迭代 : element-ui 发版至今 release 了四十多个版本，之前平均都是一周一个小版本更新（是不是不小心暴露了它 bug 多的问题）。ps: 至 2017.12.4 已经迭代了 74 个版本，还保持着较高更新频率。

3、生态圈优异，社区活跃 ：其 contributors 已经有 250 多人（前期我有饶有兴致的贡献过几个 pr，参与过七八十个 issue），社区里也有很多基于 element-ui 的拓展组件，也有很多相关的 qq 讨论群或者 gitter。

4、社区的认可：目前 Element 已经是 vue 相关最多 star 的开源项目了，体现出了社区对其的认可。

说了这么多优点，作为一个资深 element-ui 用户还是有些要抱怨的，和 react 老大哥 Ant Design 相比还是有一定的差距的，不管是组件的丰富性，参数的可配性还是文档的完整性，亦或是 UI 的交互和美观度。不过 ant 也是经过了近 9k 次 commit 的不断打磨，才有了今天。我也相信 element-ui 也会越来越好的。

这里还有一些其它的框架（只讨论 pc 端的框架）大家可以自行选择：

1、ivew 一国人个人写的框架，美观度和交互性都不错，有种介于 Element 和 Ant 之间的感觉，之前和 element 团队小小的撕了一下，有兴趣的自己去围观吧，框架还是很不做的，一个人能做出这样，也是很不容易的。作者公开信件「[致 Element UI 团队的公开信 - 知乎](https://zhuanlan.zhihu.com/p/25893972)」。

2、vue-admin 也是一个不错的选择，代码写的和不错，官方也出了一个 admin 的架子，也很值得借鉴。

3、vue-material 一个 material design vue 框架库。

4、vuetify 又是一个 material design vue 框架库。

5、Keen-UI 又又是一个 material design vue 框架库。

6、CoreUI-Free-Bootstrap-Admin-Template 和以前的 Bootstrap 一样，搭好了一个完整的架子，大家可以进行二次拓展，它有 vue、react、angular 多个版本。

7、Framework7-Vue 个人感觉这是本人体验到现在移动端体验最好的框架。不过 Framework7-Vue 感觉还不是很完善，还需要观望一段时间。而且它有自己的路由规则，所以不能使用 vue-router，这点还是很不方便的。

简单列举了一些主流的框架，不得不感慨现在 vue 的生态圈真是太繁荣了，上述框架楼主并没有深入使用过，不好发表太多建议，大家自行甄别适合自己业务的框架吧。这里开始我们会开始介绍一些结合 Element 的开发经验。

### 3.2 基于 Element 的动态换肤

有些产品就是这么残忍，能完成需求就不错了，还要让我们做动态换肤。Element 官网上也提供了自定义主题的方案「[组件 | Element](https://element.eleme.io/#/zh-CN/component/custom-theme)」，同时也提供了一个在线自定义主题的 demo「[Element Theme Preview](https://elementui.github.io/theme-preview/#/zh-CN)」。

是不是很酷，作者也说明了实现的方案地址「[换肤问题有没有解决方案 · Issue #3054 · ElemeFE/element](https://github.com/ElemeFE/element/issues/3054)」，大概思路：1）先把默认主题文件中涉及到颜色的 CSS 值替换成关键词。2）根据用户选择的主题色生成一系列对应的颜色值。3）把关键词再换回刚刚生成的相应的颜色值。4）直接在页面上加 style 标签，把生成的样式填进去。

我看完觉得真的还是有点复杂的。有没有简单的方案呢？ 让我们思考一下，让我们自己写动态换肤该怎么写呢？最常见的方法就是写两套主题，一套叫 day theme ，一套叫 night theme，night theme 主题都在一个 .night-theme 的命名空间下，我们动态的在 body 上 add .night-theme ，remove .night-theme。这就是最简单的动态换肤。所以我们也能不能顺着这个思路，基于 element-ui 实现动态换肤呢？

首先我们下载官方通过的 Theme generator「[ElementUI/element-theme: Theme generator cli tool for Element.](https://github.com/ElementUI/element-theme)」，一个专门用来生成 Element 主题的工具。按照文档，我们生成了需要的主题。

之后就是我们要做的事情了，将这个主题的每个元素外面包裹一个 class 来做命名空间。我们这里用到了 gulp-css-wrap 这个神器，轻轻松松就完成了我们想要的结果。

```js
var path = require('path')
var gulp = require('gulp')
var cleanCSS = require('gulp-clean-css');
var cssWrap = require('gulp-css-wrap');

var customThemeName='.custom-theme'

gulp.task('css-wrap', function() {
  return gulp.src( path.resolve('./theme/index.css'))
    .pipe(cssWrap({selector:customThemeName}))
    .pipe(cleanCSS())
    .pipe(gulp.dest('dist'));
});

gulp.task('move-font', function() {
  return gulp.src(['./theme/fonts/**']).pipe(gulp.dest('dist/fonts'));
});

gulp.task('default',['css-wrap','move-font']);
```

这样就得到了一个以.custom-theme 为命名空间的自定义主题了，之后我们在项目中引入主题

```js
//main.js
import 'assets/custom-theme/index.css'
```

我们在换肤的地方 toggleClass (document.body, 'custom-theme') 一直 toggle body 的 class 就可以了。我们就简单实现了动态换肤效果。

不过这种模式实现换肤也是有一个弊端的，它等于把这两个主题都打包在了项目里，如果你的项目主题需要七八种，这种模式就不适合了。我们就需要动态的加载 css，下面就是最简单的动态添加 css 的例子，当然你可以封装一下，增加成功或者失败回调，判断是否加载过改资源等等就不展开了。

```js
var head = document.getElementsByTagName('HEAD').item(0);
var style = document.createElement('link');
style.href = 'style.css';
style.rel = 'stylesheet';
style.type = 'text/css';
head.appendChild(style);
```

更新（2017.12）

element-ui 官方更新了 2.0 版本，同时也提供了一个新的换肤思路。文档「[vue-element-admin](https://panjiachen.github.io/vue-element-admin-site/#/theme)」。

### 3.3 侧边栏

这里又有谈一下导航栏的问题，本项目里的侧边栏是根据 router.js 配置的路由并且根据权限动态生成的，这样就省去了写一遍路由还要手动再写一次侧边栏这种麻烦事，但也遇到了一个问题，路由可能会有多层嵌套，很多人反馈自己的侧边栏会有三级，甚至还有五级的。所以重构了一下侧边栏，使用了递归组件，这样不管你多少级，都能愉快的显示了。

侧边栏高亮问题：很多人在群里问为什么自己的侧边栏不能跟着自己的路由高亮，其实很简单，element-ui 官方已经给了 default-active 所以我们只要：

```js
:default-active="$route.path"
```

将 default-active 一直指向当前路由就可以了，就是这么简单。

点击侧边栏，刷新当前路由。在用 spa（单页面开发）这种开发模式之前，大部分都是多页面后台，用户每次点击侧边栏都会重新请求这个页面，用户渐渐养成了点击侧边栏当前路由来刷新页面的习惯。但现在 spa 就不一样了，用户点击当前高亮的路由并不会刷新 view，因为 vue-router 会拦截你的路由，它判断你的 url 并没有任何变化，所以它不会触发任何钩子或者是 view 的变化。issue 地址，社区也对该问题展开了激烈讨论。

尤大本来也说要增加一个方法来强刷 view，但后来他又改变了心意 。但需要就摆在这里，我们该怎么办呢？他说了不改变 current URL 就不会触发任何东西，那我可不可以强行触发东西你？上有政策，下有对策我们变着花来 hack。方法也很简单，通过不断改变 url 的 query 来触发 view 的变化。我们监听侧边栏每个 link 的 click 事件，每次点击都给 router push 一个不一样的 query 来确保会重新刷新 view。

```js
clickLink(path) {
  this.$router.push({
    path,
    query: {
      t: +new Date() //保证每次点击路由的query项都是不一样的，确保会重新刷新view
    }
  })
}
```

但这也有一个弊端就是 url 后面有一个很难看的 query 后缀如 xxx.com/article/list?t=1496832345025，但我司用户们表示能接受。。。只能暂时这样 hack 了，不知道大家有没有更好的方法，学习学习。

### 3.4 Table

经过好几个版本的迭代，element-ui 的 table 组件已经能满足大部分业务需求了。不过 rowSpan colSpan 表格行 / 列合并现在并不是支持（element-ui2.0 版本之后开始支持）。官方对此功能的更新情况可以关注这个 issue「[[Table] 希望支持 rowSpan colSpan · Issue #670 · ElemeFE/element](https://github.com/ElemeFE/element/issues/670)」。这里我着重讲一下 table 表格几个常用的业务形态。

#### 3.4.1 Table 拖拽排序

这里主要是基于 Sortable。

```js
import Sortable from 'sortablejs'
let el = document.querySelectorAll('.el-table__body-wrapper > table > tbody')[0]
let sortable = Sortable.create(el)
```

在 table mounted 之后申明 Sortable.create (el) table 的每行 tr 就可以随意拖拽了，麻烦的目前我们的排序都是基于 dom 的，我们的数据层 list 并没有随之改变。所以我们就要手动的来管理我们的列表。

```js
this.sortable = Sortable.create(el, {
  onEnd: evt => { //监听end事件 手动维护列表
    const tempIndex = this.newList.splice(evt.oldIndex, 1)[0];
    this.newList.splice(evt.newIndex, 0, tempIndex);
  }
});
```

这样我们就简单的完成了 table 拖拽排序。这里如果不是基于 dom 的排序推荐使用 Vue.Draggable「[SortableJS/Vue.Draggable: Vue drag-and-drop component based on Sortable.js](https://github.com/SortableJS/Vue.Draggable)」。完整代码「作者的页面 404」

#### 3.4.2 Table 内联编辑

table 内联编辑也是一个常见的需求。其实也很简单，当我们拿到 list 数据之后先洗一下数据，每一条数据里面插入一个 edit [true or false] 判断符，来表示当前行是否处于编辑状态。之后就是通过 v-show 动态切换不同的相应 view 就可以了。完整代码「页面 404」

```js
<el-table-column min-width="300px" label="标题">
  <template scope="scope">
    <el-input v-show="scope.row.edit" size="small" v-model="scope.row.title"></el-input>
    <span v-show="!scope.row.edit">{{ scope.row.title }}</span>
  </template>
</el-table-column>
<el-table-column align="center" label="编辑" width="120">
  <template scope="scope">
    <el-button v-show='!scope.row.edit' type="primary" @click='scope.row.edit=true' size="small" icon="edit">编辑</el-button>
    <el-button v-show='scope.row.edit' type="success" @click='scope.row.edit=false' size="small" icon="check">完成</el-button>
  </template>
</el-table-column>
```

#### 3.4.3 Table 常见坑

通过 dialog 来编辑，新建，删除 table 的元素这种业务场景相对于前面说的两种更加的常见。而且也有不少的小坑。首先我们要明确一个点，vue 是一个 MVVM 框架，我们传统写代码是命令式编程，拿到 table 这个 dom 之后就是命令式对 dom 增删改。而我们现在用声明式编程，只用关注 data 的变化就好了，所以我们这里的增删改都是基于 list 这个数组来的。这里我们还要明确一点：vue 列表渲染注意事项「[列表渲染 — Vue.js](https://cn.vuejs.org/v2/guide/list.html#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)」。

由于 JavaScript 的限制，Vue 不能检测以下变动的数组： 当你利用索引直接设置一个项时，例如： vm.items [indexOfItem] = newValue

所以我们想改变 table 中第一条数据的值，通过 this.list[0]=newValue 这样是不会生效的。解决方案：

```js
// Array.prototype.splice`
example1.items.splice(indexOfItem, 1, newValue)
```

所以我们可以通过：

```js
//添加数据
this.list.unshift(this.temp);

//删除数据 
const index = this.list.indexOf(row); //找到要删除数据在list中的位置
this.list.splice(index, 1); //通过splice 删除数据

//修改数据
const index = this.list.indexOf(row); //找到修改的数据在list中的位置
this.list.splice(index, 1,this.updatedData); //通过splice 替换数据 触发视图更新
```

这样我们就完成了对 table 的增删改操作，列表 view 也自动响应发生了变化。这里在修改数据的时候还有一个小坑需要注意。当我们拿到需要修改行的数据时候不能直接将它直接赋值给 dialog，不然会发生下面的问题。

如上图所示，我们在 dialog 里面改变状态的时候，遮罩下面的 table 里面该行的状态也在那里跟着一直变化着。原因想必大家都猜到了。赋值的数据是一个 objec 引用类型共享一个内存区域的。所以我们就不能直接连等复制，需要重新指向一个新的引用，方案如下：

```js
//赋值对象是一个obj
this.objData=Object.assign({}, row) //这样就不会共用同一个对象

//数组我们也有一个巧妙的防范
newArray = oldArray.slice(); //slice会clone返回一个新数组
```

1『所以在没有很确定的时候，不要去删改作者的源码，很多时候他是有特定考虑的。』

#### 3.4.4 Tabs

tab 在后台项目中也比较常用的。假设我们有四个 tab 选项，每个 tab 都会向后端请求数据，但我们希望一开始只会请求当前的 tab 数据，而且 tab 来回切换的时候不会重复请求，只会实例化一次。首先我们想到的就是用 v-if 这样的确能做到一开始不会挂载后面的 tab，但有一个问题，每次点击这个 tab 组件都会重新挂载一次，这是我们不想看到的，这时候我们就可以用到 \<keep-alive> 了。

keep-alive 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。它是一个抽象组件：它自身不会渲染一个 DOM 元素，也不会出现在父组件链中。

所以我们就可以这样写 tabs 了。

```html
<el-tabs v-model="activeTab">
  <el-tab-pane label="简介及公告" name="announcement">
    <announcement />
  </el-tab-pane>
  <el-tab-pane label="资讯" name="information">
    <keep-alive>
      <information v-if="activeTab=='information'" />
    </keep-alive>
  </el-tab-pane>
  <el-tab-pane label="直播流配置" name="stream">
    <keep-alive>
      <stream v-if="activeTab=='stream'" />
    </keep-alive>
  </el-tab-pane>
</el-tabs>
```

### 3.5 Select 选择器

Select 选择器直接使用没有什么太多问题，但很多时候我们需要通过 Select 来回显一些数据，当我们 \<el-select v-model="objValue"> select 绑定一个 obj value 回显就会很蛋疼了，它要求必须保持同一个引用 issue「[select value 为 object 时怎么初始化默认项？ · Issue #1780 · ElemeFE/element](https://github.com/ElemeFE/element/issues/1780)」。这就意味着，我们回显数据的时候想先要找到该数据在 arr 中的位置，再回塞：demo「[Select does not support default object value · Issue #2479 · ElemeFE/element](https://github.com/ElemeFE/element/issues/2479/)」。

这还不是在远程搜索的情况下，如果是远程搜索的情况还要当疼。这里推荐一下 vue-multiselect「[shentao/vue-multiselect: Universal select/multiselect/tagging component for Vue.js](https://github.com/shentao/vue-multiselect)」，它能完美的解决前面 Element select 的问题。目前也是 vue component 中比较好用的一个，ui 也非常的好看，建议大家可以尝试性用一下，真的非常的不错。

### 3.6 Upload 上传

Upload 本身没什么好说的，文档写的蛮清楚了。这里主要说一下怎么将 Upload 组件和七牛直传结合在一起。

这里我们选择 api 直传的方式，就是我们首先要通过后端（go、node、php 都可以）文档「[软件开发工具包 - 七牛开发者中心](https://developer.qiniu.com/sdk#official-sdk)」生成七牛上传必要的 token（上传凭证）和 key（资源的最终名称）。所以现在只要想办法讲 token 和 key 塞进 post 请求里面就可以了，好在官方也提供了这个方法。但怎么才能先异步的拿到 token 再将它塞入请求里呢？

1『这里的知识点应该可以解决，101 那边上传远程服务器后获取图片在七牛 url 的难题，哈哈。（2020-05-21）』

这时候我们又发现了 before-upload 这个钩子还支持 promise 简直合我们的心意。但我们写着写着怎样才能动态的改变之前的 dataObj 呢？通过看源码发现我们可以 \_self.\_data 这样子拿到我们想要的数据。线上代码「[vue-element-admin/upload.vue at master · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/blob/master/src/views/qiniu/upload.vue)」。

```js
<template>
  <el-upload
      action="https://upload.qbox.me"
      :data="dataObj"
      drag
      :multiple="true"
      :before-upload="beforeUpload">
    <i class="el-icon-upload"></i>
    <div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
  </el-upload>
</template>
<script>
    import { getToken } from 'api/qiniu'; // 获取七牛token 后端通过Access Key,Secret Key,bucket等生成token
    // 七牛官方sdk https://developer.qiniu.com/sdk#official-sdk
    export default{
      data() {
        return {
          dataObj: { token: '', key: '' },
          image_uri: [],
          fileList: []
        }
      },
      methods: {
        beforeUpload() {
          const _self = this;
          return new Promise((resolve, reject) => {
            getToken().then(response => {
              const key = response.data.qiniu_key;
              const token = response.data.qiniu_token;
              _self._data.dataObj.token = token;
              _self._data.dataObj.key = key;
              resolve(true);
            }).catch(err => {
              console.log(err)
              reject(false)
            });
          });
        }
      }
    }
</script>
```

#### 3.6.1 jsx

在使用 Element 的时候，官方提供了很多可以自己写 render function 的地方，但由于 Element 内部都是用 jsx 写 render function 的，所以 demo 也都是 jsx，但很多人自己项目中其实是没有安装的，导致报错。但说真的用 createElement 裸写 render 函数还是有些蛋疼。我们要用 jsx，首先要安装 babel-plugin-transform-vue-jsx「[vuejs/babel-plugin-transform-vue-jsx: babel plugin for vue 2.0 jsx](https://github.com/vuejs/babel-plugin-transform-vue-jsx)」，安装方法如下：

```
npm install\
  babel-plugin-syntax-jsx\
  babel-plugin-transform-vue-jsx\
  babel-helper-vue-jsx-merge-props\
  babel-preset-es2015\
  --save-dev
```

.babelrc: 文件

```json
{
  "presets": ["es2015"],
  "plugins": ["transform-vue-jsx"]
}
```

这样我们就可以愉快的使用 jsx 写 render function 了。

### 3.7 element 常见问题

1、click 事件不触发问题：一直有人在群里问 \<el-input @click="handlenClick">Click Me\</el-input> 怎么不触发 click 事件，虽然 element 文档还有完善的空间但这种问题大家还真要自己好好认真看一下官方的 FAQ「[element/FAQ.md at dev · ElemeFE/element](https://github.com/ElemeFE/element/blob/dev/FAQ.md)」了。

官方说明了所有的原生事件必须添加 .native 修饰符。

2、修改 element 样式问题： 用 ui 组件总免不了需要对它做一些个性化定制的需求，所以我们就要覆盖 element 的一些样式。首先我们要了解一下 vue scoped 是什么，很多人非常喜欢用 scoped，妈妈再也不用担心样式冲突问题了，其实 scoped 也没有很神秘的，它就是基于 PostCss 的，加了一个作用局的概念。

```css
//编译前
.example {
  color: red;
}
//编译后
.example[_v-f3f3eg9] {
  color: red;
}
```

它和我们传统的命名空间的方法避免 css 冲突没有什么本质性的区别。现在我们来说说怎么覆盖 element-ui 样式。由于 element-ui 的样式我们是在全局引入的，所以你想在某个 view 里面覆盖它的样式就不能加 scoped，但你又想只覆盖这个页面的 element 样式，你就可在它的父级加一个 class，以用命名空间来解决问题。

```css
.aritle-page{ //你的命名空间
    .el-tag { //element-ui 元素
      margin-right: 0px;
    }
}
```

建议向楼主一样专门建一个 scss 文件里专门自定义 element-ui 的各种样式。线上代码「[vue-element-admin/element-ui.scss at master · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/blob/master/src/styles/element-ui.scss)」。

其它关于 element 相关的东西真的没有什么好说的了，人家文档和源码就放在那里，有问题就去看文档，再去 issue 里找找，再去看看源码，大部分问题都能解决了。给一个诀窍其实大部分诡异的问题都可以通过加一个 key 或者 Vue.nextTick 来解决。

1『哈哈，作者说的这个诀窍很棒。』

### 3.8 富文本

管理后台富文本也是一个非常重要的功能，楼主在这里也踩了不少的坑。楼主在项目里最终选择了 tinymce「[tinymce/tinymce: The world's #1 JavaScript library for rich text editing. Available for React, Vue and Angular](https://github.com/tinymce/tinymce)」。

这里在简述一下推荐使用 tinymce 的原因：tinymce 是一家老牌做富文本的公司（这里也推荐 ckeditor，也是一家一直做富文本的公司，新版本很不错），它的产品经受了市场的认可，不管是文档还是配置的自由度都很好。在使用富文本的时候有一点也很关键就是复制格式化，之前在用一款韩国人做的富文本 summernote 被它的格式化坑的死去活来，但 tinymce 的去格式化相当的好，它还有一个增值项目就是 powerpaste, 那是无比的强大，支持从 word 里面复制各种东西，都不会有问题。富文本还有一点也很关键，就是拓展性。楼主用 tinymce 写了好几个插件，学习成本和容易度都不错，很方便拓展。最后一点就是文档很完善，基本你想得到的配置项，它都有。tinymce 也支持按需加载，你可以通过它官方的 build 页定制自己需要的 plugins。我再来分析一下市面上其它的一些富文本：

1、summernote 先来说一个我绝对不推荐的富文本。这是一个韩国人开源的富文本（当然不推荐的理由不是因为这个），它对很多富文本业界公认的默认行为理解是反起到而行的，而且只为用了一个 dialog 的功能，引入了 boostrap，一堆人抗议就是不改。格式化也是差劲。反正不要用！不要用！不要用！

2、ckeditor ckeditor 也是一家老牌做富文本的公司，楼主旧版后台用的就是这个，今年也出了 5.0 版本，ui 也变美观了不少，相当的不错，而且它号称是插件最丰富的富文本了。推荐大家也可以试用一下。

3、quill 也是一个非常火的富文本，长相很不错。基于它写插件也很简单，api 设计也很简单。楼主不选择它的原因是它对图片的各种操作不友善，而且很难改。如果对图片没什么操作的用户，推荐使用。

4、medium-editor 大名鼎鼎的 medium 的富文本（非官方出品），但完成度还是不很不错，拓展性也不错。不过我觉得大部分用户还是会不习惯 medium 这种写作方式的。

5、Squire 一个比较轻量的富文本，压缩完才 11.5kb，相对于其它的富文本来说是非常的小了，推荐功能不复杂的建议使用。

6、wangEditor 一个国人写的富文本，用过感觉还是不错的。不过毕竟是个人的，不像专门公司做富文本的，配置型和丰富性不足。前端几大禁忌就有富文本 为什么都说富文本编辑器是天坑？，不过个人能做成这样子很不容易了。

7、百度 UEditor 没有深入使用过，只在一个 angular1X 的项目简单用过，不过说着的 ui 真的不好看，不符合当今审美了，官方也已经很久没跟新过了。

楼主列举了很多富文本但并没有列举任何 vue 相关的富文本，主要是因为富文本真的比想象中复杂，在前面的文章里也说过了，其实用 vue 封装组件很方便的，没必要去用人家封装的东西什么 vue-quill vue-editor 这种都只是简单包了一层，没什么难度的。还不如自己来封装，灵活性可控性更强一点。还有一点基于 vue 真没什么好的富文本，不像 react 有 facebook 出的 draft-js，ory 出的 editor，这种大厂出的产品。

当然你也可以选择一些付费的富文本编辑器，作者自己公司里面有一个项目就使用了 froala-editor 这款编辑器。不管是美观和易用性都是不错的，公司买的是专业版，一年也就 \$349 ，价格也是很合理的，但其实省去的程序员开发成本可能远不止这个价钱。

#### 3.8.1 Tinymce

这里来简单讲一下在自己项目中使用 Tinymce 的方法。

由于目前使用 npm 安装 Tinymce 方法比较负责复杂而且还有一些问题（日后可能会采用该模式）。:space_invader:

目前采用全局引用的方式。代码地址：static/tinymce static 目录下的文件不会被打包，在 index.html 中引入。

使用。由于富文本不适合双向数据流，所以只会 watch 传入富文本的内容一次变化，只会就不会再监听了，如果之后还有改变富文本内容的需求。可以通过 this.refs.xxx.setContent () 来设置。源码也很简单，有任何别的需求都可以在 @/components/Tinymce/index.vue 中自行修改。

#### 3.8.2 Markdown

markdown 我们这里选用了 simplemde-markdown-editor ，简单的用 vue 封装了一下地址，如果需求方能接受 markdown 就一定要用 markdown，坑真心会比富文本少很多。这里我们用 markdown 做了编辑器，还需要一个能解析的的东西。可以你传给后端让后端帮你转化，也可以前端自己来，这里推荐一个转化库 showdown。使用方法：

```js
import('showdown').then(showdown => { //用了 Dynamic import
  const converter = new showdown.Converter();//初始化
  this.html = converter.makeHtml(this.content)//转化
})
```

用法也很简单两行代码就完成了 markdown to html，当然它还有很多个性画的配置，大家有需求自行研究吧。

1『富文本抽时间好好研究下，目前的理解是将纯文本信息转化为 html 格式。』

### 3.9 导出 excel

这里先明确一点，如果你的业务需求对导出文件的格式没有什么要求，不建议导出成 xlsx 格式的，直接导出成 csv 的就好了，真的会简单很多。创建一个 a 标签，写上 data:text/csv;charset=utf-8 头，再把数据塞进去，encodeURI (csvContent) 一下就好了，详情就不展开了，大家可以借鉴这个 stackoverflow 回答「[How to export JavaScript array info to csv (on client side)? - Stack Overflow](https://stackoverflow.com/questions/14964035/how-to-export-javascript-array-info-to-csv-on-client-side)」。

我们重点说一下转 xlsx，我们这里用到了 js-xlsx「[SheetJS/sheetjs: SheetJS Community Edition -- Spreadsheet Data Toolkit](https://github.com/SheetJS/sheetjs)」，一个功能很强大 excel 处理库，只是下载各种格式 excel，还支持读取 excel，但上手难度也非常大，相当的复杂，其中涉及不少二进制相关的东西。不过好在官方给了我们一个 demo 例子「[SheetJS JS-XLSX In-Browser Write Demo](https://sheetjs.com/demos/writexlsx.html)」，我们写不来还抄不来么，于是我们就借鉴官方的例子来改造了一下，具体原理就不详细说了，真的很复杂。重点是我们怎么使用！首先我们封装一个 Export2Excel.js「[vue-element-admin/Export2Excel.js at master](https://github.com/PanJiaChen/vue-element-admin/blob/master/src/vendor/Export2Excel.js)」，它又依赖三个库：

```js
require('script-loader!file-saver'); //保存文件用
require('script-loader!vendor/Blob'); //转二进制用
require('script-loader!xlsx/dist/xlsx.core.min'); //xlsx核心
```

由于这几个文件不支持 import 引入，所以我们需要 `script-loader` 来将他们挂载到全局环境下。

它暴露了两个接口 export\_table\_to\_excel 和 export\_json\_to\_excel, 我们常用 export\_json\_to\_excel 因为更加的可控一点，我们可以自由的洗数据。

```js
handleDownload() {
  require.ensure([], () => { // 用 webpack Code Splitting xlsl还是很大的
    const { export_json_to_excel } = require('vendor/Export2Excel');
    const tHeader = ['序号', '文章标题', '作者', '阅读数', '发布时间']; // excel 表格头
    const filterVal = ['id', 'title', 'author', 'pageviews', 'display_time'];
    const list = this.list;
    const data = this.formatJson(filterVal, list); // 自行洗数据 按序排序的一个array数组
    export_json_to_excel(tHeader, data, '列表excel');
  })
}，
formatJson(filterVal, jsonData) {
  return jsonData.map(v => filterVal.map(j => v[j]))
}
```

### 3.10 ECharts

管理后台图表也是常见得需求。这里图表就只推荐 ECharts，功能齐全，社区 demo 也丰富 gallery。我还是那个观点，大部分插件建议大家还是自己用 vue 来包装就好了，真的很简单。ECharts 支持 webpack 引入，图省事可以将 ECharts 整个引入 var echarts = require ('echarts'); 不过 ECharts 还是不小的，我们大部分情况只是用到很少一部分功能，我平时习惯于按需引入的。

```js
// 引入 ECharts 主模块
var echarts = require('echarts/lib/echarts');
// 引入柱状图
require('echarts/lib/chart/bar');
// 引入提示框和标题组件
require('echarts/lib/component/tooltip');
require('echarts/lib/component/title');

```

webpack 中使用 ECharts 文档 ECharts 按需引入模块文档「[incubator-echarts/index.js at master · apache/incubator-echarts](https://github.com/apache/incubator-echarts/blob/master/index.js)」，接下来我们就要在 vue 中声明初始化 ECharts 了。因为 ECharts 初始化必须绑定 dom，所以我们只能在 vue 的 mounted 生命周期里初始化。

```js
mounted() {
  this.initCharts();
},
methods: {
  this.initCharts() {
    this.chart = echarts.init(this.$el);
    this.setOptions();
  },
  setOptions() {
    this.chart.setOption({
      title: {
        text: 'ECharts 入门示例'
      },
      tooltip: {},
      xAxis: {
        data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"]
      },
      yAxis: {},
      series: [{
        name: '销量',
        type: 'bar',
        data: [5, 20, 36, 10, 10, 20]
      }]
    })
  }
}
```

就这样简单，ECharts 就配置完成了，这时候你想说我的 data 是远程获取的，或者说我动态改变 ECharts 的配置该怎么办呢？我们可以通过 watch 来触发 setOptions 方法。

```js
//第一种 watch options变化 利用vue的深度 watcher，options一有变化就重新setOption
watch: {
  options: {
    handler(options) {
      this.chart.setOption(this.options)
    },
    deep: true
  },
}
//第二种 只watch 数据的变化 只有数据变化时触发ECharts
watch: {
  seriesData(val) {
    this.setOptions({series:val})
  }
}
```

1『上面的监听相关的知识点，跟远程请求数据相关，这个知识点应该有很多重要的应用场景，目前还没能力吃透。（2020-05-21）』

其实都差不多，还是要结合自己业务来封装。后面就和平时使用 ECharts 没有什么区别了。题外话 ECharts 的可配置项真心多，大家使用的时候可能要花一点时间了解它的 api 的。知乎有个问题：百度还有什么比较良心的产品？答案：ECharts，可见 ECharts 的强大与好用。

### 3.11 相同 component 不同参数

创建与编辑。其实后台创建与编辑功能是最常见的了，它区别去前台项目多了改的需求，但大部分创建页面与编辑页面字段和 ui 几乎是一样的，所以我们准备公用一个 component 来对应不同的页面。有两种常见的方法，来区别创建与编辑。

1、通过路由 path 的方式 这种方式最简单暴力，我自己的项目中使用这种方式，通过约定路径中出现 'edit' 就判断为编辑模式。比较省力和方便，不过这是要在大家写路径的时候都按照规范来写的前提下。

2、通过 meta 来区分，比较推荐这种方式来区分。

```js
computed: {
  isEdit() {
    return this.$route.meta.isEdit // 根据meta判断
    // return this.$route.path.indexOf('edit') !== -1 // 根据路由判断
  }
}，
created() {
  if (this.isEdit) { 
    this.fetchData();
  }
},
```

就这样简单的实现了多路由复用了一个 component，其实不只是创建和编辑可以这样用，如两个列表的一模一样，只是一个是内部文章另一个是调取外部文章都能复用组件，通过 meta 的方式来判断调取不同的接口。

### 黑板墙

楼主问一下，这个项目的代码，我拉下来后，运行起来，发现有的表格表头和内容的 border 歪了一点。你们有遇到这种情况吗？

回复 Rouner：留给后来者：如果你的代码出现表头和内容有 1px 的距离偏差，那么请在 style 下面的 element-ui.scss 文件的最后加上 body .el-table th {display: table-cell!important;} 就能解决这个问题。问题出现原因不详。如果表格表头和内容的偏移还解决不了，可以调用 element-ui 的 doLayout 方法： this.\$refs. 你的表格.doLayout ();

## 0304. 手摸手，带你用 vue 撸后台 —— 极简的后台基础模板

这篇文章主要是介绍了 vueAdmin 做了哪些事情，希望大家如果有后台新项目要开发，建议基于 vue-admin-template 来开发，而 vue-element-admin 更多的是用来当做一个集成方案，你要什么功能就去里面找拿来用，因为两者的基础架构是一样的，所以复用成本也很低。

做这个 vueAdmin-template 的主要原因是：vue-element-admin 这个项目的初衷是一个 vue 的管理后台集成方案，把平时用到的一些组件或者经验分享给大家，同时它也在不断的维护和拓展中，比如最近重构了 dashboard，加入了全屏功能，新增了 tabs-view 等等。所以项目会越来越复杂，不太适合很多初用 vue 的同学来构建后台。所以就写了这个基础模板，它没有复杂的功能，只包含了一个后台需要最基础的东西。vueAdmin-template 主要是基于 vue-cli webpack 模板为基础开发的。

引入了如下 dependencies：1）element-ui 饿了么出品的 vue2.0 pc UI 框架。2）axios 一个现在主流并且很好用的请求库，支持 Promise。3）js-cookie 一个轻量的 JavaScript 库来处理 cookie。4）normalize.css 格式化 css。5）nprogress 轻量的全局进度条控制。6）vuex 官方状态管理。7）vue-router 官方路由。

该项目只做了一个管理后台需要极简的功能，封装了 axios 请求，支持无限层级路由，动态权限和动态侧边栏。如果需要更多复杂的功能可以参考 vue-element-admin，若还有不足，欢迎提 issue 或者 pr。下文会简单说一下用该模板需要注意的地方。

### 4.1 路由懒加载

路由懒加载应该是写大一点的项目都会用的一个功能，只有在使用这个 component 的时候才会加载这个相应的组件，这样写大大减少了初始页面 js 的大小并且能更好的利用游览器的缓存。

```js
const Foo = resolve => require(['./Foo.vue'], resolve)
//或者
const Foo = () => import('./Foo');
```

在懒加载页面不多的情况下一切是那么的美好，但我司后台业务在不断地迭代，现在项目近百个路由，这时候使用路由懒加载在开发模式下就是一件痛苦的事情了，随手改一行代码热更新都是要 6000ms + 的，这怎么能忍。楼主整整花了一天多的时间找原因，能 webpack 优化的方法都用了，什么 dll、HappyPack 等方法都是过了，但提升的效果都不是很明显，正好那段时间出了 webpack3 楼主也升级了，编译速度也得到了很大幅度的提升，不过也要 2000ms+。后来经过大神 @jzlxiaohei 的指点发现原来是路由懒加载搞得鬼，楼主猜测可能是异步加载导致 webpack 每次的 cache 失效了，所以每次的 rebuild 才会这么的慢。找到了原因我们就可以对症下药了，我们就自己封装了一个\_import () 的方法，只有在正式环境下才使用懒加载。这样解决了困扰多事的 rebuild 慢问题。代码「[vue-element-admin/index.js at master · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/blob/master/src/router/index.js#L3)」。

```js
const _import = require('./_import_' + process.env.NODE_ENV);
const Foo = _import('Foo');
```

整整比原来 6000ms 快了十多倍，我终于又能愉快的开发了。

### 4.2 权限——控制

在手摸手，带你用 vue 撸后台系列二（登录权限篇）这章中其实已经详细介绍过了。该项目中权限的实现方式是：通过获取当前用户的权限去比对路由表，生成当前用户具的权限可访问的路由表，通过 router.addRoutes 动态挂载到 router 上。但其实很多公司的业务逻辑可能不是这样的，举一个例子来说，很多公司的需求是每个页面的权限是动态配置的，不像本项目中是写死预设的。但其实原理是相同的。如这个例子，你可以在后台通过一个 tree 控件或者其它展现形式给每一个页面动态配置权限，之后将这份路由表存储到后端。当用户登录后根据 role，后端返回一个相应的路由表或者前端去请求之前存储的路由表动态生成可访问页面，之后就是 router.addRoutes 动态挂载到 router 上，你会发现原来是相同的，万变不离其宗。

### 4.3 导航

侧边栏：本项目里的侧边栏是根据 router.js 配置的路由并且根据权限动态生成的，这样就省去了写一遍路由还要再手动写侧边栏这种麻烦事，同是使用了递归组件，这样不管你路由多少级嵌套，都能愉快的显示了。权限验证那里也做了递归的处理。

面包屑：本项目中也封装了一个面包屑导航，它也是通过 watch \$route 动态生成的。代码「[vue-admin-template/index.vue at master · PanJiaChen/vue-admin-template](https://github.com/PanJiaChen/vue-admin-template/blob/master/src/components/Breadcrumb/index.vue)」。

由于侧边栏导航和面包屑亦或是权限，你会发现其实都是和 router 密切相关的，所以基于 vue-router 路由信息对象上做了一下小小的拓展，自定义了一些属性：

```
icon : the icon show in the sidebar
hidden : if hidden:true will not show in the sidebar
redirect : if redirect:noredirect will not redirct in the levelbar
noDropdown : if noDropdown:true will not has submenu in the sidebar
meta : { role: ['admin'] } will control the page role
```

大家也可以结合自己的业务需求增改这些自定义属性。

### 4.4 iconfont

element-ui 自带的图标不是很丰富，但管理后台图标的定制性又很强。这里只给大家推荐使用阿里的 iconfont「[Iconfont-阿里巴巴矢量图标库](https://www.iconfont.cn/)」，简单好用又方便管理。本项目中已经嵌入了一些 iconfont 作为例子，大家可以自行替换。这里来简单介绍一下 iconfont 的使用方式。首先注册好 iconfont 账号之后，可以在我的项目中管理自己的 iconfont 。我司所有的项目都是用这个管理的，真心推荐使用。

创建好图标库后如果有更新替换也很方便，这里我使用了 Symbol 的方式引入，这里还有 unicode，font-class 的引入方式，有兴趣的可以自行研究「[Iconfont-阿里巴巴矢量图标库](https://www.iconfont.cn/help/detail?spm=a313x.7781069.1998910419.13.HpQ1yI&helptype=code)」。之后我们点击下载 Symbol，会发现有如下这些文件，我们只要关心 iconfont.js 就可以了。我们将它替换项目中的 iconfont.js 就可以了。本项目中也封装了一个 svg component 方便大家使用。

```html
<icon-svg icon-class="填入你需要的 iconfont 名字就能使用了"></icon-svg>
```

### 4.5 favicon

每个项目都需要有一个属于自己的 favicon。其实实现起来非常的方便，我们主需要借助 html-webpack-plugin「[jantimon/html-webpack-plugin: Simplifies creation of HTML files to serve your webpack bundles](https://github.com/jantimon/html-webpack-plugin)」。

```js
//webpack config
function resolveApp(relativePath) {
    return path.resolve(relativePath);
}
new HtmlWebpackPlugin({
      filename: config.build.index,
      template: 'index.html',
      inject: true,
      favicon: resolveApp('favicon.ico')
    }),
```

你只要将本项目跟目录下的 favicon.ico 文件替换为你想要的图标即可。

### 4.6 eslint

vue cli 默认提供了 standard 和 airbnb 两种 lint 规范，说真的一个检查校验的太松一个又太紧，而且每个团队的 lint 规范又是不同的，所以楼主干脆在项目里把大部分常用的 lint 规范都列举了出来并写上了注释方便大家修改代码地址「[vue-admin-template/.eslintrc.js at master · PanJiaChen/vue-admin-template](https://github.com/PanJiaChen/vue-admin-template/blob/master/.eslintrc.js)」，大家也可以把自己的规范上传到 npm，像 vue 一样 vue-eslint-config。配置 eslint 对多人协作的项目有很大的好处，同时配置好 lint 在加 ide 的 lint 插件写代码简直要起飞。相关配置可见第一篇教程。

### 4.7 postcss

相信大部分 vue 的项目都是基于 vue-cli「[vuejs/vue-cli: Standard Tooling for Vue.js Development](https://github.com/vuejs/vue-cli) | [Vue CLI](https://cli.vuejs.org/)」来开发的，不过毕竟每个人需求都是不太一样的，需要自定义一些的东西。就比如拿 postcss 来说 vue-cli 有一个小坑，它默认 autoprefixer 只会对通过 vue-loader 引入的样式有作用，换而言之也就是 .vue 文件里面的 css autoprefixer 才会效果。相关问题 issues/544,issues/600「[Autoprefixer is only active for .vue files · Issue #600 · vuejs-templates/webpack](https://github.com/vuejs-templates/webpack/issues/600)」。解决方案也很简单粗暴。

```html
//app.vue
<style lang="scss">
  @import './styles/index.scss'; // 全局自定义的css样式
</style>
```

你在 .vue 文件中引入你要的样式就可以了，或者你可以改变 vue-cli 的文件在 css-loader 前面在加一个 postcss-loader，在前面的 issue 地址中已经给出了解决方案。这里再来说一下 postcss 的配置问题，新版的 vue-cli webpack 模板「[vuejs-templates/webpack: A full-featured Webpack + vue-loader setup with hot reload, linting, testing & css extraction.](https://github.com/vuejs-templates/webpack)」inti 之后跟目录下默认有一个.postcssrc.js 。vue-loader 的 postcss 会默认读取这个文件的里的配置项，所以在这里直接改配置文件就可以了。配置和 postcss「[postcss/postcss: Transforming styles with JS plugins](https://github.com/postcss/postcss)」是一样的。

```js
//.postcssrc.js
module.exports = {
  "plugins": {
    // to edit target browsers: use "browserlist" field in package.json
    "autoprefixer": {}
  }
}
//package.json
"browserslist": [
    "> 1%",
    "last 2 versions",
    "not ie <= 8"
  ]
```

如上代码所述，autoprefixe r 回去读取 package.json 下 browserslist 的配置文件：

1. \> 1% 兼容全球使用率大于 1% 的游览器。

2. last 2 versions 兼容每个游览器的最近两个版本。

3. not ie <= 8 不兼容 ie8 及以下 具体可见 browserslist「[browserslist/browserslist: Share target browsers between different front-end tools, like Autoprefixer, Stylelint and babel-preset-env](https://github.com/browserslist/browserslist)」、postcss 也还有很多很多其它的功能大家可以自行去把玩「[PostCSS.parts | A searchable catalog of PostCSS plugins](https://www.postcss.parts/)」。

### 4.8 babel-polyfill

本项目暂时没有兼容性需求，如有兼容性需求可自行使用 babel-polyfill。在 Node/Browserify/webpack 中使用

```
npm install --save babel-polyfill // 下载依赖
```

在入口文件中引入：

```js
import 'babel-polyfill';

// 或者
require('babel-polyfill');//es6
```

在 webpack.config.js 中加入 babel-polyfill 到你的入口数组：

```js
module.exports = {
    entry:["babel-polyfill","./app/js"]
}
```

具体可参考 link。或者更简单暴力 polyfill.io「[Polyfill.io](https://cdn.polyfill.io/v3/)」使用它给的一个 cdn 地址，引入这段 js 之后它会自动判断游览器，加载缺少的那部分 polyfill，但国内速度肯能不行，大家可以自己搭 cdn。

### 4.9 跨域问题

楼主 vue 群里的小伙伴们问的最多的问题还是关于跨域的，其实跨域问题真的不是一个很难解决的问题。这里我来简单总结一下我推荐的几种跨域解决方案。

1、我最推荐的也是我司常用的方式就是 \*\*cors\*\* 全称为 Cross Origin Resource Sharing（跨域资源共享）。这玩意对应前端来说和平时发请求写法上没有任何区别，工作量基本都在后端这里。每一次请求浏览器必须先以 OPTIONS 请求方式发送一个预请求，从而获知服务器端对跨源请求所支持 HTTP 方法。在确认服务器允许该跨源请求的情况下，以实际的 HTTP 请求方法发送那个真正的请求。推荐的原因是只要第一次配好了，之后不管有多少接口和项目复用就可以了，一劳永逸的解决了跨域问题，而且不管是开发环境还是测试环境都能方便的使用。

2、但总有后端觉得麻烦不想这么搞。那前端也是有解决方案的，在 dev 开发模式下可以下使用 \*\*webpack 的 proxy，使用也是很方便的看一下文档就会使用了，楼主一些个人项目使用的该方法。但这种方法在生成环境是不适用的。在生产环境中需要使用 Nginx 反向代理 \*\* 不管是 proxy 和 nginx 的原理都是一样的通过搭建一个中转服务器来转发请求规避跨域的问题。1）开发环境 cors；生成环境 cors。2）开发环境 proxy；生成环境 nginx。

这里我只推荐这两种方式跨域，其它的跨域方式都很多，但真心主流的也就这两种方式。

### 4.10 easy-mock

vue-element-admin 由于是一个纯前端个人项目，所以所以的数据都是用 mockjs 生成的，它的原理是：拦截了所有的请求并代理到本地模拟数据，所以 network 中没有任何的请求发出。不过这并不符合实际业务开发中的场景，所以这个项目中使用了前不久刚出的 easy-mock，支持跨域，mockjs 的语法，支持 Swagger 这几点还是挺不错的。相关文章「[活儿好又性感的在线 Mock 平台 - Easy Mock - 掘金](https://juejin.im/post/58ff1fae61ff4b0066792f6e)」。

### 4.11 baseurl

线上或者测试环境接口的 base\_url 不一样是很长见得需求，或者你在本地用了如 easy-mock 这种模拟数据到线上环境你想用自己公司生产环境的数据，这些需求都可以简单的通过用 baseurl 来解决。首先我们在 config/ 下有 dev.env.js 和 prod.env.js 这两个配置文件。用它来区分不同环境的配置参数。

```js
//dev.env.js
module.exports = {
  NODE_ENV: '"development"',
  BASE_API: '"https://easy-mock.com/mock/5950a2419adc231f356a6636/vue-admin"',
}
//prod.env.js
module.exports = {
  NODE_ENV: '"production"',
  BASE_API: '"https://prod-xxx"',
}
```

同时本项目封装了 axios 拦截器，方便大家使用，大家也可根据自己的业务自行修改。

```js
import axios from 'axios';
import { Message } from 'element-ui';
import store from '../store';

// 创建axios实例
const service = axios.create({
  baseURL: process.env.BASE_API, // api的base_url 读取config配置文件
  timeout: 5000                  // 请求超时时间
});

// request拦截器
service.interceptors.request.use(config => {
  if (store.getters.token) {
    config.headers['X-Token'] = store.getters.token; // 让每个请求携带自定义token 请根据实际情况自行修改
  }
  return config;
}, error => {
  // Do something with request error
  console.log(error); // for debug
  Promise.reject(error);
})

// respone拦截器
service.interceptors.response.use(
  response => {
  /**
  * code为非20000是抛错 可结合自己业务进行修改
  */
    const res = response.data;
    if (res.code !== 20000) {
      Message({
        message: res.data,
        type: 'error',
        duration: 5 * 1000
      });

      // 50008:非法的token; 50012:其他客户端登录了;  50014:Token 过期了;
      if (res.code === 50008 || res.code === 50012 || res.code === 50014) {
        MessageBox.confirm('你已被登出，可以取消继续留在该页面，或者重新登录', '确定登出', {
          confirmButtonText: '重新登录',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          store.dispatch('FedLogOut').then(() => {
            location.reload();// 为了重新实例化vue-router对象 避免bug
          });
        })
      }
      return Promise.reject(error);
    } else {
      return response.data;
    }
  },
  error => {
    console.log('err' + error);// for debug
    Message({
      message: error.message,
      type: 'error',
      duration: 5 * 1000
    });
    return Promise.reject(error);
  }
)

export default service;
```

由于 axios 每一个都是一个实例，你的请求都是基于这个实例来的，所以所以配置的参数属性都继承了下来。

```js
//api.xxx.js
import fetch from '@/utils/fetch';
export function getInfo(token) {
  return fetch({
    url: '/user/info',
    method: 'get',
    params: { token }
  });
}
//你可以直接这样使用，之前拦截器写的东西都是生效的，
//它自动会有一个你之前配置的baseURL,
//但你说我这个请求baseURL和其它的不同,
//这也是很方便的，你可以字请求内部修改，
//它会自动覆盖你在创建实例时候写的参数如
export function getInfo(token) {
  return fetch({
    baseURL: https://api2-xxxx.com
    url: '/user/info',
    method: 'get',
    params: { token }
  });
}
```

## 0306手摸手，带你封装一个 vue component

这里这是拿了一个很简单的 countUp 组件举了一个简单例子，有的时候自己动手丰衣足食，很多插件的封装比想象中简单的多。产品经理再也不会看到我因为这个 fu\*\* 插件怎么不支持这个功能而愁眉苦脸了，我们可以更好地满足产品了。

### 6.1 为什么选择自己封装第三方库

最近几个月我司把之前两三年的所有业务都用了 vue 重构了一遍，前台使用 vue+ssr，后台使用了 vue+element，在此过程中封装和自己写了很多 vue component。其实 vue 写 component 相当简单和方便，github 上有很多的 vue component 都只是简单的包装了一些 jquery 或者原生 js 的插件，但我个人是不太喜欢使用这些第三方封装的。理由如下：

1、很多第三方封装的组件参数配置项其实是有缺损的。如一些富文本或者图表组件，配置项远比你想想中的多得多，第三方封装组件很难覆盖全部所有配置。

2、第三方组件的更新频率很难保证。很多第三方封装组件并不能一直和原始组件保持同步更新速度，万一原始组件更新了某个你需要的功能，但第三方并没有更新那岂不是很尴尬，而且很多第三方组件维护一段时间之后就不维护了。

3、灵活性和针对性。还是那富文本来说，富文本在我司有很多定制化需求，我们需要将图片上传七牛，需要将图片打水印，需要很多针对业务的特殊需求，使用第三方包装的组件是不合适的，一般基于第三方封装的组件是很难拓展的。

所以我觉得大部分组件还是自己封装来的更为方便和灵活一些。

### 6.2 动手开干

接下来我们一起手摸手教改造包装一个 js 插件，只要几分钟就可以封装一个专属于你的 vue component。封装对象：countUp.js「[inorganik/countUp.js: Animates a numerical value by counting to it](https://github.com/inorganik/countUp.js)」，改造后结果 vue-countTo「[PanJiaChen/vue-countTo: It's a vue component that will count to a target number at a specified duration https://panjiachen.github.io/countTo/demo/](https://github.com/PanJiaChen/vue-countTo)」。

首先我们用官方提供的 vue-cli 来构建项目，这里选择了 webpack-simple（组件相对而言比较简单，不需要很多复杂的功能，所以 webpack-simple 已经满足需求了）。

```
$ npm install -g vue-cli
$ vue init webpack-simple my-project
$ cd my-project
$ npm install
```

安装 countup.js：

```
$ npm install countup.js
$ npm run dev
```

启动项目之后按照 countup.js 官方 demo 初始化插件。

app.vue

```
<template>
  <span ref='countup'></span>
</template>

<script>
import CountUp from 'countup.js'
export default {
  name: 'countup-demo',
  data () {
    return {
      numAnim:null
    }
  },
  mounted(){
    this.initCountUp()
  },
  methods:{
    initCountUp(){
      this.numAnim = new CountUp(this.$refs.countup,0, 2017)
      this.numAnim.start();
    }
  }
}
</script>
```

刷新页面，就这么简单，countUp.js 已经生效了。

接下来查看 countUp.js 的 github 发现它定义了如下可配置参数。对应 vue 就是 props，类型和初始化一目了然。

1『图片里的是 countUp.js 的 params。』

```js
props: {
  start: {
    type: Number,
    default: 0
  },
  end: {
    type: Number,
    default: 2017
  },
  decimal: {
    type: Number,
    default: 0
  },
  duration: {
    type: Number,
    default: 2.5
  },
  options: {
    type: Object
  }
}
```

之后再将 countup 之前写死的配置项替换为动态 props 就可以了。

```js
this.numAnim = new CountUp(this.$refs.countup, 
                           this.start,
                           this.end,
                           this.decimal,
                           this.duration,
                           this.options)
```

使用组件：

```html
<vue-count-up :end="2500" :duration="2.5"></vue-count-up>
```

只要几分钟一个属于自己的原生组件就包装好了，就是这么简单。完整 demo「[countUp-demo/App.vue at master · PanJiaChen/countUp-demo](https://github.com/PanJiaChen/countUp-demo/blob/master/src/App.vue)」。

这时候你如果觉得使用 countUp.js 还有些不满足你的需求，那你可以选择自己来造轮子了。

### 6.3 造轮子篇

首先当然是阅读源码。其实源码也就两部分核心代码：

第一部分：主要是就是 requestAnimationFrame，在游览器不支持 requestAnimationFrame 的情况下使用 setTimeout 来模拟，这段代码值得仔细阅读，自己在平时的项目中也能借鉴使用这段代码。

第二部分：就是 count 函数。

看懂这两部分之后造轮子就相当的简单了，demo「[PanJiaChen/vue-countTo: It's a vue component that will count to a target number at a specified duration https://panjiachen.github.io/countTo/demo/](https://github.com/PanJiaChen/vue-countTo)」。造轮子过程中发现 countUp，并没有 autoplay 这个参数项可以让组件自动开始count，没关系。。。我们可以自己来撸，我们首先定义 autoplay 这个props为布尔值，默认所有组件 autoplay 为 true

```js
 props:{
   autoplay: {
     type: Boolean,
     required: false,
     default: true
   }
 }
 ```
 
定义好 props 之后只要在 mounted 生命周期内加一个判断就完事了。

```js
mounted() {
  if (this.autoplay) {
    this.start();
  }
}
```

我们的 countUp 组件可以自动 count 了！

### 6.4 上传 npm

在不跨项目的情况下之前所做的已经满足需求了。但我们不能就此满足，我想让世界上更多的人来使用我的插件，这时候就要上传  npm「[npm | build amazing things](https://www.npmjs.com/)」了 demo「[PanJiaChen/vue-countTo: It's a vue component that will count to a target number at a specified duration https://panjiachen.github.io/countTo/demo/](https://github.com/PanJiaChen/vue-countTo)」。

首先我们新建一个index.js。

```js
import CountTo from './vue-countTo.vue'

// 导出模块
export default CountTo

//global 情况下 自动安装
if (typeof window !== 'undefined' && window.Vue) {
  window.Vue.component('count-to', CountTo)
}
```

同时我们也要改造一下 webpack 的配置，因为不是所有使用你组件的人都是通过 npm 安装使用 import 引入组件的的。还有很多人是通过 \<script> 标签的方式直接引入的，所以我们要将 libraryTarget 改为 umd 格式「[Output | webpack](https://webpack.js.org/configuration/output/)」。

```js
library: 'CountTo',
libraryTarget: 'umd',
umdNamedDefine: true
```

大功告成，现在只要将它发布到 npm 就可以了，首先注册一个npm 账号，之后配置自己的 package.json（注意填写 version，每次发布的 version 不能相同；main 为入口文件地址）。之后只要一行命令 npm publish 你的项目就发到 npm 了，快让小伙伴们一起来用你的vue component 吧！