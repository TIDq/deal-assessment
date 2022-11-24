<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link, useForm } from '@inertiajs/inertia-vue3';

const props = defineProps({
    posts: Array
});

const form = useForm();
function destroy(id) {
    if (confirm('Are you sure you want to delete?')) {
        form.delete(route('posts.destroy', id));
    }
}
</script>

<template>

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Posts
            </h2>
        </template>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 px-6">
                <div class="flex items-center justify-between mb-6">
                    <Link class="px-6 py-2 text-white bg-green-500 rounded-md focus-outline:none"
                        :href="route('posts.create')">
                    Create Post
                    </Link>
                </div>
                <table class="table-fixed w-full">
                    <thead>
                        <tr class="bg-gray-200">
                            <th class="px-4 py-2">No.</th>
                            <th class="px-4 py-2">Title</th>
                            <th class="px-4 py-2">Body</th>
                            <th class="px-4 py-2">Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="post in posts">
                            <td class="border px-4 py-2">{{ post.id }}</td>
                            <td class="border px-4 py-2">{{ post.title }}</td>
                            <td class="border px-4 py-2">{{ post.body }}</td>
                            <td class="border px-4 py-2">
                                <Link tabindex="1" class="px-4 py-2 text-sm text-white bg-blue-500 rounded"
                                    :href="route('posts.edit', post.id)">
                                Edit
                                </Link>
                                <button @click="destroy(post.id)" tabindex="-1" type="button"
                                    class="mx-1 px-4 py-2 text-sm text-white bg-red-500 rounded">
                                    Delete
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </AuthenticatedLayout>
</template>