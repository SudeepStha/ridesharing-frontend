<template>
    <div class="pt-16">
        <div class="overflow-hidden shadow sm:rounded-md max-w-sm mx-auto text-left">
            <div class="bg-white px-4 py-5 sm:p-6">
                <div class="flex justify-center">
                    <!-- form for login new user  -->
                    
                    <form action="#">
                        <h1>Where are we going?</h1>
                        <div class="my-4">
                            <input v-model="credentials.phone" type="text"  placeholder="My Destination">
                        </div>
                        <div class="flex justify-center">
                            <button type="submit" class="rounded-md border border-transparent py-2 px-4 text-sm bg-black text-white font-medium">Find A Ride</button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

</script>

<style lang="scss" scoped>

</style>