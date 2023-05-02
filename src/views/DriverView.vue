<template>
    <div class="pt-16">
        <form action="#" @submit.prevent="handleSaveDriver">
            <div class="overflow-hidden shadow sm:rounded-md max-w-sm mx-auto text-left">
                <div class="bg-white px-4 py-5 sm:p-6">
                    <div class="">                    
                        <h1 class="text-3xl font-semibold mb-4 flex justify-center">Driver and Car Details</h1>
                        <div>
                            <input type="text" name="name" id="name" v-model="driverDetails.name" placeholder="Full Name"
                            class="mt-1 block w-full px-3 py-2 rounded-md border border-gray-300 shadow-sm focus:border-black focus:outline-none"> 
                        </div>
                        <div>
                            <input type="number" name="year" id="year" 
                            v-model="driverDetails.year" placeholder="Car Year"
                            class="mt-1 block w-full px-3 py-2 rounded-md border border-gray-300 shadow-sm focus:border-black focus:outline-none"> 
                        </div>
                        <div>
                            <input type="text" name="make" id="make"
                            v-model="driverDetails.make"
                            placeholder="Make"
                            class="mt-1 block w-full px-3 py-2 rounded-md border border-gray-300 shadow-sm focus:border-black focus:outline-none"> 
                        </div>
                        <div>
                            <input type="text" name="model" id="model" 
                            v-model="driverDetails.model" placeholder="Model"
                            class="mt-1 block w-full px-3 py-2 rounded-md border border-gray-300 shadow-sm focus:border-black focus:outline-none"> 
                        </div>
                        <div>
                            <input type="text" name="color" id="color" 
                            v-model="driverDetails.color" placeholder="Color"
                            class="mt-1 block w-full px-3 py-2 rounded-md border border-gray-300 shadow-sm focus:border-black focus:outline-none"> 
                        </div>
                        <div>
                            <input type="text" name="license_plate" id="license_plate" 
                            v-model="driverDetails.license_plate" placeholder="License Plate"
                            class="mt-1 block w-full px-3 py-2 rounded-md border border-gray-300 shadow-sm focus:border-black focus:outline-none"> 
                        </div>
                        
                        <div class="px-4 py-3 text-center sm:px-6">
                            <button 
                            @click.prevent="handleSaveDriver"
                            type="submit" class="inline-flex justify-center rounded-md border border-transparent py-2 px-4 text-sm bg-black text-white font-medium">Continue</button>
                        </div>
                    </div> 
                </div>
            </div>
        </form>
    </div>
</template>

<script setup>
import { reactive } from 'vue';
import http from '@/helpers/http';
import router from '../router';


const driverDetails = reactive({
    name: '',
    year: null,
    make: '',
    model: '',
    color: '',
    license_plate: '',
})

const handleSaveDriver = () => {
    http().post('/api/driver', driverDetails)
        .then((response) => {
            // console.log(response.driverDetails.name);
            // console.log(response.driverDetails.year);
            // console.log(response.driverDetails.make);
            // console.log(response.driverDetails.model);
            // console.log(response.driverDetails.color);
            // console.log(response.driverDetails.license_plate);
            router.push({
                name: 'standby'
            })
        })
}
</script>

<style lang="scss" scoped>

</style>