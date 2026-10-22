# 领券方案

## 约定

- 活动 spring-01，发行上限 100 张。
- 领券成功后返回 coupon_id；查到用户已领取时直接返回原券。
- 用数据库中活动额度记录的 remaining 表示剩余可发放数。

## 处理流程

1. 从认证层取得 user_id。
2. 查询当前用户在本活动的券；存在则返回原 coupon_id。
3. 查询活动额度；remaining 为 0 时返回已领完。
4. 创建新的 coupon_id，插入当前用户的券记录。
5. 将 remaining 减 1。
6. 返回新 coupon_id。

## 查询

按 activity_id 和当前 user_id 查询券记录，返回已领取的 coupon_id。
