# 第九章 JS的类

## ES5中的仿类解构

``` JS
        function A() {};
        A.prototype.name = 'tom';
        A.prototype.sayName = function () {
            return 'hahaha';
        }
        var b = new A();
        console.log(b.name);    // tom
        console.log(b.sayName);   // f () {return 'hahahhah';}
        console.log(b.sayName());   // hahaha
```

## 类的声明

**私有属性**；在class中实现私有属性，在构造方法内定义`this.xx=xx;`。

``` js
  class Boy {
            constructor(){  // 新建构造函数
                this.name = 'y31'; // 私有属性
                this.age = 22 ;
            }
            sayAge() {   // 定义方法并赋值给了原型
              return this.age;
            }
        }
        let man = new Boy();
        console.log(man.name);
        console.log(man.sayAge());
```

类声明和函数声明的区别

1. 类声明不能提升，函数声明可以。
2. 类声明代码在严格模式下运行。
3. 类中的方法都不可枚举。
4. 每个都类都有`[[construct]]`方法。
5. 只能使用`new`来调用类的构造函数。
6. 不能在类中修改类名。

## 类表达式

``` js
class Boy {}
let Person = class Boy {}   // Person在外部使用，Boy只能在内部使用
let Person = Class{}
```

## 作为一等公民的类

能够被当作值使用的可称为一等公民，类与函数一样均是“一等公民”。

``` js
        class A {
            sayHi(){
                return 'Hi';
            }
        }
        function B() {
            return new A();
        }
        let b = new B();
        console.log(b.sayHi());    // Hi
```

可用于创建单例

``` js
        let what = 'xixixi';
        let word = new class {
            constructor(what){
                this.what = what ;
            }
            sayWhat(){
               console.log(this.what);
            }
        }(what);
        word.sayWhat();
```

## 访问器属性

类支持在原型上定义访问器属性

``` js
    class A {
      constructor(state) {
        this.state = state
      } 
      get myName() {   // 创建getter
        return this.state.name
      }
      set myName(name) {    // 创建setter
        this.state.name = name
      }
    }
```

## 可计算成员名

类方法和类访问器属性都可以使用可计算的名称。

``` js
let name = 'method',name2 = 'method2';
class A = {[name](){console.log('hahah')} set [name2]{}}
```

## 生成器方法

类中可以创建生成器方法

``` js
    class A {
      *printId() {
        yield 1;
        yield 2;
        yield 3;
      }
      render() {
        return this.printId()
      }
    }
    let a = new A()
    console.log(a.render().next()) // {done: false, value: 1}
```



## 静态成员

静态成员值在方法或属性名前加上`static`，静态成员不能在实例中访问，只能在**类**中直接访问。

``` js
        class A {
            constructor(){
               this.name = 'Jay' ;
               
            }
            static sayHi(){
                return 'Hi';
            }
        }
        let a = new A();
       // console.log(a.sayHi());  no
        console.log(A.sayHi());   // Hi
```

## 使用派生类继承

A称为派生类，如果派生类要使用构造方法，就必须使用super();

``` js
    class A extends Component {
       constructor(props){
           super(props)
       }
    }
```

只能在派生类中使用super，要在访问this前调用，如果不想调用super，构造函数可以返回一个对象。

### 类方法遮蔽

继承的类可以重写父类的方法。

### 静态成员继承

静态成员可以通过派生类访问。

### 从表达式中派生类

任意表达式都能在 `extends` 关键字后使用，只要该函数有`[[Construct]]`以及原型。

### 继承内置对象

### Symb.species 属性

## 在类构造器中使用 new.target

