<template>
  <div class="p-5 bg-black">
    <Nav />

    <article class="text-white flex flex-col gap-3">
      <h1 class="2xl:text-4xl text-3xl place-self-center">
        I'm a Front End Dev
      </h1>

      <div class="flex justify-evenly border-b border-white pb-4 mb-4">
        <h5
          :class="[
            '2xl:text-2xl',
            'hover:grayscale-0',
            'flex',
            'items-center',
            'gap-3',
            'cursor-pointer',
            'hover:text-white',
            number === index
              ? 'grayscale-0 text-white'
              : 'text-gray-300 grayscale',
          ]"
          v-for="(lang, index) in myProgrammingLang"
          :key="index"
        >
          <Icon :icon="lang.logo" />
          {{ lang.lang }}
        </h5>
      </div>
      <div class="flex mx-4">
        <div class="flex-1" ref="educationRef">
          <h2>Education :</h2>
          <ul class="flex flex-col gap-3 mt-3">
            <li>
              <h3>Clan 486</h3>
              <p>Flutter</p>
              <p>Vice President</p>
              <p>2022</p>
            </li>
            <li>
              <h3>STMIK PPKIA Pradnya Paramita</h3>
              <p>Kotlin</p>
              <p>Next Js</p>
              <p>Laravel</p>
              <p>Student</p>
              <p>2021 - Now</p>
            </li>
            <li>
              <h3>Bangkit Academy</h3>
              <p>Machine Learning</p>
              <p>JavaScript</p>
              <p>TypeScript</p>
              <p>Student</p>
            </li>
            <li>
              <h3>SMK National Media Center</h3>
              <p>Code Igniter</p>
              <p>PHP</p>
              <p>Java</p>
              <p>SQL</p>
            </li>
          </ul>
        </div>
        <div class="flex-1" ref="experienceRef">
          <h2>Experience :</h2>
          <ul class="flex flex-col gap-3 mt-3">
            <li>
              <h3>Bengkel TI</h3>
              <p>Front End Dev</p>
              <p>React Native</p>
              <p>Freelance</p>
              <p>Sep - Mar 2023</p>
            </li>
            <li>
              <h3>Optimasi.ai</h3>
              <p>Front End Dev</p>
              <p>Vue.js</p>
              <p>Intern</p>
              <p>Jul - Sep 2024</p>
            </li>
          </ul>
        </div>
        <Laptop />
      </div>
    </article>
    <footer>
      <hr class="my-5" />
      <h5 class="w-full text-center">Contact Me</h5>
      <div class="flex justify-evenly">
        <p
          :class="[
            '2xl:text-2xl',
            'hover:grayscale-0',
            'flex',
            'items-center',
            'gap-3',
            'cursor-pointer',
            'hover:text-white',
            number % 2 ? 'grayscale-0 text-white' : 'text-gray-300 grayscale',
          ]"
        >
          <Icon icon="logos:whatsapp-icon" /> +62 851 5677 1750
        </p>
        <p
          :class="[
            '2xl:text-2xl',
            'hover:grayscale-0',
            'flex',
            'items-center',
            'gap-3',
            'cursor-pointer',
            'hover:text-white',
            (number - 1) % 2
              ? 'grayscale-0 text-white'
              : 'text-gray-300 grayscale',
          ]"
        >
          <Icon class="text-red-500" icon="clarity:email-solid" />
          khamalapp@gmail.com
        </p>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";
import { gsap } from "gsap";
import { Icon } from "@iconify/vue";
import Nav from "./components/Nav.vue";
import Laptop from "./components/Laptop.vue";

const myProgrammingLang = [
  {
    lang: "Laravel",
    logo: "logos:laravel",
  },
  {
    lang: "React Native",
    logo: "logos:react",
  },
  {
    lang: "Next.Js",
    logo: "logos:nextjs-icon",
  },
  {
    lang: "Vue.Js",
    logo: "logos:vue",
  },
  {
    lang: "Flutter",
    logo: "logos:flutter",
  },
  {
    lang: "Code Igniter",
    logo: "logos:codeigniter-icon",
  },
];

const educationRef = ref<HTMLElement | null>(null);
const experienceRef = ref<HTMLElement | null>(null);

onMounted(() => {
  if (educationRef.value) {
    gsap.fromTo(
      educationRef.value,
      { x: -100, opacity: 0 },
      { x: 0, opacity: 1, duration: 0.5, ease: "power2.out" }
    );
  }

  if (experienceRef.value) {
    gsap.fromTo(
      experienceRef.value,
      { x: -100, opacity: 0 },
      { x: 0, opacity: 1, duration: 0.5, ease: "power2.out", delay: 0.2 }
    );
  }
});

const number = ref(1);
let intervalId: number | null = null;

onMounted(() => {
  intervalId = setInterval(() => {
    if (number.value < myProgrammingLang.length - 1) {
      number.value += 1;
    } else {
      number.value = 0; // Reset kembali ke 1 setelah mencapai 5
    }
  }, 1500);
});

onBeforeUnmount(() => {
  if (intervalId !== null) {
    clearInterval(intervalId);
  }
});
</script>

<style scoped>
p {
  @apply ml-3;
}
</style>
