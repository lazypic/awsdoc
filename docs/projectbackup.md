# Project Backup

## S3백업
1. projectname.lazypic.org 버킷을 정리합니다.
1. S3에서 진행된 프로젝트는 glacier.lazypic.org(S3 Glacier)로 이동합니다.

```
$ aws s3 mv s3://projectname.lazypic.org/ s3://glacier.lazypic.org/projectname/ --recursive --profile lazypic
```
