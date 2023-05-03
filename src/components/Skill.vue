<script setup>
import { defineProps, ref, onMounted } from 'vue'
import HTML from '../assets/skill/html.png'
import CSS from '../assets/skill/css.png'
import JS from '../assets/skill/javascript.png'
import TS from '../assets/skill/typescript.png'
import VUE from '../assets/vue.svg'
import THREEJS from '../assets/skill/threejs.svg'
import GIT from '../assets/skill/git.png'
import SkillDetail from './SkillDetail.vue'

const prpos = defineProps({
    deviceType: {
        type: String,
        default: ''
    }
})

const { deviceType } = prpos

const iconSize = ref(0)

const brShow = ref(true)

if (deviceType === 'isMiniMobile' || deviceType === 'mobile' || deviceType === 'miniIpad') {
    iconSize.value = 18
    brShow.value = false
    if (deviceType === 'miniIpad') {
        brShow.value = true
    }
} else if (deviceType === 'ipad') {
    iconSize.value = 20
} else if (deviceType === 'ipadPro') {
    iconSize.value = 22
} else if (deviceType === 'pc') {
    iconSize.value = 24
}

const imgs = [{
    name: 'HTML',
    src: HTML,
    proficiency: '85%'
}, {
    name: 'CSS',
    src: CSS,
    proficiency: '75%'
}, {
    name: 'JS',
    src: JS,
    proficiency: '70%'
}, {
    name: 'TS',
    src: TS,
    proficiency: '50%'
}, {
    name: 'VUE',
    src: VUE,
    proficiency: '80%'
}, {
    name: 'THREEJS',
    src: THREEJS,
    proficiency: '40%'
}, {
    name: 'GIT',
    src: GIT,
    proficiency: '30%'
}]


const guideIcon = ref(null)
const guideBody = ref(null)
const skillName = ref(null)
const skillDetail = ref(null)
const skillCart = ref(null)
const skillBackgroud = ref(null)
const guideFooter = ref(null)

const height = window.innerHeight
//监听页面滚动
window.addEventListener('scroll', (e) => {
    const scrollTop = document.documentElement.scrollTop
    if (iconSize.value != 18) {
        //输出滚动条滚动的距离
        if (scrollTop / height >= 1.85) {
            guideIcon.value.style.opacity = 1
            guideIcon.value.style.transform = 'scale(1)'
            guideBody.value.style.transform = 'scaleY(1)'
            skillName.value.style.opacity = 1
            skillName.value.style.transform = 'translateX(0)'
            skillDetail.value.style.opacity = 1
            skillDetail.value.style.transform = 'translateX(0)'
        } else {
            guideIcon.value.style.opacity = 0
            guideIcon.value.style.transform = 'scale(0.96)'
            guideBody.value.style.transform = 'scaleY(0)'
            skillName.value.style.opacity = 0
            skillName.value.style.transform = 'translateX(-15px)'
            skillDetail.value.style.opacity = 0
            skillDetail.value.style.transform = 'translateX(-15px)'
        }
        if(scrollTop / height >= 3.1){
            guideFooter.value.style.transform = 'scaleY(1)'
        }else{
            guideFooter.value.style.transform = 'scaleY(0)'
        }
    } else {
        if (scrollTop / height >= 0.85) {
            guideIcon.value.style.opacity = 1
            guideIcon.value.style.transform = 'scale(1)'
            guideBody.value.style.transform = 'scaleY(1)'
            skillName.value.style.opacity = 1
            skillName.value.style.transform = 'translateX(0)'
            skillDetail.value.style.opacity = 1
            skillDetail.value.style.transform = 'translateX(0)'
        } else {
            guideIcon.value.style.opacity = 0
            guideIcon.value.style.transform = 'scale(0.96)'
            guideBody.value.style.transform = 'scaleY(0)'
            skillName.value.style.opacity = 0
            skillName.value.style.transform = 'translateX(-15px)'
            skillDetail.value.style.opacity = 0
            skillDetail.value.style.transform = 'translateX(-15px)'
        }

        if(scrollTop / height >= 1.75){
            guideFooter.value.style.transform = 'scaleY(1)'
        }else{
            guideFooter.value.style.transform = 'scaleY(0)'
        }
    }
})

