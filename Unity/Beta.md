### 링킹 안내

예를 들어 Facebook 인증을 사용하여 게임을 이용하고 있는 사용자가 Google 인증으로도 동일한 사용자 아이디를 사용할 수 있도록 링킹 기능을 제공합니다. 하나의 사용자 아이디에 Facebook과 Google 인증을 링킹하면 게임 이용자는 어떤 기기에서는 Facebook, 또 다른 기기에서는 Google로 인증하여 게임을 할 수 있습니다.

링킹은 기존에 로그인된 계정에 다른 소셜 계정을 연동하거나 해제시키는 기능입니다.
많은 게임들이 하나의 계정에 여러 계정을 연동(Mapping)할 수 있도록 하고 있습니다.
GamePot의 Linking API를 사용하여 기존에 로그인된 계정에 다른 소셜의 계정을 연동/해제시킬 수 있습니다. 
주의할 점은, IdP 마다 하나의 계정씩만 연동이 가능합니다.

GamePot 사용자 ID : 123bcabca
Google ID : aa
Facebook ID : bb
AppleGameCenter ID : cc

GamePot 사용자 ID : 456abcabc
Google ID : ee
Google ID : ff -> 이미 Google ee 계정이 연동중이므로 Google계정을 추가로 연동할 수 없습니다.

### 링킹 API 방법
Linking 에는 Linking 정보/추가/해제 API 3개가 있습니다. 현재 링킹된 정보를 가져와서 UI 상에 링킹 정보를
표시해 줍니다. 표시된 링킹 정보에서 링킹을 시도할 경우 createLinking 을 링킹을 해제할 경우에는 deleteLinking 를 호출 합니다. API 는 아래와 같습니다. 

#### 현재 링킹된 전체 정보를 가져 옵니다.
List<NLinkingInfo> linkedList = GamePot.getLinkedList();

#### 구글과의 링킹을 연동 합니다.
GamePot.createLinking(NCommon.LinkingType.GOOGLE);

#### 구글과의 링킹을 연동을 해제 합니다.
GamePot.deleteLinking(NCommon.LinkType.GOOGLE);

public class NLinkingInfo
{
    public LinkingType provider { get; set; }  // google, facebook, naver
}