<script setup>
import { defineProps, ref, onMounted } from 'vue'
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

const guideIcon = ref(null)
const guideBody = ref(null)
const projectName = ref(null)
const projectDetail = ref(null)
const projectLeftCart = ref(null)
const projectRightCart = ref(null)
const projectLeftBackgroud = ref(null)
const projectRightBackgroud = ref(null)
const guideFooter = ref(null)

const height = window.innerHeight
//监听页面滚动
window.addEventListener('scroll', () => {
    const scrollTop = document.documentElement.scrollTop
    if (iconSize.value != 18) {
        //输出滚动条滚动的距离
        if (scrollTop / height >= 3.40) {
            guideIcon.value.style.opacity = 1
            guideIcon.value.style.transform = 'scale(1)'
            guideBody.value.style.transform = 'scaleY(1)'
            projectName.value.style.opacity = 1
            projectName.value.style.transform = 'translateX(0)'
            projectDetail.value.style.opacity = 1
            projectDetail.value.style.transform = 'translateX(0)'
        } else {
            guideIcon.value.style.opacity = 0
            guideIcon.value.style.transform = 'scale(0.96)'
            guideBody.value.style.transform = 'scaleY(0)'
            projectName.value.style.opacity = 0
            projectName.value.style.transform = 'translateX(-15px)'
            projectDetail.value.style.opacity = 0
            projectDetail.value.style.transform = 'translateX(-15px)'
        }
        if(scrollTop / height >= 4.75){
            guideFooter.value.style.transform = 'scaleY(1)'
        }else{
            guideFooter.value.style.transform = 'scaleY(0)'
        }
    } else {
        if (scrollTop / height >= 1.75) {
            guideIcon.value.style.opacity = 1
            guideIcon.value.style.transform = 'scale(1)'
            guideBody.value.style.transform = 'scaleY(1)'
            projectName.value.style.opacity = 1
            projectName.value.style.transform = 'translateX(0)'
            projectDetail.value.style.opacity = 1
            projectDetail.value.style.transform = 'translateX(0)'
        } else {
            guideIcon.value.style.opacity = 0
            guideIcon.value.style.transform = 'scale(0.96)'
            guideBody.value.style.transform = 'scaleY(0)'
            projectName.value.style.opacity = 0
            projectName.value.style.transform = 'translateX(-15px)'
            projectDetail.value.style.opacity = 0
            projectDetail.value.style.transform = 'translateX(-15px)'
        }

        if(scrollTop / height >= 3.45){
            guideFooter.value.style.transform = 'scaleY(1)'
        }else{
            guideFooter.value.style.transform = 'scaleY(0)'
        }
    }
})

const leftMouseEnter = () => {
    projectLeftBackgroud.value.style.opacity = 0.85
}


const leftMouseMove = (e) => {
    const rectLeft = projectLeftCart.value.getBoundingClientRect();

    const x = e.clientX - rectLeft.left;
    const y = e.clientY - rectLeft.top;


    const width = projectLeftBackgroud.value.offsetWidth
    const height = projectLeftBackgroud.value.offsetHeight
    projectLeftBackgroud.value.style.transform = `translateX(${x - width / 2}px) translateY(${y - height / 2}px)`
}

const leftMouseLeave = () => {
    projectLeftBackgroud.value.style.opacity = 0
}

const rightMouseEnter = () => {
    projectRightBackgroud.value.style.opacity = 0.85
}


const rightMouseMove = (e) => {
    const rectLeft = projectRightCart.value.getBoundingClientRect();

    const x = e.clientX - rectLeft.left;
    const y = e.clientY - rectLeft.top;


    const width = projectRightBackgroud.value.offsetWidth
    const height = projectRightBackgroud.value.offsetHeight
    projectRightBackgroud.value.style.transform = `translateX(${x - width / 2}px) translateY(${y - height / 2}px)`
}

const rightMouseLeave = () => {
    projectRightBackgroud.value.style.opacity = 0
}

