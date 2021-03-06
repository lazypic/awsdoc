# SimpleDB
문자만 저장가능하다. 하지만 많이 사용하는 이유는 비용이 엄청 저렴하기 때문이다. 1기가 미만의 작은 규모에서는 항상 $0가 나온다.
관리콘솔이 없다. 명령어로만 사용가능함.

위 특징으로 지켜야할 주의사항.
- 단순한 데이터에서만 저장할 것.
- 시간은 ISO 표준으로 저장한다.
- 숫자는 제로패딩으로 저장한다.

## cli에서 sdb 옵션을 활성화
aws cli에는 기본적으로 simpleDB가 활성화 되어있지 않습니다.
터미널에서 다음처럼 입력하여 활성화 합니다.

```bash
$ aws configure set preview.sdb true
```

## 지원리전
아직 서울을 지원하지 않는다. 명령어를 날릴 때 도쿄리전을 사용합니다.

```bash
$ aws sdb create-domain --domain-name test --region ap-northeast-1
```

## 리소스알아보기
- My Account 메뉴에서 Account ID 조회가 필요하다.
- 도쿄리전 : ap-northeast-1

## 정책생성
IAM에서 수동으로 정책을 생성해줍니다.

```
{
   "Version": "2012-10-17",
   "Statement":[{
      "Effect":"Allow",
      "Action":"sdb:*",
      "Resource":"arn:aws:sdb:ap-northeast-1:{account_id}:domain/*"
      }
   ]
}
```

> 참고 : 맨 뒤 `domain/*` 형태가 되어야 list-domains 명령어가 작동됩니다. 고객, 사용자 제한을 할 때만 정확하게 도메인 이름을 작성해줍니다.

## 테스트
```bash
$ aws sdb create-domain --domain-name lazypic_test --region ap-northeast-1
```

~/.aws/credentials 프로파일명을 따로 선언했다면 아래 옵션을 추가합니다.
```
$ aws sdb create-domain --domain-name lazypic_test --region ap-northeast-1 --profile lazypic
```

## 도메인생성
```bash
$ aws sdb create-domain --region ap-northeast-1 --domain-name lazypic_client
```

## 도메인 리스트확인
도메인 리스트를 확인하는 방법은 아래와 같습니다.

```bash
aws sdb list-domains --region ap-northeast-1
```

## 어트리뷰트 설정

전화번호를 추가해보자. 이미 값이 존재한다면 바꾼다.

```bash
$ aws sdb put-attributes --region ap-northeast-1 --domain-name lazypic_client --item-name 75mm-stuio  --attributes Name=Phone,Value=+821053162746,Replace=true
```

데이터 추가

```bash
$ aws sdb put-attributes --region ap-northeast-1 --domain-name lazypic_client --item-name 75mm-stuio  --attributes "Name=Address,Value='502,6 Nonhyeon-ro 164-gil, Gangnam-gu, Seoul, Republic of Korea',Replace=true"
```

데이터 변경

```bash
$ aws sdb put-attributes --region ap-northeast-1 --domain-name lazypic_client --item-name 75mm-stuio  --attributes "Name=Address,Value='replace',Replace=true"
```

## 아이템 삭제

```bash
$ aws sdb delete-attributes --region ap-northeast-1 --domain-name lazypic_client --item-name 75mm-studio
```

## 도메인 메타데이터 확인

```bash
$ aws sdb domain-metadata --region ap-northeast-1 --domain-name lazypic_client
```

## 도메인 삭제

```bash
$ aws sdb delete-domain --region ap-northeast-1 --domain-name lazypic_client
```

## 쿼리
cashflow 에 들어간 데이터를 가지고 오기

```bash
$ aws sdb select --region ap-northeast-1 --select-expression 'select * from `cashflow`'
```

100개만 추리기
```
select * from `cashflow` limit 100
```

name attribute의 값이 "김한웅"으로 설정되어있는 데이터 쿼리하기
```
select * from `cashflow` where name="김한웅"
```

cost Attribute의 값이 100000 보다 큰 값만 뽑기. 숫자의 경우 자릿수가 맞아야 한다.
```
select * from `cashflow` where cost > '0000100000'
```

tags Attribute값에 `donation` 이라는 문자가 있는 데이터만 검색
```
select * from `cashflow` where tags like '%donation%'
select * from `cashflow` where tags like '%셋팅%'
```

정렬하기(방법 찾아보기)

일반정렬(ascending)
```
select * from `cashflow` where tags like '%donation%' intersection cost is not null order by cost asc
```

반대정렬
```
select * from `cashflow` where tags like '%donation%' intersection cost is not null order by cost desc
```

itemName에 0000001* 형태의 아이템 추출
```
select * from `cashflow` where itemName() like '0000001%' order by itemName()
```



- 쿼리예제1 : https://docs.aws.amazon.com/ko_kr/AmazonSimpleDB/latest/DeveloperGuide/SimpleQueriesSelect.html
- 쿼리예제2 : https://docs.aws.amazon.com/ko_kr/AmazonSimpleDB/latest/DeveloperGuide/SDB_API_Select.html

## SDK
- Go : https://docs.aws.amazon.com/sdk-for-go/api/service/simpledb/

## 테스트 프로그램
- 보안 정책 시뮬레이션 : https://policysim.aws.amazon.com/home/index.jsp
- sdbNavigator Chrome Extension : https://chrome.google.com/webstore/detail/sdbnavigator/ddhigekdfabonefhiildaiccafacphgg
- DB제약사항 : https://docs.aws.amazon.com/ko_kr/AmazonSimpleDB/latest/DeveloperGuide/SDBLimits.html