<p align="center">
  <img src="jarbis_banner.png" alt="Jarbis Banner" width="600">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Version-1.0.1-brightgreen.svg" alt="Version">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-Apache_2.0-blue.svg" alt="License"></a>
  <img src="https://img.shields.io/badge/Claude_Code-Plugin-purple.svg" alt="Claude Code Plugin">
  <img src="https://img.shields.io/badge/Patterns-6_Architectures-orange.svg" alt="6 Architecture Patterns">
  <img src="https://img.shields.io/badge/Mode-Agent_Teams-green.svg" alt="Agent Teams">
  <a href="https://github.com/revfactory/jarbis/stargazers"><img src="https://img.shields.io/github/stars/revfactory/jarbis?style=social" alt="GitHub Stars"></a>
</p>

# Jarbis

**Agent Team & Skill Architect** — Claude Code プラグイン

[English](README.md) | [한국어](README_KO.md) | **日本語**

ドメインやプロジェクトに最適なハーネスを構成し、専門エージェントを定義し、エージェントが使用するスキルを生成するメタスキル。

## 概要

Jarbisは、Claude Codeのエージェントチームシステムを活用し、複雑なタスクを専門エージェントチームに分解・統制するアーキテクチャツールです。「ハーネスを構成して」と伝えるだけで、ドメインに適したエージェント定義（`.claude/agents/`）とスキル（`.claude/skills/`）を自動生成します。

## 主な機能

- **エージェントチーム設計** — パイプライン、ファンアウト/ファンイン、エキスパートプール、プロデューサー-レビューア、スーパーバイザー、階層的委任の6種アーキテクチャパターンに対応
- **スキル生成** — Progressive Disclosureパターンによるコンテキストの効率的管理を備えたスキルを自動生成
- **オーケストレーション** — エージェント間のデータ受け渡し、エラーハンドリング、チーム連携プロトコルを内蔵
- **検証体制** — トリガー検証、ドライランテスト、With-skill vs Without-skill 比較テスト

## ワークフロー

```
Phase 1: ドメイン分析
    ↓
Phase 2: チームアーキテクチャ設計（Agent Teams vs サブエージェント）
    ↓
Phase 3: エージェント定義の生成（.claude/agents/）
    ↓
Phase 4: スキル生成（.claude/skills/）
    ↓
Phase 5: 統合とオーケストレーション
    ↓
Phase 6: 検証とテスト
```

## インストール

### マーケットプレイス経由

#### マーケットプレイスの追加
```shell
/plugin marketplace add revfactory/jarbis
```

#### プラグインのインストール
```shell
/plugin install jarbis@jarbis
```

### グローバルスキルとして直接インストール

```shell
# skillsディレクトリを ~/.claude/skills/jarbis/ にコピー
cp -r skills/jarbis ~/.claude/skills/jarbis
```

## プラグイン構成

```
jarbis/
├── .claude-plugin/
│   └── plugin.json                 # プラグインマニフェスト
├── skills/
│   └── jarbis/
│       ├── SKILL.md                # メインスキル定義（6フェーズワークフロー）
│       └── references/
│           ├── agent-design-patterns.md   # 6種のアーキテクチャパターン
│           ├── orchestrator-template.md   # チーム/サブエージェント オーケストレーターテンプレート
│           ├── team-examples.md           # 実践チーム構成例 5種
│           ├── skill-writing-guide.md     # スキル作成ガイド
│           ├── skill-testing-guide.md     # テスト・評価方法論
│           └── qa-agent-guide.md          # QAエージェント統合ガイド
└── README.md
```

## 使い方

Claude Codeで以下のように呼び出します：

```
Build a jarbis for this project
Design an agent team for this domain
Set up a jarbis
```

### 実行モード

| モード | 説明 | 推奨ケース |
|--------|------|------------|
| **Agent Teams**（デフォルト） | TeamCreate + SendMessage + TaskCreate | エージェント2名以上、コラボレーションが必要な場合 |
| **サブエージェント** | Agentツール直接呼び出し | 単発タスク、エージェント間通信不要の場合 |

<p align="center">
  <img src="jarbis_team.png" alt="Jarbis Agent Team" width="500">
</p>

