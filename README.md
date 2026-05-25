# onecloud-armbian-ai-agent
Armbian with ai agent(eg: nanobot, openclaw, hermes) for onecloud(玩客云)

### Login user/passwd
xshl5lab/Xshl5lab@2026

# Usage for nanobot
### Version info
```
xshl5lab@onecloud:~$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Armbian-unofficial 25.11.0-trunk noble
Release:        24.04
Codename:       noble

xshl5lab@onecloud:~$ nanobot --version
🐈 nanobot v0.1.4.post5

xshl5lab@onecloud:~$ service nanobot-gateway status
● nanobot-gateway.service - Nanobot Gateway
     Loaded: loaded (/usr/lib/systemd/system/nanobot-gateway.service; enabled; preset: enabled)
     Active: active (running) since Fri 2026-05-22 11:41:26 UTC; 2 days ago
   Main PID: 829 (nanobot)
      Tasks: 1 (limit: 2191)
     Memory: 132.9M (peak: 160.7M)
        CPU: 25.822s
     CGroup: /system.slice/nanobot-gateway.service
```

### Model conf
```
xshl5lab@onecloud:~$ nanobot onboard
✓ Created config at /home/xshl5lab/.nanobot/config.json
Config template now uses `maxTokens` + `contextWindowTokens`; `memoryWindow` is no longer a runtime setting.
2026-05-25 10:07:25.368 | DEBUG    | nanobot.channels.registry:discover_all:64 - Skipping built-in channel 'matrix': Matrix dependencies not installed. Run: pip install nanobot-ai[matrix]

🐈 nanobot is ready!

Next steps:
  1. Add your API key to ~/.nanobot/config.json
     Get one at: https://openrouter.ai/keys
  2. Chat: nanobot agent -m "Hello!"


xshl5lab@onecloud:~$ nano .nanobot/config.json
```
Some moments later...
```
@@ -2,8 +2,8 @@
   "agents": {
     "defaults": {
       "workspace": "~/.nanobot/workspace",
-      "model": "anthropic/claude-opus-4-5",
-      "provider": "auto",
+      "model": "deepseek-v4-flash",
+      "provider": "deepseek",
       "maxTokens": 8192,
       "contextWindowTokens": 65536,
       "temperature": 0.1,
@@ -15,10 +15,10 @@
     "sendProgress": true,
     "sendToolHints": false,
     "dingtalk": {
-      "enabled": false,
-      "clientId": "",
-      "clientSecret": "",
-      "allowFrom": []
+      "enabled": true,
+      "clientId": "dingnyXXXXXXXX",
+      "clientSecret": "acuijXXXXXXXXXXXXXXX-TrMl1qXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
+      "allowFrom": ["*"]
     },
     "discord": {
       "enabled": false,
@@ -162,8 +162,8 @@
       "extraHeaders": null
     },
     "deepseek": {
-      "apiKey": "",
-      "apiBase": null,
+      "apiKey": "sk-13XXXXXXXXXXXXXXXXXXXXXXXXXXX",
+      "apiBase": "https://api.deepseek.com/v1",
       "extraHeaders": null
     },
     "groq": {
```

### Agent test
```
xshl5lab@onecloud:~$ nanobot agent -m "What model used now?"
10:28:35 - LiteLLM:WARNING: get_model_cost_map.py:271 - LiteLLM: Failed to fetch remote model cost map from https://raw.githubusercontent.com/BerriAI/litellm/main/model_prices_and_context_window.json: [Errno 111] Connection refused. Falling back to local backup.

🐈 nanobot
还是老样子：

 • 模型: deepseek-v4-flash
 • 提供商: DeepSeek
 • API: https://api.deepseek.com/v1

没变过 🐈

xshl5lab@onecloud:~$ nanobot agent -m "当前硬件温度,详细一点"
10:30:44 - LiteLLM:WARNING: get_model_cost_map.py:271 - LiteLLM: Failed to fetch remote model cost map from https://raw.githubusercontent.com/BerriAI/litellm/main/model_prices_and_context_window.json: [Errno 111] Connection refused. Falling back to local backup.

🐈 nanobot
详细硬件温度报告如下：

🌡️ SoC 温度


 当前          49.4°C
 ────────────────────
 触发降频      80°C
 触发关机保护  90°C
 硬上限        110°C


💻 硬件平台


 项目      信息
 ──────────────────────────────────────────────
 CPU       ARMv7 (v7l) × 4核
 SoC       Amlogic Meson (Amlogic 平台)
 主频      1.536 GHz (当前，最高可到 1.536 GHz)
 调频策略  ondemand (按需变频)
 可用频率  96 MHz ~ 1.536 GHz (共13档)


🧠 系统负载


 项目      数值
 ──────────────────────────────────────────────
 温度趋势  稳定 ~50°C，非常健康 ✅
 运行时长  已运行 40 分钟
 CPU负载   0.39 / 0.16 / 0.06 (1min/5min/15min)
 内存      981 MB 总内存，已用 326 MB (33%)
 Swap      490 MB，使用 0 B


结论：当前温度 49.4°C，距离降频阈值 80°C 还有很大余量，散热正常 🐈
```

# Related link
hzyitc/armbian-onecloud: https://github.com/hzyitc/armbian-onecloud
