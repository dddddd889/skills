# 现有服务与数据约定

这是本案例给定的环境事实，不需要查询外部服务。

- 活动服务配置 activity_id=spring-01，发行上限 total_limit=100。
- 领券接口为 POST /activities/spring-01/claim，当前登录用户标识 user_id 来自认证层；查询接口读取持久化的券记录。
- 部署环境有两个应用实例，请求可能落到任一实例。客户端网络失败后可能再次发送领取请求。
- PostgreSQL 支持事务、行锁、条件更新和唯一约束。数据库提交成功后查询接口可立即读到数据，不使用只读副本或缓存。
- 活动额度记录字段为 activity_id、remaining；券记录字段为 coupon_id、activity_id、user_id、created_at。
- 现有主键为 coupon_id。额度记录以 activity_id 为主键。
- 本次允许调整本案例的方案和计划，补充必要的约束和处理步骤；不允许更改本文件的接口、发行上限及环境能力，也不改变需求。
