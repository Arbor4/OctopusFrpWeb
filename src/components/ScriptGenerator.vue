<template>
  <section id="deploy" class="py-24 relative overflow-hidden bg-dark-950">
    <!-- Ambient light glow -->
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[700px] h-[500px] bg-gradient-to-tr from-cyan-500/10 via-violet-500/10 to-transparent blur-[140px] pointer-events-none"></div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-16">
        <div class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-cyan-950/60 border border-cyan-500/30 text-cyan-300 text-xs font-mono uppercase tracking-wider mb-4">
          <span>⚙️ 自动化配置生成器</span>
        </div>
        <h2 class="text-3xl sm:text-4xl font-extrabold text-white tracking-tight">
          一键部署脚本与节点配置生成
        </h2>
        <p class="mt-4 text-slate-400 text-base sm:text-lg">
          填写你的机器参数，即可实时生成定制化部署脚本。免去繁琐配置，终端单行命令秒级启动。
        </p>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
        <!-- Configuration Form (5 cols) -->
        <div class="lg:col-span-5 glass-card rounded-2xl p-6 sm:p-7 border border-white/10 space-y-6">
          <div class="flex items-center justify-between pb-4 border-b border-slate-800">
            <h3 class="text-base font-bold text-white flex items-center gap-2">
              <svg class="w-4 h-4 text-cyan-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4" />
              </svg>
              <span>节点定制参数</span>
            </h3>
            <span class="text-xs text-slate-400 font-mono">实时联动生成</span>
          </div>

          <!-- Platform Selector Tabs -->
          <div>
            <label class="block text-xs font-medium text-slate-300 mb-2">运行环境 / 架构</label>
            <div class="grid grid-cols-3 gap-2 p-1 bg-dark-900/90 rounded-xl border border-slate-800">
              <button 
                v-for="p in platforms" 
                :key="p.id"
                @click="selectedPlatform = p.id"
                class="py-2 px-2 text-xs font-medium rounded-lg transition-all flex items-center justify-center gap-1.5"
                :class="selectedPlatform === p.id 
                  ? 'bg-cyan-500/20 text-cyan-300 border border-cyan-500/40 shadow-sm' 
                  : 'text-slate-400 hover:text-slate-200'"
              >
                <span>{{ p.icon }}</span>
                <span>{{ p.label }}</span>
              </button>
            </div>
          </div>

          <!-- Form Fields -->
          <div class="space-y-4">
            <!-- Node ID -->
            <div>
              <div class="flex justify-between items-center mb-1.5">
                <label class="text-xs font-medium text-slate-300">中继节点唯一标识 (Node ID)</label>
                <span class="text-[11px] text-slate-500">建议标注机房/地区</span>
              </div>
              <div class="relative">
                <input 
                  type="text" 
                  v-model="nodeId" 
                  class="w-full bg-dark-900 border border-slate-700/80 rounded-xl px-3.5 py-2.5 text-sm text-white font-mono placeholder-slate-600 focus:outline-none focus:border-cyan-500 focus:ring-1 focus:ring-cyan-500"
                  placeholder="例如: relay-shanghai-01"
                />
              </div>
            </div>

            <!-- Bandwidth Limit -->
            <div>
              <div class="flex justify-between items-center mb-1.5">
                <label class="text-xs font-medium text-slate-300">共享带宽上限 (Bandwidth Limit)</label>
                <span class="text-xs font-mono text-cyan-400 font-bold">{{ bandwidthLimit }} Mbps</span>
              </div>
              <div class="flex items-center gap-3">
                <input 
                  type="range" 
                  min="1" 
                  max="100" 
                  v-model.number="bandwidthLimit"
                  class="w-full h-1.5 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-cyan-400"
                />
              </div>
              <p class="text-[11px] text-slate-500 mt-1">防止中继突发占满您的服务器原始业务宽带</p>
            </div>

            <!-- Bind Port -->
            <div>
              <div class="flex justify-between items-center mb-1.5">
                <label class="text-xs font-medium text-slate-300">服务监听端口 (Bind Port)</label>
                <span class="text-[11px] text-slate-500">防火墙需放行 TCP</span>
              </div>
              <input 
                type="number" 
                v-model.number="bindPort" 
                class="w-full bg-dark-900 border border-slate-700/80 rounded-xl px-3.5 py-2.5 text-sm text-white font-mono focus:outline-none focus:border-cyan-500 focus:ring-1 focus:ring-cyan-500"
              />
            </div>

            <!-- Auth Token -->
            <div>
              <div class="flex justify-between items-center mb-1.5">
                <label class="text-xs font-medium text-slate-300">集群认证 Token</label>
                <button 
                  @click="generateRandomToken" 
                  class="text-[11px] text-cyan-400 hover:text-cyan-300 font-mono flex items-center gap-1"
                >
                  <svg class="w-3 h-3" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                  </svg>
                  随机生成
                </button>
              </div>
              <input 
                type="text" 
                v-model="authToken" 
                class="w-full bg-dark-900 border border-slate-700/80 rounded-xl px-3.5 py-2.5 text-sm text-white font-mono focus:outline-none focus:border-cyan-500 focus:ring-1 focus:ring-cyan-500"
              />
            </div>
          </div>
        </div>

        <!-- Generated Output & Code Tabs (7 cols) -->
        <div class="lg:col-span-7 space-y-4">
          <!-- Code Block Card -->
          <div class="glass-card rounded-2xl border border-white/10 overflow-hidden shadow-2xl">
            <!-- Code Tab Header -->
            <div class="bg-dark-900/90 px-4 py-3 border-b border-slate-800 flex items-center justify-between">
              <div class="flex items-center gap-2">
                <button 
                  @click="activeView = 'command'"
                  class="text-xs font-medium px-3 py-1.5 rounded-lg transition-colors"
                  :class="activeView === 'command' ? 'bg-cyan-500/20 text-cyan-300 border border-cyan-500/30' : 'text-slate-400 hover:text-slate-200'"
                >
                  一键安装命令
                </button>
                <button 
                  @click="activeView = 'config'"
                  class="text-xs font-medium px-3 py-1.5 rounded-lg transition-colors"
                  :class="activeView === 'config' ? 'bg-cyan-500/20 text-cyan-300 border border-cyan-500/30' : 'text-slate-400 hover:text-slate-200'"
                >
                  配置预览 (octopus-server.toml)
                </button>
                <button 
                  @click="activeView = 'manage'"
                  class="text-xs font-medium px-3 py-1.5 rounded-lg transition-colors hidden sm:inline-block"
                  :class="activeView === 'manage' ? 'bg-cyan-500/20 text-cyan-300 border border-cyan-500/30' : 'text-slate-400 hover:text-slate-200'"
                >
                  管理指令
                </button>
              </div>

              <!-- Copy Button -->
              <button 
                @click="copyContent"
                class="flex items-center gap-1.5 px-3 py-1.5 rounded-lg text-xs font-mono font-medium transition-all"
                :class="copied 
                  ? 'bg-emerald-500/20 text-emerald-300 border border-emerald-500/40' 
                  : 'bg-dark-800 hover:bg-dark-700 text-slate-300 hover:text-white border border-slate-700'"
              >
                <svg v-if="!copied" class="w-3.5 h-3.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z" />
                </svg>
                <svg v-else class="w-3.5 h-3.5 text-emerald-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
                </svg>
                <span>{{ copied ? '已复制到剪贴板！' : '复制代码' }}</span>
              </button>
            </div>

            <!-- Code Content Body -->
            <div class="p-4 sm:p-6 bg-dark-950/90 font-mono text-xs sm:text-sm text-slate-200 overflow-x-auto min-h-[260px] max-h-[420px]">
              <!-- View 1: One-Click Command -->
              <div v-if="activeView === 'command'" class="space-y-4">
                <div class="text-slate-500 text-xs select-none">
                  # 在你的公网服务器终端直接执行以下指令（支持 root 或 sudo）：
                </div>
                <div class="text-cyan-300 leading-relaxed break-all bg-dark-900/80 p-4 rounded-xl border border-slate-800 select-all">
                  {{ oneClickCommand }}
                </div>
                <div class="text-xs text-slate-400 space-y-1 select-none">
                  <p class="flex items-center gap-1 text-emerald-400">
                    <span>✓</span> 自动下载与 Go 静态优化二进制匹配的版本
                  </p>
                  <p class="flex items-center gap-1 text-emerald-400">
                    <span>✓</span> 创建隔离受限账号 `octopus`，无 root 越权风险
                  </p>
                  <p class="flex items-center gap-1 text-emerald-400">
                    <span>✓</span> 注册 Systemd 开机自启并在发生意外断开时自动拉起
                  </p>
                </div>
              </div>

              <!-- View 2: Config Preview -->
              <pre v-else-if="activeView === 'config'" class="text-slate-300 leading-relaxed"><code>{{ configContent }}</code></pre>

              <!-- View 3: Service Management Commands -->
              <div v-else class="space-y-4">
                <div class="space-y-2">
                  <div class="text-slate-500 text-xs"># 查看中继节点运行状态与实时吞吐：</div>
                  <div class="bg-dark-900 p-2.5 rounded-lg border border-slate-800 text-cyan-300">
                    sudo systemctl status octopus-server
                  </div>
                </div>
                <div class="space-y-2">
                  <div class="text-slate-500 text-xs"># 实时追踪连接日志与健康心跳：</div>
                  <div class="bg-dark-900 p-2.5 rounded-lg border border-slate-800 text-cyan-300">
                    sudo journalctl -u octopus-server -f
                  </div>
                </div>
                <div class="space-y-2">
                  <div class="text-slate-500 text-xs"># 重启或重载中继服务：</div>
                  <div class="bg-dark-900 p-2.5 rounded-lg border border-slate-800 text-cyan-300">
                    sudo systemctl restart octopus-server
                  </div>
                </div>
                <div class="space-y-2">
                  <div class="text-slate-500 text-xs"># 优雅卸载与清理配置：</div>
                  <div class="bg-dark-900 p-2.5 rounded-lg border border-slate-800 text-rose-300">
                    sudo bash /usr/local/bin/octopus-uninstall.sh
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Friendly Tip Card -->
          <div class="p-4 rounded-xl bg-dark-900/60 border border-slate-800 flex items-start gap-3">
            <div class="text-lg">💡</div>
            <div class="text-xs text-slate-400 leading-relaxed">
              <strong class="text-slate-300">提示：</strong>
              若服务器开启了云平台安全组（如腾讯云/阿里云/华为云安全组），请确保在控制台开放入站规则端口 
              <span class="font-mono text-cyan-300">{{ bindPort }}/TCP</span>，否则内网被控端与主控端将无法建立打洞数据通道。
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

