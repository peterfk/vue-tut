<script setup>
import { ref, reactive, computed } from 'vue'
import ButtonCounter from './ButtonCounter.vue'
import BlogPost from './BlogPost.vue';
import AlertBox from './AlertBox.vue'

const posts = ref([
    { id: 1, title: 'My journey with Vue' },
    { id: 2, title: 'Blogging with Vue' },
    { id: 3, title: 'Why Vue is so fun' }
])

const postFontSize = ref(1)

</script>

<template>
    <h1>Here is a child component!</h1>
    <ButtonCounter />

    <h1>Here are many child components!</h1>
    <ButtonCounter />
    <ButtonCounter />
    <ButtonCounter />

    <div :style="{ fontSize: postFontSize + 'em' }">
        <BlogPost v-for="post in posts" :key="post.id" :title="post.title" @enlarge-text="postFontSize += 0.1" />
    </div>

    <AlertBox>
        Something bad happened.
    </AlertBox>

</template>