#  동작 파라미터화 코드 전달하기

동작 파라미터화(behavior parameterization)를 이용하면 자주 바뀌는 요구사항에 효과적으로 대응할 수 있다.<br/>
동작 파라미터화에서는 메서드 내부적으로 다양한 동작을 수행할 수 있도록 코드를 메서드 인수로 전달한다.(코드 전달 기법)<br/>
코드 전달 기법은 자바 8 이전에는 코드를 지저분하게 구현해야 했다. 익명 클래스로도 어느 정도 코드를 깔끔하게 만들 수 있으나,<br/>
자바 8에서는 **Functional Interface**를 이용하여 여러 클래스를 구현해야 하는 수고를 없앨 수 있게 되었다.

    1. Runnable
    기존부터 존재하던 인터페이스로 스레드를 생성할 때 주로 사용되었으며, 가장 기본적인 함수형 인터페이스다.<br/>
    void타입의 인자없는 메서드를 갖고 있다
    ~~~java
    Runnable r = () -> System.out.println("Hello Functional Interface");
    r.run();
    ~~~
    2. Supplier<T>
    인자는 받지 않으며 리턴타입만 존재하는 메서드로, 인자를 받지 않음으로 항상 같은 결과를 반환하는 메서드이다.
    ~~~java
    Supplier<String> s = () -> "hello supplier";  
    String result = s.get();  
    ~~~
    3. Consumer<T>
    리턴은 하지않고(void), 인자를 받는 메서드이다. 인자를 소비한다고 생각하면 된다.
    ~~~java
    Consumer<String> c = str -> System.out.println(str);  
    c.accept("hello consumer");
    ~~~
    4. Function<T, R>
    인자와 리턴타입을 가져 타입 파라미터가 2개이며, 제네릭으로 지정할 수 있다.
    ~~~java
    Function<String, Integer> f = str -> Integer.parseInt(str);  
    Integer result = f.apply("1");
    ~~~
    5. Predicate<T>
    하나의 인자와 리턴타입을 가진다.<br/>
    Function과의 차이점은 리턴타입을 지정하지 않으며, 반환타입은 boolean으로 고정되어 있다는 점이다.
    ~~~java
    Predicate<String> p = str -> str.isEmpty();  
    boolean result = p.test("hello");
    ~~~
    6. UnaryOperator<T>
    하나의 인자와 리턴타입을 가지며, 인자와 리턴값의 타입이 같아야한다.
    ~~~java
    UnaryOperator<String> u = str -> str + " operator";  
    String result = u.apply("hello unary");
    ~~~
    7. BinaryOperator<T>
    동일한 타입의 인자 2개와 리턴값을 가진다.
    ~~~java
    BinaryOperator<String> b = (str1, str2) -> str1 + " " + str2;  
    String result = b.apply("hello", "binary");
    ~~~
    8. BiPredicate<T, U>
    서로 다른 타입의 2개의 인자를 받아 boolean 타입으로 반환한다.
    ~~~java
    BiPredicate<String, Integer> bp = (str, num) -> str.equals(Integer.toString(num));  
    boolean result = bp.test("1", 1);
    ~~~
    9. BiConsumer<T, U>
    서로 다른 타입의 2개의 인자를 받아 소모(void)한다. 
    ~~~java
    BiConsumer<String, Integer> bc = (str, num) -> System.out.println(str + " :: " + num);  
    bc.accept("숫자", 5);
    ~~~
    10. BiFunction<T, U, R>
    서로 다른 타입의 2개의 인자를 또 다른 타입으로 반환한다.
    ~~~java
    BiFunction<Integer, String, String> bf = (num, str) -> String.valueOf(num) + str;  
    String result = bf.apply(5, "678");
    ~~~
    11. Comparator<T>
    전통적으로 많이 사용된 인터페이스로, 객체간 우선순위를 비교할 때 사용되는 인터페이스이다.<br/>
    람다의 등장으로 Comparator의 구현이 매우 간단해져 Comparable 인터페이스의 실효성이 많이 떨어졌다.
    ~~~java
    Comparator<String> c = (str1, str2) -> str1.compareTo(str2);  
    int result = c.compare("aaa", "bbb");
    ~~~
