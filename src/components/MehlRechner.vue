

<script setup lang="ts">
import { reactive, ref, computed } from 'vue';

const flour1 = ref(550);
const flour2 = ref(1050);
const targetflour = ref(880);
const targetgrams = ref(200);

const intermediate_result = computed(() => {
    if (flour1.value === flour2.value) {
        return 0;
    }
    return Math.round(((targetflour.value - flour2.value) / (flour1.value - flour2.value)) * 100);
});

const required_flour1 = computed(() => Math.round(targetgrams.value * intermediate_result.value / 100));
const required_flour2 = computed(() => targetgrams.value - required_flour1.value);

const result = { required_flour1, required_flour2 };
</script>

<template>
    <div class="calculator">
        <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
            <div class="grid grid-cols-2">

                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="flour1">
                        Mehltype 1
                    </label>
                    <input
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        id="flour1" v-model="flour1" type="text" placeholder="550">
                </div>
                <div class="ml-4 mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="flour2">
                        Mehltype 2
                    </label>
                    <input
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        id="flour2" v-model="flour2" type="text" placeholder="1050">
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="targetflour">
                        Zielmehltyp
                    </label>
                    <input
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        id="targetflour" v-model="targetflour" type="text" placeholder="880">
                </div>
                <div class="ml-4 mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="targetgrams">
                        Benötigte Mehlmenge [g]
                    </label>
                    <input
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        id="targetgrams" v-model="targetgrams" type="text" placeholder="200">
                </div>
            </div>
            <div class="mb-4 mt-2">
                <label class="block text-grey-700 text-lg">
                    Du benötigst {{ result.required_flour1 }}g von {{ flour1 }} und {{ result.required_flour2 }}g
                    von {{ flour2 }}
                    um {{ targetgrams }}g von {{ targetflour }} herzustellen.
                </label>
            </div>
        </form>
        <p class="text-center text-gray-500 text-xs">
            Alle Angaben ohne Gewähr
        </p>
    </div>
</template>

<style scoped>
@import './src/style.css';
</style>
