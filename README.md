# devise token authで作る 認証APIサンプル

## ユーザー登録
- コマンド
```
curl -X POST\
 -H 'Content-Type:application/json'\
 -D -\
 http://localhost:3000/auth\
 -d '{"name":"yuya","email":"fancl01@gmail.com","password":"password","team":"ウェブ帳"}'
```
- レスポンスサンプル
```
HTTP/1.1 200 OK
access-token: Oma5lChFVyIVN-wOxKTGVQ
token-type: Bearer
client: Auy5WLeV6pjUwda3YTeFFw
expiry: 1539066753
uid: fancl01@gmail.com
Content-Type: application/json; charset=utf-8
ETag: W/"7afc0c35aca1aae0c726279717314b5a"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: 5f8489af-7b76-48cb-bcfc-9da0f2d4bf59
X-Runtime: 0.251209
Transfer-Encoding: chunked

{"status":"success","data":{"id":3,"provider":"email","uid":"fancl01@gmail.com","name":"yuya","nickname":null,"image":null,"email":"fancl01@gmail.com","team":"ウェブ帳","created_at":"2018-09-09T06:32:33.029Z","updated_at":"2018-09-09T06:32:33.105Z"}}
```

## ユーザーログイン(token生成)
- コマンド
```
curl -X POST\
 -H 'Content-Type:application/json'\
 -D -\
 http://localhost:3000/auth/sign_in\
 -d '{"email":"fancl01@gmail.com","password":"password"}'
```
- レスポンスサンプル
```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
access-token: ZIhUxqRxswYeesgSi2Y0hA
token-type: Bearer
client: pAwC-6pVS_a9392bznr4qw
expiry: 1539066840
uid: fancl01@gmail.com
ETag: W/"15d7a47625ee8f2fdbd7161ed6d2948b"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: 36c02d7a-33ac-4c56-8ccd-181e9acfea73
X-Runtime: 0.242186
Transfer-Encoding: chunked

{"data":{"id":3,"email":"fancl01@gmail.com","provider":"email","uid":"fancl01@gmail.com","name":"yuya","nickname":null,"image":null,"team":"ウェブ帳"}}
```

## ユーザー情報変更
- コマンド
```
curl -X PUT\
 -H 'Content-Type:application/json' \
 -H 'uid:fancl01@gmail.com' \
 -H 'client:pAwC-6pVS_a9392bznr4qw' \
 -H 'access-token:ZIhUxqRxswYeesgSi2Y0hA' \
 -D - http://localhost:3000/auth/\
 -d '{"team":"webcyou"}'
```
- レスポンスサンプル
```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
access-token: ZIhUxqRxswYeesgSi2Y0hA
token-type: Bearer
client: pAwC-6pVS_a9392bznr4qw
expiry: 1539066840
uid: fancl01@gmail.com
ETag: W/"a7c16055ebc578acda64d3ab3d37d771"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: 9ae98917-4d6e-4091-b211-6f7995b10452
X-Runtime: 0.094561
Transfer-Encoding: chunked

{"status":"success","data":{"id":3,"team":"webcyou","email":"fancl01@gmail.com","provider":"email","uid":"fancl01@gmail.com","name":"yuya","nickname":null,"image":null,"created_at":"2018-09-09T06:32:33.029Z","updated_at":"2018-09-09T06:36:16.105Z"}}
```

## ユーザー削除
- コマンド
```
curl -X DELETE\
 -H 'uid:fancl01@gmail.com'\
 -H 'client:pAwC-6pVS_a9392bznr4qw'\
 -H 'access-token:ZIhUxqRxswYeesgSi2Y0hA'\
 -D -\
 http://localhost:3000/auth/
```
- レスポンスサンプル
```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
ETag: W/"075a89f66485f801bc1bdeae1f17d2fe"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: 8e867f0d-6047-40c2-b804-13d5870fcbba
X-Runtime: 0.008032
Transfer-Encoding: chunked

{"status":"success","message":"Account with UID 'fancl01@gmail.com' has been destroyed."}
```
