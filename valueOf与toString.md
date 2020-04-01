# valueOf 与 toString 的使用

### Object.prototype.valueOf 

把对象换成原始类型值(Number、String、Boolean)

```javascript
1 == 'string' // true
```

### Object.prototype.toString

在适用对象文本值或者当以期望字符串的方式引用对象时，该方法自调用：

```javascript
//使用原生toString
var obj = {name: 'Coco'};
var str = '123' + obj;
console.log(str);  // 123[object Object]

//obj添加toString
var obj = {
	name: 'Coco',
	toString:()=>console.log('string')
	};
var str = '123' + obj;
console.log(str);
//string
//123undefined
```

#### String 类型转换规则：

1. 如果toString方法存在并且返回原始类型，返回toString的结果
2. 如果toString方法不存在或者返回的不是原始类型，调用valueOf方法
3. 如果valueOf方法存在并且返回原始类型数据，返回valueOf的结果
4. 其他情况抛出错误

```javascript
var obj = {name: 'Coco'};
var str = '123' + obj.toString();
```

#### 假设是数组

```javascript
var array = [0,1,2,3];
var str = '123' + array;
 
console.log(str); // 1230,1,2,3
```

- 测试

  ```javascript
  var obj = {
      toString: function() {
          console.log('调用了 obj.toString');
          return {};
      },
      valueOf: function() {
          console.log('调用了 obj.valueOf')
          return '110';
      }
  }
   
  console.log(obj);
  // 调用了 obj.toString
  // 调用了 obj.valueOf
  // 110
  ```

- toString 和 valueOf返回的都不是原始类型时

  ```javascript
  var obj = {
      toString: function() {
          console.log('调用了 obj.toString');
          return {};
      },
      valueOf: function() {
          console.log('调用了 obj.valueOf')
          return {};
      }
  }
   
  console.log(obj);
  // 调用了 obj.toString
  // 调用了 obj.valueOf
  // Uncaught TypeError: Cannot convert object to primitive value
  
  ```

#### Number 转换规则

1. 如果 valueOf 存在，且返回原始类型数据，返回 valueOf 的结果。
2. 如果 toString 存在，且返回原始类型数据，返回 toString 的结果。
3. 其他情况，抛出错误。

```javascript
var obj = {
    valueOf: function() {
        console.log('调用 valueOf');
        return {};
    },
    toString: function() {
        console.log('调用 toString');
        return 10;
    }
}
 
console.log(obj + 1);
// 调用 valueOf
// 调用 toString
// 11

/* 没有基本类型返回值 */
var obj = {
    valueOf: function() {
        console.log('调用 valueOf');
        return {};
    },
    toString: function() {
        console.log('调用 toString');
        return {};
    }
}
 
console.log(obj + 1);
// 调用 valueOf
// 调用 toString
// Uncaught TypeError: Cannot convert object to primitive value

//function 
function str(){
    var i =1 ;
    this.toString =function(){
        console.log('toString')
    }
    return i;
}
str
//ƒ str(){
//        var i =1 ;
//        this.toString =function(){
//          console.log('toString')
//        }
//		return i;
// }

function str(){
    var i =1 ;
    return i;
}
str.toString =function(){
    console.log('toString')
};
str.valueOf = function (){
    console.log('valueof')
};
str
//valueof
// -上面函数调用了valueOf方法
str.toString =function(){
    console.log('toString')
    return 3;
};
str.valueOf = function (){
    console.log('valueof')
    reutrn {};
};
str
//valueof
//toString
//3
```

一段有趣的代码

```javascript
function add() {
    var args = [].slice.call(arguments);

    var fn = function () {
        var fn_args = [].slice.call(arguments);
        return add.apply(null, args.concat(fn_args))
    }

    fn.valueOf = function () {
        return args.reduce(function (a, b) {
            return a + b;
        })
    }
    return fn
}
function add () {
    console.log('进入add');
    var args = Array.prototype.slice.call(arguments);
 
    var fn = function () {
        var arg_fn = Array.prototype.slice.call(arguments);
        console.log('调用fn');
        return add.apply(null, args.concat(arg_fn));
    }
 
    fn.valueOf = function () {
        console.log('调用valueOf');
        return args.reduce(function(a, b) {
            return a + b;
        })
    }
 
    return fn;
}

add(1);
// 进入add
// 调用valueOf
// 1

其实也就是相当于：

[1].reduce(function(a, b) {
return a + b;
})
// 1

当链式调用两次的时候：

add(1)(2);
// 进入add
// 调用fn
// 进入add
// 调用valueOf
// 3

当链式调用三次的时候：

add(1)(2)(3);
// 进入add
// 调用fn
// 进入add
// 调用fn
// 进入add
// 调用valueOf
// 6

```

可以看到，这里其实有一种循环。只有最后一次调用才真正调用到 valueOf，而之前的操作都是合并参数，递归调用本身，由于最后一次调用返回的是一个 fn 函数，所以最终调用了函数的 fn.valueOf，并且利用了 reduce 方法对所有参数求和。

除了改写 valueOf 方法，也可以改写 toString 方法。

这里有个规律，如果只改写 valueOf() 或是 toString() 其中一个，会优先调用被改写了的方法，而如果两个同时改写，则会像 Number 类型转换规则一样，优先查询 valueOf() 方法，在 valueOf() 方法返回的是非原始类型的情况下再查询 toString() 方法