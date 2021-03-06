## 记忆时间

## 目录

0201 Map

## 0201. Map

The Map object holds key-value pairs and remembers the original insertion order of the keys. Any value (both objects and primitive values) may be used as either a key or a value.

[Primitive - MDN Web Docs Glossary: Definitions of Web-related terms | MDN](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)

Map 对象保存键值对，并且能够记住键的原始插入顺序。任何值（对象或者原始值）都可以作为一个键或一个值。

### 01. Description

A Map object iterates its elements in insertion order — a for...of loop returns an array of [key, value] for each iteration.

一个 Map 对象在迭代时会根据对象中元素的插入顺序来进行 — 一个 for...of 循环在每次迭代后会返回一个形式为 [key，value] 的数组。

#### 1.1 Key equality

Key equality is based on the sameValueZero algorithm.

NaN is considered the same as NaN (even though NaN !== NaN) and all other values are considered equal according to the semantics of the === operator.

In the current ECMAScript specification, -0 and +0 are considered equal, although this was not so in earlier drafts. See "Value equality for -0 and 0" in the Browser compatibility table for details.

键的相等 (Key equality)

键的比较是基于 sameValueZero 算法：

NaN 是与 NaN 相等的（虽然 NaN !== NaN），剩下所有其它的值是根据 === 运算符的结果判断是否相等。在目前的 ECMAScript 规范中，-0 和 + 0 被认为是相等的，尽管这在早期的草案中并不是这样。有关详细信息，请参阅浏览器兼容性表中的「Value equality for -0 and 0」。

#### 1.2 Objects vs. Maps

Object is similar to Map—both let you set keys to values, retrieve those values, delete keys, and detect whether something is stored at a key. For this reason (and because there were no built-in alternatives), Object has been used as Map historically.

However, there are important differences that make Map preferable in some cases:

