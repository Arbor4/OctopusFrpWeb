<template>
  <header class="fixed top-0 left-0 right-0 z-50 bg-dark-950/80 backdrop-blur-md border-b border-white/10 transition-all">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
      <!-- Brand Logo -->
      <a href="#" class="flex items-center gap-3 group">
        <div class="relative w-10 h-10 rounded-xl bg-gradient-to-br from-cyan-500/20 to-violet-600/30 border border-cyan-500/30 flex items-center justify-center text-2xl group-hover:scale-105 transition-transform duration-300">
          🐙
          <span class="absolute -bottom-0.5 -right-0.5 w-2.5 h-2.5 bg-emerald-400 rounded-full ring-2 ring-dark-950 animate-pulse"></span>
        </div>
        <div>
          <div class="flex items-center gap-2">
            <span class="font-extrabold text-xl tracking-tight bg-gradient-to-r from-cyan-400 via-sky-300 to-violet-400 bg-clip-text text-transparent">
              OctopusFrp
            </span>
            <span class="text-[10px] px-1.5 py-0.5 font-mono uppercase rounded bg-cyan-500/10 text-cyan-300 border border-cyan-500/20">
              Mesh Relay
            </span>
          </div>
          <p class="text-[11px] text-slate-400 hidden sm:block">多节点带宽聚合穿透网</p>
        </div>
      </a>

      <!-- Desktop Nav Links -->
      <nav class="hidden md:flex items-center gap-7 text-sm font-medium text-slate-300">
        <a href="#purpose" class="hover:text-cyan-400 transition-colors">为什么加入</a>
        <a href="#simulator" class="hover:text-cyan-400 transition-colors">聚合模拟器</a>
        <a href="#how-it-works" class="hover:text-cyan-400 transition-colors">加入流程</a>
        <a href="#deploy" class="hover:text-cyan-400 transition-colors">一键部署脚本</a>
        <a href="#nodes" class="hover:text-cyan-400 transition-colors">中转生态</a>
        <a href="#faq" class="hover:text-cyan-400 transition-colors">常见疑问</a>
      </nav>

      <!-- Right Action CTA -->
      <div class="hidden md:flex items-center gap-3">
        <a 
          href="https://github.com/Arbor4/OctopusFrp" 
          target="_blank" 
          rel="noopener"
          class="flex items-center gap-2 px-3.5 py-2 rounded-lg border border-slate-700 hover:border-slate-500 text-slate-300 hover:text-white text-xs font-mono transition-all bg-dark-900/50 hover:bg-dark-850"
        >
          <svg class="w-4 h-4 fill-current" viewBox="0 0 24 24">
            <path fill-rule="evenodd" clip-rule="evenodd" d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.53 1.032 1.53 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/>
          </svg>
          <span>Star</span>
        </a>

        <a 
          href="#deploy" 
          class="relative inline-flex items-center justify-center px-4 py-2 text-xs font-semibold rounded-lg text-dark-950 bg-gradient-to-r from-cyan-400 to-sky-300 hover:from-cyan-300 hover:to-sky-200 shadow-md shadow-cyan-500/25 transition-all transform hover:-translate-y-0.5 active:translate-y-0"
        >
          <span class="flex items-center gap-1.5">
            <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" />
            </svg>
            加入中转节点
          </span>
        </a>
      </div>

      <!-- Mobile menu button -->
      <button 
        @click="mobileOpen = !mobileOpen"
        class="md:hidden p-2 text-slate-400 hover:text-white rounded-lg focus:outline-none"
        aria-label="Toggle menu"
      >
        <svg v-if="!mobileOpen" class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
        <svg v-else class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </div>

    <!-- Mobile Dropdown -->
    <div v-show="mobileOpen" class="md:hidden border-b border-white/10 bg-dark-950/95 px-4 pt-2 pb-6 space-y-3">
      <a @click="mobileOpen = false" href="#purpose" class="block py-2 text-sm text-slate-300 hover:text-cyan-400">为什么加入</a>
      <a @click="mobileOpen = false" href="#simulator" class="block py-2 text-sm text-slate-300 hover:text-cyan-400">聚合模拟器</a>
      <a @click="mobileOpen = false" href="#how-it-works" class="block py-2 text-sm text-slate-300 hover:text-cyan-400">加入流程</a>
      <a @click="mobileOpen = false" href="#deploy" class="block py-2 text-sm text-slate-300 hover:text-cyan-400">一键部署脚本</a>
      <a @click="mobileOpen = false" href="#nodes" class="block py-2 text-sm text-slate-300 hover:text-cyan-400">中转生态</a>
      <a @click="mobileOpen = false" href="#faq" class="block py-2 text-sm text-slate-300 hover:text-cyan-400">常见疑问</a>
      <div class="pt-2 flex flex-col gap-2">
        <a 
          @click="mobileOpen = false"
          href="#deploy" 
          class="w-full text-center py-2.5 rounded-lg text-dark-950 font-semibold text-xs bg-gradient-to-r from-cyan-400 to-sky-300"
        >
          ⚡ 加入中转节点 (一键部署)
        </a>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue'

const mobileOpen = ref(false)
</script>
