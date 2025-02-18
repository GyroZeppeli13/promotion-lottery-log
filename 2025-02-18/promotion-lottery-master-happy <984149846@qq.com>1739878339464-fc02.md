代码评审：

1. **数据库变动**:
   - `promotion-lottery.sql` 文件中，`strategy_award` 表的数据被更新，奖品的中奖概率(`award_rate`)被调整，并增加了新的记录。这可能是为了调整抽奖策略，但需要确保这些变动不会影响现有的业务逻辑和系统的稳定性。
   - 新增了查询特定策略下奖品列表的 SQL 语句，这可能是为了支持新的业务需求。

2. **依赖变动**:
   - `pom.xml` 和 `promotion-lottery-app/pom.xml` 中增加了 Redisson 的依赖，这表明项目开始使用 Redisson 来处理分布式锁、队列等 Redis 操作，这是一个好的选择，因为 Redisson 提供了很多方便的 Redis 操作封装。

3. **Redis 配置**:
   - 新增了 `RedisClientConfig` 和 `RedisClientConfigProperties` 类来配置 Redis 连接，这是合理的，因为使用配置文件来管理配置参数更加灵活和方便。

4. **MyBatis 映射文件**:
   - `strategy_award_mapper.xml` 中新增了查询特定策略下奖品列表的 SQL 映射，这与数据库变动相对应，支持新的业务需求。

5. **单元测试**:
   - 新增了 `StrategyTest` 类，其中包括了策略装配和随机获取奖品ID的测试，这有助于确保新的策略逻辑是正确的。但是，测试用例需要更加全面，覆盖更多的边界情况和异常情况。

6. **领域模型**:
   - 新增了 `StrategyAwardEntity`、`AwardEntity` 和 `StrategyConditionEntity` 类，这些实体类可能用于表示领域模型中的实体，这是 DDD（领域驱动设计）实践的一部分。

7. **策略装配服务**:
   - `IStrategyArmory` 和 `StrategyArmory` 接口和实现类用于装配抽奖策略，这是新的业务逻辑，需要确保其正确性和效率。

8. **仓储实现**:
   - `StrategyRepository` 类实现了 `IStrategyRepository` 接口，提供了查询策略奖品列表和存储策略奖品概率查找表的方法，这是领域模型与数据库之间的桥梁。

9. **Redis 服务**:
   - `IRedisService` 和 `RedissonService` 接口和实现类提供了 Redis 操作的方法，这是项目开始使用 Redis 的体现。

总体来说，这次代码变动较大，涉及数据库、依赖、配置、领域模型、服务和测试等多个方面。需要确保这些变动不会引入新的问题，并且需要通过充分的测试来验证新的功能和逻辑的正确性。