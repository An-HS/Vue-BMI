<!-- computed -->
<template>
  <div class="text-center m-auto my-10 w-64 p-8 shadow-xl rounded-lg bg-white sm:w-72 md:w-96 lg:w-96">
    <p class="text-[color:#61CEA7] text-2xl sm:text-3xl md:text-3xl lg:text-4xl font-extrabold">BMI 計算機</p>

    <div class="text-[color:#9B9B9B]">
      <p class="my-1 text-left text-xs sm:text-sm md:text-base lg:text-base">身高</p>
      <div
        class="border-2 rounded-[8px] text-black border-[color:#61CEA7] w-full"
      >
        <input type="number" v-model="h" class="p-1 focus:outline-none w-36 sm:w-44 md:w-60 lg:w-64" />
        <span class="text-[color:#61CEA7] text-xs sm:text-sm md:text-base lg:text-base">公分</span>
      </div>

      <p class="my-1 text-left text-xs sm:text-sm md:text-base lg:text-base">體重</p>
      <div
        class="border-2 rounded-[8px] text-black border-[color:#61CEA7] w-full"
      >
        <input type="number" v-model="w" class="p-1 focus:outline-none w-36 sm:w-44 md:w-60 lg:w-64" />
        <span class="text-[color:#61CEA7] text-xs sm:text-sm md:text-base lg:text-base">公斤</span>
      </div>
    </div>

    <div class="mt-16">
      <p>
        BMI
        <span
          class="my-16 text-3xl"
          :class="level_data[level].textColor"
          >{{ bmi }}</span
        >
      </p>
    </div>
    <div
      class="mx-0 my-6 p-1 rounded-lg text-xs text-white sm:text-sm sm:mx-2 md:text-base md:mx-10 lg:text-lg lg:mx-8"
      :class="level_data[level].bgColor"      
    >
      你的體重為
      <span class="font-bold text-sm sm:text-lg md:text-xl lg:text-2xl">{{level_data[level].text}}</span>
    </div>

    <table class="w-full text-xs font-semibold sm:text-sm md:text-base lg:text-base">
      <tr v-for="item in level_data" :key="item" class="">
        <td class="text-left"
            :class="item.textColor">{{item.text}}</td>
        <td class="text-right"
            :class="item.textColor">{{item.bmi}}</td>
      </tr>
    </table>

  </div>
</template>

<script setup>
import { ref, computed } from "vue";
const level_data = [
  { text: "體重過輕", bgColor: "bg-blue-500", textColor: "text-blue-500", bmi:"BMI < 18.5" },
  { text: "正常範圍", bgColor: "bg-green-500", textColor: "text-green-500", bmi:"18.5 ≤ BMI < 24" },
  { text: "體重過重", bgColor: "bg-yellow-500" , textColor: "text-yellow-500", bmi:"24 ≤ BMI < 27"},
  { text: "輕度肥胖", bgColor: "bg-red-500", textColor: "text-red-500", bmi:"27 ≤ BMI < 30" },
  { text: "中度肥胖", bgColor: "bg-red-700", textColor: "text-red-700", bmi:"30 ≤ BMI < 35" },
  { text: "重度肥胖", bgColor: "bg-red-900", textColor: "text-red-900", bmi:"BMI ≥ 35" },
];
const h = ref(0);
const w = ref(0);
const bmi = computed(() => {
  if (w.value == 0) return 0;
  const num = (w.value / (h.value / 100) / (h.value / 100)).toFixed(2);
  return num;
});

const level = computed(() => {
    if( bmi.value < 18.5){
      return 0
    }else if( bmi.value >=18.5 &&  bmi.value < 24){
      return 1
    }else if( bmi.value >=24 &&  bmi.value < 27){
    return 2
    }else if( bmi.value >=27 &&  bmi.value < 30){
    return 3
    }else if( bmi.value >=30 &&  bmi.value < 35){
    return 4
    }else {
    return 5
    }
})
</script>

<style>
html{
  background-color: #61CEA7;
}
/* #app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
