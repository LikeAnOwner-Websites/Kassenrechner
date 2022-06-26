<template>
    <div class="antialiased font-sans grid place-items-center h-screen text-black">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 mb-4 text-black">
            <div class="mt-10 mx-auto max-w-screen-xl px-4 sm:px-6">
                <div class="text-center">
                    <h1 class="text-4xl tracking-tight font-extrabold text-gray-900 sm:text-5xl md:text-6xl">
                        <span class="block xl:inline">Weiher</span> <span class="block text-indigo-600 xl:inline">Kassenrechner</span>
                    </h1>
                </div>
            </div>
            <div class="mt-8 mx-auto max-w-max grid grid-cols-2">
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
            </div>
            <div class="mx-auto max-w-max grid grid-cols-1">
                <button
                    type="button"
                    class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
                    @click="calculatePrice(4, 2)"
                >
                    SUP/Paddelboot
                    <span class="inline-flex items-center justify-center w-4 h-4 ml-2 text-xs font-semibold text-blue-800 bg-blue-200 rounded-full"> {{ boats }} </span>
                </button>
            </div>
            <div class="mt-8 text-center">
                <h1 class="text-6xl tracking-tight font-extrabold text-gray-900">
                    <span>{{ priceFormatted }}</span>
                </h1>
            </div>
            <div class="mt-8 mx-auto max-w-max grid grid-cols-3">
                <button
                    type="button"
                    class="mt-2 mb-6 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm p-2.5 text-center inline-flex items-center mr-2"
                    @click="undo"
                >
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M12 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2M3 12l6.414 6.414a2 2 0 001.414.586H19a2 2 0 002-2V7a2 2 0 00-2-2h-8.172a2 2 0 00-1.414.586L3 12z"
                        />
                    </svg>
                </button>
                <button
                    type="button"
                    class="mt-2 mb-6 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm p-2.5 text-center inline-flex items-center mr-2"
                    @click="clearPrice"
                >
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
                        />
                    </svg>
                </button>
                <button
                    type="button"
                    class="mt-2 mb-6 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm p-2.5 text-center inline-flex items-center mr-2"
                    @click="clearPrice"
                >
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
                    </svg>
                </button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'App',
    created() {
        document.title = 'Heisterberger Weiher - Kassenrechner';
    },
    data() {
        return {
            price: 0,
            kids: 0,
            adults: 0,
            boats: 0,
            inputHistory: [],
        };
    },
    methods: {
        calculatePrice(value, type) {
            this.price = this.price + value;
            this.inputHistory.push([value, type]);
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
            this.inputHistory = [];
        },
        undo() {
            if (this.inputHistory.length > 0) {
                this.price = this.price - this.inputHistory[this.inputHistory.length - 1][0];
                if (this.inputHistory[this.inputHistory.length - 1][1] === 0) {
                    this.kids--;
                } else if (this.inputHistory[this.inputHistory.length - 1][1] === 1) {
                    this.adults--;
                } else if (this.inputHistory[this.inputHistory.length - 1][1] === 2) {
                    this.boats--;
                }
                this.inputHistory.pop();
            }
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
