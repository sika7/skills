## Workflow設計図

**コマンド名（案）**：`workflow-generate`
**説明**：設計図ファイル（Markdown）を読み込み、Workflowコマンドとサブエージェント定義ファイルを自動生成・保存する
**引数**：`$ARGUMENTS` — 設計図ファイルのパス（例：`./design.md`）

### フロー図

```mermaid
flowchart TD
    A["引数: $ARGUMENTS (設計図ファイルパス)"] --> B["設計図ファイルを読み込む (Read)"]
    B --> C["設計図を解析: コマンド名・引数・ステップ・エージェント・Skills・MCPツールを把握"]
    C --> D["Workflowコマンド用Markdownを生成"]
    D --> E["`.claude/commands/{コマンド名}.md` に保存 (Write)"]
    E --> F{"サブエージェントが設計図に含まれるか"}
    F -->|"あり"| G["各サブエージェント定義Markdownを生成"]
    G --> H["`.claude/agents/{agent-name}.md` に保存 (Write)"]
    H --> I["配置方法・実行方法をターミナルに出力"]
    F -->|"なし"| I
    I --> J["完了"]
```

### 使用するコンポーネント

- **サブエージェント**：なし
- **Skills**：なし
- **MCPツール**：なし（Read / Write ツールのみ使用）

---

次のステップ：`/workflow-generate` にこの設計図を渡してMarkdownを生成してください。
