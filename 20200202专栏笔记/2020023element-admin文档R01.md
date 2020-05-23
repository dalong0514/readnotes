## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

#### 01. 常识

#### 02. 反常识

#### 03. 知识来源

比如提出者，如何演化成型的；书或专栏具体出现的地方。

#### 04. 例子

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

例子。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。找一个他的 TED 演讲，有的话。

#### 01. 基本信息

用一句话描述你对这个大牛的印象。

#### 02. 贡献及著作

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是在这个专栏的整个地图里，这一章节所在的节点。

### 2. 摘录及评论

## 0101. 介绍

vue-element-admin 是一个后台前端解决方案，它基于 vue 和 element-ui 实现。它使用了最新的前端技术栈，内置了 i18 国际化解决方案，动态路由，权限验证，提炼了典型的业务模型，提供了丰富的功能组件，它可以帮助你快速搭建企业级中后台产品原型。相信不管你的需求是什么，本项目都能帮助到你。

建议：本项目的定位是后台集成方案，不太适合当基础模板来进行二次开发。因为本项目集成了很多你可能用不到的功能，会造成不少的代码冗余。如果你的项目不关注这方面的问题，也可以直接基于它进行二次开发。

### 1.1 功能

```
- 登录 / 注销

- 权限验证
  - 页面权限
  - 指令权限
  - 权限配置
  - 二步登录

- 多环境发布
  - dev sit stage prod

- 全局功能
  - 国际化多语言
  - 多种动态换肤
  - 动态侧边栏（支持多级路由嵌套）
  - 动态面包屑
  - 快捷导航(标签页)
  - Svg Sprite 图标
  - 本地/后端 mock 数据
  - Screenfull全屏
  - 自适应收缩侧边栏

- 编辑器
  - 富文本
  - Markdown
  - JSON 等多格式

- Excel
  - 导出excel
  - 导入excel
  - 前端可视化excel
  - 导出zip

- 表格
  - 动态表格
  - 拖拽表格
  - 内联编辑

- 错误页面
  - 401
  - 404

- 組件
  - 头像上传
  - 返回顶部
  - 拖拽Dialog
  - 拖拽Select
  - 拖拽看板
  - 列表拖拽
  - SplitPane
  - Dropzone
  - Sticky
  - CountTo

- 综合实例
- 错误日志
- Dashboard
- 引导页
- ECharts 图表
- Clipboard(剪贴复制)
- Markdown2html
```

### 1.2 前序准备

你需要在本地安装 node 和 git。本项目技术栈基于 ES2015+、vue、vuex、vue-router 、vue-cli 、axios 和 element-ui，所有的请求数据都使用 Mock.js 进行模拟，提前了解和学习这些知识会对使用本项目有很大的帮助。同时配套一个系列的教程文章，如何从零构建后一个完整的管理后台项目，建议大家先看完这些文章再来实践本项目。

1『该系列文章，也记录在本教程里。』

### 1.3 目录结构

本项目已经为你生成了一个完整的开发框架，提供了涵盖中后台开发的各类功能和坑位，下面是整个项目的目录结构。

```
├── build                      # 构建相关
├── mock                       # 项目mock 模拟数据
├── plop-templates             # 基本模板
├── public                     # 静态资源
│   │── favicon.ico            # favicon图标
│   └── index.html             # html模板
├── src                        # 源代码
│   ├── api                    # 所有请求
│   ├── assets                 # 主题 字体等静态资源
│   ├── components             # 全局公用组件
│   ├── directive              # 全局指令
│   ├── filters                # 全局 filter
│   ├── icons                  # 项目所有 svg icons
│   ├── lang                   # 国际化 language
│   ├── layout                 # 全局 layout
│   ├── router                 # 路由
│   ├── store                  # 全局 store管理
│   ├── styles                 # 全局样式
│   ├── utils                  # 全局公用方法
│   ├── vendor                 # 公用vendor
│   ├── views                  # views 所有页面
│   ├── App.vue                # 入口页面
│   ├── main.js                # 入口文件 加载组件 初始化等
│   └── permission.js          # 权限管理
├── tests                      # 测试
├── .env.xxx                   # 环境变量配置
├── .eslintrc.js               # eslint 配置项
├── .babelrc                   # babel-loader 配置
├── .travis.yml                # 自动化CI配置
├── vue.config.js              # vue-cli 配置
├── postcss.config.js          # postcss 配置
└── package.json               # package.json
```

### 1.4 安装

