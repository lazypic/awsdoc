# Software

오픈소스프로그램 + 자체제작 소프트웨어를 사용하여 콘텐츠를 제작합니다.
제작에 사용되는 프로그램은 s3://app.lazypic.org 버킷으로 관리됩니다.
OS 설치이후 해당 버킷에 존재하는 프로그램을 한번에 다운로드합니다.
lazypic은 macOS, CentOS만 지원합니다.

## 목적
- 아티스트 셋팅통일화
- EC2 인스턴스로 렌더팜 생성시 일괄 셋팅
- OS별 소프트웨어 관리

## 소프트웨어 목록

버전을 정확하게 맞추어야 하는 프로그램만 업로드합니다.

- s3://app.lazypic.org/uname/blender
- s3://app.lazypic.org/uname/blenderdev

아직 버전을 정확하게 맞추지 않아도 바로 협업할 수 있는 프로그램

- s3://app.lazypic.org/uname/krita
- s3://app.lazypic.org/uname/ardour
- s3://app.lazypic.org/uname/inkscape
- s3://app.lazypic.org/uname/gimp
- s3://app.lazypic.org/uname/djv


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
            "Resource": "arn:aws:s3:::app.lazypic.org"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:GetObjectAcl"
            ],
            "Resource": "arn:aws:s3:::app.lazypic.org/*"
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
            "Resource": "arn:aws:s3:::app.lazypic.org"
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
            "Resource": "arn:aws:s3:::app.lazypic.org/*"
        }
    ]
}
```