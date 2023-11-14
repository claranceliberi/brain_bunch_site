<script setup lang="ts">
import NavBar from '@/components/NavBar.vue'

</script>

<template>
  <main class="about">
        <!-- nav-section -->
        <!-- <NavBar /> -->

        <div class=" flex items-center relative w-full h-[100vh]">
            <div class="bg-[url(/img/challenges/chal-2.jpg)]  bg-cover bg-center w-full h-[100vh] absolute brightness-75">
            </div>


            <div class="flex z-10">
            
                <div class="challenge-description pl-10  max-w-xl space-y-4">
                    <div class="line w-10 h-2 bg-white"></div>
                    <div class="challenge-number text-slate-100"> Challenge 01 </div>
                    <div class="challenge-title text-8xl font-bold capitalize text-white"> Track the missing track </div>
                    <div class="challenge-solution text-slate-100">We have been able to produce the best solution to this challenge, do not worry how it gonna look like we have alot to care about</div>
                </div>
                <div class="challenges">
                </div>
            </div>

        </div>
  </main>
</template>