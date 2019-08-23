# 数据访问
JDBC
Mybatis
JPA

## JDBC

- 引入starter
```xml
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>

<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<scope>runtime</scope>
</dependency>
```
- 配置application.yml
```yaml
spring:
  datasource:
    username: root
    password: root
    url: jdbc:mysql://localhost:3306/jdbc
    driver-class-name: com.mysql.jdbc.Driver
```
    数据源:com.zaxxer.hikari.HikariDataSource
    自动配置：DataSourceConfiguration.class
        spring.datasource.type指定
        也可以自定义
    操作数据库：
        自动配置了JdbcTemplateAutoConfiguration.class 
- 测试
```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class SpringBoot05DataJdbcApplicationTests {
	@Autowired
	DataSource dataSource;

	@Test
	public void contextLoads() throws SQLException {
		System.out.println(dataSource.getClass());

		Connection connection=dataSource.getConnection();
		System.out.println(connection);
		connection.close();
	}

}

```
- 使用
```java
@Controller
public class HelloController
{
    @Autowired
    JdbcTemplate jdbcTemplate;

    @ResponseBody
    @GetMapping("/query")
    public Map<String,Object> map(){
        List<Map<String,Object>> list=jdbcTemplate.queryForList("select * from department");
        return list.get(0);
    }
}
```
- 高级配置：使用druid数据源
        - 引入druid
        - 配置属性
- 配置druid数据源监控