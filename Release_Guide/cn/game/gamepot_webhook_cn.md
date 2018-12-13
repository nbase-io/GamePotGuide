### 储值API对接方法

#### 储值成功之后服务器会对游戏服务器请求发放item物品

以以下形式对游戏服请求，依照此请求内容发放给用户相关物品即可

Request:

```web-idl
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productid={productId}&store={store}&payment={payment}&transactionId={transactionId}
```

| Attribute   | Type   | Description                                                  |
| ----------- | ------ | ------------------------------------------------------------ |
| domain      | String | 游戏服务器发放物品的服务器域名                               |
| userId      | String | 用户 UID                                                     |
| orderId     | String | 订单号 ( 自动生成 )                                          |
| projectId   | String | ProjectID                                                    |
| projectId   | String | Google/Apple/Onestore的商品ID                                |
| platform    | String | 平台 Platform信息 (Android, IOS)                             |
| store       | String | 渠道信息(ios, google, one)                                   |
| payment     | String | 储值方式 (apple, google, one, mycard, mol)                   |
| transaction | String | transaction id of Google/Apple/Onestore<br/>(ex. Google is “GPA.0000-0000-0000-00000”) |

Response:

```json
{
	"status": 1,
	"message" : ""
}
```

| Attribute | Type   | Description                 |
| --------- | ------ | --------------------------- |
| status    | Int    | 结果值 ( 0: 失败, 1: 成功 ) |
| message   | String | 错误内容                    |

