<script setup>
import { ArrowDownRight, ArrowUpRight } from 'lucide-vue-next'
import HeroVisual from './HeroVisual.vue'
const props = defineProps({ portfolio: { type: Object, required: true } })
</script>

<template>
  <section id="home" data-section="home" class="page-section hero-section">
    <div class="page-shell hero-shell">
      <div class="hero-copy">
        <div class="eyebrow"><span class="eyebrow-line"></span>{{ portfolio.role }}</div>
        <h1>Ideas into<br /><span class="serif-italic">interfaces<span class="accent-period">.</span></span></h1>
        <p class="hero-lede">{{ portfolio.intro }}</p>
        <div class="hero-buttons">
          <a class="button button-primary" href="#work">Explore selected work <ArrowDownRight :size="17" /></a>
          <a class="quiet-link" :href="portfolio.githubUrl" target="_blank" rel="noreferrer">GitHub profile <ArrowUpRight :size="15" /></a>
        </div>
        <div class="hero-footline"><span><i class="availability-dot"></i>{{ portfolio.locationLabel }}</span></div>
      </div>
      <HeroVisual />
    </div>

  </section>
</template>
