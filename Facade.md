## 外观（Facade）模式    

### 定义：     
> 外观模式是一种结构型模式。它为更大的代码体提供了一个方便的高层次接口，能够隐藏其底层的真实复杂性。简单说就是——小接口有大智慧。    

### 例子：    
> 使用jQuery的$(el).css()或$(el).animate()方法时，实际上我们是在使用Facade：一种更简单的公有接口，使我们不必手动在jQuery核心调用很多内部方法以便实现某些行为。

### 优点：    
1. 易于使用。

2. 实现该模式时占用空间小。

3. 调用者与底层代码解耦。     

### 缺点：    
1. 可能存在隐性成本，性能下降。   

### 使用场景：    
1. 为一个复杂子系统提供一个简单接口。

2. 提高子系统的独立性。    

### 示例：    
使用Facade来简化用于监听跨浏览器事件的接口。    
```
var addMyEvent = function( el,ev,fn ){
    if( el.addEventListener ){
        el.addEventListener( ev,fn, false );
    }else if(el.attachEvent){
        el.attachEvent( "on" + ev, fn );
    } else{
        el["on" + ev] = fn;
    }
};
```    

### 结论：     
> 当使用Facade模式时，要了解涉及的任何性能成本，并确认是否值得抽象。