#### 1. spring的结构

<img src="C:\Users\12964\Desktop\笔记\spring笔记\Snipaste_2020-07-02_17-10-33.png" style="zoom: 50%;" />

#### 2. 配置文件beans.xml

- 普通类型，实体类中只有一个name属性

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    //id表示实体类中的对象名   class对应实体类的位置 name可以用于给id取别名 scope是创建对象模式，singleton是单例模式
    <bean id="hello" class="com.bs.pojo.Hello" name="hello2,hello3" scope="singleton">
        //property表示变量  value可以设置变量的值
        <property name="str" value="Hello World"/>
    </bean>
    
    //import用于将其余的beans.xml整合到一起
	<import resource="beans.xml"/>
    <import resource="beans2.xml"/>
</beans>
```

- DI注入，实体类中有多种属性

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="hero1" class="com.bs.pojo.Hero">
        <property name="name" value="盖伦"/>
    </bean>

    <bean id="hello" class="com.bs.pojo.Hello" >
<!--        第一种方式，值插入，普通变量类型-->
        <property name="str" value="Hello World"/>
<!--        第二种方式，bean注入，用于类型为对象饮用型-->
        <property name="hero" ref="hero1"></property>
<!--        第三种，用于类型为数组型-->
        <property name="books">
            <array>
                <value>三国</value>
                <value>水浒</value>
                <value>红楼</value>
                <value>西游</value>
            </array>
        </property>

<!--        list类型-->
        <property name="hobbys">
            <list>
                <value>打肖正</value>
            </list>
        </property>
    </bean>
    
</beans>
```

- DI注入之p与c注入

1. p命名空间注入，直接注入的是属性值，可以自动识别实体类中的属性

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="user" class="com.bs.pojo.User" p:age="18" p:name="肖正"/>
</beans>
```

2. c命名空间注入，通过构造器进行注入，没有构造器无法注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    //下面中c：name注入之后不能进行c：0的注入，只能选一个
    <bean id="user" class="com.bs.pojo.User" c:age="19" c:name="" c:_0="肖正"/>
</beans>
```

#### 3.实体类Hello

```java
public class Hello {
    private String str;

    public String getStr() {
        return str;
    }

    public void setStr(String str) {
        this.str = str;
    }
}
```

我是你爸