const onMouseEnter = () => {
    skillBackgroud.value.style.opacity = 0.85
}

const onMouseMove = (e) => {

    const rect = skillCart.value.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;


    const width = skillBackgroud.value.offsetWidth
    const height = skillBackgroud.value.offsetHeight
    skillBackgroud.value.style.transform = `translateX(${x - width / 2}px) translateY(${y - height / 2}px)`

}

const onMouseLeave = () => {
    skillBackgroud.value.style.opacity = 0
}

onMounted(() => {
    VanillaTilt.init(skillCart.value, {
        max: 2,
        speed: 400
    })
})
</script>

<template>
    <div class="skill">
        <div class="skill-body">
            <div class="skill-body-left">
                <div class="guide-icon" ref="guideIcon">
                    <svg t="1682510533302" class="icon" viewBox="0 0 1024 1024" version="1.1"
                        xmlns="http://www.w3.org/2000/svg" p-id="4670" :width="iconSize" :height="iconSize">
                        <path
                            d="M351.056457 649.479314v-185.782857l160.914286-92.949943 160.914286 92.949943v185.782857l-160.914286 92.949943z"
                            fill="#ffffff" p-id="4671"></path>
                        <path
                            d="M511.941486 0l-109.597257 59.567543v119.105828l85.079771 46.197029v102.1952h49.122743V224.841143l85.021257-46.197029V59.538286z m-60.445257 151.990857V86.2208l60.445257-32.885029 60.503771 32.885029v65.770057l-60.503771 32.885029z m259.247542 539.092114l94.032458 51.082972v92.423314l109.597257 59.567543L1024 834.589257v-119.105828l-109.626514-59.567543L829.352229 702.171429l-94.090972-51.141486z m143.008915 116.765258v-65.711543l60.503771-32.885029 60.562286 32.885029v65.711543l-60.562286 32.885028z m-183.178972-602.697143l-24.517485 13.370514 245.321142 133.295543v263.021714l22.879086-12.463543 26.331429 14.248229v-291.313372l-269.867886-146.724571v26.565486zM109.597257 602.580114l22.9376 12.463543v-263.050971l245.321143-133.295543-24.634514-13.312v-26.770286l-269.780115 146.666057v291.459657l26.126629-14.248228z m402.344229 368.0256L268.317257 838.217143v23.083886l-27.882057 15.125942 271.506286 147.543772 271.594057-147.543772-27.882057-15.125942v-23.083886l-243.682743 132.359314zM194.647771 702.171429l-85.079771-46.197029-109.597257 59.509029v119.105828l109.597257 59.567543 109.626514-59.567543v-92.511086l94.032457-51.112228-24.576-40.023772z m-145.6128 105.6768v-65.828572l60.503772-32.885028 60.503771 32.885028v65.828572l-60.503771 32.885028-60.503772-32.885028z"
                            fill="#ffffff" p-id="4672"></path>
                    </svg>
                    <div class="guide-icon-shadow"></div>
                </div>
                <div class="guide-body" ref="guideBody"></div>
            </div>
            <div class="skill-body-right">
                <h2 class="skill-name" ref="skillName">Professional Skill</h2>
                <h3 class="skill-detail" ref="skillDetail">
                    <span style="color: var(--skill-main-color);">I love to learn professional skills </span> <br v-if="brShow" /> and
                    improve my abilities through <br v-if="brShow" /> continuous learning .
                    The following<br v-if="brShow" /> are the frontEnd skills I have mastered
                </h3>
            </div>
        </div>
        <div class="skill-introduce" ref="skillCart" @mousemove="onMouseMove" @mouseenter="onMouseEnter"
            @mouseleave="onMouseLeave">
            <div class="skill-introduce-body">
                <SkillDetail v-for="(item, index) in imgs" :key="index" :skill="item" :index="index" :iconSize="iconSize" />
            </div>
            <div class="skill-backgroud" ref="skillBackgroud"></div>
        </div>
        <div class="skill-footer">
            <div class="skill-footer-left">
                <div class="guide-footer" ref="guideFooter"></div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.skill {
    width: 100%;
    display: flex;
    justify-content: center;
    flex-direction: column;
}

