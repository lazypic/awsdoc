# SNS
lazypic에 이메일로 알람을 설정하는 방법.
보통 프로젝트가 시작되면 project 이름으로 topic을 만듭니다.
`000000000000` 문자 대신 자신의 Account ID를 사용해주세요.

## 토픽 생성하기.
lazypic에 `circle` 프로젝트로 topic을 생성합니다.

```bash
$ aws sns create-topic --name circle --profile lazypic
```

ARN 코드가 생성됩니다. 이 문서는 공개모델이기 때문에 문서에 적지 않습니다.

```
arn:aws:sns:ap-northeast-2:000000000000:circle
```

## 구독자 등록

woong@lazypic.org 유저를 circle 프로젝트의 topic의 구독자로 등록하는 방법.

```bash
$ aws sns subscribe --topic-arn arn:aws:sns:ap-northeast-2:000000000000:circle --protocol email --notification-endpoint woong@lazypic.org --profile lazypic
```

## 뉴스 전송
circle 프로젝트 구독자에게 test 라는 내용으로 이메일을 보내는 방법

```bash
$ aws sns publish --topic-arn arn:aws:sns:ap-northeast-2:000000000000:circle --message "test" --profile lazypic
```

- circle 프로젝트를 예로 들어 설명했지만 자유롭게 topic을 생성할 수 있습니다.
- 팀명으로 topic을 만들 수 있습니다.
- 동호회명으로 topic을 만들 수 있습니다.
