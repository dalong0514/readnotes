## 记忆时间

## 卡片

### 0101. 主题卡 —— 创建一个 react 项目

信息源自「0101Tutorial-Intro-to-React.md」

```
npx create-react-app my-app
```

或者

```
yarn create react-app my-app
```

个人更建议用 yarn 来生成项目。

把系统默认生成的 app.js、app.css 都删掉，值保留 index.js、index.css。

index.js

```js
import React from 'react'
import ReactDOM from 'react-dom'
import './index.css'
import { Button } from 'antd'

class Game extends React.Component {
  testFun() {
    console.log('dalong')
  }

  render() {
    return (
      <div>
        <Button type="primary" onClick={this.testFun}>测试按钮</Button>
      </div>
    )
  }
}

ReactDOM.render(
  <Game />,
  document.getElementById('root')
)
```

2、安装 eslint。

```
yarn add eslint --dev

yarn run eslint --init
```

个人配置：

```json
    "rules": {
        "space-before-function-paren": ["warn", "never"],
        'semi': ["warn", 'never'],
        "no-unused-vars": ["warn", { "vars": "all", "args": "after-used", "ignoreRestSiblings": false }]
    }
```

3、安装 ant Design。

```
yarn add antd
```

安装完发现 ant design 的样式无法生效，后来发现样式没引入，在 index.css 里最开始加上:

```
@import '~antd/dist/antd.css';
```

### 0201. 术语卡 ——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 数据信息卡 —— react 里约定俗成的时间监听和事件处理函数命名原则

Note: The DOM `<button>` element's onClick attribute has a special meaning to React because it is a built-in component. For custom components like Square, the naming is up to you. We could give any name to the Square's onClick prop or Board's handleClick method, and the code would work the same. In React, it's conventional to use on[Event] names for props which represent events and handle[Event] for the methods which handle the events.

1-2『 react 里约定俗成的时间监听和事件处理函数命名原则，做一张信息数据卡片。（2021-04-29）』

注意：因为 DOM 元素 `<button>` 是一个内置组件，因此其 onClick 属性在 React 中有特殊的含义。而对于用户自定义的组件来说，命名就可以由用户自己来定义了。我们给 Square 的 onClick 和 Board 的 handleClick 赋予任意的名称，代码依旧有效。在 React 中，有一个命名规范，通常会将代表事件的监听 prop 命名为 `on[Event]`，将处理事件的监听方法命名为 `handle[Event]` 这样的格式。

### 0401. 任意卡 ——

最后还有一张任意卡，记录个人阅读感想。

