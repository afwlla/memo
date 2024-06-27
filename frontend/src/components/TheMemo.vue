<template>
  <div class="memo">
    <div class="act">
      <button class="btn btn-primary" @click="add()">추가</button>
    </div>

    <ul>
      <li v-for="d in data" :key="d">{{ d }}</li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const data = ref(['내용1', '내용2', '내용3', '내용4', '내용5'])

const add = () => {
  data.value.push('추가메모')
}
</script>

<style lang="scss" scoped>
.memo {
  .act {
    padding: 10px 10px 5px 5px;
    text-align: right;
  }

  ul {
    list-style: none;
    padding: 15px;
    margin: 0;

    li {
      padding: 15px;
      margin: 10px 0;
      border: 1px solid #eee;
    }
  }
}
</style>
