<template>
    <nav
        class="relative bg-white border border-0 border-b dark:border-gray-700 px-2 sm:px-4 py-2.5 dark:bg-gray-800"
    >
        <div
            class="container flex grow flex-wrap items-center justify-end mx-auto"
        >
            <div class="flex space-x-4 items-center md:order-2">
                <Material icon="chat_bubble" class="text-white" />
                <Material icon="notifications" class="text-white" />
                <button
                    @click="toggle"
                    type="button"
                    class="flex mr-3 text-sm bg-gray-800 rounded-full md:mr-0 focus:ring-4 focus:ring-gray-300 dark:focus:ring-gray-600"
                    id="user-menu-button"
                    aria-expanded="false"
                    data-dropdown-toggle="user-dropdown"
                    data-dropdown-placement="bottom"
                >
                    <span class="sr-only">Open user menu</span>
                    <img
                        class="w-8 h-8 rounded-full"
                        src="https://flowbite.com/docs/images/people/profile-picture-3.jpg"
                        alt="user photo"
                    />
                </button>
                <!-- Dropdown menu -->
                <div
                    v-if="toggled"
                    class="absolute right-10 top-5 z-50 my-4 text-base list-none bg-white divide-y divide-gray-100 rounded shadow dark:bg-gray-700 dark:divide-gray-600"
                    id="user-dropdown"
                >
                    <div class="px-4 py-3">
                        <span
                            class="block text-sm text-gray-900 dark:text-white"
                            >Bonnie Green</span
                        >
                        <span
                            class="block text-sm font-medium text-gray-500 truncate dark:text-gray-400"
                            >name@flowbite.com</span
                        >
                    </div>
                    <ul class="py-1" aria-labelledby="user-menu-button">
                        <li>
                            <Link
                                :href="route('app.profile.index')"
                                class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:hover:bg-gray-600 dark:text-gray-200 dark:hover:text-white"
                                >Nustatymai</Link
                            >
                        </li>
                        <li>
                            <a
                                href="#"
                                class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:hover:bg-gray-600 dark:text-gray-200 dark:hover:text-white"
                                >Atsijungti</a
                            >
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </nav>
</template>

<script setup>
import { ref } from "vue";
import Material from "@/Components/Material.vue";
import { Link } from "@inertiajs/inertia-vue3";

const toggled = ref(false);
const toggledNotifications = ref(false);
const toggledMessages = ref(false);

const toggle = () => {
    toggled.value = !toggled.value;
};

const toggleNotifications = () => {
    toggledNotifications.value = !toggledNotifications.value;
};

const toggleMessages = () => {
    toggledMessages.value = !toggledMessages.value;
};
</script>
