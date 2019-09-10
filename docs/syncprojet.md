# 프로젝트 동기화

### circle 프로젝트 Up Sync
노트북의 모든 데이터를 클라우드에 올릴 때 실행한다.
특이사항일 때 만 사용한다.

```bash
#!/bin/sh
aws s3 sync ~/project/circle s3://project-circle --profile lazypic
```

### publish
S3에는 과거 버전을 기억하고 있다. publish 할 때는 복사하면 된다.

```bash
#!/bin/sh
aws s3 cp ~/project/circle/file.ext s3://project-circle/file.ext --profile lazypic
```

### circle 프로젝트 Down Sync
최초 노트북에 아무 데이터도 없을 때 실행한다.

```bash
#!/bin/sh
aws s3 sync s3://project-circle ~/project/circle --profile lazypic
```
