# Gitコマンドまとめ

## 基本的なコマンド

- add：ワークツリーからステージに上げる
- commit: ステージからリポジトリに上げる

### `git diff --staged`
`git status`で変更されたものの差分が見れる

### `git log`
変更履歴を表示
- `git log -p <ファイル名>`　変更差分を表示
- `git log -n <コミット数>`　表示するコミット数を指定

### `git rm <ファイル名>　/ git rm -r <ディレクトリ名>`
そもそもファイルやディレクトリがいらない場合にファイルごと削除

- `git rm --cached <ファイル名>` ステージングされたファイルのみ削除（ワークツリーには残しておきたい場合）

### `git mv <旧ファイル名> <新ファイル名>`
ファイルの移動や名前の変更をGitのコミット履歴に記録する

以下のコマンドと同じこと
```bash
mv <旧> <新>
git rm <旧>
git add <新>
```

## 変更を元に戻す
### `git restore <ファイル名>`
ワーキングディレクトリの変更をaddする前に戻す

### `git restore --staged`
addされた変更を取り消す

※`git reset HEAD`と似ているけど、こちらでよい

### `git commit --amend`
コミットのやり直しができる

**ただし、pushする前のみ！！**

## Githubとのやりとり
### `git fetch <リモート名(originなど)>`
リモートの情報をローカルリポジトリに反映

### `git merge <リモート名(originなど)> <ブランチ名(mainなど)>`
ローカルリポジトリの内容をワークツリーに反映

### `git pull ( <リモート名>　<ブランチ名>　)`
`git fetch`と`git merge`を同時に実行してくれる

> [!WARNING]
> `git pull`をすると今いるブランチに自動でマージされてしまう

> 例) mainブランチで`git pull origin hoge`するとmainにhogeがマージされてしまう！

### `git remote rename <旧リポジトリ名>　<新リポジトリ名>`
リモートリポジトリの名前を変更する

### `git remote rm <リポジトリ名>`
リモートリポジトリを削除する


## ブランチとマージ
### `git branch`
ブランチの一覧を表示

- `git branch <ブランチ名>`　ブランチを作る

### `git switch <ブランチ名>`
そのブランチに移動する

### `git branch -m <新ブランチ名>`
今いるブランチの名前を<新ブランチ名>に変える

### `git branch -d <ブランチ名>`
ブランチを削除する

**mainにマージされていないものは削除されない！！**

### `git branch -D <ブランチ名>`
mainへのマージに関わらず、強制的にブランチを削除する

### コンフリクトを起こりにくくするポイント
- 複数人で同じブランチを触らない
- pullやmergeをする前に変更中のブランチをcommitやstashする
- pullはブランチを移動して実行する
- もし、コンフリクトしても慌てない！落ち着いてコンフリクトを解消する

### ブランチについて
https://backlog.com/ja/git-tutorial/stepup/01/


## リベース
リベースすると履歴を整えながら、他のブランチを取り込みできる
**pushしたものをrebaseするのは絶対NG**
### リベースとマージ
#### リベース
- メリット：履歴が綺麗に残る
- デメリット：コンフリクトの解消が少し難しい

#### マージ
- メリット：コンフリクトの解消がしやすい
- デメリット：コミットがたくさんできてしまう

#### 結論
- pushする前ならリベースで整え、pushした後ならマージを使う
- コンフリクトしそうならマージを使う

### pullについて
- `git pull origin main`はmerge型なので、pullの履歴が残る
- `git pull --rebase origin main`は、rebase型なのでpullの履歴が残らない
- もし、Githubの中身をとって期待だけなら`--rebase`してあげると履歴が綺麗

### `git rebase -i <コミットID>`
複数のコミットのやり直し

### rebaseの使い方
https://backlog.com/ja/git-tutorial/stepup/32/

## stashについて
### `git stash`
commitできないけど、ブランチを切り替えたい場合に一時避難させる

- `git stash list`　避難している作業の一覧を確認
- `git stash apply` 最新の作業を復元する
- `git stash apply --index` ステージの状況も復元する
- `git stash apply <スタッシュ名>` 特定のスタッシュを復元
- `git drop stash` スタッシュの削除

### stashの使い方
https://backlog.com/ja/git-tutorial/reference/stash/#section1



