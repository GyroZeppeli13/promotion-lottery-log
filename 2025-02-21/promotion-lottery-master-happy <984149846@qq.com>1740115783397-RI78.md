根据提供的 `git diff` 记录，以下是对代码变更的评审：

**1. 数据库变更 (`promotion-lottery.sql`)**:
- `strategy` 表新增了三条记录，包括新的抽奖策略和相关的规则模型。
- `strategy_award` 表新增了三条记录，包括新的奖品和对应的策略ID。
- `strategy_rule` 表新增了三条记录，包括新的规则和对应的策略ID。

**2. MyBatis Mapper变更 (`strategy_award_mapper.xml`)**:
- 新增了一个查询方法 `queryStrategyAwardRuleModels`，用于查询特定奖品ID的规则模型。

**3. 单元测试变更 (`RaffleStrategyTest.java`)**:
- 新增了 `IStrategyArmory` 和 `RuleLockLogicFilter` 的依赖注入。
- `setUp` 方法中增加了策略装配的测试，并设置了 `userScore` 和 `userRaffleCount` 的模拟值。
- 新增了 `test_raffle_center_rule_lock` 测试方法，用于验证抽奖次数解锁规则。

**4. 接口变更 (`IStrategyRepository.java`)**:
- 新增了 `queryStrategyAwardRuleModelVO` 方法，用于查询奖品规则模型。

**5. 实体类变更 (`RaffleFactorEntity.java`)**:
- 新增了 `awardId` 属性，用于表示奖品ID。

**6. 抽奖策略抽象类变更 (`AbstractRaffleStrategy.java`)**:
- 新增了 `doCheckRaffleCenterLogic` 方法，用于执行抽奖中规则过滤。

**7. 默认抽奖策略变更 (`DefaultRaffleStrategy.java`)**:
- 实现了 `doCheckRaffleCenterLogic` 方法，用于执行抽奖中规则过滤。
- 优化了 `doCheckRaffleBeforeLogic` 方法，增加了空逻辑判断。

**8. 规则工厂变更 (`DefaultLogicFactory.java`)**:
- 新增了 `LogicModel` 枚举的 `type` 属性，用于区分规则类型（抽奖前、抽奖中、抽奖后）。
- 新增了 `fromCode` 和 `isCenter`、`isAfter` 方法，用于根据代码获取枚举实例和判断规则类型。

**9. 新增规则实现 (`RuleLockLogicFilter.java`)**:
- 实现了 `RuleLockLogicFilter` 类，用于处理抽奖次数解锁规则。

**10. 积分权重规则变更 (`RuleWeightLogicFilter.java`)**:
- 优化了 `filter` 方法，改为寻找最接近符合的积分值。

**11. 数据访问层变更 (`StrategyRepository.java` 和 `IStrategyAwardDao.java`)**:
- 实现了 `queryStrategyAwardRuleModelVO` 方法，用于查询奖品规则模型。

**12. 常量类变更 (`Constants.java`)**:
- 新增了 `UNDERLINE` 常量，用于表示下划线。

**评审意见**:
- 代码变更看起来是为了增加新的抽奖策略和规则，以及相关的测试和实现。
- 新增的规则类型和实现类使得代码更加模块化和可扩展。
- 单元测试的覆盖范围有所增加，有助于确保代码质量。
- 代码风格和命名规范保持一致，易于理解和维护。

**建议**:
- 确保所有新增的代码都有相应的单元测试覆盖。
- 考虑对数据库变更进行版本控制，以便于管理和回滚。
- 在代码中添加注释，解释新增的规则和逻辑。
- 对 `RuleWeightLogicFilter` 的优化进行测试，确保其符合预期行为。

**总体而言，代码变更看起来合理且符合良好的编程实践。建议在合并到主分支之前，进行彻底的测试和代码审查**。