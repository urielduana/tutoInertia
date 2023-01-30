<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
import InputError from "@/Components/InputError.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";

import { router } from '@inertiajs/vue3'
import { reactive } from 'vue';

const props = defineProps({ customer: Object, errors : Object })


const form = reactive({
    name: props.customer.name,
    email: props.customer.email,
    password: "",
});


function submit() {
    router.put(route('user.update', {'customer':props.customer}), form)
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
                            <input-error :message="props.errors.name" />

                            <label>Email: </label>
                            <input class="my-1 block w-full" type="text" v-model="form.email"/>
                            <input-error :message="props.errors.email" />

                            <label>Password: </label>
                            <input class="my-1 block w-full" type="password" v-model="form.password"/>
                            <input-error :message="props.errors.password" />

                            <primary-button type="submit">Submit</primary-button>

                            
                        </form>
                        
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
