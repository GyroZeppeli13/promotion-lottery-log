根据提供的 git diff 记录，以下是代码评审的要点：

**1. 数据库变更**:

*   **`promotion-lottery.sql` 和 `promotion-lottery_01.sql`**:
    *   更新了 `raffle_activity_count` 和 `raffle_activity_sku` 表的数据，包括活动计数和库存数量。
    *   新增了 `strategy_rule` 表，用于存储抽奖策略规则。
    *   更新了 `strategy` 表，增加了规则模型字段。
    *   更新了 `strategy_award` 表，调整了奖品数量。
    *   新增了 `raffle_activity_account_month` 表，用于存储用户活动账户的月次数信息。
    *   更新了 `raffle_activity_order_001` 表，增加了新的订单数据。
    *   更新了 `task` 表，增加了新的任务数据。
    *   更新了 `user_award_record_001` 表，增加了新的中奖记录数据。
    *   更新了 `user_behavior_rebate_order_001` 表，增加了新的返利订单数据。
    *   新增了 `user_behavior_rebate_order_000` 和 `user_behavior_rebate_order_002` 表，用于存储用户行为返利订单数据。
*   **`promotion-lottery_02.sql`**:
    *   更新了 `raffle_activity_account` 表，增加了新的用户活动账户数据。
    *   新增了 `raffle_activity_order_000` 表，用于存储抽奖活动订单数据。
    *   新增了 `task` 表，用于存储任务数据。

**2. 代码变更**:

*   **`IRaffleActivityService.java`**:
    *   新增了 `isCalendarSignRebate` 和 `queryUserActivityAccount` 方法，分别用于判断用户是否完成日历签到返利和查询用户活动账户信息。
*   **`IRaffleStrategyService.java`**:
    *   新增了 `queryRaffleStrategyRuleWeight` 方法，用于查询抽奖策略权重规则配置。
*   **`RaffleStrategyRuleWeightRequestDTO.java` 和 `RaffleStrategyRuleWeightResponseDTO.java`**:
    *   新增了请求和响应对象，用于查询抽奖策略权重规则配置。
*   **`UserActivityAccountRequestDTO.java` 和 `UserActivityAccountResponseDTO.java`**:
    *   新增了请求和响应对象，用于查询用户活动账户信息。
*   **`RaffleActivityControllerTest.java`**:
    *   新增了测试用例，用于测试 `isCalendarSignRebate` 和 `queryUserActivityAccount` 方法。
*   **`RaffleStrategyControllerTest.java`**:
    *   新增了测试用例，用于测试 `queryRaffleStrategyRuleWeight` 方法。
*   **`IActivityRepository.java`**:
    *   新增了 `queryRaffleActivityAccountPartakeCount` 和 `queryActivityAccountEntity` 方法，分别用于查询用户活动账户参与次数和查询活动账户实体信息。
*   **`IRaffleActivityAccountQuotaService.java`**:
    *   新增了 `queryRaffleActivityAccountPartakeCount` 和 `queryActivityAccountEntity` 方法，分别用于查询用户活动账户参与次数和查询活动账户实体信息。
*   **`AbstractRaffleActivityAccountQuota.java`**:
    *   实现了 `queryRaffleActivityAccountPartakeCount` 和 `queryActivityAccountEntity` 方法。
*   **`IBehaviorRebateRepository.java`**:
    *   新增了 `queryOrderByOutBusinessNo` 方法，用于根据外部业务ID查询用户行为返利订单。
*   **`BehaviorRebateOrderEntity.java`**:
    *   新增了 `outBusinessNo` 字段，用于存储业务防重ID。
*   **`BehaviorRebateService.java`**:
    *   实现了 `queryOrderByOutBusinessNo` 方法。
*   **`IBehaviorRebateService.java`**:
    *   新增了 `queryOrderByOutBusinessNo` 方法。
*   **`IStrategyRepository.java`**:
    *   新增了 `queryActivityAccountTotalUseCount` 和 `queryAwardRuleWeight` 方法，分别用于查询用户活动账户总使用量和查询奖品权重配置。
*   **`RuleWeightVO.java`**:
    *   新增了值对象，用于存储权重规则信息。
*   **`IRaffleRule.java`**:
    *   新增了 `queryAwardRuleWeight` 和 `queryAwardRuleWeightByActivityId` 方法，分别用于查询奖品权重配置。
*   **`DefaultRaffleStrategy.java`**:
    *   实现了 `query