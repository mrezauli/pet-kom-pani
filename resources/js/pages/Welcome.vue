<script setup lang="ts">
import { Head, useForm } from '@inertiajs/vue3';

// Use Inertia's useForm with a remember key so Inertia will persist the
// form state across page reloads and tab/window closes.
// API shape: useForm(rememberKey, initialData)
const form = useForm('welcome_form', {
    numeric: '',
    alphanumeric: '',
    text: ''
});

const submit = () => {
    // Submit via Inertia; on success, reset the form which also clears the remembered state.
    form.post('/add', {
        onSuccess: () => {
            form.reset();
        }
    });
};
</script>

<template>

    <Head title="Welcome">
        <link rel="preconnect" href="https://rsms.me/" />
        <link rel="stylesheet" href="https://rsms.me/inter/inter.css" />
    </Head>
    <div
        class="flex min-h-screen flex-col items-center bg-[#FDFDFC] p-6 text-[#1b1b18] lg:justify-center lg:p-8 dark:bg-[#0a0a0a]">
        <header class="mb-6 w-full max-w-[335px] text-sm not-has-[nav]:hidden lg:max-w-4xl">
            <nav class="flex items-center justify-end gap-4">

            </nav>
        </header>
        <div
            class="flex w-full items-center justify-center opacity-100 transition-opacity duration-750 lg:grow starting:opacity-0">
            <main
                class="flex w-full max-w-[335px] flex-col-reverse overflow-hidden rounded-lg lg:max-w-4xl lg:flex-row">
                <form @submit.prevent="submit" class="w-full space-y-6 p-6">
                    <div>
                        <label for="numeric-input"
                            class="block text-sm font-medium text-gray-900 dark:text-gray-100">Numeric Input</label>
                        <input type="number" id="numeric-input" name="numeric-input" v-model="form.numeric"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 dark:border-gray-700 dark:bg-gray-800 dark:text-gray-100 sm:text-sm" />
                    </div>

                    <div>
                        <label for="alphanumeric-input"
                            class="block text-sm font-medium text-gray-900 dark:text-gray-100">Alphanumeric with Special
                            Characters</label>
                        <input type="text" id="alphanumeric-input" name="alphanumeric-input" v-model="form.alphanumeric"
                            pattern="^[a-zA-Z0-9!@#$%^&*()_+\-=[\]{};:'\\|,.<>\/?]*$"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 dark:border-gray-700 dark:bg-gray-800 dark:text-gray-100 sm:text-sm" />
                    </div>

                    <div>
                        <label for="text-area" class="block text-sm font-medium text-gray-900 dark:text-gray-100">Text
                            Area</label>
                        <textarea id="text-area" name="text-area" rows="20" v-model="form.text"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 dark:border-gray-700 dark:bg-gray-800 dark:text-gray-100 sm:text-sm"></textarea>
                    </div>

                    <div class="flex justify-end">
                        <button type="submit"
                            class="inline-flex items-center rounded-md border border-transparent bg-indigo-600 px-4 py-2 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 dark:bg-indigo-500 dark:hover:bg-indigo-400">
                            Submit
                        </button>
                    </div>
                </form>
            </main>
        </div>
        <div class="hidden h-14.5 lg:block"></div>
    </div>
</template>
