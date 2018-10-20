# 부록

## 1. 스토어 변경

SDK적용이 완료된 상태에서 다른 스토어로 변경하려면 build.gradle에 관련 설정을 변경해야 합니다.

스토어를 변경하더라도 기존 계정은 그대로 사용 가능하며, 스토어에 해당하는 결제 모듈이 사용된다고 보시면 됩니다.

해당 항목은 Android만 해당하며 SDK에서 지원하는 스토어는 아래와 같습니다.

* [Google store](https://play.google.com/store)
* [One store](https://www.onestore.co.kr)

가이드는 Google store에서 One store로 변경하는 방법에 대한 가이드입니다.

1. build.gradle 수정

   1. `gamepot_store` 값을 `one`으로 변경

      ```java
      resValue "string", "gamepot_store", "one" // required
      ```

   2. IGAWorks를 사용하고 스토어별로 구분할 경우 `gamepot_igaworks_app_key`와 `gamepot_igaworks_hash_key` 에 값을 변경

      ```java
      resValue "string", "gamepot_igaworks_app_key", "000000000"
      resValue "string", "gamepot_igaworks_hash_key", "aaaaaaaaaaaaaaaaa"
      ```

   3. Adjust를 사용하고 스토어별로 구분할 경우 `gamepot_adjust_apptoken`와 `gamepot_adjust_signature` 에 값을 변경

      ```java
      resValue "string", "gamepot_adjust_apptoken","aaaaaaaaaaaa"
      resValue "string", "gamepot_adjust_signature","(1, 111111111, 111111111, 111111111, 111111111)"
      ```

   4. `gamepot-billing-onestore.aar` 파일 추가

      ```java
      ...
      dependencies {
      	...
      	implementation(name: 'gamepot-billing-onestore', ext: 'aar')
      	...
      }
      ```

2. `purchase ` api 호출 시 `producId`  값을 스토어 별로 맞는 값으로 수정

   ```java
   GamePot.getInstance().purchase('productid');
   ```
