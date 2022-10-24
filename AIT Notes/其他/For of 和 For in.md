# for…in和for…of的用法与区别

[TOC]

##### 一句话概括：for in是遍历（object）键名，for of是遍历（array）键值。

文章的内容大部分来自MDN。

## for...in

`for...in` 循环只遍历可枚举属性（包括它的原型链上的可枚举属性）。像 `Array`和`Object`使用内置构造函数所创建的对象都会继承自`Object.prototype`和`String.prototype`的不可枚举属性，例如 [`String`](https://link.segmentfault.com/?enc=s2CInr5W73tg4U25KJbJIQ%3D%3D.ntEn%2F8KJRhgBnN7sroGcIQNMWVVQdLwuL65N4OcjQQw%2FXgvEzGWpQCVCQoNLz9oQwWHh7Ek0%2FarAANNrSS2RzAJYwmdh66uhlvqzNFMxW8o%3D) 的 [`indexOf()`](https://link.segmentfault.com/?enc=ptXQ0iQEYff06OjKJsp%2F%2FA%3D%3D.VgZxm7htSZRupZlYZc1IE3D2OgT21Xvu7Ia3y79IYMug02WD04b6jpiiMBBlKJxullMakuvFrvohyn776LVtoaTY02PVPmdH43oLE8bt3DT4MoG1aIe5I2kqhAXUToom) 方法或 [`Object`](https://link.segmentfault.com/?enc=WuMZSCZ8PEgSnRz0ZHivkA%3D%3D.GzAVt%2BEsbtEMjg4QQDLJx4nQXWQrfjfBEjz%2Brv9RomcbVjqpL9wQvL%2FIHA6q%2BZs6SGYS2InZV9Ygd6HxZcDJKaixZ177e3MJqrq%2BaK%2B9f5q1yY2coBBUkVWWn3G5bipS)的[`toString()`](https://link.segmentfault.com/?enc=HB3t4ABBGjMfh67vaj6kwQ%3D%3D.1Aw2ARYvAr25aJozQAX5RM6g8KR9AZsBFezN24UXgubvOSxhokdZZQQQ38lJ7shE1FShtHvN3MgTVHXLeoCL9vX3%2BeNV5zeVpvDRJbf8AW%2BeF1bfxYqGQftn2x32LnUme%2BgZwyao2aRd%2FItykOj85w%3D%3D)方法。循环将遍历对象本身的所有可枚举属性，以及对象从其构造函数原型中继承的属性（更接近原型链中对象的属性覆盖原型属性）。

```arcade
var obj = {a:1, b:2, c:3};
    
for (let key in obj) {
  console.log(key);
}

// a
// b
// c
```

## for...of

**`for...of`语句**在[可迭代对象](https://link.segmentfault.com/?enc=5EeigbCmEk6V4xosSraZVA%3D%3D.V15ooZMqx9YUyblqNztCXPf2%2FazwQjtRZ41CQK9CKchKhmfyJaT4ZdA87aiTgttIadx0BgUPGldKNehajuVcZ9cST6R2%2BCS0urP%2BWajW%2F34%3D)（包括[`Array`](https://link.segmentfault.com/?enc=4H2fqOG7l23wm1wwvmGx6Q%3D%3D.lELl6zDb%2FWeqY%2FReAuN0Mi5tqtDjy9i%2BJb4sIfeueHo9grektlFQkHxlk59YMs00YAKH%2FP%2BCPWhigE4UmNqN0Qh%2F8laisnahVrFDX8OJSGc%3D)，[`Map`](https://link.segmentfault.com/?enc=oEK6EIr17fC09gqWH4tu3g%3D%3D.u8d3KKCyDSkwOIHSCG1Yp7EXH%2Fxypi%2F1mH8a86nEwIANytGcxsJsgPlyUeFghJ9bndbwaMJyip0qY1VECjL93a1Ey%2F0KZtDl5U7y%2BMk%2BPK4%3D)，[`Set`](https://link.segmentfault.com/?enc=fD1hbrr8ez7aO0xuqX%2F6Cg%3D%3D.zizmYS4omT6RJVlb%2BexiS8JZR32BcbzlShk%2FQj4afFJMCLPM6vDkWIbPI0zrHw2Z6w9FVQgyIqrq1edikjET3fLUEhQg7YlJLZKfZEfiBWJ%2BWhOLoVDARMku%2B%2FzjTFrZ)，[`String`](https://link.segmentfault.com/?enc=Kt5ebGAD3oGPxj%2FEOv%2FD8A%3D%3D.upUHiFeCcv5bWgdp8m0%2BJxKctFZMzZWatjGwDRuV3wSJE4mgrCJLSJu0TqZsijVpTnuLae%2B0MlHZIYT5taNqPMpEjbEEJkAtdzNmQV1HnnY%3D)，[`TypedArray`](https://link.segmentfault.com/?enc=YkMIbLw%2BmsnydYK8hQXHpA%3D%3D.arIxIx9MJxA0P%2BH591aGtJM%2BMysMv51LjZPDYMF32%2B3sGCcqMhWga5g1Md652St%2BwOnhKV%2BOL8tRXi5H7wZN4KymOki%2FtUbvF54rWyggopOqBap%2BMP%2BB0kVFvJvRYov3)，[arguments](https://link.segmentfault.com/?enc=sCCud2Rf08D%2FtozQKeeVug%3D%3D.YGt4%2Fx7DZoTKvYKyGh%2FTgRpE2ucEUjQq56F9HBKduCZmIIzQ9Vbeq7exOjdCtNFmW12qV8%2BW3nTe9jNNP7%2Bfk%2Bs%2BDdjYLRwwlQYAkf0QDx3wgrskRyguwkO1sQZHFHdRaGmz3c3C1dmQXI1DVso6zQ%3D%3D) 对象等等）上创建一个迭代循环，调用自定义迭代钩子，并为每个不同属性的值执行语句

```kotlin
const array1 = ['a', 'b', 'c'];

for (const val of array1) {
  console.log(val);
}

// a
// b
// c
```

**for of不可以遍历普通对象**，想要遍历对象的属性，可以用for in循环, 或内建的Object.keys()方法

## for...of与for...in的区别

无论是`for...in`还是`for...of`语句都是迭代一些东西。它们之间的主要区别在于它们的迭代方式。

[`for...in`](https://link.segmentfault.com/?enc=X67WP%2FilNqC4LIbo%2B%2Flung%3D%3D.ZetsHTJvJcuA2VfIy1jg7GZjkdCCwqMrNo0XUf2NvV1zwfSl6TKehbsE96%2FxfH%2FkT5T6KSDhA64o6GPuQo7PVCzcNmguyPePFBKdyhnm%2BLVbfFQv4c5VYJChWeHVsiOj)语句以任意顺序迭代对象的[可枚举属性](https://link.segmentfault.com/?enc=p2sOidmirOmwpIWpOIXhSg%3D%3D.Artua8WsWIM0GXmmtrzYpx0RFLGPhsvayI83NXsPgNboraHjvHEBqxkXbhWMselX2o7tezygHvED0%2F2HwsqTyXMsbEkuR809gmw7LC6CztKdwMdGRnA2hRjC9HdAE%2Fo0EsDQQ2TshyGuuuzfuIsuYQ%3D%3D)。

`for...of` 语句遍历[可迭代对象](https://link.segmentfault.com/?enc=VYS3Hf5oKgMdiZFpfKGKgg%3D%3D.u3JXxiaLJf46DOo%2FHGuovQ5rvFixQNsh7x7ZyUULTv5MaQTqJplNcJStCYjzmIwET7GezCf9lE%2FoCsexhaTJvU0ykoXQiZR0ts6i%2FxZnkiqSfi7VngLkcAOsoM4LO%2Ff6yMAwveNzhViBnweX38FTqw%3D%3D)定义要迭代的数据。

以下示例显示了与[`Array`](https://link.segmentfault.com/?enc=ossSZj6lfFSK%2BRL%2BEGl%2BkQ%3D%3D.eVA2mz5Lso4hgvW60%2B4EYpPoEadm%2BlVd8xjPG%2F3BeVaxqZheh2Bw2un17FB7lvtXtLJNM0QbJ99eaht%2BLX030B2jYaW3bE%2FTk6yeudD%2FAv8%3D)一起使用时，`for...of`循环和`for...in`循环之间的区别。

```javascript
Object.prototype.objCustom = function() {}; 
Array.prototype.arrCustom = function() {};

let iterable = [3, 5, 7];
iterable.foo = 'hello';

for (let i in iterable) {
  console.log(i); // 0, 1, 2, "foo", "arrCustom", "objCustom"
}

for (let i in iterable) {
  if (iterable.hasOwnProperty(i)) {
    console.log(i); // 0, 1, 2, "foo"
  }
}

for (let i of iterable) {
  console.log(i); // logs 3, 5, 7
}
```

总结：**for in 一般用来遍历对象的key**、**for of 一般用来遍历数组的value**

## 用 for of 遍历 object需要用Object.entries

```javascript
const object1 = {
  a: 'somestring',
  b: 42
};

for (const [key, value] of Object.entries(object1)) {
  console.log(`${key}: ${value}`);
}

// expected output:
// "a: somestring"
// "b: 42"

```

