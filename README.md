# MLX-Audio

基于 Apple MLX 框架构建的最佳音频处理库，在 Apple Silicon 上提供快速高效的文本转语音（TTS）、语音转文本（STT）和语音转语音（STS）功能。

## 特性

- 针对 Apple Silicon（M 系列芯片）优化的快速推理
- 支持 TTS、STT 和 STS 的多种模型架构
- 跨模型的多语言支持
- 语音定制和克隆功能
- 可调节的语速控制
- 带有 3D 音频可视化的交互式 Web 界面
- 兼容 OpenAI 的 REST API
- 支持量化（3 位、4 位、6 位、8 位及更多）以优化性能
- 用于 iOS/macOS 集成的 Swift 包

## 安装

### 使用 pip
```bash
pip install mlx-audio
```

### 使用 uv 仅安装命令行工具
从 PyPI 安装最新版本：
```bash
uv tool install --force mlx-audio --prerelease=allow
```

从 GitHub 安装最新代码：
```bash
uv tool install --force git+https://github.com/Blaizzy/mlx-audio.git --prerelease=allow
```

### 用于开发或 Web 界面：

```bash
git clone https://github.com/Blaizzy/mlx-audio.git
cd mlx-audio
pip install -e ".[dev]"
```

## 快速开始

### 命令行

```bash
# 基本 TTS 生成
mlx_audio.tts.generate --model mlx-community/Kokoro-82M-bf16 --text '你好，世界！' --lang_code a

# 带语音选择和语速调整
mlx_audio.tts.generate --model mlx-community/Kokoro-82M-bf16 --text '你好！' --voice af_heart --speed 1.2 --lang_code a

# 立即播放音频
mlx_audio.tts.generate --model mlx-community/Kokoro-82M-bf16 --text '你好！' --play  --lang_code a

# 保存到特定目录
mlx_audio.tts.generate --model mlx-community/Kokoro-82M-bf16 --text '你好！' --output_path ./my_audio  --lang_code a
```

### Python API

```python
from mlx_audio.tts.utils import load_model

# 加载模型
model = load_model("mlx-community/Kokoro-82M-bf16")

# 生成语音
for result in model.generate("来自 MLX-Audio 的问候！", voice="af_heart"):
    print(f"生成了 {result.audio.shape[0]} 个样本")
    # result.audio 包含作为 mx.array 的波形
```

## 支持的模型

### 文本转语音（TTS）

