# Mailgun

mailgun 셋팅방법을 다룹니다.
AWS 서비스가 아니지만 다루는 이유는 추후 Route53 서비스 설정이 포함되어 있기 때문입니다.

## 가입, 도메인등록
- https://www.mailgun.com 에 가입합니다.
- 구입한 도메인을 mailgun에 등록합니다.

## Route53 등록값
mailgun에서 DNS를 등록후 mailgun의 Add DNS Records For Sending 항목으로
Route53값을 추가적으로 셋팅 합니다.

#### TXT등록
- Name : 
- Type : TXT
```
TXT lazypic.org v=spf1 include:mailgun.org ~all
TXT k1._domainkey.lazypic.org k=rsa;~~
```

#### MX Setting
- Type : MX - Mail exchange
- Value
```
10 mxa.mailgun.org
10 mxb.mailgun.org
```

## CNAME Setting
- Name : email.lazypic.org
- Type : CNAME
- Value : mailgun.org

## Wait For Your Domain To Verify
mailgun에서 Get Started Sending 버튼을 클릭합니다.
48시간 이후 State가 "Unverified" 에서 "Active" 로 바뀌면 성공입니다.

## 사용자등록 / stmp credentials 메뉴로 이동합니다.
- 메일등록을 합니다. : https://app.mailgun.com/app/domains/lazypic.org/credentials

## Routes 셋팅 / 메뉴에서 Route
woong@lazypic.org 메일을 khw7096@gmail.com 으로 포워딩하는 설정입니다.

- Expression Type : Match Recipient
- Recipent : woong@lazypic.org
- Actions(Forward Check) : khw7096@gmail.com(`,`문자를 이용해서 복수입력이 가능합니다.)
- Priority : 0
- Description : 김한웅

## 사용자 등록절차
- https://lazypic.github.io/메일포워딩-셋팅/ 을 참고합니다.
