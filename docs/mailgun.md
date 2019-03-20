# Mailgun

mailgun 셋팅방법을 다룹니다.
AWS 서비스가 아니지만 다루는 이유는 추후 Route53 서비스 설정이 포함되어 있기 때문입니다.

## 가입, 도메인등록
- https://www.mailgun.com 에 가입합니다.
- 구입한 도메인을 mailgun에 등록합니다.

## Route53 등록값
mailgun에서 DNS를 등록후 mailgun의 Add DNS Records For Sending 항목으로
Route53값을 추가적으로 셋팅 합니다.

#### TXT 셋팅1
- Name : lazypic.org
- Type : TXT
- Value : v=spf1 include:mailgun.org ~all

#### TXT 셋팅2
- Name : k1._domainkey.lazypic.org
- Type : TXT
- Value : k=rsa;~~

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
48시간 이후 State가 Unverified 에서 ""로 바뀌면 성공입니다.

## 사용자등록
