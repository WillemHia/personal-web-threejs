<script setup>
import Navigation from './components/Navigation.vue';
import Home from './components/Home.vue';
import Education from './components/Education.vue';
import Skill from './components/Skill.vue';
import MyProject from './components/MyProject.vue';
import Contact from './components/Contact.vue';
import Footer from './components/Footer.vue';

const isMiniMobile = window.matchMedia("(min-width:0px)" && "(max-width: 350px)").matches

const isMobile = window.matchMedia("(min-with:351px)"&&"(max-width: 540px)").matches

const isMiniIpad = window.matchMedia("(min-width:541px)" &&"(max-width: 768px)").matches

const isIpad = window.matchMedia("(min-width:769px)" && "(max-width: 1024px)").matches

const isIpadPro = window.matchMedia("(min-width:1025px)" && "(max-width: 1366px)").matches

let deviceType = ''

if (isMiniMobile) {
  deviceType = 'isMiniMobile'
}else if(isMobile){
  deviceType = 'mobile'
} else if (isMiniIpad) {
  deviceType = 'miniIpad'
} else if (isIpad) {
  deviceType = 'ipad'
} else if (isIpadPro) {
  deviceType = 'ipadPro'
} else {
  deviceType = 'pc'
}



</script>

<template>
  <Navigation :deviceType="deviceType"/>
  <Home :deviceType="deviceType"/>
  <Education :deviceType="deviceType"/>
  <Skill :deviceType="deviceType"/>
  <MyProject :deviceType="deviceType"/>
  <Contact :deviceType="deviceType"/>
  <Footer />
</template>

<style scoped>
</style>
