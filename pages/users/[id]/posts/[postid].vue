<template>
    <div>
        <p>{{ data }}</p>
    </div>
</template>

<script setup>
    const { postid } = useRoute().params
    const { data } = await useFetch(`https://dummyjson.com/posts/${postid}`)
</script>