.skill-body,
.skill-items,
.skill-footer {
    width: 100%;
    padding: 0 var(--body-padding-left-right);
    display: flex;
    justify-content: flex-start;
    align-items: flex-start;
    gap: var(--body-gap);
    max-width: var(--max-width);
    margin: 0 auto;
}

.skill-items {
    flex-wrap: wrap;
    justify-content: center;
}


.skill-body-left,
.skill-footer-left {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.skill-footer-left {
    width: var(--guide-icon-size);
}

.guide-icon {
    width: var(--guide-icon-size);
    height: var(--guide-icon-size);
    margin: var(--guide-icon-top-bottom) 0rem;
    position: relative;
    opacity: 0;
    transform: scale(0.96);
    transition: opacity .7s cubic-bezier(0.16, 1, 0.3, 1), transform .7s cubic-bezier(0.16, 1, 0.3, 1);
}

.guide-icon-shadow {
    position: absolute;
    top: 50%;
    left: 50%;
    box-shadow: var(--skill-guide-icon-shadow);
}

.guide-body {
    width: var(--guide-body-footer-width);
    height: var(--guide-body-height);
    background: var(--skill-guide-body-bg);
    transform: scaleY(0);
    transform-origin: center top;
    transition: transform .7s cubic-bezier(0.16, 1, 0.3, 1) .5s;
}

.skill-body-right {
    padding-top: var(--guide-icon-top-bottom)
}

.skill-name {
    color: #fff;
    font-size: var(--title-font-size);
    font-weight: var(--title-font-weight);
    line-height: var(--title-line-height);
    opacity: 0;
    transform: translateX(-15px);
    transition: opacity .6s cubic-bezier(0.16, 1, 0.3, 1), transform .6s cubic-bezier(0.16, 1, 0.3, 1);
    transition-delay: 0.2s;
    user-select: none;
}

.skill-detail {
    margin-top: var(--detail-margin-top);
    font-size: var(--detail-font-size);
    line-height: var(--detail-line-height);
    font-weight: var(--detail-font-weight);
    color: #fff;
    user-select: none;
    opacity: 0;
    transform: translateX(-15px);
    transition: opacity .6s cubic-bezier(0.16, 1, 0.3, 1), transform .6s cubic-bezier(0.16, 1, 0.3, 1);
    transition-delay: 0.3s;
}

.skill-introduce {
    position: relative;
    width: var(--introduce-width);
    background-color: #161b22;
    padding: 0 var(--body-padding-left-right);
    display: flex;
    max-width: var(--max-width);
    margin: 0 auto;
    border-radius: var(--introduce-border-radius);
    overflow: hidden;
    border: 1px solid #30363d;
}

.skill-backgroud {
    width: var(--cart-background-size);
    height: var(--cart-background-size);
    position: absolute;
    top: 0;
    left: 0;
    border-radius: var(--cart-background-border-radius);
    opacity: 0;
    filter: blur(var(--cart-background-filter));
    background-color: var(--skill-main-color);
    transition: opacity 1.2s cubic-bezier(0.16, 1, 0.3, 1);
    mix-blend-mode: soft-light;
    z-index: 0;
}

.skill-introduce-body {
    width: 100%;
    padding: var(--skill-introduce-body-padding-top-bottom) var(--skill-introduce-body-padding-left-right);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    gap: var(--skill-introduce-body-gap);
    position: relative;
    z-index: 1;
}
.guide-footer{
    width: var(--guide-body-footer-width);
    height: var(--guide-footer-height);
    background: var(--skill-guide-footer-bg);
    transform: scaleY(0);
    transform-origin: center top;
    transition: transform .7s cubic-bezier(0.16, 1, 0.3, 1);
}
</style>