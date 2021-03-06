# Software

오픈소스프로그램 + 자체제작 소프트웨어를 사용하여 콘텐츠를 제작합니다.
제작에 사용되는 프로그램은 s3://lazypic-app 버킷으로 관리됩니다.
OS 설치이후 해당 버킷에 존재하는 프로그램을 한번에 다운로드합니다.
lazypic은 macOS, CentOS만 지원합니다.

## 목 적
- 아티스트 셋팅통일화
- EC2 인스턴스로 렌더팜 생성시 application 일괄 셋팅
- OS별 소프트웨어 관리
- 서울리전을 이용해서 클라이언트, EC2에 설치속도 향상

## uname
각 OS 에서 uname 명령어를 실행하면 OS 이름이 출력됩니다.
macOS는 `Darwin`이 출력되고, `CentOS`는 Linux 라고 출력됩니다.
이 문자를 이용해서 아래에서 진행되는 예제 코드부터는
os별로 소프트웨어를 구분합니다.

## 소프트웨어 목록

버전을 정확하게 맞추어야 하는 프로그램만 업로드합니다.

- s3://lazypic-app/uname/blender
- s3://lazypic-app/uname/blenderdev

아직 버전을 정확하게 맞추지 않아도 바로 협업할 수 있는 프로그램

- s3://lazypic-app/uname/krita
- s3://lazypic-app/uname/ardour
- s3://lazypic-app/uname/inkscape
- s3://lazypic-app/uname/gimp
- s3://lazypic-app/uname/djv


## 로컬 설치위치

~/app

## Security policy

s3AppUser

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
            "Resource": "arn:aws:s3:::lazypic-app"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:GetObjectAcl"
            ],
            "Resource": "arn:aws:s3:::lazypic-app/*"
        }
    ]
}
```

s3AppAdmin
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
            "Resource": "arn:aws:s3:::lazypic-app"
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
            "Resource": "arn:aws:s3:::lazypic-app/*"
        }
    ]
}
```
