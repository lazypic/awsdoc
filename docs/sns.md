# SNS
lazypic에 이메일로 알람을 설정하는 방법.

## 토픽 생성하기.
lazypic에 `news` 라는이름의 topic을 생성합니다.

```bash
$ aws sns create-topic --name news
```

ARN 코드가 생성됩니다. 이 문서는 공개모델이기 때문에 문서에 적지 않습니다.

```
arn:aws:sns:ap-northeast-2:000000000000:news
```

## 구독자 등록

구독자를 등록하는 방법.

```bash
$ aws sns subscribe --topic-arn arn:aws:sns:ap-northeast-2:000000000000:news --protocol email --notification-endpoint woong@lazypic.org
```

## 뉴스 전송
구독자에게 test 라는 내용으로 이메일을 보내는 방법

```bash
$ aws sns publish --topic-arn arn:aws:sns:ap-northeast-2:000000000000:news --message "test"
```

- 프로젝트명으로 topic을 만들 수 있습니다.
- 팀명으로 topic을 만들 수 있습니다.
- 동호회명으로 topic을 만들 수 있습니다.
