---
title: クイックリファレンス用Gitチートシート
---

## クイックリファレンス用Gitチートシート

- 様々な言語で印刷可能なGitチートシートが[こちら](https://github.github.com/training-kit/)から利用できます（[英語版はこちら](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)）。さらに多くの資料が[GitHubトレーニングサイト](https://try.github.io/)にあります。
- ワークスペース、ステージングエリア、ローカルリポジトリ、アップストリームリポジトリ間の関係と、それぞれに関連するコマンドを説明する[インタラクティブな一枚の可視化ツール](https://ndpsoftware.com/git-cheatsheet.html)も利用可能です。
- これらのリソースは、スペイン語、フランス語など、他の言語でも利用可能です。
- "[Happy Git and GitHub for the useR](https://happygitwithr.com)"は、Jenny Bryanによる無料でアクセス可能なオンラインブックで、GitとGitHubを設定して使用する方法を解説しています。特にRStudioとの統合やRでGitを使用する方法についての詳細が含まれています。
- [GitとGitHubを使用したオープンサイエンス](https://open-source-for-researchers.github.io/open-source-workshop/) - バージョン管理やオープンソースソフトウェアについて研究者が学べるように、説明と短い実践課題をまとめたものです。

## 用語集

[changeset]{#changeset}
:   1つ以上のファイルに対する変更のグループ。これが[バージョン管理](#version-control)の[リポジトリ](#repository)に単一の[コミット](#commit)として追加される、またはされる予定です。

[commit]{#commit}
:   一連のファイル（[変更セット](#changeset)）の現在の状態を[バージョン管理](#version-control)の[リポジトリ](#repository)に記録すること。名詞としては、リポジトリに記録された変更セット、つまりコミットを指します。コミットには複数のファイルの変更が含まれる場合があり、すべての変更が一緒に記録されます。

[conflict]{#conflict}
:   [バージョン管理システム](#version-control)の他のユーザーによる変更と互換性がない変更。コンフリクトを[解決する](#resolve)ことは、バージョン管理の主要なタスクの1つです。

[HTTP]{#http}
:   Webページやその他のデータをワールドワイドウェブ上で共有するために使用されるハイパーテキスト転送[プロトコル](#protocol)。

[merge]{#merge}
:   （リポジトリ）2つの変更セットを[リポジトリ](#repository)に統合すること。

[protocol]{#protocol}
:   1台のコンピュータが別のコンピュータと通信する方法を定義する一連のルール。インターネット上で一般的なプロトコルには[HTTP](#http)や[SSH](#ssh)があります。

[remote]{#remote}
:   （リポジトリ）他のリポジトリと接続され、[コミット](#commit)を交換することで同期を保つことができる[バージョン管理](#version-control)の[リポジトリ](#repository)。

[repository]{#repository}
:   プロジェクトの[コミット](#commit)の完全な履歴と、誰がいつ何を変更したかに関する情報を保存する[バージョン管理](#version-control)システムの保存領域。

[resolve]{#resolve}
:   [バージョン管理](#version-control)システムで管理されているファイルまたはファイルセットへの2つ以上の互換性のない変更間の[コンフリクト](#conflict)を解消すること。

[revision]{#revision}
:   [コミット](#commit)の同義語。

[SHA-1]{#sha-1}
:   [SHA-1ハッシュ](https://en.wikipedia.org/wiki/SHA-1)はGitが識別子を計算するために使用するものです。これにはコミットの実際の変更だけでなく、日付、著者、メッセージなどのメタデータ、さらには前の変更のすべてのコミット識別子も含まれます。このため、GitのコミットIDは事実上ユニークです。すなわち、独立して行われた2つのコミットが、同じ変更であっても同じIDを受け取る可能性は極めて低いです。

[SSH]{#ssh}
:   コンピュータ間での安全な通信に使用されるセキュアシェル[プロトコル](#protocol)。

[timestamp]{#timestamp}
:   特定のイベントが発生した時刻の記録。

[version control]{#version-control}
:   ファイルセットへの変更を管理するツール。各変更セットは新しい[コミット](#commit)を作成します。バージョン管理システムは、古いコミットを確実に復元できるようにし、異なるユーザーによって行われた競合する変更を管理するのに役立ちます。