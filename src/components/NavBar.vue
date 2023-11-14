<script lang="ts"  setup>
import  { onMounted } from 'vue';
import gsap from 'gsap';

onMounted(() => {
    gsap.from(".logo", {
      duration:1.6,
    delay:0.2,
    opacity:0,
    y:20,
    ease:"expo.out",
  })

  gsap.from(".search", {
    duration:1.6,
    delay:0.2,
    opacity:0,
    y:20,
    ease:"expo.out",
  })
})
</script>
<template>
    <div class="navbar flex justify-between items-center w-[80%] my-10 mx-40 z-[1]">
      <div class="logo text-xl font-bold uppercase py-[10px] px-12">
        <span>Brainy Bunch</span>
      </div>
      <div class="search text-xl space-x-4 font-bold uppercase">
        <ion-icon name="search"></ion-icon>
        <ion-icon name="menu"></ion-icon>
      </div>
    </div>
</template>