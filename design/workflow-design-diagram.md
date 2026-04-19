---
command: workflow-design
version: 1.0.0
updated: 2026-04-17
---

## Workflow設計図

**コマンド名（案）**：workflow-design
**説明**：ユーザーと壁打ちしながら要件を整理し、Workflowの設計図（Mermaidフロー図）を生成するアシスタントコマンド
**引数**：`$ARGUMENTS`（任意）— アイデアを記載したMarkdownファイルのパス、または省略可

### フロー図

```mermaid
flowchart TD
    A["引数: $ARGUMENTS"] --> B{引数あり?}

    B -->|ファイルパス| C["ファイルを読み込む"]
    C --> D["内容を要約してユーザーに伝える"]
    D --> E

    B -->|なし| E["AskUser: 自動化したいフローを教えてください"]

    E --> F["壁打ちループ"]

    F --> G["質問: トリガー・引数"]
    G --> H["質問: ステップ分担"]
    H --> I["質問: Skills・MCPツール"]
    I --> J["質問: 条件分岐・エラー処理"]
    J --> K["質問: 完了条件"]

    K --> L["AskUser: 設計図を作成してよいですか?"]

    L -->|Yes| M["Mermaidフロー図を生成"]
    L -->|No| F

    M --> N["AskUser: 設計図の確認"]

    N -->|修正あり| M
    N -->|確定| O["最終設計図を出力"]

    O --> P["次のステップ案内: /workflow-generate へ渡す"]
```

### 使用するコンポーネント

- **サブエージェント**：なし
- **Skills**：なし（壁打ちはClaudeが直接担当）
- **MCPツール**：なし

---

次のステップ：`/workflow-generate` にこの設計図を渡してMarkdownを生成してください。
