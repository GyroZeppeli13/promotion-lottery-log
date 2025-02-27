代码评审：

1. **数据库脚本变更**:
    - `promotion-lottery.sql` 文件中，对 `rule_tree_node` 表的 `rule_luck_award` 规则的 `rule_value` 字段进行了更新，由 "1,100" 改为 "101:1,100"。这表明可能增加了新的配置项，需要确认该变更是否影响了相关业务逻辑。
    - 同样在 `promotion-lottery.sql` 文件中，对 `strategy_award` 表的数据进行了更新，涉及到奖品库存和描述的变更。需要确保这些变更与实际业务需求相符，并且已经通知到相关团队成员。

2. **依赖版本更新**:
    - `pom.xml` 文件中，`redisson-spring-boot-starter` 版本从 3.23.4 升级到 3.26.0。需要确认新版本是否兼容现有代码，并且是否需要进行额外的配置调整。

3. **代码结构变更**:
    - `Application.java` 文件中，增加了 `@EnableScheduling` 注解，这表明应用中增加了定时任务的功能。需要确保定时任务逻辑的正确性，并且已经进行了充分的测试。

4. **MyBatis 映射文件变更**:
    - `strategy_award_mapper.xml` 文件中，增加了 `updateStrategyAwardStock` 的 SQL 更新操作。需要确保这个更新操作与业务逻辑相符，并且已经进行了数据库层面的测试。

5. **单元测试变更**:
    - `RaffleStrategyTest.java` 文件中，增加了对库存扣减和队列操作的测试。这是一个好的实践，但需要确保测试用例的全面性和准确性，覆盖各种边界情况。

6. **接口变更**:
    - `IStrategyRepository.java` 接口中，增加了缓存奖品库存和扣减库存的相关方法。需要确保这些方法实现正确，并且与业务逻辑相符。

7. **领域模型变更**:
    - 新增了 `StrategyAwardStockKeyVO.java`，用于表示策略奖品库存的键。这是一个好的实践，可以清晰地表示领域模型。

8. **策略服务变更**:
    - `AbstractRaffleStrategy.java` 和 `DefaultRaffleStrategy.java` 中，增加了对库存操作的支持。需要确保这些变更不会影响到现有抽奖策略的逻辑。

9. **规则树节点变更**:
    - `RuleLockLogicTreeNode.java`、`RuleLuckAwardLogicTreeNode.java` 和 `RuleStockLogicTreeNode.java` 中，增加了对规则值参数的处理。需要确保这些变更不会影响到现有规则节点的逻辑。

10. **仓储实现变更**:
    - `StrategyRepository.java` 中，实现了缓存奖品库存和扣减库存的相关方法。需要确保这些方法实现正确，并且进行了充分的测试。

11. **Redis 服务变更**:
    - `IRedisService.java` 和 `RedissonService.java` 中，增加了对原子操作和延迟队列的支持。需要确保这些变更不会影响到现有 Redis 操作的逻辑。

12. **定时任务变更**:
    - 新增了 `UpdateAwardStockJob.java`，用于异步更新奖品库存。需要确保定时任务配置正确，并且已经进行了充分的测试。

总体来说，代码变更涉及到数据库脚本、依赖版本、代码结构、MyBatis 映射文件、单元测试、接口、领域模型、策略服务、规则树节点、仓储实现、Redis 服务和定时任务等多个方面。需要确保所有变更都已经经过充分的测试，并且与实际业务需求相符。同时，需要确保所有变更都已经通知到相关团队成员，并进行代码审查和代码合并操作。