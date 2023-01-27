<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
import InputError from "@/Components/InputError.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";


import { router } from '@inertiajs/vue3'
import { reactive } from 'vue'

defineProps({ errors: Object },{ user: Object })


const form = reactive({
    name: "",
    email: "",
    password: "",
});
function submit() {
    router.post(route('user.store'), form)
}
</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Add Users
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <div class="p-6 sm:px-20 bg-white border-b border-gray-200">
                        <form @submit.prevent="submit">
                            <label>Name: </label>
                            <input class="my-1 block w-full" type="text" v-model="form.name"/>
                            <input-error :message="errors.name" />

                            <label>Email: </label>
                            <input class="my-1 block w-full" type="text" v-model="form.email"/>
                            <input-error :message="errors.email" />

                            <label>Password: </label>
                            <input class="my-1 block w-full" type="password" v-model="form.password"/>
                            <input-error :message="errors.password" />

                            <primary-button type="submit">Submit</primary-button>
                        </form>
                        
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
