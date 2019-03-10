# DynamoDB
최초 개발단계에서는 비용을 줄이기 위해서 On-Demand로 셋팅합니다.

## Attribute Value으로 사용하면 안되는 값
- https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/ReservedWords.html

- 자주 실수하는 단어 : name, type, date, unit

## 테이블리스트 보기

```bash
$ aws dynamodb list-tables
```

## 전체 아이템 보기

```bash
$ aws dynamodb scan --table-name client
```

## 특정 아이템 가지고오기
키를 이용하는 방법1

```bash
$ aws dynamodb get-item --table-name client --key '{"client":{"S":"75mm-studio"}}'
```

키를 이용하는 방법2

```bash
$ aws dynamodb get-item --table-name cashflow --key '{"id":{"N":"1"}}'
```

## 쿼리
딱 하나만 가지온다.

```bash
$ aws dynamodb query --table-name cashflow --key-condition-expression 'id = :id' --expression-attribute-values '{":id": {"N":"1"}}'
```
관련자료 : https://stackoverflow.com/questions/31017460/query-a-single-value-with-hash-and-range-amazon-dynamodb


## 스캔
대규모로 app 구축시 비싼 솔루션이다.
기본적으로 값을 가지고 올 수 있도록 app을 설계한다.

```bash
$ aws dynamodb scan --table-name cashflow --filter-expression "income = :t" --expression-attribute-values '{":t":{"BOOL":true}}'
```



## Reference
- http://www.daleseo.com/aws-cli-dynamodb/