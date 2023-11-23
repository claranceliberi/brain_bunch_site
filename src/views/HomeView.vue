<script setup lang="ts">
import NavBar from '@/components/NavBar.vue'
import {gsap} from 'gsap'
import { onMounted, ref, computed } from 'vue';

onMounted(() => {


  gsap.from(".img", {
    duration:3,
    delay:0.7,
    opacity:0,
    y:20,
    ease:"expo.out",
  })

  gsap.from(".bottom-bar", {
    duration:2,
    delay:2,
    opacity:0,
    x: -40,
    ease:"expo.out",
  })

  gsap.from(".icn", {
    duration:2,
    delay:2.5,
    opacity:0,
    y:40,
    ease:"expo.out",
  })

  gsap.from(".title span", {
    duration:3,
    delay:3,
    opacity:0,
    x: -100,
    ease:"expo.out",
  })
  gsap.from(".media ul li", {
    duration:3,
    delay:3,
    opacity:0,
    x: 50,
    ease:"expo.out",
  })
})

const people = ref([
  {name:`Nelly`,image:`bg-[url('/img/img-1.jpg')]`},
  {name:`Liberi`,image:`bg-[url('/img/img-2.jpg')]`},
  {name:`Lyza`,image:`bg-[url('/img/img-3.jpg')]`},
  {name:`Eliel`,image:`bg-[url('/img/img-4.jpg')]`},
  {name:`Melisa`,image:`bg-[url('/img/img-5.jpg')]`},
  {name:`Mitali`,image:`bg-[url('/img/img-6.jpg')]`}
])

const filteredPeople  = computed(() => people.value.filter((person,index,array) => {
  // if(index !== array.length-1) return person 
  return true
}))

</script>

<template>
  <main class="home-container w-full">
    <!-- nav-section -->
    <NavBar />

    <!-- images -->
    <div class="flex justify-center items-center h-[75vh]">
      <div class="images flex ">
      <div v-for="person in filteredPeople" :key="person?.image"
        class="img img-1 hover:grayscale-[1] w-44 h-96 m-10 cursor-pointer scale-[1.1] bg-center bg-no-repeat bg-cover " :class="person?.image"
      ></div>
      
    </div>
    </div> . 

    <!-- title -->
    <div class="title pointer-events-none">
      <span class="absolute text-[150px] uppercase text-white text-center w-full top-[40%] font-bold  tracking-[20px]">Brainy Bunch</span>
    </div>

    <div class="side-icon absolute top-[45%] text-4xl flex justify-between w-full p-10">
      <span class="icn p-2 cursor-pointer"><ion-icon name="chevron-back-circle"></ion-icon></span>
      <span class="icn p-2 cursor-pointer"><ion-icon name="chevron-forward-circle"></ion-icon></span>
    </div>

    <div class="bottom-bar w-full mx-auto mt-5 flex justify-around uppercase tracking-[4px]">
      <div>ALU</div>
      <div>2023</div>
      <div>Cohort 5</div>
    </div>

    <!-- social media -->
    <div class="media absolute right-[5%] bottom-[15%]">
      <ul class="p-3 ">
        <li class="text-2xl animate-bounce"><a target="_blank" href="https://www.instagram.com/brainybunch9/"><ion-icon name="logo-instagram"></ion-icon></a></li>
      </ul>
    </div>
  </main>
</template>
