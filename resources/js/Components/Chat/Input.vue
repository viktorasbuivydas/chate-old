<template>
    <div>
        <ChatDropdown v-if="showMentionUsersList" @mention="handleMention" />
        <div class="absolute bottom-20 left-10">
            <EmojiPicker
                v-if="showEmojiList"
                @emoji_click="handleEmoji"
                @close="closeEmojiPicker"
            />
        </div>
        <form class="absolute bottom-0 w-full" @submit.prevent="submit">
            <label for="chat" class="sr-only">Your message</label>
            <div
                class="flex items-center px-3 py-2 bg-gray-50 dark:bg-gray-700"
            >
                <button
                    type="button"
                    class="cursor-not-allowed inline-flex justify-center p-2 text-gray-500 rounded-lg hover:text-gray-900 hover:bg-gray-100 dark:text-gray-400 dark:hover:text-white dark:hover:bg-gray-600"
                >
                    <svg
                        aria-hidden="true"
                        class="w-6 h-6"
                        fill="currentColor"
                        viewBox="0 0 20 20"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path
                            fill-rule="evenodd"
                            d="M4 3a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V5a2 2 0 00-2-2H4zm12 12H4l4-8 3 6 2-4 3 6z"
                            clip-rule="evenodd"
                        ></path>
                    </svg>
                    <span class="sr-only">Upload image</span>
                </button>
                <button
                    type="button"
                    @click="showEmojiList = !showEmojiList"
                    class="hidden md:flex p-2 text-gray-500 rounded-lg cursor-pointer hover:text-gray-900 hover:bg-gray-100 dark:text-gray-400 dark:hover:text-white dark:hover:bg-gray-600"
                >
                    <svg
                        aria-hidden="true"
                        class="w-6 h-6"
                        fill="currentColor"
                        viewBox="0 0 20 20"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path
                            fill-rule="evenodd"
                            d="M10 18a8 8 0 100-16 8 8 0 000 16zM7 9a1 1 0 100-2 1 1 0 000 2zm7-1a1 1 0 11-2 0 1 1 0 012 0zm-.464 5.535a1 1 0 10-1.415-1.414 3 3 0 01-4.242 0 1 1 0 00-1.415 1.414 5 5 0 007.072 0z"
                            clip-rule="evenodd"
                        ></path>
                    </svg>
                    <span class="sr-only">Add emoji</span>
                </button>
                <input
                    v-model="form.message"
                    @input="handleInput"
                    id="chat"
                    autocomplete="off"
                    class="block mx-4 p-2.5 w-full text-sm text-gray-900 bg-white rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-800 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 focus:outline-none"
                    placeholder="Your message..."
                />
                <button
                    type="submit"
                    :disabled="loading"
                    class="inline-flex justify-center p-2 text-blue-600 rounded-full cursor-pointer hover:bg-blue-100 dark:text-blue-500 dark:hover:bg-gray-600"
                >
                    <template v-if="!loading">
                        <svg
                            aria-hidden="true"
                            class="w-6 h-6 rotate-90"
                            fill="currentColor"
                            viewBox="0 0 20 20"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                d="M10.894 2.553a1 1 0 00-1.788 0l-7 14a1 1 0 001.169 1.409l5-1.429A1 1 0 009 15.571V11a1 1 0 112 0v4.571a1 1 0 00.725.962l5 1.428a1 1 0 001.17-1.408l-7-14z"
                            ></path>
                        </svg>
                    </template>
                    <template v-else>
                        <div role="status">
                            <svg
                                aria-hidden="true"
                                class="w-8 h-8 mr-2 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600"
                                viewBox="0 0 100 101"
                                fill="none"
                                xmlns="http://www.w3.org/2000/svg"
                            >
                                <path
                                    d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
                                    fill="currentColor"
                                />
                                <path
                                    d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
                                    fill="currentFill"
                                />
                            </svg>
                            <span class="sr-only">Loading...</span>
                        </div>
                    </template>

                    <span class="sr-only">Send message</span>
                </button>
            </div>
        </form>
    </div>
</template>

<script setup>
import { useForm } from "@inertiajs/inertia-vue3";
import { ref } from "vue";
import ChatDropdown from "@/Components/Chat/Dropdown.vue";
import EmojiPicker from "@/Components/EmojiPicker.vue";

const props = defineProps({
    chat: {
        type: Object,
        required: true,
    },
});

const form = useForm({
    message: "",
});

const loading = ref(false);
const showMentionUsersList = ref(false);
const showEmojiList = ref(false);

const submit = () => {
    loading.value = true;
    closeEmojiPicker();
    form.post(
        route("app.chat.messages.store", {
            chat: props.chat,
        }),
        {
            onSuccess: () => {
                form.reset("message");
            },
            onFinish: () => {
                loading.value = false;
            },
        }
    );
};

const handleInput = (e) => {
    if (e.target.value.startsWith("@") && e.target.value.length > 1) {
        showMentionUsersList.value = true;
    } else {
        showMentionUsersList.value = false;
    }
};

const handleMention = (user) => {
    form.message = `@${user.name} `;
    showMentionUsersList.value = false;
};

const handleEmoji = (emoji) => {
    form.message += emoji + " ";
};

const closeEmojiPicker = () => {
    showEmojiList.value = false;
};
</script>
