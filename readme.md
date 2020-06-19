# git の使い方についてまとめるディレクトリ

# git とは

- 分散型バージョン管理システム

  - 分散型:自分のマシンにリポジトリ（開発過程が保存されるデータベースを持っている）→ ローカルリポジトリ
  - バージョン管理システム：開発過程を記録しながら開発を行うためのシステム

- git について理解があやふやな人へ
  - とりあえず'(えらい参考になる)[https://qiita.com/satoshi1335/items/ead109412430a078feaa]'の git 概念図について頭に叩き込む。そして以下の一連の git によるバージョン管理の流れをいったん理解する。
  ```
  1 リモートリポジトリが存在(作成)し、
  2 それをローカルに持ってきて（ローカルリポジトリ）、
  3 それを編集し、ステージングエリアにコンテンツを追加（'$ git add'）し、
  4 ステージングエリアのコンテンツをローカルリポジトリに登録('$ git commit -m 'commit_message')し、
  5 ローカルリポジトリに登録された情報をリモートリポジトリに追加('$ git push origin branch_name')
  ```

##【用語】

- ローカルリポジトリ：自分のコンピュータ内にあるリポジトリ
- リモートリポジトリ：自分のコンピュータ外にある（複数人で共有する）リポジトリ
- ステージングエリア：ローカルリポジトリに登録するファイルやディレクトリのリスト
- ワークツリー：バージョン管理対象の（開発過程を記録する）ファイルやディレクトリ
- ステージング：ワークツリーの変更を加えたファイルをステージングエリアに追加すること (add ＜ー＞ reset)
- コミット：ステージングエリアのファイルをローカルリポジトリに登録すること (commit)
- プッシュ：ローカルリポジトリに登録された情報をリモートリポジトリに追加すること(push)
- origin：リモートリポジトリの URL の別名。変数みたいなもの。
- origin/master：リモートリポジトリの master ブランチであることを意味する( origin を省略した master はローカルリポジトリの master ブランチを意味する)
- HEAD：ブランチの最新の commit 位置を指す
- HEAD^：ブランチの 1 つ前の commit 位置(HEAD~も同義)を指定する時に使う
- HEAD^^：ブランチの 2 つ前の commit 位置(HEAD^^, HEAD~2 も同義)を指定する時に使う

### \* 注意

- ここではファイル・ディレクトリ(\*.jpg とかの画像も)をひっくるめてコンテンツとする

# リモートリポジトリの作成 ~ 登録

## リモートリポジトリがないケース

1. 任意のディレクトリを作成し git init する
   1. git init すると .git が作成される
   2. .git 内の config を確認するとリモートリポジトリの場所等が確認できる
2. readme.md 書く
3. ステージングエリアにコンテンツを追加する
   - '\$ git add .'
4. ステージングエリアのコンテンツ
   - '\$ git commit -m 'xxx''
5. github GUI にてリモートリポジトリ作成
6. リモートリポジトリが登録されているか念のため確認（git remote -v)
   1. '\$ git remote add origin url' （登録）
   2. '\$ git remote set-url origin url' (変更)
7. .gitignore の作成

