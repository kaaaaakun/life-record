# Life Record

このリポジトリは、GitHub Issuesを使用して日々のジャーナル（振り返りや学んだこと）を自動でMarkdown形式に変換し、リポジトリに保存する仕組みを提供します。GitHub Actionsを利用して、自動でIssue生成され、クローズされた際に自動でMarkdownファイルが生成され、`issues/`ディレクトリに保存されます。

## 目次
- [概要](#概要)
- [フォークして使用する方法](#フォークして使用する方法)
- [ディレクトリ構成](#ディレクトリ構成)
- [使い方](#使い方)
- [設定の変更方法](#設定の変更方法)
- [カスタマイズ方法](#カスタマイズ方法)

---

## 概要

このリポジトリは、日々のタスクや学びをGitHub Issuesで管理し、それをMarkdown形式で保存することで日記のように記録できるツールです。  
クローズされたIssueは、自動でMarkdownファイルに変換され、リポジトリの`issues/`ディレクトリに保存されます。

---

## フォークして使用する方法

1. このリポジトリをGitHub上でフォークします。
2. フォークしたリポジトリを自分のローカルにクローンする必要はありません。
3. Settings > Actions > General の中で、GITHUB_TOKENの権限が「Read and write」に設定してください。<img width="809" alt="スクリーンショット 2024-09-09 18 41 15" src="https://github.com/user-attachments/assets/07dcd2ca-571e-40ae-944c-7406db26dada">
4. リポジトリにある`.github/workflows`と`ISSUE_TEMPLATE`を必要に応じてカスタマイズします（後述）。
5. GitHub上で新しいIssueを作成し、日々のタスクや学びを記録します。
6. Issueをクローズすると、GitHub Actionsが自動でMarkdownファイルを生成し、`issues/`フォルダに保存されます。

---

## ディレクトリ構成

```
├── .github
│   ├── ISSUE_TEMPLATE
│   │   ├── to-do.md                  # To-Do Issue用のテンプレート
│   ├── journal.md                    # 日記のテンプレート
│   └── workflows
│       ├── issue-close-to-markdown.yml # クローズしたIssueをMarkdownに変換するワークフロー
│       └── issue-open.yml               # Issueをオープン時にトリガーするワークフロー
├── .gitignore                         # 不要なファイルをGit管理から除外
├── README.md                          # ドキュメントファイル
└── issues
    └── .gitkeep                       # 空のissuesフォルダをGitに保持するためのファイル
```

### 主なファイル説明

1. **`.github/ISSUE_TEMPLATE/to-do.md`**  
   Issueを作成する際に使用するTo-Do形式のテンプレートです。
   
2. **`.github/workflows/issue-close-to-markdown.yml`**  
   Issueがクローズされた際に自動でその内容をMarkdownファイルに変換するGitHub Actionの設定です。

3. **`issues/`**  
   クローズされたIssueの内容がMarkdown形式で保存されるディレクトリです。

---

## 使い方

### 1. **新しいジャーナル（Issue）を作成**

- 大きなToDoに関して
1. GitHubリポジトリの「Issues」タブを開き、「New Issue」をクリックします。
2. **To-Do**テンプレートを選択します。
3. 大きなプロジェクトはそのように管理できます。

- 毎日の日記に関して
1. 毎朝自動でIssueが作成されます。
2. そのIssueを編集してタスクやや学んだこと、振り返り、その他のメモを記入します。

**注意**: 画像もアップすることができますが、リポジトリ内には保存されず、リンクのみが保存されます。

### 2. **Issueをクローズ**

1. その日のタスクが完了したら、Issueをクローズします。
2. 自動でGitHub Actionsが起動し、Issueの内容がMarkdown形式に変換されます。

### 3. **ジャーナルの確認**

- `issues/`フォルダ内に、クローズされたIssueの内容がMarkdownファイルとして保存されます。ファイル名はIssueのクローズ日時が反映されます。

---

## 設定の変更方法

### 1. **GitHub Actionsの設定**

ワークフローは`.github/workflows/`ディレクトリにあります。ここでは、GitHubでのイベント（Issueがクローズされた時など）をトリガーにして自動処理を行います。

- **`issue-close-to-markdown.yml`**  
  Issueがクローズされた時にトリガーされ、Issueの内容をMarkdownファイルに変換します。

### 2. **Issueテンプレートのカスタマイズ**

Issueを作成する際のテンプレートは`.github/ISSUE_TEMPLATE/`内にあります。  
`to-do.md`ファイルを編集して、必要なフィールドを追加・削除することができます。

### 3. **環境変数の設定**

GitHub Actionsでは、`GITHUB_TOKEN`が必要になります。この設定はGitHubリポジトリの「Settings」 > 「Secrets」 で設定してください。  
これにより、APIリクエストが認証され、アクションが正常に実行されます。

---

## カスタマイズ方法

### 1. **Issueテンプレートのカスタマイズ**

`.github/ISSUE_TEMPLATE/to-do.md`を編集して、自分に合ったテンプレートを作成できます。  
例えば、以下のようなフィールドを追加することが可能です：

```markdown
## 新たな挑戦
- [ ] 新しいスキルを学ぶ
- [ ] 読書

### 2. **GitHub Actionsのカスタマイズ**

ワークフローをカスタマイズする場合は、`.github/workflows/`内のYAMLファイルを編集します。  
例えば、追加のメタデータをMarkdownに含める場合は、`issue-close-to-markdown.yml`を編集し、`Create markdown file`ステップを修正してください。

---

## 例

### Issueの例

**Issue タイトル**: `Daily Journal - 2024-09-10`

**Issue 本文**:
```markdown
## 今日の予定
- [x] タスク1
- [ ] タスク2

## 学んだこと
- 新しいアルゴリズムの概念を理解した。

## 振り返りと反省
- タスク管理をもっと改善する必要がある。

## 明日やること
- タスク2を完了させる。

## その他メモ
- プロジェクトの進捗を確認する。
```

### 生成されたMarkdownファイル

**`issues/2024-09-10.md`**:
```markdown
Daily Journal - 2024-09-10
-------------------------

## 今日の予定
- [x] タスク1
- [ ] タスク2

## 学んだこと
- 新しいアルゴリズムの概念を理解した。

## 振り返りと反省
- タスク管理をもっと改善する必要がある。

## 明日やること
- タスク2を完了させる。

## その他メモ
- プロジェクトの進捗を確認する。

**Closed on**: 2024-09-10T17:20:00+0900
```

---

この構成により、GitHub Issuesを使用して簡単に日々の振り返りや学びを記録し、それをMarkdownファイルとして保存して参照できるようになります。
