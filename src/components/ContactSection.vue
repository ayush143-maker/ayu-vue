<script setup>
import { ArrowUpRight, Github, Mail } from 'lucide-vue-next'
const props = defineProps({ portfolio: { type: Object, required: true } })
const year = new Date().getFullYear()
</script>

<template>
  <section id="contact" data-section="contact" class="page-section contact-section">
    <div class="page-shell contact-shell">
      <div class="contact-topline"><span><i class="availability-dot"></i> OPEN TO GOOD IDEAS</span><span>THE NEXT CHAPTER / 04</span></div>
      <div class="contact-main">
        <div class="contact-copy"><div class="eyebrow"><span class="eyebrow-line"></span> HAVE SOMETHING IN MIND?</div><h2>Let's build<br />something <span class="serif-italic">meaningful<span class="accent-period">.</span></span></h2><p>A useful idea, an interesting collaboration, or a conversation about making digital things feel better — I’m listening.</p><div class="contact-actions"><a v-if="portfolio.email" class="button button-primary" :href="`mailto:${portfolio.email}`">Start a conversation <Mail :size="16" /></a><a v-else class="button button-primary" :href="portfolio.githubUrl" target="_blank" rel="noreferrer">Say hello on GitHub <ArrowUpRight :size="16" /></a><a class="quiet-link" :href="portfolio.githubUrl" target="_blank" rel="noreferrer"><Github :size="15" /> Follow the work</a></div></div>
        <div class="contact-orbit" aria-hidden="true"><div class="contact-orbit-wash"></div><div class="contact-ring contact-ring-one"></div><div class="contact-ring contact-ring-two"></div><div class="contact-ring contact-ring-three"></div><div class="contact-ring contact-ring-four"></div><span class="contact-planet contact-planet-one"></span><span class="contact-planet contact-planet-two"></span><div class="contact-monogram">a<span>.</span></div><span class="contact-star contact-star-one">✳</span><span class="contact-star contact-star-two">+</span><span class="contact-orbit-label">MAKE SOMETHING MATTER</span></div>
      </div>
      <footer class="site-footer"><a class="brand footer-brand" href="#home"><span class="brand-mark">{{ portfolio.monogram[0] }}<i>.</i></span><span class="brand-name"><strong>{{ portfolio.name }}</strong><small>MADE WITH INTENTION</small></span></a><span class="footer-note">A WORK IN PROGRESS, BY DESIGN.</span><a class="footer-social" :href="portfolio.githubUrl" target="_blank" rel="noreferrer"><Github :size="15" /> GitHub <ArrowUpRight :size="13" /></a><span class="copyright">© {{ year }} {{ portfolio.name }}</span></footer>
    </div>
    <span class="section-counter">03 <i>/</i> 04</span>
  </section>
</template>
