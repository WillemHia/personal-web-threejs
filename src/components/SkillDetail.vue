<script setup>
import { defineProps, ref } from 'vue'

const prpos = defineProps({
    skill: {
        type: Object,
        default: {}
    },
    iconSize: {
        type: Number,
        default: 0
    }
})

const { skill, iconSize } = prpos

const skillHave = ref(null)
const skillProficiency = ref(null)

const height = window.innerHeight
//监听页面滚动
window.addEventListener('scroll', (e) => {
    const scrollTop = document.documentElement.scrollTop
    if (iconSize != 18) {
        //输出滚动条滚动的距离
        if (scrollTop / height >= 2.6) {
            skillProficiency.value.style.opacity = 1
            skillProficiency.value.style.transform = 'scale(1)'
            skillHave.value.style.transform = 'scaleX(1)'
        } else {
            skillProficiency.value.style.opacity = 0
            skillProficiency.value.style.transform = 'scale(0.96)'
            skillHave.value.style.transform = 'scaleX(0)'
        }

    } else {
        if (scrollTop / height >= 1.2) {
            skillProficiency.value.style.opacity = 1
            skillProficiency.value.style.transform = 'scale(1)'
            skillHave.value.style.transform = 'scaleX(1)'
        } else {
            skillProficiency.value.style.opacity = 0
            skillProficiency.value.style.transform = 'scale(0.96)'
            skillHave.value.style.transform = 'scaleX(0)'
        }
    }
})


</script>

<template>
    <div class="skill-item">
        <img :src="skill.src" class="skill-item-img" :style="{ transform: skill.name === 'VUE' ? 'scale(0.8)' : '' }">
        <div class="skill-item-body">
            <div style="width: 100%;display: flex;align-items: center;justify-content: space-between;">
                <div class="skill-item-title">{{ skill.name }}</div>
                <div class="skill-item-title skill-proficiency" ref="skillProficiency">{{ skill.proficiency }}</div>
            </div>
            <div class="skill-item-baisc"></div>
            <div class="skill-item-have" :style="{ width: skill.proficiency }" ref="skillHave"></div>
        </div>
    </div>
</template>

<style scoped>
.skill-item {
    display: flex;
    justify-content: flex-start;
    position: relative;
    width: 100%;
    gap: var(--skill-item-gap);
}

.skill-item-img {
    width: var(--skill-item-img-size);
    height: var(--skill-item-img-size);
}

.skill-item-body {
    display: flex;
    flex-direction: column;
    position: absolute;
    left: calc(var(--skill-item-img-size) + var(--skill-item-gap));
    width: calc(100% - var(--skill-item-img-size) - var(--skill-item-gap));
}

.skill-item-title {
    font-size: var(--skill-item-title-font-size);
    font-weight: var(--skill-item-title-font-weight);
    color: var(--skill-item-title-color);
    margin-bottom: var(--skill-item-title-margin-bottom);
}

.skill-proficiency{
    opacity: 0;
    transform: scale(0.96);
    transition: opacity .7s cubic-bezier(0.16, 1, 0.3, 1), transform .7s cubic-bezier(0.16, 1, 0.3, 1);
    transition-delay: .5s;
}

.skill-item-baisc {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: var(--skill-item-body-height);
    border-radius: var(--skill-item-body-border-radius);
    background-color: rgba(182, 110, 92, 0.5);
}

.skill-item-have {
    position: absolute;
    bottom: 0;
    border-radius: var(--skill-item-body-border-radius);
    height: var(--skill-item-body-height);
    background-color: rgb(255, 139, 109);
    transform: scaleX(0);
    transform-origin: left center;
    transition: transform .7s cubic-bezier(0.16, 1, 0.3, 1);
}</style>