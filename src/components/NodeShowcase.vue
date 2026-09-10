<template>
  <section id="nodes" class="py-24 relative border-t border-white/5 bg-dark-900/30">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-16">
        <div class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-sky-950/60 border border-sky-500/30 text-sky-300 text-xs font-mono uppercase tracking-wider mb-4">
          <span>🌐 互联分布式网格</span>
        </div>
        <h2 class="text-3xl sm:text-4xl font-extrabold text-white tracking-tight">
          活跃中继生态与节点态势
        </h2>
        <p class="mt-4 text-slate-400 text-base sm:text-lg">
          散落在各地的低成本云服务器正通过 OctopusFrp 织就一张高可用、自愈容灾的弹性聚合网。
        </p>
      </div>

      <!-- Network Overview Bar -->
      <div class="glass-card rounded-2xl p-6 mb-10 border border-white/10 grid grid-cols-2 md:grid-cols-4 gap-6 text-center">
        <div>
          <div class="text-xs text-slate-400 font-mono uppercase">当前在线中继</div>
          <div class="text-2xl sm:text-3xl font-extrabold text-white font-mono mt-1 flex items-center justify-center gap-1.5">
            <span class="w-2.5 h-2.5 rounded-full bg-emerald-400 animate-pulse"></span>
            <span>18 台</span>
          </div>
          <p class="text-[11px] text-emerald-400/80 mt-0.5">覆盖 9 个核心网络骨干区</p>
        </div>
        <div>
          <div class="text-xs text-slate-400 font-mono uppercase">全网聚合总带宽</div>
          <div class="text-2xl sm:text-3xl font-extrabold text-cyan-400 font-mono mt-1">
            215 Mbps
          </div>
          <p class="text-[11px] text-cyan-400/80 mt-0.5">多链路条带化调度中</p>
        </div>
        <div>
          <div class="text-xs text-slate-400 font-mono uppercase">平均心跳延迟</div>
          <div class="text-2xl sm:text-3xl font-extrabold text-violet-400 font-mono mt-1">
            21.4 ms
          </div>
          <p class="text-[11px] text-violet-400/80 mt-0.5">SWRR 动态优选低延迟链路</p>
        </div>
        <div>
          <div class="text-xs text-slate-400 font-mono uppercase">链路容灾切换</div>
          <div class="text-2xl sm:text-3xl font-extrabold text-emerald-400 font-mono mt-1">
            &lt; 50 ms
          </div>
          <p class="text-[11px] text-emerald-400/80 mt-0.5">单节点宕机业务无感</p>
        </div>
      </div>

      <!-- Simulated Relay Node Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div 
          v-for="item in relayList" 
          :key="item.id"
          class="glass-card rounded-2xl p-5 border border-white/5 hover:border-cyan-500/30 transition-all duration-300 relative group overflow-hidden"
        >
          <!-- Hover accent glow -->
          <div class="absolute -right-6 -bottom-6 w-24 h-24 bg-cyan-500/10 rounded-full blur-xl group-hover:bg-cyan-500/20 transition-colors"></div>

          <div class="flex items-start justify-between mb-3">
            <div class="flex items-center gap-2.5">
              <div class="text-2xl">{{ item.flag }}</div>
              <div>
                <h4 class="text-sm font-bold text-white group-hover:text-cyan-300 transition-colors">
                  {{ item.name }}
                </h4>
                <p class="text-xs text-slate-400 font-mono">{{ item.provider }} · {{ item.location }}</p>
              </div>
            </div>
            <span class="inline-flex items-center gap-1 text-[11px] font-mono px-2 py-0.5 rounded-full bg-emerald-950/60 border border-emerald-500/30 text-emerald-400">
              <span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span>
              {{ item.status }}
            </span>
          </div>

          <!-- Specs -->
          <div class="grid grid-cols-3 gap-2 py-3 px-3 rounded-xl bg-dark-950/60 border border-slate-800/80 font-mono text-center">
            <div>
              <span class="text-[10px] text-slate-500 block">贡献限额</span>
              <span class="text-xs font-bold text-cyan-400">{{ item.bandwidth }}</span>
            </div>
            <div>
              <span class="text-[10px] text-slate-500 block">探测延时</span>
              <span class="text-xs font-bold text-slate-200">{{ item.ping }}</span>
            </div>
            <div>
              <span class="text-[10px] text-slate-500 block">健康评分</span>
              <span class="text-xs font-bold text-emerald-400">{{ item.health }}</span>
            </div>
          </div>

          <!-- Bottom Info -->
          <div class="mt-3 flex items-center justify-between text-[11px] text-slate-400">
            <span>调度算法：SWRR 权重 {{ item.weight }}</span>
            <span class="text-slate-500 font-mono">{{ item.uptime }} 连续在线</span>
          </div>
        </div>
      </div>

      <!-- Bottom Invite Card -->
      <div class="mt-12 text-center p-8 rounded-2xl glass-card border border-cyan-500/30 bg-gradient-to-r from-cyan-950/30 via-slate-900/60 to-violet-950/30">
        <h3 class="text-xl font-bold text-white mb-2">想要你的服务器也列入中继网络？</h3>
        <p class="text-sm text-slate-300 max-w-2xl mx-auto mb-6">
          仅需在你的机器上运行一键脚本，填写节点标识与最大带宽，即可加入 OctopusFrp 聚合大家庭。
        </p>
        <a 
          href="#deploy" 
          class="inline-flex items-center gap-2 px-6 py-3 rounded-xl font-bold text-xs bg-gradient-to-r from-cyan-400 to-sky-400 text-dark-950 hover:brightness-110 shadow-lg shadow-cyan-500/20 transition-all"
        >
          <span>立即生成部署指令</span>
          <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M14 5l7 7m0 0l-7 7m7-7H3" />
          </svg>
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const relayList = ref([
  {
    id: 1,
    flag: '🇨🇳',
    name: 'relay-tencent-gz-01',
    provider: '腾讯轻量云',
    location: '广州 BGP',
    bandwidth: '5 Mbps',
    ping: '14 ms',
    health: '100分',
    weight: 5,
    uptime: '16天',
    status: '在线'
  },
  {
    id: 2,
    flag: '🇨🇳',
    name: 'relay-aliyun-sh-02',
    provider: '阿里轻量云',
    location: '上海华东',
    bandwidth: '5 Mbps',
    ping: '18 ms',
    health: '99分',
    weight: 5,
    uptime: '32天',
    status: '在线'
  },
  {
    id: 3,
    flag: '🇨🇳',
    name: 'relay-huawei-bj-01',
    provider: '华为云耀',
    location: '北京华北',
    bandwidth: '10 Mbps',
    ping: '22 ms',
    health: '100分',
    weight: 10,
    uptime: '45天',
    status: '在线'
  },
  {
    id: 4,
    flag: '🇨🇳',
    name: 'relay-community-cd',
    provider: '社区志愿者',
    location: '四川成都',
    bandwidth: '20 Mbps',
    ping: '29 ms',
    health: '98分',
    weight: 20,
    uptime: '8天',
    status: '在线'
  },
  {
    id: 5,
    flag: '🇯🇵',
    name: 'relay-tokyo-edge',
    provider: 'AWS Lightsail',
    location: '日本东京',
    bandwidth: '30 Mbps',
    ping: '48 ms',
    health: '99分',
    weight: 30,
    uptime: '60天',
    status: '在线'
  },
  {
    id: 6,
    flag: '🇩🇪',
    name: 'relay-frankfurt-vps',
    provider: 'Hetzner Cloud',
    location: '德国法兰克福',
    bandwidth: '50 Mbps',
    ping: '135 ms',
    health: '97分',
    weight: 50,
    uptime: '19天',
    status: '在线'
  }
])
</script>
