<template>
  <div class="memo">
    <div class="act">
      <button class="btn btn-primary" @click="add()">추가</button>
    </div>

    <ul>
      <li v-for="(d, idx) in data" :key="d" @click="edit(idx)">{{ d }}</li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

axios.get('/api/memos').then((res) => {
  data.value = res.data
})

const data = ref([''])

const add = () => {
  const content = prompt('추가할메모입력')
  axios.post('/api/memos', { content }).then((res) => {
    console.log(res)
  })
}
const edit = (idx) => {
  const content = prompt('변경할메모입력')
  data.value[idx] = content
  axios.put('/api/memos' + idx, { content })
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
