```java
// 代码评审

总体来说，代码改动主要集中在以下几个方面：

1. 新增了`userId`和`activityId`字段，并标记了`strategyId`字段为`@Deprecated`，这意味着在未来版本中`strategyId`可能会被移除。

2. `RaffleAwardListResponseDTO`类新增了几个字段，用于表示奖品的解锁规则和状态。

3. `IRaffleStrategyService.xml`和`rule_tree_node_mapper.xml`中新增了查询解锁规则的SQL语句。

4. 新增了`RaffleActivityControllerTest`和`RaffleStrategyControllerTest`测试类，用于测试抽奖活动相关的接口。

5. `IActivityRepository`和`IRaffleActivityAccountQuotaService`接口中新增了查询用户参与次数的方法。

6. `AbstractRaffleActivityAccountQuota`类实现了查询用户参与次数的方法。

7. `IStrategyRepository`接口中新增了查询奖品解锁规则的方法。

8. `StrategyAwardEntity`类新增了`ruleModels`字段，用于存储规则模型。

9. `IRaffleAward`接口中新增了根据活动ID查询奖品列表的方法。

10. `IRaffleRule`接口定义了查询奖品解锁规则的方法。

11. `DefaultRaffleStrategy`类实现了查询奖品解锁规则和根据活动ID查询奖品列表的方法。

12. `ActivityRepository`类实现了查询用户参与次数的方法。

13. `StrategyRepository`类实现了查询奖品解锁规则的方法。

14. `IRaffleActivityAccountDayDao`和`IRuleTreeNodeDao`接口中新增了查询解锁规则的SQL语句。

15. `RaffleStrategyController`类中修改了查询奖品列表的方法，增加了查询解锁规则和用户参与次数的逻辑，并修改了参数校验。

建议：

1. 代码中使用了`@Deprecated`标记`strategyId`字段，建议在未来的版本中移除该字段，并更新相关的代码。

2. 新增的测试类可以进一步完善，增加更多的测试用例，以确保代码的稳定性和可靠性。

3. 在`RaffleStrategyController`类中，建议将查询解锁规则和用户参与次数的逻辑封装到单独的方法中，以提高代码的可读性和可维护性。

4. 代码中使用了`lombok`的`@Data`注解，建议在类名上方添加`@AllArgsConstructor`和`@NoArgsConstructor`注解，以生成带参构造函数和无参构造函数。

5. 代码中使用了`com.alibaba.fastjson.JSON`进行JSON序列化，建议使用`org.springframework.boot.jackson.JsonComponent`进行JSON序列化，以保持与Spring Boot的一致性。

6. 代码中使用了`org.apache.commons.lang3.StringUtils`进行字符串操作，建议使用`java.util.Objects`进行字符串操作，以保持与Java标准库的一致性。

7. 代码中使用了`org.springframework.web.bind.annotation.RequestMapping`注解进行路由映射，建议使用`org.springframework.web.bind.annotation.GetMapping`和`org.springframework.web.bind.annotation.PostMapping`注解进行路由映射，以提高代码的可读性和可维护性。

8. 代码中使用了`org.slf4j.Logger`进行日志记录，建议使用`org.slf4j.LoggerFactory`进行日志记录，以保持与SLF4J的一致性。

9. 代码中使用了`org.springframework.stereotype.Service`注解进行服务注册，建议使用`org.springframework.stereotype.Component`注解进行服务注册，以保持与Spring Boot的一致性。

10. 代码中使用了`org.springframework.beans.factory.annotation.Autowired`注解进行依赖注入，建议使用`org.springframework.beans.factory.annotation.Qualifier`注解进行依赖注入，以提高代码的可读性和可维护性。
```