onMounted(() => {
    VanillaTilt.init([projectLeftCart.value, projectRightCart.value], {
        max: 2,
        speed: 400
    })
})
</script>

<template>
    <div id="project">
        <div class="project-body">
            <div class="project-body-left">
                <div class="guide-icon" ref="guideIcon">
                    <svg t="1682513310368" class="icon" viewBox="0 0 1024 1024" version="1.1"
                        xmlns="http://www.w3.org/2000/svg" p-id="5595" :width="iconSize" :height="iconSize">
                        <path
                            d="M392.966 140.089l-262.292 0 0 262.292c0 52.672 42.706 95.378 95.379 95.378l262.292 0 0-262.291c0-52.685-42.707-95.379-95.379-95.379zM428.734 366.613l0 71.534-190.759 0c-26.335 0-47.689-21.353-47.689-47.701 0-4.133 0-11.91 0-11.91l0-178.835 190.758 0c26.337 0 47.69 21.341 47.69 47.69 0 0 0 74.385 0 119.222zM798.327 545.45l-262.292 0 0 262.29c0 52.674 42.706 95.379 95.378 95.379l262.292 0 0-262.292c0.001-52.683-42.707-95.377-95.378-95.377zM834.093 783.895l0 59.613-190.758 0c-26.337 0-47.69-21.352-47.69-47.69 0 0 0-127.537 0-131.146l0-59.612 190.758 0c26.337 0 47.69 21.352 47.69 47.69 0 4.133 0 131.145 0 131.145zM631.413 140.089c-52.673 0-95.378 42.694-95.378 95.379l0 262.291 262.291 0c52.673 0 95.379-42.707 95.379-95.378l0-262.292-262.292 0zM834.093 283.158c0 0 0 103.156 0 107.29 0 26.348-21.352 47.701-47.69 47.701l-190.758 0 0-71.534c0-44.837 0-119.223 0-119.223 0-26.349 21.352-47.69 47.69-47.69l190.758 0 0 83.457zM130.675 640.827l0 262.292 262.292 0c52.673 0 95.379-42.706 95.379-95.379l0-262.29-262.292 0c-52.674 0-95.379 42.694-95.379 95.377zM428.734 605.06c0 0 0 67.298 0 71.534 0 44.826 0 119.223 0 119.223 0 26.337-21.352 47.69-47.69 47.69l-190.758 0 0-59.613c0 0 0-127.012 0-131.145 0-26.337 21.354-47.69 47.689-47.69l190.759 0z"
                            fill="#ffffff" p-id="5596" data-spm-anchor-id="a313x.7781069.0.i0" class="selected"></path>
                    </svg>
                    <div class="guide-icon-shadow"></div>
                </div>
                <div class="guide-body" ref="guideBody"></div>
            </div>
            <div class="project-body-right">
                <h2 class="project-name" ref="projectName">Projects</h2>
                <h3 class="project-detail" ref="projectDetail">
                    <span style="color: var(--project-main-color);">Practice is the sole criterion for <br v-if="brShow" /> testing truth.
                    </span>
                    The following are some <br v-if="brShow" />specific actual combat projects that I <br
                        v-if="brShow" />personally did
                </h3>
            </div>
        </div>
        <div class="project-introduce">
            <div class="project-introduce-body" ref="projectLeftCart" @mousemove="leftMouseMove"
                @mouseenter="leftMouseEnter" @mouseleave="leftMouseLeave">
                <div class="project-introduce-body-top">
                    <div>
                        <h3 class="project-item-name">System</h3>
                        <div class="project-item-detail">
                            This is a restaurant management system, including data visualization, real-time data monitoring,
                            customer management, menu management, etc.
                        </div>
                    </div>

                    <div>
                        <a class="go-github" href="https://github.com/WillemHia">GO TO GITHUB
                            <svg xmlns="http://www.w3.org/2000/svg" class="go-icon" width="16" height="16"
                                viewBox="0 0 16 16" fill="none">
                                <path fill="currentColor"
                                    d="M7.28033 3.21967C6.98744 2.92678 6.51256 2.92678 6.21967 3.21967C5.92678 3.51256 5.92678 3.98744 6.21967 4.28033L7.28033 3.21967ZM11 8L11.5303 8.53033C11.8232 8.23744 11.8232 7.76256 11.5303 7.46967L11 8ZM6.21967 11.7197C5.92678 12.0126 5.92678 12.4874 6.21967 12.7803C6.51256 13.0732 6.98744 13.0732 7.28033 12.7803L6.21967 11.7197ZM6.21967 4.28033L10.4697 8.53033L11.5303 7.46967L7.28033 3.21967L6.21967 4.28033ZM10.4697 7.46967L6.21967 11.7197L7.28033 12.7803L11.5303 8.53033L10.4697 7.46967Z">
                                </path>
                                <path class="go-icon-line" stroke="currentColor" d="M1.75 8H11" stroke-width="1.5"
                                    stroke-linecap="round"></path>
                            </svg>
                        </a>
                    </div>
                </div>
                <div class="project-introduce-body-bottom">
                    <img src="../assets/project1.png" class="project-img"/>
                </div>

                <div class="project-backgroud" ref="projectLeftBackgroud"></div>
            </div>
            <div class="project-introduce-body" ref="projectRightCart" @mousemove="rightMouseMove"
                @mouseenter="rightMouseEnter" @mouseleave="rightMouseLeave">
                <div class="project-introduce-body-top">
                    <div>
                        <h3 class="project-item-name">Component</h3>
                        <div class="project-item-detail">
                            This is a frontEnd validation component. Encapsulation based on three.js. The principle is to use the movement of the mouse to change the position of the letters.
                        </div>
                    </div>

                    <div>
                        <a class="go-github" href="https://github.com/WillemHia">GO TO GITHUB
                            <svg xmlns="http://www.w3.org/2000/svg" class="go-icon" width="16" height="16"
                                viewBox="0 0 16 16" fill="none">
                                <path fill="currentColor"
                                    d="M7.28033 3.21967C6.98744 2.92678 6.51256 2.92678 6.21967 3.21967C5.92678 3.51256 5.92678 3.98744 6.21967 4.28033L7.28033 3.21967ZM11 8L11.5303 8.53033C11.8232 8.23744 11.8232 7.76256 11.5303 7.46967L11 8ZM6.21967 11.7197C5.92678 12.0126 5.92678 12.4874 6.21967 12.7803C6.51256 13.0732 6.98744 13.0732 7.28033 12.7803L6.21967 11.7197ZM6.21967 4.28033L10.4697 8.53033L11.5303 7.46967L7.28033 3.21967L6.21967 4.28033ZM10.4697 7.46967L6.21967 11.7197L7.28033 12.7803L11.5303 8.53033L10.4697 7.46967Z">
                                </path>
                                <path class="go-icon-line" stroke="currentColor" d="M1.75 8H11" stroke-width="1.5"
                                    stroke-linecap="round"></path>
                            </svg>
                        </a>
                    </div>
                </div>
                <div class="project-introduce-body-bottom">
                    <img src="../assets/project2.png" class="project-img"/>
                </div>
                <div class="project-backgroud" ref="projectRightBackgroud"></div>
            </div>
        </div>
        <div class="project-footer">
            <div class="project-footer-left">
                <div class="guide-footer" ref="guideFooter"></div>
            </div>
        </div>
    </div>
