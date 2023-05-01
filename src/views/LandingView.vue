<template>
    <div class="pt-16">
        <h1 class="text-3xl font-semibold mb-4">U-Ride</h1>
        <div class="overflow-hidden shadow sm:rounded-md max-w-sm mx-auto text-left">
            <div class="bg-white px-4 py-5 sm:p-6">
                <div class="flex justify-between">
                    <button type="submit" class="rounded-md border border-transparent py-2 px-4 text-sm bg-black text-white font-medium">Start Driving</button>
                    <button 
                    @click.prevent="handleFindARide"
                    type="submit" class="rounded-md border border-transparent py-2 px-4 text-sm bg-black text-white font-medium">Find A Ride</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { useRouter } from 'vue-router';


const router = useRouter()

const handleFindARide= () => {
    router.push({
        name: 'location'
    })
}
</script>

<style lang="scss" scoped>

</style> 