## 单例（Singleton）模式   

> 单例模式它限制了类的实例化次数只能一次。在实例不存在的情况下，可以通过一个方法创建一个类来实现创建类的新实例；如果实例已经存在，它会简单返回该对象的引用。（这跟我想的一样）    

```
var mySingleton = (function () {
  // Instance stores a reference to the Singleton
  var instance;
  function init() {
    // Singleton
    // Private methods and variables
    function privateMethod(){
        console.log( "I am private" );
    }
    var privateVariable = "Im also private";
    var privateRandomNumber = Math.random();
    return {
      // Public methods and variables
      publicMethod: function () {
        console.log( "The public can see me!" );
      },
      publicProperty: "I am also public",
      getRandomNumber: function() {
        return privateRandomNumber;
      }
    };
  };
  return {
    // Get the Singleton instance if one exists
    // or create one if it doesn't
    getInstance: function () {
      if ( !instance ) {
        instance = init();
      }
      return instance;
    }
  };
})();
```   

### 特别地方：

1. 单例不同于静态类（或对象），因为我们可以推迟它们的初始化（通常是因为它们需要的参数信息在类定义时是无法获得的），直到需要使用静态实例时，无需使用资源或内存。

2. 单例的唯一实例能够通过子类去扩展，使用者不用更改代码就能使用一个扩展的实例。

3. 单例将导致测试变困难，不利于单元测试。

### 何时使用单例（When it really is a singleton）：   

1. 是否每个应用程序使用这个类的方式都完全相同？

2. 是否每个应用程序任何时候都只需要一个类的实例？

3. 使用者不需要知道该类是这应用程序的哪个部分？（或许翻译不好）

当满足这三个点，那就可以用单例。关键就在于类的使用方式都相同，并且不需要应用上下文。