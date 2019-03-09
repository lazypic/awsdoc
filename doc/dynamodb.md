# DynamoDB
최초 개발단계에서는 비용을 줄이기 위해서 On-Demand로 셋팅합니다.

## 테이블리스트 보기

```bash
$ aws dynamodb list-tables
```

## 전체 아이템 보기

```bash
$ aws dynamodb scan --table-name client
```

## 특정 아이템 가지고오기

```bash
$ aws dynamodb get-item --table-name client --key '{"name":{"S":"75mm-studio"}}'
```

## 쿼리
딱 하나만 가지온다.
```
$ aws dynamodb query --table-name cashflow --key-condition-expression 'id = :id' --expression-attribute-values '{":id": {"N":"1"}}'
```
관련자료 : https://stackoverflow.com/questions/31017460/query-a-single-value-with-hash-and-range-amazon-dynamodb




## Reference
- http://www.daleseo.com/aws-cli-dynamodb/