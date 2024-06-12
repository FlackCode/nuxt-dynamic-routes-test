<template>
    <div class="bg-gray-100 flex justify-center gap-4 w-full">
        <div v-if="error" class="m-4 p-4 max-w-fit bg-white text-red-500">
            Error: {{ error }}
        </div>
        <div v-else-if="loading" class="m-4 p-4 max-w-fit bg-white">
            Loading...
        </div>
        <div v-else class="w-full flex justify-center gap-4 px-48 m-4">
            <div class="p-4 flex flex-col gap-4 bg-white w-1/3 rounded-md shadow-sm">
                <div class="flex flex-col py-2">
                    <img :src="user.image" class="w-4 h-4">
                    <h1 class="text-lg font-bold">{{ user.firstName }} {{ user.lastName }}</h1>
                    <p class="text-gray-400">{{ user.email }}</p>
                </div>
                <hr />
                <div class="flex flex-col gap-2 py-2">
                    <h1 class="text-lg font-bold">Links</h1>
                    <nuxt-link :to="{ name: 'users-id-posts', params: { id: user.id }}" 
                    class="py-2 px-16 border border-gray-300 rounded-md flex justify-center">Posts</nuxt-link>
                    <nuxt-link :to="{ name: 'users-id-todos', params: { id: user.id }}" class="py-2 px-16 border border-gray-300 rounded-md flex justify-center">Todos</nuxt-link>
                    <nuxt-link :to="{ name: 'users-id-carts', params: { id: user.id }}" class="py-2 px-16 border border-gray-300 rounded-md flex justify-center">Carts</nuxt-link>
                </div>
            </div>
            <div class="p-4 flex flex-col gap-4 bg-white w-2/3 rounded-md shadow-sm">
                <div>
                    <NuxtPage :user="user"/>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

const route = useRoute()
const user = ref(null)
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
    const { id } = route.params
    try {
        const response = await fetch(`https://dummyjson.com/users/${id}`)
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`)
        }
        user.value = await response.json()
    } catch (err) {
        error.value = err.message
    } finally {
        loading.value = false
    }
});
</script>
