<script setup lang="ts">
import NavBar from '@/components/NavBar.vue'
import {gsap} from 'gsap'
import { onMounted } from 'vue';

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

</script>

<template>
  <main class="home-container w-full">
    <!-- nav-section -->
    <NavBar />

    <!-- images -->
    <div class="flex justify-center items-center h-[75vh]">
      <div class="images flex ">
      <div
        class="img img-1 hover:grayscale-[1] w-44 h-96 m-10 cursor-pointer scale-[1.1] bg-center bg-no-repeat bg-cover bg-[url('/img/img-1.jpg')]"
      ></div>
      <div
        class="img img-2 hover:grayscale-[1] w-44 h-96 m-10  cursor-pointer scale-[1.4] bg-center bg-no-repeat bg-cover bg-[url('/img/img-2.jpg')]"
      ></div>
      <div
        class="img img-3 hover:grayscale-[1] w-44 h-96 m-10 cursor-pointer scale-[1.1] bg-center bg-no-repeat bg-cover bg-[url('/img/img-3.jpg')]"
      ></div>
      <div
        class="img img-4 hover:grayscale-[1] w-44 h-96 m-10  cursor-pointer scale-[1.4] bg-center bg-no-repeat bg-cover bg-[url('/img/img-4.jpg')]"
      ></div>
      <div
        class="img img-5 hover:grayscale-[1] w-44 h-96 m-10 cursor-pointer scale-[1.1] bg-center bg-no-repeat bg-cover bg-[url('/img/img-5.jpg')]"
      ></div>
    </div>
    </div> . 

    <!-- title -->
    <div class="title">
      <span class="absolute text-[150px] uppercase text-white text-center w-full top-[40%] font-bold  tracking-[20px]">Brainy Bunch</span>
    </div>

    <div class="side-icon absolute top-[45%] text-4xl flex justify-between w-full p-10">
      <ion-icon name="arrow-dropleft-circle" class="icn"></ion-icon>
      <ion-icon name="arrow-dropright-circle" class="icn"></ion-icon>
    </div>

    <div class="bottom-bar w-full mx-auto mt-5 flex justify-around uppercase tracking-[4px]">
      <div>ALU</div>
      <div>2023</div>
      <div>Cohort 5</div>
    </div>

    <!-- social media -->
    <div class="media absolute right-[5%] bottom-[15%]">
      <ul class="p-3 ">
        <li class="text-2xl"><a target="_blank" href="https://www.instagram.com/brainybunch9/"><ion-icon name="logo-instagram"></ion-icon></a></li>
      </ul>
    </div>
  </main>
</template>
