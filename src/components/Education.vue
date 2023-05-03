<script setup>
import { ref, defineProps, onMounted } from 'vue'
import VanillaTilt from 'vanilla-tilt'

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
const eduName = ref(null)
const eduDetail = ref(null)
const eduCart = ref(null)
const eduBackgroud = ref(null)
const guideFooter = ref(null)
const eduLeft = ref(null)

const height = window.innerHeight
//监听页面滚动
window.addEventListener('scroll', () => {
    const scrollTop = document.documentElement.scrollTop
    if (iconSize.value != 18) {
        //输出滚动条滚动的距离
        if (scrollTop / height >= 0.43) {
            guideIcon.value.style.opacity = 1
            guideIcon.value.style.transform = 'scale(1)'
            guideBody.value.style.transform = 'scaleY(1)'
            eduName.value.style.opacity = 1
            eduName.value.style.transform = 'translateX(0)'
            eduDetail.value.style.opacity = 1
            eduDetail.value.style.transform = 'translateX(0)'
        } else {
            guideIcon.value.style.opacity = 0
            guideIcon.value.style.transform = 'scale(0.96)'
            guideBody.value.style.transform = 'scaleY(0)'
            eduName.value.style.opacity = 0
            eduName.value.style.transform = 'translateX(-15px)'
            eduDetail.value.style.opacity = 0
            eduDetail.value.style.transform = 'translateX(-15px)'
        }

        if(scrollTop / height >= 1.6){
            guideFooter.value.style.transform = 'scaleY(1)'
        }else{
            guideFooter.value.style.transform = 'scaleY(0)'
        }

    }else{
        if(scrollTop / height >= 0.65){
            guideFooter.value.style.transform = 'scaleY(1)'
        }else{
            guideFooter.value.style.transform = 'scaleY(0)'
        }
    }
})


onMounted(() => {
    if (iconSize.value === 18) {
        setTimeout(() => {
            guideIcon.value.style.opacity = 1
            guideIcon.value.style.transform = 'scale(1)'
            guideBody.value.style.transform = 'scaleY(1)'
            eduName.value.style.opacity = 1
            eduName.value.style.transform = 'translateX(0)'
            eduDetail.value.style.opacity = 1
            eduDetail.value.style.transform = 'translateX(0)'
        }, 1500)
    }
    VanillaTilt.init(eduCart.value, {
        max: 2,
        speed: 400
    })
})

const onMouseEnter = () => {
    eduBackgroud.value.style.opacity = 0.85
}

const onMouseMove = (e) => {

    const rect = eduCart.value.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;


    const width = eduBackgroud.value.offsetWidth
    const height = eduBackgroud.value.offsetHeight
    eduBackgroud.value.style.transform = `translateX(${x - width / 2}px) translateY(${y - height / 2}px)`

}

const onMouseLeave = () => {
    eduBackgroud.value.style.opacity = 0
}


</script>

<template>
    <div id="edu">
        <div class="edu-body">
            <div class="edu-body-left">
                <div class="guide-icon" ref="guideIcon">
                    <svg t="1682155654527" class="icon" viewBox="0 0 1092 1024" version="1.1"
                        xmlns="http://www.w3.org/2000/svg" p-id="7551" :width="iconSize" :height="iconSize">
                        <path
                            d="M542.624 10.66666667a31.99999969 31.99999969 0 0 1 31.99999969 31.99999969v93.44000062c2.33599969 1.08799969 4.608 2.33599969 6.816 3.71199938l4.86400031 3.29600062 244.704 180.73599938a41.79199969 41.79199969 0 0 1-20.57599969 75.20000062l-4.25600062 0.192h-13.56799969l-0.03199969 53.21599969H1023.99999969a31.99999969 31.99999969 0 0 1 31.776 28.28800031l0.22400062 3.71199938a31.99999969 31.99999969 0 0 1-28.25600062 31.776l-3.744 0.22400062h-26.784v418.62399938a31.99999969 31.99999969 0 0 1-31.99999969 32.00000062H126.39999969a31.99999969 31.99999969 0 0 1-31.776-28.28800031l-0.22399969-3.71200031-0.03199969-418.62399938H63.99999969a31.99999969 31.99999969 0 0 1-31.776-28.25600062L32 484.45866636a31.99999969 31.99999969 0 0 1 28.25599969-31.776L63.99999969 452.45866667h239.232v-53.21599969H288.96000031a41.79199969 41.79199969 0 0 1-28.76800031-72.096l3.48799969-2.94400031 237.24800062-180.48a71.35999969 71.35999969 0 0 1 9.696-6.20800031V74.66666698H384.00000031a31.99999969 31.99999969 0 0 1 0-64.00000031h158.62399969z m390.59200031 505.79200031h-140.64v386.592h140.64V516.49066667z m-629.98400062 0H158.336l0.03199969 386.62399969 144.864-0.03199969V516.45866698z m238.08-322.752l-1.632 0.96-189.63199969 144.22399969a31.99999969 31.99999969 0 0 1 16.96000031 24.31999969l0.22399969 4.032v535.84000031l64.76800031-0.03199969v-145.344l0.25599938-6.24c3.84-57.984 52.8-103.07200031 111.744-103.07200031 61.69600031 0 112.00000031 49.27999969 112.00000031 110.36800031v144.288h72.60799969V367.27466698c0-10.49599969 5.05600031-19.84000031 12.89600062-25.66400062l3.072-2.016-196.28800031-144.96a7.2 7.2 0 0 0-6.97600031-0.89599969zM543.99999969 712.42666667c-25.47199969 0-46.30399969 19.2-47.83999969 42.24l-0.16000031 4.128v144.31999969h96v-144.31999969c0-25.47199969-21.34399969-46.39999969-48-46.39999969z m-63.99999938-220.73599969h127.99999969a31.99999969 31.99999969 0 0 1 3.744 63.77599969L608 555.62666698h-127.99999969a31.99999969 31.99999969 0 0 1-3.744-63.80800031l3.744-0.192h127.99999969-127.99999969z m127.99999969-137.15200031a31.99999969 31.99999969 0 0 1 3.744 63.77599969l-3.744 0.22400062h-127.99999969a31.99999969 31.99999969 0 0 1-3.744-63.77600062l3.744-0.22399969h127.99999969z"
                            fill="#ffffff" p-id="7552"></path>
                    </svg>
                    <div class="guide-icon-shadow"></div>
                </div>
                <div class="guide-body" ref="guideBody"></div>
            </div>
            <div class="edu-body-right">
                <h2 class="edu-name" ref="eduName">Education</h2>
                <h3 class="edu-detail" ref="eduDetail">
                    <span style="color: var(--edu-main-color);">I am an undergraduate student of <br v-if="brShow" />Shanghai Polytechnic
                        University.</span> <br v-if="brShow" />My major is intelligent science and technology.
                </h3>
            </div>
        </div>
        <div class="edu-introduce" ref="eduCart" @mousemove="onMouseMove" @mouseenter="onMouseEnter"
            @mouseleave="onMouseLeave">
            <div class="edu-introduce-left">
                <h3 class="award">Award</h3>
                <ul class="award-detail">
                    <li>2021-2022 Second Class Scholarship of Shanghai Polytechnic University</li>
                    <li>2020-2021 Third Class Scholarship of Shanghai Polytechnic University</li>
                    <li>2020-2021 Outstanding Students of Shanghai Polytechnic University</li>
                </ul>
            </div>
            <div class="edu-introduce-right">
                <img src="../assets/school.jpg" class="edu-introduce-img" />
            </div>
            <div class="edu-backgroud" ref="eduBackgroud"></div>
        </div>
        <div class="edu-footer">
            <div class="edu-footer-left">
                <div class="guide-footer" ref="guideFooter"></div>
            </div>
        </div>
    </div>
