# Glacier
백업을 위해서 사용합니다.

## Vault 생성
test_project 이름으로 vault 이름을 생성합니다.

```bash
$ aws glacier create-vault --account-id - --vault-name test_project
```

## Upload
데이터 업로드
```bash
$ aws glacier upload-archive --account-id - --vault-name test_project --body archive.zip
```

## Tag 추가하기
```bash
$ aws glacier add-tags-to-vault --account-id - --vault-name test_project --tags id=1234,date=july2015
```