<script setup>
import { ref, defineProps, onMounted, onBeforeMount } from 'vue'
import VanillaTilt from 'vanilla-tilt'
import Earth from './Earth.vue'
import Star from './Star.vue'
import emailjs from '@emailjs/browser'

const prpos = defineProps({
    deviceType: {
        type: String,
        default: ''
    }
})

const { deviceType } = prpos

const iconSize = ref(0)

const brShow = ref(true)

const isRow = ref(true)



if (deviceType === 'isMiniMobile' || deviceType === 'mobile' || deviceType === 'miniIpad') {
    iconSize.value = 18
    brShow.value = false
    if (deviceType === 'miniIpad') {
        brShow.value = true
    }
    isRow.value = false
} else if (deviceType === 'ipad') {
    iconSize.value = 20
} else if (deviceType === 'ipadPro') {
    iconSize.value = 22
} else if (deviceType === 'pc') {
    iconSize.value = 24
}
const guideIcon = ref(null)
const guideBody = ref(null)
const contactName = ref(null)
const contactDetail = ref(null)
const contactCart = ref(null)
const earthContainer = ref(null)

const height = window.innerHeight
//监听页面滚动
window.addEventListener('scroll', () => {
    const scrollTop = document.documentElement.scrollTop
    if (iconSize.value != 18) {
        //输出滚动条滚动的距离
        if (scrollTop / height >= 5.0) {
            guideIcon.value.style.opacity = 1
            guideIcon.value.style.transform = 'scale(1)'
            guideBody.value.style.transform = 'scaleY(1)'
            contactName.value.style.opacity = 1
            contactName.value.style.transform = 'translateX(0)'
            contactDetail.value.style.opacity = 1
            contactDetail.value.style.transform = 'translateX(0)'
        } else {
            guideIcon.value.style.opacity = 0
            guideIcon.value.style.transform = 'scale(0.96)'
            guideBody.value.style.transform = 'scaleY(0)'
            contactName.value.style.opacity = 0
            contactName.value.style.transform = 'translateX(-15px)'
            contactDetail.value.style.opacity = 0
            contactDetail.value.style.transform = 'translateX(-15px)'
        }

        if (scrollTop / height >= 5.9) {
            contactCart.value.style.transform = 'translateX(0)'
            contactCart.value.style.opacity = 1
            earthContainer.value.style.transform = 'translateX(0)'
            earthContainer.value.style.opacity = 1
        } else {
            contactCart.value.style.transform = 'translateX(-150px)'
            contactCart.value.style.opacity = 0
            earthContainer.value.style.transform = 'translateX(150px)'
            earthContainer.value.style.opacity = 0
        }

    } else {
        if (scrollTop / height >= 3.65) {
            guideIcon.value.style.opacity = 1
            guideIcon.value.style.transform = 'scale(1)'
            guideBody.value.style.transform = 'scaleY(1)'
            contactName.value.style.opacity = 1
            contactName.value.style.transform = 'translateX(0)'
            contactDetail.value.style.opacity = 1
            contactDetail.value.style.transform = 'translateX(0)'
        } else {
            guideIcon.value.style.opacity = 0
            guideIcon.value.style.transform = 'scale(0.96)'
            guideBody.value.style.transform = 'scaleY(0)'
            contactName.value.style.opacity = 0
            contactName.value.style.transform = 'translateX(-15px)'
            contactDetail.value.style.opacity = 0
            contactDetail.value.style.transform = 'translateX(-15px)'
        }
    }
})

const formData = ref({
    name: '',
    email: '',
    message: ''
})

onMounted(() => {
    VanillaTilt.init(contactCart.value, {
        max: 2,
        speed: 400
    })
})

const isSending = ref(false)
const isSendEnd = ref(false)
const isSendTipEnd = ref(false)
const tipWord = ref('')
const isSendSuccess = ref(false)

const onSubmit = () => {
    isSendEnd.value = false
    isSendTipEnd.value = false
    isSending.value = true
    emailjs.send('service_36ikzx5', 'template_zcuqa09', { name: formData.value.name, email: formData.value.email, message: formData.value.message }, 'KnEe1raJLH7hPM-2n')
        .then(() => {
            isSendSuccess.value = true
            isSending.value = false
            isSendEnd.value = true
            tipWord.value = 'Send Successfully'
            setTimeout(() => {
                isSendTipEnd.value = true
            }, 2000)
        }, () => {
            isSendSuccess.value = false
            isSending.value = false
            isSendEnd.value = true
            tipWord.value = 'Send Failed'
            setTimeout(() => {
                isSendTipEnd.value = true
            }, 2000)
        });
}


