# awsdoc

lazypic에서 자주 사용하는 AWS 명령어 문서 모음집 입니다.

## Service
- [S3](docs/s3.md)
- [Sns](docs/sns.md)
- [IAM](docs/iam.md)
- [Certificate Manager](docs/acm.md)
- [CloudFront](docs/cloudfront.md)
- [Cognito](docs/cognito.md)
- [Route53](docs/route53.md)
- [APIGatway](docs/apigatway.md)
- [Lambda](docs/lambda.md)
- [DynamoDB](docs/dynamodb.md)
- [DocumentDB](docs/documentdb.md)
- [Glacier](docs/glacier.md)

## Lang
- [Node.js](docs/nodejs.md)

## Install
awscli를 설치해야 합니다.

```bash
$ cd /tmp
$ curl -O https://bootstrap.pypa.io/get-pip.py
$ python3 get-pip.py
$ pip3 install awscli
```

## 권한
각 명령어가 잘 작동하기 위해서는 AWS_ACCESS_KEY_ID와 AWS_SECRET_ACCESS_KEY가 필요합니다.
admin@lazypic.org에 문의하세요.

## 테스트를 위한 참고사이트
- 테스트 이메일생성 : https://10minutemail.com

## 요금관련 계산기
- 가격 계산기 : https://calculator.s3.amazonaws.com/index.html
