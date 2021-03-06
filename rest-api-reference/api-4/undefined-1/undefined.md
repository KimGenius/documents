# 그룹 생성

메시지 그룹 생성 API 사용방법을 기술합니다.

메시지 그룹은 메시지 메시지들을 담는 그릇이 되며, 한번의 요청으로 대량의 메시지를 관리/발송하려면 발송 전 메시지 그룹을 생성해야 합니다. 또한 이미 발송에 사용된 메시지 그룹은 더 이상 발송할 수 없습니다.

## Request

POST [https://rest.coolsms.co.kr/messages/v4/groups](https://rest.coolsms.co.kr/messages/v4/groups)

curl -X POST [https://rest.coolsms.co.kr/messages/v4/groups](https://rest.coolsms.co.kr/messages/v4/groups)  --header "Authorization : HMAC-SHA256 ApiKey=\[API\_KEY\], Date=\[DATE\], Salt=\[UNIQID\], Signature= \[SIGNATURE\]" \

### Optional Body Parameters

* `appId` - 쿨에스엠에스 앱스토어에 앱이 등록되어 있는 경우, 해당 앱의 아이디를 이용하여 발송 시 수익을 공유 받습니다.
* `appVersion` - 발송하는 앱의 버전
* `osPlatform` - 발송 운영체제 환경

### Sample Code

{% tabs %}
{% tab title="NodeJS" %}
```text
request({ url: "
https://rest.coolsms.co.kr/messages/v4/groups
",method: 'post', headers: { 'Authorization': HMAC-SHA256 ApiKey=[API_KEY], Date=[DATE], Salt=[UNIQID], Signature=[SIGNATURE] }, json: { appId: 'MYAPPID' } } )
```
{% endtab %}

{% tab title="Python" %}
```text
conn = HTTPSConnection('rest.coolsms.co.kr') conn.request( "POST", "/messages/v4/groups","{appId:'MYAPPID'}", {"Authorization":"HMAC-SHA256 ApiKey=[API_KEY], Date=[DATE], Salt=[UNIQID], Signature=[SIGNATURE]"}) conn.close()
```
{% endtab %}

{% tab title="PHP" %}
```text
<?php $ch = curl_init(); curl_setopt($ch, CURLOPT_URL, "
https://rest.coolsms.co.kr/messages/v4/groups
"); curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST"); curl_setopt($ch, CURLOPT_POSTFIELDS, "{'appId':'MYAPPID'}"); curl_setopt($ch, CURLOPT_HTTPHEADER, array( 'Authorization: HMAC-SHA256 ApiKey=[API_KEY], Date=[DATE], Salt=[UNIQID], Signature=[SIGNATURE]' )); curl_exec($ch); curl_close($ch);
```
{% endtab %}
{% endtabs %}

## Response

{ "agent": { "appId": "String", "appVersion": "String", "sdkVersion": "String", "osPlatform": "String" }, "count": { "sms": Int, "lms": Int, "mms": Int, "ata": Int, "cta": Int, "push": Int }, "log": Array, "groupId": "String", "status": "String", "accountId": "String", "apiVersion": "String", "\_id": "String" }

{ "agent": { "appId": "MYAPPID", "appVersion": null, "sdkVersion": null, "osPlatform": null }, "count": { "sms": 0, "lms": 0, "mms": 0, "ata": 0, "cta": 0 }, "log": \[ { "date": "2018-04-03 15:32:21", "message": "메시지 그룹 생성", "agent": { "appId": "MYAPPID", "appVersion": null, "sdkVersion": null, "osPlatform": null } } \], "groupId": "G4V20180403153221CKAFBUVJ51OF7AV", "status": "PENDING", "accountId": "12925149", "apiVersion": "4", "\_id": "G4V20180403153221CKAFBUVJ51OF7AV" }

* `agent` - 사용자 agent 정보
  * `appId` - 그룹 생성 시 함께 요청한 appId
  * `appVersion` - 그룹 생성 시 함께 요청한 앱 버전
  * `sdkVersion` - sdk를 이용하여 발송한 경우 해당 sdk의 버전
  * `osPlatform` - 그룹 생성 시 함께 요청한 운영체제 환경
* `count` - 그룹에 등록되어 있는 문자메시지 수
  * `sms` - 그룹에 등록된 sms 수
  * `lms` - 그룹에 등록된 lms 수
  * `mms` - 그룹에 등록된 mms 수
  * `ata` - 그룹에 등록된 ata 수
  * `cta` - 그룹에 등록된 cta 수
* `log` - 해당 메시지 그룹의 모든 이력 정보
* `groupId` - 해당 메시지 그룹의 아이디
* `status` - 해당 메시지 그룹의 상태 정보. \(자세한 사항은 그룹정보조회 문서 참조\)
* `accountId` - 사용자 고유 값
* `apiVersion` - 요청에 사용된 api 버전 정보
* `_id` - groupId와 동일한 그룹 고유 값

  **Errors**

* `InvalidAppId(400)` - 유효하지 않은 앱 아이디 

