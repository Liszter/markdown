

### 1. call、 apple、 bind

#### 1.1 call的用法

* ```javascript
  function sayName (n1, n2) {
      return n1 + n2;
  }
  
  function sayNameCall (n1, n2) {
      return sayName.call(this, n1, n2) 
  }
  ```

#### 1.2 apply的用法

* ```javascript
  function sayName (n1, n2) {
      return n1 + n2;
  }
  
  function sayNameApply(n1, n2) {
  	return sayName.apply(this, arguments) // 或  return sayName.apply(thism, [n1, n2])
  }
  ```

#### 1.3 bind的用法

* ```javascript
  window.color = 'red'
  this.box = {
      color: 'blue'
  }
  function sayName () {
     console.log(this.color)
  }
  
  sayName(); // red
  let sayNameNew = sayName.bind(box);  // 相当于创建了一个sayName的新实例，this的值绑定到box上
  ```



### 2.  用途

#### 2.1  call 和 apply

* ```
  在特定的作用域中调用函数，实际上等于设置函数体内的this对象的值。
  ```

#### 2.2.  bind

* ```
  该方法创建一个函数的实例， this的值会绑定到传给bind()函数的值。
  ```

### 3.区别

#### 3.1  call和apply

* ```js
  call 传递的参数是  this + （arguments）或者是数组 sayName(this, arguments)
  apply 传递的参数是 this + 单独的参数   sayName(this, n1, n2)
  ```



### 4. 总结

```javascript
    window.color = 'red'
var box = {
    color: 'white'
}


function sayName (color) {
    return color
}

sayName(); // red
sayName.call(box); // white





    // call  apply 的用途： 在特定的作用域中调用函数，实际上等于设置函数体内this对象的值。
    
    // apply 一个是在其中 运行函数的作用域，另一个是 参数数组
    function sum(num1, num2){
        return num1 + num2;
    } 

    function callSum1(num1, num2) {
        return sum.apply(this, arguments)
    }

    function callSum2(num1, num2) {
        return sum.apply(this, arguments)
    }



    // call 第一个参数是 this 值，其余参数都直接传递给函数
    function callsum3 (num1, num2) {
        return sum.call(this, num1, num2)
    }
    
    // 它们真正强大的地方是能够扩充函数赖以运行的作用域。
    // 例如:
    window.color = 'red';
    var o = { color: 'blue' };

    function sayColor() {
        console.log(this.color);
    }
    sayColor();  // red

    sayColor.call(this); //red
    sayColor.call(window); //red
    // *****************************************
    sayColor.call(o); //blue  指向函数运行的作用域为 o   ，函数体内的 this 对象指向了 o


    // bind 该方法创建一个函数的实例， this值会绑定到传给bind()函数的值
    sayColor.bind(o);
    console.log(sayColor.bind(o));


    var objectSayColor = sayColor.bind(o);
    objectSayColor();
```

