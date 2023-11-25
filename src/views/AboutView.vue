<script setup lang="ts">
import NavBar from '@/components/NavBar.vue'
import { reactive, ref } from 'vue';

type TextType = 'problem' | 'solution' | 'mission'
type Data = {
  title:string,
  description:string,
  image:string
}
type DataType = Record<TextType, Data>

const data = reactive<DataType>({
  problem:{
    title:'Addressing Malnutrition and Poverty in Rutsiro District, Rwanda',
    description:`According to the Ministry of Health [MOH] [Rwanda], 2019/2020, stunting in the Rutsiro district has dropped to 44.4 % in 2020 from 45.1 % in 2015.
The national goal is to reduce stunting to 19 percent in 2024. 
immense poverty since the end of the civil war and genocide in 1994 caused a high malnutrition rate and low access to an efficient, balanced diet.
Since then, their agricultural production has been at a shallow rate, which caused an increase in the cost of living of people in that community in different aspects, including the market cost of things and distance from the source of agricultural products.
`,
image: '/img/problem.jpg'
  },
  solution:{
    title:'Sustainable Approach to Combating Malnutrition and Poverty',
    description:`We found that the root cause of poor health conditions and high malnutrition rate sustained in different parts of Rwanda is poverty, whereby the demographic health survey made in 2019/2020 showed that the poor health conditions and malnutrition rates didn't decrease as expected from the year's national goal. The government and different N.G.O.s tried to solve these problems by trying to distribute additional food supplements, including shisha kibondo among others, trying to provide nutritional education, gira inka program, hygiene, and sanitation programs, and all those solutions didn't work sustainably because people instead of using all these aid supports, they result selling them for covering their other basic needs. So, that's why we decided to first base on how to increase their living standard sustainably instead of giving them different food supplements, among others. We suggested making an NGO which connect different farmers cooperatives to boost the productivity of cash crops that can directly consumed by local people and be exported at high rate to raise enough income for paying local people for firstly solving their poverty issues which is causing the malnutrition problems. After solving this poverty issue, people will have good living standards and improved health conditions, and the malnutrition rate will decrease.`,
    image: '/img/solution.png'
  },
  mission:{
    title:'Enhancing Agricultural Practices for Healthier Communities in Africa',
    description:`Our mission statement is to improve efficiency in agricultural practices 
for upgrading access and affordability to a balanced diet to get proper health conditions 
in different African communities.`,
    image: '/img/mission.jpg'
  }
})

const active = ref<TextType>('mission')

</script>

<template>
  <main class="about">
        <!-- nav-section -->
        <NavBar />

        <div class="px-8">
          <div class="flex space-x-4 py-4">
            <button @click="active = 'mission'" class="py-2 px-4 border-2 border-solid border-black  rounded-full  transition-all duration-75" :class="{'bg-black text-white': active == 'mission'}">Mission</button>
            <button @click="active = 'problem'" class="py-2 px-4 border-2 border-solid border-black  rounded-full  transition-all duration-75" :class="{'bg-black text-white': active == 'problem'}">Problem</button>
            <button @click="active= 'solution'" class="py-2 px-4 border-2 border-solid border-black  rounded-full  transition-all duration-75" :class="{'bg-black text-white': active == 'solution'}">Solution</button>
          </div>
          <div class="py-8">
            <Transition name="slide-fade" mode="out-in">
              <div v-if="active == 'problem'" class="flex space-x-6 items-center">
                <div class="w-1/2">
                  <h1 class="pb-8 text-3xl font-semibold ">{{ data.problem.title }}</h1>
                <p>{{ data.problem.description }}</p>
                </div>
                <div class="py-8">
                  <img :src="data.problem.image" alt="" class="w-full h-full object-cover max-h-96">
                </div>
              </div>
              <div v-else-if="active == 'solution'"  class="flex space-x-6 items-center">
                <div class="w-1/2">
                  <h1 class="pb-8 text-3xl font-semibold ">{{ data.solution.title }}</h1>
                <p>{{ data.solution.description }}</p>
                </div>
                <div class="py-8 w-1/2">
                  <img :src="data.solution.image" alt="" class="w-full h-full object-cover ">
                </div>
              </div>
              <div v-else-if="active == 'mission'"  class="flex space-x-6 items-center">
                <div class="w-1/2">
                  <h1 class="pb-8 text-3xl font-semibold ">{{ data.mission.title }}</h1>
                <p>{{ data.mission.description }}</p>
                </div>
                <div class="py-8 w-1/2">
                  <img :src="data.mission.image" alt="" class="w-full h-full object-cover">
                </div>
              </div>
            </Transition>

          </div>
        </div>
  </main>
</template>

<style>

.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
</style>
