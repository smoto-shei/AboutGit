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

# git
## git status
直前の commit (HEAD) の状態との差分を表す
- Changes to be commited
    - git add されているが commit されていない

- Changes not staged for commit:
    - 変更されているがまだ add されていない（ステージング環境にない）

- Untracked files
    - Git管理外（ワークツリーに新規作成されローカルリポジトリにない）、かつ .gitignore でも除外されていない

### git status -s でさらに簡略的にみることができる
- M_ : add されてるけど commit されてない
- _M : 編集・変更・削除されているけどまだ add されていない
- ?? : git 管理されていない（新規作成されローカルリポジトリにない）かつ .gitignore でも除外されていない



# github actions

[google document](https://docs.google.com/document/d/1p5Cq1_FvGitcaJIi8upoHPnAC8ejsElwwU9RjhrTRH4/edit?ts=5ee1980a#)
