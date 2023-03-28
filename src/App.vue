<template>
  <div id="app">
    <div class="md-container mx-auto px-4 sm:px-6 lg:px-8 flex justify-center items-center flex-col">
      <Calculator
        :coursename="coursename"
        :lecturehours="lecturehours"
        :tutorialhours="tutorialhours"
        :practicalhours="practicalhours"
        :totalweeks="totalweeks"
        :totalSkippableHours="totalSkippableHours"
        @inputChange="inputChange"
        @reset="reset"
        @calculate="calculate"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Calculator from '@/components/Calculator.vue';

export default defineComponent({
  name: 'App',
  components: {
    Calculator,
  },
  data() {
    return {
      coursename: '',
      lecturehours: 0,
      tutorialhours: 0,
      practicalhours: 0,
      totalweeks: 0,
      totalSkippableHours: 0,
    };
  },
  methods: {
    inputChange(target: HTMLInputElement) {
      const id: string = target.id as string;

      if(id === "coursename") {
        this[id] = target.value;
        return;
      } else if(id === "lecturehours" || id === "tutorialhours" || id === "practicalhours" || id === "totalweeks" ) {
        this[id] = parseInt(target.value);
      }
    },
    reset() {
      this.coursename = '';
      this.lecturehours = 0;
      this.tutorialhours = 0;
      this.practicalhours = 0;
      this.totalweeks = 0;
      this.totalSkippableHours = 0;
    },
    calculate() {
      this.totalSkippableHours = (this.lecturehours + this.tutorialhours + this.practicalhours) * this.totalweeks * 0.2;
    },
  },
});
</script>
