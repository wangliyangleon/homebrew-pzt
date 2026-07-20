# homebrew-pzt

[PicZTream (`pzt`)](https://github.com/wangliyangleon/picztream) 的 Homebrew tap。含终端全键盘照片筛选与色彩处理工具 `pzt`，以及配套的 Telegram 半自动选片-交付 agent `pzt-agent`。

> 仅支持 macOS / Apple Silicon（M 系列芯片）。

## 安装 CLI（`pzt`）

```sh
brew tap wangliyangleon/pzt
brew trust wangliyangleon/pzt   # Homebrew 6+ 对第三方 tap 的一次性信任门
brew install pzt
pzt --version
```

用法与选片按键见主仓 [README](https://github.com/wangliyangleon/picztream#快速上手)。

## 安装 Telegram agent（`pzt-agent`）

`pzt-agent` 会顺带把 `pzt` 一起装上，单用户自托管。

**前置**：一个 Telegram bot（token + 你的 chat_id）、一个 AI 模型（本地 Ollama 或云端 key）。

```sh
# 1) 装 agent（自动拉 pzt 依赖）
brew tap wangliyangleon/pzt
brew trust wangliyangleon/pzt
brew install pzt-agent

# 2) 本地 AI 模型（默认 provider=local；用云端就跳过这步、改配 API key）
brew install --cask ollama
ollama pull gemma4:e2b            # 默认模型，可换别的 Ollama 模型

# 3) Telegram：@BotFather 发 /newbot 拿 TELEGRAM_BOT_TOKEN；
#    取自己的 chat_id：给 bot 发一条消息后开
#    https://api.telegram.org/bot<token>/getUpdates 看 chat.id，或问 @userinfobot

# 4) 配置并启动
cp "$(brew --prefix)/share/pzt-agent/pzt-agent.env.example" ~/.pzt-agent.env
$EDITOR ~/.pzt-agent.env          # 填 TELEGRAM_BOT_TOKEN / TELEGRAM_CHAT_ID
set -a; source ~/.pzt-agent.env; set +a
pzt-agent                          # 长驻建议放 tmux：tmux new -s pzt 'pzt-agent'
```

启动后在 Telegram 里给 bot 连发几张照片、再发一句话（比如“给朋友圈选 9 张，暖色调”），按提示确认即可。完整环境变量、换模型、命令行参数见主仓 [agent/README.md](https://github.com/wangliyangleon/picztream/blob/main/agent/README.md)。

## 升级

```sh
brew update && brew upgrade pzt pzt-agent
```

---

## 维护说明

`Formula/*.rb` 由主仓 [`picztream`](https://github.com/wangliyangleon/picztream) 的 `packaging/homebrew/*.rb` 经 `scripts/release.sh` / 发布 workflow **自动同步过来**，**请勿在本仓手改 Formula**（会被下次发布覆盖）。本 README 则是本仓手工维护、不自动同步，改这里不影响主仓。发布流程见主仓 [`docs/RELEASE.md`](https://github.com/wangliyangleon/picztream/blob/main/docs/RELEASE.md)。
