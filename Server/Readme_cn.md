### Server To Server API 请求

支付完成后服务器会对游戏服务器请求发放物品。游戏服务会按照以下形式传达，依照此信息发放用户相关物品即可。

```javascript
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productid={productId}&store={store}&payment={payment}&transactionId={transactionId}
```



| Attribute     | Type   | Description                                   |
| ------------- | ------ | --------------------------------------------- |
| userId        | String | 用户 UID                                    |
| transactionId | String | 订单号(GPA-xxxx-xxxx-)                     |
| store         | String | 渠道信息(ios, google, one)                 |
| projectId     | String | Project ID                                    |
| productId     | String | Google/Apple/Onestore所登记的物品ID            |
| platform      | String | 运营Platform信息 (Android, IOS)            |
| payment       | String | 支付方式( apple, google, one, mycard, mol ) |
| orderId       | String | 点单号 ( 自动生成 )                         |
| domain        | String | 游戏服务器所发放物品的服务器域名         |



```json
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                 |
| --------- | ------ | --------------------------- |
| status    | Int    | 结果值 ( 0: 失败, 1: 成功 ) |
| message   | String | 错误信息                  |


必须要按照以上形式传达信息才能正常处理。错误时提示相关错误信息的化之后可以确认内容。

