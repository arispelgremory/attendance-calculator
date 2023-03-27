<template>
  <div id="app">
    <div class="md-container mx-auto px-4 sm:px-6 lg:px-8 flex justify-center items-center flex-col">
        <CalculatorVue 
          :coursename="coursename" 
          :lecturehours="lecturehours" 
          :tutorialhours="tutorialhours"
          :practicalhours="practicalhours"
          :totalweeks="totalweeks"
          :totalSkippableHours = "totalSkippableHours"
          @inputChange="inputChange"
          @reset="reset"
          @calculate="calculate"
        />
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
      lecturehours: 0,
      tutorialhours: 0,
      practicalhours: 0,
      totalweeks: 0,
      totalSkippableHours: 0,
    }
  }, 
  methods: {
    inputChange($event) {
      const { id, value } = $event;
      
      if (id === 'coursename') {
        this.coursename = value;
      } else if (id === 'lecturehour') {
        this.lecturehours = parseInt(value) || 0;
      } else if (id === 'tutorialhour') {
        this.tutorialhours = parseInt(value) || 0;
      } else if (id === 'practicalhour') {
        this.practicalhours = parseInt(value) || 0;
      } else if (id === 'totalweek') {
        this.totalweeks = parseInt(value) || 0;
      }
    },
    reset() {
      this.coursename = "";
      this.lecturehours = 0;
      this.tutorialhours = 0;
      this.practicalhours = 0;
      this.totalweeks = 0;
      this.totalSkippableHours = 0;
    }, 
    calculate() {
      const totalhours: number = this.lecturehours + this.tutorialhours + this.practicalhours;
      this.totalSkippableHours = Math.floor((totalhours * this.totalweeks) * 0.2); // 20% of total hours
    }
  }
  
}
</script>