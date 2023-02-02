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
    modalOpen:false,
    selectedUser:Object,
});

function deleteUser(data) {
    // if(!confirm("Are you sure you want to delete this user " + data.name + "?")) return;
    router.delete(route('user.destroy', {customer:this.data.selectedUser}))
    this.data.modalOpen=false;
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
                        <Link class="pb-8" :href="route('user.create')">
                            <primary-button>
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v6m3-3H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />
                                </svg>
                                Crear Usuario
                            </primary-button>
                        </Link>
                        
                        <table class="table-auto w-full text-center">
                            <thead>
                                <tr>
                                    <th class="p-3">ID</th>
                                    <th class="p-3">NAME</th>
                                    <th class="p-3">EMAIL</th>
                                    <th class="p-3">ACTIONS</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="u in users" :key="u.id">
                                    <td class="p-3 border">{{u.id}}</td>
                                    <td class="p-3 border">{{u.name}}</td>
                                    <td class="p-3 border">{{u.email}}</td>
                                    <td class="p-3 border">
                                        <Link class="btn btn-success inline-block" :href="route('user.show', { customer:u })">
                                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                                                    <path stroke-linecap="round" stroke-linejoin="round" d="M2.036 12.322a1.012 1.012 0 010-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178z" />
                                                    <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                                                  </svg>
                                        </Link>
                                        <Link class="btn btn-primary inline-block" :href="route('user.edit', { customer:u })">
                                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                                                    <path stroke-linecap="round" stroke-linejoin="round" d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L10.582 16.07a4.5 4.5 0 01-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 011.13-1.897l8.932-8.931zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0115.75 21H5.25A2.25 2.25 0 013 18.75V8.25A2.25 2.25 0 015.25 6H10" />
                                                </svg>
                                        </Link>
                                        <!-- <Link :href="route('user.destroy', { customer:u })" method="DELETE" as="button">Delete</Link> -->
                                        <!-- <button @click="deleteUser(u)">Delete</button> -->
                                        <button class="btn btn-danger" style="vertical-align: top" @click="data.modalOpen=true;data.selectedUser=u">
                                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                                                <path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
                                            </svg>
                                        </button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <dialog-modal :show="data.modalOpen">
            <template v-slot:title>
                <h1>Titulo Modal</h1>
            </template>
            <template v-slot:content>
                <h1 v-if="data.selectedUser">Are you sure you want to delete this user {{data.selectedUser.name}}?</h1>
            </template>
            <template v-slot:footer>

                <primary-button @click="deleteUser()">Eliminar</primary-button>
                <danger-button @click="data.modalOpen=false" >Cerrar</danger-button>



            </template>
        </dialog-modal>
    </AppLayout>
</template>
