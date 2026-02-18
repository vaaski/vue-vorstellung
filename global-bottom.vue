<script setup lang="ts">
import { useNav } from "@slidev/client"
import { onMounted, watch } from "vue"

const nav = useNav()
let transitionSound: HTMLAudioElement

onMounted(() => {
  transitionSound = new Audio("/transition.mp3")
  transitionSound.volume = 0.5
  transitionSound.preload = "auto"
})

watch(nav.currentPage, (newPage, previousPage) => {
  if (previousPage == null || newPage === previousPage) return
  if (nav.isPresenter.value || !transitionSound) return

  transitionSound.currentTime = 0
  transitionSound.play().catch(() => {})
})
</script>

<template>
  <footer class="absolute bottom-0 right-0 p-4">
    <img src="/T-Systems_Logo_2024.svg" alt="T-Systems" class="h-4" />
  </footer>
</template>
