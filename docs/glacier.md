
## Upload
데이터 업로드
```bash
$ aws glacier upload-archive --account-id - --vault-name my-vault --body archive.zip
```

## Tag 추가하기
```bash
$ aws glacier add-tags-to-vault --account-id - --vault-name my-vault --tags id=1234,date=july2015
```