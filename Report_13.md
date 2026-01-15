# 第13回 Webエンジニアリング演習 レポート
## 学籍番号
4723221
## 実装したコード

```
<script setup lang=ts>
import { computed, ref } from 'vue';
import AddTodo from './components/AddTodo.vue';
import { useTodoStore } from './stores/todoStore';
const name = ref('Vue 3 with TypeScript');

const todoStore = useTodoStore();

</script>

<template>
  <div id="app">
    <section class="todo-app">
      <h2>Todos</h2>
      <ul>
        <li
          v-for="todo in todoStore.todos"
          :key="todo.id"
          style="display:flex; align-items:center; gap:0.5rem; margin:0.25rem 0;"
        >
          <input type="checkbox" v-model="todo.completed" />
          <span :style="{ textDecoration: todo.completed ? 'line-through' : 'none' }">
            {{ todo.title }}
          </span>
          <button @click="todoStore.removeTodo(todo.id)">
            削除
          </button>
       </li>
      </ul>
    </section>
    <section>
      <AddTodo />
    </section>
  </div>
</template>
```
```
// import './assets/main.css'

import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'

const app =  createApp(App)
const pinia = createPinia()

app.use(pinia)
app.mount('#app')
```
```
<script setup lang=ts>
import { ref } from 'vue';
import { useTodoStore } from '@/stores/todoStore';

const todoStore = useTodoStore();

const newTitle = ref<string>('');

function addTodo(){
  todoStore.addTodo(newTitle.value);
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
        <button v-on:click="todoStore.addTodo(newTitle)" :disabled="!newTitle.trim()">Add</button>
      </div>
    </section>
</template>
```
```
import { defineStore } from 'pinia'
import { ref } from 'vue'

interface Todo {
  id: number
  title: string
  completed: boolean
}

export const useTodoStore = defineStore('todo', () => {
    let serialID = 4

    const todos = ref<Todo[]>([
        { id: 1, title: 'Buy groceries', completed: false },
        { id: 2, title: 'Write report', completed: true },
        { id: 3, title: 'Call Alice', completed: false },
    ])

    const addTodo = (title: string) => {
        const newTodo: Todo = {
            id: serialID++,
            title: title,
            completed: false,
        }
        todos.value.push(newTodo)
    }
    const removeTodo = (id: number) => {
        todos.value = todos.value.filter(todo => todo.id !== id)
    }
    return { todos, addTodo, removeTodo }
})
```