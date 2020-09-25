# Optional
- 概要：
    - 定义：
        - Optional<T> 类是一个容器类，代表一个值存在或者不存在，原来用 null 表示一个值不存在，现在 Optional 可以更好的表达这个概念。并且可以避免空指针的问题。
    - api：
        - Optional.of(T t)：
            - 创建 Optional 的实例。
        - empty()：
            - 创建空的 optional。
        - ofNullable(T t)：
            - 若 t 不为null,创建 optional 实例，否则创建空实例。
        - isPresent()：
            - 判断是否有值。
        - orElse(T t)：
            - 如果调用对象包含值，返回该值。否则返回 t。
        - orElseGet(Supplier s)：
            - 如果调用对象包含值，就返回该值。否则返回 s 获取的值。
        - map(Function f)：
            - 如果有值对其进行处理，并且返回处理后的 option,否则返回 optional.empty()。
        - flatMap(Function mapper)：
            - 和 map 类似，要求必须返回  Optional。
- 语法：
- 案例：
    ```java
        /**
        * 创建实例
        */
            @Test
            public void function01() {
                Optional<Person> person = Optional.of(new Person());
                System.out.println(person.get());
            }
        
        /**
        * 创建空的 optional
        */
            @Test
            public void function02() {
                Optional<Person> person = Optional.empty();
                System.out.println(person.get());//报错
            }

        /**
        * 判断是否有值
        */
            @Test
            public void function03() {
                Optional<Person> person = Optional.ofNullable(new Person());
                
                if(person.isPresent()) {
                    System.out.println(person.get());
                }
            }
    ```
