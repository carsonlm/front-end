[1 Array.from()](#1)  
[2 Array.isArray](#2)

<h2 id='1'>1 Array.from()</h2>
```javascript
  方法从一个类似数组或者可迭代对象中创建一个新的数组实例
  
  console.log(Array.from('foo'))
  //["f","o","o"]
  console.log(Array.from([1,2,3,4],x => x+x))
  //[2,4,6,8]
```
* Grammar:
   > Array.from(arrayLike[,mapFn[,thisArg]])
* Arguments：
  * arrayLike：想要转换成数组的伪数组对象或可迭代对象
  * mapFn：可选参数，如果指定了该参数，新数组中的每个元素都会执行该回调函数
  * thisArg：可选，执行回调函数mapFn时this对象
  * 返回值：新数组

<h2 id='2'>2 Array.isArray()</h2>
```javascript
  用于判断传递的值是否是Array
  Array.isArray([1,2,3])  // true
```
<h2 id='3'>3 Array.of()</h2>
```javascript
  用于创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。
  Array.of() 和 Array 构造函数之间的区别在于处理整数参数：Array.of(7) 创建一个具有单个元素 7 的数组，
  而 Array(7) 创建一个长度为7的空数组（注意：这是指一个有7个空位的数组，而不是由7个undefined组成的数组）。
  
  Array.of(7);       // [7] 
  Array.of(1, 2, 3); // [1, 2, 3]
  Array(7);          // [ , , , , , , ]
  Array(1, 2, 3);    // [1, 2, 3]
```
<h2 id='4'>4 Array.prototype.concat()</h2>
```javascript
  用于合并两个或多个数组，此方法不会更改现数组，而是创建新数组。
  var array1 = ['a', 'b', 'c'];
  var array2 = ['d', 'e', 'f'];
  console.log(array1.concat(array2));
  // ["a", "b", "c", "d", "e", "f"]
```
<h2 id='5'>5 Array.prototype.copyWithin<h2>
* Grammar: 方法浅复制数组的一部分到同一数组的另一个位置，并返回它，而不是修改其大小。
  > arr.copyWithin(target[, start[, end]])
* Arguments: 三个参数必须为整数
   * target: 0为基底的索引，复制序列到该位置。如果是负数，则从末尾开始算
   * start：0为基底的索引，开始复制元素的起始位置。负数则从末尾开始算。如果忽略，copyWithin将从0开始复制。
   * end：0为基底的索引，开始复制元素的结束位置。copyWithin将会拷贝到该位置，但不包括该end这个位置的元素。负数，从尾算。
          end如果被忽略，则会复制到arr.length。
    ```javascript
      [1, 2, 3, 4, 5].copyWithin(-2);
      // [1, 2, 3, 1, 2]
      [1, 2, 3, 4, 5].copyWithin(0, 3);
      // [4, 5, 3, 4, 5]
      [1, 2, 3, 4, 5].copyWithin(0, 3, 4);
      // [4, 2, 3, 4, 5]
      [1, 2, 3, 4, 5].copyWithin(-2, -3, -1);
      // [1, 2, 3, 3, 4]
      [].copyWithin.call({length: 5, 3: 1}, 0, 3);
      // {0: 1, 3: 1, length: 5}
    ```
<h2 id='6'>6 Array.prototype.entries()</h2>
* Grammar:
 >arr.entries() 方法返回一个新的Array Iterator对象，该对象包含数组中每个索引的键/值对。
 ```javascript
  var array1 = ['a', 'b', 'c'];
  var iterator1 = array1.entries();
  
  console.log(iterator1.next().value);
  // expected output: Array [0, "a"]
  console.log(iterator1.next().value);
  // [1,"b"]
```
<h2 id='7'>7 Array.prototype.every()</h2>
* Grammar:
  > arr.every(callback[, thisArg]) 测试数组的所有元素是否都通过了指定函数的测试
* Arguments:
   * callback:用来测试每个元素的函数
   * thisArg: 执行callback时使用的this值
```javascript
function isBelow(currentValue) {
    return currentValue<40;
}
var arr=[1,23,32,44];
console.log(arr.every(isBelow))
// false
```
<h2 id='8'>8 Array.prototype.fill()<h2>
* Grammar:
  > arr.fill(value[,start[,end]])  方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。
* Arguments:
  * value: 用来填充数组元素的值
  * start: 可选，起始索引，默认为0
  * end: 可选，结束索引，默认为this.length
  * 返回值：修改后的数组
```javascript
var array1 = [1, 2, 3, 4];
// fill with 0 from position 2 until position 4
console.log(array1.fill(0, 2, 4));
// expected output: [1, 2, 0, 0]
// fill with 5 from position 1
console.log(array1.fill(5, 1));
// expected output: [1, 5, 5, 5]
console.log(array1.fill(6));
// expected output: [6, 6, 6, 6]
```
<h2 id='9'>9 Array.prototype.filter()</h2>
* Grammar:
  > arr.filter(callback(element[,index[,array]]),thisArg) 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。
* Arguments：
   * callback：用来测试数组的每个元素的函数。调用时使用参数 (element, index, array)。返回true表示保留该元素（通过测试），false则不保留。
       * element：当前数组中处理的元素
       * index：可选，正在处理元素在数组中的索引
       * array：可选，调用了filter的数组
   * thisArg：执行callback时，this的值
```javascript
var words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
const result = words.filter(word => word.length > 6);
console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```
<h2 id='10'>10 Array.prototype.find()</h2>
* Grammar:
  > arr.find(callback(element[,index[,array]]),thisArg) 方法返回数组中满足提供的测试函数的第一个元素的值。否则返回 undefined。
* Arguments:
   * callback:测试函数
       * element: 当前遍历到的元素
       * index:当前元素的索引
       * array:数组本身
   * thisArg：可选，指定callback的this参数
```javascript
var array1 = [5, 12, 8, 130, 44];

var found = array1.find(function(element) {
  return element > 10;
});
console.log(found);
// expected output: 12
```
<h2 id='11'>11 Array.prototype.findIndex()<h2>
* Grammar:
  > arr.findIndex(参数同上) 方法返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1
* Arguments:
   同上：
```javascript
 var array1 = [5, 12, 8, 130, 44];
 
 function findFirstLargeNumber(element) {
   return element > 13;
 }
 console.log(array1.findIndex(findFirstLargeNumber));
 // expected output: 3
```
<h2 id='12'>12 Array.prototype.</h2>
* Grammar:
 > array.forEach(callback(currentValue, index, array){
       //do something
   }, this)
   array.forEach(callback[, thisArg]) 方法对数组的每个元素执行一次提供的函数
* Arguments:
   * callback:为数组中每个元素执行的函数，该函数接收三个参数：
         * currentValue:数组中正在处理的当前元素。
         * index: 当前元素的索引
         * array: 正在foreach的数组
   * thisArg: 可选参数。当执行回调 函数时用作this的值(参考对象)。
```javascript
var array1 = ['a', 'b', 'c'];

array1.forEach(function(element) {
  console.log(element);
});

// expected output: "a"
// expected output: "b"
// expected output: "c"
```
<h2 id='13'>13 Array.prototype.includes()</h2>
* Grammar:
  > arr.includes(searchElement, fromIndex) 方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false。
* Arguments:
   * searchElement:需要查找的元素值
   * fromIndex:可选，从该索引处开始查找 searchElement。如果为负值，则按升序从 array.length + fromIndex 的索引开始搜索。默认为 0。
    ```javascript
    var array1 = [1, 2, 3];
    
    console.log(array1.includes(2));
    // expected output: true
    var pets = ['cat', 'dog', 'bat'];
    console.log(pets.includes('cat'));
    // expected output: true
    console.log(pets.includes('at'));
    // expected output: false
    ```
  <h2 id='14'>14 Array.prototype.indexOf()</h2>
* Grammar:
  > arr.indexOf(searchElement[, fromIndex = 0]) 方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1
  > 和String.indexOf()方法类似
* Arguments：
   * searchElement:要查找的元素
   * fromIndex：开始查找的位置
   ```javascript
      var beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];
      
      console.log(beasts.indexOf('bison'));
      // expected output: 1
      
      // start from index 2
      console.log(beasts.indexOf('bison', 2));
      // expected output: 4
      
      console.log(beasts.indexOf('giraffe'));
      // expected output: -1
  ```
 <h2 id='15'>15 Array.prototype.join()</h2>
 * Grammar:
   > str = arr.join(separator) 方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。
 * Arguments:
   * separator:指定一个字符串来分隔数组的每个元素。
               如果需要(separator)，将分隔符转换为字符串。
               如果省略()，数组元素用逗号分隔。默认为 ","。
               如果separator是空字符串("")，则所有元素之间都没有任何字符。
 ```javascript
  var elements = ['Fire', 'Wind', 'Rain'];
  
  console.log(elements.join());
  // expected output: Fire,Wind,Rain
  
  console.log(elements.join(''));
  // expected output: FireWindRain
  
  console.log(elements.join('-'));
  // expected output: Fire-Wind-Rain
```
<h2 id='16'>16 Array.prototype.keys()</h2>
  * Grammar:
     > arr.keys()  方法返回一个包含数组中每个索引键的Array Iterator对象。
     返回值：一个新的 Array 迭代器对象
```javascript
 var array1 = ['a', 'b', 'c'];
 var iterator = array1.keys(); 
   
 for (let key of iterator) {
   console.log(key); // expected output: 0 1 2
 }
```
<h2 id='17'>17 Array.prototype.lastIndexOf()</h2>
* Grammar:
    > arr.lastIndexOf(searchElement[, fromIndex = arr.length - 1]) 方法返回指定元素（也即有效的 JavaScript 值或变量）在数组中的最后一个的索引，如果不存在则返回 -1。从数组的后面向前查找，从 fromIndex 处开始。
* Arguments:
    * searchElement: 被查找的元素
    * fromIndex:从此位置开始逆向查找。
```javascript
var animals = ['Dodo', 'Tiger', 'Penguin', 'Dodo'];

console.log(animals.lastIndexOf('Dodo'));
// expected output: 3

console.log(animals.lastIndexOf('Tiger'));
// expected output: 1
```
<h2 id='18'>18 Array.prototype.map()</h2>
* Grammar:
   > var new_array = arr.map(function callback(currentValue[, index[, array]]) {
           // Return element for new_array }[, 
          thisArg]) 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果
* Arguments:
   * callback:生成新数组元素的函数，三个参数
       * currentValue:callback 数组中正在处理的当前元素。
       * index：可选，当前元素的索引。
       * array：可选，callback 
       * 返回值：一个新数组，每个元素都是回调函数的结果
```javascript
var array1 = [1, 4, 9, 16];
// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```
<h2 id='19'>19 Array.prototype.pop()</h2>
* 方法从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。
```javascript
var plants = ['broccoli', 'cauliflower', 'cabbage', 'kale', 'tomato'];

console.log(plants.pop());
// expected output: "tomato"

console.log(plants);
// expected output: Array ["broccoli", "cauliflower", "cabbage", "kale"]

plants.pop();

console.log(plants);
// expected output: Array ["broccoli", "cauliflower", "cabbage"]
```
<h2 id='20'>20 Array.prototype.push()</h2>
* 方法将一个或多个元素添加到数组的末尾，并返回新数组的长度
```javascript
var animals = ['pigs', 'goats', 'sheep'];

console.log(animals.push('cows'));
// expected output: 4

console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows"]

animals.push('chickens');

console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows", "chickens"]
```
<h2 id='21'>21 Array.prototype.reduce()</h2>
* 方法对累加器和数组中的每个元素（从左到右）应用一个函数，将其简化为单个值。
```javascript
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```
<h2 id='22'>22 Array.prototype.reduceRight()</h2>
* 方法接受一个函数作为累加器（accumulator）和数组的每个值（从右到左）将其减少为单个值。
```javascript
const array1 = [[0, 1], [2, 3], [4, 5]].reduceRight(
  (accumulator, currentValue) => accumulator.concat(currentValue)
);

console.log(array1);
// expected output: Array [4, 5, 2, 3, 0, 1]

```
<h2 id='23'>23 Array.prototype.reverse()</h2>
* 将数组中元素的位置颠倒
```javascript

```
<h2 id='24'>24 Array.prototype.shift()</h2>
* 从数组中删除第一个元素，并返回它的值。改变数组长度
```javascript

```
<h2 id='25'>25 Array.prototype.slice()</h2>
* 返回一个从开始到结束（不包括结束）选择的数组的一部分浅拷贝到一个新数组对象。且原始数组不会被修改。
```javascript
var animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// expected output: Array ["camel", "duck"]

console.log(animals.slice(1, 5));
// expected output: Array ["bison", "camel", "duck", "elephant"]

```
<h2 id='26'>26 Array.prototype.some()</h2>
* 测试数组中的某些元素是否通过由提供的函数实现的测试
* 注：空数组调用该方法返回false
```javascript
var array = [1, 2, 3, 4, 5];

var even = function(element) {
  // checks whether an element is even
  return element % 2 === 0;
};

console.log(array.some(even));
// expected output: true
```
<h2 id='27'>27 Array.prototype.sort()</h2>
* 用原地算法对数组的元素进行排序，并返回数组。排序不一定是稳定的。默认排序顺序是根据字符串Unicode码点。
*  由于它取决于具体实现，因此无法保证排序的时间和空间复杂性。
```javascript
var months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// expected output: Array ["Dec", "Feb", "Jan", "March"]

var array1 = [1, 30, 4, 21];
array1.sort();
console.log(array1);
// expected output: Array [1, 21, 30, 4]
```
<h2 id='28'>28 Array.prototype.splice()</h2>
* 通过删除现有元素和/或添加新元素来更改一个数组的内容
* Grammar：
  >
* Arguments:
  * 第一个参数表示操作的起始位置
  * 第二个参数，整数，表示要移除的数组元素的个数。如果 deleteCount 是 0，则不移除元素。
     这种情况下，至少应添加一个新元素。
     如果 deleteCount 大于start 之后的元素的总数，则从 start 后面的元素都将被删除（含第 start 位）。
  * 第三个参数，要添加进数组的元素,从start 位置开始。如果不指定，则 splice() 将只删除数组元素。
```javascript
var months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// inserts at 1st index position
console.log(months);
// expected output: Array ['Jan', 'Feb', 'March', 'April', 'June']

months.splice(4, 1, 'May');
// replaces 1 element at 4th index
console.log(months);
// expected output: Array ['Jan', 'Feb', 'March', 'April', 'May']

```
<h2 id='29'>29 Array.prototype.toLocalString()</h2>
* 
```javascript

```
<h2 id='30'>30 Array.prototype.toSource()</h2>
* 返回数组的源代码
```javascript

```
<h2 id='31'>31 Array.prototype.toString()</h2>
* 
```javascript

```
<h2 id='32'>32 Array.prototype.unShift()</h2>
* 
```javascript

```
<h2 id='33'>33 Array.prototype.values()</h2>
* 方法返回一个新的 Array Iterator 对象，该对象包含数组每个索引的值
```javascript
const array1 = ['a', 'b', 'c'];
const iterator = array1.values();

for (const value of iterator) {
  console.log(value); // expected output: "a" "b" "c"
}

```