</template>

<style scoped>
#project {
    width: 100%;
    display: flex;
    justify-content: center;
    flex-direction: column;
}

.project-body,
.project-footer {
    width: 100%;
    padding: 0 var(--body-padding-left-right);
    display: flex;
    justify-content: flex-start;
    align-items: flex-start;
    gap: var(--body-gap);
    max-width: var(--max-width);
    margin: 0 auto;
}


.project-body-left,
.project-footer-left {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.project-footer-left {
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
    box-shadow: var(--project-guide-icon-shadow);
}

.guide-body {
    width: var(--guide-body-footer-width);
    height: var(--guide-body-height);
    background: var(--project-guide-body-bg);
    transform: scaleY(0);
    transform-origin: center top;
    transition: transform .7s cubic-bezier(0.16, 1, 0.3, 1) .5s;
}

.project-body-right {
    padding-top: var(--guide-icon-top-bottom)
}

.project-name {
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

.project-detail {
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

.project-introduce {
    position: relative;
    width: var(--introduce-width);
    display: flex;
    max-width: var(--max-width);
    margin: 0 auto;
    flex-direction: var(--project-introduce-flex-derection);
    justify-content: center;
    align-items: center;
    gap: var(--project-introduce-gap);
}

.project-introduce-body {
    width: var(--project-introduce-body-width);
    background-color: #161b22;
    border-radius: var(--introduce-border-radius);
    padding: var(--introduce-padding-top-bottom) var(--project-introduce-body-padding-left-right);
    overflow: hidden;
    border: 1px solid #30363d;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: var(--project-introduce-gap);
    z-index: 1;
}

.project-introduce-body-top {
    width: 100%;
    display: flex;
    flex-direction: column;
}

.project-item-name {
    font-size: var(--introduce-title-font-size);
    line-height: var(--introduce-title-line-height);
    font-weight: var(--introduce-title-font-weight);
    color: #fff;
}

.project-item-detail {
    height: var(--project-item-detail-height);
    margin-top: var(--project-item-detail-margin-top);
    font-size: var(--introduce-title-detail-font-size);
    font-weight: var(--introduce-title-detail-font-weight);
    color: var(--introduce-title-detail-color);
    line-height: var(--project-item-line-height);
}

.project-img{
    width: 100%;
    border-radius: var(--introduce-border-radius);
}

.go-github {
    position: relative;
    display: inline-block;
    font-size: var(--introduce-title-detail-font-size);
    font-weight: var(--introduce-title-font-weight);
    line-height: var(--edu-award-detail-li-line-height);
    color: #fff;
    cursor: pointer;
    padding: 0.25rem 0;
    text-decoration: none;
}

.go-github::after {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 0.125rem;
    border-radius: 1px;
    pointer-events: none;
    background-color: #fff;
    content: "";
    transform: scaleX(0);
    transform-origin: 0 0;
    transition: transform .3s ease;
}

.go-github:hover::after {
    transform: scaleX(1);
}

.go-icon {
    position: absolute;
    top: 50%;
    width: 1.25rem;
    height: 1.25rem;
    margin-left: 0.25rem;
    display: inline-block;
    overflow: visible;
    transform: translateX(0) translateY(-50%);
    transition: transform .2s linear;
}

.go-github:hover .go-icon {
    transform: translateX(4px) translateY(-50%);
}
.go-icon-line {
    stroke-dasharray: 10;
    stroke-dashoffset: 10;
    transition: stroke-dashoffset .2s linear;
}

.go-github:hover .go-icon-line {
    stroke-dashoffset: 20;
}

.project-backgroud {
    width: calc(var(--cart-background-size) / 1.3);
    height: calc(var(--cart-background-size) / 1.3);
    position: absolute;
    top: 0;
    left: 0;
    border-radius: calc(var(--cart-background-border-radius) / 1.3);
    opacity: 0;
    filter: blur(calc(var(--cart-background-filter) / 1.3));
    background-color: var(--project-main-color);
    transition: opacity 1.2s cubic-bezier(0.16, 1, 0.3, 1);
    mix-blend-mode: soft-light;
    will-change: transform;
    z-index: -1;
}

.guide-footer {
    width: var(--guide-body-footer-width);
    height: var(--guide-footer-height);
    background: var(--project-guide-footer-bg);
    transform: scaleY(0);
    transform-origin: center top;
    transition: transform .7s cubic-bezier(0.16, 1, 0.3, 1);
}
</style>