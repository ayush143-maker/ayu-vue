<script setup>
import { computed } from 'vue'
import { AudioLines, CircleDot, Grid2X2, Layers3, Orbit, Sparkles } from 'lucide-vue-next'

const props = defineProps({
  projects: { type: Array, required: true },
  activeIndex: { type: Number, default: 0 },
})
const emit = defineEmits(['select'])
const iconMap = { audio: AudioLines, layers: Layers3, spark: Sparkles, grid: Grid2X2, orbit: Orbit }
const nodes = computed(() => props.projects.map((project, index) => {
  const angle = ((index - props.activeIndex) / props.projects.length) * Math.PI * 2 - Math.PI / 2
  const radius = 36
  return {
    ...project,
    index,
    Icon: iconMap[project.icon] ?? CircleDot,
    style: { left: `${50 + Math.cos(angle) * radius}%`, top: `${50 + Math.sin(angle) * radius}%` },
  }
}))
const activeProject = computed(() => props.projects[props.activeIndex])
</script>

<template>
  <div class="dial-module">
    <div class="dial-topline"><span>PROJECT INDEX</span><span>SELECT / ROTATE</span></div>
    <div class="project-dial" :class="`dial-${activeProject.accent}`" role="group" aria-label="Select a featured project">
      <div class="dial-glow"></div><div class="dial-ring ring-outer"></div><div class="dial-ring ring-middle"></div><div class="dial-ring ring-inner"></div>
      <div class="dial-axis axis-horizontal"></div><div class="dial-axis axis-vertical"></div>
      <span class="dial-orbit-dot orbit-dot-one"></span><span class="dial-orbit-dot orbit-dot-two"></span><span class="dial-orbit-dot orbit-dot-three"></span>
      <button v-for="node in nodes" :key="node.id" type="button" class="dial-node" :class="[{ 'is-active': activeIndex === node.index }, `node-${node.accent}`]" :style="node.style" :aria-label="`Select project ${node.number}: ${node.name}`" :aria-pressed="activeIndex === node.index" @click="emit('select', node.index)">
        <span class="node-number">{{ node.number }}</span><span class="node-dot"></span>
      </button>
      <div class="dial-center"><div class="dial-center-icon"><component :is="iconMap[activeProject.icon] ?? CircleDot" :size="20" :stroke-width="1.55" /></div><span class="dial-center-caption">NOW EXPLORING</span><strong>{{ activeProject.number }}</strong><span class="dial-center-total">OF {{ String(projects.length).padStart(2, '0') }}</span></div>
      <span class="dial-coordinate coordinate-one">N 04° 18′</span><span class="dial-coordinate coordinate-two">FIELD / {{ activeProject.number }}</span>
    </div>
    <div class="dial-controls"><button type="button" aria-label="Previous project" @click="emit('select', (activeIndex - 1 + projects.length) % projects.length)">←</button><div class="dial-pagination" aria-label="Choose project"><button v-for="(project, index) in projects" :key="project.id" type="button" :aria-label="`Go to ${project.name}`" :aria-current="index === activeIndex ? 'true' : undefined" :class="{ 'is-active': index === activeIndex }" @click="emit('select', index)"></button></div><button type="button" aria-label="Next project" @click="emit('select', (activeIndex + 1) % projects.length)">→</button></div>
    <p class="dial-hint"><span>↔</span> Tap a node or swipe through the work</p>
  </div>
</template>
