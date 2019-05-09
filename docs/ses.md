# SES
AWS SES 서비스는 버지니아 북부 리전에서만 사용이 가능합니다.
따로 ~/.aws/credentials 에 리전이 할당된 프로파일을 만들고 사용하면 편리합니다.

```
[lazypic_ses]
region=us-east-1
aws_access_key_id = XXXXXXXXXXX
aws_secret_access_key = XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```


## Send Email
아래 명령어를 통해서 이메일을 받을 사람, 템플릿을 지정하고 이메일을 전송할 수 있습니다.

```bash
$ aws ses send-email --from hello@openpipeline.io --destination file://destination.json --message file://message.json --profile lazypic_ses
```

destination.json
```json
{
  "ToAddresses":  ["khw7096@gmail.com"],
  "CcAddresses":  ["khw7096@gmail.com"],
  "BccAddresses": []
}
```

message.json
```json
{
   "Subject": {
       "Data": "Hello Lazypic OpenPipeline IO Service",
       "Charset": "UTF-8"
   },
   "Body": {
       "Text": {
           "Data": "This is the message body in text format.",
           "Charset": "UTF-8"
       },
       "Html": {
           "Data": "This message body contains HTML formatting. It can, for example, contain links like this one: <a class=\"ulink\" href=\"http://docs.aws.amazon.com/ses/latest/DeveloperGuide\" target=\"_blank\">Amazon SES Developer Guide</a>.",
           "Charset": "UTF-8"
       }
   }
}
```