<template>
    <div class="pt-16">
        <h1 class="text-3xl font-semibold mb-4">{{ title }}</h1>
        <div v-if="!trip.id" class="mt-8 flex justify-center">
            <Loader />
        </div>
        <div v-else class="overflow-hidden shadow sm:rounded-md max-w-sm mx-auto text-left">
            <div class="bg-white px-4 py-5 sm:p-6">
                <div class="">                    
                    <!-- <h1 class="text-3xl font-semibold mb-4 flex justify-center">Where are we going?</h1> -->
                    <div>
                        <GMapMap :zoom="10" 
                        ref="gMap" :center="trip.destination"
                        style="width: 100%; height: 190px;">
                        </GMapMap>
                    </div>
                    <div class="mt-2">
                        <p class="text-xl">Going to <strong>{{ trip.destination_name }}</strong></p>
                    </div>
                </div> 
                <div class="flex justify-between bg-grayy-50 px-4 py-3 text-right sm:px-6">
                    <button class="rounded-md border border-transparent py-2 px-4 text-sm bg-black text-white font-medium">Decline</button>
                    <button class="rounded-md border border-transparent py-2 px-4 text-sm bg-black text-white font-medium">Accept</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

import Loader from '@/components/Loader.vue'
import Echo from 'laravel-echo'
import Pusher from 'pusher-js'
import { onMounted, ref } from 'vue';
import { useTripStore } from '@/stores/trip'

const gMap = ref(null)

const title = ref('Waiting for a ride request...')

const trip = useTripStore()
 
onMounted(() => {
    let echo = new Echo({
        broadcaster: 'pusher',
        key: 'mykey',
        cluster: 'mt1',
        wsHost: window.location.hostname,
        wsPort: 6001,
        forceTLS: false,
        disableStats: true,
        enabledTransports: ['ws', 'wss']
    })
    
    echo.channel('drivers')
    .listen('TripCreated', (e) => {
        title.value = 'Ride requested:'
        trip.$patch(e.trip)

        console.log('TripCreated', e)

        setTimeout(initMapDirections, 2000)
    })


})

const initMapDirections = () => {
    gMap.value.$mapPromise.then((mapObject) => {
        let originPoint = new google.maps.LatLng(trip.origin),
            destinationPoint = new google.maps.LatLng(trip.destination),
            directionsService = new google.maps.DirectionsService,
            directionsDisplay = new google.maps.DirectionsRenderer({
                map: mapObject
            })

        directionsService.route({
            origin: originPoint,
            destination: destinationPoint,
            avoidTolls: false,
            avoidHighways: false,
            travelMode: google.maps.TravelMode.DRIVING
        }, (res, status) => {
            if(status == google.maps.DirectionsStatus.OK){
                directionsDisplay.setDirections(res)
            }else{
                console.error(status);
            }
        })
    })
}

</script>

<style>

</style>