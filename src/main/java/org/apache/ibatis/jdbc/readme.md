# 20260407
问题：整个JDBC包没有被外部引用，该包存在的意义？

jdbc包时mybatis提供的一个功能独立的工具包，留给用户自行使用，而不是mybatis调用；
选择拼接SQL语句的方式

```java
public class UserProvider{
    public String queryUserBySchoolName(){
        return "SELECT * FROM user WHERE schoolName = #{schoolName}";
    }
}
```

```java
import org.apache.ibatis.jdbc.SQL;

public class UserProvider {
    public String queryUserBySchoolName() {
        return new SQL()
                .SELECT("*")
                .FROM("user")
                .WHERE("schoolName = #{schoolName}")
                .toString();
    }
}
```
有些情况下，我们需要对数据库进行一些设置操作（如运行一些DDL操作），并不需要mybatis提供ORM功能，那么SqlRunner类和ScriptRunner类最好的选择；