# 小智 AI 聊天机器人 （XiaoZhi AI Chatbot）

# 目录
- [终端对接 Home Assistant 说明](#终端对接-home-assistant-说明)
- [如何通过串口命令设置 WebSocket 服务器地址](#如何通过串口命令设置-websocket-服务器地址)
- [如何通过OTA配置 WebSocket 服务器地址](#如何通过ota配置-websocket-服务器地址)
- [音频格式说明](#音频格式说明)
- [对接HA自定义组件的协议建议](#对接ha自定义组件的协议建议)
- [配置建议](#配置建议)
- [鉴权说明](#鉴权说明)
- [云端与本地模式切换](#云端与本地模式切换)
- [常见问题排查](#常见问题排查)
- [推荐参考资料](#推荐参考资料)
- [技术支持](#技术支持)
- [下一步](#下一步)

# 终端对接 Home Assistant 说明

要让本终端通过 WebSocket 连接 Home Assistant（HA）自定义组件，请在设备配置中将 WebSocket 服务器地址（url）设置为 HA 的地址，例如：

```
ws://<HA_IP>:<端口>/api/xiaozhi_ws
```

如：
```
ws://192.168.1.100:8123/api/xiaozhi_ws
```

你可以通过串口、OTA配置或直接写入 NVS 的方式设置此地址。

---

## 如何通过串口命令设置 WebSocket 服务器地址

1. 连接设备串口，打开串口终端（如：115200 波特率）。
2. 输入如下命令，将 WebSocket 地址指向 HA：

```
set websocket url ws://<HA_IP>:<端口>/api/xiaozhi_ws
```

例如：
```
set websocket url ws://192.168.1.100:8123/api/xiaozhi_ws
```

3. 重启设备即可生效。

---

## 如何通过OTA配置 WebSocket 服务器地址

1. 在OTA配置文件（如JSON）中添加 websocket 字段：

```json
{
  "websocket": {
    "url": "ws://192.168.1.100:8123/api/xiaozhi_ws"
  }
}
```

2. 通过OTA升级推送该配置，设备会自动切换到新的WebSocket服务器。

---

（中文 | [English](README_en.md) | [日本語](README_ja.md)）

## 视频介绍

👉 [ESP32+SenseVoice+Qwen72B打造你的AI聊天伴侣！【bilibili】](https://www.bilibili.com/video/BV11msTenEH3/)

👉 [给小智装上 DeepSeek 的聪明大脑【bilibili】](https://www.bilibili.com/video/BV1GQP6eNEFG/)

👉 [手工打造你的 AI 女友，新手入门教程【bilibili】](https://www.bilibili.com/video/BV1XnmFYLEJN/)

## 项目目的

本项目是由虾哥开源的一个开源项目，以 MIT 许可证发布，允许任何人免费使用，并可以用于商业用途。

我们希望通过这个项目，能够帮助更多人入门 AI 硬件开发，了解如何将当下飞速发展的大语言模型应用到实际的硬件设备中。无论你是对 AI 感兴趣的学生，还是想要探索新技术的开发者，都可以通过这个项目获得宝贵的学习经验。

欢迎所有人参与到项目的开发和改进中来。如果你有任何想法或建议，请随时提出 Issue 或加入群聊。

学习交流 QQ 群：376893254

## 已实现功能

- Wi-Fi / ML307 Cat.1 4G
- BOOT 键唤醒和打断，支持点击和长按两种触发方式
- 离线语音唤醒 [ESP-SR](https://github.com/espressif/esp-sr)
- 流式语音对话（WebSocket 或 UDP 协议）
- 支持国语、粤语、英语、日语、韩语 5 种语言识别 [SenseVoice](https://github.com/FunAudioLLM/SenseVoice)
- 声纹识别，识别是谁在喊 AI 的名字 [3D Speaker](https://github.com/modelscope/3D-Speaker)
- 大模型 TTS（火山引擎 或 CosyVoice）
- 大模型 LLM（Qwen, DeepSeek, Doubao）
- 可配置的提示词和音色（自定义角色）
- 短期记忆，每轮对话后自我总结
- OLED / LCD 显示屏，显示信号强弱或对话内容
- 支持 LCD 显示图片表情
- 支持多语言（中文、英文）

## ✅ 已支持的芯片平台

- ✅ ESP32-S3
- ✅ ESP32-C3
- ✅ ESP32-P4

## 硬件部分

### 面包板手工制作实践

详见飞书文档教程：

👉 [《小智 AI 聊天机器人百科全书》](https://ccnphfhqs21z.feishu.cn/wiki/F5krwD16viZoF0kKkvDcrZNYnhb?from=from_copylink)

面包板效果图如下：

![面包板效果图](docs/wiring2.jpg)

### 已支持的开源硬件

- <a href="https://oshwhub.com/li-chuang-kai-fa-ban/li-chuang-shi-zhan-pai-esp32-s3-kai-fa-ban" target="_blank" title="立创·实战派 ESP32-S3 开发板">立创·实战派 ESP32-S3 开发板</a>
- <a href="https://github.com/espressif/esp-box" target="_blank" title="乐鑫 ESP32-S3-BOX3">乐鑫 ESP32-S3-BOX3</a>
- <a href="https://docs.m5stack.com/zh_CN/core/CoreS3" target="_blank" title="M5Stack CoreS3">M5Stack CoreS3</a>
- <a href="https://docs.m5stack.com/en/atom/Atomic%20Echo%20Base" target="_blank" title="AtomS3R + Echo Base">AtomS3R + Echo Base</a>
- <a href="https://docs.m5stack.com/en/core/ATOM%20Matrix" target="_blank" title="AtomMatrix + Echo Base">AtomMatrix + Echo Base</a>
- <a href="https://gf.bilibili.com/item/detail/1108782064" target="_blank" title="神奇按钮 2.4">神奇按钮 2.4</a>
- <a href="https://www.waveshare.net/shop/ESP32-S3-Touch-AMOLED-1.8.htm" target="_blank" title="微雪电子 ESP32-S3-Touch-AMOLED-1.8">微雪电子 ESP32-S3-Touch-AMOLED-1.8</a>
- <a href="https://github.com/Xinyuan-LilyGO/T-Circle-S3" target="_blank" title="LILYGO T-Circle-S3">LILYGO T-Circle-S3</a>
- <a href="https://oshwhub.com/tenclass01/xmini_c3" target="_blank" title="虾哥 Mini C3">虾哥 Mini C3</a>
- <a href="https://oshwhub.com/movecall/moji-xiaozhi-ai-derivative-editi" target="_blank" title="Movecall Moji ESP32S3">Moji 小智AI衍生版</a>
- <a href="https://oshwhub.com/movecall/cuican-ai-pendant-lights-up-y" target="_blank" title="Movecall CuiCan ESP32S3">璀璨·AI吊坠</a>
- <a href="https://github.com/WMnologo/xingzhi-ai" target="_blank" title="无名科技Nologo-星智-1.54">无名科技Nologo-星智-1.54TFT</a>
- <a href="https://www.seeedstudio.com/SenseCAP-Watcher-W1-A-p-5979.html" target="_blank" title="SenseCAP Watcher">SenseCAP Watcher</a>
<div style="display: flex; justify-content: space-between;">
  <a href="docs/v1/lichuang-s3.jpg" target="_blank" title="立创·实战派 ESP32-S3 开发板">
    <img src="docs/v1/lichuang-s3.jpg" width="240" />
  </a>
  <a href="docs/v1/espbox3.jpg" target="_blank" title="乐鑫 ESP32-S3-BOX3">
    <img src="docs/v1/espbox3.jpg" width="240" />
  </a>
  <a href="docs/v1/m5cores3.jpg" target="_blank" title="M5Stack CoreS3">
    <img src="docs/v1/m5cores3.jpg" width="240" />
  </a>
  <a href="docs/v1/atoms3r.jpg" target="_blank" title="AtomS3R + Echo Base">
    <img src="docs/v1/atoms3r.jpg" width="240" />
  </a>
  <a href="docs/v1/magiclick.jpg" target="_blank" title="神奇按钮 2.4">
    <img src="docs/v1/magiclick.jpg" width="240" />
  </a>
  <a href="docs/v1/waveshare.jpg" target="_blank" title="微雪电子 ESP32-S3-Touch-AMOLED-1.8">
    <img src="docs/v1/waveshare.jpg" width="240" />
  </a>
  <a href="docs/lilygo-t-circle-s3.jpg" target="_blank" title="LILYGO T-Circle-S3">
    <img src="docs/lilygo-t-circle-s3.jpg" width="240" />
  </a>
  <a href="docs/xmini-c3.jpg" target="_blank" title="虾哥 Mini C3">
    <img src="docs/xmini-c3.jpg" width="240" />
  </a>
  <a href="docs/v1/movecall-moji-esp32s3.jpg" target="_blank" title="Movecall Moji 小智AI衍生版">
    <img src="docs/v1/movecall-moji-esp32s3.jpg" width="240" />
  </a>
  <a href="docs/v1/movecall-cuican-esp32s3.jpg" target="_blank" title="CuiCan">
    <img src="docs/v1/movecall-cuican-esp32s3.jpg" width="240" />
  </a>
  <a href="docs/v1/wmnologo_xingzhi_1.54.jpg" target="_blank" title="无名科技Nologo-星智-1.54">
    <img src="docs/v1/wmnologo_xingzhi_1.54.jpg" width="240" />
  </a>
  <a href="docs/v1/sensecap_watcher.jpg" target="_blank" title="SenseCAP Watcher">
    <img src="docs/v1/sensecap_watcher.jpg" width="240" />
  </a>
</div>

## 固件部分

### 免开发环境烧录

新手第一次操作建议先不要搭建开发环境，直接使用免开发环境烧录的固件。

固件默认接入 [xiaozhi.me](https://xiaozhi.me) 官方服务器，目前个人用户注册账号可以免费使用 Qwen 实时模型。

👉 [Flash烧录固件（无IDF开发环境）](https://ccnphfhqs21z.feishu.cn/wiki/Zpz4wXBtdimBrLk25WdcXzxcnNS) 


### 开发环境

- Cursor 或 VSCode
- 安装 ESP-IDF 插件，选择 SDK 版本 5.3 或以上
- Linux 比 Windows 更好，编译速度快，也免去驱动问题的困扰
- 使用 Google C++ 代码风格，提交代码时请确保符合规范

### 开发者文档

- [开发板定制指南](main/boards/README.md) - 学习如何为小智创建自定义开发板适配
- [物联网控制模块](main/iot/README.md) - 了解如何通过AI语音控制物联网设备


## 智能体配置

如果你已经拥有一个小智 AI 聊天机器人设备，可以登录 [xiaozhi.me](https://xiaozhi.me) 控制台进行配置。

👉 [后台操作视频教程（旧版界面）](https://www.bilibili.com/video/BV1jUCUY2EKM/)

## 技术原理与私有化部署

👉 [一份详细的 WebSocket 通信协议文档](docs/websocket.md)

在个人电脑上部署服务器，可以参考另一位作者同样以 MIT 许可证开源的项目 [xiaozhi-esp32-server](https://github.com/xinnan-tech/xiaozhi-esp32-server)

## Star History

<a href="https://star-history.com/#78/xiaozhi-esp32&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=78/xiaozhi-esp32&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=78/xiaozhi-esp32&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=78/xiaozhi-esp32&type=Date" />
 </picture>
</a>

---

## 音频格式说明

- 本终端与 Home Assistant 语音助手、ESPHome 语音助手兼容，音频流采用 OPUS 编码，采样率 16kHz，单声道。
- 终端推送音频时无需更改格式，HA 侧可直接解码处理。

---

## 对接HA自定义组件的协议建议

- 建议 WebSocket 协议版本使用 3（可在NVS或OTA配置中设置 version=3）。
- 音频数据采用二进制帧（OPUS编码），控制消息（如hello、listen、tts等）采用JSON文本帧。
- 具体协议可参考 ESPHome 语音助手或 xiaozhi_websocket 协议。

---

## 配置建议

- 对接Home Assistant时，建议在NVS或OTA配置中设置：
  - websocket version = 3
  - websocket url = ws://<HA_IP>:<端口>/api/xiaozhi_ws

---

## 鉴权说明

- 对接Home Assistant时，websocket token 字段可为空（本地网络无需鉴权）。
- 如需安全访问，可在token字段填写HA的Long-Lived Access Token（长期访问令牌）。
- 令牌获取方式：HA用户界面 → 个人资料 → 创建长期访问令牌。

---

## 云端与本地模式切换

- 对接Home Assistant时，建议关闭云端server相关配置，仅保留websocket协议。
- 可通过OTA或串口命令清除云端server配置，仅设置websocket参数。

---

## 常见问题排查

- 音频无响应：请检查WebSocket地址是否指向HA，协议version是否为3，音频参数是否为OPUS/16000/1。
- TTS无声音：请检查HA自定义组件是否正确返回TTS音频，终端是否收到二进制音频帧。
- 连接失败：请检查HA防火墙、token权限、网络连通性。

---

## 推荐参考资料

- [ESPHome Voice Assistant 官方文档](https://esphome.io/components/voice_assistant.html)
- [Home Assistant Assist Pipeline API](https://developers.home-assistant.io/docs/voice_assistants/assist_pipeline/)
- [HA TTS 服务](https://www.home-assistant.io/integrations/tts/)
- [自定义组件开发文档](https://developers.home-assistant.io/docs/creating_component_index/)

---

## 技术支持

- 如需对接Home Assistant遇到问题，欢迎提交issue或PR。
- 也可联系本项目维护者获取技术支持。

---

## 下一步

- 即将提供 Home Assistant custom component（xiaozhi-hacs）示例，支持WebSocket对接本终端。
- 欢迎关注和试用！

---

# 小智AI终端

基于ESP32-S3的智能语音终端，支持与Home Assistant无缝集成。

## 🚀 版本历史

### v1.6.5 (当前版本) - 2025.05.28
**🎯 Home Assistant WebSocket集成版本**

#### ✨ 新功能
- **WebSocket协议支持**：添加完整的WebSocket客户端实现
- **Home Assistant集成**：原生支持HA Assist Pipeline
- **动态协议选择**：优先使用WebSocket，MQTT作为备用
- **OPUS音频优化**：16kHz单声道，完美兼容ESPHome语音助手

#### 🔧 技术改进
- **OTA配置增强**：支持通过OTA动态配置WebSocket地址
- **设备跟踪**：OTA服务器记录设备连接历史
- **智能重启**：避免无限重启循环
- **音频格式标准化**：OPUS 16kHz单声道，60ms帧长度

#### 📋 配置要求
**擦除Flash重新烧录**（重要）：
```bash
# 完全清除设置
idf.py erase-flash

# 重新烧录v1.6.5固件
idf.py flash monitor
```

**WebSocket配置**：
- 协议版本：3（推荐）
- 音频格式：OPUS 16kHz单声道
- 目标地址：`ws://<HA_IP>:8123/api/xiaozhi_ws`
- 帧长度：60ms

#### 🔗 Home Assistant对接

**前置要求**：
1. Home Assistant 2024.1+
2. ESPHome集成（可选，用于测试）
3. xiaozhi-hacs自定义组件

**配置步骤**：
1. 安装xiaozhi-hacs组件到HA
2. 重启Home Assistant
3. 终端设置OTA地址：`http://<PC_IP>:5000/xiaozhi/ota/`
4. 设备自动获取WebSocket配置并重启

**验证连接**：
```bash
# 检查WebSocket连接日志
tail -f home-assistant.log | grep xiaozhi

# 测试语音处理
# 设备应显示WebSocket连接状态
```

#### 🎵 音频兼容性
- **输入**：16kHz单声道PCM → OPUS编码
- **输出**：OPUS解码 → 24kHz播放
- **帧长度**：60ms（推荐），支持20/40/60ms
- **比特率**：自适应，优化语音质量

### v1.6.4 (之前版本)
**🏗️ MQTT协议基础版本**

#### 功能特性
- MQTT协议支持
- 基础OTA功能
- 云端语音处理
- WiFi配网

## 🛠️ 开发环境

### 编译要求
- ESP-IDF v5.0+
- Python 3.8+
- CMake 3.16+

### 硬件支持
- ESP32-S3 (推荐16MB Flash)
- 麦克风模块
- 扬声器/耳机输出
- 按键/触摸控制

## 📡 Home Assistant对接详细说明

### WebSocket协议选择原因
1. **低延迟**：WebSocket连接延迟比MQTT低20-30ms
2. **音频流支持**：原生支持二进制音频数据传输
3. **HA集成**：与HA Assist Pipeline完美契合
4. **协议简洁**：减少中间件，提高可靠性

### OPUS音频格式优势
- **压缩比高**：比PCM减少75%带宽占用
- **低延迟**：支持20ms超低延迟编码
- **质量优秀**：语音质量接近无损
- **标准兼容**：HA/ESPHome原生支持

### 网络架构
```
[小智终端] <--WebSocket--> [Home Assistant] <--> [语音处理引擎]
     |                              |
     +-- OPUS音频流 ---------> Assist Pipeline
     |                              |
     +-- 控制命令 <----------- 智能家居控制
```

### 故障排查

#### WebSocket连接失败
1. 检查HA地址和端口
2. 确认xiaozhi-hacs组件已安装
3. 查看HA日志：`tail -f home-assistant.log`
4. 验证网络连通性：`ping <HA_IP>`

#### 音频质量问题
1. 确认OPUS格式：16kHz单声道
2. 检查网络延迟：建议<50ms
3. 调整帧长度：60ms平衡质量与延迟
4. 监控丢包率：应<1%

#### 设备重启循环
1. 擦除Flash：`idf.py erase-flash`
2. 重新烧录：`idf.py flash monitor`
3. 检查OTA服务器配置
4. 确认固件版本匹配

## 🔧 串口命令

### 网络配置
```bash
# WiFi配置
wifi_ssid <SSID>
wifi_password <PASSWORD>

# OTA地址
ota_url http://<PC_IP>:5000/xiaozhi/ota/

# WebSocket配置（自动通过OTA下发）
websocket_url ws://<HA_IP>:8123/api/xiaozhi_ws
websocket_version 3

# 重启应用配置
reboot
```

### 调试命令
```bash
# 查看网络状态
network_info

# 查看WebSocket状态
websocket_status

# 查看音频统计
audio_stats

# 重置所有配置
factory_reset
```

## 📚 参考资料

- [Home Assistant Assist Pipeline](https://developers.home-assistant.io/docs/voice/)
- [ESPHome语音助手](https://esphome.io/components/voice_assistant.html)
- [OPUS音频编解码](https://opus-codec.org/)
- [WebSocket协议规范](https://tools.ietf.org/html/rfc6455)

## 🤝 贡献

欢迎提交Issue和Pull Request来改进这个项目。

## 📄 许可证

MIT License - 详见LICENSE文件。

---
