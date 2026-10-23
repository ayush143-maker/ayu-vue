<script setup>
import { ArrowUpRight, Compass, Layers3, ScanLine } from 'lucide-vue-next'
const props = defineProps({ portfolio: { type: Object, required: true } })
const principles = [
  { number: '01', icon: Compass, title: 'Start with the feeling.', description: 'Useful interfaces should feel clear, calm, and considered before you even think about how they work.' },
  { number: '02', icon: Layers3, title: 'Take ideas seriously.', description: 'A good idea gets more interesting when it meets real constraints, real code, and a real person using it.' },
  { number: '03', icon: ScanLine, title: 'Refine what matters.', description: 'Keep the meaningful details. Remove the noise. Give every interaction a reason to be there.' },
]
</script>

<template>
  <section id="about" data-section="about" class="page-section about-section">
    <div class="page-shell about-shell">
      <div class="about-main">
        <div class="eyebrow"><span class="eyebrow-line"></span> A LITTLE ABOUT HOW I WORK</div>
        <h2>Curious by default.<br /><span class="serif-italic">Intentional</span> by design<span class="accent-period">.</span></h2>
        <p>{{ portfolio.about }}</p>
        <a class="quiet-link" :href="portfolio.githubUrl" target="_blank" rel="noreferrer">A little more on GitHub <ArrowUpRight :size="15" /></a>
        <div class="currently-card"><span class="currently-icon"><span></span></span><div><small>CURRENTLY EXPLORING</small><p>{{ portfolio.currently }}</p></div><span class="currently-arrow">↗</span></div>
      </div>

      <div class="about-side">
        <div class="principles-label"><span>HOW I THINK</span><span>THREE SMALL PRINCIPLES</span></div>
        <div class="principles-list"><article v-for="principle in principles" :key="principle.number" class="principle-row"><span class="principle-number">{{ principle.number }}</span><span class="principle-icon"><component :is="principle.icon" :size="20" :stroke-width="1.5" /></span><div class="principle-copy"><h3>{{ principle.title }}</h3><p>{{ principle.description }}</p></div><span class="principle-mark">↗</span></article></div>
        <div class="toolkit-block"><span class="toolkit-label">TOOLKIT / CURRENTLY</span><div class="toolkit-tags"><span v-for="tool in portfolio.toolkit" :key="tool">{{ tool }}</span></div></div>
        <div class="about-endnote"><span>NOT MORE. JUST MORE THOUGHTFUL.</span><span>PROCESS / 001—003</span></div>
      </div>
    </div>
    <span class="section-counter">02 <i>/</i> 04</span>
  </section>
</template>
