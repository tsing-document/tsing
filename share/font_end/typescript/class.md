# 类
- hello world：
    ```ts
        class Demo {
            say: string;
            constructor(userinput: string) {
                this.say = userinput;
            }

            sayHello () {
                return "Hello，" + this.say;
            }
        }
    ```
- 继承：
    ```ts
        class Person {

            name: string;
            age: number;

            jump(heght: number = 0) {
                console.log(`我能跳 ${heght} 高`);
            }
        }

        class Student extends Person {
            running () {
                console.log('我是学生，我跑的很快！！！');
            }
        }

        const stu = new Student();
        stu.running()
        stu.jump(100);
        stu.running();

    ```
- 复杂继承：
    ```ts
        class Animal {
            name: string;

            constructor(theName: string) {
                this.name = theName;
            }

            move(distanceInMeters: number = 0) {
                console.log(`${this.name} moved ${distanceInMeters}`);
            }
        }

        class Snake extends Animal{
            constructor(name: string) {
                super(name);
            };

            move(distanceInMeters = 5) {
                console.log("构造函数：I am Snake");
                super.move(distanceInMeters);
            }
        }

        class Horse extends Animal{
            constructor(name: string) {
                super(name)
            };

            move(distanceInMeters = 45) {
                console.log("构造函数：I am Horse");
                super.move(distanceInMeters);
            };
        }

        let sam = new Snake('Snake is 蛇');
        let tom: Animal = new Horse("Horse is 房子");
        sam.move();
        tom.move(45);
    ```
- 抽象类：
    - 概念：
        - 抽象类作为其他派生类的基类使用。他们一般不会实例化。不同于接口，抽象类可以包含成员的实现细节。
          `abstract` 关键子是用于定义抽象类和在抽象类内部定义抽象方法。
            ```ts
                abstract class Animal {
                    abstract makeSound(): void;

                    move(): void {
                        console.log("roming the earch...");
                    }
                }
            ```
        - 抽象类中的抽象方法不包含具体必须在在派生类中实现。抽象方法的语法和接口方法相似。两者都是定义方法签名但不包含方法体。然而，抽象方法必须包含 `abstract` 关键字并且可以包含访问修饰符。
            ```ts
                abstract class Departement {
                constructor(public name: string) {}

                printName(): void {
                    console.log("Departement name:" + this.name);
                }

                abstract printMeeting(): void; //必须在派生类中实现
            }

            class AccountingDepartement extends Departement {
                constructor() {
                    super("Accounting and Auditing"); //在派生类的构造函数中必须调用 spuer()
                }

                printMeeting(): void {
                    console.log("The Accounting Departent meets each monday at 10am.");
                }

                generateReports(): void {
                    console.log("Generating accounting reports...");
                }
            }

            let department: Departement; //允许创建一个对抽象类型的引用
            //department = new Departement(); 错误：不能创建一个抽象类的实例
            department = new AccountingDepartement(); //允许对一个抽象子类进行实例化和赋值
            department.printName();
            department.printMeeting();
            //department.generateReports(); 错误：方法在声明的抽象类中不存在
            ···
- 公共、私有与受保护的修饰符：
    - `public` 公共
    - `private` 私有
    - `protected` 
    - `readonly` 只读
- 静态属性：
    -  在属性值前面加 `static`，使用方式用类名 `点`。

