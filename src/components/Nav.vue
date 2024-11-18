<template>
  <header class="flex flex-col text-white py-4">
    <h1 class="text-3xl bg-black z-10">Mahendra Khamal Akbar</h1>
    <div class="relative">
      <div class="flex items-center gap-3">
        <p ref="currentText" class="text-xl"></p>
      </div>
    </div>
  </header>
</template>

<script setup lang="ts">
import gsap from "gsap";
import { onMounted, ref } from "vue";

const data = [
  "Front End Dev",
  "Just A Person",
  "Web Dev",
  "Mobile Dev",
  "im not doing Asembly",
];

// Reference for the paragraph displaying current text
const currentText = ref<HTMLElement | null>(null);

onMounted(() => {
  let currentIndex = 0; // Track the current index of data array

  const updateText = () => {
    // Update the text content
    if (currentText.value) {
      currentText.value.innerText = data[currentIndex];
    }

    // Animate the text element with from and to effect
    gsap.fromTo(
      currentText.value,
      { opacity: 0, y: 20, rotateX: 90 }, // Start state (from): hidden and below position
      {
        opacity: 1,
        y: 0,
        duration: 1,
        ease: "power2.out",
        stagger: 0.2,
        rotateX: 0,
      } // End state (to): visible and in place
    );

    // Update to the next index, loop back to the start if at the end
    currentIndex = (currentIndex + 1) % data.length;
  };

  // Initial text update and animation
  updateText();

  // Repeat every 22 seconds
  setInterval(updateText, 5000);
});
</script>

<style scoped>
p {
  position: relative;
  opacity: 0; /* Start with hidden text */
}
</style>
