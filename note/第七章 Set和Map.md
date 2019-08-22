# 第七章 Set和Map

## ES5中的Set和Map

对象的属性值只能是字符串，key2和key3都被转换为同一个字符串"[object Object]"，因此会指向同一个属性（被后面的对象覆盖）。

``` js
        let key1 = {};
        let key2 = {};
        let key3 = {};
        key1[key2] = "hahah";
        key1[key3] = "aaaas";
        console.log(Object.keys(key1));  //["[object Object]"]
        console.log(key1[key2]);  // aaaas
```

## ES6的Set

ES6新增了Set类型，无重复值（数值，字符串，null）的有序列表。

```JavaScript
let set = new Set();
```

常用方法（支持forEach）

```js
        let set = new Set();
        set.add('haha'); // add() 向Set对象尾部添加元素
        set.add(Symbol('haha'));
        console.log(set.size); //2    // 返回Set对象元素的个数
        console.log(set.has('haha')); // true    //返回布尔值，表示该值是否存在
        set = new Set([1, 2, 2, '3', '3']);
        console.log(set); // {1, 2, "3"} 数组转换为Set并去除数组中重复值
        console.log(Array.from(set)); //[1, 2, "3"] 转换为数组 还有array = [...set];
        set.delete(2);
        console.log(set); //  {1, "3"} delete()方法删除单个值
        set.clear();
        console.log(set); //  {} clear()方法清楚所有值
```

Weak Set集合,只能存放对象值（不能存放原始值），不能被枚举，弱引用，如果没有其它变量属性引用该对象，则该对象值会被回收（Set中会始终存在）。

```JavaScript
let set = new Set(),
    key = {};
	set.add(key);
	key = null;
	key = [...set][0];   // 可重新取回原来的对象
```

```js
    let set = new WeakSet();
    const class_1 = {}, class_2 = {};
    set.add(class_1);
    set.add(class_2);
    console.log(set) // WeakSet {Object {}, Object {}}
    console.log(set.has(class_1)) // true
    console.log(set.has(class_2)) // true
```

##  ES6中的Map

Map存储键值的有序列表，key和value支持所有数据类型。

``` js
        let map = new Map(),k = {};
        map.set("a",1);
        map.set(k,k);
        console.log(map.get(k));  // {}
        console.log(map.get("a"));   // 1
		map.delete(k);
        console.log(map.get(k));  // undefined Map中没有枚举，因此也没有clear()方法
```

Weak Map，与弱Set相似，所有的键必须是对象。

```JavaScript
let map = new WeakMap(),
```

