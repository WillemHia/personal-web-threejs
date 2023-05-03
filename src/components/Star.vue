<script setup>
import { ref, onMounted, defineProps } from 'vue';
import * as THREE from 'three';

const props = defineProps({
    isRow: {
        type: Boolean,
        default: false
    }
})

const { isRow } = props

const star = ref(null)
onMounted(() => {
    const scene = new THREE.Scene();
    const rect = star.value.getBoundingClientRect();
    const size = {
        width: rect.width,
        height: rect.height,
    };

    const camera = new THREE.PerspectiveCamera(75, size.width / size.height, 0.1, 1000);
    camera.position.z = 5;

    const renderer = new THREE.WebGLRenderer({
        antialias: true,
        alpha: true,
    });

    renderer.setSize(size.width, size.height);
    star.value.appendChild(renderer.domElement);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))

    const textureLoader = new THREE.TextureLoader();
    const starTexture = textureLoader.load('/star/star.png');

    const positions = new Float32Array(1000 * 3);

    for (let i = 0; i < 1000; i++) {
        positions[i * 3 + 0] = (Math.random() - 0.5) * 10;
        positions[i * 3 + 1] = (Math.random() - 0.7) * 10;
        positions[i * 3 + 2] = (Math.random() - 0.5) * 10;
    }

    const geometry = new THREE.BufferGeometry();
    geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));

    const material = new THREE.PointsMaterial({
        size: 0.1,
        alphaMap: starTexture,
        transparent: true,
        blending: THREE.AdditiveBlending,
        depthWrite: false,
    });

    const points = new THREE.Points(geometry, material);
    scene.add(points);

    const animate = function () {
        requestAnimationFrame(animate);

        points.rotation.y += 0.001;

        renderer.render(scene, camera);
    };

    animate();
})
</script>

<template>
    <div class="star-container" ref="star" :class="isRow ? '' : 'star-container-phone'"></div>
</template>

<style scoped>
.star-container {
    position: absolute;
    top: calc(var(--guide-body-height));
    left: 0;
    height: calc(var(--contact-introduce-body-height) + var(--guide-icon-all-height) * 2);
    width: 100%;
}

.star-container-phone {
    height: calc(var(--contact-introduce-body-height) * 2 + var(--guide-icon-all-height) * 2);
}
</style>