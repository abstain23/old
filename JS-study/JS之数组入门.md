﻿#数组 Array
* 数组（array）是按次序排列的一组值。每个值的位置都有编号（从0开始），整个数组用方括号表示。
>> var arr = ['a', 'b', 'c'];
> 上面代码中的a、b、c就构成一个数组，两端的方括号是数组的标志。a是0号位置，b是1号位置，c是2号位置。
* 任何类型的数据，都可以放入数组。
>> var arr = [
>>   {a: 1},
>>   [1, 2, 3],
>>   function() {return true;}
>> ];
>> 
>> arr[0] // Object {a: 1}
>> arr[1] // [1, 2, 3]
>> arr[2] // function (){return true;}
> 上面数组arr的3个成员依次是对象、数组、函数。
* 如果数组的元素还是数组，就形成了多维数组。
>> var a = [[1, 2], [3, 4]];
>> a[0][1] // 2
>> a[1][1] // 4
* 本质上，数组属于一种特殊的对象。typeof运算符会返回数组的类型是object。
>> typeof [1, 2, 3] // "object"
* 数组的特殊性体现在，它的键名是按次序排列的一组整数（0，1，2...）。

>> ar arr = ['a', 'b', 'c'];
>> 
>> bject.keys(arr)
>> / ["0", "1", "2"]
> 上面代码中，Object.keys方法返回数组的所有键名。可以看到数组的键名就是整数0、1、2。
*由于数组成员的键名是固定的（默认总是0、1、2...），因此数组不用为每个元素指定键名，而对象的每个成员都必须指定键名。JavaScript 语言规定，对象的键名一律为字符串，所以，数组的键名其实也是字符串。之所以可以用数值读取，是因为非字符串的键名会被转为字符串。*
>> var arr = ['a', 'b', 'c'];
>> 
>> arr['0'] // 'a'
>> arr[0] // 'a
*注意不能使用点结构，因为键名为数值*
* 数组的length属性，返回数组的成员数量
>> ['a', 'b', 'c'].length // 3
> JavaScript 使用一个32位整数，保存数组的元素个数。这意味着，数组成员最多只有 4294967295 个（232 - 1）个，也就是说length属性的最大值就是 4294967295。

* 只要是数组，就一定有length属性。该属性是一个动态的值，等于键名中的最大整数加上1。
>> var arr = ['a', 'b'];
>> arr.length // 2
>> 
>> arr[2] = 'c';
>> arr.length // 3
>> 
>> arr[9] = 'd';
>> arr.length // 10
>> 
>> arr[1000] = 'e';
>> arr.length // 1001
> 上面代码表示，数组的数字键不需要连续，length属性的值总是比最大的那个整数键大1。另外，这也表明数组是一种动态的数据结构，可以随时增减数组的成员
* length属性是可写的。如果人为设置一个小于当前成员个数的值，该数组的成员会自动减少到length设置的值。    
>> var arr = [ 'a', 'b', 'c' ];
>> arr.length // 3
>> 
>> arr.length = 2;
>> arr // ["a", "b"]
*清空数组的一个有效方法，就是将length属性设为0*
* 如果人为设置length大于当前元素个数，则数组的成员数量会增加到这个值，新增的位置都是空位。
>> var a = ['a'];
>> 
>> a.length = 3;
>> a[1] // undefined
*由于数组本质上是一种对象，所以可以为数组添加属性，但是这不影响length属性的值。*
>> var a = [];

>> a['p'] = 'abc';
>> a.length // 0
>> 
>> a[2.1] = 'abc';
>> a.length // 0
> 上面代码将数组的键分别设为字符串和小数，结果都不影响length属性。因为，length属性的值就是等于最大的数字键加1，而这个数组没有整数键，所以length属性保持为0。
* 如果数组的键名是添加超出范围的数值，该键名会自动转为字符串
>> var arr = [];
>> arr[-1] = 'a';
>> arr[Math.pow(2, 32)] = 'b';
>> 
>> arr.length // 0
>> arr[-1] // "a"
>> arr[4294967296] // "b"
> 上面代码中，我们为数组arr添加了两个不合法的数字键，结果length属性没有发生变化。这些数字键都变成了字符串键名。最后两行之所以会取到值，是因为取键值时，数字键名会默认转为字符串。