</script>

<template>
    <div id="contact">
        <div class="contact-body">
            <div class="contact-body-left">
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
            <div class="contact-body-right">
                <h2 class="contact-name" ref="contactName">Contact</h2>
                <h3 class="contact-detail" ref="contactDetail">
                    <span style="color: var(--contact-main-color);">You can find me through the <br
                            v-if="brShow" />following contact
                        information.</span> Let's <br v-if="brShow" />study frontEnd technology together <br
                        v-if="brShow" /> and make progress together
                </h3>
            </div>
        </div>
        <Star :isRow="isRow" />
        <div class="contact-introduce">
            <div class="contact-introduce-body" ref="contactCart">
                <form class="contact-form" ref="contactForm" @submit.prevent="onSubmit">
                    <div class="contact-form-title">Contact Me</div>
                    <div class="contact-form-body">
                        <div class="contact-form-body-item">
                            <label for="name" class="contact-form-body-item-label">Your Name</label>
                            <input type="text" id="name" class="input" placeholder="What's your name"
                                v-model="formData.name" />
                        </div>
                        <div class="contact-form-body-item">
                            <label for="email" class="contact-form-body-item-label">Your Email</label>
                            <input type="email" id="email" class="input" placeholder="What's your email"
                                v-model="formData.email" />
                        </div>

                        <div class="contact-form-body-item">
                            <label for="message" class="contact-form-body-item-label">Your Message</label>
                            <textarea id="message" class="textarea" placeholder="What's your message"
                                v-model="formData.message"></textarea>
                        </div>
                    </div>
                    <div>
                        <button type="submit" class="contact-form-btn" v-if="!isSending">
                            <div>
                                Send
                            </div>
                        </button>
                        <button type="submit" class="contact-form-btn-loading" v-else disabled="true">
                            <div style="display: flex;align-items: center;gap: 0.5rem;">
                                Sending
                                <div class="loader"></div>
                            </div>
                        </button>
                    </div>
                </form>
            </div>
            <div class="earth-container" ref="earthContainer">
                <Earth :deviceType="deviceType" />
            </div>
        </div>
    </div>
    <div class="send-tip" :class="isSendEnd ? 'send-tip-show' : '', isSendTipEnd ? 'send-tip-hidden' : ''"  :style="{color: isSendSuccess ? '#fff':'#FA5151'}">
        {{ tipWord }}
    </div>
</template>

<style scoped>
#contact {
    width: 100%;
    display: flex;
    justify-content: center;
    flex-direction: column;
    position: relative;
}

.contact-body,
.contact-footer {
    width: 100%;
    padding: 0 var(--body-padding-left-right);
    display: flex;
    justify-content: flex-start;
    align-items: flex-start;
    gap: var(--body-gap);
    max-width: var(--max-width);
    margin: 0 auto;
}


