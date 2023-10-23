<script setup>
import MainNav from "@/Components/MainNav.vue";
import { useDark, useToggle } from "@vueuse/core";
import { ref, provide } from "vue";
import { Link } from "@inertiajs/vue3";

let width = ref("w-[220px]");
let hide = ref(false);
const selectedColor = ref("");
const isDark = useDark();
const toggleDark = useToggle(isDark);

provide("selectedColor", selectedColor);

function toggleWidth() {
    if (width.value == "w-[220px]") {
        width.value = "w-[100px]";
        hide.value = true;
    } else {
        width.value = ["w-[220px]"];
        hide.value = false;
    }
}
</script>

<template>
    <div class="flex min-h-screen">
        <div
            id="sidebar"
            class="bg-gray-400 p-6 duration-500"
            :class="
                ([width],
                {
                    'bg-red-600': selectedColor == 'red',
                    'bg-blue-600': selectedColor == 'blue',
                    'bg-green-600': selectedColor == 'green',
                })
            "
            style="position: relative"
        >
            <button
                class="text-xl text-white"
                @click="toggleWidth"
                style="position: absolute; right: 10px; top: 10px"
            >
                <i class="fa-solid fa-bars"></i>
            </button>
            <div id="branding" :hidden="hide">
                <img
                    src="https://img.freepik.com/free-photo/man-red-suit-with-blue-shirt-tie_1340-36720.jpg"
                    alt="Logo"
                    class="w-[170px] h-[170px] mx-auto rounded-full object-cover mb-2"
                />
            </div>

            <MainNav :hidden="hide"></MainNav>
            <div class="mt-5" :hidden="hide">
                <div class="flex flex-col text-white text-center">
                    
                    <button
                        class="bg-gray-700 p-2 rounded-full hover:bg-gray-900 duration-100"
                        @click="toggleDark()"
                    >
                    <span v-if="isDark"><i class="fa fa-sun"></i></span>
                    <span v-else><i class="fa fa-moon"></i></span>
                    </button>
                </div>
            </div>
        </div>
        <div id="container" class="flex-1 p-3 dark:bg-gray-800 dark:text-white">
            <slot />

        </div>
    </div>
</template>
