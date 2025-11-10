# 第7回 Webエンジニアリング演習 レポート
## 学籍番号（名前は書かなくてよい）
4723221
## PUTリクエスト検証用のモデルとAPI部分のコード
```
@app.put("/todos", response_model=TodoItem) 
def update_todo(todo_id: int, req: TodoItemCreateSchema): 
    for i, todo in enumerate(todos): 
        if todo.id == todo_id: 
            todos[i] = TodoItem( 
                id=todo_id, 
                title=req.title if req.title is not None else todo.title, 
                description=req.description if req.description is not None else todo.description, 
                completed=req.completed if req.completed is not None else todo.completed 
            )
            return todos[i]
    raise HTTPException(status_code=404, detail=f"ID {todo_id} のTODOが見つかりません")
```

## 動作確認結果

- Swagger UIでのPUTエンドポイントテスト結果
- 正常系：存在するタスクの変更
```
Request:
curl -X 'PUT' \
'http://localhost:8000/todos?todo_id=1' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": 0,
  "title": "あ行",
  "description": "あいうえお",
  "completed": true
}'

Respons:
{
  "id": 1,
  "title": "あ行",
  "description": "あいうえお",
  "completed": true
}
```
- 異常系：存在しないタスクIDでのエラー確認
```
Request:
curl -X 'PUT' \
  'http://localhost:8000/todos?todo_id=8' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": 0,
  "title": "あ行",
  "description": "あいうえお",
  "completed": true
}'

Respons:
{
  "detail": "ID 8 のTODOが見つかりません"
}
```