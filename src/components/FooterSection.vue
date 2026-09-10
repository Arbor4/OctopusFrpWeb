<template>
  <footer class="bg-dark-950 border-t border-slate-800/80 pt-16 pb-12">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid grid-cols-1 md:grid-cols-4 gap-10 pb-12 border-b border-slate-800">
        <!-- Col 1: Brand -->
        <div class="md:col-span-2 space-y-4">
          <div class="flex items-center gap-2.5">
            <span class="text-3xl">🐙</span>
            <span class="font-black text-xl tracking-tight bg-gradient-to-r from-cyan-400 to-violet-400 bg-clip-text text-transparent">
              OctopusFrp
            </span>
          </div>
          <p class="text-sm text-slate-400 max-w-md leading-relaxed">
            基于多服务器带宽聚合的高性能分布式内网穿透系统。通过跨公网数据包分片条带化与动态 SWRR 加权调度，彻底打破单台廉价云服务器的带宽枷锁。
          </p>
          <div class="text-xs text-slate-500 font-mono">
            开源协议：MIT License | Powered by Go & Vue 3
          </div>
        </div>

        <!-- Col 2: Navigation -->
        <div>
          <h4 class="text-xs font-bold text-white uppercase tracking-wider font-mono mb-4">快速导航</h4>
          <ul class="space-y-2.5 text-sm text-slate-400">
            <li><a href="#purpose" class="hover:text-cyan-400 transition-colors">为什么加入中转</a></li>
            <li><a href="#simulator" class="hover:text-cyan-400 transition-colors">带宽聚合模拟器</a></li>
            <li><a href="#how-it-works" class="hover:text-cyan-400 transition-colors">三步加入指南</a></li>
            <li><a href="#deploy" class="hover:text-cyan-400 transition-colors">一键部署生成器</a></li>
            <li><a href="#nodes" class="hover:text-cyan-400 transition-colors">活跃中继节点</a></li>
          </ul>
        </div>

        <!-- Col 3: Community & Source -->
        <div>
          <h4 class="text-xs font-bold text-white uppercase tracking-wider font-mono mb-4">社区与生态</h4>
          <ul class="space-y-2.5 text-sm text-slate-400">
            <li>
              <a 
                href="https://github.com/Arbor4/OctopusFrp" 
                target="_blank" 
                rel="noopener"
                class="hover:text-cyan-400 transition-colors flex items-center gap-1.5"
              >
                <span>GitHub 仓库</span>
                <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
                </svg>
              </a>
            </li>
            <li>
              <a 
                href="https://github.com/Arbor4/OctopusFrp#readme" 
                target="_blank" 
                rel="noopener"
                class="hover:text-cyan-400 transition-colors"
              >
                技术架构全景白皮书
              </a>
            </li>
            <li>
              <a 
                href="https://github.com/Arbor4/OctopusFrp/issues" 
                target="_blank" 
                rel="noopener"
                class="hover:text-cyan-400 transition-colors"
              >
                提交 Issue / 需求反馈
              </a>
            </li>
          </ul>
        </div>
      </div>

      <!-- Bottom copyright & back to top -->
      <div class="pt-8 flex flex-col sm:flex-row items-center justify-between gap-4 text-xs text-slate-500">
        <div>
          © 2026 OctopusFrp Open Source Community. 保留所有权利。
        </div>
        <div class="flex items-center gap-6">
          <a href="#" class="hover:text-slate-300 transition-colors flex items-center gap-1">
            <span>回到顶部</span>
            <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 10l7-7m0 0l7 7m-7-7v18" />
            </svg>
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>
