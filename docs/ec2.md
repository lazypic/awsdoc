# EC2
AWS에서 컴퓨터를 예약후 사용하는 서비스 입니다.

인스턴스를 정지하면 인스턴스 자체는 과금되지 않습니다.
하지만 인스턴스가 사용하는 하드디스크 용량 비용은 과금이 발생합니다.
인스턴스를 삭제하면 과금이 발생되지 않습니다.

## 가격
지인들이 자신의 업무를 위해서 간혹 ec2셋팅을 물어보면서 가격을 같이 말하게 되는 경우가 많습니다.
가격은 아래 URI를 통해서 알 수 있습니다.

https://aws.amazon.com/ko/ec2/pricing/on-demand/

## 키페어 생성
인스턴스에 접속하기 위해서는 키페어를 생성해야합니다.
lazypic은 주로 렌더팜을 사용하기 때문에 렌더팜용 key-pair를 생성하는 경우가 많이 있습니다.

필요시 렌더팜 key-pari+{project_codename} 을 활용합니다.

생성하기 위해서 필요한 policy 정책은.. 리서치하기.

```
$ aws ec2 create-key-pair --key-name renderfarm --query 'KeyMaterial' --output text > renderfarm.pem --profile lazypic
$ chmod 400 renderfarm.pem
```

키페어 확인
```
$ aws ec2 describe-key-pairs --key-name renderfarm --profile lazypic
```

## 키페어 삭제

```
$ aws ec2 delete-key-pair --key-name MyKeyPair
```
네트워크 및 보안 > 키페어에서 수동 생성이 가능합니다.

## 인스턴스 정보 확인

## 인스턴스 생성

## 인스턴스 삭제

