<template>
    <div class="pt-16">

        <div class="overflow-hidden shadow sm:rounded-md max-w-sm mx-auto text-left">
            <div class="bg-white px-4 py-5 sm:p-6">
                <div class="flex justify-center">
                    <!-- form for login new user  -->
                    
                    <form v-if="!waitingOnVerification" action="#" @submit.prevent="handleLogin">
                        <h1 class="text-3xl font-semibold mb-4">Enter Your Phone number.</h1>
                        <div class="my-4">
                            <input v-maska data-maska="(+###) #######" v-model="credentials.phone" type="text"  placeholder="(+123) 4567890">
                        </div>
                        <div class="flex justify-center">
                            <button type="submit" @submit.prevent="handleLogin" class="rounded-md border border-transparent py-2 px-4 text-sm bg-black text-white font-medium">Submit</button>
                        </div>
                    </form>

                    <!-- form for verification -->
                    <form v-else action="#" @submit.prevent="handleVerification">
                        <h1 class="text-3xl font-semibold mb-4">Enter Your Login Code.</h1>
                        <div class="my-4">
                            <input v-maska data-maska="######" v-model="credentials.login_code" type="text"  placeholder="123456">
                        </div>
                        <div class="flex justify-center">
                            <button type="submit" @submit.prevent="handleVerification" class="rounded-md border border-transparent py-2 px-4 text-sm bg-black text-white font-medium">Verify</button>
                        </div>
                    </form> 
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { vMaska } from "maska"
import { onMounted, reactive, ref, computed } from "vue"
import axios from "axios"
import { useRouter } from "vue-router"

    const router = useRouter() 
  
    const credentials = reactive({
        phone: null,
        login_code: null
    });

    const waitingOnVerification = ref(false);

    onMounted(() => {
        if(localStorage.getItem('token')){
            router.push({
                name: 'landing'
            })
        }
    })

    const formattedCredentials = () => {
        return {
            phone : credentials.phone.replaceAll(' ', '').replace('(', '').replace(')', '').replace('+', ''),
            login_code : credentials.login_code
        }
    }

    const handleLogin = () => {
        axios.post('http://localhost:8000/api/login', formattedCredentials() )

        .then((response) => {
            console.warn(response.data);
            waitingOnVerification.value = true;

        })
             
        .catch((error) => {
            console.error(error);
            alert(error.response.data.message);
        })
    }

    const handleVerification = () => {
        axios.post('http://localhost:8000/api/login/verify', formattedCredentials() )

        .then((response) => {
            console.log(response.data) //auth token
            localStorage.setItem('token', response.data)
            router.push({
                name: 'landing'
            })
        })

        .catch((error) => {
            console.error(error);
            alert(error.response.data.message);
        })
    }
</script>

<style lang="scss" scoped>

</style>