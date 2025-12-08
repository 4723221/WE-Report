# 第10回 Webエンジニアリング演習 レポート
## 学籍番号（名前は書かなくてよい）
4723221
## 実装したコード
```
<script setup lang="ts">
  import { ref } from 'vue';
  const name = ref('John Doe')
  setInterval(() => {
    if(name.value == '自分の名前') {
      name.value = 'John Doe'
    }else{
      name.value = '自分の名前'
    }
  }, 2000)
</script>

<template>
  <div>
    <p>Hello, {{ name }}!</p>
  </div>
</template>
```