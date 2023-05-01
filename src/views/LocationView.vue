<template>
    <div class="pt-16">
        <div class="overflow-hidden shadow sm:rounded-md max-w-sm mx-auto text-left">
            <div class="bg-white px-4 py-5 sm:p-6">
                <div class="flex justify-center">
                    <!-- form for login new user  -->
                    
                    <form action="#">
                        <h1 class="text-3xl font-semibold mb-4 flex justify-center">Where are we going?</h1>
                        <div class="my-4">
                            <GMapAutocomplete
                                placeholder="My destination"
                                @place_changed="handleLocationChanged"
                                class="mt-1 block w-full px-3 py-2 rounded-md border border-gray-300 shadow-sm focus:border-black focus:outline-none"
                                >
                            </GMapAutocomplete>
                        </div>
                        <div class="flex justify-center">
                            <button 
                            @click.prevent="handleSelectLocation"
                            type="submit" class="rounded-md border border-transparent py-2 px-4 text-sm bg-black text-white font-medium">Find A Ride</button>
                        </div>
                    </form>
                </div> 
            </div>
        </div>
    </div>
</template>

<script setup>
// import { useLocationStore } from '@/stores/location'
import { useLocationStore } from '@/stores/location'
import router from '../router';

const location = useLocationStore();

const handleLocationChanged = (e) => {
    
    console.log('handleLocationChanged', e)

    location.$patch({
        destination: {
            name: e.name,
            address: e.formatted_address,
            geometry: {
                lat: e.geometry.location.lat(),
                lng: e.geometry.location.lng(),
            }
        }
    })
}

const handleSelectLocation = () => {
    if(location.destination.name !== ''){
        router.push({
            name: 'map'
        })
    }
}
</script>

<style lang="scss" scoped>

</style>