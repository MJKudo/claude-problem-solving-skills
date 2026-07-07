# Claude Code 構造化問題解決スキル

[Claude Code](https://claude.com/claude-code) 用の構造化問題解決ワークフロースキル2種。いずれも6工程(**問題構造の明確化 → 目標状態の定義 → 課題の特定 → 要件定義 → 手順計画 → レポート**)で問題を扱い、各工程の成果物を会話履歴を持たない独立サブエージェントが批判的にレビューし、疑義があれば上流工程へ巻き戻す。明示起動のみ(自動起動しない)。内容は日本語。

## 収録スキル

### consulting-workflow

最上席コンサルタントとして、要望の背景にある問題構造から解決までを6工程で扱う汎用の問題解決ワークフロー。システム思考の氷山モデル(出来事→パターン→構造→メンタルモデル)で問題構造を把握し、競合仮説の並置と反証、システム境界の宣言、介入点の深さ×実行可能性の検討などを組み込む。

### system-analysis-workflow

装置システム・Web システム等の技術課題を6工程で分析する。**障害モード**(発生済み不具合の原因究明)と**改善モード**(改修・構築の構想)を持つ。証拠収集と仮説検証、原因分析手法の使い分け(特性要因図/FTA/FMEA/5 Whys)、複数の寄与要因の考慮に加え、次の安全規範を備える:

- 操作手順は状態の復元手段の事前確保、または再現可能な記録を必須とする
- 稼働中の本番環境への直接の不可逆操作を禁止(環境が本番か不明な場合は本番とみなす)
- 提示資料は「正しくない前提」で実態と突合する

## 共通の設計

- 6工程の線形フロー + 疑義時の巻き戻し + 問題の複雑さに応じた反復運用(起動時に線形/複雑を軽く分類)
- 各工程で独立サブエージェントによる重大度付き(CRITICAL/HIGH/MEDIUM/LOW)レビュー
- 難解用語・独自定義語のラベリング禁止(初出時に平易な言葉で定義)
- 事実の出所表記((確認済み)/(資料記載)/(推定)/(帰結))で事実と推測を区別(system-analysis)
- 原典・研究(氷山モデル、McKinsey 問題解決、Cynefin、RCA、SRE postmortem 等)に基づく設計

## インストール

各スキルフォルダを `~/.claude/skills/` 配下にコピーする:

```bash
cp -r consulting-workflow ~/.claude/skills/
cp -r system-analysis-workflow ~/.claude/skills/
```

Claude Code で `/consulting-workflow` または `/system-analysis-workflow` として起動する。

## 構成

```
consulting-workflow/
  SKILL.md                        # 6工程フロー・共通サイクル・行動規範
  references/
    stage-templates.md            # 各工程の成果物テンプレート
    review-prompt.md              # 独立レビュワー用プロンプト
    handoff-templates.md          # 引継書テンプレート
system-analysis-workflow/
  SKILL.md
  references/
    stage-templates.md
    investigation-guide.md        # 調査・検証・本番保護の手順
    review-prompt.md
    handoff-templates.md
```

## ライセンス

両スキルとも [MIT License](LICENSE)。各スキルフォルダにも同一の LICENSE を同梱しているため、フォルダ単位でコピーしてもライセンスが携行される。

