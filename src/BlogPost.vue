<!-- BlogPost.vue -->
<script setup>

const props = defineProps(['title'])
defineEmits(['enlarge-text'])
console.log(props.title)
</script>

<template>
    <h4>{{ title }}</h4>
    <button @click="$emit('enlarge-text')">Enlarge text</button>
</template>