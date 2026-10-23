<script setup>
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'
import { ArrowLeft, ArrowRight, ArrowUpRight } from 'lucide-vue-next'
import { projects } from '../data/projects'
import ProjectArtwork from './ProjectArtwork.vue'

const props = defineProps({ portfolio: { type: Object, required: true } })
const activeIndex = ref(0)
const activeProject = computed(() => projects[activeIndex.value])
const orbitItems = computed(() => projects.map((project, index) => {
  const angle = (index / projects.length) * Math.PI * 2 - Math.PI / 2
  return { ...project, index, style: { '--angle': `${angle}rad`, '--delay': `${index * -0.7}s` } }
}))
let touchStartX = 0
function selectProject(index) { activeIndex.value = (index + projects.length) % projects.length }
function nextProject() { selectProject(activeIndex.value + 1) }
function previousProject() { selectProject(activeIndex.value - 1) }
function onKeydown(event) {
  if (event.key === 'ArrowRight') nextProject()
  if (event.key === 'ArrowLeft') previousProject()
}
onMounted(() => window.addEventListener('keydown', onKeydown))
onBeforeUnmount(() => window.removeEventListener('keydown', onKeydown))
function onTouchStart(event) { touchStartX = event.changedTouches[0]?.clientX ?? 0 }
function onTouchEnd(event) {
  const dx = (event.changedTouches[0]?.clientX ?? 0) - touchStartX
  if (Math.abs(dx) > 48) dx < 0 ? nextProject() : previousProject()
}
</script>

<template>
  <section id="work" data-section="work" class="page-section work-section work-v1">
    <div class="page-shell work-shell-v1">
      <header class="work-heading-v1">
        <div><p class="eyebrow">SELECTED WORK</p><h2>Things in <span class="serif-italic">orbit.</span></h2></div>
        <p class="work-subtitle-v1">A few ideas, experiments, and things I’m building.</p>
      </header>

      <div class="swirl-stage" @touchstart.passive="onTouchStart" @touchend.passive="onTouchEnd">
        <div class="swirl-backdrop" aria-hidden="true"><span></span><span></span><span></span></div>
        <div class="orbit-track" aria-label="Choose a project">
          <button v-for="item in orbitItems" :key="item.id" class="orbit-project" :class="[{ 'is-selected': activeIndex === item.index }, `orbit-${item.accent}`]" :style="item.style" type="button" :aria-label="`Show ${item.name}`" :aria-pressed="activeIndex === item.index" @click="selectProject(item.index)">
            <span class="orbit-project-number">{{ item.number }}</span><span class="orbit-project-name">{{ item.name }}</span>
          </button>
        </div>
        <Transition name="feature-swap" mode="out-in">
          <article :key="activeProject.id" class="featured-project-v1">
            <div class="featured-topline"><span>{{ activeProject.number }} / 07</span><span>{{ activeProject.type }}</span></div>
            <ProjectArtwork :project="activeProject" />
            <div class="featured-copy-v1"><div><h3>{{ activeProject.name }}<span class="accent-period">.</span></h3><p>{{ activeProject.title }}</p></div><span class="concept-label">{{ activeProject.status }}</span></div>
            <p class="featured-description-v1">{{ activeProject.summary }}</p>
            <div class="featured-bottomline"><div class="featured-tags"><span v-for="tag in activeProject.tags" :key="tag">{{ tag }}</span></div><a :href="activeProject.href || portfolio.githubUrl" target="_blank" rel="noreferrer" class="featured-link" :aria-label="`${activeProject.cta} on GitHub`"><ArrowUpRight :size="19" /></a></div>
          </article>
        </Transition>
      </div>

      <div class="work-controls-v1"><button type="button" aria-label="Previous project" @click="previousProject"><ArrowLeft :size="17" /></button><div class="work-progress-v1"><span>{{ activeProject.number }}</span><div><i :style="{ width: `${((activeIndex + 1) / projects.length) * 100}%` }"></i></div><span>07</span></div><button type="button" aria-label="Next project" @click="nextProject"><ArrowRight :size="17" /></button></div>
      <p class="work-note-v1">Concept projects are illustrative studies; shipped work is labelled separately.</p>
    </div>
  </section>
</template>
