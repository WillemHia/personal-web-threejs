<script setup>
import * as THREE from 'three';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader';
import { onMounted, ref, defineProps } from 'vue';

const computer = ref(null);
const prpos = defineProps({
    deviceType: {
        type: String,
        default: ''
    }
})

const { deviceType } = prpos

const strategy = [
    [(deviceType) => { return deviceType === 'isMiniMobile' }, (obj) => { obj.scale.set(0.60, 0.60, 0.60); obj.position.set(0, -3.7, -1.5); }],
    [(deviceType) => { return deviceType === 'mobile' }, (obj) => { obj.scale.set(0.7, 0.7, 0.7); obj.position.set(0, -3.25, -1.5); }],
    [(deviceType) => { return deviceType === 'miniIpad' }, (obj) => { obj.scale.set(0.8, 0.8, 0.8); obj.position.set(0, -3.25, -1.5); }],
    [(deviceType) => { return deviceType === 'ipad' }, (obj) => { obj.scale.set(0.65, 0.65, 0.65); obj.position.set(0, -3.25, -1.5); pointLight.position.set(0, -0.5, 0); }],
    [(deviceType) => { return deviceType === 'ipadPro' }, (obj) => { obj.scale.set(0.72, 0.72, 0.72); obj.position.set(0, -3.25, -1.5); pointLight.position.set(0, -0.4, 0); }],
    [(deviceType) => { return deviceType === 'pc' }, (obj) => { obj.scale.set(0.75, 0.75, 0.75); obj.position.set(0, -3.25, -1.5); }]
]

const loaded = ref(0);

const scene = new THREE.Scene();

const size = {
    width: window.innerWidth,
    height: deviceType === 'mobile' || deviceType === 'isMiniMobile' || deviceType === 'miniIpad' ? window.innerHeight / 2.5 : window.innerHeight,
};

const camera = new THREE.PerspectiveCamera(25, size.width / size.height, 0.1, 1000);
camera.position.set(20, 3, 5)

const renderer = new THREE.WebGLRenderer({
    antialias: true,
    alpha: true,
});

renderer.useLegacyLights = true
renderer.outputEncoding = THREE.sRGBEncoding
renderer.shadowMap.enabled = true
renderer.shadowMap.type = THREE.PCFSoftShadowMap
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
renderer.setSize(size.width, size.height)



//给物体添加阴影效果
const updateAllmaterials = () => {
    scene.traverse((child) => {
        if (child instanceof THREE.Mesh && child.material instanceof THREE.MeshStandardMaterial) {
            child.material.needsUpdate = true
            child.castShadow = true
            child.receiveShadow = true
        }
    })
}

const lodingManager = new THREE.LoadingManager(
    () => {
        computer.value.style.opacity = 1
    },
    (itemUrl, itemLoaded, itemTotal) => {
        loaded.value = itemLoaded / itemTotal * 100
    }
);

const gltfLoader = new GLTFLoader(lodingManager);

const hemiLight = new THREE.HemisphereLight(0xffffff, 0x000000, 0.15);
scene.add(hemiLight)

const pointLight = new THREE.PointLight();
scene.add(pointLight);

const spotLight = new THREE.SpotLight(0xffffff, 1);
spotLight.position.set(-20, 50, 10);
spotLight.angle = 0.12;
spotLight.penumbra = 1;
spotLight.castShadow = true;
spotLight.shadow.mapSize.width = 1024;
spotLight.shadow.mapSize.height = 1024;
spotLight.shadow.camera.near = 0.5;
spotLight.shadow.camera.far = 500;
spotLight.shadow.camera.fov = 30;
scene.add(spotLight);

gltfLoader.load('/desktop_pc/scene.gltf', (gltf) => {
    strategy.forEach((item) => {
        if (item[0](deviceType)) {
            item[1](gltf.scene)
        }
    })
    gltf.scene.rotation.set(-0.01, -0.2, -0.1)
    scene.add(gltf.scene);
    updateAllmaterials();
    window.addEventListener('resize', () => {
        size.width = window.innerWidth
        if (window.innerWidth <= 350) {
            gltf.scene.scale.set(0.6, 0.6, 0.6)
            gltf.scene.position.set(0, -3.7, -1.5)
        } else if (window.innerWidth <= 540) {
            gltf.scene.scale.set(0.7, 0.7, 0.7)
        }
        else if (window.innerWidth <= 768) {
            gltf.scene.scale.set(0.75, 0.75, 0.75)
        } else if (window.innerWidth <= 1024) {
            gltf.scene.scale.set(0.65, 0.65, 0.65)
        } else if (window.innerWidth <= 1366) {
            gltf.scene.scale.set(0.7, 0.7, 0.7)
        } else {
            gltf.scene.scale.set(0.75, 0.75, 0.75)
        }
        camera.aspect = size.width / size.height
        camera.updateProjectionMatrix()
        renderer.setSize(size.width, size.height)
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
    });
});



const control = new OrbitControls(camera, renderer.domElement);
control.enableDamping = true;
control.enableZoom = false;
control.maxPolarAngle = Math.PI / 2;
control.minPolarAngle = Math.PI / 2;


const animate = () => {
    requestAnimationFrame(animate);
    control.update();
    renderer.render(scene, camera);
};



onMounted(() => {
    animate();
    computer.value.appendChild(renderer.domElement);
});



</script>

<template>
    <div class="computer-container" ref="computer"></div>
    <div class="load-container" :class="loaded === 100 ? 'load-hidden' : ''">
        <div class="loader">
            <div class="orbe" style="--index: 0"></div>
            <div class="orbe" style="--index: 1"></div>
            <div class="orbe" style="--index: 2"></div>
            <div class="orbe" style="--index: 3"></div>
            <div class="orbe" style="--index: 4"></div>
        </div>
        <div class="loaded">
            {{ loaded.toFixed(2) }}%
        </div>
    </div>
</template>


<style scoped>
.computer-container {
    position: absolute;
    top: 0;
    left: 0;
    opacity: 0;
    transition: opacity 1s ease-out 0.3s;
}

.load-container {
    position: absolute;
    bottom: var(--load-container-bottom);
    display: flex;
    align-items: center;
    flex-direction: column;
    gap: var(--load-contianer-gap);
    color: var(--home-main-color);
    transition: opacity 0.3s ease-out;
}

.load-hidden {
    opacity: 0;
}

.loader {
    color: #fff;
    width: var(--size-loader);
    height: var(--size-loader);
    position: relative;
    transform: rotate(45deg);
}

.orbe {
    position: absolute;
    width: 100%;
    height: 100%;
    --delay: calc(var(--index) * 0.1s);
    animation: orbit ease-in-out 1.5s var(--delay) infinite;
    opacity: calc(1 - calc(0.2 * var(--index)));
}

.orbe::after {
    position: absolute;
    content: '';
    top: 0;
    left: 0;
    width: var(--size-orbe);
    height: var(--size-orbe);
    background-color: var(--home-minor-color);
    box-shadow: 0 0 10px 2px var(--home-minor-color);
    border-radius: 50%;
}

.loaded {
    font-size: var(--loaded-font-size);
}

@keyframes orbit {
    0% {}

    80% {
        transform: rotate(360deg);
    }

    100% {
        transform: rotate(360deg);
    }
}
</style>