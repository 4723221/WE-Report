# 第12回 Webエンジニアリング演習 レポート
## 学籍番号（名前は書かなくてよい）
4723221
## 本日の感想
AddTodo.vue側のtodos.valueの部分にエラーのような表記が出てしまい苦戦しました。表記が出ても問題なく動いたのでエラーはひとまず無視して最初から動作確認しに行くべきだったなと思いました。
## 実装したコード
AddTodo.vue
```
<script setup lang=ts>
import { ref } from 'vue'; 
const todos = defineModel("todos")
// New todo input state
const newTitle = ref('');
// compute next id from existing todos 
const nextId = ref(Math.max(0, ...todos.value.map((t) => t.id)) + 1); 

function addTodo(){
  const title = newTitle.value;
  todos.value.push({ id: nextId.value++, title, completed: false }); 
  newTitle.value = ''; 
}
</script>
<template>
      <section>
      <h2>New Todo</h2>
      <div style="display: flex; align-items: center; gap: 0.5rem; margin: 0.25rem 0;">
        <input
          v-model="newTitle"
          type="text"
          placeholder="New todo title"
          aria-label="New todo title"
        />
        <button v-on:click="addTodo" :disabled="!newTitle.trim()">Add</button>
      </div>
    </section>
</template>
```
App.vue
```
<template>
  <div id="app">
    <section class="todo-app">
      <h2>
        Todos
        <span style="margin-left: 0.5rem; font-size: 0.9em;">
    ({{ unfinishedCount }})
  </span>
      </h2>
      <ul>
        <li
          v-for="todo in todos"
          :key="todo.id"
          style="display:flex; align-items:center; gap:0.5rem; margin:0.25rem 0;"
        >
          <input type="checkbox" v-model="todo.completed" />
          <span :style="{ textDecoration: todo.completed ? 'line-through' : 'none' }">
            {{ todo.title }}
          </span>
       </li>
      </ul>
    </section>
    <section>
      <AddTodo v-model:todos="todos" />
    </section>
  </div>
</template>
```
