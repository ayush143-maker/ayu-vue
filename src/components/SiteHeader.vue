<script setup>
import { ref, watch } from 'vue'
import { ArrowUpRight, Menu, X } from 'lucide-vue-next'

const props = defineProps({
  portfolio: { type: Object, required: true },
  activeSection: { type: String, default: 'home' },
})
const menuOpen = ref(false)
const links = [
  { id: 'work', number: '01', label: 'Selected work' },
  { id: 'about', number: '02', label: 'About' },
  { id: 'contact', number: '03', label: 'Contact' },
]
function closeMenu() { menuOpen.value = false }
watch(() => props.activeSection, closeMenu)
</script>

<template>
  <header class="site-header">
    <a class="brand" href="#home" aria-label="Ayush, back to home" @click="closeMenu">
      <span class="brand-mark">{{ portfolio.monogram[0] }}<i>.</i></span>
      <span class="brand-name"><strong>{{ portfolio.name }}</strong><small>INDEPENDENT BUILDER</small></span>
    </a>

    <nav class="desktop-nav" aria-label="Main navigation">
      <a v-for="link in links" :key="link.id" :href="`#${link.id}`" :class="{ 'is-current': activeSection === link.id }">
        {{ link.label }} <span>{{ link.number }}</span>
      </a>
    </nav>

    <a class="header-cta" href="#contact"><span class="availability-dot"></span> Open to good ideas <ArrowUpRight :size="14" /></a>

    <button class="menu-toggle" type="button" :aria-expanded="menuOpen" aria-controls="mobile-navigation" :aria-label="menuOpen ? 'Close navigation' : 'Open navigation'" @click="menuOpen = !menuOpen">
      <X v-if="menuOpen" :size="19" />
      <Menu v-else :size="19" />
    </button>

    <Transition name="menu-drop">
      <nav v-if="menuOpen" id="mobile-navigation" class="mobile-nav" aria-label="Mobile navigation">
        <a v-for="link in links" :key="link.id" :href="`#${link.id}`" @click="closeMenu">
          <span><small>{{ link.number }}</small>{{ link.label }}</span><ArrowUpRight :size="17" />
        </a>
        <div class="mobile-nav-footer"><span class="availability-dot"></span> Available for interesting ideas</div>
      </nav>
    </Transition>
  </header>
</template>
