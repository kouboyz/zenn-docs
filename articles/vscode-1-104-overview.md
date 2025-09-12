---
title: "VS Code v1.104 新機能ざっくりまとめ"
emoji: "📚"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["vscode","github","copilot"]
published: false
---

## 本記事の3行まとめ
* 2025-09-12 公開の VS Code v1.104 [リリースノート](https://code.visualstudio.com/updates/v1_104)を日本語で読み歩くための個人向けメモです。
* 気になるアプデ: Autoモデル選択/Copilot運用基盤(AGENTS.md・条件付きプロンプト・Todo可視化)と安全ガード強化、さらにターミナル・タスク・タブ・Python・拡張APIの地味改善が積み重なって日常フローの摩擦を削った v1.104。
* その他: 11月の [GitHub Universe](https://githubuniverse.com/) に向けて覇権を取りに来てほしいと期待している今日この頃なわたしには刺さるアプデでした。

---

ざっくり自分用に VS Code 1.104 の気になった所をCopilotくんに日本語化＆メモにしてもらいました。深掘りは原文リンクを踏めるように揃えてもらっています。注目している軸は⭐マークを付けています。邪魔だったらごめんね！

公式リリースノート: https://code.visualstudio.com/updates/v1_104

---

## 💬 Chat / Copilot まわり
| トピック | 要点 | リンク |
|----------|------|--------|
| ⭐ 自動モデル選択 (Auto model) | 利用状況やレート制限を考慮し最適モデル自動選択 (Claude / GPT / Gemini など候補)。 | [Auto model selection](https://code.visualstudio.com/updates/v1_104#_auto-model-selection-preview) |
| ⭐ 機密/重要ファイル編集の確認 | 敏感ファイル変更前に確認ダイアログ。`chat.tools.edits.autoApprove` で制御。 | [Confirm edits](https://code.visualstudio.com/updates/v1_104#_confirm-edits-to-sensitive-files) |
| ⭐ `AGENTS.md` 対応 | ルートに置くとエージェントの共通コンテキストに自動読込。チーム標準化に有効。 | [AGENTS.md](https://code.visualstudio.com/updates/v1_104#_support-for-agentsmd-files-experimental) |
| ⭐ 変更ファイルリスト刷新 | 提案差分 UI/折りたたみ/自動除去でエージェントモード中の視認性向上。 | [Changed files](https://code.visualstudio.com/updates/v1_104#_improved-changed-files-experience) |
| ⭐ プロンプトファイルのカスタムモード | 独自 chat モード指定が可能に。ワークフロー分離が容易。 | [Custom chat modes](https://code.visualstudio.com/updates/v1_104#_use-custom-chat-modes-in-prompt-files) |
| ⭐ プロンプトファイル候補設定 (実験) | 条件式で特定ファイル種別時に候補提示。ナレッジの“必要な時だけ”出現。 | [Prompt file suggestions](https://code.visualstudio.com/updates/v1_104#_configure-prompt-file-suggestions-experimental) |
| ツールセット内個別有効化 | tool set 内のツール粒度を GUI で制御。 | [Tool sets](https://code.visualstudio.com/updates/v1_104#_select-tools-in-tool-sets) |
| チャット用フォント設定 | `chat.fontFamily` / `chat.fontSize` で可読性調整。 | [Chat font](https://code.visualstudio.com/updates/v1_104#_configure-font-used-in-chat) |
| Coding Agent 協調 (実験) | 複数セッション/ステータスバー追跡/PR 操作など連携拡張。 | [Collaborate with coding agents](https://code.visualstudio.com/updates/v1_104#_collaborate-with-coding-agents-experimental) |
| Google サインイン | Copilot への Google アカウント Social Sign-In GA。 | [Social sign in](https://code.visualstudio.com/updates/v1_104#_social-sign-in-with-google) |
| ⭐ ターミナル自動承認強化 | 安全警告/ルール UI/パス扱い改善/ネット取得警告など。 | [Terminal auto approve](https://code.visualstudio.com/updates/v1_104#_terminal-auto-approve) |
| グローバル自動承認警告 | 誤用防止の強い Warning + 設定リネーム。 | [Global auto approve](https://code.visualstudio.com/updates/v1_104#_global-auto-approve) |
| 数式レンダリング既定ON | KaTeX による `$...$` / `$$...$$`。 | [Math rendering](https://code.visualstudio.com/updates/v1_104#_math-rendering-enabled-by-default) |
| Chat 初期表示 | Secondary Side Bar の既定表示設定。 | [Chat view visibility](https://code.visualstudio.com/updates/v1_104#_chat-view-default-visibility) |
| タスク連携強化 | 入力検知/問題マッチャ結果の構造表示/複合タスク可視化。 | [Improved task support](https://code.visualstudio.com/updates/v1_104#_improved-task-support) |
| ターミナルツール改善 | core 取り込み/タイムアウト設定/Command Prompt 回避など。 | [Improved terminal support](https://code.visualstudio.com/updates/v1_104#_improved-terminal-support) |
| ⭐ Todo List tool | エージェント進捗分解 UI がデフォルト有効。 | [Todo List tool](https://code.visualstudio.com/updates/v1_104#_todo-list-tool) |
| ツール呼び出しスキップ | 部分キャンセル的にスキップ可能。 | [Skip tool calls](https://code.visualstudio.com/updates/v1_104#_skip-tool-calls) |
| ⭐ セマンティック検索改善 | 新 embeddings で精度向上/サイズ 6% に圧縮。 | [Semantic workspace search](https://code.visualstudio.com/updates/v1_104#_improvements-to-semantic-workspace-search) |
| AI 機能無効化設定 | 統合的に Copilot 生成系を隠す `chat.disableAIFeatures`。 | [Hide/disable AI](https://code.visualstudio.com/updates/v1_104#_hide-and-disable-github-copilot-ai-features) |

## 🔌 MCP (Model Context Protocol)
| トピック | 要点 | リンク |
|----------|------|--------|
| サーバー instructions 読込 | MCP サーバーの追加メタ指示を基礎プロンプトへ。 | [Server instructions](https://code.visualstudio.com/updates/v1_104#_support-for-server-instructions) |
| 自動ディスカバリ既定OFF | 安全/明示性重視で `chat.mcp.discovery.enabled` デフォルト無効。 | [Auto discovery](https://code.visualstudio.com/updates/v1_104#_mcp-auto-discovery-disabled-by-default) |
| アクセス制御設定刷新 | 旧 boolean から `chat.mcp.access` (all/none) に整理。 | [Enable MCP](https://code.visualstudio.com/updates/v1_104#_enable-mcp) |

## ♿ Accessibility
| トピック | 要点 | リンク |
|----------|------|--------|
| Chat 確認アクションフォーカス | ショートカットで確認ダイアログへ即移動。 | [Focus chat confirmation](https://code.visualstudio.com/updates/v1_104#_focus-chat-confirmation-action) |

## ✏️ Code Editing / Editor Experience
| トピック | 要点 | リンク |
|----------|------|--------|
| インライン補完遅延設定 | 表示タイミングを遅らせノイズ軽減。 | [Inline suggestion delay](https://code.visualstudio.com/updates/v1_104#_configurable-inline-suggestion-delay) |
| ウィンドウ枠色 (Win) | 複数ウィンドウ識別しやすく。 | [Window border color](https://code.visualstudio.com/updates/v1_104#_window-border-color-support-on-windows) |
| 拡張アカウント選択 | Extension ごとにアカウント再割り当て。 | [Manage extension account preference](https://code.visualstudio.com/updates/v1_104#_manage-extension-account-preference) |
| タブインデックス表示 | ショートカット移動支援。 | [Editor tab index](https://code.visualstudio.com/updates/v1_104#_editor-tab-index) |
| タブバースクロール可視性制御 | `workbench.editor.titleScrollbarVisibility`。 | [Tab bar scrollbar](https://code.visualstudio.com/updates/v1_104#_editor-tab-bar-scrollbar-visibility) |
| Issue Reporter 改善 | GitHub での Create/Preview 選択性向上。 | [Issue reporter improvements](https://code.visualstudio.com/updates/v1_104#_issue-reporter-improvements) |

## 📓 Notebooks
| トピック | 要点 | リンク |
|----------|------|--------|
| Next Edit Suggestions (実験) | Notebook 全体文脈でより的確な次編集案。 | [NES suggestions](https://code.visualstudio.com/updates/v1_104#_improved-nes-suggestions-experimental) |

## 🔀 Source Control
| トピック | 要点 | リンク |
|----------|------|--------|
| Worktree 差分プレビュー & 移行 | Worktree との差分比較と一括マイグレーション。 | [Worktree changes](https://code.visualstudio.com/updates/v1_104#_preview-and-migrate-git-worktree-changes) |

## 🖥️ Terminal
| トピック | 要点 | リンク |
|----------|------|--------|
| ⭐別ウィンドウ発見性向上 | 複数エントリポイント追加 & コンパクトモード調整。 | [Terminal window](https://code.visualstudio.com/updates/v1_104#_terminal-window-discoverability-and-polish) |
| エディタ内アクション統一 | エディタ内ターミナルでも同等操作。 | [Terminal actions](https://code.visualstudio.com/updates/v1_104#_terminal-actions-in-terminal-editors) |
| IntelliSense 拡充 | パフォ向上 + 多数コマンド spec 追加。 | [Terminal IntelliSense](https://code.visualstudio.com/updates/v1_104#_terminal-intellisense-improvements-preview) |
| Sticky Scroll 改善 | 既定有効 & Pager 対応洗練。 | [Terminal sticky scroll](https://code.visualstudio.com/updates/v1_104#_terminal-sticky-scroll-improvements) |

## 🧪 Languages (抜粋: JS/TS & Python)
| トピック | 要点 | リンク |
|----------|------|--------|
| Bower IntelliSense 削除 | 老朽化/低利用のため削除。 | [JS/TS](https://code.visualstudio.com/updates/v1_104#_javascript-and-typescript) |
| Pipenv 検出/選択 | Python Environments 拡張が Pipenv を自動管理。 | [Pipenv support](https://code.visualstudio.com/updates/v1_104#_python-environments-extension-support-for-pipenv) |
| .env 注入制御 | `python.useEnvFile` で環境変数挙動切替。 | [Env injection](https://code.visualstudio.com/updates/v1_104#_configure-environment-variable-injection) |
| AI Hover Summary (実験) | 未ドキュメントシンボルを要約表示。 | [AI hover summaries](https://code.visualstudio.com/updates/v1_104#_ai-powered-hover-summaries-with-pylance-experimental) |
| Python Run Snippet Tool | In-memory 実行でエスケープ煩雑さ軽減。 | [Run code snippet tool](https://code.visualstudio.com/updates/v1_104#_run-code-snippet-tool) |
| IntelliSense 全面有効 | すべての Python ドキュメントで Pylance 有効化既定。 | [Pylance IntelliSense](https://code.visualstudio.com/updates/v1_104#_pylance-intellisense-enabled-in-all-python-documents) |
| Activation Hooks 改善 | シェル統合経由で確実に環境活性化。 | [Activation hooks](https://code.visualstudio.com/updates/v1_104#_activation-hooks) |

## 🧩 Extension Authoring / Proposed APIs
| トピック | 要点 | リンク |
|----------|------|--------|
| ⭐ Language Model Chat Provider API | 拡張が独自/ローカル/クラウド LLM を提供。 | [LM Chat Provider](https://code.visualstudio.com/updates/v1_104#_language-model-chat-provider-api) |
| WWW-Authenticate 対応 | MFA などチャレンジ応答を `getSession` で処理。 | [Auth challenges](https://code.visualstudio.com/updates/v1_104#_authentication-supporting-www-authenticate-challenges-in-getsession) |
| Secondary Side Bar への View | `secondarySidebar` へのコンテナ貢献（提案 API）。 | [Secondary Side Bar](https://code.visualstudio.com/updates/v1_104#_view-containers-in-the-secondary-side-bar) |
| shellIntegrationNonce | ターミナル起動時 nonce 制御。 | [shellIntegrationNonce](https://code.visualstudio.com/updates/v1_104#_shellintegrationnonce-for-extension-launched-terminals) |

## 🛠️ Engineering / Notable fixes
内部的な Playwright + MCP 活用実験 (エージェントを開発ループへ) や、多数のメモリリーク/安定性修正が進行。細部は以下を参照。

* [Engineering](https://code.visualstudio.com/updates/v1_104#_engineering)
* [Notable fixes](https://code.visualstudio.com/updates/v1_104#_notable-fixes)

メモ用途なので抜けや誤りあればぜひ突っ込みください。気になったら原文で “Show more” を踏みながら散歩するのがおすすめ。 