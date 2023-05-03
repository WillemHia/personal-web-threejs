<script setup>
import Computer from './Computer.vue';
import { defineProps, ref, onMounted } from 'vue';

const prpos = defineProps({
    deviceType: {
        type: String,
        default: ''
    }
})

const { deviceType } = prpos

const homeName = ref(null)
const homeIntroduce = ref(null)
const guideHeader = ref(null)
const guideBody = ref(null)
const guideIcon = ref(null)
const guideFooter = ref(null)

let iconSize = 0

if (deviceType === 'isMiniMobile' || deviceType === 'mobile' || deviceType === 'miniIpad') {
    iconSize = 18
} else if (deviceType === 'ipad') {
    iconSize = 20
} else if (deviceType === 'ipadPro') {
    iconSize = 22
} else if (deviceType === 'pc') {
    iconSize = 24
}

onMounted(() => {
    setTimeout(() => {
        guideHeader.value.style.opacity = 1
        guideHeader.value.style.transform = 'scale(1)'
        guideBody.value.style.opacity = 1
        guideBody.value.style.transform = 'scaleY(1)'
        homeName.value.style.opacity = 1
        homeName.value.style.transform = 'translateX(0)'
        homeIntroduce.value.style.opacity = 1
        homeIntroduce.value.style.transform = 'translateX(0)'
        guideIcon.value.style.opacity = 1
        guideIcon.value.style.transform = 'scale(1)'
        guideFooter.value.style.opacity = 1
        guideFooter.value.style.transform = 'scaleY(1)'
    }, 0)
})
</script>

<template>
    <div class="home">
        <div class="home-body">
            <div class="home-body-left">
                <div class="guide-header" ref="guideHeader"></div>
                <div class="guide-body" ref="guideBody"></div>
                <div class="guide-icon" ref="guideIcon">
                    <svg t="1682132247089" class="icon" viewBox="0 0 1024 1024" version="1.1"
                        xmlns="http://www.w3.org/2000/svg" p-id="3845" data-spm-anchor-id="a313x.7781069.0.i11"
                        :width="iconSize" :height="iconSize">
                        <path
                            d="M810.551167 57.547768H213.847946C127.696233 57.547768 57.568888 127.674115 57.568888 213.827826v369.388137c0 86.209692 70.127346 156.280058 156.279058 156.280058h127.355226c-3.466781 45.518997-18.355547 118.090484-75.354508 146.618454a42.604022 42.604022 0 0 0 19.037307 80.69763h454.630169a42.585029 42.585029 0 0 0 19.037308-80.69763c-57.395822-28.698911-72.057667-101.154438-75.473467-146.618454h127.471186c86.209692 0 156.280058-70.070366 156.280058-156.280058V213.827826c0-86.152712-70.069366-156.280058-156.280058-156.280058z m-422.521457 824.020306c27.845211-48.645898 36.426194-103.996439 38.757374-142.072053h170.826944c2.330181 38.075614 10.969144 93.426155 38.814354 142.072053z m493.558483-298.352111a71.062017 71.062017 0 0 1-71.037026 71.037026H213.847946a71.098005 71.098005 0 0 1-71.032028-71.037026V213.827826a71.134992 71.134992 0 0 1 71.036026-71.037026h596.699223a71.099004 71.099004 0 0 1 71.037026 71.037026z"
                            p-id="3846" data-spm-anchor-id="a313x.7781069.0.i10" class="" fill="#ffffff"></path>
                    </svg>
                    <div class="guide-icon-shadow"></div>
                </div>
                <div class="guide-footer" ref="guideFooter"></div>
            </div>
            <div>
                <h1 class="home-name" ref="homeName">Hi I'm<span style="color: #7d58bc;"> Andy Will</span></h1>
                <p class="home-introduce" ref="homeIntroduce">
                    I'm a Frontend developer,
                    <br />
                    this is my personal website.
                </p>
            </div>
        </div>
        <Computer :deviceType="deviceType" />
    </div>
</template>

<style scoped>
.home {
    position: relative;
    width: 100%;
    height: var(--home-height);
    margin-top: var(--home-margin-top);
    display: flex;
    justify-content: center;
}

.home-body {
    position: absolute;
    width: 100%;
    top: var(--home-body-top);
    user-select: none;
    padding: 0 var(--body-padding-left-right);
    display: flex;
    justify-content: flex-start;
    gap: var(--body-gap);
    max-width: var(--max-width);
    margin: 0 auto;
}

.home-body-left {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: var(--home-body-margin-top);
}

.guide-header {
    width: var(--home-guide-header-size);
    height: var(--home-guide-header-size);
    border-radius: 50%;
    background-color: var(--home-main-color);
    opacity: 0;
    transform: scale(0.96);
    transition: opacity .7s cubic-bezier(0.16, 1, 0.3, 1), transform .7s cubic-bezier(0.16, 1, 0.3, 1);
}

.guide-body {
    width: var(--guide-body-footer-width);
    height: var(--home-guide-body-height);
    background: var(--home-guide-body-bg);
    transform: scaleY(0);
    transform-origin: center top;
    transition: transform .7s cubic-bezier(0.16, 1, 0.3, 1) .5s;
}


.guide-icon {
    width: var(--guide-icon-size);
    height: var(--guide-icon-size);
    margin: var(--guide-icon-top-bottom) 0rem;
    position: relative;
    opacity: 0;
    transform: scale(0.96);
    transition: opacity .7s cubic-bezier(0.16, 1, 0.3, 1), transform .7s cubic-bezier(0.16, 1, 0.3, 1);
    transition-delay: 0.8s;
}

.guide-icon-shadow {
    position: absolute;
    top: 50%;
    left: 50%;
    box-shadow: var(--home-guide-icon-shadow);
}

.guide-footer {
    width: var(--guide-body-footer-width);
    height: var(--home-guide-footer-height);
    background: var(--home-guide-footer-bg);
    transform: scaleY(0);
    transform-origin: center top;
    transition: transform .7s cubic-bezier(0.16, 1, 0.3, 1) 1.3s;
}

.home-name {
    color: #fff;
    margin-top: var(--home-name-margin-top);
    font-size: var(--home-name-font-size);
    font-weight: var(--home-name-font-weight);
    opacity: 0;
    transform: translateX(-15px);
    transition: opacity .6s cubic-bezier(0.16, 1, 0.3, 1), transform .6s cubic-bezier(0.16, 1, 0.3, 1);
    transition-delay: 0.2s;
}

.home-introduce {
    color: rgb(243, 243, 243);
    font-size: var( --home-introduce-font-size);
    line-height: var(--home-introduce-line-height);
    font-weight: var(--home-introduce-font-weight);
    margin-top: var(--home-introduce-margin-top);
    color: #fff;
    opacity: 0;
    transform: translateX(-15px);
    transition: opacity .6s cubic-bezier(0.16, 1, 0.3, 1), transform .6s cubic-bezier(0.16, 1, 0.3, 1);
    transition-delay: 0.3s;
}
</style>