# Stream
- 概要：
    - 流（stream）是什么？
        - 是数据渠道，用于操作数据（集合、数组等）所生成的元素序列。`集合讲的是数据，流讲的是计算。`
    - Stream 的三个操作步骤：
        - 1.创建 Stream
        - 2.中间操作：
            - 概念：
                - 多个中间操作可以链接起来形成一个流水线，除非流水线上触发终止操作，否则中间操作不会执行任何的处理！而在终止操作时一次性全部处理，称为`惰性求值`。
            - api：
                - filter：
                    - 从流中排除某些元素。
                - limit：
                    - 截断流，使元素不超过给定数量。
                - skip：
                    - 跳过元素，返回一个丢掉了前 n 个元素的流，若流中元素不足 n 个，则返回一个空流。和 limit 互补。
                - map：
                    - 映射，将元素转换成其他形式或者提取信息，接受一个函数作为参数，该函数会被应用到每一个元素上，并将映射成一个新的元素。
                - flatmap：
                    - 接受一个函数作为参数，把流中的每一个值都转换成另一个流，然后把所有的流转换成一个流。
                - sorted：
                    - 自然排序（Comparable）。
                - sorted(Compartor com)：
                    - 定制排序（Compartor）。
        - 3.终止操作：
            - api：
                - allMatch：
                    - 检查是否匹配的所有元素。
                - anyMatch：
                    - 至少有一个匹配。
                - noneMatch：
                    - 检查是否没有匹配所有元素。
                - findFirst：
                    - 返回第一个元素。
                - findAny：todo:??
                    - 返回当前流中任意元素。
                - count：
                    - 返回流中元素的总数。
                - max：
                    - 返回流中最大的值。
                - mix：
                    - 返回流中最小的值。
    - 其他：
        - api：
            - reduce：
                - 将流中的所有元素都加起来，最后得到一个值。
            - collect：
                - 将流转化成其他形式，接受一个 Collector 接口的实现，用于给 stream 中元素做汇总的方法。
                - 可以计算出 总数、平均值、总和、最大值、最小值、分组、多级分组、分区等。
