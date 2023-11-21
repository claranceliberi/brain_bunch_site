<script setup lang="ts">
import NavBar from '@/components/NavBar.vue'
import { ref, computed, onMounted } from 'vue';
import { gsap } from 'gsap'


const challenges = ref([
    {
        id:1,
        number: 'Challenge 01',
        title:'Track the missing track',
        description:'We have been able to produce the best solution to this challenge, do not worry how it gonna look like we have alot to care about',
        image: 'bg-[url(/img/challenges/chal-1.jpg)]'
    },
    {
        id:2,
        number: 'Challenge 02',
        title:'We are here for Good',
        description:'We have been able to produce the best solution to this challenge, do not worry how it gonna look like we have alot to care about',
        image: 'bg-[url(/img/challenges/chal-2.jpg)]'
    },
    {
        id:3,
        number: 'Challenge 03',
        title:'Dark appears in the absence of light',
        description:'We have been able to produce the best solution to this challenge, do not worry how it gonna look like we have alot to care about',
        image: 'bg-[url(/img/challenges/chal-3.jpg)]'
    },
    {
        id: 4,
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
    replaceImageCoverInContainer(activeChal.id, {
        onStart: () => {
            gsap.to('.challenge-description', {
                duration:1,
                opacity:0,
                x:-200,
                ease:'expo.out',
            
            })
        },
        onEnd: () => {
        challenges.value.push(activeChal)
        challenges.value.splice(index, 1)
    }
    })


}

function startDescription(){
    gsap.from(".challenge-description", {
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

    // gsap.to(prevChallengeImageCover, {
    //     duration:1,
    //     opacity:0,
    //     ease:'expo.out',
    // })


    const totalWidth = getTotalWidthWithMargin(".challenge-card");
    gsap.from(".challenge-card", {
        duration:1.5,
        x:totalWidth,
        ease:'expo.out',
        stagger:0.2,
    })



}


function getTotalWidthWithMargin(selector:string) {
    const element = document.querySelector(selector) as HTMLElement;
    const style = window.getComputedStyle(element);

    const width = element.offsetWidth; // Width including padding and border
    const margin = parseFloat(style.marginLeft) + parseFloat(style.marginRight);

    return width + margin;
}

function addImageToContainer(chal: typeof challenges.value[0]){
    const containerElement = document.querySelector('.slide-container') as HTMLElement;

    const imageCover = document.createElement('div');
    imageCover.classList.add('bg-cover', 'bg-center', 'absolute', 'brightness-90','rounded-xl' , 'cover-'+chal.id, chal.image);

    containerElement.appendChild(imageCover);

    return imageCover;
}

async function replaceImageCoverInContainer(challengeId:number, {onStart, onEnd}: {onStart?: () => void, onEnd?: () => void} = {}){
    onStart && onStart()
    const prevChallengeCardId = ((challengeId +2) % 4) +1     
    const newChallengeCard = document.querySelector(`.challenge-card-id__${challengeId}`) as HTMLElement;
    const newChallengeCardRect = newChallengeCard.getBoundingClientRect();

    const imageCover =  addImageToContainer(challenges.value.find(chal => chal.id === challengeId)!)
    

    //START: animate the card that is leaving
    gsap.to(`.challenge-card-id__${challengeId}`,{
        duration:0.01,
        boxShadow: 'none',
        
    })

    gsap.to(`.challenge-card-id__${challengeId} .text-description`,{
        duration:1,
        opacity:0,
        y:20,
        ease:'expo.out',
    })

    gsap.to(`.challenge-card-id__${challengeId} .bg-cover`,{
        duration:0.01,
        opacity:0,
        backgroundImage: 'none',
        
    })
    // END: animate the card that is leaving

    // START: animate image cover to fill the screen
    gsap.fromTo(imageCover, {
        width: `${newChallengeCardRect.width}px`,
        height: `${newChallengeCardRect.height}px`,
        top: `${newChallengeCardRect.top}px`,
        left: `${newChallengeCardRect.left}px`,
    }, {
        duration:1,
        width: '100vw',
        height: '100vh',
        borderRadius: 0,
        top: 0,
        left: 0,
        ease:'power4.out',
        onComplete: () => {
            onEnd && onEnd()
        }
    })
    // END: animate image cover to fill the screen

    const prevChallengeImageCover = document.querySelector(`.cover-${prevChallengeCardId}`) as HTMLElement;

    console.log(challengeId, prevChallengeCardId,prevChallengeImageCover)
    // START: animate the image cover that is leaving
    gsap.to(prevChallengeImageCover, {
        duration:1,
        opacity:0,
        scale:1.5,
        ease:'expo.out',
        onComplete: () => {
            // remove previous image cover
            if(prevChallengeImageCover)
                prevChallengeImageCover.remove();
        }
    })
    // END: animate the image cover that is leaving

}


onMounted(() => {
    // console.log('mounted')
    const imageCover =  addImageToContainer(challenges.value[active.value])
imageCover.classList.add('w-full', 'h-full', 'top-0', 'left-0', 'z-0','rounded-none')
})

</script>

<template>
  <main class="about">
        <!-- nav-section -->
      
            <NavBar theme="light" class="absolute top-0 z-10 w-full"/>
    

        <div class=" flex items-end w-full h-[100vh] slide-container  overflow-hidden bg-black">

            <div class="flex justify-stretch z-10 pt-10  w-full pb-32">
            
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
                        <div @click="handleSlides(i)" :class="`challenge-card-id__${challenge.id}`"  class="challenge-card h-80 w-52 mx-4 rounded-xl flex relative items-end shadow-lg shadow-black/70 cursor-pointer" v-if="i !=active">
                            <div class="absolute bg-cover bg-center w-full h-full brightness-75 " :class="`${challenge.image}`"></div>
                            <div class="text-white z-10 p-3 space-y-2 text-description">
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
