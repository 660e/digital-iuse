<script setup lang="ts">
import * as THREE from 'three';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';

const scene = new THREE.Scene();
scene.add(new THREE.GridHelper(100, 10));

const camera = new THREE.PerspectiveCamera();
camera.aspect = window.innerWidth / window.innerHeight;
camera.updateProjectionMatrix();
camera.position.set(100, 100, 100);

const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);

const orbitControls = new OrbitControls(camera, renderer.domElement);
const animate = () => {
  orbitControls.update();
  renderer.render(scene, camera);
};
renderer.setAnimationLoop(animate);

const bodyRef = ref();
onMounted(() => {
  bodyRef.value.appendChild(renderer.domElement);
});
</script>

<template>
  <div ref="bodyRef">
    <div class="fixed right-2 bottom-2 text-xs leading-none">v{{ THREE.REVISION }}</div>
  </div>
</template>
