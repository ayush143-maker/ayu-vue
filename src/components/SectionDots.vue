<script setup>
import { computed } from 'vue'
const props = defineProps({ activeSection: { type: String, default: 'home' } })
const sections = [
  { id: 'home', label: 'Introduction', number: '00' },
  { id: 'work', label: 'Selected work', number: '01' },
  { id: 'about', label: 'About', number: '02' },
  { id: 'contact', label: 'Contact', number: '03' },
]
const activeNumber = computed(() => sections.find((item) => item.id === props.activeSection)?.number ?? '00')
</script>

<template>
  <aside class="section-rail" aria-label="Page sections">
    <span class="rail-current">{{ activeNumber }}</span>
    <span class="rail-line"></span>
    <a v-for="section in sections" :key="section.id" :href="`#${section.id}`" :aria-label="section.label" :aria-current="activeSection === section.id ? 'location' : undefined" :class="{ 'is-active': activeSection === section.id }"><span></span></a>
    <span class="rail-total">04</span>
  </aside>
</template>
