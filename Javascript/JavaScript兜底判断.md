**一、JS基础数据类型普及**

JS数据类型：JS 的数据类型有几种？

   8种。Number、String、Boolean、Null、undefined、object、symbol、bigInt。

JS数据类型：Object 中包含了哪几种类型？

   其中包含了Data、function、Array等。这三种是常规用的。

JS数据类型：JS的基本类型和引用类型有哪些呢？

  基本类型（单类型）：除Object。 String、Number、boolean、null、undefined。

  引用类型：object。里面包含的 function、Array、Date。

JS数据类型：JS 中 typeof 输出分别是什么？

  { } 、[ ] 输出 object。

  console.log( ) 输出 function。

  注意一点：NaN 是 Number 中的一种，非Number 。

JS数据类型：null 和 undefined 有什么区别？

   Null 只有一个值，是 null。不存在的对象。

  Undefined 只有一个值，是undefined。没有初始化。undefined 是从 null 中派生出来的。

  简单理解就是：undefined 是没有定义的，null 是定义了但是为空。

JS数据类型：== 和 === 有什么区别，什么场景下使用？

​    == 表示相同。

  比较的是物理地址，相当于比较两个对象的 hashCode ，肯定不相等的。

   类型不同，值也可能相等。

=== 表示严格相同。

   例：同为 null／undefined ，相等。

   简单理解就是 == 就是先比较数据类型是否一样。=== 类型不同直接就是 false

JS数据类型：对象比较

  对象是可以比较，遍历比较key 和 value就行, Object.is(val1, val2)

JS数据类型：null 和 undefined 有什么区别？

   Null 只有一个值，是 null。不存在的对象。

  Undefined 只有一个值，是undefined。没有初始化。undefined 是从 null 中派生出来的。

  简单理解就是：undefined 是没有定义的，null 是定义了但是为空。

**二、实战应用**

**1. 判断返回的数据类型是否为指定类型**

 **typeof运算符的返回类型为字符串，值包括如下6种：**

​    **1. 'undefined'       --未定义的变量或值**

​    **2. 'boolean'         --布尔类型的变量或值**

​    **3. 'string'           --字符串类型的变量或值**

​    **4. 'number'         --数字类型的变量或值**

​    **5. 'object'          --对象类型的变量或值，或者null(这个是js历史遗留问题，将null作为object类型处理)**

​    **6. 'function'         --函数类型的变量或值**

**总结：typeof运算符用于判断对象的类型，但是对于一些创建的对象，它们都会返回'object'，有时我们需要判断该实例是否为某个对象的实例，那么这个时候需要用到instanceof运算符，后续记录instanceof运算符的相关用法。**

```javascript
// 示例
console.log(typeof a);    //'undefined'
console.log(typeof(true));  //'boolean'
console.log(typeof '123');  //'string'
console.log(typeof 123);   //'number'
console.log(typeof NaN);   //'number'
console.log(typeof null);  //'object'    
var obj = new String();
console.log(typeof(obj));    //'object'
var  fn = function(){};
console.log(typeof(fn));  //'function'
console.log(typeof(class c{}));  //'function'
```

**2. 如何判断返回的数据为特殊类型（undefined、null、NaN）**

```javascript
// 判断是否为undefined
typeof(res)=="undefined"

// 判断是否为null isNaN() 函数通常用于检测 parseFloat() 和 parseInt() 的结果，以判断它们表示的是否是合法的数字。当然也可以用 isNaN() 函数来检测算数错误，比如用 0 作除数的情况
!res&&typeof(res)!="undefined"&&res!=0

// 判断是否为NaN
isNaN(res)

// 判断undefined和null 注：null==undefined 说明null和undefined不严格相等
res==null || res==undefined

// 判断undefined、null与NaN 注：一般不那么区分就使用这个足够
!res
```

**3. 通用判断方法（较为严谨， 除NaN外，皆可用此方法判断具体基础类型）**

