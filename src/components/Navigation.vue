<script setup>
import { defineProps, ref } from 'vue';

const props = defineProps({
    deviceType: {
        type: String,
        default: ''
    }
})

const { deviceType } = props

const isPhone = ref(false)

const aboutActive = ref(0)
const projectActive = ref(0)
const contactActive = ref(0)

if (deviceType === 'isMiniMobile' || deviceType === 'mobile' || deviceType === 'miniIpad') {
    isPhone.value = true
}

const height = window.innerHeight
//监听页面滚动
window.addEventListener('scroll', () => {
    const scrollTop = document.documentElement.scrollTop
    if (!isPhone.value) {
        //输出滚动条滚动的距离
        if (scrollTop / height >= 5.0) {
            aboutActive.value = 0
            projectActive.value = 0
            contactActive.value = 1
        } else if (scrollTop / height >= 3.40) {
            aboutActive.value = 0
            projectActive.value = 1
            contactActive.value = 0
        } else if (scrollTop / height >= 0.43) {
            aboutActive.value = 1
            projectActive.value = 0
            contactActive.value = 0
        } else {
            aboutActive.value = 0
            projectActive.value = 0
            contactActive.value = 0
        }

    } else {
        if (scrollTop / height >= 3.65) {
            aboutActive.value = 0
            projectActive.value = 0
            contactActive.value = 1
        } else if (scrollTop / height >=  1.75) {
            aboutActive.value = 0
            projectActive.value = 1
            contactActive.value = 0
        } else if (scrollTop / height >=  0.4) {
            aboutActive.value = 1
            projectActive.value = 0
            contactActive.value = 0
        } else {
            aboutActive.value = 0
            projectActive.value = 0
            contactActive.value = 0
        }
    }
})

</script>

<template>
    <nav class="nav-container">
        <div class="nav-body">
            <div class="nav-body-left">
                <img src="../assets/logo.svg" class="logo" />
                <p class="name">Adny&nbsp;Will</p>
            </div>
            <div class="nav-body-right">
                <ul>
                    <li><a href="#edu"
                            :style="{ '--about-scale': aboutActive, '--about-delay': (aboutActive ? '.2s' : ''), '--about-color': (aboutActive ? '#fff' : ' var(--nav-li-a-color)') }">About</a>
                    </li>
                    <li><a href="#project"
                            :style="{ '--project-scale': projectActive, '--project-delay': (projectActive ? '.2s' : ''), '--project-color': (projectActive ? '#fff' : ' var(--nav-li-a-color)') }">Projects</a>
                    </li>
                    <li><a href="#contact"
                            :style="{ '--contact-scale': contactActive, '--contact-delay': (contactActive ? '.2s' : ''), '--contact-color': (contactActive ? '#fff' : ' var(--nav-li-a-color)') }">Contact</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>

<style scoped>
.nav-container {
    position: fixed;
    display: flex;
    align-items: center;
    top: 0;
    left: 0;
    width: 100%;
    height: var(--nav-height);
    padding: var(--nav-padding-top-bottom) var(--nav-padding-left-right);
    background-color: var(--default-backgroud);
    z-index: 999;
}

.nav-body {
    width: 100%;
    max-width: var(--max-width);
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.nav-body-left {
    display: flex;
    align-items: center;
}

.logo {
    width: var(--nav-logo-size);
    height: var(--nav-logo-size);
}

.name {
    font-size: var(--nav-name-li-font-size);
    font-weight: var(--nav-name-font-weight);
    color: #fff;
}

.nav-body-right {
    display: flex;
    align-items: center;
}

.nav-body-right ul {
    display: flex;
    align-items: center;
    gap: var(--nav-ul-gap);
    list-style: none;
}

.nav-body-right ul li {
    font-size: var(--nav-name-li-font-size);
    font-weight: var(--nav-li-font-weight);
    cursor: pointer;
    user-select: none;
}

.nav-body-right ul li a {
    position: relative;
    text-decoration: none;
    padding: var(--nav-a-padding-top-bottom) 0;
}

.nav-body-right ul li:nth-child(1) a {
    color: var(--about-color);
}

.nav-body-right ul li:nth-child(2) a {
    color: var(--project-color);
}

.nav-body-right ul li:nth-child(3) a {
    color: var(--contact-color);
}


.nav-body-right ul li a::after {
    position: absolute;
    bottom: 0;
    left: 15%;
    width: 70%;
    height: 1px;
    content: "";
    background-color: #fff;
    transition: transform .25s ease-in-out;
}

.nav-body-right ul li:nth-child(1) a::after {
    transform: scale(var(--about-scale));
    transition-delay: var(--about-delay);
}

.nav-body-right ul li:nth-child(2) a::after {
    transform: scale(var(--project-scale));
    transition-delay: var(--project-delay);
}


.nav-body-right ul li:nth-child(3) a::after {
    transform: scale(var(--contact-scale));
    transition-delay: var(--contact-delay);
}

.nav-body-right ul li a:hover {
    color: var(--nav-li-a-hover-color);
}

.nav-body-right ul li a:hover::after {
    transform: scale(1);
}
</style>