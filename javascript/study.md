
- [1 多个js有同名函数按照最后引入的为准](#1-多个js有同名函数按照最后引入的为准)
- [2 var let const区别](#2-var-let-const区别)
- [3 数据类型](#3-数据类型)
- [4 乘法规则](#4-乘法规则)
- [5 typeof Array 和Object都是显示object](#5-typeof-array-和object都是显示object)
- [6 for in 遍历数组和对象](#6-for-in-遍历数组和对象)
- [7 对象](#7-对象)
- [8 函数](#8-函数)
- [9 事件](#9-事件)
- [10 JavaScript == 与 === 区别](#10-javascript--与--区别)
- [11 js中的foreach用法](#11-js中的foreach用法)
- [12 类型转换](#12-类型转换)
- [13 正则表达式](#13-正则表达式)
- [14 变量提升](#14-变量提升)
- [15 this注意事项](#15-this注意事项)
- [16 ES6 class](#16-es6-class)
- [16  console.log注意事项](#16--consolelog注意事项)
- [17 异步编程](#17-异步编程)
### 1 多个js有同名函数按照最后引入的为准

- 1 查找是否有外部引入的js文件

- 2 如果没有那么转到第3步，如果有，那么按照引入顺序首先检查a.js中是否有函数名为F的函数，找到那么记录，并且继续在该文件中查找，如果有同样的F函数名(注意这里只管函数名，不管参数和返回值)，如果有则覆盖前面的记录，直到该文件末尾，最后实际调用的就是该文件中的最后一个函数；如果在a.js中没有找到F函数名一样的函数，那么查找b.js文件中是否有F函数，处理和a.js中一样。如果最终在外部引入的js文件中都没有找到该函数，那么转到下面第3步

- 3 在本html内部按照顺序查找是否有F函数，如果没有，出错处理；如果有同样按照后面覆盖前面的原则进行函数调用。

###  2 var let const区别

- 1 作用域不一样，var相当于全局，后声明会把前面的覆盖， let则会报错，let 变量如果在块内声明，则只在块内生效
- 2 const不能修改

###  3 数据类型

- var length = 16;                      						                 // Number 通过数字字面量赋值
- var points = x * 10;                                                         // Number 通过表达式字面量赋值
- var lastName = "Johnson";                                            // String 通过字符串字面量赋值
- var cars = ["Saab", "Volvo", "BMW"];                           // Array 通过数组字面量赋值
- var person = {firstName:"John", lastName:"Doe"};  // Object 通过对象字面量赋值 

### 4 乘法规则

```javascript
// 如果a或者b中包含非数字，输出为NaN, 否则就算是字符串也会解析成数字进行计算
function multiply(a, b) {
  return a * b;
}
```



### 5 typeof Array 和Object都是显示object

```javascript
  var arr = [1, 2, 3]
  var obj = {
    value:123,
	label:"123"
  }
  console.log(typeof(arr)) // object
  console.log(typeof(arr)) // object
  console.log(Array.isArray(arr)) // true
```

###  6 for in 遍历数组和对象

```javascript
    var arr = [3, 2, 1]
    var obj = {
        value:123,
        label:"123"
    }
    for (let item in arr) { // let可以省略
        console.log(item, arr[item])
    }
    for (item in obj) {
        console.log(item, obj[item])
    }
```

### 7 对象

- 对象访问

  ```javascript
  var person = {
      firstname: "John",
      lastname: "Doe",
      id: 5566
  };
  console.log(person.firstname)    // right
  console.log(person["firstname"]) // right
  console.log(person[firstname])   // wrong, 需要加引号，属性是字符串
  ```

  

- 对象创建

  ```javascript
  // 第一种
  function Demo(){
      var obj=new Object();
      obj.name="张思";
      obj.age=12;
      obj.firstF=function(){
      }
      obj.secondF=function(){
      }
      return obj;
  }
  var one=Demo();
  
  // 第二种
  function Demo(){
      this.name="张思";
      this.age=12;
      this.firstF=function(){
      }
      this.secondF=function(){
      }
  }
  var one=new Demo
  ```



- javaScript对象中属性具有唯一性（这里的属性包括方法），如果有两个重复的属性，则以最后赋值为准
- 如果您把值赋给尚未声明的变量，该变量将被自动作为 window 的一个属性,非严格模式下给未声明变量赋值创建的全局变量，是全局对象的可配置属性，可以删除。
    ```javascript
        var var1 = 1; // 不可配置全局属性
        var2 = 2; // 没有使用 var 声明，可配置全局属性
        console.log(this.var1); // 1
        console.log(window.var1); // 1
        console.log(window.var2); // 2
        delete var1; // false 无法删除
        console.log(var1); //1
        delete var2; 
        console.log(delete var2); // true
        console.log(var2); // 已经删除 报错变量未定义
    ```
- 对象定义简写, es6简写方式，假如属性和变量名一样，可以省略，包括定义对象方法function也可以省略；
    ```javascript
        // 之前JavaScript的写法
		let obj = {
			name: name,
			sex: sex,
			getName: function(){
				return this.name;
			}
		}
		// ES6的写法
		let obj2 = {
			name,
			sex,
			getName(){
				return this.name;
			}
		}
    ```
- 模板字符串
    ```javascript
    
		let obj = {goodName: "衬衫",price: "九磅十五便士"};
		// 之前JavaScript的写法
		let str = "商品：" + obj.goodName + ",价格：" + obj.price;
		console.log(str);
		
		// ES6写法
		let es6str = `商品:${obj.goodName},价格:${obj.price}`;
    
    ```
### 8 函数
- 箭头函数, 
    - 常见定义方式, 主要是省了function
        ```javascript
            // 原来定义
            function test(a, b){
                console.log(a, b)
            }
            let test = function (a, b) {
                console.log(a, b)
            }
        
            // es6写法
            // 有多个参数， 可以省略function关键字
            let test = (a, b) => {
                console.log(a, b)
            }
            // 一个参数多条语句，可以省略参数的括号
            let test = a => {
                console.log(a)
                console.log(a)
            }
            // 一个参数一条语句， 可以省略大括号
            let test = a => console.log(a)
            // 没有参数, = 号还是不能省略的
            let test = () => console.log(a)
        ```
        
    - 关于this, 箭头函数没有自己的this，箭头函数的this不是调用的时候决定的，而是在定义的时候所在的对象就是它的this；箭头函数的this看外层是否有函数，如果有，外层函数的this就是内部调用箭头函数的this；如果没有，则this是window
    
    - 参数， arguments参数
    
        ```javascript
        function test() {
        	console.log(arguments)
        }
        ```
    
    - 默认参数 `function test(name = "blakeyi")`
    
    - 闭包，匿名函数经常被人误认为是闭包（closure）。闭包指的是那些引用了另一个函数作用域中变量的函数，通常是在嵌套函数中实现的
    
        ```javascript
        function createComparisonFunction(propertyName) {
            return function (object1, object2) {
                let value1 = object1[propertyName];
                let value2 = object2[propertyName];
                if (value1 < value2) {
                    return -1;
                } else if (value1 > value2) {
                    return 1;
                } else {
                    return 0;
                }
            };
        }
        let stu1 = {
            age:20
        }
        let stu2 = {
            age:21
        }
        let compare = createComparisonFunction("age")
        console.log(`${compare(stu1, stu2) == -1 ? "stu1" : "stu2"}`)
        ```
    
        

### 9 事件
- 种类，[更多点击此处](https://www.runoob.com/jsref/dom-obj-event.html)
    - onchange	HTML 元素改变
    - onclick	    用户点击 HTML 元素
    - onmouseover	用户在一个HTML元素上移动鼠标
    - onmouseout	用户从一个HTML元素上移开鼠标
    - onkeydown	用户按下键盘按键
    - onload	    浏览器已完成页面的加载

    ```javascript
        // 在onload的时候添加事件监听，不推荐
        window.onload = () => {
            let btn = document.getElementById("btn")
            btn.addEventListener("click", () => {
                console.log("click")
            })
            btn.addEventListener("mouseover", () => {
                console.log("mouseover")
            })
        }
        // 直接在dom上绑定事件
        <button id="btn" onclick="handleClick()">点我</button>
    ```

### 10 JavaScript == 与 === 区别
- 尽量使用 === 和 !==
- 高级类型不适用 === 和 == 来判断，自己写比较函数
    ```javascript
        // 类型比较
        // 基础类型, number, string
        let num = 111
        let str = "111"
        console.log(num == str)  // 类型不同，值相同, 结果为 true
        console.log(num === str) // 类型不同，结果直接为 false
    
        console.log(num != str)  // 类型不同，值相同, 结果为 false
        console.log(num !== str) // 类型不同，结果直接为 true
    
        // 高级类型, array,object, 建议自己写比较函数, 如isObjEqual
    
        let arr = ["123", "abc"]
        let obj = {
            123:"123",
            abc:"abc"
        }
        let obj1 = {
            123:"123",
            abc:"abc"
        }
        console.log(arr == obj)     // false
        console.log(arr === obj)    // false
        console.log(obj == obj1)    // false
        console.log(obj === obj1)   // false
    
        console.log(isObjEqual(obj, obj1)) // true
        
        // 自定义比较函数，可以根据需求指定需要比较的字段
        const isObjEqual = (obj1, obj2) => {
            let keys1 = Object.keys(obj1)
            let keys2 = Object.keys(obj2)
            // 先判断属性数量
            if (keys1.length !== keys2.length) {
                return false
            }
            for (let key of keys1) { // 注意 for in(遍历key) 和for of(遍历value)的区别
                if (obj1[key] !== obj2[key]) {
                    return false
                }
            }
            return true
        }
    ```
### 11 js中的foreach用法
- 主要对数组遍历使用
    ```javascript
        // 数组遍历
        let arr = [111, 222, 333]
        // 注意value在前，index在后
        arr.forEach(function(value, index, arr){
            console.log(index, value, arr)
        })
        // 只接收value
        arr.forEach(function(value){
            console.log(value)
        })
        // es6新写法
        arr.forEach((value, index) => {
            console.log(index, value)
        })
    
        // 对象遍历, 和数组遍历不同，还不如直接用for in或者 for of
        let obj = {
            name:"blakeyi",
            sex:"male"
        }
        Object.keys(obj).forEach(function(value){
            console.log(`attr: ${value}, value: ${obj[value]}`)
        })
    ```

### 12 类型转换
```javascript
    // 数字和字符串互转
    let num = 110
    let str = "222"
    console.log(String(num))    // 转字符串
    console.log(num.toString()) // 转字符串1
    console.log(num.toFixed(4)) // 固定4为小数，110.0000
    console.log(parseInt(str))  // 转数字

    // 日期类
    let date = new Date
    console.log(Date())         // 返回字符串
    console.log(date.valueOf())

    //日期格式化
    var d = new Date();
    var useDate1 = d.format('yyyy-MM-dd');
    var useDate2 = d.format('yyyy年-MM月-dd日 hh时:mm分:ss秒.S毫秒 qq季度')
    var useDate3 = d.format('yyy-MM-dd hh:mm:ss')
    console.log(useDate1)
    console.log(useDate2)
    console.log(useDate3)

    Date.prototype.format = function (format) {
        var o = {
            "M+": this.getMonth() + 1,                      //month
            "d+": this.getDate(),                           //day
            "h+": this.getHours(),                          //hour
            "m+": this.getMinutes(),                        //minute
            "s+": this.getSeconds(),                        //second
            "q+": Math.floor((this.getMonth() + 3) / 3),    //quarter
            "S": this.getMilliseconds()                     //millisecond
        }
        if (/(y+)/.test(format)) { // /(y+)/是一个regex对象, 用于处理年，单独处理是因为显示的位数不确定
            // RegExp.$1 代表输入的y部分
            // substr 代表截取年的位数
            format = format.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length))

        }
        for (var k in o) {
            if (new RegExp("(" + k + ")").test(format)) {
                format = format.replace(
                    // 同上，用于分别处理各个属性，进行替换，注意补0
                    RegExp.$1, RegExp.$1.length == 1 ? o[k] : ("00" + o[k]).substr(("" + o[k]).length)
                );
            }

        }
        return format;
    }
```

### 13 正则表达式
```javascript
        // 正则表达式 基础
        let pattern = /runoob/i  // 用两个斜杆进行包裹, /runoob/(i, g, m) i:忽略大小写, g：全局匹配, m: 多行匹配
        let str = "hello runoob"
        console.log(str.search(pattern)) // 输出开始下标，为6
        console.log(str.replace(pattern, "blakeyi")) // 输出 hello blakeyi
        console.log(pattern.test(str)) // 测试str是否包含pattern
```

### 14 变量提升

- 遇到 script 标签的话 js 就进行预解析，将变量 var 和 function 声明提升，但不会执行 function，然后就进入上下文执行，上下文执行还是执行预解析同样操作，直到没有 var 和 function，就开始执行上下文， 注意function提升在前

  ```javascript
  var getName=function(){
    console.log(2);
  }
  
  function getName(){
    console.log(1);
  }
  
  getName();
  //结果为2
  ```

### 15 this注意事项

- 简单理解，this指向的是该this所在的最里层的object对象。

  - 1. 函数不是object对象，所以没有写在object对象里的函数调用this会指向window

  - 2. 构造函数是object对象，所以在构造函数中调用this会指向该构造函数

  - 3. html元素是object元素，所以在html元素中调用this会指向该元素

  - 4. 函数1 return 函数2，函数2 return this，该this会指向window

- 场景
  - 1. 在方法中，this 表示该方法所属的对象。
  - 2. 如果单独使用，this 表示全局对象。
  - 3. 在函数中，this 表示全局对象。
  - 4. 在函数中，在严格模式下，this 是未定义的(undefined)。
  - 5. 在事件中，this 表示接收事件的元素。
  - 6. 类似 call() 和 apply() 方法可以将 this 引用到任何对象。

```javascript
    let obj1 = {
        fun1:function(){
            return function(){
                return this;
            }
        },
    };
    let obj2 = {
        fun1:function(){
            return this
        },
    };
    console.log(obj1.fun1()());     //window
    console.log(obj2.fun1());       //fun1
```



### 16 ES6 class

- 构造函数,`constructor`方法是类的默认方法，通过`new`命令生成对象实例时，自动调用该方法。一个类必须有`constructor`方法，如果没有显式定义，一个空的`constructor`方法会被默认添加。`constructor`方法默认返回实例对象（即`this`），完全可以指定返回另外一个对象, 类的构造函数，不使用`new`是没法调用的，会报错

  ```javascript
  class Point {
    constructor(x, y) {
      this.x = x;
      this.y = y;
    }
  
    toString() {
      return '(' + this.x + ', ' + this.y + ')';
    }
  }
  ```

  

- 定义“类”的方法的时候，前面不需要加上`function`这个关键字

- 构造函数的`prototype`属性，在ES6的“类”上面继续存在。事实上，类的所有方法都定义在类的`prototype`属性上面

- `Object.assign`方法可以很方便地一次向类添加多个方法。

  ```javascript
  Object.assign(Point.prototype, {
    toString(){},
    toValue(){}
  });
  ```

  

- 继承，通过修改prototype的指向实现继承关系

  ```javascript
  function SuperType() {
      this.property = true;
  }
  SuperType.prototype.getSuperValue = function () {
      return this.property;
  };
  function SubType() {
      this.subproperty = false;
  }
  // 继承 SuperType
  SubType.prototype = new SuperType();
  
  // 或者调用call来实现继承
  function SubType() {
  // 继承 SuperType 并传参
  	SuperType.call(this, "Nicholas");
  }
  let temp = new SubType()
  console.log(temp.getSuperValue())
  ```

  ### 16  console.log注意事项

  - 打印引用类型如map，数组等等时，打印的是最终的值，可以使用 debugger或者将对象转为字符串进行打印(JSON.stringify)

  ### 17 异步编程

  - async和await， async用于修饰函数，如果函数有返回值的话会把返回值包装成一个promise对象

    ```javascript
    async function foo() {
        console.log(1);
        return 3;
        //  return Promise.resolve(3)
    }
    // 给返回的期约添加一个解决处理程序
    foo().then(console.log);
    console.log(2);
    // 输出结果为：
    // 1
    // 2
    // 3
    ```

    下面例子可以看出async的执行顺序， 结果是 1.....9，顺序输出，  await 关键字暂停执行，向消息队列中添加一个期约在落定之后执行的任务，期约立即落定，把给 await 提供值的任务添加到消息队列，  JavaScript 运行时从消息队列中取出解决 await 期约的处理程序，并将解决的值 6 提供给它，然后执行await后面的语句

    ```javascript
    async function foo() {
        console.log(2);
        console.log(await Promise.resolve(6));
        console.log(7);
    }
    
    async function bar() {
        console.log(4);
        console.log(await 8);
        console.log(9);
    }
    console.log(1);
    foo();
    console.log(3);
    bar();
    console.log(5);
    ```

    

  

