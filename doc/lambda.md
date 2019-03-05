# Lambda


## Node.js 버전
node.js 8.10, 6.10을 지원합니다.
https://nodejs.org/dist/v0.8.10/


웹에서 인라인 편집기를 사용할 수 있기 때문에 굉장히 빠르게 app을 설계할 수 있습니다.

## Python 예제
기본적으로 아래 코드를 작성하고 event와 context의 구조를 확인할 수 있습니다.

```python
def handler_name(event, context): 
    print(event)
    print(context)
    return event
```

## Reference
- https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/python-programming-model-handler-types.html
- https://m.youtube.com/watch?v=g7AHiymJ7I4