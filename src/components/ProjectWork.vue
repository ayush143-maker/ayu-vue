<script setup>
import { computed, ref } from 'vue'
import { ArrowLeft, ArrowRight, ArrowUpRight, Check, CircleDashed } from 'lucide-vue-next'
import { projects } from '../data/projects'
import ProjectDial from './ProjectDial.vue'
import ProjectArtwork from './ProjectArtwork.vue'

const props = defineProps({ portfolio: { type: Object, required: true } })
const activeIndex = ref(0)
const activeProject = computed(() => projects[activeIndex.value])
let touchStartX = 0
let touchStartY = 0
function selectProject(index) { activeIndex.value = (index + projects.length) % projects.length }
function nextProject() { selectProject(activeIndex.value + 1) }
function previousProject() { selectProject(activeIndex.value - 1) }
function onTouchStart(event) { touchStartX = event.changedTouches[0]?.clientX ?? 0; touchStartY = event.changedTouches[0]?.clientY ?? 0 }
function onTouchEnd(event) {
  const dx = (event.changedTouches[0]?.clientX ?? 0) - touchStartX
  const dy = (event.changedTouches[0]?.clientY ?? 0) - touchStartY
  if (Math.abs(dx) > 46 && Math.abs(dx) > Math.abs(dy) * 1.2) dx < 0 ? nextProject() : previousProject()
}
</script>

<template>
  <section id="work" data-section="work" class="page-section work-section">
    <div class="page-shell work-shell">
      <div class="section-intro work-intro">
        <div><div class="eyebrow"><span class="eyebrow-line"></span> A FEW THINGS IN MOTION</div><h2>Selected <span class="serif-italic">work<span class="accent-period">.</span></span></h2></div>
        <p>Projects, prototypes, and ideas<br class="desktop-only" /> becoming something real.</p>
        <span class="intro-index">01 — 05 / PROJECTS</span>
      </div>

      <div class="work-grid" @touchstart.passive="onTouchStart" @touchend.passive="onTouchEnd">
        <div class="work-copy-column">
          <div class="project-copy-head"><span class="project-kind">{{ activeProject.type }}</span><span class="project-index-pill">{{ activeProject.number }} <i>/</i> {{ String(projects.length).padStart(2, '0') }}</span></div>
          <Transition name="project-fade" mode="out-in">
            <article :key="activeProject.id" class="project-copy">
              <div class="project-status"><CircleDashed :size="13" /> {{ activeProject.status }}</div>
              <h3>{{ activeProject.name }}<span class="accent-period">.</span></h3>
              <p class="project-promise">{{ activeProject.title }}</p>
              <p class="project-description">{{ activeProject.summary }}</p>
              <div class="project-tags"><span v-for="tag in activeProject.tags" :key="tag">{{ tag }}</span></div>
              <div class="project-action-row"><a class="button button-primary" :href="activeProject.href || portfolio.githubUrl" target="_blank" rel="noreferrer">{{ activeProject.href ? activeProject.cta : 'Explore on GitHub' }} <ArrowUpRight :size="16" /></a><span class="project-availability"><Check :size="13" /> Built in public, where possible</span></div>
            </article>
          </Transition>
          <div class="project-switcher"><button type="button" aria-label="Previous project" @click="previousProject"><ArrowLeft :size="16" /></button><span>MOVE THROUGH THE WORK</span><button type="button" aria-label="Next project" @click="nextProject"><ArrowRight :size="16" /></button></div>
        </div>

        <div class="work-visual-column">
          <Transition name="art-swap" mode="out-in"><ProjectArtwork :key="activeProject.id" :project="activeProject" /></Transition>
          <ProjectDial :projects="projects" :active-index="activeIndex" @select="selectProject" />
        </div>
      </div>
      <div class="work-bottomline"><span>SELECT WITH INTENTION.</span><span><i></i> {{ String(activeIndex + 1).padStart(2, '0') }} OF {{ String(projects.length).padStart(2, '0') }}</span></div>
    </div>
    <span class="section-counter">01 <i>/</i> 04</span>
  </section>
</template>