const platforms = [
  { id: 'linux', label: 'Linux (Systemd)', icon: '🐧' },
  { id: 'docker', label: 'Docker 容器', icon: '🐳' },
  { id: 'windows', label: 'Windows (PowerShell)', icon: '🪟' },
]

const selectedPlatform = ref('linux')
const activeView = ref('command')
const nodeId = ref('relay-node-gz-01')
const bandwidthLimit = ref(10)
const bindPort = ref(7000)
const authToken = ref('octopus-cluster-secret-key-2026')
const copied = ref(false)

const generateRandomToken = () => {
  const chars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
  let res = 'oct_'
  for (let i = 0; i < 24; i++) {
    res += chars.charAt(Math.floor(Math.random() * chars.length))
  }
  authToken.value = res
}

const oneClickCommand = computed(() => {
  if (selectedPlatform.value === 'linux') {
    return `curl -fsSL https://raw.githubusercontent.com/Arbor4/OctopusFrp/main/deploy/install.sh | sudo bash -s -- --role server --node-id "${nodeId.value}" --port ${bindPort.value} --bandwidth ${bandwidthLimit.value} --token "${authToken.value}"`
  } else if (selectedPlatform.value === 'docker') {
    return `docker run -d \\
  --name octopus-relay \\
  --restart always \\
  --net=host \\
  -e NODE_ID="${nodeId.value}" \\
  -e BIND_PORT=${bindPort.value} \\
  -e BANDWIDTH_LIMIT=${bandwidthLimit.value} \\
  -e AUTH_TOKEN="${authToken.value}" \\
  octopusfrp/server:latest`
  } else {
    return `irm https://raw.githubusercontent.com/Arbor4/OctopusFrp/main/deploy/install.ps1 | iex -NodeId "${nodeId.value}" -Port ${bindPort.value} -Bandwidth ${bandwidthLimit.value} -Token "${authToken.value}"`
  }
})

