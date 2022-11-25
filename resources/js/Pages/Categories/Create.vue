<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link, useForm } from '@inertiajs/inertia-vue3';

const props = defineProps({
    categories: {
        type: Object,
        default: () => ({}),
    },
});

const form = useForm({
    title: ''
});

const submit = () => {
    form.post(route('categories.store'));
};

</script>

<template>

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Create Category
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm-rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <div class="flex items-center justify-between mb-6">
                            <Link class="px-6 py-2 text-white bg-blue-500 rounded" :href="route('categories.index')">
                            Back
                            </Link>
                        </div>
                        <form @submit.prevents="submit">
                            <div class="flex flex-col">
                                <div class="mb-4">
                                    <label 
                                    for="Title">Title</label>
                                    <input
                                    type="text"
                                    class="mt- block w-full"
                                    v-model="form.title"
                                    placeholder=""
                                    autofocus 
                                    />
                                <span class="text-red-600" v-if="form.errors.title">
                                    {{ form.errors.title }}
                                </span>
                                </div>
                            </div>

                            <div class="mt-4">
                            <button 
                                type="submit"
                                class="text-white bg-green-500 focus:outline-none px-6 py-2 rounded"
                                :disabled="form.processing"
                                :class="{ 'opacity-25': form.processing }"
                                >
                                    Save
                            </button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>