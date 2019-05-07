![1557215455833](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557215455833.png)

![1557215549991](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557215549991.png)

![1557215678179](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557215678179.png)

![1557215757445](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557215757445.png)

![1557215876551](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557215876551.png)

![1557218553250](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557218553250.png)

![1557218581372](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557218581372.png)

![1557218744923](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557218744923.png)

![1557218920427](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557218920427.png)

![1557218941062](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557218941062.png)

```java
package com.hefeng.config;

import lombok.Data;
import org.springframework.boot.context.properties.ConfigurationProperties;

@ConfigurationProperties
@Data
public class JdbcProperties {
    String url;
    String driverClassName;
    String username;
    String password;
}
```



@Data 源码：  编译成class时，直接生成Getter，Setter，ToString，HashCode。

```java
/**
 * Generates getters for all fields, a useful toString method, and hashCode and equals implementations that check
 * all non-transient fields. Will also generate setters for all non-final fields, as well as a constructor.
 * <p>
 * Equivalent to {@code @Getter @Setter @RequiredArgsConstructor @ToString @EqualsAndHashCode}.
 * <p>
 * Complete documentation is found at <a href="https://projectlombok.org/features/Data">the project lombok features page for &#64;Data</a>.
 * 
 * @see Getter
 * @see Setter
 * @see RequiredArgsConstructor
 * @see ToString
 * @see EqualsAndHashCode
 * @see lombok.Value
 */
```

![1557226357652](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557226357652.png)

![1557226406537](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557226406537.png)

![1557226447486](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557226447486.png)

![1557226464321](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557226464321.png)

![1557226482969](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557226482969.png)