---
title: GitHub におけるリモート
teaching: 45
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- リモートリポジトリとは何なのか、そしてなぜそれが役立つのかを説明します。
- リモートリポジトリへのプッシュまたはリモートリポジトリからのプル。

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- 自分の変更をウェブ上で他の人と共有するにはどうすればよいですか？

::::::::::::::::::::::::::::::::::::::::::::::::::

バージョン管理が真価を発揮するのは、他の人々と共同作業を始めるときです。  これを行うために必要な機構のほとんどはすでに揃っています。
唯一欠けているのは、あるリポジトリから別のリポジトリに変更をコピーすることです。

Git のようなシステムを使用すると、任意の 2 つのリポジトリ間で作業結果を動かすことができます。  ただし、実際には、1 つのコピーを中央ハブとして使用し、それを誰かのラップトップではなくウェブ上に
保管するのが最も簡単です。  ほとんどのプログラマーは、[GitHub](https://github.com) や [Bitbucket](https://bitbucket.org)、あるいは [GitLab](https://gitlab.com/) のようなホスティングサービス
に、これらのメインコピーを保持しています。この長所と短所については、[後のエピソード](13-hosting.md) で探ります。

まずは、現在のプロジェクトに加えた変更を世界と共有することから始めましょう。 この目的のために、_ローカル_ リポジトリにリンクされる _リモート_ リポジトリを作成します。

## 1\. リモートリポジトリを作成する。

[GitHub](https://github.com) にログインし、右上隅のアイコンをクリックして `planets` という名前の新しいリポジトリを作成してみましょう：

![](fig/github-create-repo-01.png){alt='The first step in creating a repository on GitHub: clicking the "create new" button'}

リポジトリに「planets」という名前を付けて、「Create Repository」をクリックします。

注: このリポジトリはローカルのリポジトリに接続されるため、空にしておく必要があります。 「Initialize this repository with a README」のチェックを外したままにし、「Add .gitignore」と「Add a license.」の両方のオプションを「None」のままにします。 リポジトリを空にしておく必要がある理由の完全な説明については、以下の「GitHub ライセンスと README ファイル」の演習を参照してください。

![](fig/github-create-repo-02.png){alt='The second step in creating a repository on GitHub: filling out the new repository form to provide the repository name, and specify that neither a readme nor a license should be created'}

リポジトリが作成されるとすぐに、GitHub には ある URL と、ローカルのリポジトリの構成方法に関する情報が記載されたページが表示されます。

![](fig/github-create-repo-03.png){alt='The summary page displayed by GitHub after a new repository has been created. It contains instructions for configuring the new GitHub repository as a git remote'}

これにより、GitHub のサーバー上で次のことが効果的に行われます。

```bash
$ mkdir planets
$ cd planets
$ git init
```

もしあなたが以前の [エピソード](04-changes.md) を覚えていれば、私達は `mars.txt` に以前の作業を追加してコミットしました。
ローカルリポジトリのダイアグラムは次のようになります：

![](fig/git-staging-area.svg){alt='「git add」で変更がステージングエリアに登録され、「git commit」でステージングエリアからリポジトリに変更が移動する様子を示した図'}

現在、2つのリポジトリを持っているので、このような図が必要です：

![](fig/git-freshly-made-github-repo.svg){alt='GitHubの「planets」リポジトリが、ローカルリポジトリと同様にgitリポジトリであることを示す図。ただし、現在は空の状態。'}

ローカルリポジトリには先ほど作成した `mars.txt` に関する作業がまだ含まれていますが、  
GitHub上のリモートリポジトリはまだファイルが含まれていないため空に見えます。

## 2\. ローカルリポジトリとリモートリポジトリを接続する

次に、2つのリポジトリを接続します。これを行うには、GitHubリポジトリをローカルリポジトリの[リモート](../learners/reference.md#remote)として設定します。  
GitHub上のリポジトリのホームページには、それを特定するために必要なURL文字列が含まれています：

![](fig/github-find-repo-string.png){alt='GitHubでリポジトリのURLを取得するために「Copy to Clipboard」ボタンをクリックする様子'}

'SSH'リンクをクリックして、[プロトコル](../learners/reference.md#protocol)をHTTPSからSSHに変更してください。

:::::::::::::::::::::::::::::::::::::::::  callout

## HTTPS 対 SSH

ここではSSHを使用します。SSHは追加の設定が必要ですが、多くのアプリケーションで広く使用されているセキュリティプロトコルです。以下の手順は、GitHubでのSSHの基本的な使い方について説明しています。

::::::::::::::::::::::::::::::::::::::::::::::::::

![](fig/github-change-repo-string.png){alt='「SSH」をクリックすると、GitHubがリポジトリのHTTPS URLの代わりにSSH URLを提供する様子'}

そのURLをブラウザからコピーし、ローカルの `planets` リポジトリに移動して、次のコマンドを実行します：

```bash
$ git remote add origin git@github.com:vlad/planets.git
```

自分のリポジトリのURLを使用することを忘れないでください。`vlad` の代わりに自分のユーザー名に変更するだけです。

`origin` はリモートリポジトリを指すローカル名です。他の名前を付けても構いませんが、`origin` はGitやGitHubでデフォルトとしてよく使われる慣例的な名前です。特別な理由がない限り、この名前を使用するのが便利です。

コマンドが正しく動作したかどうかを確認するには、次のコマンドを実行します：

```bash
$ git remote -v
```

```output
origin   git@github.com:vlad/planets.git (fetch)
origin   git@github.com:vlad/planets.git (push)
```

リモートについては、次のエピソードでコラボレーションでの活用方法を説明しながら詳しく議論します。

## 3\. SSH の背景と設定

ドラキュラがリモートリポジトリに接続するには、GitHubが彼のコンピュータで認証されていることを確認する方法を設定する必要があります。
これから説明する方法は、コマンドラインでアクセスを認証するために多くのサービスで一般的に使用されている方法です。この方法は「Secure Shell Protocol（SSH）」と呼ばれます。
SSHは暗号化ネットワークプロトコルで、安全でないネットワークを使用しても、コンピュータ間で安全な通信を可能にします。

SSHは「鍵ペア」というものを使用します。鍵ペアは、アクセスを検証するために一緒に動作する2つの鍵です。1つは「公開鍵」と呼ばれる公開される鍵で、もう1つは秘密にされる「秘密鍵」です。それぞれの名前の通りの役割を持っています。

公開鍵を南京錠、秘密鍵をその南京錠を開ける鍵と考えることができます。公開鍵をGitHubのような安全な通信を必要とする場所に提供します。これにより、「この南京錠（公開鍵）を使って私のアカウントへの通信をロックしてください。私の秘密鍵を持っているコンピュータだけが通信を解除し、Gitコマンドを私のGitHubアカウントとして送信できます」と指示することができます。

ここでは、SSH鍵を設定し、公開鍵をGitHubアカウントに追加するために必要な最小限の手順を説明します。

:::::::::::::::::::::::::::::::::::::::::  callout

## SSH（上級編）

このレッスンの補足エピソードでは、SSHと鍵ペアについてさらに深く詳しく説明しています。

::::::::::::::::::::::::::::::::::::::::::::::::::

まず最初に、この作業が現在使用しているコンピュータで既に行われているかどうかを確認します。一般的に、この設定は一度行えば、それ以降は再設定する必要はありません。

:::::::::::::::::::::::::::::::::::::::::  callout

## 鍵を安全に保つ

SSH鍵はアカウントのセキュリティを守るためのものなので、本当に「忘れる」べきではありません。定期的にSSH鍵を監査するのは良い習慣です。特に複数のコンピュータからアカウントにアクセスしている場合は注意が必要です。

::::::::::::::::::::::::::::::::::::::::::::::::::

以下のリストコマンドを実行して、既に存在する鍵ペアを確認します。

```bash
ls -al ~/.ssh
```

使用しているコンピュータでSSHが設定されているかどうかによって、出力は異なります。

ドラキュラのコンピュータではSSHがまだ設定されていないため、出力は次のようになります：

```output
ls: cannot access '/c/Users/Vlad Dracula/.ssh': No such file or directory
```

もしSSHが設定済みの場合、公開鍵と秘密鍵がリストされます。鍵ペアは設定方法に応じて、`id_ed25519`/`id_ed25519.pub` または `id_rsa`/`id_rsa.pub` という名前になっています。\
ドラキュラのコンピュータには鍵が存在しないため、次のコマンドを使って鍵を作成します。

### 3\.1 SSH鍵ペアを作成する

SSH鍵ペアを作成するには、以下のコマンドを使用します。`-t` オプションでアルゴリズムの種類を指定し、`-C` で鍵にコメントを追加します（ここではドラキュラのメールアドレスを使用しています）。

```bash
$ ssh-keygen -t ed25519 -C "vlad@tran.sylvan.ia"
```

もし古いシステムでEd25519アルゴリズムがサポートされていない場合は、次のコマンドを使用してください：
`$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

```output
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/Vlad Dracula/.ssh/id_ed25519):
```

デフォルトのファイルを使用するので、<kbd>Enter</kbd> を押してください。

```output
Created directory '/c/Users/Vlad Dracula/.ssh'.
Enter passphrase (empty for no passphrase):
```

ここでパスフレーズの入力を求められます。他の人がアクセスする可能性のある研究室のラップトップを使用しているため、ドラキュラはパスフレーズを作成します。
覚えやすいものを使うか、どこかに保存してください。パスワードリセットオプションはありません。
ターミナルでパスフレーズを入力しても、入力内容が画面に表示されないのは正常です。

```output
Enter same passphrase again:
```

2回目のパスフレーズ入力後、次の確認メッセージが表示されます：

```output
Your identification has been saved in /c/Users/Vlad Dracula/.ssh/id_ed25519
Your public key has been saved in /c/Users/Vlad Dracula/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:SMSPIStNyA00KPxuYu94KpZgRAYjgt9g4BA4kFy3g1o vlad@tran.sylvan.ia
The key's randomart image is:
+--[ED25519 256]--+
|^B== o.          |
|%*=.*.+          |
|+=.E =.+         |
| .=.+.o..        |
|....  . S        |
|.+ o             |
|+ =              |
|.o.o             |
|oo+.             |
+----[SHA256]-----+
```

「identification（識別情報）」とは秘密鍵を指します。これは絶対に共有しないでください。公開鍵はその名の通り公開して問題ありません。
「key fingerprint（鍵のフィンガープリント）」は、公開鍵の短縮版です。

SSH鍵を生成したので、再度確認してみましょう。

```bash
ls -al ~/.ssh
```

```output
drwxr-xr-x 1 Vlad Dracula 197121   0 Jul 16 14:48 ./
drwxr-xr-x 1 Vlad Dracula 197121   0 Jul 16 14:48 ../
-rw-r--r-- 1 Vlad Dracula 197121 419 Jul 16 14:48 id_ed25519
-rw-r--r-- 1 Vlad Dracula 197121 106 Jul 16 14:48 id_ed25519.pub
```

### 3\.2 公開鍵をGitHubにコピーする

SSH鍵ペアができたので、GitHubが認証情報を読み取れるか確認します。

```bash
ssh -T git@github.com
```

```output
The authenticity of host 'github.com (192.30.255.112)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? y
Please type 'yes', 'no' or the fingerprint: yes
Warning: Permanently added 'github.com' (RSA) to the list of known

 hosts.
git@github.com: Permission denied (publickey).
```

ここで公開鍵をGitHubに渡すのを忘れていることに気付きます！

まず、公開鍵をコピーします。`.pub` を含めて指定してください。そうしないと秘密鍵を見てしまいます。

```bash
cat ~/.ssh/id_ed25519.pub
```

```output
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDmRA3d51X0uu9wXek559gfn6UFNF69yZjChyBIU2qKI vlad@tran.sylvan.ia
```

次にGitHub.comにアクセスし、右上のプロフィールアイコンをクリックしてドロップダウンメニューを開きます。「Settings（設定）」をクリックし、設定ページの左側メニューから「SSH and GPG keys」を選択します。右側の「New SSH key」ボタンをクリックします。
ここで、タイトルを入力し（ドラキュラは「Vlad's Lab Laptop」と名付け、元の鍵ペアファイルの場所を覚えられるようにしました）、SSH鍵をフィールドに貼り付け、「Add SSH key」をクリックして設定を完了します。

設定が完了したので、再度認証を確認してみましょう。

```bash
$ ssh -T git@github.com
```

```output
Hi Vlad! You've successfully authenticated, but GitHub does not provide shell access.
```

よし！この出力はSSH鍵が正常に機能していることを確認しています。これでリモートリポジトリに作業をプッシュする準備が整いました。

## 4\. ローカルの変更をリモートにプッシュする

認証設定が完了したので、リモートリポジトリに戻りましょう。このコマンドを使用して、ローカルリポジトリの変更をGitHubのリポジトリにプッシュします：

```bash
$ git push origin main
```

ドラキュラがパスフレーズを設定している場合、入力を求められます。高度な認証設定を完了している場合は、パスフレーズを求められることはありません。

```output
Enumerating objects: 16, done.
Counting objects: 100% (16/16), done.
Delta compression using up to 8 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (16/16), 1.45 KiB | 372.00 KiB/s, done.
Total 16 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), done.
To https://github.com/vlad/planets.git
 * [new branch]      main -> main
```

:::::::::::::::::::::::::::::::::::::::::  callout

## プロキシ

もし接続しているネットワークがプロキシを使用している場合、最後のコマンドが「ホスト名を解決できません」というエラーメッセージで失敗することがあります。この問題を解決するには、Gitにプロキシ情報を伝える必要があります：

```bash
$ git config --global http.proxy http://user:password@proxy.url
$ git config --global https.proxy https://user:password@proxy.url
```

プロキシを使用していないネットワークに接続した際には、次のコマンドを使ってプロキシを無効化する必要があります：

```bash
$ git config --global --unset http.proxy
$ git config --global --unset https.proxy
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## パスワードマネージャー

オペレーティングシステムにパスワードマネージャーが設定されている場合、`git push` はユーザー名とパスワードが必要な際にそれを使用しようとします。たとえば、WindowsのGit Bashではこれがデフォルトの動作です。ターミナルでユーザー名とパスワードを直接入力したい場合は、次のコマンドを実行してください：

```bash
$ unset SSH_ASKPASS
```

この設定により、Gitがターミナルで直接ユーザー名とパスワードを使用するようになります。また、`~/.bashrc` の最後に `unset SSH_ASKPASS` を追加すると、デフォルトでターミナルでの入力が使用されるようになります。

::::::::::::::::::::::::::::::::::::::::::::::::::

ローカルリポジトリとリモートリポジトリの状態は次のようになります：

![](fig/github-repo-after-first-push.svg){alt='「git push origin」でローカルリポジトリの変更をリモートにプッシュし、リモートリポジトリがローカルリポジトリの正確なコピーになる様子'}

:::::::::::::::::::::::::::::::::::::::::  callout

## `-u` フラグ

一部のドキュメントでは、`git push` コマンドで `-u` オプションを使用しているのを見かけることがあります。このオプションは `git branch` コマンドの `--set-upstream-to` オプションと同義で、現在のブランチをリモートブランチに関連付けるために使用されます。これにより、引数なしで `git pull` コマンドを使用できるようになります。リモート設定後、一度だけ次のコマンドを使用してください：

```bash
$ git push -u origin main
```

::::::::::::::::::::::::::::::::::::::::::::::::::

リモートリポジトリの変更をローカルリポジトリにプルすることもできます：

```bash
$ git pull origin main
```

```output
From https://github.com/vlad/planets
 * branch            main     -> FETCH_HEAD
Already up-to-date.
```

この場合、両方のリポジトリが既に同期されているため、プルしても影響はありません。しかし、他の誰かがGitHubのリポジトリに変更をプッシュしていた場合、このコマンドはその変更をローカルリポジトリにダウンロードします。

:::::::::::::::::::::::::::::::::::::::  challenge

## GitHub GUI

GitHub上の `planets` リポジトリをブラウズしてください。
「Code」ボタンの下で「XX commits」（XXは数値）というテキストを見つけてクリックしてください。
各コミットの右側にある3つのボタンにカーソルを合わせたりクリックしてください。
これらのボタンからどのような情報を収集/探索できますか？
シェルで同じ情報を取得するにはどうすればよいですか？

:::::::::::::::  solution

## 解答

最も左のボタン（クリップボードの画像）は、コミットの完全な識別子をクリップボードにコピーします。
シェルでは、`git log` を使用すると各コミットの完全な識別子を確認できます。

中央のボタンをクリックすると、その特定のコミットで行われたすべての変更が表示されます。緑色のラインは追加を、赤色のラインは削除を示します。
シェルでは、`git diff` コマンドを使用して同じ情報を確認できます。特に、`git diff ID1..ID2`（例：`git diff a3bf1e5..041e637`）を使用すると、2つのコミット間の差分を表示できます。

最も右のボタンは、そのコミット時点でのリポジトリ内のすべてのファイルを表示します。
シェルで同じ操作を行うには、その特定の時点でリポジトリをチェックアウトする必要があります。`git checkout ID`（IDは見たいコミットの識別子）を使用します。その後、リポジトリを元の状態に戻すことを忘れないようにしてください！

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## GitHubブラウザでの直接アップロード

GitHubでは、コマンドラインをスキップしてブラウザから直接リポジトリにファイルをアップロードすることもできます。2つの方法があります。
1つ目は、ファイルツリーの上部ツールバーにある「Upload files」ボタンをクリックすることです。2つ目は、デスクトップからファイルツリーにファイルをドラッグ＆ドロップすることです。詳細は[GitHubのこのページ](https://help.github.com/articles/adding-a-file-to-a-repository/)で確認できます。

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## GitHubのタイムスタンプ

GitHubでリモートリポジトリを作成します。ローカルリポジトリの内容をリモートにプッシュします。ローカルリポジトリを変更して、その変更をプッシュします。作成したGitHubリポジトリに移動して、ファイルの[タイムスタンプ](../learners/reference.md#timestamp)を確認してください。GitHubはどのように時刻を記録しており、その理由は何ですか？

:::::::::::::::  solution

## 解答

GitHubはタイムスタンプを人間が読みやすい相対形式（例："22 hours ago" や "three weeks ago"）で表示します。ただし、タイムスタンプにカーソルを合わせると、ファイルの最後の変更が行われた正確な時刻を確認できます。

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## プッシュとコミットの違い

このエピソードでは「git push」コマンドを紹介しました。
「git push」は「git commit」とどのように異なりますか？

:::::::::::::::  solution

## 解答

プッシュではリモートリポジトリに変更を送信します。これにより、リモートリポジトリを更新し、しばしば他の人と変更を共有します。
コミットはローカルリポジトリのみを更新します。

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## GitHubのライセンスとREADMEファイル

このエピソードではGitHub上でリモートリポジトリを作成する方法を学びましたが、GitHubリポジトリを初期化する際にREADME.mdやライセンスファイルを追加しませんでした。もし追加していた場合、ローカルリポジトリ

とリモートリポジトリをリンクしようとした際に何が起こったでしょうか？

:::::::::::::::  solution

## 解答

この場合、無関係な履歴のためにマージコンフリクトが発生します。GitHubがREADME.mdファイルを作成すると、リモートリポジトリでコミットが行われます。リモートリポジトリをローカルリポジトリにプルしようとすると、Gitは共通の起源を持たない履歴を検出し、マージを拒否します。

```bash
$ git pull origin main
```

```output
warning: no common commits
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/vlad/planets
 * branch            main     -> FETCH_HEAD
 * [new branch]      main     -> origin/main
fatal: refusing to merge unrelated histories
```

`--allow-unrelated-histories` オプションを使用して、2つのリポジトリを強制的にマージすることができます。このオプションを使用する際は注意が必要で、マージする前にローカルリポジトリとリモートリポジトリの内容を慎重に確認してください。

```bash
$ git pull --allow-unrelated-histories origin main
```

```output
From https://github.com/vlad/planets
 * branch            main     -> FETCH_HEAD
Merge made by the 'recursive' strategy.
README.md | 1 +
1 file changed, 1 insertion(+)
create mode 100644 README.md
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- ローカルGitリポジトリは1つ以上のリモートリポジトリに接続できます。
- リモートリポジトリへの接続にはSSHプロトコルを使用します。
- `git push` はローカルリポジトリからリモートリポジトリに変更をコピーします。
- `git pull` はリモートリポジトリからローカルリポジトリに変更をコピーします。

::::::::::::::::::::::::::::::::::::::::::::::::::
