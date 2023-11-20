<script lang="ts"  setup>
import  { computed, onMounted } from 'vue';
import gsap from 'gsap';

interface Props {
  transparent?: boolean;
  theme?: 'light' | 'dark';
}


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
    <div class="navbar flex justify-between items-center w-[80%] my-10 mx-40 z-[1]" :class="`${classes}`">
      <div class="logo text-xl font-bold uppercase py-[10px] px-12">
        <span>Brainy Bunch</span>
      </div>
      <div class="search text-xl space-x-4 font-bold uppercase">
        <ion-icon name="search"></ion-icon>
        <ion-icon name="menu"></ion-icon>
      </div>
    </div>
</template>