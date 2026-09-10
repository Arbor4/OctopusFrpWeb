<template>
  <div class="min-h-screen bg-dark-950 text-slate-100 flex flex-col font-sans selection:bg-cyan-500/30 selection:text-cyan-300">
    <!-- Fixed Navigation Bar -->
    <Navbar />

    <!-- Main Content Stream -->
    <main class="flex-grow">
      <!-- 1. Hero Area -->
      <HeroSection />

      <!-- 2. Purpose & Philosophy (为什么需要大家加入中转节点) -->
      <PurposeSection />

      <!-- 3. Interactive Bandwidth Simulator (多中转聚合演示器) -->
      <AggregationDemo />

      <!-- 4. 3-Step Joining Guide (如何加入成为中转节点) -->
      <JoinStepsSection />

      <!-- 5. One-Click Script Generator (一键部署脚本交互生成器) -->
      <ScriptGenerator />

      <!-- 6. Distributed Node Showcase (活跃中继节点态势展示) -->
      <NodeShowcase />

      <!-- 7. Frequently Asked Questions (FAQ) -->
      <FaqSection />
    </main>

    <!-- Footer -->
    <FooterSection />
  </div>
</template>

<script setup>
import Navbar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import PurposeSection from './components/PurposeSection.vue'
import AggregationDemo from './components/AggregationDemo.vue'
import JoinStepsSection from './components/JoinStepsSection.vue'
import ScriptGenerator from './components/ScriptGenerator.vue'
import NodeShowcase from './components/NodeShowcase.vue'
import FaqSection from './components/FaqSection.vue'
import FooterSection from './components/FooterSection.vue'
</script>
