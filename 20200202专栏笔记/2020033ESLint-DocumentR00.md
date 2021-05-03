## 记忆时间

## 卡片

### 0101. 主题卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡——

### 0301. 信息数据卡——

### 0401. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 个人配置

1、规则收集。

```json
    "rules": {
        "space-before-function-paren": ["warn", "never"],
        'semi': ["warn", 'never'],
        "no-unused-vars": ["warn", { "vars": "all", "args": "after-used", "ignoreRestSiblings": false }]
    }
```

2、忽略文件设置。

在根目录下新建 `.eslintignore` 文件，里面设置不检测语法的文件。

```
dist/assets/
sample.js
```

## 问题汇总

1、react 开发时，eslint 报错：

```
'value' is missing in props validation  react/prop-types
```

解决方法：禁用检测这条语法。

[reactjs - How to disable ESLint react/prop-types rule in a file? - Stack Overflow](https://stackoverflow.com/questions/30948970/how-to-disable-eslint-react-prop-types-rule-in-a-file)

Just put this on top of your file:

```
/* eslint-disable react/prop-types */
```

2、跑的时候报错，说找不到 react 的版本号。

```
React version not specified in eslint-plugin-react settings
```

[[7.12.4]React version not specified in eslint-plugin-react settings · Issue #2157 · yannickcr/eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react/issues/2157)

只需要在 .eslintrc.js 添加设置：

```json
    "settings": {
        "react": {
          "version": "detect"
        }
      }
```

## 0101. Getting Started with ESLint

[ESLint - Pluggable JavaScript linter](https://eslint.org/)

[Getting Started with ESLint - ESLint - Pluggable JavaScript linter](https://eslint.org/docs/user-guide/getting-started)

ESLint is a tool for identifying and reporting on patterns found in ECMAScript/JavaScript code, with the goal of making code more consistent and avoiding bugs. In many ways, it is similar to JSLint and JSHint with a few exceptions: 1) ESLint uses Espree for JavaScript parsing. 2) ESLint uses an AST to evaluate patterns in code. 3) ESLint is completely pluggable, every single rule is a plugin and you can add more at runtime.

1『

从墨菲那边学到，直接跑一下命令即可，前提要设置里先设置好（2020-09-14）。

```
npm run lint
```

补充：为啥这里用的是 `lint`，因为是墨菲自己设置的脚本命令（2021-04-16）。

```
  "scripts": {
    "dev": "vue-cli-service serve",
    "build:prod": "vue-cli-service build",
    "build:stage": "vue-cli-service build --mode staging",
    "preview": "node build/index.js --preview",
    "lint": "eslint --fix --ext .js,.vue src/views",
    "svgo": "svgo -f src/icons/svg --config=src/icons/svgo.yml",
    "new": "plop"
  }
```

』

### 1.1 Installation and Usage

Prerequisites: Node.js (`^10.12.0, or >=12.0.0`) built with SSL support. (If you are using an official Node.js distribution, SSL is always built in.) You can install ESLint using npm or yarn:

```
npm install eslint --save-dev

# or

yarn add eslint --dev
```

You should then set up a configuration file:

```
$ npx eslint --init

# or

$ yarn run eslint --init
```

After that, you can run ESLint on any file or directory like this:

```
$ npx eslint yourfile.js

# or

$ yarn run eslint yourfile.js
```

It is also possible to install ESLint globally rather than locally (using npm install eslint --global). However, this is not recommended, and any plugins or shareable configs that you use must be installed locally in either case.

### 1.2 Configuration

Note: If you are coming from a version before 1.0.0 please see the migration guide.

After running eslint --init, you'll have a .eslintrc.{js,yml,json} file in your directory. In it, you'll see some rules configured like this:

```json
{
    "rules": {
        "semi": ["error", "always"],
        "quotes": ["error", "double"]
    }
}
```

The names "semi" and "quotes" are the names of rules in ESLint. The first value is the error level of the rule and can be one of these values:

```
"off" or 0 - turn the rule off
"warn" or 1 - turn the rule on as a warning (doesn't affect exit code)
"error" or 2 - turn the rule on as an error (exit code will be 1)
```

The three error levels allow you fine-grained control over how ESLint applies rules (for more configuration options and details, see the configuration docs). 

Your .eslintrc.{js,yml,json} configuration file will also include the line:

```json
{
    "extends": "eslint:recommended"
}
```

Because of this line, all of the rules marked "√" on the rules page will be turned on. Alternatively, you can use configurations that others have created by searching for "eslint-config" on npmjs.com. ESLint will not lint your code unless you extend from a shared configuration or explicitly turn rules on in your configuration.

### 1.3 Next Steps

Learn about advanced configuration of ESLint.——[Configuring ESLint - ESLint - Pluggable JavaScript linter](https://eslint.org/docs/user-guide/configuring)

Get familiar with the command line options.——[Command Line Interface - ESLint - Pluggable JavaScript linter](https://eslint.org/docs/user-guide/command-line-interface)

Explore ESLint integrations into other tools like editors, build systems, and more.——[Integrations - ESLint - Pluggable JavaScript linter](https://eslint.org/docs/user-guide/integrations)

Can't find just the right rule? Make your own custom rule.——[Working with Rules - ESLint - Pluggable JavaScript linter](https://eslint.org/docs/developer-guide/working-with-rules)

Make ESLint even better by contributing.——[Contributing - ESLint - Pluggable JavaScript linter](https://eslint.org/docs/developer-guide/contributing/)