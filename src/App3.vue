<script setup>
import { ref, reactive, computed, onMounted, watch } from 'vue'

const count = ref(0)

const name = ref('Vue.js')

function greet(event) {
    alert(`Hello ${name.value}!`)
    // `event` is the native DOM event
    if (event) {
        alert(event.target.tagName)
    }
}

function say(message) {
    alert(message)
}

function warn(message, event) {
    // now we have access to the native event
    if (event) {
        event.preventDefault()
    }
    alert(message)
}

const message2 = ref('')

onMounted(() => {
    console.log(`the component is now mounted.`)
})

const question = ref('')
const answer = ref('Questions usually contain a question mark. ;-)')
const loading = ref(false)

// watch works directly on a ref
watch(question, async (newQuestion, oldQuestion) => {
    if (newQuestion.includes('?')) {
        loading.value = true
        answer.value = 'Thinking...'
        try {
            const res = await fetch('https://yesno.wtf/api')
            answer.value = (await res.json()).answer
        } catch (error) {
            answer.value = 'Error! Could not reach the API. ' + error
        } finally {
            loading.value = false
        }
    }
})

</script>

<template>

    <p>
        Ask a yes/no question:
        <input v-model="question" :disabled="loading" />
    </p>
    <p>{{ answer }}</p>

    <button @click="count++">Add 1</button>
    <p>Count is: {{ count }}</p>

    <!-- `greet` is the name of the method defined above -->
    <button @click="greet">Greet</button>

    <button @click="say('hello')">Say hello</button>
    <button @click="say('bye')">Say bye</button>
    <p></p>
    <!-- using $event special variable -->
    <button @click="warn('Form cannot be submitted yet.', $event)">
        Submit
    </button>

    <!-- using inline arrow function -->
    <button @click="(event) => warn('Form cannot be submitted yet.', event)">
        Submit
    </button>
    <p></p>
    <input v-model="text">

    <p>Message is: {{ message2 }}</p>
    <input v-model="message2" placeholder="edit me" />



</template>