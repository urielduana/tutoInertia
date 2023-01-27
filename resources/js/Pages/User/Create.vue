<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
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
                            <input type="text" v-model="form.name"  id="name"/>
                            <div v-if="errors.name">{{ errors.name }}</div>

                            <label>Email: </label>
                            <input type="text" v-model="form.email" id="email"/>
                            <div v-if="errors.email">{{ errors.email }}</div>

                            <label>Password: </label>
                            <input type="password" v-model="form.password" id="password"/>
                            <div v-if="errors.password">{{ errors.password }}</div>

                            <button type="submit">Submit</button>
                        </form>
                        
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