</template>

<style scoped>
#edu {
    width: 100%;
    display: flex;
    justify-content: center;
    flex-direction: column;
}

.edu-body,.edu-footer {
    width: 100%;
    padding: 0 var(--body-padding-left-right);
    display: flex;
    justify-content: flex-start;
    align-items: flex-start;
    gap: var(--body-gap);
    max-width: var(--max-width);
    margin: 0 auto;
}


.edu-body-left, .edu-footer-left {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.edu-footer-left{
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
    box-shadow: var(--edu-guide-icon-shadow);
}

.guide-body {
    width: var(--guide-body-footer-width);
    height: var(--guide-body-height);
    background: var(--edu-guide-body-bg);
    transform: scaleY(0);
    transform-origin: center top;
    transition: transform .7s cubic-bezier(0.16, 1, 0.3, 1) .5s;
}

.edu-body-right {
    padding-top: var(--guide-icon-top-bottom)
}

.edu-name {
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

.edu-detail {
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

.edu-introduce {
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
    flex-direction: var(--edu-introduce-flex-derection);
}

.edu-backgroud {
    width: var(--cart-background-size);
    height: var(--cart-background-size);
    position: absolute;
    top: 0;
    left: 0;
    border-radius: var(--cart-background-border-radius);
    opacity: 0;
    filter: blur(var(--cart-background-filter));
    background-color: var(--edu-main-color);
    transition: opacity 1.2s cubic-bezier(0.16, 1, 0.3, 1);
    mix-blend-mode: soft-light;
    will-change: transform;
    z-index: 0;
}

.edu-introduce-left {
    width: var(--edu-introduce-left-width);
    display: flex;
    flex-direction: column;
    padding: var(--edu-introduce-left-padding) 0;
    z-index: 1;
}

.award {
    font-size: var(--introduce-title-font-size);
    line-height: var(--introduce-title-line-height);
    font-weight: var(--introduce-title-font-weight);
    margin-top: var(--edu-award-margin-top);
    color: #fff;
}

.award-detail {
    margin-top: var(--edu-award-detail-margin-top);
    font-size: var(--introduce-title-detail-font-size);
    font-weight: var(--introduce-title-detail-font-weight);
    color: var(--introduce-title-detail-color);
    list-style: none;
}

.award-detail li {
    margin: var(--edu-award-detail-li-margin-top-bottom) 0;
    line-height: var(--edu-award-detail-li-line-height);
}

.edu-introduce-right {
    width: var(--edu-introduce-right-width);
    display: flex;
    padding: var(--introduce-padding-top-bottom) var(--edu-introduce-right-padding-left);
    padding-right: var(--edu-introduce-right-padding-right);
    z-index: 1;
}

.edu-introduce-img {
    min-height: var(--edu-introduce-img-min-height);
    width: 100%;
    border-radius: 0.25rem;
    border: 1px solid #30363d
}

.guide-footer{
    width: var(--guide-body-footer-width);
    height: var(--guide-footer-height);
    background: var(--edu-guide-footer-bg);
    transform: scaleY(0);
    transform-origin: center top;
    transition: transform .7s cubic-bezier(0.16, 1, 0.3, 1);
}
</style>