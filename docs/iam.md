# IAM
json을 이용해서 정책을 설정하는 방법입니다.
사용자를 먼저 생성후 각 사용자에 맞는 정책을 생성하고 물려서 사용합니다.

## S3
로그인 사용자마다 다른 정책을 부여할 때 사용합니다.
lazypic S3 버킷에 해당 사용자만 부여된 권한을 이용하는 방법입니다.
정책을 만들고 사용자에게 부여하여 사용하세요.

Statement에 `"Action": ["s3:ListAllMyBuckets"],"Resource": "arn:aws:s3:::*"` 항목이 추가되어야 버킷 리스트가 보입니다.

- 권한 : 읽기, 쓰기, 삭제


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
            "Resource": "arn:aws:s3:::lazypic"
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
            "Resource": "arn:aws:s3:::lazypic/*"
        }
    ]
}
```