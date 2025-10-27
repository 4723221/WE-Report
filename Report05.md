#　第５回 Webエンジニアリング演習　レポート
## 学籍番号
 4723221
## 各エンドポイントのSwagger UIでのテスト結果
### GET /
```
Request:
curl -X 'GET' \
  'http://127.0.0.1:8000/' \
  -H 'accept: application/json'
```
```
Response:
Response body
{
  "Hello": "World"
}
```
### GET /health
```
Request:
curl -X 'GET' \
  'http://127.0.0.1:8000/health' \
  -H 'accept: application/json'
```
```
Response:
Response body
{
  "status": "healthy"
}
```
### GET /items/{item_id}
```
Request:
curl -X 'GET' \
  'http://127.0.0.1:8000/items/1?q=q' \
  -H 'accept: application/json'
```
```
Response:
{
  "item_id": 1,
  "q": "q"
}
```

### GET /items/{item_id}
```
Request:
curl -X 'GET' \
  'http://127.0.0.1:8000/items/-1' \
  -H 'accept: application/json'
```
```
Response:
{
  "detail": "Item ID must be positive"
}
```