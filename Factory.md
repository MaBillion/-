## 工厂（Factory）模式   

> 工厂模式提供一个通用的接口来创建对象。    

```
function Car( options ) {
  this.doors = options.doors || 4;
  this.state = options.state || "brand new";
  this.color = options.color || "silver";
}
 
function Truck( options){
  this.state = options.state || "used";
  this.wheelSize = options.wheelSize || "large";
  this.color = options.color || "blue";
}
 
function VehicleFactory() {}
VehicleFactory.prototype.createVehicle = function ( options ) {
  switch(options.vehicleType){
    case "car":
      this.vehicleClass = Car;
      break;
    case "truck":
      this.vehicleClass = Truck;
      break;
    //defaults to VehicleFactory.prototype.vehicleClass (Car)
  }
  return new this.vehicleClass( options );
};
var carFactory = new VehicleFactory();
var car = carFactory.createVehicle( {
            vehicleType: "car",
            color: "yellow",
            doors: 6 } );
console.log( car instanceof Car ); // Outputs: true
```   

### 何时使用工厂：   

1. 当对象或组件设置非常复杂的时候。

2. 当需要根据所在的不同环境轻松生成对象的不同实例时。

3. 当处理很多共享相同属性的小型对象或组件时。

4. 对象的实例只需要满足一个约定——鸭子类型(duck typing)。利于解耦。   

> PS：鸭子类型——“当看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子。”我们并不关心对象是什么类型，到底是不是鸭子，只关心行为。   

## 抽象工厂（Abstract Factory）模式    

### 书中描述：   
> 使用抽象工厂模式场景：一个系统必须独立于它所创建的对象的生成方式，或它需要与多种对象类型一起工作。
PS：我觉得没描述清楚。

### 网上定义：    
> 为创建一组相关或相互依赖的对象提供一个接口，而且无需指定他们的具体类。
PS：这个才比较清晰。

### 我的理解：    
> 在工厂模式的加上一层抽象，工厂的工厂。  

### 总结     
> 单例模式和工厂模式概念上是比较简单，但是在使用上需要留心。该不该用单例，就考虑上面讲的单例三要点；该不该用工厂，就要看它是否带来大量不必要的复杂性，带来不必要的开销（不为了用模式而用模式）。抽象工厂模式并没有找到好的示例，就先略下。
