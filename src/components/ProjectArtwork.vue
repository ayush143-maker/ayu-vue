<script setup>
defineProps({ project: { type: Object, required: true } })
</script>

<template>
  <div class="project-artwork" :class="`art-${project.accent}`">
    <img :key="project.artwork" :src="project.artwork" :alt="`${project.name} interface concept artwork`" class="artwork-image" />
  </div>
</template>