### アーキテクチャパターン

| パターン | 説明 |
|----------|------|
| パイプライン | 順次依存タスク |
| ファンアウト/ファンイン | 並列独立タスク |
| エキスパートプール | 状況に応じた選択的呼び出し |
| プロデューサー-レビューア | 生成後の品質レビュー |
| スーパーバイザー | 中央エージェントによる動的タスク分配 |
| 階層的委任 | 上位→下位への再帰的委任 |

## 出力

Jarbisが生成するファイル：

```
your-project/
├── .claude/
│   ├── agents/          # エージェント定義ファイル
│   │   ├── analyst.md
│   │   ├── builder.md
│   │   └── qa.md
│   └── skills/          # スキルファイル
│       ├── analyze/
│       │   └── SKILL.md
│       └── build/
│           ├── SKILL.md
│           └── references/
```

## ユースケース — そのまま使えるプロンプト

Jarbisインストール後、以下のプロンプトをClaude Codeにコピーしてお使いください：

**ディープリサーチ**
```
Build a jarbis for deep research. I need an agent team that can investigate
any topic from multiple angles — web search, academic sources, community
sentiment — then cross-validate findings and produce a comprehensive report.
```

**ウェブサイト制作**
```
Build a jarbis for full-stack website development. The team should handle
design, frontend (React/Next.js), backend (API), and QA testing in a
coordinated pipeline from wireframe to deployment.
```

**ウェブトゥーン制作**
```
Build a jarbis for webtoon episode production. I need agents for story
writing, character design prompts, panel layout planning, and dialogue
editing. They should review each other's work for style consistency.
```

**YouTube コンテンツ企画**
```
Build a jarbis for YouTube content creation. The team should research
trending topics, write scripts, optimize titles/tags for SEO, and plan
thumbnail concepts — all coordinated by a supervisor agent.
```

**コードレビュー**
```
Build a jarbis for comprehensive code review. I want parallel agents
checking architecture, security vulnerabilities, performance bottlenecks,
and code style — then merging all findings into a single report.
```

**技術ドキュメント作成**
```
Build a jarbis that generates API documentation from this codebase.
Agents should analyze endpoints, write descriptions, generate usage
examples, and review for completeness.
```

**データパイプライン設計**
```
Build a jarbis for designing data pipelines. I need agents for schema
design, ETL logic, data validation rules, and monitoring setup that
delegate sub-tasks hierarchically.
```

**マーケティングキャンペーン**
```
Build a jarbis for marketing campaign creation. The team should research
the target market, write ad copy, design visual concepts, and set up
A/B test plans with iterative quality review.
```

## Jarbisで構築されたプロジェクト

### Jarbis 100

**[revfactory/jarbis-100](https://github.com/revfactory/jarbis-100)** — 10ドメイン、100のプロダクションレディなエージェントチームハーネス（英韓200パッケージ）。各ハーネスには4〜5名の専門エージェント、オーケストレータースキル、ドメイン特化スキルが含まれており、すべて本プラグインで生成されました。コンテンツ制作、ソフトウェア開発、データ/AI、ビジネス戦略、教育、法律、ヘルスケアなど1,808のMarkdownファイル。

### 研究：Jarbis適用前後のA/Bテスト

**[revfactory/claude-code-jarbis](https://github.com/revfactory/claude-code-jarbis)** — 15のソフトウェアエンジニアリング課題を対象とした統制実験で、構造化された事前設定がLLMコードエージェントの出力品質に与える影響を測定しました。

| 指標 | Jarbis未適用 | Jarbis適用 | 改善 |
|------|:-:|:-:|:-:|
| 平均品質スコア | 49.5 | 79.3 | **+60%** |
| 勝率 | — | — | **100%** (15/15) |
| 出力分散 | — | — | **-32%** |

主な発見：課題の難易度が高いほど改善効果が増大（Basic +23.8、Advanced +29.6、Expert +36.2）。

> 論文全文：*Hwang, M. (2026). Jarbis: Structured Pre-Configuration for Enhancing LLM Code Agent Output Quality.*

## 要件

- [Agent Teams機能の有効化](https://code.claude.com/docs/en/agent-teams)：`CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`

## ライセンス

Apache 2.0
