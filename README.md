# Zenn Docs Template (iPad × GitHub Codespaces)

iPad のブラウザ + GitHub Codespaces + Dev Container + Zenn CLI で Zenn 記事を書くためのリポジトリ。Zennの記事を読んだ後そのまま使えます。

目的: すぐに記事を書き始める / 迷わずプレビューまで到達する。

## 📁 構成

```
.
├─ .devcontainer/
│  └─ devcontainer.json
├─ LICENSE
└─ README.md
```

## 🚀 使い方
1. **Use this template** か Fork → Codespace を作成
2. ターミナルで:
```bash
zenn init          # 初回のみ (既に構造があれば省略)
zenn new:article   # 記事雛形
zenn preview       # http://localhost:8000
```
3. PORTS から 8000 をブラウザで開く

非対話例:
```bash
zenn new:article --slug ipad-codespaces-zenn --title "iPad × Codespaces でどこでも執筆"
```

## 🧩 Dev Container
Node ベースイメージ + いくつかの Markdown 支援拡張 + 初回 `zenn-cli` 導入。

## ✍️ Frontmatter 雛形
記事ファイル (`articles/your-slug.md`) 冒頭:
```markdown
---
title: "タイトル"
emoji: "📝"
type: "tech"        # tech / idea
topics: ["zenn","github","codespaces"]
published: false     # 公開時に true
---
```

## 🔁 よく使うコマンド
```bash
zenn init              # 初回のみ
zenn new:article       # 記事 (対話式)
zenn new:book          # 本 (対話式)
zenn preview --port 8000
```

## 🧠 slug / topics
* slug: 英小文字/数字/ハイフン/アンダースコア (12〜50 目安)
* topics: 最大 5 個

## 🖼 画像運用ミニガイド
* `articles/images/<slug>/` などで整理
* 参照は相対パス: `![プレビュー](./images/<slug>/preview.png)`
* alt は“画像の意味”を端的に

## 💡 iPad Tips
* Keyboard Shortcuts で衝突を必要に応じ調整
* `editor.wordWrap` を on
* 日本語入力確定時の改行は Suggestion キー変更で軽減

## 🧪 拡張例 (必要になったら)
| 目的 | 例 |
|------|----|
| 体裁 | Prettier / EditorConfig |
| 品質 | Markdown Lint / リンクチェッカ |
| 画像 | `sharp` で WebP 化 |
| 自動化 | テンプレ生成スクリプト |

## 🆘 トラブルシュート
| 症状 | 対処 |
|------|------|
| プレビュー出ない | `zenn preview` 稼働 / PORTS に 8000 / Forward |
| 拡張が効かない | 起動直後は待つ → 再読み込み |
| 自動停止 | 30 分で停止。設定で延長 |
| オフライン | 再接続で復元 |

## 🛡 Codespaces 無料枠 (要公式確認)
* Free: 120 コア時間 / 月, 15GB-month
* Pro: 180 コア時間 / 月, 20GB-month
* 詳細: Docs 参照

## 📤 公開 (Zenn)
1. `published: true`
2. コミット & プッシュ
3. Zenn で確認

## 🔗 参考リンク
* Zenn Official Docs: https://zenn.dev
* Codespaces Billing: https://docs.github.com/en/billing/managing-billing-for-your-products/about-billing-for-github-codespaces
* Timeout 設定: https://docs.github.com/en/codespaces/setting-your-user-preferences/setting-your-timeout-period-for-github-codespaces

## 📝 ライセンス
`LICENSE` を参照してください。

---
改善提案は Issue / PR でどうぞ。