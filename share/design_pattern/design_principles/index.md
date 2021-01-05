#### SOLID设计原则
- SOLID是面向对象和编程中的几个重要的原则的首字母的缩写。
  | 简写    | 全拼    |     |
  | --- | --- | --- |
  | SRP    |  The Single Responsibility Principle	    |  单一责任原则 |
  |  OCP   |  The Open Closed Principle	   |   开放封闭原则 |
  | LSP    |  The Liskov Substitution Principle   | 里氏替换原则|
  |  DIP   |  The Dependency Inversion Principle	   |  依赖倒置原则 |
  | ISP   |  The Interface Segregation Principle	   |   接口分离原则 |

##### 单一责任原则
- 当需要修改某个类的时候的原因有且只有一个。其实就是让一个类只做一种类型责任，当这个类需要承担其他类型的责任的时候，需要分解这个类。

##### 开放封闭原则
- 软件实体应该是可以扩展的，而不可修改的。俗话说就是，类对扩展时开发的，对类修改是封闭的。

##### 里氏替换原则
- 当一个子类的实例应该能够替换任何其超类的实例时，他们之间才具有IS-A关系。

##### 依赖倒置原则
- 高层模块不应该依赖底层模块，二者都应该依赖于抽象。
- 抽象不应该依赖细节，细节应该依赖于抽象。

##### 接口分离原则
- 不能强迫用户去依赖那些他们不使用的接口，其实就是使用多个专门的接口比使用单一的接口好。