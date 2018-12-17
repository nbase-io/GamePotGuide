---
search:
  keyword: ['gamepot']
---

### 储值API对接方法

## Purchase

支付完成后服务器会对游戏服务器请求发放物品。游戏服务会按照以下形式传达，依照此信息发放用户相关物品即可。

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
| productid   | String | Google/Apple/Onestore的商品ID                                |
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



## Item

使用优惠卷时会对游戏服务器请求发放物品
会依照以下形式来请求，游戏服务器就依照传达过来的内容发放给玩家相关物品即可。

Request:

```web-idl
https://{domain}?
userId={userId}&projectId={projectId}&platform={platform}&itemId=[{itemData}, {itemData}, ...]
```

| Attribute | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| userId    | String          | 用户 UID                                                     |
| projectId | String          | ProjectID                                                    |
| platform  | String          | 平台 Platform信息 (Android, IOS)                             |
| itemID    | Array<itemData> | itemData Array<br /><br />- itemData(JSON) <br /> {"item_id" : String, "store_item_id" : String, "count" : Number} |

ex) 
https://{domain}?itemId=[{"item_id":"989caae1-5f70-41d9-b797","store_item_id":"item1","count":1},{"item_id":"563e8ed5-ee1f-4f7f-a3c9","store_item_id":"item2","count":2}]&platform=android&userId=dcea66-0719-418-8dcd-f638f85e4

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



## Authentication check

请求验证用户ID 

请求验证时，GamePot服务器会实际的进行验证，按照验证结果会执行用户Block。

Request:

```web-idl
POST
url : https://{GamePot API URL}/loginauth
Header : 'content-type: application/json'
data: 
{
	"memberId": {GamePot SDK의 memberId},
	"token": {GamePot SDK의 Token}
}
```

| Attribute | Type   | Description            |
| --------- | ------ | ---------------------- |
| memberId  | String | GamePot SDK의 memberId |
| token     | String | GamePot SDK의 Token    |

GamePot API URL : GamePot Dashboard 网址的 :8080 之前的网址。 

Dashboard 网址为 https://xxxxxxx.gamepot.ntruss.com:8080/aaaaaaa-aaaaaaa-aaaaaa/dashboard/analysis 的时候 [xxxxxxx.gamepot.ntruss.com](https://0bmnkzvhzd.gamepot.ntruss.com:8080/d1516c57-f7b5-41cc-a22c-8c0aaff56259/dashboard/analysis)就指这部分。 

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