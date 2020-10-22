JavaScript的可迭代对象

1）数组Arrays

console.log([][Symbol.iterator])

 

for(let x of ['a','b'])

  console.log(x)

2）字符串Strings

console.log(""[Symbol.iterator])

for(let x of "abc")

  console.log(x)

3）Map

let map = new Map().set('a', 1).set('b', 2);

console.log(map[Symbol.iterator]);

for (let pair of map) {

  console.log(pair);

}

4）Set

let set = new Set().add('a').add('b');

for (let x of set) {

  console.log(x);

}

5）arguments

function printArgs() {

  for (let x of arguments) {

​    console.log(x);

  }

}

printArgs('a', 'b');

6）Typed Arrays

7）Generators，ES6新增加