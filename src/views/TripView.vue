<template>
    <div class="pt-16">
        <div class="overflow-hidden shadow sm:rounded-md max-w-sm mx-auto text-left">
            <div class="bg-white px-4 py-5 sm:p-6">
                <div>                    
                    <h1 class="text-3xl font-semibold mb-4 flex justify-center">Waiting for a driver...</h1>
                    <div class="bg-white px-4 py-5 sm:p-6">
                        <div>
                            <GMapMap :zoom="10" 
                            ref="gMap"
                            style="width: 100%; height: 190px;">
                            </GMapMap>
                        </div>
                        <div class="bg-gray-50 px-4 py-3 text-center sm:px-6">
                            <span>When a driver accepts the trip, their info will appear here.</span>
                        </div>
                    </div>
                </div> 
            </div>
        </div>
    </div>
</template>

<script setup>

</script>

<style lang="scss" scoped>

</style>