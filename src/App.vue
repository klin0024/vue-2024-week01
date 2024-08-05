<script setup>
import { ref } from 'vue'
const items = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20,
    isEdit: false
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '香濃奶茶搭配QQ珍珠',
    price: 45,
    stock: 18,
    isEdit: false
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34,
    isEdit: false
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10,
    isEdit: false
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25,
    isEdit: false
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20,
    isEdit: false
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18,
    isEdit: false
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20,
    isEdit: false
  }
])

const changeStockNum = (item, action) => {
  if (action === 1) {
    item.stock++
  } else {
    if (item.stock > 0) {
      item.stock--
    }
  }
}

const temp = ref('')

const change = {
  on: (item) => {
    items.value.forEach((i) => (i.isEdit = false))
    item.isEdit = true
    temp.value = item.name
  },
  save: (item) => {
    item.name = temp.value
    item.isEdit = false
  },
  cancle: (item) => {
    item.isEdit = false
  },
  delete: (index) => {
    items.value.splice(index, 1)
  }
}
</script>

<template>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
      </tr>
    </thead>
    <tbody v-for="(item, index) in items" :key="item.id">
      <td @dblclick="change.on(item)">
        <dev v-if="!item.isEdit">
          {{ item.name }}
          <button type="buttom" @click="change.delete(index)">刪除</button>
        </dev>
        <dev v-else>
          <input type="text" v-model="temp" />
          <button type="buttom" @click="change.save(item)">save</button>
          <button type="buttom" @click="change.cancle(item)">cancle</button>
        </dev>
      </td>
      <td>{{ item.description }}</td>
      <td>
        {{ item.price }}
      </td>
      <td>
        <button type="button" @click="changeStockNum(item, 0)">-</button>
        {{ item.stock }}
        <button type="button" @click="changeStockNum(item, 1)">+</button>
      </td>
    </tbody>
  </table>
</template>

<style scoped></style>
