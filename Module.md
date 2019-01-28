## 模块（Module）模式   

> 模块模式是为类提供私有变量和特权方法（有权访问私有变量和私有函数的公有方法）的方法。在JavaScript，就可通过闭包的方式，模拟实现模块模式。     

### 对象字面量   

```
var myModule = {
    variableKey: variableValue,
    getKey: function () {
      // ...
    }
};
```   
> 严格上讲，对象字面量实现的只是不完整的模块模式，因为无法达到变量、方法私有效果。不过确实有分离和组织代码的能力，也就算一种简略的模块模式的实现方式。

```
var myModule = (function(){
    var privateVar = 10;
    return {
        getPrivateVar : function(){
             return privateVar;
        }
    }
})();
```    

### 引入全局变量例子   

```
// Global module
var myModule = (function ( jQ, _ ) {
    function privateMethod1(){
        jQ(".container").html("test");
    }
    function privateMethod2(){
      console.log( _.min([10, 5, 100, 2, 1000]) );
    }
    return{
        publicMethod: function(){
            privateMethod1();
        }
    };
// Pull in jQuery and Underscore
})( jQuery, _ );
```    
> PS：书中还有相应结合Dojo、ExtJS、YUI、jQuery等框架的模块模式的实现方式，不过我觉得只要理解模块模式的就行了，也不一一列例子。   

### 揭示（Revealling）模块模式    
> 这种是模块模式的改进版本，它是在模块代码底部，定义所有对外公布的函数（仅是指针）和变量。    

```
var myRevealingModule = (function () {
    var privateVar = "Ben Cherry",
        publicVar = "Hey there!";
    function privateFunction() {
        console.log( "Name:" + privateVar );
    }
    function publicSetName( strName ) {
        privateVar = strName;
    }
    function publicGetName() {
        privateFunction();
    }
    // Reveal public pointers to
    // private functions and properties
    return {
        setName: publicSetName,
        greeting: publicVar,
        getName: publicGetName
    };
})();
```    
> 这种模式我经常使用，它很容易指出哪些函数和变量可以被公开访问，增强了可读性。    

### 总结

> 有时我们在不经意间就使用了某种模式（例如上面两种模式），但并不知道写的东西已经是前人总结很好的东西了。所以在细细阅读过程中，书中内容使得我自己对模式的认识更加系统全面，也能改正自己使用上的误区。