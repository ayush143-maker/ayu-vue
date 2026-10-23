<script setup>
import { ArrowUpRight } from 'lucide-vue-next'
defineProps({ project: { type: Object, required: true } })
</script>

<template>
  <div class="project-artwork" :class="`art-${project.accent}`">
    <div class="artwork-topline"><span>PREVIEW / {{ project.number }}</span><span>{{ project.status.toUpperCase() }}</span></div>
    <div class="artwork-image-wrap"><img :key="project.artwork" :src="project.artwork" :alt="`${project.name} interface concept`" class="artwork-image" /></div>
    <div class="artwork-footer"><span class="artwork-name">{{ project.name }}<small>{{ project.type }}</small></span><span class="artwork-arrow"><ArrowUpRight :size="16" /></span></div>
    <span class="artwork-corner corner-top-left"></span><span class="artwork-corner corner-bottom-right"></span>
  </div>
</template>
