<script lang="ts"  setup>
import  { computed, watchEffect, onMounted, ref } from 'vue';
import gsap from 'gsap';

interface Props {
  transparent?: boolean;
  theme?: 'light' | 'dark';
}

const navOpen = ref(false);

const props = withDefaults(defineProps<Props>(),{
  transparent: false,
  theme: 'dark'
})

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


const tl = gsap.timeline({ defaults: { duration: 1, ease: 'expo.inOut' } });


function handleNav(isOpen: boolean){
  navOpen.value = isOpen;
  console.log(tl)
  if(isOpen){
    if(tl.reversed()){
      tl.play()
    }else{
      tl
      .set(".large-nav",{zIndex:100})
      .to('.large-nav',{right:0})
      .to(".large-nav",{height:'100vh'},'-=.1')
      // .to(".nav", {display:'none'}, '-=.1')
      .from([".large-nav .logo", ".large-nav .close"],{opacity:0,x:-10},'-=.8')
      .from(".large-nav .link-text",{opacity:0,y:10,stagger:.2},'-=1')
      
    }
    console.log("opening");
    
  }else{
    console.log('reversing');
    
    tl.reverse()
  } 
}
const classes = computed(() => {
  let _classes = '';

  switch(props.theme){
    case 'dark':
      _classes += ' text-black';
      break;
    case 'light':
      _classes += ' text-white';
      break;
  }


  return _classes;
})

</script>
<template>
    <div  class="navbar flex flex-col  w-[100%] h-full z-50" :class="`${classes}`">
      <nav class="flex justify-between items-center py-10 px-40 ">
        <div class="logo text-xl font-bold uppercase py-[10px] px-12">
          <span>Brainy Bunch</span>
        </div>
        <div class="search text-xl font-bold uppercase">
          <span><ion-icon name="search" ></ion-icon></span>
          <span class="cursor-pointer p-4" @click="handleNav(true)"> <ion-icon name="menu" class=" " ></ion-icon> </span>
          
        </div>
      </nav>
      <div class="large-nav backdrop-blur-sm m-auto h-[2rem] text-white  w-full absolute bg-black/90 right-[-200vw] top-[50%] translate-y-[-50%]">
        <div class="div w-full flex justify-between py-4">
          <div class="logo text-xl font-bold uppercase py-[10px] px-12">
            <span>Brainy Bunch</span>
          </div>
          <div>
            <span class="close" @click="handleNav(false)"><ion-icon name="add-outline" class="text-white rotate-45 px-4 text-4xl cursor-pointer font-bold" ></ion-icon></span>
          </div>
        </div>
        <div class="flex flex-col justify-center h-full">
          <ul >
          <li class="text-center text-5xl py-4 uppercase font-semibold cursor-pointer link-text"><router-link  to="/">Home</router-link></li>
          <li class="text-center text-5xl py-4 uppercase font-semibold cursor-pointer link-text"><router-link  to="/about">About</router-link></li>
          <li class="text-center text-5xl py-4 uppercase font-semibold cursor-pointer link-text"><router-link  to="/challenges">Challenges</router-link></li>
        </ul>
        </div>
      </div>
    </div>
</template>
<style>

.large-nav ul li a{
	color: #fafafa;
}


.large-nav ul li a::after{
	content: '';
	width: 100%;
	position: absolute;
	height: 30px;
	border-radius: 5px;
	background: #fff;
	bottom: -10px;
	left: 0;
	transform-origin: left;
	transition: transform .5s ease;
	transform: scaleX(0);
}

.large-nav ul li a::hover::after{
	transform: scaleX(1);
}

</style>