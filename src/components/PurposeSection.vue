<template>
  <section id="purpose" class="py-24 relative border-t border-white/5 bg-dark-900/40">
    <!-- Section Header -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center max-w-3xl mx-auto mb-16">
        <div class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-violet-950/60 border border-violet-500/30 text-violet-300 text-xs font-mono uppercase tracking-wider mb-4">
          <span>🤝 互惠互利 · 众筹带宽</span>
        </div>
        <h2 class="text-3xl sm:text-4xl font-extrabold text-white tracking-tight">
          为什么希望大家加入中转节点？
        </h2>
        <p class="mt-4 text-slate-400 text-base sm:text-lg">
          在网络世界中，单台廉价云服务器的 3~5 Mbps 宛如孤岛水滴；<br class="hidden sm:inline" />
          当分散的节点连接在一起，便是一场颠覆传统的带宽聚合革命。
        </p>
      </div>

      <!-- Problem vs Solution Comparison Card -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-16">
        <!-- The Homelab Dilemma -->
        <div class="glass-card rounded-2xl p-7 border border-rose-500/20 bg-gradient-to-b from-rose-950/20 to-transparent relative overflow-hidden">
          <div class="absolute top-0 right-0 transform translate-x-4 -translate-y-4 w-32 h-32 bg-rose-500/10 rounded-full blur-2xl"></div>
          <div class="flex items-center gap-3 mb-5">
            <div class="w-10 h-10 rounded-xl bg-rose-500/20 border border-rose-500/30 flex items-center justify-center text-rose-400 text-xl font-bold">
              ✕
            </div>
            <div>
              <h3 class="text-lg font-bold text-white">传统内网穿透的无奈与痛点</h3>
              <p class="text-xs text-rose-300/80">传统 FRP 架构 1 对 1 绑定的天然局限</p>
            </div>
          </div>
          <ul class="space-y-3.5 text-sm text-slate-300">
            <li class="flex items-start gap-3">
              <span class="text-rose-400 font-bold mt-0.5">•</span>
              <div>
                <strong class="text-white">家宽带宽富余却被封锁：</strong>
                家庭 NAS、机房工控机上行往往有 30M~100M，但苦于无公网固定 IPv4，不得不依靠云端中继。
              </div>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-rose-400 font-bold mt-0.5">•</span>
              <div>
                <strong class="text-white">云 VPS 贫瘠碎片：</strong>
                廉价轻量服务器单台仅 3~5 Mbps。拉大文件速度被死死锁在几百 KB/s，远程桌面 (RDP) 画面撕裂拖拽卡顿。
              </div>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-rose-400 font-bold mt-0.5">•</span>
              <div>
                <strong class="text-white">单点故障断联风险：</strong>
                中继 VPS 一旦网络抖动或服务宕机，整个内网穿透完全断线，运维手忙脚乱。
              </div>
            </li>
          </ul>
        </div>

        <!-- The OctopusFrp Vision -->
        <div class="glass-card rounded-2xl p-7 border border-cyan-500/30 bg-gradient-to-b from-cyan-950/20 to-transparent relative overflow-hidden">
          <div class="absolute top-0 right-0 transform translate-x-4 -translate-y-4 w-32 h-32 bg-cyan-500/10 rounded-full blur-2xl"></div>
          <div class="flex items-center gap-3 mb-5">
            <div class="w-10 h-10 rounded-xl bg-cyan-500/20 border border-cyan-500/30 flex items-center justify-center text-cyan-400 text-xl font-bold">
              ✓
            </div>
            <div>
              <h3 class="text-lg font-bold text-white">OctopusFrp 多触手聚合革命</h3>
              <p class="text-xs text-cyan-300/80">八爪鱼跨地域条带化聚合与自愈网格</p>
            </div>
          </div>
          <ul class="space-y-3.5 text-sm text-slate-300">
            <li class="flex items-start gap-3">
              <span class="text-cyan-400 font-bold mt-0.5">•</span>
              <div>
                <strong class="text-white">带宽叠加强化（1+1 &gt; 2）：</strong>
                将腾讯云 4M + 阿里云 5M + 华为云 10M + 闲置 VPS 并行调度，聚合后直接突破到 30M~50Mbps 飞速体验！
              </div>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-cyan-400 font-bold mt-0.5">•</span>
              <div>
                <strong class="text-white">单流切片与乱序重排：</strong>
                独创数据链路层分片算法（Striping Engine），哪怕单线程大文件也能跨节点并发回传。
              </div>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-cyan-400 font-bold mt-0.5">•</span>
              <div>
                <strong class="text-white">毫秒级故障平滑转移：</strong>
                任何一台节点掉线，SWRR 调度器毫秒级将其隔离退避，剩余健康节点无缝承载流量，服务永不中断。
              </div>
            </li>
          </ul>
        </div>
      </div>

      <!-- Core Pillars: Why Everyone Should Contribute -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <!-- Card 1 -->
        <div class="glass-card rounded-2xl p-6 border border-white/5 hover:border-cyan-500/40 transition-all group">
          <div class="w-12 h-12 rounded-xl bg-cyan-500/10 border border-cyan-500/20 flex items-center justify-center text-cyan-400 mb-4 group-hover:scale-110 transition-transform">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z" />
            </svg>
          </div>
          <h3 class="text-base font-bold text-white mb-2">人人为我，我为人人</h3>
          <p class="text-sm text-slate-400 leading-relaxed">
            大多数人手头都有 1~2 台每月大量闲置流量的轻量 VPS。拿出 2~5Mbps 的空闲带宽贡献给聚合池，当你自己外出访问内网时，就能享受整个网络带来的数倍聚合提速。
          </p>
        </div>

        <!-- Card 2 -->
        <div class="glass-card rounded-2xl p-6 border border-white/5 hover:border-violet-500/40 transition-all group">
          <div class="w-12 h-12 rounded-xl bg-violet-500/10 border border-violet-500/20 flex items-center justify-center text-violet-400 mb-4 group-hover:scale-110 transition-transform">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
            </svg>
          </div>
          <h3 class="text-base font-bold text-white mb-2">绝对纯净，零信任安全</h3>
          <p class="text-sm text-slate-400 leading-relaxed">
            数据在客户端通过 TLS/mTLS 端到端加密并切片打碎。中转节点只负责纯数据帧转交，既无法嗅探内容，也无法伪造数据包，代码完全开源透明，放心中转。
          </p>
        </div>

        <!-- Card 3 -->
        <div class="glass-card rounded-2xl p-6 border border-white/5 hover:border-emerald-500/40 transition-all group">
          <div class="w-12 h-12 rounded-xl bg-emerald-500/10 border border-emerald-500/20 flex items-center justify-center text-emerald-400 mb-4 group-hover:scale-110 transition-transform">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" />
            </svg>
          </div>
          <h3 class="text-base font-bold text-white mb-2">超低开销，随心限速</h3>
          <p class="text-sm text-slate-400 leading-relaxed">
            Go 原生高并发架构，常驻内存仅需十余兆。通过配置文件或部署脚本，你可以自由限制贡献的最大带宽（如仅 3Mbps），不影响服务器原本跑的其他业务。
          </p>
        </div>
      </div>
    </div>
  </section>
</template>
