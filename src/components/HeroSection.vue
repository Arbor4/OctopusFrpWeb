<template>
  <section class="relative pt-32 pb-20 md:pt-40 md:pb-28 overflow-hidden">
    <!-- Ambient Background Glows -->
    <div class="absolute top-1/4 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[650px] h-[450px] bg-gradient-to-tr from-cyan-500/15 via-sky-500/10 to-violet-600/20 blur-[120px] rounded-full pointer-events-none"></div>
    <div class="absolute top-10 right-10 w-72 h-72 bg-violet-600/10 blur-[90px] rounded-full pointer-events-none"></div>
    <div class="absolute bottom-0 left-10 w-80 h-80 bg-cyan-600/10 blur-[100px] rounded-full pointer-events-none"></div>

    <!-- Background Grid Pattern -->
    <div class="absolute inset-0 bg-grid-pattern bg-[size:40px_40px] opacity-[0.18] pointer-events-none"></div>

    <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
      <!-- Top Pill Badge -->
      <div class="inline-flex items-center gap-2 px-3.5 py-1.5 rounded-full bg-cyan-950/60 border border-cyan-500/30 text-cyan-300 text-xs font-medium mb-8 backdrop-blur shadow-lg shadow-cyan-950/40 animate-float">
        <span class="flex h-2 w-2 relative">
          <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-cyan-400 opacity-75"></span>
          <span class="relative inline-flex rounded-full h-2 w-2 bg-cyan-500"></span>
        </span>
        <span>突破单台 VPS 限速瓶颈 · 多中继协同聚合时代到来</span>
        <span class="text-cyan-500/60">|</span>
        <span class="text-slate-400 hover:text-white transition-colors cursor-pointer">招募中继节点 🚀</span>
      </div>

      <!-- Main Headline -->
      <h1 class="text-4xl sm:text-6xl lg:text-7xl font-extrabold tracking-tight text-white mb-6">
        汇聚碎片带宽 <br class="hidden sm:inline" />
        <span class="bg-gradient-to-r from-cyan-400 via-sky-300 to-violet-400 bg-clip-text text-transparent">
          触达极限穿透
        </span>
      </h1>

      <!-- Subtitle Description -->
      <p class="max-w-3xl mx-auto text-base sm:text-xl text-slate-300 leading-relaxed mb-10 font-normal">
        你的便宜云主机（腾讯云 4M、阿里云 5M、华为云 10M、闲置海外 VPS）还在孤立沉睡？
        <span class="text-cyan-300 font-medium">OctopusFrp (八爪鱼穿透)</span>
        像八爪鱼触手般将多节点带宽跨网条带化并发聚合，让家宽 NAS 满速传输，让远程桌面告别卡顿！
      </p>

      <!-- CTA Buttons -->
      <div class="flex flex-col sm:flex-row items-center justify-center gap-4 mb-16">
        <a 
          href="#deploy" 
          class="w-full sm:w-auto px-8 py-4 rounded-xl font-bold text-sm bg-gradient-to-r from-cyan-400 via-sky-400 to-cyan-300 text-dark-950 hover:brightness-110 shadow-xl shadow-cyan-500/25 transition-all transform hover:-translate-y-1 flex items-center justify-center gap-2 group"
        >
          <svg class="w-5 h-5 transition-transform group-hover:scale-110" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" />
          </svg>
          <span>加入中转节点（一键部署）</span>
        </a>

        <a 
          href="#simulator" 
          class="w-full sm:w-auto px-8 py-4 rounded-xl font-semibold text-sm bg-dark-850/80 hover:bg-dark-800 text-slate-200 hover:text-white border border-slate-700/80 hover:border-cyan-500/50 transition-all transform hover:-translate-y-0.5 flex items-center justify-center gap-2 shadow-lg"
        >
          <svg class="w-5 h-5 text-cyan-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
          </svg>
          <span>试玩聚合模拟器</span>
        </a>

        <a 
          href="https://github.com/Arbor4/OctopusFrp" 
          target="_blank" 
          rel="noopener"
          class="w-full sm:w-auto px-6 py-4 rounded-xl font-medium text-sm text-slate-400 hover:text-slate-200 transition-colors flex items-center justify-center gap-2 hover:bg-white/5"
        >
          <span>了解架构源码</span>
          <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
          </svg>
        </a>
      </div>

      <!-- Live Network Metric Highlights -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-4 max-w-5xl mx-auto pt-6 border-t border-slate-800/80">
        <div class="glass-card rounded-2xl p-5 text-left border border-white/5 hover:border-cyan-500/30 transition-all">
          <div class="text-2xl sm:text-3xl font-extrabold text-cyan-400 font-mono tracking-tight flex items-center gap-1">
            <span>Σ Bandwidth</span>
          </div>
          <p class="text-xs text-slate-400 mt-1">突破单机限速上限</p>
          <div class="mt-2 text-xs font-mono text-cyan-300/80 bg-cyan-950/40 px-2 py-0.5 rounded inline-block">
            5M + 5M + 10M = 20M+
          </div>
        </div>

        <div class="glass-card rounded-2xl p-5 text-left border border-white/5 hover:border-violet-500/30 transition-all">
          <div class="text-2xl sm:text-3xl font-extrabold text-violet-400 font-mono tracking-tight flex items-center gap-1">
            <span>&lt; 15 MB</span>
          </div>
          <p class="text-xs text-slate-400 mt-1">中继常驻超低内存</p>
          <div class="mt-2 text-xs font-mono text-violet-300/80 bg-violet-950/40 px-2 py-0.5 rounded inline-block">
            1C512M VPS 零负担
          </div>
        </div>

        <div class="glass-card rounded-2xl p-5 text-left border border-white/5 hover:border-sky-500/30 transition-all">
          <div class="text-2xl sm:text-3xl font-extrabold text-sky-400 font-mono tracking-tight flex items-center gap-1">
            <span>0 ms</span>
          </div>
          <p class="text-xs text-slate-400 mt-1">宕机平滑熔断自愈</p>
          <div class="mt-2 text-xs font-mono text-sky-300/80 bg-sky-950/40 px-2 py-0.5 rounded inline-block">
            单点 VPS 宕机业务不掉线
          </div>
        </div>

        <div class="glass-card rounded-2xl p-5 text-left border border-white/5 hover:border-emerald-500/30 transition-all">
          <div class="text-2xl sm:text-3xl font-extrabold text-emerald-400 font-mono tracking-tight flex items-center gap-1">
            <span>E2EE TLS</span>
          </div>
          <p class="text-xs text-slate-400 mt-1">端到端全链路加密</p>
          <div class="mt-2 text-xs font-mono text-emerald-300/80 bg-emerald-950/40 px-2 py-0.5 rounded inline-block">
            中继节点只转发无权解密
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
