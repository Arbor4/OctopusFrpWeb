<template>
  <section id="simulator" class="py-24 relative overflow-hidden bg-dark-950">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Header -->
      <div class="text-center max-w-3xl mx-auto mb-16">
        <div class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-cyan-950/60 border border-cyan-500/30 text-cyan-300 text-xs font-mono uppercase tracking-wider mb-4">
          <span>⚡ 核心黑科技演示</span>
        </div>
        <h2 class="text-3xl sm:text-4xl font-extrabold text-white tracking-tight">
          动态体验：多中继带宽聚合模拟器
        </h2>
        <p class="mt-4 text-slate-400 text-base sm:text-lg">
          随意开启或调整中转节点的物理带宽，感受八爪鱼并发条带化（Striping）带来的质变加速。
        </p>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
        <!-- Left: Node Pool Controls (7 Cols) -->
        <div class="lg:col-span-7 glass-card rounded-2xl p-6 sm:p-8 border border-white/10">
          <div class="flex items-center justify-between mb-6 pb-4 border-b border-slate-800">
            <div>
              <h3 class="text-lg font-bold text-white flex items-center gap-2">
                <span>中继节点集群池 (Relay Pool)</span>
                <span class="text-xs px-2 py-0.5 rounded bg-cyan-500/10 text-cyan-400 font-mono">
                  已启用 {{ activeNodeCount }} / {{ nodes.length }} 节点
                </span>
              </h3>
              <p class="text-xs text-slate-400 mt-0.5">勾选节点或调节滑块，模拟不同公网机器加入聚合集群</p>
            </div>
            <button 
              @click="resetNodes" 
              class="text-xs text-slate-400 hover:text-cyan-400 font-mono transition-colors"
            >
              重置参数
            </button>
          </div>

          <!-- Nodes List -->
          <div class="space-y-4">
            <div 
              v-for="node in nodes" 
              :key="node.id"
              class="p-4 rounded-xl border transition-all duration-300"
              :class="node.enabled 
                ? 'bg-dark-850/80 border-cyan-500/30 shadow-md shadow-cyan-950/20' 
                : 'bg-dark-900/30 border-slate-800 opacity-60'"
            >
              <div class="flex items-center justify-between mb-3">
                <div class="flex items-center gap-3">
                  <input 
                    type="checkbox" 
                    v-model="node.enabled"
                    :id="'node-' + node.id"
                    class="w-4 h-4 rounded bg-dark-900 border-slate-700 text-cyan-500 focus:ring-cyan-500 focus:ring-offset-dark-950 cursor-pointer"
                  />
                  <label :for="'node-' + node.id" class="text-sm font-semibold text-white cursor-pointer flex items-center gap-2">
                    <span>{{ node.name }}</span>
                    <span class="text-[11px] px-1.5 py-0.2 rounded font-mono" :class="node.badgeClass">
                      {{ node.region }}
                    </span>
                  </label>
                </div>
                <div class="text-right font-mono">
                  <span class="text-sm font-bold" :class="node.enabled ? 'text-cyan-400' : 'text-slate-500'">
                    {{ node.bandwidth }} Mbps
                  </span>
                </div>
              </div>

              <!-- Bandwidth Slider -->
              <div class="flex items-center gap-3">
                <span class="text-xs text-slate-400 font-mono w-8">1M</span>
                <input 
                  type="range" 
                  min="1" 
                  max="50" 
                  v-model.number="node.bandwidth" 
                  :disabled="!node.enabled"
                  class="w-full h-1.5 bg-slate-700 rounded-lg appearance-none cursor-pointer accent-cyan-400 disabled:opacity-30 disabled:cursor-not-allowed"
                />
                <span class="text-xs text-slate-400 font-mono w-10">50M</span>
              </div>
            </div>
          </div>

          <!-- Add Node Hint -->
          <div class="mt-6 pt-4 border-t border-slate-800 flex items-center justify-between text-xs text-slate-400">
            <span class="flex items-center gap-1.5">
              <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
              支持平滑加权轮询 (SWRR) 智能分配流量
            </span>
            <a href="#deploy" class="text-cyan-400 hover:underline">部署你的节点加入测试 →</a>
          </div>
        </div>

        <!-- Right: Aggregation Result & Telemetry (5 Cols) -->
        <div class="lg:col-span-5 space-y-6">
          <!-- Total Aggregation Meter -->
          <div class="glass-card rounded-2xl p-6 sm:p-8 border border-cyan-500/40 relative overflow-hidden box-glow-cyan">
            <div class="absolute -right-8 -bottom-8 w-40 h-40 bg-cyan-500/10 rounded-full blur-2xl pointer-events-none"></div>
            
            <span class="text-xs font-mono uppercase tracking-wider text-cyan-300">聚合总出站吞吐</span>
            <div class="mt-2 flex items-baseline gap-3">
              <div class="text-5xl sm:text-6xl font-black text-white font-mono tracking-tight">
                {{ totalBandwidth }}
              </div>
              <span class="text-xl font-bold text-cyan-400 font-mono">Mbps</span>
              <span class="text-xs font-mono text-emerald-400 bg-emerald-950/60 px-2 py-0.5 rounded border border-emerald-500/30">
                提升 {{ speedMultiplier }}x
              </span>
            </div>

            <!-- Mathematical Equation -->
            <div class="mt-4 p-3 rounded-lg bg-dark-900/80 border border-slate-800 font-mono text-xs text-slate-300 overflow-x-auto">
              <span class="text-slate-400">吞吐公式：</span>
              <span class="text-cyan-300">{{ equationText }}</span>
            </div>

            <!-- Progress Bar comparing single vs aggregated -->
            <div class="mt-6 space-y-3">
              <div>
                <div class="flex justify-between text-xs font-mono mb-1">
                  <span class="text-slate-400">传统单台 VPS 极限 (5M)</span>
                  <span class="text-slate-400">约 600 KB/s</span>
                </div>
                <div class="w-full bg-slate-800 rounded-full h-2">
                  <div class="bg-slate-500 h-2 rounded-full" style="width: 12%"></div>
                </div>
              </div>

              <div>
                <div class="flex justify-between text-xs font-mono mb-1">
                  <span class="text-cyan-300 font-semibold">OctopusFrp 聚合速率</span>
                  <span class="text-cyan-400 font-semibold font-mono">约 {{ (totalBandwidth / 8).toFixed(1) }} MB/s</span>
                </div>
                <div class="w-full bg-slate-800 rounded-full h-3 overflow-hidden p-0.5">
                  <div 
                    class="bg-gradient-to-r from-cyan-400 to-violet-500 h-full rounded-full transition-all duration-500" 
                    :style="{ width: Math.min(100, Math.max(8, (totalBandwidth / 70) * 100)) + '%' }"
                  ></div>
                </div>
              </div>
            </div>
          </div>

          <!-- Scenario Comparison Cards -->
          <div class="glass-card rounded-2xl p-6 border border-white/10 space-y-4">
            <h4 class="text-sm font-bold text-white uppercase tracking-wider font-mono">实际场景表现对比</h4>
            
            <div class="p-3.5 rounded-xl bg-dark-850/60 border border-slate-800/80 flex items-center justify-between">
              <div class="flex items-center gap-3">
                <div class="text-2xl">🖥️</div>
                <div>
                  <div class="text-xs font-bold text-white">Windows 远程桌面 (RDP 3389)</div>
                  <div class="text-[11px] text-slate-400">消除 Bufferbloat 拥塞，极低手感延迟</div>
                </div>
              </div>
              <span class="text-xs font-bold font-mono px-2 py-1 rounded bg-emerald-500/10 text-emerald-400 border border-emerald-500/20">
                60 FPS 极速直连
              </span>
            </div>

            <div class="p-3.5 rounded-xl bg-dark-850/60 border border-slate-800/80 flex items-center justify-between">
              <div class="flex items-center gap-3">
                <div class="text-2xl">📦</div>
                <div>
                  <div class="text-xs font-bold text-white">家庭 NAS 传输 (1GB 视频)</div>
                  <div class="text-[11px] text-slate-400">单机器 27 分钟 ➔ 聚合后大幅缩减</div>
                </div>
              </div>
              <span class="text-xs font-bold font-mono px-2 py-1 rounded bg-cyan-500/10 text-cyan-400 border border-cyan-500/20">
                仅需 {{ downloadDuration }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

const nodes = ref([
  { id: 1, name: '腾讯轻量云 (广州)', region: '国内低延时', bandwidth: 5, enabled: true, badgeClass: 'bg-blue-500/10 text-blue-300 border border-blue-500/20' },
  { id: 2, name: '阿里轻量云 (上海)', region: '骨干 BGP', bandwidth: 5, enabled: true, badgeClass: 'bg-amber-500/10 text-amber-300 border border-amber-500/20' },
  { id: 3, name: '华为云耀 (北京)', region: '稳定企业线', bandwidth: 10, enabled: true, badgeClass: 'bg-rose-500/10 text-rose-300 border border-rose-500/20' },
  { id: 4, name: '社区中继节点 #08', region: '志愿者贡献', bandwidth: 15, enabled: true, badgeClass: 'bg-emerald-500/10 text-emerald-300 border border-emerald-500/20' },
  { id: 5, name: '甲骨文海外 VPS (首尔/东京)', region: '海外大带宽', bandwidth: 25, enabled: false, badgeClass: 'bg-purple-500/10 text-purple-300 border border-purple-500/20' },
])

const activeNodeCount = computed(() => nodes.value.filter(n => n.enabled).length)

const totalBandwidth = computed(() => {
  return nodes.value.reduce((acc, cur) => cur.enabled ? acc + cur.bandwidth : acc, 0)
})

const speedMultiplier = computed(() => {
  const baseline = 5
  const multi = (totalBandwidth.value / baseline).toFixed(1)
  return multi > 0 ? multi : '1.0'
})

const equationText = computed(() => {
  const active = nodes.value.filter(n => n.enabled)
  if (active.length === 0) return '未启用任何中继节点 (0 Mbps)'
  const parts = active.map(n => `${n.bandwidth}M`)
  return `${parts.join(' + ')} = ${totalBandwidth.value} Mbps`
})

const downloadDuration = computed(() => {
  if (totalBandwidth.value <= 0) return '∞'
  const seconds = (1024 * 8) / totalBandwidth.value
  if (seconds < 60) {
    return `${Math.round(seconds)} 秒`
  }
  const minutes = (seconds / 60).toFixed(1)
  return `${minutes} 分钟`
})

const resetNodes = () => {
  nodes.value = [
    { id: 1, name: '腾讯轻量云 (广州)', region: '国内低延时', bandwidth: 5, enabled: true, badgeClass: 'bg-blue-500/10 text-blue-300 border border-blue-500/20' },
    { id: 2, name: '阿里轻量云 (上海)', region: '骨干 BGP', bandwidth: 5, enabled: true, badgeClass: 'bg-amber-500/10 text-amber-300 border border-amber-500/20' },
    { id: 3, name: '华为云耀 (北京)', region: '稳定企业线', bandwidth: 10, enabled: true, badgeClass: 'bg-rose-500/10 text-rose-300 border border-rose-500/20' },
    { id: 4, name: '社区中继节点 #08', region: '志愿者贡献', bandwidth: 15, enabled: true, badgeClass: 'bg-emerald-500/10 text-emerald-300 border border-emerald-500/20' },
    { id: 5, name: '甲骨文海外 VPS (首尔/东京)', region: '海外大带宽', bandwidth: 25, enabled: false, badgeClass: 'bg-purple-500/10 text-purple-300 border border-purple-500/20' },
  ]
}
</script>
