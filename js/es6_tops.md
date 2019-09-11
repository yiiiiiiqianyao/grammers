# Proxy ES6 原生提供 Proxy 构造函数，用来生成 Proxy 实例  

    作为构造函数，Proxy接受两个参数  
    第一个参数是所要代理的目标对象  
    第二个参数是一个配置对象，对于每一个被代理的操作，需要提供一个对应的处理函数，该函数将拦截对应的操作  

```
    var proxy = new Proxy(target, handler)  // 如果handler没有设置任何拦截，那就等同于直接通向原对象
```

# Proxy 支持的拦截操作一共 13 种

* get(target, propKey, receiver)：拦截对象属性的读取，比如proxy.foo和proxy['foo']
```
    get: function (target, key, receiver) {
        console.log(`getting ${key}!`);
        return Reflect.get(target, key, receiver);  // return key
    }
```
* set(target, propKey, value, receiver)：拦截对象属性的设置，比如proxy.foo = v或proxy['foo'] = v，返回一个布尔值
```
    set: function (target, key, value, receiver) {
        console.log(`setting ${key}!`);
        return Reflect.set(target, key, value, receiver);
    }
```
* has(target, propKey)：拦截propKey in proxy的操作，返回一个布尔值
* deleteProperty(target, propKey)：拦截delete proxy[propKey]的操作，返回一个布尔值
* ownKeys(target)：拦截Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy)、for...in循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而Object.keys()的返回结果仅包括目标对象自身的可遍历属性
* getOwnPropertyDescriptor(target, propKey)：拦截Object.getOwnPropertyDescriptor(proxy, propKey)，返回属性的描述对象
* defineProperty(target, propKey, propDesc)：拦截Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值
* preventExtensions(target)：拦截Object.preventExtensions(proxy)，返回一个布尔值
* getPrototypeOf(target)：拦截Object.getPrototypeOf(proxy)，返回一个对象
* isExtensible(target)：拦截Object.isExtensible(proxy)，返回一个布尔值
* setPrototypeOf(target, proto)：拦截Object.setPrototypeOf(proxy, proto)，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截
* apply(target, object, args)：拦截 Proxy 实例作为函数调用的操作，比如proxy(...args)、proxy.call(object, ...args)、proxy.apply(...)
* construct(target, args)：拦截 Proxy 实例作为构造函数调用的操作，比如new proxy(...args)

# Reflect 对象是对代替 Object 而设计的新 api

    ```
        // 老写法
        try {
            Object.defineProperty(target, property, attributes);
            // success
        } catch (e) {
            // failure
        }

        // 新写法
        if (Reflect.defineProperty(target, property, attributes)) {
            // success
        } else {
            // failure
        }
    ```

# Array.from()  用于将两类对象转为真正的数组 
1. 类似数组的对象（array-like object）
2. 可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）
    ```
        let arrayLike = {
            '0': 'a',
            '1': 'b',
            '2': 'c',
            length: 3
        };
        Array.from(arrayLike )
        // ['a', 'b', 'c']
    ```

# Array.of() 用于将一组值，转换为数组

    Array.of总是返回参数值组成的数组。如果没有参数，就返回一个空数组

    ```
        Array.of() // []
        Array.of(undefined) // [undefined]
        Array.of(1) // [1]
        Array.of(1, 2) // [1, 2]
    ```
    
# 数组实例的 entries()，keys() 和 values() 

* keys()是对键名的遍历
    ```
        for (let index of ['a', 'b'].keys()) {
            console.log(index);
        }
        // 0
        // 1
    ```
* values()是对键值的遍历
    ```
        for (let elem of ['a', 'b'].values()) {
            console.log(elem);
        }
        // 'a'
        // 'b'
    ```
* entries()是对键值对的遍历
    ```
        for (let [index, elem] of ['a', 'b'].entries()) {
            console.log(index, elem);
        }
        // 0 "a"
        // 1 "b"
    ```

# 数组实例的 flat()，flatMap() 
* flat 用于将嵌套的数组“拉平”，变成一维的数组
flat()默认只会“拉平”一层，如果想要“拉平”多层的嵌套数组，可以将flat()方法的参数写成一个整数，表示想要拉平的层数，默认为1

```
    [1, 2, [3, [4, 5]]].flat()
    // [1, 2, 3, [4, 5]]

    [1, 2, [3, [4, 5]]].flat(2)
    // [1, 2, 3, 4, 5]
```

* flatMap 对原数组的每个成员执行一个函数（相当于执行Array.prototype.map()），然后对返回值组成的数组执行flat()方法

# Set
* Set 实例的属性和方法
```
    Set.prototype.constructor：构造函数，默认就是Set函数。
    Set.prototype.size：返回Set实例的成员总数。
    Set.prototype.add(value)：添加某个值，返回 Set 结构本身。
    Set.prototype.delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
    Set.prototype.has(value)：返回一个布尔值，表示该值是否为Set的成员。
    Set.prototype.clear()：清除所有成员，没有返回值。
```
* 使用 Set 可以很容易地实现并集（Union）、交集（Intersect）和差集（Difference）
```
    let a = new Set([1, 2, 3]);
    let b = new Set([4, 3, 2]);

    // 并集
    let union = new Set([...a, ...b]);
    // Set {1, 2, 3, 4}

    // 交集
    let intersect = new Set([...a].filter(x => b.has(x)));
    // set {2, 3}

    // 差集
    let difference = new Set([...a].filter(x => !b.has(x)));
    // Set {1}
```

# Map

* Map 结构的实例有以下属性和操作方法

* size 属性
* Map.prototype.set(key, value)
* Map.prototype.get(key)
* Map.prototype.has(key)
* Map.prototype.delete(key)
* Map.prototype.clear()
