<script setup>
import * as THREE from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader';
import { onMounted, ref, defineProps } from 'vue'

const props = defineProps({
    deviceType: {
        type: String,
        default: ''
    }
})

const { deviceType } = props

const canvas = ref(null)
const earth = ref(null)

onMounted(() => {
    const scene = new THREE.Scene();
    const rect = canvas.value.getBoundingClientRect();
    const size = {
        width: rect.width,
        height: rect.height,
    };

    const camera = new THREE.PerspectiveCamera(45, size.width / size.height, 0.1, 200);
    camera.position.set(-3, 3, 6)

    const renderer = new THREE.WebGLRenderer({
        antialias: true,
        alpha: true,
        canvas: canvas.value,
    });

    renderer.useLegacyLights = true
    renderer.outputEncoding = THREE.sRGBEncoding
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
    renderer.setSize(size.width, size.height)

    const lodingManager = new THREE.LoadingManager(
        () => {
            // earth.value.style.opacity = 1
        },
        (itemUrl, itemLoaded, itemTotal) => {
            // loaded.value = itemLoaded / itemTotal * 100
        }
    );

    const gltfLoader = new GLTFLoader(lodingManager);





    gltfLoader.load('/earth/scene.gltf', (gltf) => {
        if(deviceType === 'isMiniMobile') {
            gltf.scene.scale.set(2.1, 2.1, 2.1);
        }else if(deviceType === 'mobile'){
            gltf.scene.scale.set(2.4, 2.4, 2.4);

        }else if(deviceType === 'ipad'){
            gltf.scene.scale.set(2.5, 2.5, 2.5);
        } else {
            gltf.scene.scale.set(2.8, 2.8, 2.8);
        }
        scene.add(gltf.scene);
        window.addEventListener('resize', () => {
            const rect = earth.value.getBoundingClientRect();
            size.width = rect.width
            size.height = rect.height
            camera.aspect = size.width / size.height
            camera.updateProjectionMatrix()
            renderer.setSize(size.width, size.height)
            renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
        });
    });



    const control = new OrbitControls(camera, renderer.domElement);
    control.enableDamping = true;
    control.enableZoom = false;
    control.autoRotate = true;

    const animate = () => {
        requestAnimationFrame(animate);
        control.update();
        renderer.render(scene, camera);
    };

    animate();
})
</script>

<template>
    <div class="earth" ref="earth">
        <canvas ref="canvas" class="canvas"></canvas>
    </div>
</template>

<style scoped>
.earth {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
}

.canvas {
    width: 100%;
    height: 100%;
}
</style>