```javascript
// 该方法适合所有类型判断 注：res为验证的对象 type为js基础数据类型字符串（例如：'String', 'undefined', 'null', 'Number', 'boolean', 'Array', 'Function', ）
toString.call(res).indexof(type)>-1

// 字符串类型
var tmp = '1111'; toString.call(tmp)
"[object String]"

// 数字类型
var tmp = 1111; toString.call(tmp)
"[object Number]"

// 函数类型
var tmp = function(){}; toString.call(tmp)
"[object Function]"

// 布尔类型
var tmp = true; toString.call(tmp)
"[object Boolean]"

// 数组类型
var tmp = []; toString.call(tmp)
"[object Array]"

// 对象类型
var tmp = {}; toString.call(tmp)
"[object Object]"

// NaN被判断为数字类型（需要特殊判断isNaN()）
var tmp = NaN; toString.call(tmp)
"[object Number]"

// undefined
var tmp = undefined; toString.call(tmp)
"[object Undefined]"

// null
var tmp = null; toString.call(tmp)
"[object Null]"

// Symbol类型
var tmp = Symbol('key'); toString.call(tmp)
"[object Symbol]"

// BigInt类型
var tmp = BigInt("9007199254740995"); toString.call(tmp)
"[object BigInt]"
```

**4. 数组类型的检测方法**

```javascript
// instanceof 操作符
var tmp = []; tmp instanceof Array
true

// 对象的 constructor 属性
var tmp = []; tmp.constructor===Array
true

// Array.isArray( ) 检验值是否为数组
var tmp = []; Array.isArray(tmp)
true
```

**5. 特殊的检测方法（转换为布尔值--Boolean()）**

**下面6种值转化为布尔值时为false，其他转化都为true**

**1、undefined（未定义，找不到值时出现）**

**2、null（代表空值）**

**3、false（布尔值的false，字符串"false"布尔值为true）**

**4、0（数字0，字符串"0"布尔值为true）**

**5、NaN（无法计算结果时出现，表示"非数值"；但是typeof NaN==="number"）**

**6、""（双引号）或''（单引号） （空字符串，中间有空格时也是true）**

```javascript
// 进行类型转换时，结果为false的情况(共6种)
Boolean()

// 未定义类型转布尔值：为false——undefined
var un;
var un = undefined;
console.log(Boolean(un));
// ->false

// 字符串类型转布尔值：为false——空字符串
var str = ""
console.log(Boolean(str));
// ->false

// 数值类型转布尔值：为false——0，0.0，-0，NaN
var num = 1;
var num = 0.1;
var num = 0.0;
var num = 0;
var num = NaN;
console.log(Boolean(num));
// ->false

// 对象类型转布尔值：为false——null
var obj = {name:'Allen',age:24};
var obj = {};
var obj = null;
console.log(Boolean(obj));
// ->false

// 对象类型转布尔值：为false——false
var obj = false;
console.log(Boolean(obj));
// ->false
```

**6. 使用instanceof进行实例检测**

**instanceof** **运算符用来测试一个对象在其原型链中是否存在一个构造函数的** **prototype** **属性。**

```javascript
console.log(2 instanceof Number);                    // false
console.log(true instanceof Boolean);                // false 
console.log('str' instanceof String);                // false  
console.log([] instanceof Array);                    // true
console.log(function(){} instanceof Function);       // true
console.log({} instanceof Object);                   // true    
```

> 注意： 直接的字面量值判断数据类型，只有引用数据类型（Array，Function，Object）被精准判断，其他（数值Number，布尔值Boolean，字符串String）字面值不能被instanceof精准判断

**三、最不靠谱的类型检测方式（constructor）**

```javascript
// 为什么不靠谱？请看如下代码
function Fn(){};
 
Fn.prototype=new Array();
 
var f=new Fn();
 
console.log(f.constructor===Fn);    // false
console.log(f.constructor===Array); // true
```

> 注意：如果我创建一个对象，更改它的原型，那么constructor就不靠谱了

