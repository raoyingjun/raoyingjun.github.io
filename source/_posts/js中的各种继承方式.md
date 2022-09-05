---
title: js中的各种继承方式
date: 2022-2-22 0:35:27
tags: 前端
categories: 前端
---

### 原型链继承

利用原型链实现继承，是通过子类原型引用父类实例来实现对父类的继承，具体实现示例如下

```javascript
function Super() {
    this.name = 'Rose'
}

function Sub() {
}

// 子类原型引用父类实例来实现对父类的继承
Sub.prototype = new Super()
```

优点

* 子类可以继承父类的属性和方法

缺点

* 由于原型对象上的引用值是在实例中共享的，因此属性一般是定义在构造函数中。在父类构造函数中定义的引用值，作为原型对象被子类实例共享，这种情况是不应该的
* 子类实例化无法给父类构造函数传参

### 盗用构造函数继承

通过 `call()` 和 `apply()` 方法盗用 `this` 实现继承，具体实现示例如下

```javascript
function Super(name) {
    this.name = name
}

function Sub(name) {
    // 盗用 this 实现继承
    Super.call(this, name) // or Super.apply(this)
}
```

优点

* 可以向父类构造函数传参
* 子类可以继承父类构造函数上的属性和方法

缺点

* 子类无法访问父类原型上的方法
* 在父类构造函数中定义的方法不能重用。每一个子类实例都会拷贝一份在父类构造函数中定义的方法，无法像原型一样共用

### 组合继承（常用的继承方式）

结合原型链继承和盗用构造函数继承，具体实现示例如下

```javascript
function Super(name) {
    this.name = name
}

function Sub(name, age) {
    // 盗用 this 实现继承
    Super.call(this, name, age) // or Super.apply(this, [name, age])
    this.age = age
}

// 子类原型引用父类实例来实现对父类的继承（一般是继承原型上定义的方法，属性通常不会定义在原型对象上）
Sub.prototype = new Super()
```

优点

* 弥补了原型链继承和盗用构造函数继承的不足
* `instanceof` 操作符和 `isPrototypeOf` 方法正常有效

缺点

* 父类构造函数会被执行两次。一次是调用 `Super.call(this, name, age)`，另一次是 `Sub.prototype = new Super()`

### 原型式继承

不使用构造函数来实现继承，而是通过原型来实现对象之间的信息共享，具体实现示例如下

```javascript
let prototype = {
    name: 'Nickname',
    hobbys: ['song', 'jump']
}
// 方式一
let rose = Object.create(prototype); // 创建以 prototype 作为原型对象的对象
rose.name = 'Rose'
rose.hobbys.push('basketball')
// 方式二
let jack = Object.create(prototype, { // 创建以 prototype 作为原型对象的对象
    name: {
        value: 'Jack',
    }
})

```

优点

* 适用于不需要创建构造函数但仍需要在对象之间共享信息的场景。利用 `Object.create()` 创建一个以指定对象为原型的对象，通过这个指定的原型对象共享信息

缺点

* 原型中的引用值在相关对象之间也是共享的，跟原型链继承类似

### 寄生式继承

结合原型式继承和工厂函数实现继承，包装一层函数实现继承，然后增强该对象并返回，具体实现示例如下

```javascript
// 使用工厂函数创建对象
function createPerson(prototype) {
    // 创建以 prototype 作为原型对象的新对象
    const instance = Object.create(prototype)
    // 添加属性或方法增强新对象
    instance.sayName = function () {
        console.log(instance.name)
    }
    // 添加属性或方法增强新对象
    instance.age = 18
    return instance // 返回新对象
}

let prototype = {
    name: 'Nickname',
    hobbys: ['song', 'jump']
}
// 调用工厂函数传入指定原型对象，创建并返回增强后的对象
const rose = createPerson(prototype)

```

优点

* 适用于不在乎类型和构造函数的场景，适用于只关注对象的情况

缺点

* 通过这种继承方式添加的函数难以复用，与构造函数模式类似。在构造函数模式中定义的属性和方法都被拷贝到其对象实例上，导致方法也是难以重用

### 寄生式组合继承（最佳方案）

通过盗用构造函数继承属性，混合原型式继承来继承方法，利用寄生式继承的方式来继承父类的原型，然后将返回的新对象赋值给子类原型，具体实现示例如下

```javascript
function Super(name) {
    this.name = name
}

function Sub(name) {
    // 盗用构造函数继承属性
    Super.call(this, name) // or Super.apply(this)
}

// 混合原型式继承来继承方法
Sub.prototype = Object.create(Super.prototype);
// 由于上面重写原型导致默认 constructor 属性丢失，我们这里手动设置一下
Sub.prototype.constructor = Sub
```

我们将上面的代码整理封装下，改写后如下示例：

```javascript
/**
 * 子类继承父类
 * @param {Function} Sub 子类
 * @param {Function} Super 父类
 */
// 包装成实现继承的函数
function inheritPrototype(Sub, Super) {
    // 原型式继承来继承方法
    const subPrototype = Object.create(Super.prototype)
    // 由于上面重写原型导致默认 constructor 属性丢失，我们这里手动设置一下
    subPrototype.constructor = Sub
    // 将上面创建的新对象 subPrototype 赋值给子类原型，后续直接在子类原型上添加方法或属性增强该对象即可
    Sub.prototype = subPrototype
}

function Super(name) {
    this.name = name
}

function Sub(name, age) {
    // 盗用构造函数继承属性
    Super.call(this, name) // or Super.apply(this)
    this.age = age
}

// 子类 Sub 继承父类 Super
inheritPrototype(Sub, Super)
```

优点

* 只调用一次父类构造函数
* 避免了在子类原型上创建不必要的属性。像组合继承中，子类原型是通过引用父类实例作为原型来继承，不可避免的多余了不必要的属性
* `instanceof` 操作符和 `isPrototypeOf` 方法正常有效



