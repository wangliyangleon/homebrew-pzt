# homebrew-pzt

[PicZTream (`pzt`)](https://github.com/wangliyangleon/picztream) 的 Homebrew tap。

## 安装

```sh
brew tap wangliyangleon/pzt
brew trust wangliyangleon/pzt   # Homebrew 6+ 对第三方 tap 的一次性信任门
brew install pzt
```

仅支持 macOS / Apple Silicon。formula 由主仓 `picztream` 的
`packaging/homebrew/pzt.rb` 经 `scripts/release.sh` 同步发布,请勿在本仓手改。
