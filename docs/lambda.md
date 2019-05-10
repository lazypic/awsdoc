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
아래 람다 함수가 작동되기 위해서는 람다 실행함수 권한에 추가로 필요한 권한을 적용해야 합니다.
저는 람다함수에 SNS를 물리는 작업을 진행하고 있기 때문에 아래 권한을 설정했습니다.

- AWSLambdaSNSPublishPolicyExecutionRole
- AWSLambdaBasicExecutionRole

실행코드
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

```bash
$ curl -d '{"key1":"value1", "key2":"value2"}' -H "Content-Type: application/json" -X POST https://lpn8sb0mc9.execute-api.ap-northeast-2.amazonaws.com/estimate
```

## Reference
- https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/python-programming-model-handler-types.html
- https://m.youtube.com/watch?v=g7AHiymJ7I4
