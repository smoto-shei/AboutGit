# git の使い方についてのディレクトリ

# リモートリポジトリの作成 ~ 登録

1. 任意のディレクトリを作成し git init する
   1. git init すると .git が作成される
   2. .git 内の config を確認するとリモートリポジトリの場所等が確認できる
2. readme.md 書く
3. git add .
4. git commit -m 'xxx'
5. github GUI にてリモートリポジトリ作成
6. リモートリポジトリが登録されているか念のため確認（git remote -v)
   1. git remote add origin url （登録）
   2. git remote set-url origin {new url} (変更)

## .gitignore の作成

- .gitignore に記述されたファイルは git 　のトラッキング対象外(staging に追加されない)になる
  [追加の仕方](https://qiita.com/anqooqie/items/110957797b3d5280c)
- gibo を使用すると簡単に .gitignore を作成できるのでおすすめ
  [gibo](https://qiita.com/tmknom/items/c4bcebe17d25381fa45d)
  例）gibo dump MacOS python >> .gitignore

# git とは

- 分散型バージョン管理システム
  - 分散型:自分のマシンにリポジトリ（開発過程が保存されるデータベースを持っている）→ ローカルリポジトリ
  - バージョン管理システム：開発過程を記録しながら開発を行うためのシステム
  - (えらい参考になる)[https://qiita.com/satoshi1335/items/ead109412430a078feaa]

##【用語】

- ローカルリポジトリ：自分のコンピュータ内にあるリポジトリ
- リモートリポジトリ：自分のコンピュータ外にある（複数人で共有する）リポジトリ
- ステージングエリア：ローカルリポジトリに登録するファイルやディレクトリのリスト
- ワークツリー：バージョン管理対象の（開発過程を記録する）ファイルやディレクトリ
- ステージング：ワークツリーの変更を加えたファイルをステージングエリアに追加すること (add ＜ー＞ reset)
- コミット：ステージングエリアのファイルをローカルリポジトリに登録すること (commit)
- プッシュ：ローカルリポジトリに登録された情報をリモートリポジトリに追加すること(push)

# git でのファイル更新過程

## やりたいことをざっと把握

- 複数人で作業をする場合、各々が好き勝手ファイルを編集すると訳のわからないことになる。
  → リモートリポジトリで開発過程を共有する

- リモートリポジトリの更新は各々が持っているローカルリポジトリの情報を追加することで行う

# git コマンド

## git status

直前の commit (HEAD) の状態との差分を表す

- Changes to be commited

  - git add されているが commit されていない

- Changes not staged for commit:

  - 変更されているがまだ add されていない（ステージング環境にない）

- Untracked files
  - Git 管理外（ワークツリーに新規作成されローカルリポジトリにない）、かつ .gitignore でも除外されていない

### git status -s でさらに簡略的にみることができる

- M\_ : add されてるけど commit されてない
- \_M : 編集・変更・削除されているけどまだ add されていない
- ?? : git 管理されていない（新規作成されローカルリポジトリにない）かつ .gitignore でも除外されていない

## git diff

ワークツリーで行った変更をみる

# github actions

[google document](https://docs.google.com/document/d/1p5Cq1_FvGitcaJIi8upoHPnAC8ejsElwwU9RjhrTRH4/edit?ts=5ee1980a#)
