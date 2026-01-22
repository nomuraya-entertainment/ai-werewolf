# AI人狼 - エージェント向けガイド

## セッション引き継ぎ

**最新の引き継ぎIssueを確認**: `gh issue list --label "引き継ぎ" --limit 1` または [Issues](https://github.com/nomuraya-entertainment/ai-werewolf/issues)

---

## クイックリファレンス

### 重要ファイル

| 用途 | パス |
|------|------|
| 知識ベース | `knowledge/index.md` |
| GMロジック | `experiments/v2-minimal/gm-logic.md` |
| プレイヤープロンプト | `experiments/v2-minimal/player-prompt.md` |
| 定跡集 | `knowledge/joseki/index.md` |
| 思考アルゴリズム | `knowledge/algorithm/index.md` |

---

## 知識ベース構造

```
knowledge/
├── index.md              # 全体概要・運用方針
├── tactics/              # 戦術考察（ゲーム前の分析）
│   ├── analysis-framework.md  # 思考フレームワーク
│   └── compositions/     # 構成別の考察
├── logs/                 # ゲームログ（リザルト）
├── joseki/               # 定跡集
│   └── index.md          # 有力な行動とその理由
└── algorithm/            # 思考アルゴリズム
    └── index.md          # 状況判断のアルゴリズム
```

### 4層の役割

| 層 | 目的 | 使用タイミング |
|----|------|---------------|
| tactics/ | 構成の事前分析 | 新構成を試す前 |
| logs/ | ゲーム記録 | ゲーム後 |
| joseki/ | 定跡パターン | プレイヤー注入 |
| algorithm/ | 思考アルゴリズム | プレイヤー注入 |

---

## ゲーム実行方法

### 準備

1. 構成を決める（例: 5人村・村2占1狼1狂1）
2. `tactics/compositions/` で事前考察を確認（なければ作成）
3. 役職を配布

### ゲーム実行

1. GMがTask agentで各プレイヤーを起動
2. プレイヤープロンプト + joseki/ + algorithm/ を注入
3. 発言→投票→夜行動のサイクルを実行
4. 勝敗決定まで繰り返し

### 記録

1. `logs/` にゲーム結果をYAML形式で記録
2. `knowledge/index.md` のサマリーを更新
3. 必要に応じて joseki/, algorithm/ にフィードバック
