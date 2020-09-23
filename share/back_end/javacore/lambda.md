# lambda 表达式：todo
- 概念：
    - 定义：
        - Java8 中引入一个新的操作符 `->`。箭头将表达式拆分成两部分：
            - 左侧：表达式的参数列表。
            - 右侧：表达式所执行的功能。
        - `lambda` 表达式，也可以称为闭包，它是推动 java8 发布的最重要的新特性。
        - `lambda` 允许把函数作为一个方法的参数（函数作为参数传递方法中）。
        - 使用 `Lambda` 表达式可以使代码变得更加简洁。
    - 重要特征：
        - 表达式需要 `函数式接口` 的支持。
            - 接口中只存在一个抽象方法的接口称为函数式接口。用注解 `@FunctionalInterface` 修饰，可以检测是否是函数式接口。
    - 四大核心内置函数接口：
        - Consumer<T>：
            - 消费型接口
                - void accept(T t);
        - Supplier<T>：
            - 供给型接口
                - T get();
        - Function(T, R)：
            - 函数式接口
                - R apply(T t);
        - Predicate<T>：
            - 断言型接口
                - boolean test(T t);
    - 方法引用：
        - 定义：
            - 若表达式体内容有方法已经实现了，我们可以使用`方法引用` 。可以理解为方法引用是表达式的另一种的表现形式。
        - 语法格式：
            - 对象::实例方法名
            - 类::静态方法名
            - 类::实例方法名
    
- 语法：
    ```java
        (paramters) -> expression
        或
        (paramters) -> { statements; }

        //1.无参数、无返回值
            （）-> System.out.println("say hello!");

        //2.有一个参数、并且无返回值。如果只有一个参数，小括号可以不写

        //3.多个参数、有返回值。并且有多条语句。如果只有一条语句 return和打括号都可以不写。

        //4.数据类型可以不写，因为他本身可以类型推断。

        //方法引用
            //对象::实例方法名
            //类::静态方法名
            //类::实例方法名

    ```
- 案例：
    ```java
        //0.say hello
            public class DemoLambda {
	
                ArrayList<Person> list = new ArrayList<Person>();
                
                @Test
                public void function01() {
                    
                    list.add(new Person(1L, "青衣", 25, "男"));
                    list.add(new Person(2L, "青衣", 235, "女"));
                    list.add(new Person(3L, "青衣", 835, "男"));
                    list.add(new Person(4L, "青衣", 265, "女"));
                    
                    list.stream()
                        .filter((e) -> e.getAge() > 400).forEach(System.out::println);
                }

            }

        //1.无参数、无返回值
            @Test
            public void function02() {
                Runnable r1 = () -> System.out.println("say hello!");
                r1.run();
            }

        //2.有一个参数、并且无返回值
            @Test
            public void function03() {
                Consumer<String> co = (x) -> System.out.println(x);
                co.accept("青衣不伤心");
            }

        //3.多个参数、有返回值。并且有多条语句
            @Test
            public void function04() {
                Comparator<Integer> com = (x, y) -> {
                    System.out.println("操作执行了！");
                    return x + y;
                };
            }
        
        //四大核心内置函数接口：
            //Consumer<T>：
                //void accept(T t);
                    @Test
                    public void function05() {
                        //Consumer<T>
                        happy(100.00, (m) -> System.out.println("旅游花费了" + m + "元"));
                        
                    }
                    
                    public void happy(double money, Consumer<Double> con) {
                        con.accept(money);
                    }

            //Supplier<T>：
                //T get();
                    @Test
                    public void function05() {
                        //Supplier<T>
                        ArrayList<Integer> list = getNumList(10, () -> (int)(Math.random() * 10));
                        System.out.println(list.toString());
                    }
                    
                    public ArrayList<Integer> getNumList(int num, Supplier<Integer> sup) {
                        ArrayList<Integer> list = new ArrayList<Integer>();
                        
                        for (int i = 0; i < num; i++) {
                            list.add(sup.get());
                        }

                        return list;
                    }

            //Function<T, R>：
                //R apply(T t);
                    @Test
                    public void function05() {
                        //Function<T, R>
                        String temp = setHeadler("\t\t 青衣", (str) -> str.trim());
                        System.out.println(temp);
                        
                    }
                    
                    public String setHeadler(String str, Function<String, String> fun) {
                        return fun.apply(str);
                    }

            //Predicate<T>：
                //boolean test(T t);
                    @Test
                    public void function05() {
                        List<String> list = Arrays.asList("on", "no", "yes", "qingyi");
                        
                        List<String> result = filterStr(list, (m) -> m.length() > 3);
                        System.out.println(result);
                    }
                    
                    public ArrayList<String> filterStr(List<String> list, Predicate<String> pre) {
                        ArrayList<String> result = new ArrayList<String>();
                        
                        for (String str : list) {
                            if(pre.test(str)) {
                                result.add(str);
                            }
                        }
                        
                        return result;
                    }
        //方法引用
            //对象::实例方法名
            //类::静态方法名
            //类::实例方法名
    ```
