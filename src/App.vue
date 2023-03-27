<template>
  <div id="app">
    <div class="md-container mx-auto px-4 sm:px-6 lg:px-8 flex justify-center items-center flex-col">
        <CalculatorVue :coursename="coursename" />
    </div>
  </div>

</template>

<script lang="ts">
import CalculatorVue from './components/Calculator.vue';

export default {
  components: {
    CalculatorVue
  },
  data() {
    return {
      coursename: 'Your course',
    }
  }, 
  
}
</script>