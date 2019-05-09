# awsdoc
lazypic AWS 인프라를 운용하면서 작성되는 메뉴얼입니다.

- lazypic에서 프로젝트를 진행하며 자주 사용하는 AWS 명령어에 대해서도 설명되어 있습니다.
- lazypic은 유저별, 프로젝트별, ARN(리소스별)로 권한관리를 진행합니다.
- layzpic은 비용절감을 위해서 솔루션 제작시 Serverless 솔루션을 권장합니다.

> 이 문서는 프로젝트를 진행하면서 지속적으로 수정중입니다. 부분부분 설명이 매끄럽지 못할 수 있습니다.

## Service
- [S3](docs/s3.md)
- [Ses](docs/ses.md)
- [Sns](docs/sns.md)
- [IAM](docs/iam.md)
- [Certificate Manager](docs/acm.md)
- [CloudFront](docs/cloudfront.md)
- [Cognito](docs/cognito.md)
- [Route53](docs/route53.md)
- [APIGatway](docs/apigatway.md)
- [Lambda](docs/lambda.md)
- [SimpleDB](docs/simpledb.md)
- [DynamoDB](docs/dynamodb.md)
- [DocumentDB](docs/documentdb.md)
- [Glacier](docs/glacier.md)
- [ec2](docs/ec2.md)
- [Machine Learning](docs/ml.md)

## Function
- [Create Project](docs/createproject.md)
- [Backup Project](docs/backupproject.md)
- [Software](docs/software.md) : s3://lazypic-app 정책

## Mail
- [mailgun](docs/mailgun.md)

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

## AWS 키설정
각 명령어가 잘 작동하기 위해서는 AWS_ACCESS_KEY_ID와 AWS_SECRET_ACCESS_KEY가 필요합니다.

admin@lazypic.org에 문의하세요.

~/.aws/credentials 파일에 아래처럼 작성해주세요. 여러 AWS 계정을 사용중일 수 있으니 명확하게 lazypic 프로파일 이름을 지정해주세요.

```
[lazypic]
aws_access_key_id = AAAAAAAAAAAAAAAAAAAA
aws_secret_access_key = BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
```

## 테스트를 위한 참고사이트
- 테스트 이메일생성 : https://10minutemail.com
- 보안 정책 시뮬레이션 : https://policysim.aws.amazon.com/home/index.jsp

## 요금관련 계산기
- 가격 계산기 : https://calculator.s3.amazonaws.com/index.html
