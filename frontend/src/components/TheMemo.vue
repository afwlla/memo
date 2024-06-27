<template>
  <div class="memo">
    <div class="act">
      <button class="btn btn-primary" @click="add()">추가</button>
    </div>

    <ul>
      <li v-for="d in data" :key="d.id" @click="edit(d.id)">{{ d.content }}</li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const data = ref([])
const getMemos = async () =>
  await axios.get('/api/memos').then((res) => {
    data.value = res.data
  })
getMemos()

const add = async () => {
  const content = prompt('추가할메모입력')
  await axios.post('/api/memos', { content }).then(() => {
    getMemos()
  })
}
const edit = async (id) => {
  const content = prompt('변경할메모입력')
  data.value[id] = content
  await axios.put('/api/memos/' + id, { content }).then(() => {
    getMemos()
  })
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
