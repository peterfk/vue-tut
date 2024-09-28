<script setup>
import { ref, reactive, computed } from 'vue'

console.log("test!")

const count = ref(0)

const state = reactive({ count: 0 })
console.log(state)

console.log(count) // { value: 0 }
console.log(count.value) // 0

count.value++
console.log(count.value) // 1

function increment() {
  count.value++
}

const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})

// a computed ref
const publishedBooksMessage = computed(() => {
  return author.books.length > 0 ? 'Yes' : 'No'
})

const isActive = ref(false)
const hasError = ref(true)

const activeClass = ref('active')
const errorClass = ref('text-danger')

var awesome = ref(true)

const parentMessage = ref('Parent')
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])

items.value.forEach((item, index) => {
  // has access to outer scope `parentMessage`
  // but `item` and `index` are only available in here
  console.log(parentMessage.value, item.message, index)
})

const myObject = reactive({
  title: 'How to do lists in Vue',
  author: 'Jane Doe',
  publishedAt: '2016-04-10'
})

</script>

<template>
  <button @click="increment">
    {{ count }}
  </button>
  <br>
  <p>Has published books:</p>
  <span>{{ publishedBooksMessage }}</span>

  <div class="static" :class="{ active: isActive, 'text-danger': hasError }"></div>

  <div :class="[activeClass, errorClass]"></div>

  <div :class="[{ [activeClass]: isActive }, errorClass]"></div>

  <h1 v-if="true">Vue is awesome!</h1>


  <button @click="awesome = !awesome">Toggle</button>

  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>

  <template v-if="true">
    <h1>Title</h1>
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
  </template>

  <li v-for="item in items">
    {{ item.message }}
  </li>

  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>

  <ul>
    <li v-for="value in myObject">
      {{ value }}
    </li>
  </ul>

  <li v-for="(value, key, index) in myObject">
    {{ index }}. {{ key }}: {{ value }}
  </li>

</template>

<style scoped>
/* header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
} */

/* @media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
} */
</style>