.contact-body-left,
.contact-footer-left {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.contact-footer-left {
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
    box-shadow: var(--contact-guide-icon-shadow);
}

.guide-body {
    width: var(--guide-body-footer-width);
    height: var(--guide-body-height);
    background: var(--contact-guide-body-bg);
    transform: scaleY(0);
    transform-origin: center top;
    transition: transform .7s cubic-bezier(0.16, 1, 0.3, 1) .5s;
}

.contact-body-right {
    padding-top: var(--guide-icon-top-bottom)
}

.contact-name {
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

.contact-detail {
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

.contact-introduce {
    position: relative;
    width: var(--introduce-width);
    display: flex;
    max-width: var(--max-width);
    margin: 0 auto;
    flex-direction: var(--project-introduce-flex-derection);
    justify-content: center;
    align-items: center;
    gap: var(--project-introduce-gap);
    overflow: hidden;
}

.contact-introduce-body,
.earth-container {
    width: var(--contact-introduce-body-width);
    background-color: rgba(22, 27, 37, 0.5);
    border-radius: var(--introduce-border-radius);
    padding: var(--introduce-padding-top-bottom) var(--project-introduce-body-padding-left-right);
    overflow: hidden;
    border: 1px solid #30363d;
    transition: opacity 1s cubic-bezier(0.5, 1, 0.2, 1), transform 1s cubic-bezier(0.5, 1, 0.2, 1);
}

.earth-container {
    width: var(--earth-container-width);
    background-color: transparent;
    position: relative;
    padding: 0;
    border: none;
    border-radius: 0;
    height: var(--contact-introduce-body-height);
}

.contact-form {
    position: relative;
    color: #fff;
    display: flex;
    flex-direction: column;
    gap: var(--project-introduce-gap);
}

.contact-form-title {
    font-size: var(--introduce-title-font-size);
    line-height: var(--contact-form-title-line-height);
    font-weight: var(--introduce-title-font-weight);
}

.contact-form-body {
    display: flex;
    flex-direction: column;
    gap: calc(var(--project-introduce-gap) / 1.2);
}

.contact-form-body-item {
    display: flex;
    flex-direction: column;
    gap: calc(var(--project-introduce-gap) / 2.5);
}

.contact-form-body-item-label {
    font-size: var(--introduce-title-detail-font-size);
    line-height: var(--contact-form-label-line-height);
    font-weight: var(--introduce-title-detail-font-weight);
}

.input {
    font-family: "Poppins", sans-serif;
    outline: none;
    caret-color: #fff;
    background-color: rgba(31, 39, 45, 0.5);
    border: none;
    height: var(--input-height);
    border-radius: var(--input-border-radius);
    line-height: var(--contact-form-label-line-height);
    font-size: var(--input-font-size);
    color: #fff;
    padding: var(--input-padding-top-bottom) var(--input-padding-left-right);
}

.input::placeholder,
.textarea::placeholder {
    color: var(--introduce-title-detail-color);
    font-size: var(--input-font-size);
}

.textarea {
    outline: none;
    caret-color: #fff;
    background-color: rgba(31, 39, 45, 0.5);
    border: none;
    height: var(--textarea-height);
    border-radius: var(--input-border-radius);
    font-size: var(--input-font-size);
    color: #fff;
    padding: var(--input-padding-top-bottom) var(--input-padding-left-right);
    resize: none;
    box-sizing: content-box;
    letter-spacing: 0.5px;
    font-family: "Poppins", sans-serif;
}


.contact-form-btn,
.contact-form-btn-loading {
    background-color: rgba(31, 39, 45, 0.5);
    border: none;
    outline: none;
    border-radius: var(--input-border-radius);
    font-size: var(--introduce-title-detail-font-size);
    line-height: var(--contact-form-btn-line-height);
    font-weight: var(--introduce-title-detail-font-weight);
    padding: var(--contact-form-btn-padding-top-bottom) var(--contact-form-btn-padding-left-right);
    color: #fff;
    cursor: pointer;
    box-shadow: 0 4px 6px -1px rgba(13, 17, 23, 0.3), 0 2px 4px -2px rgba(13, 17, 23, 0.3);
    transition:
        transform 0.4s cubic-bezier(0, 0.85, 0.35, 1),
        background-color 0.5s cubic-bezier(0, 0.75, 0.25, 1);
}

.contact-form-btn-loading {
    cursor: wait;
}

.contact-form-btn:active {
    transform: scale(0.95);
    background-color: #353a40;
}

.loader {
    display: inline-block;
    border: 3px solid rgba(255, 144, 181, 0.2);
    border-top-color: var(--contact-main-color);
    border-radius: 50%;
    width: var(--introduce-title-detail-font-size);
    height: var(--introduce-title-detail-font-size);
    animation: spin 1s linear infinite;
}

@keyframes spin {
    to {
        transform: rotate(360deg);
    }
}

.send-tip {
    position: fixed;
    left: 50%;
    top: calc(var(--nav-height) + 3rem);
    background-color: rgb(46, 46, 46);
    z-index: 999;
    transform: translate(-50%, -50%) translateY(-10rem);
    opacity: 0;
    padding: 0.5rem 1.5rem;
    border-radius: var(--send-tip-border-radius);
    font-size: var(--send-tip-font-size);
    transition: all 1s cubic-bezier(0.16, 1, 0.3, 1);
}

.send-tip-show {
    transform: translate(-50%, -50%) translateY(0);
    opacity: 1;
}

.send-tip-hidden {
    opacity: 0;
}
</style>