```
Request:
curl -X 'GET' \
  'http://localhost:8000/todos' \
  -H 'accept: application/json'

Response:
[
  {
    "id": 1,
    "title": "牛乳とパンを買う",
    "description": "牛乳は低温殺菌じゃないとだめ",
    "completed": false
  },
  {
    "id": 2,
    "title": "Pythonの勉強",
    "description": "30分勉強する",
    "completed": true
  },
  {
    "id": 3,
    "title": "30分のジョギング",
    "description": "",
    "completed": false
  },
  {
    "id": 4,
    "title": "技術書を読む",
    "description": "",
    "completed": false
  },
  {
    "id": 5,
    "title": "夕食の準備",
    "description": "カレーを作る",
    "completed": true
  }
]
```
```
Request:
curl -X 'GET' \
  'http://localhost:8000/todos?query=%E7%89%9B%E4%B9%B3' \
  -H 'accept: application/json'

Response:
[
  {
    "id": 1,
    "title": "牛乳とパンを買う",
    "description": "牛乳は低温殺菌じゃないとだめ",
    "completed": false
  }
]
```
```
Request:
curl -X 'GET' \
  'http://localhost:8000/todos?query=%E3%81%82%E3%81%82' \
  -H 'accept: application/json'

Response:
[]
```