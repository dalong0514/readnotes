## 记忆时间

## 卡片

### 0101.  主题卡 ——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡 ——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0301. 术语卡 —— 信息数据卡

### 0301. 任意卡 ——

最后还有一张任意卡，记录个人阅读感想。

## 目录

0101Introduction.md

0102Using-Matchers.md

## 0101Introduction.md

[Getting Started · Jest](https://jestjs.io/docs/en/getting-started)

### 1.1 Getting Started

Install Jest using yarn:

```
yarn add --dev jest
```

Or npm:

```
npm install --save-dev jest
```

Note: Jest documentation uses yarn commands, but npm will also work. You can compare yarn and npm commands in the yarn docs, here. Let's get started by writing a test for a hypothetical function that adds two numbers. First, create a sum.js file:

```js
function sum(a, b) {
  return a + b;
}

module.exports = sum;
```

Then, create a file named sum.test.js. This will contain our actual test:

```js
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

Add the following section to your package.json:

```js
{
  "scripts": {
    "test": "jest"
  }
}
```

Finally, run yarn test or npm run test and Jest will print this message:

```
PASS  ./sum.test.js
✓ adds 1 + 2 to equal 3 (5ms)
```

You just successfully wrote your first test using Jest! This test used expect and toBe to test that two values were exactly identical. To learn about the other things that Jest can test, see Using Matchers.

### 1.2 Running from command line

You can run Jest directly from the CLI (if it's globally available in your PATH, e.g. by yarn global add jest or npm install jest --global) with a variety of useful options. Here's how to run Jest on files matching my-test, using config.json as a configuration file and display a native OS notification after the run:

```
jest my-test --notify --config=config.json
```

If you'd like to learn more about running jest through the command line, take a look at the Jest CLI Options page.

### 1.3 Additional Configuration

Generate a basic configuration file. Based on your project, Jest will ask you a few questions and will create a basic configuration file with a short description for each option:

```
jest --init
```

Using Babel. To use Babel, install required dependencies via yarn:

```
yarn add --dev babel-jest @babel/core @babel/preset-env
```

Configure Babel to target your current version of Node by creating a babel.config.js file in the root of your project:

```js
// babel.config.js
module.exports = {
  presets: [
    [
      '@babel/preset-env',
      {
        targets: {
          node: 'current',
        },
      },
    ],
  ],
};
```

The ideal configuration for Babel will depend on your project. See Babel's docs for more details.

Making your Babel config jest-aware.

Babel 6 support.

Using webpack. Jest can be used in projects that use webpack to manage assets, styles, and compilation. webpack does offer some unique challenges over other tools. Refer to the webpack guide to get started.

Using parcel. Jest can be used in projects that use parcel-bundler to manage assets, styles, and compilation similar to webpack. Parcel requires zero configuration. Refer to the official docs to get started.

Using TypeScript. Jest supports TypeScript, via Babel. First, make sure you followed the instructions on using Babel above. Next, install the @babel/preset-typescript via yarn:

```
yarn add --dev @babel/preset-typescript
```

Then add @babel/preset-typescript to the list of presets in your babel.config.js.

```js
// babel.config.js
module.exports = {
  presets: [
    ['@babel/preset-env', {targets: {node: 'current'}}],
+    '@babel/preset-typescript',
  ],
};
```

However, there are some caveats to using TypeScript with Babel. Because TypeScript support in Babel is transpilation, Jest will not type-check your tests as they are run. If you want that, you can use ts-jest.

## 0102Using-Matchers.md

Jest uses "matchers" to let you test values in different ways. This document will introduce some commonly used matchers. For the full list, see the expect API doc ([Expect · Jest](https://jestjs.io/docs/en/expect)).

### 2.1 Common Matchers

The simplest way to test a value is with exact equality.

```js
test('two plus two is four', () => {
  expect(2 + 2).toBe(4);
});
```

In this code, `expect(2 + 2)` returns an "expectation" object. You typically won't do much with these expectation objects except call matchers on them. In this code, `.toBe(4)` is the matcher. When Jest runs, it tracks all the failing matchers so that it can print out nice error messages for you.

toBe uses Object.is to test exact equality. If you want to check the value of an object, use toEqual instead:

```js
test('object assignment', () => {
  const data = {one: 1};
  data['two'] = 2;
  expect(data).toEqual({one: 1, two: 2});
});
```

1『

这里注意啊，expect 就一个参数 data，之前自己码的时候把后面的箭头函数也当作参数传进去了。

```js
test('object assignment', () => {
  const data = { one: 1 }
  data.two = 2
  expect(data).toEqual({
    one: 1,
    two: 2
  })
})
```

』

toEqual recursively checks every field of an object or array. You can also test for the opposite of a matcher:

```js
test('adding positive numbers is not zero', () => {
  for (let a = 1; a < 10; a++) {
    for (let b = 1; b < 10; b++) {
      expect(a + b).not.toBe(0);
    }
  }
});
```

### 2.2 Truthiness

In tests, you sometimes need to distinguish between undefined, null, and false, but you sometimes do not want to treat these differently. Jest contains helpers that let you be explicit about what you want.

```
toBeNull matches only null
toBeUndefined matches only undefined
toBeDefined is the opposite of toBeUndefined
toBeTruthy matches anything that an if statement treats as true
toBeFalsy matches anything that an if statement treats as false
```

For example:

```js
test('null', () => {
  const n = null;
  expect(n).toBeNull();
  expect(n).toBeDefined();
  expect(n).not.toBeUndefined();
  expect(n).not.toBeTruthy();
  expect(n).toBeFalsy();
});

test('zero', () => {
  const z = 0;
  expect(z).not.toBeNull();
  expect(z).toBeDefined();
  expect(z).not.toBeUndefined();
  expect(z).not.toBeTruthy();
  expect(z).toBeFalsy();
});
```

You should use the matcher that most precisely corresponds to what you want your code to be doing.

### 2.3 Numbers

Most ways of comparing numbers have matcher equivalents.

```js
test('two plus two', () => {
  const value = 2 + 2;
  expect(value).toBeGreaterThan(3);
  expect(value).toBeGreaterThanOrEqual(3.5);
  expect(value).toBeLessThan(5);
  expect(value).toBeLessThanOrEqual(4.5);

  // toBe and toEqual are equivalent for numbers
  expect(value).toBe(4);
  expect(value).toEqual(4);
});
```

For floating point equality, use toBeCloseTo instead of toEqual, because you don't want a test to depend on a tiny rounding error.

```js
test('adding floating point numbers', () => {
  const value = 0.1 + 0.2;
  //expect(value).toBe(0.3);           This won't work because of rounding error
  expect(value).toBeCloseTo(0.3); // This works.
});
```

### 2.4 Strings

You can check strings against regular expressions with toMatch:

```js
test('there is no I in team', () => {
  expect('team').not.toMatch(/I/);
});

test('but there is a "stop" in Christoph', () => {
  expect('Christoph').toMatch(/stop/);
});
```

### 2.5 Arrays and iterables

You can check if an array or iterable contains a particular item using toContain:

```js
const shoppingList = [
  'diapers',
  'kleenex',
  'trash bags',
  'paper towels',
  'beer',
];

test('the shopping list has beer on it', () => {
  expect(shoppingList).toContain('beer');
  expect(new Set(shoppingList)).toContain('beer');
});
```

### 2.6 Exceptions

If you want to test whether a particular function throws an error when it's called, use toThrow.

```js
function compileAndroidCode() {
  throw new Error('you are using the wrong JDK');
}

test('compiling android goes as expected', () => {
  expect(compileAndroidCode).toThrow();
  expect(compileAndroidCode).toThrow(Error);

  // You can also use the exact error message or a regexp
  expect(compileAndroidCode).toThrow('you are using the wrong JDK');
  expect(compileAndroidCode).toThrow(/JDK/);
});
```

### 2.7 And More

This is just a taste. For a complete list of matchers, check out the reference docs.

Once you've learned about the matchers that are available, a good next step is to check out how Jest lets you test asynchronous code.