* 检查某个键名是否存在的运算符in，适用于对象，也适用于数组。
>> var arr = [ 'a', 'b', 'c' ];
>> 2 in arr  // true
>> '2' in arr // true
>> 4 in arr // false
*注意，如果数组的某个位置是空位，in运算符返回false。*
>> var arr = [];
>> arr[100] = 'a';
>> 
>> 100 in arr // true
>> 1 in arr // false
* for...in循环不仅可以遍历对象，也可以遍历数组，毕竟数组只是一种特殊对象
>> var a = [1, 2, 3];
>> 
>> for (var i in a) {
>>   console.log(a[i]);
>> }
>> // 1
>> // 2
>> // 3
* 但是，for...in不仅会遍历数组所有的数字键，还会遍历非数字键。
>> var a = [1, 2, 3];
>> a.foo = true;
>> 
>> for (var key in a) {
>>   console.log(key);
>> }
>> // 0
>> // 1
>> // 2
>> // foo
* 数组的遍历可以考虑使用for循环或while循环。
* 数组的forEach方法，也可以用来遍历数组
>> var colors = ['red', 'green', 'blue'];
>> colors.forEach(function (color) {
>>   console.log(color);
>> });
>> // red
>> // green
>> // blue
* 当数组的某个位置是空元素，即两个逗号之间没有任何值，我们称该数组存在空位
>> var a = [1, , 1];
>> a.length // 3
* 数组的空位是可以读取的，返回undefined
* 使用delete命令删除一个数组成员，会形成空位，并且不会影响length属性。
>> var a = [1, 2, 3];
>> delete a[1];
>> 
>> a[1] // undefined
>> a.length // 3
> 上面代码用delete命令删除了数组的第二个元素，这个位置就形成了空位，但是对length属性没有影响。也就是说，length属性不过滤空位。所以，使用length属性进行数组遍历，一定要非常小心。
* 数组的某个位置是空位，与某个位置是undefined，是不一样的。如果是空位，使用数组的forEach方法、for...in结构、以及Object.keys方法进行遍历，空位都会被跳过。
>> var a = [, , ,];
>> 
>> a.forEach(function (x, i) {
>>   console.log(i + '. ' + x);
>> })
>> // 不产生任何输出
>> 
>> for (var i in a) {
>>   console.log(i);
>> }
>> // 不产生任何输出
>> 
>> Object.keys(a)
>> // []
* 如果某个位置是undefined，遍历的时候就不会被跳过。
>> var a = [undefined, undefined, undefined];
>> 
>> a.forEach(function (x, i) {
>>   console.log(i + '. ' + x);
>> });
>> // 0. undefined
>> // 1. undefined
>> // 2. undefined
>> 
>> for (var i in a) {
>>   console.log(i);
>> }
>> // 0
>> // 1
>> // 2
>> 
>> Object.keys(a)
>> // ['0', '1', '2']
> *这就是说，空位就是数组没有这个元素，所以不会被遍历到，而undefined则表示数组有这个元素，值是undefined，所以遍历不会跳过。*

## 类似数组的对象
* 如果一个对象的所有键名都是正整数或零，并且有length属性，那么这个对象就很像数组，语法上称为“类似数组的对象”（array-like object）
>> var obj = {
>>   0: 'a',
>>   1: 'b',
>>   2: 'c',
>>   length: 3
>> };
>> 
>> obj[0] // 'a'
>> obj[1] // 'b'
>> obj.length // 3
>> obj.push('d') // TypeError: obj.push is not a function
> 上面代码中，对象obj就是一个类似数组的对象。但是，“类似数组的对象”并不是数组，因为它们不具备数组特有的方法。对象obj没有数组的push方法，使用该方法就会报错。
* “类似数组的对象”的根本特征，就是具有length属性。只要有length属性，就可以认为这个对象类似于数组。但是有一个问题，这种length属性不是动态值，不会随着成员的变化而变化。
>> var obj = {
>>   length: 0
>> };
>> obj[3] = 'd';
>> obj.length // 0
*典型的“类似数组的对象”是函数的arguments对象，以及大多数 DOM 元素集，还有字符串。*
>> // arguments对象
>> function args() { return arguments }
>> var arrayLike = args('a', 'b');
>> 
>> arrayLike[0] // 'a'
>> arrayLike.length // 2
>> arrayLike instanceof Array // false
>> 
>> // DOM元素集
>> var elts = document.getElementsByTagName('h3');
>> elts.length // 3
>> elts instanceof Array // false
>> 
>> // 字符串
>> 'abc'[1] // 'b'
>> 'abc'.length // 3
>> 'abc' instanceof Array // false
*数组的slice方法可以将“类似数组的对象”变成真正的数组。* 
> *var arr = Array.prototype.slice.call(arrayLike);*
*除了转为真正的数组，“类似数组的对象”还有一个办法可以使用数组的方法，就是通过call()把数组的方法放到对象上面。*

>>function print(value, index) {
>>  console.log(index + ' : ' + value);
>>}
>>
>>Array.prototype.forEach.call(arrayLike, print);
>>上面代码中，arrayLike代表一个类似数组的对象，本来是不可以使用数组的>>forEach()方法的，但是通过call()，可以把forEach()嫁接到arrayLike上面调用。