| - | Map | Object |
| --- | --- | ---- |
| Accidental Keys | 	A Map does not contain any keys by default. It only contains what is explicitly put into it. | An Object has a prototype, so it contains default keys that could collide with your own keys if you're not careful. Note: As of ES5, this can be bypassed by using Object.create(null), but this is seldom done. |
| Key Types | A Map's keys can be any value (including functions, objects, or any primitive). | The keys of an Object must be either a String or a Symbol. |
| Key Order | The keys in Map are ordered in a simple, straightforward way: A Map object iterates entries, keys, and values in the order of entry insertion. | Although the keys of an ordinary Object are ordered now, this was not always the case, and the order is complex. As a result, it's best not to rely on property order. The order was first defined for own properties only in ECMAScript 2015; ECMAScript 2020 defines order for inherited properties as well. See the OrdinaryOwnPropertyKeys and EnumerateObjectProperties abstract specification operations. But note that no single mechanism iterates all of an object's properties; the various mechanisms each include different subsets of properties. (for-in includes only enumerable string-keyed properties; Object.keys includes only own, enumerable, string-keyed properties; Object.getOwnPropertyNames includes own, string-keyed properties even if non-enumerable; Object.getOwnPropertySymbols does the same for just Symbol-keyed properties, etc.) |
| Size | The number of items in an Object must be determined manually. |
| Iteration | A Map is an iterable, so it can be directly iterated. | Object does not implement an iteration protocol, and so objects are not directly iterable using the JavaScript for...of statement (by default). Note: 1) An object can implement the iteration protocol, or you can get an iterable for an object using Object.keys or Object.entries. 2) The for...in statement allows you to iterate over the enumerable properties of an object. |
| Performance | Performs better in scenarios involving frequent additions and removals of key-value pairs. | Not optimized for frequent additions and removals of key-value pairs. |
| Serialization and parsing | No native support for serialization or parsing. (But you can build your own serialization and parsing support for Map by using JSON.stringify() with its replacer argument, and by using JSON.parse() with its reviver argument. See the Stack Overflow question How do you JSON.stringify an ES6 Map? | Native support for serialization from Object to JSON, using JSON.stringify(). Native support for parsing from JSON to Object, using JSON.parse(). |

Objects 和 Maps 类似的是，它们都允许你按键存取一个值、删除键、检测一个键是否绑定了值。因此（并且也没有其他内建的替代方式了）过去我们一直都把对象当成 Maps 使用。不过 Maps 和 Objects 有一些重要的区别，在下列情况里使用 Map 会是更好的选择：

| - | Map | Object |
| --- | --- | ---- |
| 意外的键 | Map 默认情况不包含任何键。只包含显式插入的键。 | 一个 Object 有一个原型，原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。注意: 虽然 ES5 开始可以用 Object.create(null) 来创建一个没有原型的对象，但是这种用法不太常见。 |
| 键的类型 | 一个 Map的键可以是任意值，包括函数、对象或任意基本类型。 | 一个 Object 的键必须是一个 String 或是 Symbol。 |
| 键的顺序 | Map 中的 key 是有序的。因此，当迭代的时候，一个 Map 对象以插入的顺序返回键值。 | 一个 Object 的键是无序的。注意：自 ECMAScript 2015 规范以来，对象确实保留了字符串和 Symbol 键的创建顺序； 因此，在只有字符串键的对象上进行迭代将按插入顺序产生键。 |
| Size | Map 的键值对个数可以轻易地通过 size 属性获取。 | Object 的键值对个数只能手动计算。 |
| 迭代 | Map 是 iterable 的，所以可以直接被迭代。 | 迭代一个 Object 需要以某种方式获取它的键然后才能迭代。 |
| 性能 | 在频繁增删键值对的场景下表现更好。 | 在频繁添加和删除键值对的场景下未作出优化。 |

#### 1.3 Setting object properties

Setting Object properties works for Map objects as well, and can cause considerable confusion. Therefore, this appears to work in a way:

```js
let wrongMap = new Map()
wrongMap['bla'] = 'blaa'
wrongMap['bla2'] = 'blaaa2'

console.log(wrongMap)  // Map { bla: 'blaa', bla2: 'blaaa2' }
```

But that way of setting a property does not interact with the Map data structure. It uses the feature of the generic object. The value of 'bla' is not stored in the Map for queries. Other operations on the data fail:

```js
wrongMap.has('bla')    // false
wrongMap.delete('bla') // false
console.log(wrongMap)  // Map { bla: 'blaa', bla2: 'blaaa2' }
```

The correct usage for storing data in the Map is through the set(key, value) method.

```js
let contacts = new Map()
contacts.set('Jessie', {phone: "213-555-1234", address: "123 N 1st Ave"})
contacts.has('Jessie') // true
contacts.get('Hilary') // undefined
contacts.set('Hilary', {phone: "617-555-4321", address: "321 S 2nd St"})
contacts.get('Jessie') // {phone: "213-555-1234", address: "123 N 1st Ave"}
contacts.delete('Raymond') // false
contacts.delete('Jessie') // true
console.log(contacts.size) // 1
```

### 02. Constructor

Map()

Creates a new Map object.

[Map() constructor - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/Map)

The Map() constructor creates Map objects.

Syntax

```js
new Map()
new Map(iterable)
```

Parameters

iterable Optional

An Array or other iterable object whose elements are key-value pairs. (For example, arrays with two elements, such as [[ 1, 'one' ],[ 2, 'two' ]].) Each key-value pair is added to the new Map.

Examples

Creating a new Map

```js
let myMap = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
])
```

### 03. Static properties

get Map[@@species]

The constructor function that is used to create derived objects.

The Map[@@species] accessor property returns the Map constructor.

Description: The species accessor property returns the default constructor for Map objects. Subclass constructors may over-ride it to change the constructor assignment.

Examples

1 Species in ordinary objects

The species property returns the default constructor function, which is the Map constructor for Map objects:

```js
Map[Symbol.species]; // function Map()
```

1 Species in derived objects

In a derived collection object (e.g. your custom map MyMap), the MyMap species is the MyMap constructor. However, you might want to overwrite this, in order to return parent Map objects in your derived class methods:

```js
class MyMap extends Map {
  // Overwrite MyMap species to the parent Map constructor
  static get [Symbol.species]() { return Map; }
}
```

### 04. Instance properties

Map.prototype.size

Returns the number of key/value pairs in the Map object.

The size accessor property returns the number of elements in a Map object.

Description: The value of size is an integer representing how many entries the Map object has. A set accessor function for size is undefined; you can not change this property.

Examples

Using size

```js
const map1 = new Map();

map1.set('a', 'alpha');
map1.set('b', 'beta');
map1.set('g', 'gamma');

console.log(map1.size);
// expected output: 3
```

### 05. Instance methods

1 Map.prototype.clear()

Removes all key-value pairs from the Map object.

2 Map.prototype.delete(key)

Returns true if an element in the Map object existed and has been removed, or false if the element does not exist. Map.prototype.has(key) will return false afterwards.

3 Map.prototype.get(key)

Returns the value associated to the key, or undefined if there is none.

4 Map.prototype.has(key)

Returns a boolean asserting whether a value has been associated to the key in the Map object or not.

5 Map.prototype.set(key, value)

Sets the value for the key in the Map object. Returns the Map object.

#### 5.1 Iteration methods

```js
Map.prototype[@@iterator]()
```

Returns a new Iterator object that contains an array of [key, value] for each element in the Map object in insertion order.

Map.prototype.keys()

Returns a new Iterator object that contains the keys for each element in the Map object in insertion order.

Map.prototype.values()

Returns a new Iterator object that contains the values for each element in the Map object in insertion order.

Map.prototype.entries()

Returns a new Iterator object that contains an array of [key, value] for each element in the Map object in insertion order.

Map.prototype.forEach(callbackFn[, thisArg])

Calls callbackFn once for each key-value pair present in the Map object, in insertion order. If a thisArg parameter is provided to forEach, it will be used as the this value for each callback.

### 06. Examples

#### 6.1 Using the Map object

```js
let myMap = new Map()

let keyString = 'a string'
let keyObj    = {}
let keyFunc   = function() {}

// setting the values
myMap.set(keyString, "value associated with 'a string'")
myMap.set(keyObj, 'value associated with keyObj')
myMap.set(keyFunc, 'value associated with keyFunc')

myMap.size              // 3

// getting the values
myMap.get(keyString)    // "value associated with 'a string'"
myMap.get(keyObj)       // "value associated with keyObj"
myMap.get(keyFunc)      // "value associated with keyFunc"

myMap.get('a string')    // "value associated with 'a string'"
                         // because keyString === 'a string'
myMap.get({})            // undefined, because keyObj !== {}
myMap.get(function() {}) // undefined, because keyFunc !== function () {}
```

#### 6.2 Using NaN as Map keys

NaN can also be used as a key. Even though every NaN is not equal to itself (NaN !== NaN is true), the following example works because NaNs are indistinguishable from each other:

```js
let myMap = new Map()
myMap.set(NaN, 'not a number')

myMap.get(NaN)
// "not a number"

let otherNaN = Number('foo')
myMap.get(otherNaN)
// "not a number"
```

#### 6.3 Iterating Map with for..of

Maps can be iterated using a for..of loop:

```js
let myMap = new Map()
myMap.set(0, 'zero')
myMap.set(1, 'one')

for (let [key, value] of myMap) {
  console.log(key + ' = ' + value)
}
// 0 = zero
// 1 = one

for (let key of myMap.keys()) {
  console.log(key)
}
// 0
// 1

for (let value of myMap.values()) {
  console.log(value)
}
// zero
// one

for (let [key, value] of myMap.entries()) {
  console.log(key + ' = ' + value)
}
// 0 = zero
// 1 = one
```

#### 6.4 Iterating Map with forEach()

Maps can be iterated using the forEach() method:

```js
myMap.forEach(function(value, key) {
  console.log(key + ' = ' + value)
})
// 0 = zero
// 1 = one
```

#### 6.5 Relation with Array objects

```js
let kvArray = [['key1', 'value1'], ['key2', 'value2']]

// Use the regular Map constructor to transform a 2D key-value Array into a map
let myMap = new Map(kvArray)

myMap.get('key1') // returns "value1"

// Use Array.from() to transform a map into a 2D key-value Array
console.log(Array.from(myMap)) // Will show you exactly the same Array as kvArray

// A succinct way to do the same, using the spread syntax
console.log([...myMap])

// Or use the keys() or values() iterators, and convert them to an array
console.log(Array.from(myMap.keys())) // ["key1", "key2"]
```

#### 6.6 Cloning and merging Maps

Just like Arrays, Maps can be cloned:

```js
let original = new Map([
  [1, 'one']
])

let clone = new Map(original)

console.log(clone.get(1))       // one
console.log(original === clone) // false (useful for shallow comparison)
```

Note: Keep in mind that the data itself is not cloned.

Maps can be merged, maintaining key uniqueness:

```js
let first = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
])

let second = new Map([
  [1, 'uno'],
  [2, 'dos']
])

// Merge two maps. The last repeated key wins.
// Spread operator essentially converts a Map to an Array
let merged = new Map([...first, ...second])

console.log(merged.get(1)) // uno
console.log(merged.get(2)) // dos
console.log(merged.get(3)) // three
```

Maps can be merged with Arrays, too:

```js
let first = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
])

let second = new Map([
  [1, 'uno'],
  [2, 'dos']
])

// Merge maps with an array. The last repeated key wins.
let merged = new Map([...first, ...second, [1, 'eins']])

console.log(merged.get(1)) // eins
console.log(merged.get(2)) // dos
console.log(merged.get(3)) // three
```