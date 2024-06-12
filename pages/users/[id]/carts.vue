<template>
    <div>
        <p>{{ data }}</p>
    </div>
</template>

<script setup>
    const { id } = useRoute().params
    const { data } = await useFetch(`https://dummyjson.com/carts/user/${id}`)
</script>