| 模型 | 描述 | 语言 | 仓库 |
|------|------|------|------|
| **Kokoro** | 快速、高质量的多语言 TTS | 英文、日文、中文、法文、西班牙文、意大利文、葡萄牙文、印地文 | [mlx-community/Kokoro-82M-bf16](https://huggingface.co/mlx-community/Kokoro-82M-bf16) |
| **Qwen3-TTS** | 阿里巴巴的多语言 TTS，支持语音设计 | 中文、英文、日文、韩文等 | [mlx-community/Qwen3-TTS-12Hz-1.7B-VoiceDesign-bf16](https://huggingface.co/mlx-community/Qwen3-TTS-12Hz-1.7B-VoiceDesign-bf16) |
| **CSM** | 具有语音克隆功能的会话语音模型 | 英文 | [mlx-community/csm-1b](https://huggingface.co/mlx-community/csm-1b) |
| **Dia** | 专注于对话的 TTS | 英文 | [mlx-community/Dia-1.6B-bf16](https://huggingface.co/mlx-community/Dia-1.6B-bf16) |
| **OuteTTS** | 高效的 TTS 模型 | 英文 | [mlx-community/OuteTTS-0.2-500M](https://huggingface.co/mlx-community/OuteTTS-0.2-500M) |
| **Spark** | SparkTTS 模型 | 英文、中文 | [mlx-community/SparkTTS-0.5B-bf16](https://huggingface.co/mlx-community/SparkTTS-0.5B-bf16) |
| **Chatterbox** | 富有表现力的多语言 TTS | 英文、西班牙文、法文、德文、意大利文、葡萄牙文、波兰文、土耳其文、俄文、荷兰文、捷克文、阿拉伯文、中文、日文、匈牙利文、韩文 | [mlx-community/Chatterbox-bf16](https://huggingface.co/mlx-community/Chatterbox-bf16) |
| **Soprano** | 高质量 TTS | 英文 | [mlx-community/Soprano-bf16](https://huggingface.co/mlx-community/Soprano-bf16) |

### 语音转文本（STT）

| 模型 | 描述 | 语言 | 仓库 |
|------|------|------|------|
| **Whisper** | OpenAI 的强大 STT 模型 | 99+ 种语言 | [mlx-community/whisper-large-v3-turbo-asr-fp16](https://huggingface.co/mlx-community/whisper-large-v3-turbo-asr-fp16) |
| **Qwen3-ASR** | 阿里巴巴的多语言 ASR | 中文、英文、日文、韩文等 | [mlx-community/Qwen3-ASR-1.7B-8bit](https://huggingface.co/mlx-community/Qwen3-ASR-1.7B-8bit) |
| **Qwen3-ForcedAligner** | 词级音频对齐 | 中文、英文、日文、韩文等 | [mlx-community/Qwen3-ForcedAligner-0.6B-8bit](https://huggingface.co/mlx-community/Qwen3-ForcedAligner-0.6B-8bit) |
| **Parakeet** | NVIDIA 的精确 STT | 英文 | [mlx-community/parakeet-tdt-0.6b-v2](https://huggingface.co/mlx-community/parakeet-tdt-0.6b-v2) |
| **Voxtral** | Mistral 的语音模型 | 多种语言 | [mlx-community/Voxtral-Mini-3B-2507-bf16](https://huggingface.co/mlx-community/Voxtral-Mini-3B-2507-bf16) |
| **VibeVoice-ASR** | 微软的 9B ASR，支持说话人分离和时间戳 | 多种语言 | [mlx-community/VibeVoice-ASR-bf16](https://huggingface.co/mlx-community/VibeVoice-ASR-bf16) |

### 语音转语音（STS）

| 模型 | 描述 | 用例 | 仓库 |
|------|------|------|------|
| **SAM-Audio** | 文本引导的源分离 | 提取特定声音 | [mlx-community/sam-audio-large](https://huggingface.co/mlx-community/sam-audio-large) |
| **Liquid2.5-Audio*** | 语音转语音、文本转语音和语音转文本 | 语音交互 | [mlx-community/LFM2.5-Audio-1.5B-8bit](https://huggingface.co/mlx-community/LFM2.5-Audio-1.5B-8bit)
| **MossFormer2 SE** | 语音增强 | 噪声去除 | [starkdmi/MossFormer2_SE_48K_MLX](https://huggingface.co/starkdmi/MossFormer2_SE_48K_MLX) |

## 模型示例

### Kokoro TTS

Kokoro 是一个快速的多语言 TTS 模型，带有 54 种语音预设。

```python
from mlx_audio.tts.utils import load_model

model = load_model("mlx-community/Kokoro-82M-bf16")

# 使用不同语音生成
for result in model.generate(
    text="欢迎使用 MLX-Audio！",
    voice="af_heart",  # 美国女性
    speed=1.0,
    lang_code="a"  # 美式英语
):
    audio = result.audio
```

**可用语音：**
- 美式英语：`af_heart`、`af_bella`、`af_nova`、`af_sky`、`am_adam`、`am_echo` 等
- 英式英语：`bf_alice`、`bf_emma`、`bm_daniel`、`bm_george` 等
- 日语：`jf_alpha`、`jm_kumo` 等
- 中文：`zf_xiaobei`、`zm_yunxi` 等

**语言代码：**
| 代码 | 语言 | 说明 |
|------|------|------|
| `a` | 美式英语 | 默认 |
| `b` | 英式英语 | |
| `j` | 日语 | 需要 `pip install misaki[ja]` |
| `z` | 中文普通话 | 需要 `pip install misaki[zh]` |
| `e` | 西班牙语 | |
| `f` | 法语 | |

### Qwen3-TTS

阿里巴巴的最先进多语言 TTS，支持语音克隆、情感控制和语音设计功能。

```python
from mlx_audio.tts.utils import load_model

model = load_model("mlx-community/Qwen3-TTS-12Hz-0.6B-Base-bf16")
results = list(model.generate(
    text="你好，欢迎使用 MLX-Audio！",
    voice="Chelsie",
    language="English",
))

audio = results[0].audio  # mx.array
```

有关语音克隆、CustomVoice、VoiceDesign 和所有可用模型，请参阅 [Qwen3-TTS README](mlx_audio/tts/models/qwen3_tts/README.md)。

### CSM（语音克隆）

使用参考音频样本克隆任何语音：

```bash
mlx_audio.tts.generate \
    --model mlx-community/csm-1b \
    --text "来自芝麻街的问候。" \
    --ref_audio ./reference_voice.wav \
    --play
```

### Whisper STT

```python
from mlx_audio.stt.generate import generate_transcription

result = generate_transcription(
    model="mlx-community/whisper-large-v3-turbo-asr-fp16",
    audio="audio.wav",
)
print(result.text)
```

### Qwen3-ASR 和 ForcedAligner

阿里巴巴的多语言语音模型，用于转录和词级对齐。

```python
from mlx_audio.stt import load

# 语音识别
model = load("mlx-community/Qwen3-ASR-0.6B-8bit")
result = model.generate("audio.wav", language="English")
print(result.text)

# 词级强制对齐
aligner = load("mlx-community/Qwen3-ForcedAligner-0.6B-8bit")
result = aligner.generate("audio.wav", text="I have a dream", language="English")
for item in result:
    print(f"[{item.start_time:.2f}s - {item.end_time:.2f}s] {item.text}")
```

有关 CLI 使用、所有模型和更多示例，请参阅 [Qwen3-ASR README](mlx_audio/stt/models/qwen3_asr/README.md)。

### VibeVoice-ASR

微软的 9B 参数语音转文本模型，支持说话人分离和时间戳。支持长音频（最长 60 分钟）并输出结构化 JSON。

```python
from mlx_audio.stt.utils import load

model = load("mlx-community/VibeVoice-ASR-bf16")

# 基本转录
result = model.generate(audio="meeting.wav", max_tokens=8192, temperature=0.0)
print(result.text)
# [{"Start":0,"End":5.2,"Speaker":0,"Content":"大家好，我们开始吧。"},
#  {"Start":5.5,"End":9.8,"Speaker":1,"Content":"感谢今天的参与。"}]

# 访问解析后的片段
for seg in result.segments:
    print(f"[{seg['start_time']:.1f}-{seg['end_time']:.1f}] 说话人 {seg['speaker_id']}: {seg['text']}")
```

**流式转录：**

```python
# 生成时流式输出标记
for text in model.stream_transcribe(audio="speech.wav", max_tokens=4096):
    print(text, end="", flush=True)
```

**带上下文（热词/元数据）：**

```python
result = model.generate(
    audio="technical_talk.wav",
    context="MLX, Apple Silicon, PyTorch, Transformer",
    max_tokens=8192,
    temperature=0.0,
)
```

**CLI 使用：**

```bash
# 基本转录
python -m mlx_audio.stt.generate \
    --model mlx-community/VibeVoice-ASR-bf16 \
    --audio meeting.wav \
    --output-path output \
    --format json \
    --max-tokens 8192 \
    --verbose

# 带上下文/热词
python -m mlx_audio.stt.generate \
    --model mlx-community/VibeVoice-ASR-bf16 \
    --audio technical_talk.wav \
    --output-path output \
    --format json \
    --max-tokens 8192 \
    --context "MLX, Apple Silicon, PyTorch, Transformer" \
    --verbose
```

### SAM-Audio（源分离）

使用文本提示从音频中分离特定声音：

```python
from mlx_audio.sts import SAMAudio, SAMAudioProcessor, save_audio

model = SAMAudio.from_pretrained("mlx-community/sam-audio-large")
processor = SAMAudioProcessor.from_pretrained("mlx-community/sam-audio-large")

batch = processor(
    descriptions=["一个人在说话"],
    audios=["mixed_audio.wav"],
)

result = model.separate_long(
    batch.audios,
    descriptions=batch.descriptions,
    anchors=batch.anchor_ids,
    chunk_seconds=10.0,
    overlap_seconds=3.0,
    ode_opt={"method": "midpoint", "step_size": 2/32},
)

save_audio(result.target[0], "voice.wav")
save_audio(result.residual[0], "background.wav")
```

### MossFormer2（语音增强）

从语音录音中去除噪声：

```python
from mlx_audio.sts import MossFormer2SEModel, save_audio

model = MossFormer2SEModel.from_pretrained("starkdmi/MossFormer2_SE_48K_MLX")
enhanced = model.enhance("noisy_speech.wav")
save_audio(enhanced, "clean.wav", 48000)
```

## Web 界面和 API 服务器

MLX-Audio 包含现代化的 Web 界面和兼容 OpenAI 的 API。

### 启动服务器

```bash
# 启动 API 服务器
mlx_audio.server --host 0.0.0.0 --port 8000

# 启动 Web UI（在另一个终端）
cd mlx_audio/ui
npm install && npm run dev
```

### API 端点

**文本转语音**（兼容 OpenAI）：
```bash
curl -X POST http://localhost:8000/v1/audio/speech \
  -H "Content-Type: application/json" \
  -d '{"model": "mlx-community/Kokoro-82M-bf16", "input": "你好！", "voice": "af_heart"}' \
  --output speech.wav
```

**语音转文本**：
```bash
curl -X POST http://localhost:8000/v1/audio/transcriptions \
  -F "file=@audio.wav" \
  -F "model=mlx-community/whisper-large-v3-turbo-asr-fp16"
```

## 量化

使用转换脚本通过量化减小模型大小并提高性能：

```bash
# 转换并量化为 4 位
python -m mlx_audio.convert \
    --hf-path prince-canuma/Kokoro-82M \
    --mlx-path ./Kokoro-82M-4bit \
    --quantize \
    --q-bits 4 \
    --upload-repo username/Kokoro-82M-4bit (可选：如果要将模型上传到 Hugging Face)

# 使用特定数据类型转换（bfloat16）
python -m mlx_audio.convert \
    --hf-path prince-canuma/Kokoro-82M \
    --mlx-path ./Kokoro-82M-bf16 \
    --dtype bfloat16 \
    --upload-repo username/Kokoro-82M-bf16 (可选：如果要将模型上传到 Hugging Face)
```

**选项：**
| 标志 | 描述 |
|------|------|
| `--hf-path` | 源 Hugging Face 模型或本地路径 |
| `--mlx-path` | 转换后模型的输出目录 |
| `-q, --quantize` | 启用量化 |
| `--q-bits` | 每权重位数（4、6 或 8） |
| `--q-group-size` | 量化的组大小（默认：64） |
| `--dtype` | 权重数据类型：`float16`、`bfloat16`、`float32` |
| `--upload-repo` | 将转换后的模型上传到 HF Hub |

## Swift

寻找 Swift/iOS 支持？查看 [mlx-audio-swift](https://github.com/Blaizzy/mlx-audio-swift)，用于在 macOS 和 iOS 上使用 MLX 进行设备端 TTS。

## 要求

- Python 3.10+
- Apple Silicon Mac（M1/M2/M3/M4）
- MLX 框架
- **ffmpeg**（保存 MP3/FLAC 音频格式所需）

### 安装 ffmpeg

保存 MP3 或 FLAC 格式的音频需要 ffmpeg。使用以下命令安装：

```bash
# macOS（使用 Homebrew）
brew install ffmpeg

# Ubuntu/Debian
sudo apt install ffmpeg
```

WAV 格式无需 ffmpeg 即可工作。

## 许可证

[MIT 许可证](LICENSE)

## 引用

```bibtex
@misc{mlx-audio,
  author = {Canuma, Prince},
  title = {MLX Audio},
  year = {2025},
  howpublished = {\url{https://github.com/Blaizzy/mlx-audio}},
  note = {用于 Apple Silicon 的音频处理库，具有 TTS、STT 和 STS 功能。}
}
```

## 致谢

- [Apple MLX 团队](https://github.com/ml-explore/mlx) 提供 MLX 框架