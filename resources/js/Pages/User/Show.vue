<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";



defineProps({ customer : Object })


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
                        
                        <label>Number: {{customer.id}}</label><br>
                        <label>Name: {{customer.name}}</label><br>
                        <label>Email: {{customer.email}}</label><br>

                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
