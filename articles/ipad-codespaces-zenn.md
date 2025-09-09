---
title: "iPad × GitHub Codespaces でどこでもZenn執筆"
emoji: "📝"
type: "tech"
topics: ["zenn","github","codespaces","vscode","ipad"]
published: true
published_at: 2025-09-10 7:00
---

## 本記事の3行まとめ
* iPad + GitHub Codespaces + Dev Container + Zenn CLI でローカル構築なし執筆。
* 設定ファイルと初回コマンドをコピペで再現。
* iPadユーザーが無料枠内ですぐプレビュー表示まで到達するのがゴール。

---

## なぜ iPad + Codespaces なのか

* **持ち物は iPad とキーボードだけ**：PCを開けない移動中やカフェでも執筆に集中できます。
* **環境差分ゼロ**：Dev Container により Node/Zenn/拡張機能がリポジトリで定義され、どこで開いても同じ体験。
* **ブラウザ VS Code**：Codespaces の VS Code Web が iPad でも快適に動作。プレビューはポートフォワードでワンタップ表示。
* **無料枠で十分試せる**：個人アカウントは毎月 **120 コア時間 & 15GB-month** まで無料（超過は従量）。※最新の条件は**GitHub Docs**をご確認ください→ [About billing for GitHub Codespaces](https://docs.github.com/en/billing/managing-billing-for-your-products/about-billing-for-github-codespaces)、[GitHub’s products（Free/Proの枠）](https://docs.github.com/get-started/learning-about-github/githubs-products)。

---

## 事前に用意するもの

* GitHub パーソナルアカウント（公開リポジトリでOK）
* iPad（外付けキーボード推奨）
* Zenn に投稿するリポジトリ（新規でも既存でもOK）

---

## リポジトリに最小の Dev Container を置く

リポジトリ直下に `.devcontainer/` を作成して、以下を配置します。

**.devcontainer/devcontainer.json**

```json
{
  "name": "zenn-on-codespaces",
  "image": "mcr.microsoft.com/devcontainers/javascript-node:20",
  "onCreateCommand": "npm i -g zenn-cli@latest",
  "forwardPorts": [8000],
  "customizations": {
    "vscode": {
      "extensions": [
        "yzhang.markdown-all-in-one",
        "esbenp.prettier-vscode",
        "ms-vscode.vscode-typescript-next"
      ],
      "settings": {
        "editor.wordWrap": "on",
        "editor.renderWhitespace": "boundary",
        "files.trimTrailingWhitespace": true,
        "editor.tabSize": 2
      }
    }
  }
}
```

> メモ：`postCreateCommand` は再作成時にも毎回走るため、**初回のみ**で十分な導入処理（グローバル `zenn-cli` など）は `onCreateCommand` に寄せています。より厳密に制御したい場合は、`updateContentCommand` も併用してください（Dev Container 仕様参照）。

---

## Codespaces を起動して書き始める

1. GitHub のリポジトリで **Code ▸ Create codespace on main** を選択。
2. ターミナルで初回セットアップ：

   ```bash
   zenn init                  # 初回のみ（articles/ などが作成される）
   zenn new:article           # 記事の雛形を作成（対話式）
   zenn preview               # 既定: http://localhost:8000 でプレビュー
   ```
3. 画面下部の **PORTS** パネルに `8000` が表示されます。行の右端から **Open in Browser** を押すとブラウザで開きます。必要に応じて **Visibility: Private/Public** を切り替え可能（既定は Private）。

> 補足：`zenn new:article` は `--slug`・`--title` で非対話作成できます。例：
>
> ```bash
> zenn new:article \
>   --slug ipad-codespaces-zenn \
>   --title "iPad × Codespaces でどこでも執筆"
> ```

---

## 画像運用のミニガイド

* **配置**：`articles/images/2025-09-ipad-codespaces/` のように日付orスラッグ毎にまとめると管理が楽。
* **参照**：Markdown では **相対パス** を推奨。
* **alt テキスト**：読み上げ・SEO・アクセシビリティのため、**画面の意味**を短く記述（例：`![ZennプレビューをiPadブラウザで表示]`）。

---

## 無料枠・課金のポイント

* 個人 Free プラン：**120 コア時間 / 月**、**15GB-month ストレージ**が無料枠。Pro は **180 コア時間 / 月**、**20GB-month**。
* 使わないときは **Stop** で停止（**非アクティブ30分**で自動停止。既定値は変更可能）。設定手順→ [Setting your timeout period for Codespaces](https://docs.github.com/en/codespaces/setting-your-user-preferences/setting-your-timeout-period-for-github-codespaces)
* 公式まとめ→ [About billing for GitHub Codespaces](https://docs.github.com/en/billing/managing-billing-for-your-products/about-billing-for-github-codespaces)

> オフライン時は Codespaces に接続できないため、**プレビューも不可**（インターネット必須）。再接続すれば前回の状態から再開できます。参考→ [Understanding the codespace lifecycle](https://docs.github.com/en/codespaces/about-codespaces/understanding-the-codespace-lifecycle)

---

## 運用の小ワザ（iPad 編）

* **キーバインド**：ブラウザ由来のショートカット衝突が気になる場合は VS Code の *Keyboard Shortcuts* でリマップ。
* **日本語入力**：変換確定時の改行混入は、`Accept Suggestion` のキー変更や候補ウィンドウの操作で緩和。
* **集中モード**：エディタのズーム（⌘+/⌘-）と `editor.wordWrap` を有効化すると視線移動が減って快適。

---

## テンプレの足し算（次の一歩）

**Prettier / EditorConfig（差分の“揺れ”を減らす）**

**.prettierrc.json**

```json
{
  "semi": false,
  "singleQuote": true,
  "printWidth": 100,
  "proseWrap": "always"
}
```

**.editorconfig**

```
root = true

[*]
charset = utf-8
end_of_line = lf
indent_style = space
indent_size = 2
insert_final_newline = true
trim_trailing_whitespace = true
```

**Makefile（任意）**

```make
new:
	zenn new:article

preview:
	zenn preview
```

---

## よくあるハマりどころ

* **プレビューが開かない**：`zenn preview` が動いているか、**PORTS** に 8000 が出ているか確認。見えない場合は *Forward a Port* で `8000` を追加。
* **拡張が効かない**：Dev Container 起動直後はインストール待ちのことがあります。数十秒待ってから再読み込み。
* **自動停止**：非アクティブ既定 **30分**で自動停止。長くしたい場合は個人設定でタイムアウト延長（上限4時間）。

---

## 公開手順のメモ（Zenn）

* Frontmatter の `published: true` に変更してコミット＆プッシュ。
* **slug の命名**：半角英小文字・数字・ハイフン・アンダースコア、**12〜50字**が推奨（Zennの仕様）。参考→ [Zennのスラッグ（slug）とは](https://zenn.dev/zenn/articles/what-is-slug)
* `topics` は5個まで。検索流入を意識して適切に。

---

## 再利用用の雛形リポジトリ

* **Sample Repo**：[https://github.com/kouboyz/zenn-template](https://github.com/kouboyz/zenn-docs)
  このリポジトリには本記事で紹介した `.devcontainer/devcontainer.json` と設定例が含まれます。Fork してお使いください（テンプレート化も可）。

---

## この最小構成のゴール

* ローカルインストール不要で **即執筆**
* リポジトリに環境定義が閉じていて **どこで開いても同じ**
* iPad でも PC でも **切り替えコストゼロ**

> まずはこの“スモールスタート”で運用し、必要に応じて Linter/Formatter、メディア最適化（`sharp` など）、原稿テンプレ自動生成スクリプトを足していくのがおすすめです。