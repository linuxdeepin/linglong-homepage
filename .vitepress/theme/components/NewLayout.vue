<template>
  <Layout v-if="lay.isDefault" />
  <Home v-if="lay.isHome" />
  <EnHome v-if="lay.isEnHome" />
</template>
<script setup>
import Home from './zh/home/index.vue'
import EnHome from './en/home/index.vue'

import { useRoute } from 'vitepress'
import DefaultTheme from 'vitepress/theme'
import { onMounted, computed } from 'vue'
const { Layout } = DefaultTheme

const route = useRoute()

const lay = computed(() => {
  let _lay = {
    isDefault: false,
    isHome: false,
    isEnHome: false
  }
  if (route.path === '/') {
    _lay.isHome = true
  }
  if (route.path.startsWith('/en/index.html')) {
    _lay.isEnHome = true
  }
  if (route.path !== '/' && !route.path.startsWith('/en/index.html')) {
    _lay.isDefault = true
  }
  return _lay
})

// onMounted(() => {
//   if (route.path === '/en/') {
//     location.href = '/en/index.html'
//   }
// })
</script>
