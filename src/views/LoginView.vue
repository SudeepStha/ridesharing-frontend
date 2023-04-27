<template>
    <div class="pt-16">
        <h1>Enter Your Phone number.</h1>
        <form action="#" @submit.prevent="handleLogin">
            <div class="my-4">
                <input v-maska data-maska="(+###) ##########" v-model="data.phone" type="text"  placeholder="(+977)  1234567890">
            </div>
            <div>
                <button type="submit" @submit.prevent="handleLogin" class="bg-black text-white btn">Submit</button>
            </div>
        </form>
    </div>
</template>

<script setup>
    import { vMaska } from "maska";
    import { reactive } from "vue";  
  
    const data = reactive({
        phone: null

    });

    const handleLogin = () => {
        console.log(data.phone);
    }
</script>

<style lang="scss" scoped>

</style>