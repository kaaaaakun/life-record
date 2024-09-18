# 概要

このリポジトリは、日々のタスクや学びをGitHub Issuesで管理し、クローズしたIssueをMarkdown形式で保存するツールです。  
毎朝自動でジャーナルIssueが作成され、その日の振り返りを記録。クローズ後にIssue内容は`issues/`ディレクトリにMarkdown形式で保存されます。  
同様に、自分で作成したIssueもクローズ時にMarkdownとして保存されます。

---

# 使用方法

1. **リポジトリのフォーク**
    - GitHubでこのリポジトリをフォーク
    - フォークしたリポジトリのSettingsでGITHUB_TOKENの権限を「Read and write」に設定
    - 必要に応じて`.github/workflows`や`ISSUE_TEMPLATE`をカスタマイズ

2. **ジャーナルの自動作成**
    - 毎朝、ジャーナルIssueが自動作成される
    - Issueにタスクや学んだことを記録

3. **Issueをクローズ**
    - タスク完了後、Issueをクローズ
    - 自動でMarkdownファイルが生成され、`issues/`フォルダに保存

---

# ディレクトリ構成

```
├── .github
│   ├── ISSUE_TEMPLATE
│   │   ├── to-do.md                  # To-Do Issue用テンプレート
│   ├── journal.md                    # 日記テンプレート
│   └── workflows
│       ├── issue-close-to-markdown.yml # クローズIssueをMarkdown変換するワークフロー
│       └── issue-open.yml               # Issue作成時のワークフロー
├── issues
└── README.md
```

---

# カスタマイズ

1. **テンプレートのカスタマイズ**
    - `.github/ISSUE_TEMPLATE/`内のテンプレートを編集して、To-Doや日記のフォーマットを変更

2. **GitHub Actionsの変更**
    - `.github/workflows/`内のYAMLファイルを編集し、アクション内容や動作条件を調整

3. **環境変数の設定**
    - `GITHUB_TOKEN`をリポジトリのSettings > Secretsで設定し、認証やAPIリクエストを管理

---

# 例

### Issueの例

```markdown
## 今日の予定
- [x] タスク1
- [ ] タスク2

## 学んだこと
- 新しいアルゴリズムを学んだ

## 振り返り
- タスク管理の改善が必要

## 明日の予定
- タスク2を完了する
```

### 生成されたMarkdownファイル

```
issues/2024-09-10.md

## 今日の予定
- [x] タスク1
- [ ] タスク2

## 学んだこと
- 新しいアルゴリズムを学んだ

## 振り返り
- タスク管理の改善が必要

## 明日の予定
- タスク2を完了する

Closed on: 2024-09-10
```

---

このリポジトリを使うことで、GitHub Issuesを日記やTo-Doリストとして活用し、クローズ後にMarkdownファイルとして自動保存されます。