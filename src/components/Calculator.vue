<script setup lang="ts">
</script>

<template>
    <div class="flex justify-between sm-container mx-auto w-3/5">
        <h1 class="text-4xl">Course Hour Calculator</h1>
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="coursename">Course Name:</label>
        <input :value="coursename" type="text" class="w-3/5 border border-300 rounded-md" id="coursename" name="coursename">
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="lecturehour">Lecture Class Hour per Week:</label>
        <input type="text" class="w-3/5 border border-300 rounded-md" id="lecturehour" name="lecturehour">
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="tutorialhour">Tutorial Class Hour per Week:</label>
        <input type="text" class="w-3/5 border border-300 rounded-md" id="tutorialhour" name="tutorialhour">
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="practicalhour">Practical Class Hour per Week:</label>
        <input type="text" class="w-3/5 border border-300 rounded-md" id="practicalhour" name="practicalhour">
    </div>
    
    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="totalweek">Total Weeks:</label>
        <input type="text" class="w-3/5 border border-300 rounded-md" id="totalweek" name="totalweek">
    </div>

    <div class="flex justify-between sm-container mx-auto w-1/5">
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
            Calculate
        </button>

        <button class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded">
            Reset
        </button>

    </div>

    <div class="flex flex-col justify-center sm-container mx-auto w-3/5">
        <h2 class="text-3xl">Calculation Results</h2>
        <h4>This semester, you may skip {{ coursename }} hours of classes.</h4>
    </div>


</template>

<style scoped>
    h1 {
        font-size: 2rem;
    }

    label {
        font-size: 1.15rem;
    }

    div {
        margin: 1rem 0;
    }

    input {
        height: 2rem;
        padding: 0 0.5rem;
    }

</style>

<script setup lang="ts">
    export default {
        props: {
            coursename: String,
            lecturehours: Number,
            tutorialhours: Number,
            practicalhours: Number,
            totalweeks: Number,
            totalSkippableHours: Number,
        } as undefined as Props, // Cast props as the Props interface
        methods: {
            inputChange($event: Event) {
                this.$emit('inputChange', $event.target);
            },
            reset() {
                this.$emit('reset', null);

                // Clear out input values in the DOM
                const inputs = document.querySelectorAll('input');
                inputs.forEach(input => input.value = '');
            },
            calculate() {
                this.$emit('calculate', null);
            },
        },

    }
</script>