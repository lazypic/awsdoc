# cloudfront
S3를 이용해서 https 서비스를 할 수 있는 서비스입니다.

## 클라우드 프론트 설정
- Price Class : Use U.S, Canada, Europe, Aisa and Africa
- Alternate Domain Names(CNAMES) : lazypic.org
- [SSL Certificate](acm.md) 에서 Custom SSL Certificate를 선택하고 생성한 인증서를 물려줍니다.
- Default Root Ojbect : index.html

#### Behavior
- Origin or Origin Group : S3-lazypic.org
- Protocal Policy : Redirect HTTP to HTTPS

#### 캐쉬
- 86400 : 24시간
- 31536000 : 1년 

#### Custom Error Response Setting
- HTTP Error Code : 404:Not Found
- Error Caching Minimum TTL 300
- CFustomize Error Response : Yes
- Response Page Path : /error.html
- HTTP Response Code : 200:OK


## Route53 설정

A, AAAA 값을 추가합니다.

```
lazypic.org
Alias Target : d2b049f4e53vuh.cloudfront.net.
```

## www.lazypic.org
- www.lazypic.org 버킷을 만든다.
- https://lazypic.org로 redirect 한다.

## Reference
- https://docs.aws.amazon.com/ko_kr/AmazonCloudFront/latest/DeveloperGuide/Expiration.html
