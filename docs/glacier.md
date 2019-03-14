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
볼트 내부 데이터를 확인하기 위해서 먼저 확인겠다고 하는 job을 생성합니다.

```
$ aws glacier initiate-job --account-id - --vault-name test_project --job-parameters '{"Type": "inventory-retrieval"}'
```

진행중인 Jobs는 아래 명령어를 이용해서 확인 가능합니다.
```
$ aws glacier list-jobs --account-id - --vault-name test_project
```

## Vault 리스트 확인하기

```bash
$ aws glacier list-vaults --account-id -
```

## Archive 삭제
```
$ aws glacier initiate-job --account-id - --vault-name test_project --job-parameters '{"Type": "inventory-retrieval"}'
$ aws glacier list-jobs --account-id - --vault-name test_project
```

StatusCode에 "InProgress" -> Completed가 뜨면 json 파일로 저장합니다.

```
$ aws glacier get-job-output --account-id - --vault-name test_project --job-id n7XzcNhdl0QMBK3G-Y3F8pLst9oqIlwafsdfsdfsdfsdfGhSL2CpNL2_3yYlgu1Cc-riLJIHVFkRLpnx0WTakjflndsflnaMpgDj0kw output.json
```

output.json파일을 보면 과거에 올렸던 Archive 갯수만큼 Archive 리스트가 저장되어 있습니다. archive-id 를 알아내고 삭제를 진행합니다.

```
$ aws glacier delete-archive --account-id - --vault-name test_project --archive-id n7XzcNhdl0QMBK3G-Y3F8pLst9oqIlwafsdfsdfsdfsdfGhSL2CpNL2_3yYlgu1Cc-riLJIHVFkRLpnx0WTakjflndsflnaMpgDj0kw
```

## Vault 삭제
볼트를 삭제하려면 내부가 비워져 있어야 합니다.
```
$ aws glacier delete-vault --account-id - --vault-name test_project
```

## S3 to Glacier
개인적으로는 S3에 이전 정책을 작성하여 사용하는 것이 더 편리합니다.