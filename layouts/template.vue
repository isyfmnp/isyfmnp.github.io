<template>
  <div id="page">
    <NavBar />
    <ButtonScroll />

    <main id="body">
      <slot />
    </main>

    <Footer />
  </div>
</template>

<style scoped>
#body {
  max-width: min(var(--content-width), 100vw);
  --page-margin: 1.5rem;
  margin: 1rem auto 5rem;
  padding-inline: var(--page-margin);
  min-height: 110vh;
}
</style>

<script setup>
import ButtonScroll from "../components/button/scroll.vue";
import { ref, onMounted } from "vue";

import { gsap } from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";

const height = ref(0);
onMounted(() => {
  window.error = false;

  gsap.registerPlugin(ScrollTrigger);

  const sections = gsap.utils.toArray("main section");

  sections.forEach((section) => {
    gsap.from(section, {
      opacity: 0.125,
      y: 15,
      duration: 0.375,
      delay: 0.125,
      ease: "power3.inOut",
      scrollTrigger: section,
    });
  });
});

useSeoMeta({
  title: 'ISYF 2025',
  ogTitle: 'ISYF 2025',
  ogDescription: 'International Science Youth Forum 2025',
  ogImage: 'https://isyf.hci.edu.sg/icon_light_solid.png',
})
</script>
