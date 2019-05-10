# Create Project

## 프로젝트 생성
- S3 : s3://project-projectname
	- Amazon S3 Transfer Acceleration 를 사용하기 위해서는 `.`이 없어야 한다.
- ~/project/projectname/..
	- 리눅스를 기본적으로 설치하면 HOME 디렉토리 용량을 가장 많이 잡습니다.
	- 각 사용자별로 관리할 수 있다.
	- 사용자 계정의 ~/.aws/credential 파일을 설정하면 됩니다.
- Github : https://github.com/lazypic/projectname
- Slack : #projectname
- Amazon SNS : projectname

## 프로젝트 Sync 하기
~/project/circle 경로에 circle.sh 파일을 생성합니다. 파일내용은 아래와 같습니다.

현재 하위경로를 업로드하고, 새로 업데이트된 파일을 다운로드 하게 됩니다.

circle.sh
```sh
#!/bin/sh
FILENAME=$0
PROJECT="${FILENAME%.*}"
aws s3 sync s3://project-$PROJECT ~/project/$PROJECT --profile lazypic
```