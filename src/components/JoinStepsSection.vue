<template>
  <section id="how-it-works" class="py-24 relative border-t border-white/5 bg-dark-900/50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-20">
        <div class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-emerald-950/60 border border-emerald-500/30 text-emerald-300 text-xs font-mono uppercase tracking-wider mb-4">
          <span>🚀 零门槛接入</span>
        </div>
        <h2 class="text-3xl sm:text-4xl font-extrabold text-white tracking-tight">
          仅需 3 步，点亮你的中转节点
        </h2>
        <p class="mt-4 text-slate-400 text-base sm:text-lg">
          无论是一台吃灰的 1 核 512MB 便宜 VPS，还是带有公网 IP 的闲置服务器，都能立刻变身成为高可用穿透中继。
        </p>
      </div>

      <!-- 3 Steps Grid -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 relative">
        <!-- Connecting Line (Desktop) -->
        <div class="hidden md:block absolute top-1/2 left-1/4 right-1/4 h-0.5 bg-gradient-to-r from-cyan-500/20 via-violet-500/40 to-cyan-500/20 -translate-y-12 z-0 pointer-events-none"></div>

        <!-- Step 1 -->
        <div class="glass-card rounded-2xl p-8 border border-white/10 relative z-10 hover:border-cyan-500/40 transition-all group">
          <div class="flex items-center justify-between mb-6">
            <div class="w-12 h-12 rounded-xl bg-cyan-500/10 border border-cyan-500/30 flex items-center justify-center text-cyan-400 font-mono font-bold text-lg group-hover:scale-110 transition-transform">
              01
            </div>
            <span class="text-xs font-mono text-cyan-400/80 bg-cyan-950/60 px-2.5 py-1 rounded-full border border-cyan-500/20">
              准备节点环境
            </span>
          </div>
          <h3 class="text-lg font-bold text-white mb-2">准备任意公网机器</h3>
          <p class="text-sm text-slate-400 leading-relaxed mb-4">
            任何拥有公网固定 IP 的 Linux VPS、云服务器（Ubuntu / Debian / CentOS / Alpine）或 Windows 主机。
          </p>
          <div class="p-3 rounded-lg bg-dark-950/70 border border-slate-800 text-xs text-slate-400 space-y-1">
            <div class="flex items-center justify-between">
              <span>最低 CPU：</span>
              <span class="font-mono text-slate-300">1 vCPU</span>
            </div>
            <div class="flex items-center justify-between">
              <span>最低内存：</span>
              <span class="font-mono text-slate-300">256 MB (实测仅占 &lt;15M)</span>
            </div>
            <div class="flex items-center justify-between">
              <span>带宽要求：</span>
              <span class="font-mono text-slate-300">1 Mbps 起步皆可</span>
            </div>
          </div>
        </div>

        <!-- Step 2 -->
        <div class="glass-card rounded-2xl p-8 border border-white/10 relative z-10 hover:border-violet-500/40 transition-all group">
          <div class="flex items-center justify-between mb-6">
            <div class="w-12 h-12 rounded-xl bg-violet-500/10 border border-violet-500/30 flex items-center justify-center text-violet-400 font-mono font-bold text-lg group-hover:scale-110 transition-transform">
              02
            </div>
            <span class="text-xs font-mono text-violet-400/80 bg-violet-950/60 px-2.5 py-1 rounded-full border border-violet-500/20">
              定制专属配置
            </span>
          </div>
          <h3 class="text-lg font-bold text-white mb-2">生成个性化参数</h3>
          <p class="text-sm text-slate-400 leading-relaxed mb-4">
            在下方生成器中输入你的节点别名（如 <code class="text-violet-300">bj-relay-01</code>）与允许贡献的最大带宽上限，绝不超跑你的原业务流量。
          </p>
          <div class="p-3 rounded-lg bg-dark-950/70 border border-slate-800 text-xs text-slate-400 space-y-1">
            <div class="flex items-center justify-between">
              <span>防跑满保护：</span>
              <span class="font-mono text-violet-300">可自定义硬限速</span>
            </div>
            <div class="flex items-center justify-between">
              <span>通信端口：</span>
              <span class="font-mono text-slate-300">默认 7000 (可自选)</span>
            </div>
            <div class="flex items-center justify-between">
              <span>认证方式：</span>
              <span class="font-mono text-slate-300">Cluster Token 鉴权</span>
            </div>
          </div>
        </div>

        <!-- Step 3 -->
        <div class="glass-card rounded-2xl p-8 border border-white/10 relative z-10 hover:border-emerald-500/40 transition-all group">
          <div class="flex items-center justify-between mb-6">
            <div class="w-12 h-12 rounded-xl bg-emerald-500/10 border border-emerald-500/30 flex items-center justify-center text-emerald-400 font-mono font-bold text-lg group-hover:scale-110 transition-transform">
              03
            </div>
            <span class="text-xs font-mono text-emerald-400/80 bg-emerald-950/60 px-2.5 py-1 rounded-full border border-emerald-500/20">
              一键执行上线
            </span>
          </div>
          <h3 class="text-lg font-bold text-white mb-2">一键部署并开机常驻</h3>
          <p class="text-sm text-slate-400 leading-relaxed mb-4">
            复制一键安装指令到终端粘贴运行。脚本将自动创建隔离用户、配置 Systemd 服务并开启自动保活守护。
          </p>
          <div class="p-3 rounded-lg bg-dark-950/70 border border-slate-800 text-xs text-slate-400 space-y-1">
            <div class="flex items-center justify-between">
              <span>运行权限：</span>
              <span class="font-mono text-emerald-300">低权限 octopus 专用用户</span>
            </div>
            <div class="flex items-center justify-between">
              <span>故障重启：</span>
              <span class="font-mono text-slate-300">Systemd Always 自动恢复</span>
            </div>
            <div class="flex items-center justify-between">
              <span>随时卸载：</span>
              <span class="font-mono text-slate-300">支持一键清理与停止</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
