# Glacier
백업을 위해서 사용합니다. circle 프로젝트를 예로들어서 설명합니다.

## Vault 생성
test_project 이름으로 vault 이름을 생성합니다.

```bash
$ aws glacier create-vault --account-id - --vault-name circle
```

## Upload
데이터 업로드
```bash
$ aws glacier upload-archive --account-id - --vault-name circle --body circle.zip
```

## Tag 추가하기
```bash
$ aws glacier add-tags-to-vault --account-id - --vault-name circle --tags project=circle,date=2019.03.07
```

## 진행중인 Job을 확인하기

```bash
$ aws glacier list-jobs --account-id - --vault-name test_project
```

## Vault 내부 데이터 확인
볼트 내부 데이터를 확인하는 방법입니다.


## Vault 리스트 확인하기

```bash
$ aws glacier list-vaults --account-id -
```

## 삭제
볼트를 삭제하려면 내부가 비워져 있어야 합니다.