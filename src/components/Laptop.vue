<template>
  <div ref="threeContainer"></div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";
import * as THREE from "three";
import { GLTFLoader } from "three/addons/loaders/GLTFLoader.js";

// Ref untuk div kontainer Three.js
const threeContainer = ref<HTMLElement | null>(null);

onMounted(() => {
  // Membuat scene, kamera, dan renderer
  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(75, 500 / 300, 0.1, 500);

  const renderer = new THREE.WebGLRenderer();
  renderer.setSize(500, 300);

  // Attach the renderer to the div element controlled by Vue
  if (threeContainer.value) {
    threeContainer.value.appendChild(renderer.domElement);
  }

  // Mengatur posisi kamera
  camera.position.z = 2.5;

  // Menambahkan pencahayaan
  const light = new THREE.AmbientLight(0x404040); // Cahaya ambient
  scene.add(light);

  const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
  directionalLight.position.set(1, 1, 1).normalize();
  scene.add(directionalLight);

  // Memuat model GLTF
  const loader = new GLTFLoader();
  let modelGroup: THREE.Group | null = null; // Menyimpan grup model

  loader.load(
    "/laptop.gltf", // Path model GLTF
    (gltf) => {
      modelGroup = new THREE.Group(); // Membuat grup baru
      const model = gltf.scene;
      model.scale.set(2, 2, 2); // Memperbesar model
      modelGroup.add(model); // Menambahkan model ke grup

      // Menyesuaikan posisi model agar pivot berada di pusat grup
      model.position.set(-1, -1, -1); // Posisikan model di pusat grup (ubah jika diperlukan)

      scene.add(modelGroup); // Tambahkan grup ke scene
    },
    undefined,
    (error) => {
      console.error("An error occurred while loading the model", error);
    }
  );

  // Fungsi animasi
  function animate() {
    requestAnimationFrame(animate);

    // Jika modelGroup sudah dimuat, putar modelGroup
    if (modelGroup) {
      modelGroup.rotation.y += 0.01; // Putar grup setiap frame
    }

    // Render scene dan kamera
    renderer.render(scene, camera);
  }

  animate();
});
</script>
