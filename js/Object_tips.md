* Object.keys方法 Object.keys方法是JavaScript中用于遍历对象属性的一个方法 。它传入的参数是一个对象，返回的是一个数组，数组中包含的是该对象所有的属性名
```
    var cat= { 
        name:’mini’, 
        age:2, 
        color:’yellow’, 
        desc:”cute” 
    }
    console.log(Object.keys(cat)); // ["name", "age", "color", "desc"]
```

* Object.values()方法 Object.values方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（ enumerable ）属性的键值。
```
    var obj = { foo: "bar", baz: 42 };  
    Object.values(obj)  
    // ["bar", 42] 
```

* Object.create(proto, [propertiesObject])  
```
    proto 新创建对象的原型对象   
    propertiesObject 可选。如果没有指定为 undefined，
                        则是要添加到新创建对象的可枚举属性（即其自身定义的属性，而不是其原型链上的枚举属性）
                        对象的属性描述符以及相应的属性名称。这些属性对应Object.defineProperties()的第二个参数。
    返回值 一个新对象，带着指定的原型对象和属性
```

* Object.hasOwnProperty()方法 判断对象自身属性中是否具有指定的属性。 这个方法是不包括对象原型链上的方法的属性

* Object.assign: 将所有可枚举属性的值从一个或多个对象复制到目标对象，并返回目标对象

* Object.defineProperty: 定义或修改一个对象中的属性

* Object.defineProperties: 定义或修改一个对象中的多个属性

* Object.getOwnPropertyDescriptor: 获取一个对象中的一个属性描述

* Object.getOwnPropertyDescriptors: 获取一个对象中的所有属性描述

```
    /*
    * 数据属性
    * [[Configurable]]: 能否通过delete删除此属性，能否修改属性的特征
    * [[Enumerable]]: 该属性是否可枚举，即是否可通过for-in或Object.keys()返回属性
    * [[Writable]]: 能否修改属性的值
    * [[Value]]: 该属性的值，默认为undefined
    *
    * 访问器属性
    * [[Configurable]]、[[Enumerable]] 和数据属性一致
    * [[Get]]: 提供一个 getter 方法，访问对象属性时会调用该方法
    * [[Set]]: 提供一个 setter 方法，读取对象属性时会调用该方法
    */
```

* Object.entries: 返回一个对象自身可枚举属性的键值对，顺序与for-in循环时的顺序一致

* Object.freeze: 冻结一个对象(只有一层)，不能修改任何信息，包括新增属性、删除属性、修改属性值

* Object.isFrozen: 判断一个对象是否已经被冻结

* Object.getOwnPropertyNames: 获取一个对象所有属性的key值(包括不可枚举属性，不包括Symbol属性)

* Object.getOwnPropertySymbols: 获取一个对象所有Symbol属性

* Object.isPrototypeOf: 判断一个对象是否在某个对象的原型链上