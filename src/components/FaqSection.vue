<template>
  <section id="faq" class="py-24 relative border-t border-white/5 bg-dark-950">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Header -->
      <div class="text-center mb-16">
        <div class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-violet-950/60 border border-violet-500/30 text-violet-300 text-xs font-mono uppercase tracking-wider mb-4">
          <span>💬 解除一切顾虑</span>
        </div>
        <h2 class="text-3xl sm:text-4xl font-extrabold text-white tracking-tight">
          常见问题与解答 (FAQ)
        </h2>
        <p class="mt-4 text-slate-400 text-base">
          关于中转节点部署、数据隐私保护、流量控制与运行机制的解答。
        </p>
      </div>

      <!-- FAQ Accordion -->
      <div class="space-y-4">
        <div 
          v-for="(item, idx) in faqs" 
          :key="idx"
          class="glass-card rounded-2xl border border-white/5 overflow-hidden transition-all duration-200"
          :class="openIndex === idx ? 'border-cyan-500/40 bg-dark-850/80 shadow-lg shadow-cyan-950/30' : 'hover:border-white/10'"
        >
          <button 
            @click="toggle(idx)"
            class="w-full px-6 py-5 text-left flex items-center justify-between gap-4 focus:outline-none"
          >
            <span class="text-sm sm:text-base font-bold text-white flex items-center gap-3">
              <span class="text-cyan-400 font-mono text-sm font-semibold">0{{ idx + 1 }}.</span>
              <span>{{ item.q }}</span>
            </span>
            <span class="p-1 rounded-lg bg-dark-900 text-slate-400 transition-transform duration-200" :class="{ 'rotate-180 text-cyan-400': openIndex === idx }">
              <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
              </svg>
            </span>
          </button>

          <div 
            v-show="openIndex === idx" 
            class="px-6 pb-6 pt-1 text-sm text-slate-300 leading-relaxed border-t border-slate-800/60"
          >
            {{ item.a }}
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const openIndex = ref(0)

const toggle = (idx) => {
  openIndex.value = openIndex.value === idx ? -1 : idx
}

const faqs = [
  {
    q: '我贡献做中继节点，会不会被耗尽云服务器的流量？',
    a: '绝对不会。OctopusFrp 提供了严格的带宽限额声明机制（例如限制为 3Mbps 或 5Mbps），内核会执行平滑加权排队控制，绝不无节制超跑。同时您也可以根据云厂商每月的免费额度，随时在配置文件中调小限速。'
  },
  {
    q: '中转节点能否看到穿透用户的传输数据内容？会有隐私风险吗？',
    a: '完全无法看到。所有经过中继的数据流均在主控端与被控端之间建立端到端 TLS/mTLS 加密，并由 Striping 切片引擎打散为带序列号的纯二进制数据块。中转节点在物理上仅扮演无状态的分片路由中转角色，没有任何私钥进行解密，代码完全开源接受任何审计。'
  },
  {
    q: '对中继 VPS 的配置有严格要求吗？内存占用大不大？',
    a: '门槛极低！服务端核心代码完全采用 Go 语言静态编译，去除了任何无意义的重型依赖。在生产测试中，常驻内存仅占 10MB ~ 15MB 左右，CPU 占用基本低于 1%。即便是一台仅有 1核 256MB 内存的超低配轻量机也能零压力运行。'
  },
  {
    q: '如果有某个中继节点突然断网或者宕机，穿透会卡死吗？',
    a: '完全不会。OctopusFrp 吸收了 HypoMux 的动态调度哲学，当向某一中转节点的 TCP 管道写入失败时，会立即触发 2s / 5s / 15s / 30s 指数退避与自动隔离熔断机制，并在数毫秒内将数据重传分派至其余正常运转的中继节点，用户业务（如 RDP、SSH、网页浏览）保持持续无感。'
  },
  {
    q: '如果我以后不想当中继了，如何停止或卸载？',
    a: '只需在终端中执行 sudo systemctl stop octopus-server 并禁用服务即可瞬间下线；若想完全清除，运行配套的卸载命令即可彻底删除二进制与配置，不残留任何后台守护进程。'
  }
]
</script>
