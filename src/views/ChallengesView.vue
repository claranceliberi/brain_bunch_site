<script setup lang="ts">
import NavBar from '@/components/NavBar.vue'
import { ref, computed } from 'vue';
import { gsap } from 'gsap'



const challenges = ref([
    {
        id:'01',
        number: 'Challenge 01',
        title:'Track the missing track',
        description:'We have been able to produce the best solution to this challenge, do not worry how it gonna look like we have alot to care about',
        image: 'bg-[url(/img/challenges/chal-1.jpg)]'
    },
    {
        id:'02',
        number: 'Challenge 02',
        title:'We are here for Good',
        description:'We have been able to produce the best solution to this challenge, do not worry how it gonna look like we have alot to care about',
        image: 'bg-[url(/img/challenges/chal-2.jpg)]'
    },
    {
        id:'03',
        number: 'Challenge 03',
        title:'Dark appears in the absence of light',
        description:'We have been able to produce the best solution to this challenge, do not worry how it gonna look like we have alot to care about',
        image: 'bg-[url(/img/challenges/chal-3.jpg)]'
    },
    {
        id: '04',
        number: 'Challenge 04',
        title:'Nothing heals past like time',
        description:'We have been able to produce the best solution to this challenge, do not worry how it gonna look like we have alot to care about',
        image: 'bg-[url(/img/challenges/chal-4.jpg)]'
    }
])
const active = ref(challenges.value.length - 1)
const activeChallenge = computed(() => challenges.value[active.value])



function handleSlides(index: number) {
    const activeChal = challenges.value[index]
    challenges.value.push(activeChal)
    challenges.value.splice(index, 1)
}

function startDescription(){
    gsap.from(".challenge-description .line", {
    duration:3,
    delay:0.1,
    opacity:0,
    y:20,
    ease:"expo.out",
  })

  gsap.from(".challenge-description .challenge-number", {
    duration:3,
    delay:0.1,
    opacity:0,
    y:20,
    ease:"expo.out",
  })

  gsap.from(".challenge-description .challenge-title", {
    duration:3,
    delay:0.1,
    opacity:0,
    y:20,
    ease:"expo.out",
  })

  gsap.from(".challenge-description .challenge-solution", {
    duration:3,
    delay:0.1,
    opacity:0,
    y:20,
    ease:"expo.out",
  })
  
  animateChallengeCards()

  console.log('ahaa')
}


function animateChallengeCards(){

    const totalWidth = getTotalWidthWithMargin(".challenge-card");
    gsap.from(".challenge-card", {
        duration:1,
        x:totalWidth,
    })
}


function getTotalWidthWithMargin(selector:string) {
    const element = document.querySelector(selector) as HTMLElement;
    const style = window.getComputedStyle(element);

    const width = element.offsetWidth; // Width including padding and border
    const margin = parseFloat(style.marginLeft) + parseFloat(style.marginRight);

    return width + margin;
}

</script>

<template>
  <main class="about">
        <!-- nav-section -->
        <!-- <NavBar /> -->

        <div class=" flex items-end relative w-full h-[100vh]">
            <div class=" bg-cover bg-center w-full h-[100vh] absolute brightness-50 " :class="challenges[active].image">
            </div>


            <div class="flex justify-stretch z-10 pt-10 relative w-full pb-32">
            
               <TransitionGroup @enter="startDescription" :css="false" appear>
                <template v-for="(challenge,i) in challenges" :key="challenge.id">
                    <div class="challenge-description pl-10  max-w-xl space-y-4 " v-if="i === active" >
                        <div class="line w-10 h-2 bg-white"></div>
                        <div class="challenge-number text-slate-100"> {{challenge.number}} </div>
                        <div class="challenge-title text-8xl font-bold capitalize text-white"> {{ challenge.title }} </div>
                        <div class="challenge-solution text-slate-100"> {{ challenge.description }} </div>
                    </div>
               </template>
               </TransitionGroup>
                <div class="challenges flex items-end justify-end flex-1 pb-4 translate-x-16">
                    <template 
                     v-for="(challenge, i) in challenges"
                     :key="challenge.id" >
                        <div @click="handleSlides(i)"  class="challenge-card h-80 w-52 mx-4 rounded-xl flex relative items-end shadow-lg shadow-black/70 cursor-pointer" v-if="i !=active">
                            <div class="absolute bg-cover bg-center w-full h-full brightness-75 " :class="challenge.image"></div>
                            <div  class="absolute bg-cover bg-center w-full h-full brightness-75 " :class="`${challenge.image} bg-image-${challenge.id}`"></div>
                            <div class="text-white z-10 p-3 space-y-2">
                                <div class="challenge--card__line h-1 w-6 bg-white" ></div>
                                <div class="challenge--card__number text-sm">{{ challenge.number }}</div>
                                <div class="challenge--card__title capitalize font-bold text-2xl">{{ challenge.title }}</div>
                            </div>
                        </div>
                    </template>
                   
                </div>
            </div>

        </div>
  </main>
</template>
