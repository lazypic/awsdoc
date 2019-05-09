# Project Backup

## S3백업
1. project-circle 버킷을 정리합니다.
1. S3에서 진행된 프로젝트는 lazypic-glacier 버킷으로 이동합니다.

```
$ aws s3 cp s3://project-circle/ s3://lazypic-glacier/circle/ --recursive --profile lazypic
```
