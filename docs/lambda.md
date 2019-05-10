# Lambda


## Node.js 버전
node.js 8.10, 6.10을 지원합니다.
https://nodejs.org/dist/v0.8.10/


웹에서 인라인 편집기를 사용할 수 있기 때문에 굉장히 빠르게 app을 설계할 수 있습니다.

## Python 예제
기본적으로 아래 코드를 작성하고 event와 context의 구조를 확인할 수 있습니다.

```python
def handler_name(event, context): 
    print(event)
    print(context)
    return event
```

## DynamoDB 연동
리서치
#### Create
#### Read
#### Update
#### Delete

## S3 데이터 업로드
리서치

## S3 데이터 다운로드
리서치

## SNS 전송
람다 함수는 아래와 같다. 이 함수가 작동되기 위해서는 gatewayAPI, Lambda, SNS 모두 권한이 존재해야 한다.

```javascript
var ACCOUNTID = "000000000000"
var AWS = require("aws-sdk");

exports.handler = function(event, context) {
    var eventText = JSON.stringify(event, null, 2);
    let responseBody = {
        message: `${event}`,
        input: event
    };
    let response = {
        statusCode: 200,
        body: JSON.stringify(responseBody)
    };
    var sns = new AWS.SNS();
    var params = {
        Message: eventText, 
        Subject: "Test SNS From Lambda",
        TopicArn: "arn:aws:sns:ap-northeast-2:${ACCOUNTID}:circle"
    };
    sns.publish(params, context.done);
    return response;
};
```

터미널에서 실행해보기.
```
$ curl -d '{"key1":"value1", "key2":"value2"}' -H "Conion/json" -X POST https://lpn8sb0mc9.execute-api.ap-northeast-2.amazonaws.com/estimate
```

## Reference
- https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/python-programming-model-handler-types.html
- https://m.youtube.com/watch?v=g7AHiymJ7I4
