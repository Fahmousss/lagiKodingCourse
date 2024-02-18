<template>
   <Head title="Posts" />
   <AuthenticatedLayout>
       <template #header>
           <Link :href="route('posts.create')"
               class="inline-flex items-center px-4 py-2 bg-gray-800 border border-transparent rounded-lg font-semibold text-xs text-white uppercase tracking-widest hover:bg-white-700 active:bg-white-900 focus:outline-none focus:border-white-900 focus:ring ring-white-300 disabled:opacity-25 transition ease-in-out duration-150">
           Create Post
           </Link>
       </template>
       
       <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
           <div v-if="$page.props.flash.success" class=" text-center bg-gray-300 font-bold text-blue-900 p-1">
           {{ $page.props.flash.success }}
       </div>
               </div>
       <div class="py-12">
           <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
               <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                   <div class="mx-auto">
                       <table class="w-full whitespace-nowrap">
                           <thead>
                               <tr class="bg-gray-800 text-white font-extrabold">
                                   <th class="px-4 py-1 border">No</th>
                                   <th class="px-4 py-1 border">Title</th>
                                   <th class="px-4 py-1 border">Content</th>
                                   <th class="px-4 py-1 border">Actions</th>
                               </tr>
                           </thead>
                           <tbody>
                               <tr v-for="(item, index) in data" :key="item.id">
                                   <td class="px-4 text-center py-1 border">{{ index + 1 }}</td>
                                   <td class="px-4 text-center py-1 border">{{ item.title }}</td>
                                   <td class="px-4 text-center py-1 border">{{ item.body }}</td>
                                   <td class="px-4 text-center py-1 border">
                                       <PrimaryButton @click="edit(item.id)" class="mr-4">
                                           Edit
                                       </PrimaryButton>
                                       <DangerButton @click="destroy(item.id)">
                                           Delete
                                       </DangerButton>
                                   </td>
                               </tr>
                           </tbody>
                       </table>

                   </div>
               </div>
           </div>
       </div>

   </AuthenticatedLayout>
</template>
<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue'
import PrimaryButton from '@/Components/PrimaryButton.vue'
import DangerButton from '@/Components/DangerButton.vue'
import { router, Head, Link } from '@inertiajs/vue3'
const props = defineProps({
   data: Object,
})
const edit = (id) => {
   router.visit(route('posts.edit', id))
}
const destroy = (id) => {
   router.visit(route('posts.destroy', id), { method: 'delete' })
}
</script>