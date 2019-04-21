# IAM
json을 이용해서 정책을 설정하는 방법입니다.
사용자를 먼저 생성후 각 사용자에 맞는 정책을 생성하고 물려서 사용합니다.

## 사용자 생성
```
$ aws iam create-user --user-name woong@lazypic.org --profile lazypic
```

- 초기비밀번호 : `Nice2meetyou!`
- 로그인 이후 사용자의 새 비밀번호 생성을 요청합니다.

## 정책검색
```
$ aws iam list-policies --query 'Policies[?PolicyName==`AmazonS3FullAccess`].{ARN:Arn}' --output text --profile lazypic
```

## 사용자와 정책을 연결하는 방법
```
$ aws iam attach-user-policy --user-name username --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess --profile lazypic
```

## 사용자의 정책 확인
```
$ aws iam list-attached-user-policies --user-name username --profile lazypic
```

## 제한된 S3 정책을 생성하고 적용하기 
로그인 사용자마다 다른 정책을 부여할 때 사용합니다.
lazypic S3 버킷에 해당 사용자만 부여된 권한을 이용하는 방법입니다.
정책을 만들고 사용자에게 부여하여 사용하세요.

Statement에 `"Action": ["s3:ListAllMyBuckets"],"Resource": "arn:aws:s3:::*"` 항목이 추가되어야 버킷 리스트가 보입니다.

- 권한 : 읽기, 쓰기, 삭제


먼저 명령어를 이용해서 정책을 생성합니다.
```
$ aws iam create-policy --policy-name my-policy --policy-document file://policy
```

policy 파일내용
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets"
            ],
            "Resource": "arn:aws:s3:::*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:GetBucketLocation"
            ],
            "Resource": "arn:aws:s3:::bucketname"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:GetObjectAcl",
                "s3:PutObject",
                "s3:PutObjectAcl",
                "s3:DeleteObject"
            ],
            "Resource": "arn:aws:s3:::bucketname/*"
        }
    ]
}
```

## MFA 생성
MFA를 위해서 디바이스등록, QR코드를 생성합니다.

```bash
$ aws iam create-virtual-mfa-device --virtual-mfa-device-name clientnameMFADevice --outfile /tmp/qrcode/woong@lazypic.org --bootstrap-method QRCodePNG --profile lazypic
```

사용자와 연결하기
Google Authenticator 로 생성되는 코드 2개를 연달아서 입력해야합니다. 210987654321 값 대신 AccountID를 입력합니다.

```bash
$ aws iam enable-mfa-device --user-name woong@lazypic.org --serial-number arn:aws:iam::210987654321:mfa/clientnameMFADevice --authentication-code-1 123456 --authentication-code-2 789012 --profile lazypic
```


## 응용
- 아래 절차를 거쳐서 클라이언트 셋팅을 자동화 할 수 있습니다.
    1. 클라이언트 이름으로 사용자 생성
    1. 사용자가 사용해야할 MFA QR코드 생성
    1. 사용자 제한 정책 생성
    1. 사용자에게 정책 연결
    1. 사용자만 쓸 수 있는 S3 버킷생성