- 语法：
- 案例：
    ```java
        /**
        * 中间操作 筛选： 
        * 		- filter:
        * 			- 从流中排除某些元素。
        */
            @Test
            public void function01() {
                List<Person> list = Arrays.asList(new Person(1L, "李栋", 25, "男"), new Person(2L, "王彦书", 20, "女"),
                        new Person(3L, "孙兵兵", 24, "女"));

                // 中间操作
                Stream<Person> filterPersons = list.stream().filter((e) -> {
                    System.out.println("中间过程");
                    return e.getAge() > 2;
                });
                
                // 终止操作
                filterPersons.forEach(System.out::println);
            }
        
        /**
        * 中间操作： 
        * 	- limit: 
        * 		- 截断流，使元素不超过给定数量。
        */
            @Test
            public void function02() {
                List<Person> list = Arrays.asList(new Person(1L, "李栋", 25, "男"), new Person(2L, "王彦书", 20, "女"),
                        new Person(3L, "孙兵兵", 24, "女"));

                Stream<Person> limitPersons = list.stream().limit(1);
                
                limitPersons.forEach(System.out::println);

            }

        /**
        * 中间操作： 
        * 	- skip: 
        * 		- 跳过元素，返回一个丢掉了前 n 个元素的流，若流中元素不足 n 个，则返回一个空流。和 limit 互补。
        */
            @Test
            public void function03() {
                List<Person> list = Arrays.asList(
                                            new Person(1L, "李栋", 25, "男"),
                                            new Person(2L, "王彦书", 20, "女"),
                                            new Person(3L, "孙兵兵", 24, "女"));
                
                Stream<Person> skipPerson = list.stream().skip(2);
                
                skipPerson.forEach(System.out::println);
            }

        /**
        * 中间操作： 
        * 	- distinct: 
        * 		- 通过流所生成的 hashCode() 和 equals() 去除重复的数据。 Person 类中必须重写 hashCode() 和 equals() 方
        * 法。
        */
            @Test
            public void function04() {
                List<Person> list = Arrays.asList(
                        new Person(1L, "李栋", 25, "男"),
                        new Person(2L, "王彦书", 20, "女"),
                        new Person(3L, "孙兵兵", 24, "女"),
                        new Person(3L, "孙兵兵", 24, "女"));
                
                Stream<Person> distinctPerson = list.stream().distinct();
                distinctPerson.forEach(System.out::println);
            }

        /**
        * 中间操作： 
        * 	- map: 
        * 		- 映射，将元素转换成其他形式或者提取信息，接受一个函数作为参数，该函数会被应用到每一个元素上，并将映射成一个新的元素。
        */
            @Test
            public void function05() {
                List<String> list = Arrays.asList("aaa", "bbb", "ccc", "dddd");
                
                Stream<String> mapList = list.stream().map((str) -> str.toUpperCase());
                
                mapList.forEach(System.out::println);
            }

        /**
        * 中间操作??： 
        * 	- flatmap: 
        * 		- 接受一个函数作为参数，把流中的每一个值都转换成另一个流，然后把所有的流转换成一个流。
        */
            @Test
            public void function06() {
                List<String> list = Arrays.asList("aaa", "bbb", "ccc", "dddd");
                ?????????????
            }
	
        /**
        * 中间操作： 
        * 	- sorted: 
        * 		- 自然排序
        */
            @Test
            public void function07() {
                List<String> list = Arrays.asList("fff", "aaa", "bbb", "ccc", "dddd");
                
                Stream<String> ch = list.stream().sorted();
                
                ch.forEach(System.out::println);
            }

        /**
        * 中间操作： 
        * 	- sorted(Compartor com): 
        * 		- 定制排序
        */
            @Test
            public void function08() {
                List<Person> list = Arrays.asList(
                        new Person(1L, "李栋", 25, "男"),
                        new Person(2L, "王彦书", 20, "女"),
                        new Person(3L, "孙兵兵", 24, "女"));
                
                list.stream().sorted((e1, e2) -> {
                    if(e1.getName().equals(e2.getName())) {
                        return e1.getName().compareTo(e2.getName());
                    } else {
                        return -e1.getSex().compareTo(e2.getSex());
                    }
                }).forEach(System.out::println);
            }

        /**
        * 中间操作： 
        * 	- allMatch： 
        * 		- 检查是否匹配的所有元素。
        */
            @Test
            public void function09() {
                List<Person> list = Arrays.asList(
                        new Person(1L, "李栋", 25, "男", Status.BUSY),
                        new Person(2L, "王彦书", 20, "女", Status.VOCATION),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.VOCATION)
                        );
            
                boolean bo = list.stream().allMatch((e) -> {
                    return e.getStatus().equals(Status.BUSY);
                });
                
                System.out.println(bo);
            }
        
        /**
        * 中间操作： 
        * 	- anyMatch： 
        * 		- 至少有一个匹配。
        */
            @Test
            public void function10() {
                List<Person> list = Arrays.asList(
                        new Person(1L, "李栋", 25, "男", Status.BUSY),
                        new Person(2L, "王彦书", 20, "女", Status.VOCATION),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.VOCATION)
                        );
            
                boolean bo = list.stream().anyMatch((e) -> {
                    return e.getStatus().equals(Status.BUSY);
                });
                
                System.out.println(bo);
            }

        /**
        * 中间操作： 
        * 	- noneMatch： 
        * 		- 检查是否没有匹配元素。
        */
            @Test
            public void function11() {
                List<Person> list = Arrays.asList(
                        new Person(1L, "李栋", 25, "男", Status.BUSY),
                        new Person(2L, "王彦书", 20, "女", Status.VOCATION),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.VOCATION)
                        );
            
                boolean bo = list.stream().noneMatch((e) -> {
                    return e.getStatus().equals("ddd");
                });
                
                System.out.println(bo);
            }

        /**
        * 中间操作： 
        * 	- findFirst： 
        * 		- 获取第一个元素。
        */
            @Test
            public void function12() {
                List<Person> list = Arrays.asList(
                        new Person(1L, "李栋", 25, "男", Status.BUSY),
                        new Person(2L, "王彦书", 20, "女", Status.VOCATION),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.VOCATION)
                        );
            
                Optional<Person> pers = list.stream().findFirst();
                
                System.out.println(pers.get());
            }
        
        /**
        * 中间操作： 
        * 	- findAny： 
        * 		- 
        */

        /**
        * 中间操作： 
        * 	- conut： 
        * 		- 返回流中元素的总数。
        */
            @Test
            public void function14() {
                List<Person> list = Arrays.asList(
                        new Person(1L, "李栋", 25, "男", Status.BUSY),
                        new Person(2L, "王彦书", 20, "女", Status.VOCATION),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.VOCATION)
                        );
                
                long count = list.stream().count();
                System.out.println(count);
            }

        /**
        * 中间操作： 
        * 	- max： 
        * 		- 返回流中最大的值。
        */
            @Test
            public void function15() {
                List<Person> list = Arrays.asList(
                        new Person(1L, "李栋", 25, "男", Status.BUSY),
                        new Person(2L, "王彦书", 20, "女", Status.VOCATION),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.VOCATION)
                        );
                
                Optional<Person> p = list.stream().max((e1, e2) -> {
                    return Double.compare(e1.getAge(), e2.getAge());
                });
                
                System.out.println(p.get());
            }
            
        /**
        * 归约
        */
            @Test
            public void function16() {
                List<Integer> list = Arrays.asList(
                        1,
                        2,
                        3,
                        4,
                        5
                        );
                
                
                //0 是初始值。
                Integer sum = list.stream().reduce((0), (x, y) -> {
                    return x + y;
                });
                
                System.out.println(sum);
            }

            @Test
            public void function17() {
                List<Person> list = Arrays.asList(
                        new Person(1L, "李栋", 25, "男", Status.BUSY),
                        new Person(2L, "王彦书", 20, "女", Status.VOCATION),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.VOCATION)
                        );
                
                Optional<Integer> sum = list.stream().map(Person::getAge).reduce(Integer::sum);
                
                System.out.println(sum.get());
            
            }

        /**
        * 收集
        *	- 将流转化成其他形式，接受一个 Collector 接口的实现，用于给 stream 中元素做汇总的方法。
        */
            @Test
            public void function18() {
                List<Person> list = Arrays.asList(
                        new Person(1L, "李栋", 25, "男", Status.BUSY),
                        new Person(2L, "王彦书", 20, "女", Status.VOCATION),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.FREE),
                        new Person(3L, "孙兵兵", 24, "女", Status.VOCATION)
                        );
                
                List<String> personNameList = list.stream().map(Person::getName).collect(Collectors.toList());
                
                System.out.println(personNameList.toString());
            }
    ```
