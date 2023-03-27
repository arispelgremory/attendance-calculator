<script lang="ts">
</script>

<template>
    <div class="flex justify-between sm-container mx-auto w-3/5">
        <h1 class="text-4xl">Course Hour Calculator</h1>
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="coursename">Course Name:</label>
        <input v-on:input="inputChange" type="text" class="w-3/5 border border-300 rounded-md" id="coursename" name="coursename">
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="lecturehour">Lecture Class Hour per Week:</label>
        <input v-on:input="inputChange" type="text" class="w-3/5 border border-300 rounded-md" id="lecturehour" name="lecturehour">
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="tutorialhour">Tutorial Class Hour per Week:</label>
        <input v-on:input="inputChange" type="text" class="w-3/5 border border-300 rounded-md" id="tutorialhour" name="tutorialhour">
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="practicalhour">Practical Class Hour per Week:</label>
        <input v-on:input="inputChange" type="text" class="w-3/5 border border-300 rounded-md" id="practicalhour" name="practicalhour">
    </div>
    
    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="totalweeks">Total Weeks:</label>
        <input v-on:input="inputChange" type="text" class="w-3/5 border border-300 rounded-md" id="totalweek" name="totalweek">
    </div>

    <div class="flex justify-between sm-container mx-auto w-1/5">
        <button @click="calculate" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
            Calculate
        </button>

        <button @click="reset" class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded">
            Reset
        </button>

    </div>

    <div v-show="totalSkippableHours" class="flex flex-col justify-center sm-container mx-auto w-3/5">
        <h2 class="text-3xl">Calculated Results</h2>
        <h4 class="text-lg">This semester, you may skip {{ coursename }}'s {{ totalSkippableHours }} hours of classes.</h4>
        <div>
            <p>Which equals to:</p>
            <h3 v-show="lecturehours && totalSkippableHours" class="text-xl text-sky-500">{{ totalSkippableHours / lecturehours | 0 }} times of lecture classes OR</h3> 
            <h3 v-show="tutorialhours  && totalSkippableHours" class="text-xl text-sky-500">{{ totalSkippableHours / tutorialhours | 0 }} times of tutorial classes OR</h3> 
            <h3 v-show="practicalhours && totalSkippableHours" class="text-xl text-sky-500">{{ totalSkippableHours / practicalhours | 0 }} times of practical classes</h3>
            
        </div>
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

<script lang="ts">
    import { defineComponent } from 'vue';

    interface Props {
        coursename: string;
        lecturehours: number;
        tutorialhours: number;
        practicalhours: number;
        totalweeks: number;
        totalSkippableHours: number;
    }

    export default defineComponent({
        name: 'CourseHourCalculator',
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
                console.log('Calculate');
                
                this.$emit('calculate', null);
            },
        },
        emits: ['inputChange', 'reset', 'calculate'],
    });

</script>