<template>
    <div class="antialiased font-sans">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 mb-4">
            <div class="mt-10 mx-auto max-w-screen-xl px-4 sm:px-6">
                <div class="text-center">
                    <h1 class="text-4xl tracking-tight font-extrabold text-gray-900 sm:text-5xl md:text-6xl">
                        <span class="block xl:inline">Weiher</span> <span class="block text-indigo-600 xl:inline">Kassenrechner</span>
                    </h1>
                </div>
            </div>
            <div class="mt-8 mx-auto max-w-max">
                <button
                    type="button"
                    class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
                    @click="calculatePrice(3, 0)"
                >
                    Kind/Student
                    <span class="inline-flex items-center justify-center w-4 h-4 ml-2 text-xs font-semibold text-blue-800 bg-blue-200 rounded-full"> {{ kids }} </span>
                </button>
                <button
                    type="button"
                    class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
                    @click="calculatePrice(4, 1)"
                >
                    Erwachsener
                    <span class="inline-flex items-center justify-center w-4 h-4 ml-2 text-xs font-semibold text-blue-800 bg-blue-200 rounded-full"> {{ adults }} </span>
                </button>
                <button
                    type="button"
                    class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
                    @click="calculatePrice(4, 2)"
                >
                    SUP/Paddelboot
                    <span class="inline-flex items-center justify-center w-4 h-4 ml-2 text-xs font-semibold text-blue-800 bg-blue-200 rounded-full"> {{ boats }} </span>
                </button>
                <div class="flex flex-row space-x-2">
                    <input
                        type="text"
                        id="disabled-input"
                        class="mt-2 mb-6 bg-gray-100 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 cursor-not-allowed dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-gray-400 dark:focus:ring-blue-500 dark:focus:border-blue-500"
                        v-model="priceFormatted"
                        disabled
                    />
                    <button
                        type="button"
                        class="mt-2 mb-6 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm p-2.5 text-center inline-flex items-center mr-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                        @click="clearPrice"
                    >
                        <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path
                                fill-rule="evenodd"
                                d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z"
                                clip-rule="evenodd"
                            ></path>
                        </svg>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'App',
    data() {
        return {
            price: 0,
            kids: 0,
            adults: 0,
            boats: 0,
        };
    },
    methods: {
        calculatePrice(value, type) {
            this.price = this.price + value;
            if (type === 0) {
                this.kids++;
            } else if (type === 1) {
                this.adults++;
            } else if (type === 2) {
                this.boats++;
            }
        },
        clearPrice() {
            this.price = 0;
            this.kids = 0;
            this.adults = 0;
            this.boats = 0;
        },
    },
    computed: {
        priceFormatted() {
            return this.price + ' €';
        },
    },
};
</script>

<style></style>
