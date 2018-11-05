### 서버투서버 API 요청

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