const configContent = computed(() => {
  return `# octopus-server.toml (位于 /etc/octopus/ 或当前目录)
node_id = "${nodeId.value}"
bind_addr = "0.0.0.0"
bind_port = ${bindPort.value}

# 集群统一认证鉴权密钥 (需与 client 一致)
auth_token = "${authToken.value}"

# 当前中继节点声称的最大物理限额 (Mbps)
# 调度引擎将根据此数值计算 SWRR 基准分发权重
bandwidth_limit_mbps = ${bandwidthLimit.value}

[transport]
heartbeat_interval = "30s"
heartbeat_timeout = "90s"
tls = false
`
})

const copyContent = async () => {
  let text = ''
  if (activeView.value === 'command') {
    text = oneClickCommand.value
  } else if (activeView.value === 'config') {
    text = configContent.value
  } else {
    text = `sudo systemctl status octopus-server\nsudo journalctl -u octopus-server -f`
  }

  try {
    if (navigator.clipboard) {
      await navigator.clipboard.writeText(text)
    } else {
      const textarea = document.createElement('textarea')
      textarea.value = text
      document.body.appendChild(textarea)
      textarea.select()
      document.execCommand('copy')
      document.body.removeChild(textarea)
    }
    copied.value = true
    setTimeout(() => {
      copied.value = false
    }, 2500)
  } catch (err) {
    console.error('Failed to copy: ', err)
  }
}
</script>
