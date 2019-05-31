# Mailgun

mailgun 셋팅방법을 다룹니다.
AWS 서비스가 아니지만 다루는 이유는 Route53 서비스와 함께 설정, 사용이 가능하기 때문입니다.
또한 AWS Workmail은 계정당 $4 이기 때문에 비용절감 차원도 있습니다.

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

## 주의사항1. mailgun DNS disabled
메일건으로 셋팅한 메일을 AWS SNS 서비스에 물리지 않습니다. 너무 많은 메일이 자동으로 전송되면 mailgun 측에서 고객의 스팸공격 방지를 위해서 DNS를 임시로 막습니다. 하지만 비즈니스를 진행하기 위해서 많은 메일을 처리해야합니다. 메일이 많이 오게되면 아래 메일을 받게되니 참고하세요.

메일원문
```
In order to complete this process please answer the questions below (in as much detail as possible) Please be sure to provide us with links to your webpage, privacy policy, terms of service and sign up page:

1. What types of emails will you be sending - transactional or marketing? Please tell us briefly about how your business uses email.

서비스 URL을 작성하기.


2. Where do you source your database/list of email addresses? Please provide any available links.

Email lists are managed through AWS SNS.

3. Are all of your email addresses double-opt in? (This means that the user has requested your emails through sign-up and then confirmed via email that they want to receive your communication).

Yes.

4. What is your expected monthly volume of messages?

May 2019 is in the development phase, so many tests have been conducted. We expect 1000 cases a month.

5. Have you read our Email Best Practices document?

 Yes.

6. Please provide a link to your Privacy Policy, Terms of Service, and Sign-up link (if applicable).

Send Term and Privacy policy(Korean)

7. Please provide a sample email you would typically send to your users.

생성되는 패턴메일을 보내기.
```