- .gitignore に記述されたファイルは git のトラッキング対象外(ステージングエリアに追加されない)になる
  [追加の仕方](https://qiita.com/anqooqie/items/110957797b3d5280c)
- gibo を使用すると簡単に .gitignore を作成できるのでおすすめ
  [gibo](https://qiita.com/tmknom/items/c4bcebe17d25381fa45d)
  例）gibo dump MacOS python >> .gitignore

8. リモートリポジトリを更新する

- '\$ git push origin リポジトリ名' でリモートリポジトリを更新する

<!-- コマンド一覧 -->

# git コマンド

<!-- git add 関連 -->

### git add [file_name]

[参考](https://eng-entrance.com/git-add)

- ワークツリーのコンテンツ(ファイル・ディレクトリ等)を見つけてインデックス(ステージングエリア)に追加(== git 管理の対象にいれる。コミットの対象となるのはステージングエリアに存在するコンテンツのみ。ステージングエリアに上げたくないコンテンツは .gitignore に追加する)

#### git reset file_name

- ステージングエリアに上げたファイルを取り消す

#### git status

- ステージングエリアにあるファイルを確認する(直前の commit (HEAD) の状態との差分を表す)

##### status 一覧

- Changes to be commited

  - git add されているが commit されていない

- Changes not staged for commit:

  - 変更されているがまだ add されていない（ステージング環境にない）

- Untracked files
  - Git 管理外（ワークツリーに新規作成されローカルリポジトリにない）、かつ .gitignore でも除外されていない

##### git status -s でさらに簡略的にみることができる

- M\_ : add されてるけど commit されてない
- \_M : 編集・変更・削除されているけどまだ add されていない
- ?? : git 管理されていない（新規作成されローカルリポジトリにない）かつ .gitignore でも除外されていない

<!-- git commit 関連 -->

### git commit -m 'コミットメッセージ'

- ステージングエリアにあるコンテンツをローカルリポジトリに登録する
- commit を取り消すには'\$ git reset'を使う
- commit を修正するには '\$ git commit --amend'を使う（上書きすることになる)

#### 修正早見

##### git reset option

- コミットを取り消す

###### git reset --soft

- コミットだけを取り消す(ローカルのワークツリーの内容は変更しない)

###### git reset --hard(多用厳禁)

- ローカルのワークツリーの内容も含めコミットを取り消す

<!-- git push -->

### git push origin branch_name

- ローカルリポジトリのブランチをリモートリポジトリへアップロードする
- rebase したあとは -f オプションをつける必要がある

### git clone

- リモートリポジトリをローカルに複製(ワークツリーを作成)

ワークツリーで行った変更をみる

<!-- git reset -->

### git reset

- HEAD の位置を変更するコマンド。オプションによってステージングエリア、ワークツリーの内容も変更する。
  - --option は何を(ローカルリポジトリの状態(==commit), ステージングの状態(== add), ワークツリーの状態)変更を指定する
    - soft：ローカルリポジトリ(HEAD)の位置を変更する
    - mixed(またはオプションなし)：ローカルリポジトリ, ステージングエリアの位置を変更する
    - hard：ローカルリポジトリ、ステージングエリア、ワークツリーの位置を全て変更する(例えば、'\$git reset --hard HEAD^' とした場合は 「ローカルリポジトリの HEAD^ == ステージングエリア(空) == ワークツリー」 となる。ワークツリーまでも変更されるので多用厳禁)

```
git reset <何を戻す?> <どこまで戻す?>
```

- reset 自体を reset で取り消すこともできる。ミスって --hard して消えた！！となっても落ち着いて reflog を見て reset で戻せる。

<!-- git fetch -->

### git fetch

- ローカルリポジトリをリモートリポジトリの最新で更新する。

<!-- git merge -->

### git merge branch_name

- 指定したブランチを現在のブランチに統合する
- fast-forward と non-fast-forward で処理の仕方が異なる
  - fast-forward：派生元ブランチ作成時と比較して何も更新されていない（commit がそのまま統合される）
  - non-fast-forward：派生元ブランチ作成時と比較して何も更新されている（マージコミットを積む）

<!-- git rebase -->

### git rebase branch_name[origin/master がよく使われるのかな]

- 履歴を更新する。派生ブランチの根元を最新のものに付け替える。例えば、master から branchA を作成した後で、branchB が master にマージされ master が進んだ際、branchA 上でも進んだ分のコミットを反映させる必要がある。rebase の際、コンフリクトのあるなしで対応が変わる。[参考](https://qiita.com/gold-kou/items/7f6a3b46e2781b0dd4a0)
  - コンフリクトある場合
    - コンフリクトを解消して'$ git add file_name' & '$ git rebase --continue' & '\$ git push origin branch_name -f'

<!-- git pull  -->

### git pull

- 最新のリモートリポジトリの内容をローカルリポジトリに反映する

<!-- git stash -->

### git stash

- commit していない(ローカルリポジトリに追加していない)コンテンツを一時的に避難する(ステージングエリアにあるものも stash される）。作業ブランチを間違えた時とかに、「stash して変更内容を避難し、正しいブランチに移動し、stash を戻す」みたいな動作をする。

<!-- cherry-pick -->

### git cherry-pick commit_id

- 他のブランチの特定のコミットを現在のブランチに取り込む。「間違えて別のブランチで作業してコミットまでしちゃった」とやらかした時に、本来のブランチにそのコミットを取り込むことができる。

<!-- git log -->

### git log

- コミット履歴を表示する。上に表示されるほど新しいコミット履歴。

<!-- git reflog -->

### git reflog

- HEAD の履歴一覧を表示する。checkout,reset とかして HEAD を変更した際などの履歴も全てみることができる。新しい履歴は上。

<!-- git diff -->

### git diff --option

- リモート、ローカル、ステージ、ワークツリーの各状態との差を見ることが出来る。
  - option なし：ワークツリーと ステージングエリアとの差分を見る
  - --staged(--cached)：ステージングエリアと最新のコミット(HEAD)の差分を見る
  - HEAD^：最新のコミットと最新一つ手前のコミットとの差分を見る

# github actions

[google document](https://docs.google.com/document/d/1p5Cq1_FvGitcaJIi8upoHPnAC8ejsElwwU9RjhrTRH4/edit?ts=5ee1980a#)

# git 全体の参考

[git の基礎](https://qiita.com/satoshi1335/items/ead109412430a078feaa)
[いまさらだけど Git を基本から分かりやすくまとめてみた](https://qiita.com/gold-kou/items/7f6a3b46e2781b0dd4a0)

## 個別

<!-- git reset -->

[git reset についてまとめる](https://murank.hatenadiary.org/entry/20110327/1301224770)
['git reset についてまとめる' を受けて誰かが書いたやつ](https://qiita.com/fnobi/items/ec036c1b5d7ee5a8517c)

<!-- git diff -->

[忘れやすい人のための git diff チートシート](https://qiita.com/shibukk/items/8c9362a5bd399b9c56be)

<!-- gitignore -->

[.gitignore の仕様詳解](https://qiita.com/anqooqie/items/110957797b3d5280c44f)
