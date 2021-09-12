---
title: 'タスクの概念を知る'
linkTitle: 'タスクの概念'
date: 2021-09-09T16:48:06+09:00
type: docs
weight: 10
description: rehearsalでは、TCP通信を使用するプロセスや内部でアプリケーションを実行するプロセスをそれぞれ一つの「タスク」という単位で分割し、実行および入出力の監視を行っています。この章ではrehearsal内部におけるタスクの管理、監視、実行のプロセスを紹介します。
---

# rehearsalとは？

[「rehearsalについて（about）」](/about/#rehearsal-%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)でも述べたように、rehearsalは自らの定義を「プロセスリレーションツール」と位置づけています。具体的には、各プロセス間の入出力を監視し、「任意の形式」に変換したうえで出力をほかのプロセスの入力として与えます。任意の形式には標準入出力、シリアル通信、TCP通信などが含まれており、rehearsalは内部で相互変換を行い、任意のプロセスに入力データとして与えます。

以下は標準入出力を使用するプログラムを用いた場合のイメージ図です。
```mermaid
graph TD
    reciever([受信モジュール])
    sender([送信モジュール])

    シリアル通信の受信データ-->reciever
    他プログラムの標準出力-->reciever
    TCP通信の受信データ-->reciever
    subgraph rehearsal CUIタスク
        reciever-->|標準入力|プログラム
        プログラム-->|標準出力/標準エラー出力|sender
    end
    sender-->シリアル通信の送信データ
    sender-->他プログラムの標準入力
    sender-->TCP通信の送信データ
```
ここでひとつ重要なことがあります。 **上に示されている「rehearsal CUIタスク」の外部にあるデータはすべて他のタスクによって管理されているということです。** シリアル通信の受信データもそれを実際にシリアル通信から受信ためのタスクがあり、他プログラムの標準出力もそれを受け取るためのタスクが存在します。

タスクは内部で実行しているプロセスを監視するだけでなく、他プロセスへ出力を送信、そのデータを入力データとして内部で実行しているプロセスに送信する働きを担っているのです。