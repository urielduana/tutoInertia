<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
import DialogModal from "@/Components/DialogModal.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import DangerButton from "@/Components/DangerButton.vue";

import { reactive } from 'vue'
import { Link } from '@inertiajs/vue3'
import { router } from '@inertiajs/vue3'

defineProps({ users: Object })

const data = reactive({
    modalOpen: false,
});

function deleteUser(data) {
    if(!confirm("Are you sure you want to delete this user " + data.name + "?")) return;
    router.delete(route('user.destroy', {customer:data}))
}

</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Users
            </h2>
        </template>
        
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <div class="p-6 sm:px-20 bg-white border-b border-gray-200">
                        <br>
                        <Link :href="route('user.create')">Crear Usuario</Link>


                        <table class="table-auto w-full text-center">
                            <thead>
                                <tr>
                                    <th class="p-3">Id</th>
                                    <th class="p-3">Nombre</th>
                                    <th class="p-3">Email</th>
                                    <th class="p-3">Acciones</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="u in users" :key="u.id">
                                    <td class="p-3 border">{{u.id}}</td>
                                    <td class="p-3 border">{{u.name}}</td>
                                    <td class="p-3 border">{{u.email}}</td>
                                    <td class="p-3 border">
                                        <Link :href="route('user.show', { customer:u })">Details</Link>
                                        <Link :href="route('user.edit', { customer:u })">Edit</Link>
                                        <!-- <Link :href="route('user.destroy', { customer:u })" method="DELETE" as="button">Delete</Link> -->
                                        <button @click="deleteUser(u)">Delete</button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <dialog-modal :show="modalOpen">
            <template v-slot:title>
                <h1>Titulo Modal</h1>
            </template>
            <template v-slot:content>
                <h1>Hola</h1>
            </template>
            <template v-slot:footer>
                <danger-button @click="modalOpen=false">
                    Cerrar
                </danger-button>
            </template>
        </dialog-modal>
    </AppLayout>
</template>
