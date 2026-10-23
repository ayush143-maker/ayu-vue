<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'
import { portfolio } from './data/portfolio'
import SiteHeader from './components/SiteHeader.vue'
import SectionDots from './components/SectionDots.vue'
import HeroSection from './components/HeroSection.vue'
import ProjectWork from './components/ProjectWork.vue'
import AboutSection from './components/AboutSection.vue'
import ContactSection from './components/ContactSection.vue'

const activeSection = ref('home')
let sectionObserver

onMounted(() => {
  const sections = document.querySelectorAll('[data-section]')
  if (!('IntersectionObserver' in window)) return
  sectionObserver = new IntersectionObserver((entries) => {
    const visible = entries
      .filter((entry) => entry.isIntersecting)
      .sort((a, b) => b.intersectionRatio - a.intersectionRatio)[0]
    if (visible) activeSection.value = visible.target.dataset.section
  }, { rootMargin: '-24% 0px -52% 0px', threshold: [0.05, 0.18, 0.35, 0.55] })
  sections.forEach((section) => sectionObserver.observe(section))
})

onBeforeUnmount(() => sectionObserver?.disconnect())
</script>

<template>
  <a class="skip-link" href="#main">Skip to content</a>
  <SiteHeader :portfolio="portfolio" :active-section="activeSection" />
  <SectionDots :active-section="activeSection" />

  <main id="main" class="snap-container">
    <HeroSection :portfolio="portfolio" />
    <ProjectWork :portfolio="portfolio" />
    <AboutSection :portfolio="portfolio" />
    <ContactSection :portfolio="portfolio" />
  </main>
</template>
