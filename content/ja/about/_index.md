---
title: 'rehearsalについて'
linkTitle: 'About'
date: 2021-08-30T13:43:38+09:00
hide_readingtime: true
menu:
    main:
        weight: 10
        pre: <i class='fas fa-info-circle'></i>
layout: docs
---

{{% blocks/cover title="rehearsal" height="auto" color="primary" %}}
**rehearsal** はテスト環境を構築するプロセスリレーションツールです。一般的な入出力機能、通信規格を用いて、プロセスレベル、アプリケーションレベル、デバイスレベルで分割されたプロダクト間の通信を行うために使用されます。
{{% /blocks/cover %}}

{{% blocks/cover title="開発時のマインド" height="auto" color="secondary" %}}
プログラムに限らず、何かプロダクトを開発するにあたり、一番時間をかけるべき場所はどこでしょうか？

勿論、その答えは単純明快で、プロダクトが売りにしている場所に時間をかけるべきでしょう。しかし、消費者から見れば同じくらい「安定して動作する」という点に目が行くはずです。そして、プログラムにおいて安定した動作を確認するために、プロダクトが売りにしている場所と同じくらい動作テストに時間を割くべきなのです。

動作テストをより良いものとするために、rehearsalは **「言語・デバイス・目的の壁を越えて」** をコンセプトに開発してきました。標準入出力やTCP通信などの単純な通信方法を相互に変換することで、異なる目的で開発されたテストツールの共通化を目指します。
{{% /blocks/cover %}}

{{% blocks/section type="section" color="white" %}}
# **rehearsal** について{#about}
**rehearsal** はテスト環境を構築するプロセスリレーションツールです。一般的な入出力機能、通信規格を用いて、プロセスレベル、アプリケーションレベル、デバイスレベルで分割されたプロダクト間の通信を行うために使用されます。

> このプロダクト一つ一つの事を **rehearsal** では **「タスク」** と呼んでいます。この仕組みについては[**ドキュメント「タスクの概念について知る」**](/documents/task-concepts)をご覧ください。

ユーザーは `.yaml` 形式の設定ファイルで各タスクの実行内容（実行時のコマンド、使用するポート番号など）や各タスクのデータの送信先などを記述し、 **rehearsal** 実行時に設定ファイルのパスを指定することで実行できます。

#### **Case 1. プロセス間通信やデバイス間通信を標準入出力だけで実現**{#about-case1}

**rehearsal** を用いることで、テストツールから渡されるデータセットや外部との通信内容を送信するインターフェイスと、標準入出力だけを用いて外部とのやり取りを行うビジネスクロックに分離できます。

これにより、開発者はビジネスクロック、アルゴリズムの構築に集中できます。

#### **Case 2. プログラミング言語・デバイスの壁を無視したダイナミックなアプリケーション間通信**{#about-case2}

**rehearsal** では言語特有の機能を利用することは一切ありません。一般的に広く使われている形式を用いたプロセス間通信を行います。

これにより、いままで用いられていたテストツールの流用を容易に行えます。

{{% /blocks/section %}}

{{% blocks/section type="section" color="primary" %}}
## **rehearsal** に対する誤解{#misconception}
**rehearsal** はその立ち位置の難しさから誤解されることが多々あります。
#### **Case 1. rehearsalはテスト環境を提供するのみであり、テストツールではありません**{#misconception-case1}
**rehearsal** は内部にテストを実行・整合性チェック・可視化するための機能を備えていません。問題生成ツールやビジュアライザーなどをユーザー自身が用意し、それらの実行方法や関係性をrehearsal設定ファイルを用いて定義することで、はじめて全体でひとつのテストツールとなります。逆に言えば、どのような構造のテストツール（バッチ形式、出力限定形式、対話形式、測定器）であっても容易に定義できるのです。

#### **Case 2. rehearsalは本番環境で使えるでしょうが、使うべきではないでしょう**{#misconception-case2}
**rehearsal** はメモリ管理を内部で責任もって管理しているため、ある程度は何の問題もなくできると思われますが、静的リンクや内部に組み込まれた関数にはPythonなどの一部のスクリプト言語を除いて速度面で遠くおよびません。

また、ライセンスにGPLv3を適用しているため、動的なリンクを目的に **rehearsal** を内包した状態で頒布を行う場合には、ソースコードの公開義務が生じることもお忘れのないように（サーバー内部で利用する場合、内部で利用する場合において、ソースコードの公開義務は慣例的に生じません）。

{{% /blocks/section %}}

{{% blocks/section type="section" color="white" %}}
## ライセンス{#license}

**rehearsal** は **GNU General Public License version 3** の下に提供されます。ライセンス内容は以下をご覧ください。

[GNU General Public Lisense v3.0 (https://github.com/rehearsal-open/rehearsal/blob/nightly/LICENSE)](https://github.com/rehearsal-open/rehearsal/blob/nightly/LICENSE)

{{% /blocks/section %}}
