<template>
  <header class="container py-8">
    <h1>不知道叫什麼名字</h1>
    <p class="text-center mt-2 text-lg">{{ date }}</p>
  </header>

  <main>
    <!-- 按鈕區塊 -->
    <div class="container flex justify-center items-center space-x-2">
      <button
        type="button"
        class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:outline-none shadow-lg shadow-blue-500/50 font-medium rounded-lg text-sm px-5 py-2.5 text-center"
      >
        查詢價格
      </button>

      <button
        type="button"
        class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-gradient-to-br focus:outline-none shadow-lg shadow-red-500/50 font-medium rounded-lg text-sm px-5 py-2.5 text-center"
      >
        更改價格
      </button>
    </div>

    <!-- 清單區塊 -->
    <div class="container mt-4">
      <ul
        class="w-full h-[430px] bg-gray-50 rounded-2xl drop-shadow-xl py-3 px-5 overflow-y-scroll"
      >
        <li
          v-for="item in saleItems"
          :key="item.id"
          class="text-gray-700 mb-5 border-b-2 border-gray-300 pb-2 flex justify-between items-center"
        >
          <!-- 項目名稱 -->
          <div class="flex space-x-5 items-center">
            <h3 class="p-1.5 font-medium bg-slate-200 rounded-sm text-xl">
              {{ item.name }}
            </h3>
            <p class="text-lg flex">
              NT$：
              <template v-if="item.editing">
                <input
                  id="priceInput"
                  ref="priceInput"
                  v-model="item.price"
                  type="number"
                  class="font-bold inline-block w-10"
                  @blur="onInputBlur(item)"
                />
              </template>
              <template v-else>
                <p>
                  <span class="font-bold">{{ item.price }} </span>
                  / Kg
                </p>
              </template>
            </p>
          </div>

          <!-- 更改按鈕 -->
          <button
            type="button"
            @click="editHandler(item)"
            class="bg-slate-400 py-2 px-3 rounded-lg text-white"
          >
            更改
          </button>
        </li>
      </ul>
    </div>
  </main>
</template>

<script setup>
import { ref, reactive, onMounted, computed } from 'vue'
import dayjs from 'dayjs'

const date = ref('')

// 產生20個原物料的假資料
const saleItems = reactive([
  {
    id: 1,
    name: '鐵',
    price: 10,
    editing: false,
  },
  {
    id: 2,
    name: '鋁',
    price: 20,
    editing: false,
  },
  {
    id: 3,
    name: '銅',
    price: 30,
    editing: false,
  },
  {
    id: 4,
    name: '鋅',
    price: 40,
    editing: false,
  },
  {
    id: 5,
    name: '鎂',
    price: 50,
    editing: false,
  },
  {
    id: 6,
    name: '鉛',
    price: 60,
    editing: false,
  },
  {
    id: 7,
    name: '錫',
    price: 70,
    editing: false,
  },
  {
    id: 8,
    name: '鎳',
    price: 80,
    editing: false,
  },
  {
    id: 9,
    name: '鈷',
    price: 90,
    editing: false,
  },
  {
    id: 10,
    name: '鈦',
    price: 100,
    editing: false,
  },
  {
    id: 11,
    name: '鉭',
    price: 110,
    editing: false,
  },
  {
    id: 12,
    name: '鈮',
    price: 120,
    editing: false,
  },
  {
    id: 13,
    name: '鉑',
    price: 130,
    editing: false,
  },
  {
    id: 14,
    name: '銀',
    price: 140,
    editing: false,
  },
  {
    id: 15,
    name: '金',
    price: 150,
    editing: false,
  },
  {
    id: 16,
    name: '鈷',
    price: 160,
    editing: false,
  },
  {
    id: 17,
    name: '鈷',
    price: 170,
    editing: false,
  },
  {
    id: 18,
    name: '鈷',
    price: 180,
    editing: false,
  },
  {
    id: 19,
    name: '鈷',
    price: 190,
    editing: false,
  },
  {
    id: 20,
    name: '鈷',
    price: 200,
    editing: false,
  },
])

// 點擊後將 editHandler 的值設為 false
const editHandler = saleItems => {
  console.log(saleItems)
  saleItems.editing = !saleItems.editing

  if (saleItems.value.editing) {
    // 使用onMounted来等待DOM更新完成
    onMounted(() => {
      priceInputRef.value.focus()
    })
  }
}

onMounted(() => {
  const updateDate = () => {
    date.value = dayjs(new Date()).format('YYYY-MM-DD HH:mm:ss')
  }

  // 每秒更新一次 date 的值
  const intervalId = setInterval(updateDate, 1000)

  // 元件卸載時清除 intervalId
  onUnmounted(() => {
    clearInterval(intervalId)
  })

  // 初始化 date 的值
  updateDate()
})
</script>
