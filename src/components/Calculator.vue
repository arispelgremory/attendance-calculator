<script setup lang="ts">
    // Define props interface
    interface CalculatorOptions {
        coursename: string;
        lecturehours: number;
        tutorialhours: number;
        practicalhours: number;
        totalweeks: number;
        totalSkippableHours: number;
    }

    const props =  defineProps<CalculatorOptions>();
    const emit = defineEmits(['inputChange', 'reset', 'calculate']);

</script>

<template>
    <div class="flex justify-between sm-container mx-auto w-3/5">
        <h1 class="text-4xl">Course Hour Calculator</h1>
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="coursename">Course Name:</label>
        <input :value="coursename" @change="emit('inputChange', $event.target as HTMLInputElement)" type="text" class="w-3/5 border border-300 rounded-md" id="coursename" name="coursename">
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="lecturehours">Lecture Class Hour per Week:</label>
        <input :value="lecturehours" @change="emit('inputChange', $event.target as HTMLInputElement)" type="text" class="w-3/5 border border-300 rounded-md" id="lecturehours" name="lecturehours">
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="tutorialhours">Tutorial Class Hour per Week:</label>
        <input :value="tutorialhours" @change="emit('inputChange', $event.target as HTMLInputElement)" type="text" class="w-3/5 border border-300 rounded-md" id="tutorialhours" name="tutorialhours">
    </div>

    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="practicalhours">Practical Class Hour per Week:</label>
        <input :value="practicalhours" @change="emit('inputChange', $event.target as HTMLInputElement)" type="text" class="w-3/5 border border-300 rounded-md" id="practicalhours" name="practicalhours">
    </div>
    
    <div class="flex justify-between sm-container mx-auto w-3/5">
        <label for="totalweeks">Total Weeks:</label>
        <input :value="totalweeks" @change="emit('inputChange', $event.target as HTMLInputElement)" type="text" class="w-3/5 border border-300 rounded-md" id="totalweeks" name="totalweeks">
    </div>

    <div class="flex justify-between sm-container mx-auto w-1/5">
        <button @click="emit('calculate', null)" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
            Calculate
        </button>

        <button @click="emit('reset', null)" class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded">
            Reset
        </button>

    </div>

    <div v-show="totalSkippableHours" class="flexa flex-col justify-center sm-container mx-auto w-3/5">
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

    export default defineComponent<CalculatorOptions>({
    name: 'Calculator',
});
</script>