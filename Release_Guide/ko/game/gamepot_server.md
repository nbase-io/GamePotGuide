---
search:
  keyword: ['gamepot']
---

### 서버투서버 API 요청

## Purchase

결제 완료 후에 서버에서 게임서버로 아이템 지급에 대한 요청을 합니다.
게임서버에서는 아래와 같은 내용으로 전달드리고 해당 정보를 바탕으로 이용자에게 아이템을 지급하시면 됩니다.

```javascript
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productid={productId}&store={store}&payment={payment}&transactionId={transactionId}
```



| Attribute     | Type   | Description                                   |
| ------------- | ------ | --------------------------------------------- |
| userId        | String | 사용자 UID                                    |
| transactionId | String | 주문번호(GPA-xxxx-xxxx-)                      |
| store         | String | 스토어 정보(ios, google, one)                 |
| projectId     | String | 프로젝트ID                                    |
| productId     | String | 구글/애플/원스토어에 등록된 상품ID            |
| platform      | String | 운영 Platform 정보 (Android, IOS)             |
| payment       | String | 결제 방식 ( apple, google, one, mycard, mol ) |
| orderId       | String | 주문번호 ( 자동생성 )                         |
| domain        | String | 게임 서버에 아이템 지급 서버의 도메인         |



```json
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                 |
| --------- | ------ | --------------------------- |
| status    | Int    | 결과값 ( 0: 실패, 1: 성공 ) |
| message   | String | 오류 내용                   |


이와 같은 형식으로만 전달해 주셔야 처리가 가능하며 오류시에 오류 메시지를 적어주시면 추후 메시지를 확인이 가능합니다.  

## Item

쿠폰 사용 시 게임서버로 아이템 지급에 대한 요청을 합니다.
게임서버에서는 아래와 같은 내용으로 전달드리고 해당 정보를 바탕으로 이용자에게 아이템을 지급하시면 됩니다.

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
| status    | Int    | 결과값 ( 0: 실패, 1: 성공 ) |
| message   | String | 오류 내용                   |



## Authentication check

사용자 ID에 대한 검증을 요청 합니다. 

검증 요청 시 GamePot 서버에서는 실질적인 검증을 하며, 이에 따라 사용자 Block 처리를 하게 됩니다.

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

GamePot API URL : GamePot Dashboard 주소의 :8080 전 까지의 주소입니다. 

Dashboard 주소가 https://xxxxxxx.gamepot.ntruss.com:8080/aaaaaaa-aaaaaaa-aaaaaa/dashboard/analysis 이라면 [xxxxxxx.gamepot.ntruss.com](https://0bmnkzvhzd.gamepot.ntruss.com:8080/d1516c57-f7b5-41cc-a22c-8c0aaff56259/dashboard/analysis)를 뜻합니다. 

Response:

```json
{
	"status": 1,
	"message" : ""
}
```

| Attribute | Type   | Description                 |
| --------- | ------ | --------------------------- |
| status    | Int    | 결과값 ( 0: 실패, 1: 성공 ) |
| message   | String | 오류 내용                   |

