---
title: 'rehearsal-cli（コマンドラインツール）'
linkTitle: 'rehearsal-cli（コマンドラインツール）'
date: 2021-09-09T16:35:43+09:00
type: docs
description: rehearsal-cliはYAML形式のテンプレートファイルを使用して実際に実行するためのツールです。この章では、rehearsal-cliのインストール方法、実行コマンドを紹介します。
---

rehearsal-cliで使用できるコマンドについて解説します。

## `rehearsal-cli run`コマンド{#command-run}
### 概要{#command-run-abstract}
テンプレートファイルに基づいてタスクを実行します。テンプレートファイルについては[ドキュメント「YAMLテンプレートファイル」](/documents/yaml-template)をご覧ください。

### コマンドオプション{#command-run-options}
#### 【必須】`--path`, `-p`オプション{#command-run-options-path}
テンプレートファイルを指定するためのパスです。絶対パス・相対パス共に使用できますが、相対パスの場合は現在開いているディレクトリを基準にします。

#### 【任意】`--plain`オプション{#command-run--optionsplain}
rehearsalで出力するログを平たいテキストで表示します。これを設定しない場合は各タスクごとに文字色のあるログが生成されます。

ログをファイルに出力する場合はこのオプションを設定するべきです。

#### 【任意】`-h`, `--help`オプション{#command-run-options-help}
ヘルプを表示します。
### 例{#command-run-example}
```bash
$ rehearsal-cli run --p ./rehearsal.yml
$ rehearsal-cli run --p ./rehearsal.yml --plain > ./log.txt
```

## `rehearsal-cli help`コマンド{#command-help}
### 概要{#command-help-abstract}
ヘルプを表示します。
### 例{#command-help-example}
```bash
$ rehearsal-cli help
```

## `rehearsal-cli version`コマンド{#command-version}
### 概要{#command-version-abstract}
rehearsalのバージョン情報を表示します。

### 例{#command-version-example}
```bash
$ rehearsal-cli version
```