TIP：强烈建议不要用直接使用 cnpm 安装，会有各种诡异的 bug，可以通过重新指定 registry 来解决 npm 安装速度慢的问题。若还是不行，可使用 yarn 替代 npm。Windows 用户若安装不成功，很大概率是 node-sass 安装失败，解决方案「[node-sass 下载失败 解决方案 · Issue #24 · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/issues/24)」。另外因为 node-sass 是依赖 python环境的，如果你之前没有安装和配置过的话，需要自行查看一下相关安装教程。启动完成后会自动打开浏览器访问 http://localhost:9527， 你看到下面的页面就代表操作成功了。

接下来你可以修改代码进行业务开发了，本项目内建了典型业务模板、常用业务组件、模拟数据、HMR 实时预览、状态管理、国际化、全局路由等等各种实用的功能来辅助开发，你可以继续阅读和探索左侧的其它文档。

建议：你可以把 vue-element-admin当做工具箱或者集成方案仓库，在 vue-admin-template 的基础上进行二次开发，想要什么功能或者组件就去 vue-element-admin 那里复制过来。

### 1.5 Vue 生态圈

首先了解这些 vue 生态圈的东西，会对你上手本项目有很大的帮助。

1、Vue Router 是 vue 官方的路由。它能快速的帮助你构建一个单页面或者多页面的项目。

2、Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。它能解决你很多全局状态或者组件之间通信的问题。

3、Vue Loader 是为 vue 文件定制的一个 webpack 的 loader，它允许你以一种名为单文件组件（SFCs）的格式撰写 Vue 组件。它能在开发过程中使用热重载来保持状态，为每个组件模拟出 scoped CSS 等等功能。不过大部分情况下你不需要对它直接进行配置，脚手架都帮你封装好了。

4、Vue Test Utils 是官方提供的一个单元测试工具。它能让你更方便的写单元测试。

5、Vue Dev-Tools Vue 在浏览器下的调试工具。写 vue 必备的一个浏览器插件，能大大的提高你调试的效率。

6、Vue CLI 是官方提供的一个 vue 项目脚手架，本项目也是基于它进行构建的。它帮你封装了大量的 webpack、babel 等其它配置，让你能花更少的精力在搭建环境上，从而能更专注于页面代码的编写。不过所有的脚手架都是针对大部分情况的，所以一些特殊的需求还是需要自己进行配置。建议先阅读一遍它的文档，对一些配置有一些基本的了解。

7、Vetur 是 VS Code 的插件。如果你使用 VS Code 来写 vue 的话，这个插件是必不可少的。

## 0102. 布局

页面整体布局是一个产品最外层的框架结构，往往会包含导航、侧边栏、面包屑以及内容等。想要了解一个后台项目，先要了解它的基础布局。

### 2.1 Layout

对应代码：[vue-element-admin/src/layout at master · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/tree/master/src/layout)

1『源码所在的位置「src>layout」。』

@ 是 webpack 的 alias 不懂得请自行研究「[Resolve | webpack](https://webpack.js.org/configuration/resolve/#resolve-alias)」。

vue-element-admin 中大部分页面都是基于这个 layout 的，除了个别页面如：login、404、401 等页面没有使用该 layout。如果你想在一个项目中有多种不同的 layout 也是很方便的，只要在一级路由那里选择不同的 layout 组件就行。

1『只需改一级路由，这个很值得借鉴。』

```js
// No layout
{
  path: '/401',
  component: () => import('errorPage/401')
}

// Has layout
{
  path: '/documentation',

  // 你可以选择不同的layout组件
  component: Layout,

  // 这里开始对应的路由都会显示在app-main中 如上图所示
  children: [{
    path: 'index',
    component: () => import('documentation/index'),
    name: 'documentation'
  }]
}
```

这里使用了 vue-router 路由嵌套「[嵌套路由 | Vue Router](https://router.vuejs.org/zh/guide/essentials/nested-routes.html)」，所以一般情况下，你增加或者修改页面只会影响 app-main这个主体区域。其它配置在 layout 中的内容如：侧边栏或者导航栏都是不会随着你主体页面变化而变化的。

```
/foo                                  /bar
+------------------+                  +-----------------+
| layout           |                  | layout          |
| +--------------+ |                  | +-------------+ |
| | foo.vue      | |  +------------>  | | bar.vue     | |
| |              | |                  | |             | |
| +--------------+ |                  | +-------------+ |
+------------------+                  +-----------------+
```

当然你也可以一个项目里面使用多个不同的 layout，只要在你想作用的路由父级上引用它就可以了。

### 2.2 app-main

对应代码：@/layout/components/AppMain

这里在 app-main 外部包了一层 keep-alive 主要是为了缓存 <router-view> 的，配合页面的 tabs-view 标签导航使用，如不需要可自行去除「[快捷导航(标签栏导航) | vue-element-admin](https://panjiachen.github.io/vue-element-admin-site/zh/guide/essentials/tags-view.html)」。

其中 transition 定义了页面之间切换动画，可以根据自己的需求，自行修改转场动画。相关文档「[进入/离开 & 列表过渡 — Vue.js](https://cn.vuejs.org/v2/guide/transitions.html)」。默认提供了 fade 和 fade-transform 两个转场动画，具体 css 实现见 transition.scss「[vue-element-admin/transition.scss at master · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/blob/master/src/styles/transition.scss)」。如果需要调整可在 AppMain.vue 中调整 transition 的 name。

1『 transition 貌似可以实现点击后按钮隐藏的功能，有空试验下。』

### 2.3 router-view

Different router the same component vue 真实的业务场景中，这种情况很多。比如：

我创建和编辑的页面使用的是同一个 component，默认情况下这两个页面切换时并不会触发 vue 的 created 或者 mounted 钩子，官方说你可以通过 watch \$route 的变化来进行处理，但说真的还是蛮麻烦的。后来发现其实可以简单的在 router-view 上加上一个唯一的 key，来保证路由切换时都会重新渲染触发钩子了。这样简单的多了。

```html
<router-view :key="key"></router-view>

computed: {
  key() {
    // 只要保证 key 唯一性就可以了，保证不同页面的 key 不相同
    return this.$route.fullPath
  }
 }
 ```
 
 1『作者的这个实现方法好。』
 
TIP：或者可以像本项目中 editForm 和 createForm 声明两个不同的 view 但引入同一个 component。示例代码：@/views/example

```html
<!-- create.vue -->
<template>
  <article-detail :is-edit='false'></article-detail> //create
</template>
<script>
  import ArticleDetail from './components/ArticleDetail'
</script>

<!-- edit.vue -->
<template>
   <article-detail :is-edit='true'></article-detail> //edit
</template>
<script>
  import ArticleDetail from './components/ArticleDetail'
</script>
```

### 2.4 移动端

element-ui 官方对自己的定位是桌面端后台框架，而且对于管理后台这种重交互的项目来说是不能通过简单的适配来满足桌面端和移动端两端不同的交互，所以真要做移动版后台，建议重新做一套系统。所以本项目也不会适配移动端，只是用 media query 做了一点简单的响应式布局，有需求请自行修改。

## 0103. 路由和侧边栏

路由和侧边栏是组织起一个后台应用的关键骨架。本项目侧边栏和路由是绑定在一起的，所以你只有在 @/router/index.js 下面配置对应的路由，侧边栏就能动态的生成了。大大减轻了手动重复编辑侧边栏的工作量。当然这样就需要在配置路由的时候遵循一些约定的规则。

### 3.1 配置项

首先我们了解一些本项目配置路由时提供了哪些配置项。

```json
// 当设置 true 的时候该路由不会在侧边栏出现 如 401，login 等页面，或者如一些编辑页面 /edit/1
hidden: true // (默认 false)

//当设置 noRedirect 的时候该路由在面包屑导航中不可被点击
redirect: 'noRedirect'

// 当你一个路由下面的 children 声明的路由大于1个时，自动会变成嵌套的模式--如组件页面
// 只有一个时，会将那个子路由当做根路由显示在侧边栏--如引导页面
// 若你想不管路由下面的 children 声明的个数都显示你的根路由
// 你可以设置 alwaysShow: true，这样它就会忽略之前定义的规则，一直显示根路由
alwaysShow: true

name: 'router-name' // 设定路由的名字，一定要填写不然使用<keep-alive>时会出现各种问题
meta: {
  roles: ['admin', 'editor'] // 设置该路由进入的权限，支持多个权限叠加
  title: 'title' // 设置该路由在侧边栏和面包屑中展示的名字
  icon: 'svg-name' // 设置该路由的图标
  noCache: true // 如果设置为 true，则不会被 <keep-alive> 缓存(默认 false)
  breadcrumb: false //  如果设置为 false，则不会在 breadcrumb 面包屑中显示(默认 true)
  affix: true // 若果设置为 true，它则会固定在 tags-view 中(默认 false)

  // 当路由设置了该属性，则会高亮相对应的侧边栏。
  // 这在某些场景非常有用，比如：一个文章的列表页路由为：/article/list
  // 点击文章进入文章详情页，这时候路由为/article/1，但你想在侧边栏高亮文章列表的路由，就可以进行如下设置
  activeMenu: '/article/list'
}
```

示例：

```json
{
  path: '/permission',
  component: Layout,
  redirect: '/permission/index', //重定向地址，在面包屑中点击会重定向去的地址
  hidden: true, // 不在侧边栏线上
  alwaysShow: true, //一直显示根路由
  meta: { roles: ['admin','editor'] }, //你可以在根路由设置权限，这样它下面所有的子路由都继承了这个权限
  children: [{
    path: 'index',
    component: ()=>import('permission/index'),
    name: 'permission',
    meta: {
      title: 'permission',
      icon: 'lock', //图标
      roles: ['admin','editor'], //或者你可以给每一个子路由设置自己的权限
      noCache: true // 不会被 <keep-alive> 缓存
    }
  }]
}
```

### 3.2 路由

这里的路由分为两种，constantRoutes 和 asyncRoutes。1）constantRoutes： 代表那些不需要动态判断权限的路由，如登录页、404、等通用页面。2）asyncRoutes： 代表那些需求动态判断权限并通过 addRoutes 动态添加的页面。具体的会在权限验证页面介绍。

TIP：这里所有的路由页面都使用「路由懒加载」了 ，具体介绍见文档「」。如果你想了解更多关于 browserHistory 和 hashHistory，请参看「构建和发布」。其它的配置和 vue-router 官方并没有区别，自行查看文档。

注意事项：这里有一个需要非常注意的地方就是 404 页面一定要最后加载，如果放在 constantRoutes 一同声明了 404 ，后面的所以页面都会被拦截到 404 ，详细的问题见 addRoutes when you've got a wildcard route for 404s does not work.

### 3.3 侧边栏

本项目侧边栏主要基于 element-ui 的 el-menu 改造。前面也介绍了，侧边栏是通过读取路由并结合权限判断而动态生成的，而且还需要支持路由无限嵌套，所以这里还使用到了递归组件。代码地址：@/views/layout/components/Sidebar

这里同时也改造了 element-ui 默认侧边栏不少的样式，所有的 css 都可以在 @/styles/sidebar.scss 中找到，你也可以根据自己的需求进行修改。这里需要注意一下，一般侧边栏有两种形式即：submenu 和直接 el-menu-item。 一个是嵌套子菜单，另一个则是直接一个链接。如下图：

在 Sidebar 中已经帮你做了判断，当你一个路由下面的 children 声明的路由大于 >1 个时，自动会变成嵌套的模式。如果子路由正好等于一个就会默认将子路由作为根路由显示在侧边栏中，若不想这样，可以通过设置在根路由中设置 alwaysShow: true 来取消这一特性。如：

```json
// No submenu, because children.length===1
{
  path: '/icon',
  component: Layout,
  children: [{
    path: 'index',
    component: ()=>import('svg-icons/index'),
    name: 'icons',
    meta: { title: 'icons', icon: 'icon' }
  }]
},

// Has submenu, because children.length>=1
{
  path: '/components',
  component: Layout,
  name: 'component-demo',
  meta: {
    title: 'components',
    icon: 'component'
  },
  children: [
    { path: 'tinymce', component: ()=>import('components-demo/tinymce'), name: 'tinymce-demo', meta: { title: 'tinymce' }},
    { path: 'markdown', component: ()=>import('components-demo/markdown'), name: 'markdown-demo', meta: { title: 'markdown' }},
  ]
}
```

unique-opened，你可以在 Sidebar/index.vue 中设置 unique-opened 来控制侧边栏，是否只保持一个子菜单的展开。

### 3.4 多级目录——嵌套路由

如果你的路由是多级目录，如本项目 @/views/nested 那样， 有三级路由嵌套的情况下，不要忘记还要手动在二级目录的根文件下添加一个 \<router-view>。如：@/views/nested/menu1/index.vue，原则上有多少级路由嵌套就需要多少个 \<router-view>。

### 3.5 点击侧边栏——刷新当前路由

在用 spa（单页面应用）这种开发模式的之前，用户每次点击侧边栏都会重新请求这个页面，用户渐渐养成了点击侧边栏当前路由来刷新 view 的习惯。但现在 spa 就不一样了，用户点击当前高亮的路由并不会刷新 view，因为 vue-router 会拦截你的路由，它判断你的 url 并没有任何变化，所以它不会触发任何钩子或者是 view 的变化。issue 地址「[[Feature] A reload method like location.reload() · Issue #296 · vuejs/vue-router](https://github.com/vuejs/vue-router/issues/296)」，社区也对该问题展开了激烈讨论。

尤大本来也说要增加一个方法来强刷 view，但后来他又改变了心意。但需求就摆在这里，我们该怎么办呢？他说了不改变 current URL 就不会触发任何东西，那我可不可以强行触发你的 hook 呢？上有政策， 下有对策我们变着花来 hack。方法也很简单，通过不断改变 url 的 query 来触发 view 的变化。我们监听侧边栏每个 link 的 click 事件，每次点击都给 router push 一个不一样的 query 来确保会重新刷新 view。

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

PS：不要忘了在 router-view 加上一个特定唯一的 key，如 \<router-view :key="\$route.path"></router-view>， 但这也有一个弊端就是 url 后面有一个很难看的 query 后缀如 xxx.com/article/list?t=1496832345025

你可以从前面的 issue 中知道还有很多其它方案。我本人在公司项目中，现在采取的方案是判断当前点击的菜单路由和当前的路由是否一致，但一致的时候，会先跳转到一个专门 Redirect 的页面，它会将路由重定向到我想去的页面，这样就起到了刷新的效果了。

相关例子，如图所示。点击图片所示的全局 size 大小切换按钮，你会发现页面 app-main 区域进行了刷新。它就是运用了重定向到 Redirect 页面之后再重定向回原始页面的方法。

点击的时候重定向页面至 /redirect

```js
const { fullPath } = this.$route
this.$router.replace({
  path: '/redirect' + fullPath
})
```

redirect 页面在重定向回原始页面。

```js
// redirect.vue
// https://github.com/PanJiaChen/vue-element-admin/blob/master/src/views/redirect/index.vue
export default {
  beforeCreate() {
    const { params, query } = this.$route
    const { path } = params
    this.$router.replace({ path: '/' + path, query })
  },
  render: function(h) {
    return h() // avoid warning message
  }
}
```

### 3.6 面包屑

本项目中也封装了一个面包屑导航，它也是通过 watch \$route 变化动态生成的。它和 menu 也一样，也可以通过之前那些配置项控制一些路由在面包屑中的展现。大家也可以结合自己的业务需求增改这些自定义属性。比如可以在路由中声明 breadcrumb:false，让其不在 breadcrumb 面包屑显示。

代码地址：@/components/Breadcrumb

### 3.7 侧边栏滚动问题

之前版本的滚动都是用 css 来做处理的。

```js
overflow-y: scroll;

::-webkit-scrollbar {
  display: none;
}
```

首先这样写会有兼容性问题，在火狐或者其它低版本浏览器中都会比较不美观。其次在侧边栏收起的情况下，受限于 element-ui 的 menu 组件的实现方式，不能使用该方式来处理。所以现版本中使用了 el-scrollbar 来处理侧边栏滚动问题。

代码地址：@/components/Sidebar

1『自己用 element 搭建布局的时候也发现这个问题了，边栏滚动不了。』

### 3.8 侧边栏——外链 v3.8.2+

你也可以在侧边栏中配置一个外链，只要你在 path 中填写了合法的 url 路径，当你点击侧边栏的时候就会帮你新开这个页面。例如：

```json
{
  "path": "external-link",
  "component": Layout,
  "children": [
    {
      "path": "https://github.com/PanJiaChen/vue-element-admin",
      "meta": { "title": "externalLink", "icon": "link" }
    }
  ]
}
```

### 3.9 侧边栏默认展开

某些场景下，用户需要默认展开侧边栏的某些 sub-menu，如下图：

可以通过 default-openeds 来进行设置，首先找到侧边栏代码「[vue-element-admin/index.vue at master · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/blob/master/src/layout/components/Sidebar/index.vue)」。

```html
 <el-menu
        :default-openeds="['/example','/nested']" // 添加本行代码
        :default-active="activeMenu"
        :collapse="isCollapse"
        :background-color="variables.menuBg"
        :text-color="variables.menuText"
        :unique-opened="false"
        :active-text-color="variables.menuActiveText"
        :collapse-transition="false"
        mode="vertical"
      >
        <sidebar-item v-for="route in permission_routes" :key="route.path" :item="route" :base-path="route.path" />
      </el-menu>
```

注意 :default-openeds="['/example','/nested']" 里面填写的是 submenu 的 route-path。

## 0104. 权限验证

在手摸手，带你用 vue 撸后台系列二「登录权限篇」这篇文章中其实已经详细介绍过了。该项目中权限的实现方式是：通过获取当前用户的权限去比对路由表，生成当前用户具的权限可访问的路由表，通过 router.addRoutes 动态挂载到 router 上。

但其实很多公司的业务逻辑可能不是这样的，举一个例子来说，很多公司的需求是每个页面的权限是动态配置的，不像本项目中是写死预设的。但其实原理是相同的。如：你可以在后台通过一个 tree 控件或者其它展现形式给每一个页面动态配置权限，之后将这份路由表存储到后端。当用户登录后得到 roles，前端根据 roles 去向后端请求可访问的路由表，从而动态生成可访问页面，之后就是 router.addRoutes 动态挂载到 router 上，你会发现原来是相同的，万变不离其宗。只是多了一步将后端返回路由表和本地的组件映射到一起。相关 issue「[请问路由配置可以动态的改变吗? · Issue #293 · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/issues/293)」。

```js
const map={
 login:require('login/index').default // 同步的方式
 login:()=>import('login/index')      // 异步的方式
}
//你存在服务端的map类似于
const serviceMap=[
 { path: '/login', component: 'login', hidden: true }
]
//之后遍历这个map，动态生成asyncRoutes
并将 component 替换为 map[component]
```

Ps：不排除之后本项目会增加权限控制面板支持真正的动态配置权限。

### 4.1 逻辑修改

现在路由层面权限的控制代码都在 @/permission.js 中，如果想修改逻辑，直接在适当的判断逻辑中 next() 释放钩子即可。

### 4.2 指令权限

封装了一个指令权限，能简单快速的实现按钮级别的权限判断。 v-permission「[vue-element-admin/src/directive/permission at master · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/tree/master/src/directive/permission)」。

#### 4.2.1 使用

```html
<template>
  <!-- Admin can see this -->
  <el-tag v-permission="['admin']">admin</el-tag>

  <!-- Editor can see this -->
  <el-tag v-permission="['editor']">editor</el-tag>

  <!-- Editor can see this -->
  <el-tag v-permission="['admin','editor']">Both admin or editor can see this</el-tag>
</template>

<script>
// 当然你也可以为了方便使用，将它注册到全局
import permission from '@/directive/permission/index.js' // 权限判断指令
export default{
  directives: { permission }
}
</script>
```

#### 4.2.2 局限

In some cases it is not suitable to use v-permission, such as element Tab component which can only be achieved by manually setting the v-if.

可以使用全局权限判断函数，用法和指令 v-permission 类似。

```html
<template>
  <el-tab-pane v-if="checkPermission(['admin'])" label="Admin">Admin can see this</el-tab-pane>
  <el-tab-pane v-if="checkPermission(['editor'])" label="Editor">Editor can see this</el-tab-pane>
  <el-tab-pane v-if="checkPermission(['admin','editor'])" label="Admin-OR-Editor">Both admin or editor can see this</el-tab-pane>
</template>

<script>
import checkPermission from '@/utils/permission' // 权限判断函数

export default{
   methods: {
    checkPermission
   }
}
</script>
```

## 0105. 快捷导航

本功能是响应大家需求，后期加上的，其实本人在公司项目或者个人项目中是不太使用该功能的。以前那些传统后台框架往往会包含此功能，由于以前的后台项目大部分都是多页面的形式，所以标签栏导航功能还是具有一定意义的基本，大部分都是基于 iframe 的方式实现的。但随着时代的发展，现在的后台项目几乎都是 spa（single page web application 单页面开发），再使用以前的方案来实现标签导航显然是不合适的。

所以目前的方案大致为： 运用 keep-alive 和 router-view 的结合。代码: @/layout/components/AppMain.vue

```html
<keep-alive :include="cachedViews">
  <router-view></router-view>
</keep-alive>
```

顶部标签栏导航实际作用相当于 nav 的另一种展现形式，其实说白了都是一个个 router-link，点击跳转到相应的页面。然后我们在来监听路由 \$route 的变化，来判断当前页面是否需要重新加载或者已被缓存。

### 5.1 visitedViews && cachedViews

目前 tags-view 维护了两个数组。1）visitedViews : 用户访问过的页面就是标签栏导航显示的一个个 tag 数组集合。2）cachedViews : 实际 keep-alive 的路由。可以在配置路由的时候通过 meta.noCache 来设置是否需要缓存这个路由默认都缓存。配置文档「[路由和侧边栏 | vue-element-admin](https://panjiachen.github.io/vue-element-admin-site/zh/guide/essentials/router-and-nav.html)」。

### 5.2 注意事项

由于目前 keep-alive 和 router-view 是强耦合的，而且查看文档和源码不难发现 keep-alive 的 include 默认是优先匹配组件的 name ，所以在编写路由 router 和路由对应的 view component 的时候一定要确保两者的 name 是完全一致的。（切记 name 命名时候尽量保证唯一性，切记不要和某些组件的命名重复了，不然会递归引用最后内存溢出等问题）。

1『路由名称一定不能跟组件名重复。所以组件名索引可以都命名为 index.vue，靠文件夹来识别。而路由名一定要跟 vue 里脚本里定义的名字相同，这样才能被缓存。』

DEMO：

```json
//router 路由声明
{
  path: 'create-form',
  component: ()=>import('@/views/form/create'),
  name: 'createForm',
  meta: { title: 'createForm', icon: 'table' }
}
//路由对应的view  form/create
export default {
  name: 'createForm'
}
```

一定要保证两着的名字相同，切记写重或者写错。默认如果不写 name 就不会被缓存，详情见issue。

### 5.3 缓存不适合场景

目前缓存的方案对于某些业务是不适合的，比如文章详情页这种 /article/1、/article/2，他们的路由不同但对应的组件却是一样的，所以他们的组件 name 就是一样的，就如前面提到的，keep-alive 的 include 只能根据组件名来进行缓存，所以这样就出问题了。目前有两种解决方案：

1、不使用 keep-alive 的 include 功能 ，直接是用 keep-alive 缓存所有组件，这样子是支持前面所说的业务情况的。 前往@/layout/components/AppMain.vue文件下，移除 include 相关代码即可。当然直接使用 keep-alive 也是有弊端的，他并不能动态的删除缓存，你最多只能帮它设置一个最大缓存实例的个数 limit。相关 issue「[希望keep-alive能增加可以动态删除已缓存组件的功能 · Issue #6509 · vuejs/vue](https://github.com/vuejs/vue/issues/6509)」。

2、使用 localStorage 等浏览器缓存方案，自己进行缓存处理。

### 5.4 Affix 固钉 v3.10.0+

当在声明路由是添加了 Affix 属性，则当前 tag 会被固定在 tags-view中（不可被删除）。

```json
 {
    path: '',
    component: Layout,
    redirect: 'dashboard',
    children: [
      {
        path: 'dashboard',
        component: () => import('@/views/dashboard/index'),
        name: 'Dashboard',
        meta: {
          title: 'dashboard',
          icon: 'dashboard',
          noCache: true,
          affix: true
        }
      }
    ]
  }
```

### 5.5 移除

其实 keep-alive 源码不复杂，但逻辑还是蛮绕的，之前尤大自己修复一个 bug 的时候也不小心搞错了，连发两个版本来修复，所以如果没有标签导航栏需求的用户，建议移除此功能。首先找到 @/layout/components/AppMain.vue 然后移除 keep-alive。

```html
<template>
  <section class="app-main" style="min-height: 100%">
    <transition name="fade-transform" mode="out-in">
      <router-view></router-view>
    </transition>
  </section>
</template>
```

然后移除整个 @/layout/components/TagsView.vue 文件，并在 @/layout/components/index 和 @/layout/Layout.vue 移除相应的依赖。最后把 @/store/modules/tagsView 相关的代码删除即可。

## 0106. 新增页面

如果熟悉 vue-router 的配置就很简单了。首先在 @/router/index.js 中增加你需要添加的路由。如：新增一个 excel 页面：

```json
{
  path: '/excel',
  component: Layout,
  redirect: '/excel/export-excel',
  name: 'excel',
  meta: {
    title: 'excel',
    icon: 'excel'
  }
}
```

TIP：仅仅这样不会有任何效果的，它只是创建了一个基于 layout 的一级路由，你还需要在它下面的 children 中添加子路由。

```json
{
  path: '/excel',
  component: Layout,
  redirect: '/excel/export-excel',
  name: 'excel',
  meta: {
    title: 'excel',
    icon: 'excel'
  },
  children: [
    {
      path: 'export-excel',
      component: ()=>import('excel/exportExcel'),
      name: 'exportExcel',
      meta: { title: 'exportExcel' }
    }
  ]
}
```

这样侧边栏就会出现如图所示的 menu-item 了。

TIP：由于 children 下面只声明了一个路由所以不会有展开箭头，如果 children 下面的路由个数大于 1 就会有展开箭头，如下面所示。 如果你想忽视这个自动判断可以使用 alwaysShow: true，这样它就会忽略之前定义的规则，一直显示根路由。详情见路由和侧边栏。

```json
{
  path: '/excel',
  component: Layout,
  redirect: '/excel/export-excel',
  name: 'excel',
  meta: {
    title: 'excel',
    icon: 'excel'
  },
  children: [
    { path: 'export-excel', component: ()=>import('excel/exportExcel'), name: 'exportExcel', meta: { title: 'exportExcel' }},
    { path: 'export-selected-excel', component: ()=>import('excel/selectExcel'), name: 'selectExcel', meta: { title: 'selectExcel' }},
    { path: 'upload-excel', component: ()=>import('excel/uploadExcel'), name: 'uploadExcel', meta: { title: 'uploadExcel' }}
  ]
}
```

侧边栏就会出现如图所示的 submenu 了。

### 6.1 多级目录——嵌套路由

如果你的路由是多级目录，如本项目 @/views/nested 那样， 有三级路由嵌套的情况下，不要忘记还要手动在二级目录的根文件下添加一个 \<router-view>。如：@/views/nested/menu1/index.vue，原则上有多少级路由嵌套就需要多少个 \<router-view>。

### 6.2 新增 view

新增完路由之后不要忘记在 @/views 文件下创建对应的文件夹，一般性一个路由对应一个文件，该模块下的功能组件或者方法就建议在本文件夹下创建一个 utils 或 components 文件夹，各个功能模块维护自己的 utils 或 components 组件。如：

### 6.3 新增 api

最后在 @/api 文件夹下创建本模块对应的 api 服务。

### 6.4 新增组件

个人写 vue 项目的习惯，在全局的 @/components 只会写一些全局的组件，如富文本，各种搜索组件，封装的日期组件等等能被公用的组件。每个页面或者模块特定的业务组件则会写在当前 views 下面。如：@/views/article/components/xxx.vue。这样拆分大大减轻了维护成本。请记住拆分组件最大的好处不是公用而是可维护性！

### 6.5 新增样式

页面的样式和组件是一个道理，全局的 @/style 放置一下全局公用的样式，每一个页面的样式就写在当前 views下面，请记住加上 scoped 或者命名空间，避免造成全局的样式污染。

```css
<style>
/* global styles */
</style>

<style scoped>
/* local styles */
.xxx-container{
  /* name scoped */
  xxx
}
</style>
```

## 0107. 样式

### 7.1 CSS Modules

在样式开发过程中，有两个问题比较突出：1）全局污染 —— CSS 文件中的选择器是全局生效的，不同文件中的同名选择器，根据 build 后生成文件中的先后顺序，后面的样式会将前面的覆盖；2）选择器复杂 —— 为了避免上面的问题，我们在编写样式的时候不得不小心翼翼，类名里会带上限制范围的标示，变得越来越长，多人开发时还很容易导致命名风格混乱，一个元素上使用的选择器个数也可能越来越多，最终导致难以维护。

好在 vue 为我们提供了 scoped 可以很方便的解决上述问题。 它顾名思义给 css 加了一个域的概念。

```css
/* 编译前 */
.example {
  color: red;
}

/* 编译后 */
.example[_v-f3f3eg9] {
  color: red;
}
```

只要加上 \<style scoped> 这样 css 就只会作用在当前组件内了。详细文档见 vue-loader「[Scoped CSS | Vue Loader](https://vue-loader.vuejs.org/guide/scoped-css.html#mixing-local-and-global-styles)」

TIP：使用 scoped 后，父组件的样式将不会渗透到子组件中。不过一个子组件的根节点会同时受其父组件的 scoped CSS 和子组件的 scoped CSS 的影响。这样设计是为了让父组件可以从布局的角度出发，调整其子组件根元素的样式。

### 7.2 目录结构

vue-element-admin 所有全局样式都在 @/src/styles 目录下设置

```
├── styles
│   ├── btn.scss                 # 按钮样式
│   ├── element-ui.scss          # 全局自定义 element-ui 样式
│   ├── index.scss               # 全局通用样式
│   ├── mixin.scss               # 全局mixin
│   ├── sidebar.scss             # sidebar css
│   ├── transition.scss          # vue transition 动画
│   └── variables.scss           # 全局变量
```

常见的工作流程是，全局样式都写在 src/styles 目录下，每个页面自己对应的样式都写在自己的 .vue 文件之中

```css
<style>
/* global styles */
</style>

<style scoped>
/* local styles */
</style>
```

### 7.3 自定义 element-ui 样式

现在我们来说说怎么覆盖 element-ui 样式。由于 element-ui 的样式我们是在全局引入的，所以你想在某个页面里面覆盖它的样式就不能加 scoped，但你又想只覆盖这个页面的 element 样式，你就可在它的父级加一个 class，用命名空间来解决问题。

```css
.article-page {
  /* 你的命名空间 */
  .el-tag {
    /* element-ui 元素*/
    margin-right: 0px;
  }
}
```

当然也可以使用深度作用选择器，下文会介绍。

1『好办法，数据流开发里表格某列背景色的设置用这个办法试试。』

### 7.4 父组件改变子组件样式——深度选择器

当你子组件使用了 scoped 但在父组件又想修改子组件的样式可以通过 >>> 来实现：

```css
<style scoped>
.a >>> .b { /* ... */ }
</style>
```

将会编译成：

```css
.a[data-v-f3f3eg9] .b {
  /* ... */
}
```

如果你使用了一些预处理的东西，如 sass 你可以通过 /deep/ 来代替 >>> 实现想要的效果。所以你想覆盖某个特定页面 element 的 button 的样式，你可以这样做：

```css
.xxx-container >>> .el-button{
  xxxx
}
```

官方文档「[Scoped CSS | Vue Loader](https://vue-loader.vuejs.org/guide/scoped-css.html)」。

### 7.5 Autoprefixer [新版本已无该问题]

vue-cli 有一个小坑，它默认 autoprefixer 只会对通过 vue-loader 引入的样式才会有有作用，换而言之也就是 .vue 文件里面的 css autoprefixer 才会效果。相关问题 issues/544「[autoprefixer 只能用于通过 vue-loader 解析的样式 · Issue #544 · vuejs-templates/webpack](https://github.com/vuejs-templates/webpack/issues/544)」、issues/600「[Autoprefixer is only active for .vue files · Issue #600 · vuejs-templates/webpack](https://github.com/vuejs-templates/webpack/issues/600)」。解决方案也很简单粗暴：

```css
//app.vue
<style lang="scss">
  @import './styles/index.scss'; // 全局自定义的 css 样式
</style>
```

你在 .vue 文件中引入你要的样式就可以了，或者你可以改变 vue-cli 的文件在 css-loader 前面在加一个 postcss-loader，在前面的 issue 地址中已经给出了解决方案。不过新版本已经默认解决处理了这个问题。

### 7.6 Postcss

这里再来说一下 postcss 的配置问题，新版的 vue-cli webpack 模板 init 之后根目录下默认有一个postcss.config.js 。vue-loader 的 postcss 会默认读取这个文件的里的配置项，所以在这里直接改配置文件就可以了。配置和 postcss 是一样的。

```
// postcss.config.js
module.exports = {
  plugins: {
    autoprefixer: {}
  }
}

// package.json
"browserslist": [
    "> 1%",
    "last 2 versions",
    "not ie <= 8"
  ]
```

如上面代码所述的，autoprefixer 会去读取 package.json 下 browserslist 的配置参数：1）1% 兼容全球使用率大于 1% 的浏览器。2）last 2 versions 兼容每个浏览器的最近两个版本。3）not ie <= 8 不兼容 ie8 及以下。

具体可见 browserslist「[browserslist/browserslist: Share target browsers between different front-end tools, like Autoprefixer, Stylelint and babel-preset-env](https://github.com/browserslist/browserslist)」。postcss 也还有很多很多其它的功能大家可以自行去探究「[PostCSS.parts | A searchable catalog of PostCSS plugins](https://www.postcss.parts/)」。

### 7.7 Mixin

本项目没有设置自动注入 sass 的 mixin 到全局，所以需要在使用的地方手动引入 mixin。

```
<style rel="stylesheet/scss" lang="scss">
  @import "src/styles/mixin.scss";
</style>
```

如需要自动将 mixin 注入到全局 ，可以使用 sass-resources-loader「[shakacode/sass-resources-loader: SASS resources (e.g. variables, mixins etc.) loader for Webpack. Also works with less, post-css, etc.](https://github.com/shakacode/sass-resources-loader)」。

## 0108. 和服务端进行交互

### 8.1 前端请求流程

在 vue-element-admin 中，一个完整的前端 UI 交互到服务端处理流程是这样的：1）UI 组件交互操作；2）调用统一管理的 api service 请求函数；3）使用封装的 request.js 发送请求；4）获取服务端返回；5）更新 data。

从上面的流程可以看出，为了方便管理维护，统一的请求处理都放在 @/src/api 文件夹中，并且一般按照 model 纬度进行拆分文件，如：

```
api/
  login.js
  article.js
  remoteSearch.js
  ...
```

#### 8.1.1 request.js

其中，@/src/utils/request.js 是基于 axios 的封装，便于统一处理 POST，GET 等请求参数，请求头，以及错误提示信息等。具体可以参看 request.js。 它封装了全局 request 拦截器、response 拦截器、统一的错误处理、统一做了超时处理、baseURL 设置等。

### 8.2 一个请求文章列表页的例子

```js
// api/article.js
import request from '../utils/request';
export function fetchList(query) {
  return request({
    url: '/article/list',
    method: 'get',
    params: query
  })
}
```

```js
// views/example/list
import { fetchList } from '@/api/article'
export default {
  data() {
    list: null,
    listLoading: true
  },
  methods: {
    fetchData() {
      this.listLoading = true
      fetchList().then(response => {
        this.list = response.data.items
        this.listLoading = false
      })
    }
  }
}
```

### 8.3 设置多个 baseURL

我们可以通过环境变量设置多个 baseURL，从而请求不同的 api 地址。

```js
# .env.development
VUE_APP_BASE_API = '/dev-api' #注入本地 api 的根路径
VUE_APP_BASE_API2 = '/dev-api2' #注入本地 api 的根路径
```

之后根据环境变量创建 axios 实例，让它具有不同的 baseURL。 @/utils/request.js

```js
// create an axios instance
const service = axios.create({
  baseURL: process.env.BASE_API, // api 的 base_url
  timeout: 5000 // request timeout
})

const service2 = axios.create({
  baseURL: process.env.BASE_API2, // api 的 base_url
  timeout: 5000 // request timeout
})
```

或者

```js
export function fetchList(query) {
  return request({
    url: '/article/list',
    method: 'get',
    params: query,
    baseURL: 'xxxx' // 直接通过覆盖的方式
  })
}
```

### 8.4 从 mock 直接切换到服务端请求

见「[Mock Data | vue-element-admin](https://panjiachen.github.io/vue-element-admin-site/zh/guide/essentials/mock-api.html#%E4%BF%AE%E6%94%B9)」。

## 0109. Mock Data

Mock 数据是前端开发过程中必不可少的一环，是分离前后端开发的关键链路。通过预先跟服务器端约定好的接口，模拟请求数据甚至逻辑，能够让前端开发更加独立自主，不会被服务端的开发所阻塞。

### 9.1 Swagger

在公司的项目中通常使用 swagger， 由后端来模拟业务数据。 swagger 是一个 REST APIs 文档生成工具，它从代码注释中自动生成文档，可以跨平台，开源，支持大部分语言，社区好，总之非常不错，强烈推荐。 

### 9.2 Easy-Mock

vue-admin-template 之前使用的是 easy-mock 来模拟数据。 它是一个纯前端可视化，并且能快速生成模拟数据的持久化服务。非常的简单易用还能结合 swagger，天然支持跨域 ，不管团队还是个人项目都值得一试。

WARNING：现在线上版本的 vue-admin-template 已经不使用 easy-mock。因为 easy-mock 提供的线上免费服务很不稳定，时不时的就会挂掉，如果有需要的可以自己按照它的教程，搭建自己的服务。

### 9.3 Mockjs

由于 vue-element-admin 是一个纯前端个人项目，所有的数据都是用 mockjs 模拟生成。它的原理是：拦截了所有的请求并代理到本地，然后进行数据模拟，所以你会发现 network 中没有发出任何的请求。但它的最大的问题是就是它的实现机制。它会重写浏览器的 XMLHttpRequest 对象，从而才能拦截所有请求，代理到本地。大部分情况下用起来还是蛮方便的，但就因为它重写了 XMLHttpRequest 对象，所以比如 progress 方法，或者一些底层依赖 XMLHttpRequest 的库都会和它发生不兼容，可以看一下我项目的 issues，就知道多少人被坑了。

它还有一个问题是，因为是它本地模拟的数据，实际上不会走任何网络请求。所以本地调试起来很蛋疼，只能通过 console.log 来调试。就拿 vue-element-admin 来说，想搞清楚 getInfo() 接口返回了什么数据，只能通过看源码或者手动 Debug 才能知道。

### 9.4 新方案 v4.0.0+

在 v4.0 版本之后，在本地会启动一个 mock-server 来模拟数据，线上环境还是继续使用 mockjs 来进行模拟（因为本项目是一个纯前端项目，你也可以自己搭建一个线上 server 来提供数据）。不管是本地还是线上所有的数据模拟都是基于 mockjs 生成的，所以只要写一套 mock 数据，就可以在多环境中使用。

该方案的好处是，在保留 mockjs 的优势的同时，解决之前的痛点。由于我们的 mock 是完全基于 webpack-dev-serve 来实现的，所以在你启动前端服务的同时，mock-server 就会自动启动，而且这里还通过 chokidar 来观察 mock 文件夹内容的变化。在发生变化时会清除之前注册的 mock-api 接口，重新动态挂载新的接口，从而支持热更新。有兴趣的可以自己看一下代码 mock-server.js。由于是一个真正的 server，所以你可以通过控制台中的 network，清楚的知道接口返回的数据结构。并且同时解决了之前 mockjs 会重写 XMLHttpRequest 对象，导致很多第三方库失效的问题。

本项目的所有请求都是通过封装的 request.js 进行发送的，通过阅读源码可以发现所有的请求都设置了一个 baseURL，而这个 baseURL 又是通过读取 process.env.VUE_APP_BASE_API 这个环境变量来动态设置的，这样方便我们做到不同环境使用不同的 api 地址。

### 9.5 移除

如果你不想使用 mock-server 的话只要在 vue.config.js 中移除 webpack-dev-server 中 proxy 和 after 这个 Middleware 就可以了。现在默认情况下本地的请求会代理到 http://localhost:\${port}/mock 下，如果你想调整为自己的 mock 地址可以修改 proxy。

```js
proxy: {
  // change xxx-api/login => mock/login
  // detail: https://cli.vuejs.org/config/#devserver-proxy
  [process.env.VUE_APP_BASE_API]: {
    target: `http://localhost:${port}/mock`,
    changeOrigin: true,
    pathRewrite: {
      ['^' + process.env.VUE_APP_BASE_API]: ''
    }
  }
},
after: require('./mock/mock-server.js')
```

1『后期修改成自己的用户数据时，上面的知识点是关键。』

请注意：该操作需要重启服务。

mock-server 只会在开发环境中使用，线上生产环境目前使用 MockJs 进行模拟。如果不需要请移除。具体代码：main.js。

```js
import { mockXHR } from '../mock'
if (process.env.NODE_ENV === 'production') {
  mockXHR()
}
```

1『

所以后面自己数据的时候，这里的设置需删掉。顺便发现了使用中文，需要删除的 2 处设置。

```
import enLang from 'element-ui/lib/locale/lang/en'// 如果使用中文语言包请默认支持，无需额外引入，请删除该依赖

Vue.use(Element, {
  size: Cookies.get('size') || 'medium', // set element-ui default size
  locale: enLang // 如果使用中文，无需设置，请删除
})
```

』

### 9.6 新增

如果你想添加 mock 数据，只要在根目录下找到mock文件，添加对应的路由，对其进行拦截和模拟数据即可。比如我现在在 src/api/article 中需要添加一个查询某篇文章下面评论数的接口 fetchComments，首先新建接口：

```js
export function fetchComments(id) {
  return request({
    url: `/article/${id}/comments`,
    method: 'get'
  })
}
```

声明完接口之后，我们需要找到对应的 mock 文件夹 mock/article.js，在下面创建一个能拦截路由的 mock 接口。请注意，mock 拦截是基于路由来做的，请确保 mock 数据一定能匹配你的 api 保路由，支持正则。

```js
// fetchComments 的 mock
{
  // url 必须能匹配你的接口路由
  // 比如 fetchComments 对应的路由可能是 /article/1/comments 或者 /article/2/comments
  // 所以你需要通过正则来进行匹配
  url: '/article/[A-Za-z0-9]/comments',
  type: 'get', // 必须和你接口定义的类型一样
  response: (req, res) => {
    // 返回的结果
    // req and res detail see
    // https://expressjs.com/zh-cn/api.html#req
    return {
      code: 20000,
      data: {
        status: 'success'
      }
    }
  }
}
```

### 9.7 修改

最常见的操作就是：你本地模拟了了一些数据，待后端完成接口后，逐步替换掉原先 mock 的接口。我们以 src/api/role.js 中的 getRoles 接口为例。它原本是在 mock/role/index.js 中 mock 的数据。现在我们需要将它切换为真实后端数据，只要在 mock/role/index.js 找到对应的路由，之后将它删除即可。这时候你可以在 network 中，查看到真实的数据。

```js
// api 中声明的路由
export function getRoles() {
  return request({
    url: '/roles',
    method: 'get'
  })
}
```

```js
//找到对应的路由，并删除
{
    url: '/roles',
    type: 'get',
    response: _ => {
      return {
        code: 20000,
        data: roles
      }
    }
  },
```

1『这个思路好，只需要删除模拟路由即可。』
  
### 9.8 多个 server

目前项目只启动了一个mock-server，当然你也可以有自己其它的 mock-server 或者代理接口。可以一部分接口走这个服务，另一些接口走另一个服务。只需要将它们分别设置不同的的 baseURL 即可。 @/utils/request.js。之后根据设置的 url 规则在 vue.config.js 中配置多个 proxy 。相关文档「[开发中 server(devServer)](https://webpack.docschina.org/configuration/dev-server/#devserver-proxy)」。

1『关键知识点，代理是在「vue.config.js」里设置的。』

### 9.9 启用纯前端 Mock

现在在 mock/index.js 也封装了一个纯前端 mock 的方法，你只需要在 src/main.js 中：

```js
import { mockXHR } from '../mock'
mockXHR()
```

这样就会变成纯前端 mock 数据了和 v4.0 版本之前的 mock 方案是一样的，原理见上文。目前你看到的线上 demo 就是采用该种方式。

### 9.10 本地 Mock 数据与线上数据切换

有很多时候我们会遇到本地使用 mock 数据，线上环境使用真实数据，或者说不同环境使用不同的数据。

#### 9.10.1 Easy-Mock 的形式

你需要保证你本地模拟 api 除了根路径其它的地址是一致的。 比如：

```
https://api-dev/login   // 本地请求
https://api-prod/login  // 线上请求
```

我们可以通过之后会介绍的环境变量来做到不同环境下，请求不同的 api 地址。

```
# .env.development
VUE_APP_BASE_API = '/dev-api' #注入本地 api 的根路径
# .env.production
VUE_APP_BASE_API = '/prod-api' #注入线上 api 的根路径
```

之后根据环境变量创建 axios 实例，让它具有不同的 baseURL。 @/utils/request.js

```js
// create an axios instance
const service = axios.create({
  baseURL: process.env.BASE_API, // api 的 base_url
  timeout: 5000 // request timeout
})
```

这样我们就做到了自动根据环境变量切换本地和线上 api。

### 9.11 Mock.js 的切换

当我们本地使用 Mock.js 模拟本地数据，线上使用真实环境 api 方法。这与上面的 easy-mock 的方法是差不多的。我们主要是判断：是线上环境的时候，不引入 mock 数据就可以了，只有在本地引入 Mock.js。

```js
// main.js
// 通过环境变量来判断是否需要加载启用
if (process.env.NODE_ENV === 'development') {
  require('./mock') // simulation data
}
```

只有在本地环境之中才会引入 mock 数据。

## 0110. 引入外部模块

除了 element-ui 组件以及脚手架内置的业务组件，有时我们还需要引入其他外部组件，这里以引入 vue-count-to 为例进行介绍。

### 10.1 引入依赖

在终端输入下面的命令完成安装：

```
$ npm install vue-count-to --save
```

加上 --save 参数会自动添加依赖到 package.json 中去。

### 10.2 使用

#### 10.2.1 全局注册

main.js

```html
import countTo from 'vue-count-to'
Vue.component('countTo', countTo)
<template>
  <countTo :startVal='startVal' :endVal='endVal' :duration='3000'></countTo>
</template>
```

#### 10.2.2 局部注册

```html
<template>
  <countTo :startVal='startVal' :endVal='endVal' :duration='3000'></countTo>
</template>

<script>
import countTo from 'vue-count-to';
export default {
  components: { countTo },
  data () {
    return {
      startVal: 0,
      endVal: 2017
    }
  }
}
</script>
```

### 10.3 在 vue 中优雅的使用第三方库

在 Vuejs 项目中使用 JavaScript 库的一个优雅方式是将其代理到 Vue 的原型对象上去。按照这种方式，我们引入 Moment 库:

main.js

```js
import moment from 'moment'
Object.defineProperty(Vue.prototype, '$moment', { value: moment })
```

由于所有的组件都会从 Vue 的原型对象上继承它们的方法，因此在所有组件/实例中都可以通过 this.\$moment: 的方式访问 Moment 而不需要定义全局变量或者手动的引入。

1『这个实现太赞了，又一次体验到 JS 基于原型面向对象的强大之处。』

MyNewComponent.vue

```js
export default {
  created() {
    console.log('The time is '.this.$moment().format('HH:mm'))
  }
}
```

在诸多 Vue.js 应用中，Lodash、Moment、Axios、Async 等都是一些非常有用的 JavaScript 库。但随着项目越来越复杂，可能会采取组件化和模块化的方式来组织代码，还可能要使应用支持不同环境下的服务端渲染。除非你找到了一个简单而又健壮的方式来引入这些库供不同的组件和模块使用，不然，这些第三方库的管理会给你带来一些麻烦。这里来介绍一下 Vue.js 中使用第三方库的方式详情见该 blog「[如何在 Vue.js 中使用第三方库 · Issue #51 · dwqs/blog](https://github.com/dwqs/blog/issues/51)」。

### 10.4 自己封装一个非 vue 组件

很多时候我们会发现，有些组件并没有 vue 版本，其实在 vue 中引入第三方组件是很简单的。只要在合适的生命周期里面初始化它就好了。一般在 mounted 中，之后和正常使用它就没什么区别了。详细的可见文章：[手摸手，带你封装一个 vue component](https://segmentfault.com/a/1190000009090836)。

## 0111. 构建和发布

### 11.1 构建

当项目开发完毕，只需要运行一行命令就可以打包你的应用：

```
# 打包正式环境
npm run build:prod

# 打包预发布环境
npm run build:stage
```

构建打包成功之后，会在根目录生成 dist 文件夹，里面就是构建打包好的文件，通常是 \*\*\*.js 、\*\*\*.css、index.html 等静态文件。如果需要自定义构建，比如指定 dist 目录等，则需要通过 config「[vue-element-admin/vue.config.js at master](https://github.com/PanJiaChen/vue-element-admin/blob/master/vue.config.js)」的 outputDir 进行配置。

### 11.2 环境变量

所有测试环境或者正式环境变量的配置都在 .env.development 等 .env.xxxx 文件中。它们都会通过 webpack.DefinePlugin 插件注入到全局。

注意！！！环境变量必须以 VUE\_APP\_为开头。如：VUE\_APP\_API、VUE\_APP\_TITLE。你在代码中可以通过如下方式获取:

```js
console.log(process.env.VUE_APP_xxxx)
```

### 11.3 分析构建文件体积

如果你的构建文件很大，你可以通过 webpack-bundle-analyzer 命令构建并分析依赖模块的体积分布，从而优化你的代码。

```
npm run preview -- --report
```

运行之后你就可以在 http://localhost:9526/report.html 页面看到具体的体积分布

具体的优化可以参考 Webpack 大法之 Code Splitting「[Webpack 大法之 Code Splitting - 知乎](https://zhuanlan.zhihu.com/p/26710831)」。

TIP：强烈建议开启 gzip ，使用之后普遍体积只有原先 1/3 左右。打出来的 app.js 过大，查看一下是不是 Uglify 配置不正确或者 sourceMap 没弄对。 优化相关请看该 Webpack Freestyle 之 Long Term Cache「[Webpack Freestyle 之 Long Term Cache - 知乎](https://zhuanlan.zhihu.com/p/27710902)」。

### 11.4 发布

对于发布来讲，只需要将最终生成的静态文件，也就是通常情况下 dist 文件夹的静态文件发布到你的 cdn 或者静态服务器即可，需要注意的是其中的 index.html 通常会是你后台服务的入口页面，在确定了 js 和 css 的静态之后可能需要改变页面的引入路径。

TIP：部署时可能会发现资源路径不对，只需修改 vue.config.js 文件资源路径即可。

```
publicPath: './' //请根据自己路径来配置更改
```

### 11.5 前端路由与服务端的结合

vue-element-admin 中，前端路由使用的是 vue-router，所以你可以选择两种方式：browserHistory 和 hashHistory。

两者的区别简单来说是对路由方式的处理不一样，hashHistory 是以 # 后面的路径进行处理，通过 HTML 5 History 进行前端路由管理，而 browserHistory 则是类似我们通常的页面访问路径，并没有 #，但要通过服务端的配置，能够访问指定的 url 都定向到当前页面，从而能够进行前端的路由管理。本项目默认使用的是 hashHistory ，所以如果你的 url 里有 #，想去掉的话，需要切换为 browserHistory。 修改 src/router/index.js 中的 mode 即可。

1『也使用 hashHistory，这样不用去后端设置了。』

```js
export default new Router({
  // mode: 'history', //后端支持可开
})
```

如果你使用的是静态站点，那么使用 browserHistory 可能会无法访问你的应用，因为假设你访问 http://localhost:9527/dashboard，那么其实你的静态服务器并没有能够映射的文件，而使用 hashHistory 则不会有这个问题，因为它的页面路径是以 # 开始的，所有访问都在前端完成，如：http://localhost:9527/#/dashboard/。不过如果你有对应的后台服务器，那么我们推荐采用 browserHistory，只需要在服务端做一个映射，比如：

Apache

```
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```

nginx

```
location / {
  try_files $uri $uri/ /index.html;
}
```

TIP：更多配置请查看 vue-router 文档「[HTML5 History 模式 | Vue Router](https://router.vuejs.org/zh/guide/essentials/history-mode.html)」。

### 11.6 Apache

1、需要修改 router/index.js 中 new Router 配置，加一个 base: '/vue/'，它指定应用的基路径，该应用是服务于 localhost/vue 路径下，所以必须加 base 配置，否则应用会展示 404 页面。

2、需要修改 config/index.js 中 build 下的 assetsPublicPath: '/vue/'，如果用相对路径，chunk 文件会报错找不到。

3、修改 httpd.conf 文件，开启 rewrite_module 功能。

LoadModule rewrite\_module libexec/apache2/mod\_rewrite.so，去掉前面的 #。然后找到 AllowOverride None 的那行，把它改成 AllowOverride All，来使 .htaccess 文件生效。

4、在 apache 的 www/vue 目录下新建 .htaccess 文件, 需要修改 RewriteRule 为 /vue/index.html，否则刷新页面服务端会直接报 404 错误。

.htaccess 文件内容

```
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /vue/index.html [L]
</IfModule>
```

相关 issue「[将项目打包后发布到apache的www下的vue子目录 · Issue #370 · PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/issues/370)」。

## 0112. 环境变量

vue-element-admin 4.0 之后是基于 vue-cli 来进行构建，所以所有的环境变量配置都是基于 vue-cli 来实现和控制的。

官方文档「[环境变量和模式 | Vue CLI](https://cli.vuejs.org/zh/guide/mode-and-env.html)」。

```
.env                # 在所有的环境中被载入
.env.[mode]         # 只在指定的模式中被载入
```

一个环境文件只包含环境变量的“键=值”对：

```
FOO=bar
VUE_APP_SECRET=secret
```

注意！！！环境变量必须以 VUE\_APP\_ 为开头。如：VUE\_APP\_API、VUE\_APP\_TITLE。你在代码中可以通过如下方式获取:

```
console.log(process.env.VUE_APP_xxxx)
```

除了 VUE\_APP\_*  变量之外，在你的应用代码中始终可用的还有两个特殊的变量：

1、NODE_ENV - 会是 "development"、"production" 或 "test" 中的一个。具体的值取决于应用运行的模式。

2、BASE_URL - 会和 vue.config.js 中的 publicPath 选项相符，即你的应用会部署到的基础路径。

### 12.1 构建相关

除了一些写在 .env 的环境变量之外，还有一些构建和部署相关的变量都是需要在 vue.config.js 中配置的。你可以通过 process.env.NODE_ENV 来执行判断环境，来设置不同的参数。具体代码可借鉴 vue.config.js。









