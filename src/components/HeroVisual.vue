<script setup>
import { ArrowUpRight, AudioLines, Play, Plus } from 'lucide-vue-next'
</script>

<template>
  <div class="hero-visual" aria-label="An abstract preview of a music player interface" role="img">
    <div class="visual-caption visual-caption-top"><span>FIG. 001 — PRODUCT STUDY</span><span>01 / 04</span></div>
    <div class="visual-window">
      <div class="window-bar"><span class="window-dots"><i></i><i></i><i></i></span><span class="window-title">aurix / now playing</span><span class="window-menu">···</span></div>
      <div class="window-body">
        <div class="album-art">
          <div class="album-haze"></div><div class="album-ring album-ring-one"></div><div class="album-ring album-ring-two"></div><div class="album-ring album-ring-three"></div>
          <span class="album-cross cross-a">+</span><span class="album-cross cross-b">+</span><span class="album-label">A / 001</span>
          <div class="album-center"><AudioLines :size="31" :stroke-width="1.35" /></div>
        </div>
        <div class="player-details"><div class="player-label">YOUR SPACE TO LISTEN</div><h3>Slow<br /><em>motion</em></h3><p>Soft focus <span>—</span> 03:42</p><div class="waveform" aria-hidden="true"><i v-for="bar in 31" :key="bar" :style="{ '--bar': `${18 + ((bar * 17 + bar * bar * 3) % 61)}%` }"></i></div><div class="player-controls"><span class="control-muted">↶</span><span class="player-play"><Play :size="15" fill="currentColor" /></span><span class="control-muted">↷</span></div></div>
      </div>
      <div class="window-footer"><span>DESIGNED FOR THE MOMENT</span><span>◎ STEREO</span></div>
    </div>
    <div class="float-chip float-chip-one"><span class="chip-icon"><Plus :size="14" /></span><span><small>DESIGN PRINCIPLE</small><strong>Less, but considered.</strong></span></div>
    <div class="float-chip float-chip-two"><span class="chip-live"></span><span><small>STATUS</small><strong>In the making</strong></span><ArrowUpRight :size="14" /></div>
    <div class="visual-caption visual-caption-bottom"><span>IDEA → INTERACTION → DETAIL</span><span>MADE WITH INTENTION</span></div>
    <span class="visual-sparkle sparkle-one">✳</span><span class="visual-sparkle sparkle-two">✳</span>
  </div>
</template>
