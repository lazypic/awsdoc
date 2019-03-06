# API Gatway

## API 작성
> 참고 : Lambda에서 바로 함수를 생성하면 ANY 모드로 모든 매소드가 생성된다.

```
- restapi(Deploy Name)
    - v1(Resource Name)
        - GET(method) : 데이터를 가지고 올 때
        - POST(method) : 폼사용. 헤더x, 데이터 전송
        - DELETE(method) : 웹서버 파일을 삭제할 때
        - HEAD(method) : 헤더정보만 가지고 올 때
        - OPTIONS(method) : 지원 메소드를 확인할 때
        - PATCH(method) : 데이터를 Update시 많이 사용
        - PUT(method) : 데이터 Replace에 많이 사용
```
#### Reference
- Put & Patch : https://stackoverflow.com/questions/24241893/rest-api-patch-or-put
- [코그니토](cognito.md) + APIGatway : https://www.youtube.com/watch?v=5dbgJdcMfiU

## lambda에서 application/html 리턴하기
- Reference : https://kennbrodhagen.net/2016/01/31/how-to-return-html-from-aws-api-gateway-lambda/

## 도메인 연결 / Custom Domain Names
Route53에 레코드를 생성하고 estimate.lazypic.org 형태로 도메인을 입력한다. 40분정도 소요됨. 많이 요청하기 때문에 여러번 해볼 필요가 있다.
