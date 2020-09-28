## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。找一个他的 TED 演讲，有的话。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

### 0601. 行动卡——

行动卡是能够指导自己的行动的卡。

## 目录

0101Array.prototype.sort.md

0102Array.prototype.reduce.md

## 0101Array.prototype.sort.md

[Array.prototype.sort() - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

sort() 方法用原地算法对数组的元素进行排序，并返回数组。默认排序顺序是在将元素转换为字符串，然后比较它们的 UTF-16 代码单元值序列时构建的。由于它取决于具体实现，因此无法保证排序的时间和空间复杂性。

```js
const months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// expected output: Array ["Dec", "Feb", "Jan", "March"]

const array1 = [1, 30, 4, 21, 100000];
array1.sort();
console.log(array1);
// expected output: Array [1, 100000, 21, 30, 4]
```

### 01. 语法

```js
arr.sort([compareFunction])
```

#### 1.1 参数

compareFunction，可选，用来指定按某种顺序进行排列的函数。如果省略，元素按照转换为的字符串的各个字符的 Unicode 位点进行排序。

firstEl，第一个用于比较的元素。secondEl，第二个用于比较的元素。

#### 1.2 返回值

排序后的数组。请注意，数组已原地排序，并且不进行复制。

### 02. 描述

如果没有指明 compareFunction ，那么元素会按照转换为的字符串的诸个字符的 Unicode 位点进行排序。例如 "Banana" 会被排列到 "cherry" 之前。当数字按由小到大排序时，9 出现在 80 之前，但因为（没有指明 compareFunction），比较的数字会先被转换为字符串，所以在Unicode顺序上 "80" 要比 "9" 要靠前。

如果指明了 compareFunction ，那么数组会按照调用该函数的返回值排序。即 a 和 b 是两个将要被比较的元素：1）如果 compareFunction(a, b) 小于 0 ，那么 a 会被排列到 b 之前；2）如果 compareFunction(a, b) 等于 0 ， a 和 b 的相对位置不变。备注： ECMAScript 标准并不保证这一行为，而且也不是所有浏览器都会遵守（例如 Mozilla 在 2003 年之前的版本）；3）如果 compareFunction(a, b) 大于 0 ， b 会被排列到 a 之前。4）compareFunction(a, b) 必须总是对相同的输入返回相同的比较结果，否则排序的结果将是不确定的。所以，比较函数格式如下：

```js
function compare(a, b) {
  if (a < b ) {           // 按某种排序标准进行比较, a 小于 b
    return -1;
  }
  if (a > b ) {
    return 1;
  }
  // a must be equal to b
  return 0;
}
```

要比较数字而非字符串，比较函数可以简单的以 a 减 b，如下的函数将会将数组升序排列：

```js
function compareNumbers(a, b) {
  return a - b;
}
```

sort 方法可以使用「函数表达式」方便地书写：

```js
var numbers = [4, 2, 5, 1, 3];
numbers.sort(function(a, b) {
  return a - b;
});
console.log(numbers);
```

也可以写成：

```js
var numbers = [4, 2, 5, 1, 3]; 
numbers.sort((a, b) => a - b); 
console.log(numbers);

// [1, 2, 3, 4, 5]
```

对象可以按照某个属性排序：

```js
var items = [
  { name: 'Edward', value: 21 },
  { name: 'Sharpe', value: 37 },
  { name: 'And', value: 45 },
  { name: 'The', value: -12 },
  { name: 'Magnetic' },
  { name: 'Zeros', value: 37 }
];

// sort by value
items.sort(function (a, b) {
  return (a.value - b.value)
});

// sort by name
items.sort(function(a, b) {
  var nameA = a.name.toUpperCase(); // ignore upper and lowercase
  var nameB = b.name.toUpperCase(); // ignore upper and lowercase
  if (nameA < nameB) {
    return -1;
  }
  if (nameA > nameB) {
    return 1;
  }

  
// names must be equal

  return 0;
});
```

### 03. 示例

#### 3.1 创建、显示及排序数组

下述示例创建了四个数组，并展示原数组。之后对数组进行排序。对比了数字数组分别指定与不指定比较函数的结果。

```js
var stringArray = ["Blue", "Humpback", "Beluga"];
var numericStringArray = ["80", "9", "700"];
var numberArray = [40, 1, 5, 200];
var mixedNumericArray = ["80", "9", "700", 40, 1, 5, 200];

function compareNumbers(a, b)
{
  return a - b;
}

console.log('stringArray:' + stringArray.join());
console.log('Sorted:' + stringArray.sort());

console.log('numberArray:' + numberArray.join());
console.log('Sorted without a compare function:'+ numberArray.sort());
console.log('Sorted with compareNumbers:'+ numberArray.sort(compareNumbers));

console.log('numericStringArray:'+ numericStringArray.join());
console.log('Sorted without a compare function:'+ numericStringArray.sort());
console.log('Sorted with compareNumbers:'+ numericStringArray.sort(compareNumbers));

console.log('mixedNumericArray:'+ mixedNumericArray.join());
console.log('Sorted without a compare function:'+ mixedNumericArray.sort());
console.log('Sorted with compareNumbers:'+ mixedNumericArray.sort(compareNumbers));
```

该示例的返回结果如下。输出显示，当使用比较函数后，数字数组会按照数字大小排序。

```js
stringArray: Blue,Humpback,Beluga
Sorted: Beluga,Blue,Humpback

numberArray: 40,1,5,200
Sorted without a compare function: 1,200,40,5
Sorted with compareNumbers: 1,5,40,200

numericStringArray: 80,9,700
Sorted without a compare function: 700,80,9
Sorted with compareNumbers: 9,80,700

mixedNumericArray: 80,9,700,40,1,5,200
Sorted without a compare function: 1,200,40,5,700,80,9
Sorted with compareNumbers: 1,5,9,40,80,200,700
```

#### 3.2 对非 ASCII 字符排序

当排序非 ASCII 字符的字符串（如包含类似 e, é, è, a, ä 等字符的字符串）。一些非英语语言的字符串需要使用 String.localeCompare。这个函数可以将函数排序到正确的顺序。

```js
var items = ['réservé', 'premier', 'cliché', 'communiqué', 'café', 'adieu'];
items.sort(function (a, b) {
  return a.localeCompare(b);
});

// items is ['adieu', 'café', 'cliché', 'communiqué', 'premier', 'réservé']
```

#### 3.3 使用映射改善排序

compareFunction 可能需要对元素做多次映射以实现排序，尤其当 compareFunction 较为复杂，且元素较多的时候，某些 compareFunction 可能会导致很高的负载。使用 map 辅助排序将会是一个好主意。基本思想是首先将数组中的每个元素比较的实际值取出来，排序后再将数组恢复。

1『这个思路很好，先把要排序的数据抽出来，拍完序再放回去。』

```js
// 需要被排序的数组
var list = ['Delta', 'alpha', 'CHARLIE', 'bravo'];

// 对需要排序的数字和位置的临时存储
var mapped = list.map(function(el, i) {
  return { index: i, value: el.toLowerCase() };
})

// 按照多个值排序数组
mapped.sort(function(a, b) {
  return +(a.value > b.value) || +(a.value === b.value) - 1;
});

// 根据索引得到排序的结果
var result = mapped.map(function(el){
  return list[el.index];
});
```

### 04. 应用场景收集

#### 4.1 

数据流开发，cad 确认页面，按房间号进行排序数组中的数据。因房间号正好都是 101、102、103、201、202 之类的字符串，跟数字对应着的，所以直接用数值型的排序方式。

```js
// 初始化数据
getCadata(response) {
  if (response.status.code === 0) {
    this.roomData = response.data.room.sort((a, b) => {
      return (a.room_num - b.room_num);
    });
    this.substanceData = response.data.substance.sort((a, b) => {
      return (a.room_num - b.room_num);
    });
    this.equipmentData = response.data.equipment.sort((a, b) => {
      return (a.room_num - b.room_num);
    });
    this.uploadStatus = false;
    this.confirmStatus = true;
    this.getProjectId();
  } else console.log(response);
},
```

## 0102Array.prototype.reduce.md

[Array.prototype.reduce() - JavaScript | MDN](https://wiki.developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

reduce() 方法对数组中的每个元素执行一个由您提供的 reducer 函数（升序执行），将其结果汇总为单个返回值。

```js
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```

### 01. 语法

```js
arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])
```

reducer 函数接收 4 个参数：`Accumulator (acc)`（累计器）、`Current Value (cur)`（当前值）、`Current Index (idx)`（当前索引）、`Source Array (src)`（源数组）。您的 reducer 函数的返回值分配给累计器，该返回值在数组的每个迭代中被记住，并最后成为最终的单个结果值。

返回值：函数累计处理的结果。

### 02. 描述

reduce 为数组中的每一个元素依次执行callback函数，不包括数组中被删除或从未被赋值的元素。

回调函数第一次执行时，accumulator 和 currentValue 的取值有两种情况：如果调用 `reduce()` 时提供了 initialValue，accumulator 取值为 initialValue，currentValue 取数组中的第一个值；如果没有提供 initialValue，那么 accumulator 取数组中的第一个值，currentValue 取数组中的第二个值。注意：如果没有提供 initialValue，reduce 会从索引 1 的地方开始执行 callback 方法，跳过第一个索引。如果提供 initialValue，从索引 0 开始。

如果数组为空且没有提供 initialValue，会抛出 TypeError 。如果数组仅有一个元素（无论位置如何）并且没有提供 initialValue， 或者有提供 initialValue 但是数组为空，那么此唯一值将被返回并且 callback 不会被执行。提供初始值通常更安全，正如下面的例子，如果没有提供 initialValue，则可能有四种输出：

```js
var maxCallback = ( acc, cur ) => Math.max( acc.x, cur.x );
var maxCallback2 = ( max, cur ) => Math.max( max, cur );

// reduce() 没有初始值
[ { x: 2 }, { x: 22 }, { x: 42 } ].reduce( maxCallback ); // NaN
[ { x: 2 }, { x: 22 }            ].reduce( maxCallback ); // 22
[ { x: 2 }                       ].reduce( maxCallback ); // { x: 2 }
[                                ].reduce( maxCallback ); // TypeError

// map/reduce; 这是更好的方案，即使传入空数组或更大数组也可正常执行
[ { x: 22 }, { x: 42 } ].map( el => el.x )
                        .reduce( maxCallback2, -Infinity );
```

后面有很多例子，值得仔细研读。一个意外收获（数组去重）：如果你正在使用一个可以兼容 Set 和 Array.from() 的环境， 你可以使用 `let orderedArray = Array.from(new Set(myArray));` 来获得一个相同元素被移除的数组。这是收集到的数组去重第二个方法，第一个是用 Set() 后再用 `...` 运算符转会为数组。

### 03. 示例

#### 3.1 数组里所有值的和

```js
var sum = [0, 1, 2, 3].reduce(function (accumulator, currentValue) {
  return accumulator + currentValue;
}, 0);
// 和为 6
```

你也可以写成箭头函数的形式：

```js
var total = [ 0, 1, 2, 3 ].reduce(
  ( acc, cur ) => acc + cur,
  0
);
```

#### 3.2 累加对象数组里的值

要累加对象数组中包含的值，必须提供初始值，以便各个 item 正确通过你的函数。

```js
var initialValue = 0;
var sum = [{x: 1}, {x:2}, {x:3}].reduce(function (accumulator, currentValue) {
    return accumulator + currentValue.x;
},initialValue)

console.log(sum) // logs 6
```

你也可以写成箭头函数的形式：

```js
var initialValue = 0;
var sum = [{x: 1}, {x:2}, {x:3}].reduce(
    (accumulator, currentValue) => accumulator + currentValue.x
    ,initialValue
);

console.log(sum) // logs 6
```

#### 3.3 将二维数组转化为一维

```js
var flattened = [[0, 1], [2, 3], [4, 5]].reduce(
  function(a, b) {
    return a.concat(b);
  },
  []
);
// flattened is [0, 1, 2, 3, 4, 5]
```

你也可以写成箭头函数的形式：

```
var flattened = [[0, 1], [2, 3], [4, 5]].reduce(
 ( acc, cur ) => acc.concat(cur),
 []
);
```

#### 3.4 计算数组中每个元素出现的次数

```js
var names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];

var countedNames = names.reduce(function (allNames, name) { 
  if (name in allNames) {
    allNames[name]++;
  }
  else {
    allNames[name] = 1;
  }
  return allNames;
}, {});
// countedNames is:
// { 'Alice': 2, 'Bob': 1, 'Tiff': 1, 'Bruce': 1 }
```

#### 3.5 按属性对 object 分类

```js
var people = [
  { name: 'Alice', age: 21 },
  { name: 'Max', age: 20 },
  { name: 'Jane', age: 20 }
];

function groupBy(objectArray, property) {
  return objectArray.reduce(function (acc, obj) {
    var key = obj[property];
    if (!acc[key]) {
      acc[key] = [];
    }
    acc[key].push(obj);
    return acc;
  }, {});
}

var groupedPeople = groupBy(people, 'age');
// groupedPeople is:
// { 
//   20: [
//     { name: 'Max', age: 20 }, 
//     { name: 'Jane', age: 20 }
//   ], 
//   21: [{ name: 'Alice', age: 21 }] 
// }
```

1『上面的实现很值得借鉴，按一个对象里某个属性值，对一个对象进行分类。（2020-09-26）』

#### 3.6 使用扩展运算符和 initialValue 绑定包含在对象数组中的数组

```js
// friends - 对象数组
// where object field "books" - list of favorite books 
var friends = [{
  name: 'Anna',
  books: ['Bible', 'Harry Potter'],
  age: 21
}, {
  name: 'Bob',
  books: ['War and peace', 'Romeo and Juliet'],
  age: 26
}, {
  name: 'Alice',
  books: ['The Lord of the Rings', 'The Shining'],
  age: 18
}];

// allbooks - list which will contain all friends' books +  
// additional list contained in initialValue
var allbooks = friends.reduce(function(prev, curr) {
  return [...prev, ...curr.books];
}, ['Alphabet']);

// allbooks = [
//   'Alphabet', 'Bible', 'Harry Potter', 'War and peace', 
//   'Romeo and Juliet', 'The Lord of the Rings',
//   'The Shining'
// ]
```

#### 3.7 数组去重

注意： 如果你正在使用一个可以兼容 Set 和 Array.from() 的环境， 你可以使用 `let orderedArray = Array.from(new Set(myArray));` 来获得一个相同元素被移除的数组。

```js
let myArray = ['a', 'b', 'a', 'b', 'c', 'e', 'e', 'c', 'd', 'd', 'd', 'd']
let myOrderedArray = myArray.reduce(function (accumulator, currentValue) {
  if (accumulator.indexOf(currentValue) === -1) {
    accumulator.push(currentValue)
  }
  return accumulator
}, [])

console.log(myOrderedArray)
let arr = [1,2,1,2,3,5,4,5,3,4,4,4,4];
let result = arr.sort().reduce((init, current) => {
    if(init.length === 0 || init[init.length-1] !== current) {
        init.push(current);
    }
    return init;
}, []);
console.log(result); //[1,2,3,4,5]
```

#### 3.8 按顺序运行 Promise

```js
/**
 * Runs promises from array of functions that can return promises
 * in chained manner
 *
 * @param {array} arr - promise arr
 * @return {Object} promise object
 */
function runPromiseInSequence(arr, input) {
  return arr.reduce(
    (promiseChain, currentFunction) => promiseChain.then(currentFunction),
    Promise.resolve(input)
  );
}

// promise function 1
function p1(a) {
  return new Promise((resolve, reject) => {
    resolve(a * 5);
  });
}

// promise function 2
function p2(a) {
  return new Promise((resolve, reject) => {
    resolve(a * 2);
  });
}

// function 3  - will be wrapped in a resolved promise by .then()
function f3(a) {
 return a * 3;
}

// promise function 4
function p4(a) {
  return new Promise((resolve, reject) => {
    resolve(a * 4);
  });
}

const promiseArr = [p1, p2, f3, p4];
runPromiseInSequence(promiseArr, 10)
  .then(console.log);   // 1200
```

#### 3.9 功能型函数管道

```js
// Building-blocks to use for composition
const double = x => x + x;
const triple = x => 3 * x;
const quadruple = x => 4 * x;

// Function composition enabling pipe functionality
const pipe = (...functions) => input => functions.reduce(
    (acc, fn) => fn(acc),
    input
);

// Composed functions for multiplication of specific values
const multiply6 = pipe(double, triple);
const multiply9 = pipe(triple, triple);
const multiply16 = pipe(quadruple, quadruple);
const multiply24 = pipe(double, triple, quadruple);

// Usage
multiply6(6); // 36
multiply9(9); // 81
multiply16(16); // 256
multiply24(10); // 240
```

1『上面的实现目前没弄明白。（2020-09-26）』

#### 3.10 使用 reduce 实现 map

```js
if (!Array.prototype.mapUsingReduce) {
  Array.prototype.mapUsingReduce = function(callback, thisArg) {
    return this.reduce(function(mappedArray, currentValue, index, array) {
      mappedArray[index] = callback.call(thisArg, currentValue, index, array)
      return mappedArray
    }, [])
  }
}

[1, 2, , 3].mapUsingReduce(
  (currentValue, index, array) => currentValue + index + array.length
) // [5, 7, , 10]
```

