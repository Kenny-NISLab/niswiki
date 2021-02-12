# NISLAB Wiki

ネットワーク情報システム研究室（NISLAB Wiki）  
Network Information Systems Lab Wiki

> NISLAB Wiki は [こちら](https://wiki.nislab.io/)  
> <https://wiki.nislab.io/>

## 目次

1. [NISLAB Wiki の編集手順](#nislab-wiki-%E3%81%AE%E7%B7%A8%E9%9B%86%E6%89%8B%E9%A0%86)
   1. [環境構築](#%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89)
   2. [プロジェクトのクローン](#%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E3%82%AF%E3%83%AD%E3%83%BC%E3%83%B3)
   3. [ページの追加・編集](#%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%AE%E8%BF%BD%E5%8A%A0%E7%B7%A8%E9%9B%86)
   4. [編集完了後の公開手順](#%E7%B7%A8%E9%9B%86%E5%AE%8C%E4%BA%86%E5%BE%8C%E3%81%AE%E5%85%AC%E9%96%8B%E6%89%8B%E9%A0%86)
2. [仕組み](#%E4%BB%95%E7%B5%84%E3%81%BF)

## NISLAB Wiki の編集手順

基本的に Mac で編集することを前提として記載しています。  
Windows を使用している人は、適宜調べながら作業を行ってください。

### 環境構築

Terminal から下記のコマンドを叩いて、必要なパッケージがインストールされているか確認してください。  
バージョンが表示されればインストールされているので問題ありません。

> 下記の 3 つがインストールされていない人は、MacOS 用のパッケージ管理システムである Homebrew を用いてインストール等を行ってください。

```zsh
# Homebrew の確認
brew -v

# git の確認
git --version

# Node Package Manager の確認
npm -v
```

特段の理由がない場合、これらをアップデートすることを推奨していますので、下記のコマンドからパッケージのアップデートを行ってください。

> 下記のコマンドの実行には数分かかることがありますので、安定した回線で実行してください

```zsh
# Homebrew のアップデート
brew update

# Homebrew + パッケージ のアップデート
brew upgrade
```

### プロジェクトのクローン

GitHub で管理されているプロジェクトをクローン（コピー）して、適宜編集を行います。  
必要なパッケージのインストールも行います。

```zsh
# デスクトップへディレクトリを移動
cd
cd Desktop/

# プロジェクトをクローン
# git clone GITHUB_REPOSITORY
git clone https://github.com/kogepanh/niswiki/

# プロジェクトのディレクトリに移動
cd niswiki

# パッケージのインストール
npm install
```

### ページの追加・編集

できれば、GitHub Issue を用いて管理すべきですが、必須ではありませんので、興味のある人のみ適宜調べて作業してください。  
基本的には、各自でブランチを切ってもらい、作業をおこない、GitHub 上でマージしてもらう形になるかと思います。

```zsh
# 最新のリモートリポジトリを取得
git pull origin main

# 自分の作業用のブランチを切る
git checkout -b ブランチ名
```

ページを編集するには、プロジェクトの `docs/` 以下を編集します。  
`docs/` より下層のフォルダに作成した `README.md` が、自動的にメニューとしてサイドバーに追加されます。また、トップページとなる `docs/README.md` に目次の欄がありますが、公開時に自動的に追記される箇所ですので、記述は不要です。  
記事は `Markdown` で記述します。 記法については、 [Qiita の記事](https://qiita.com/tbpgr/items/989c6badefff69377da7) などを参考にしてください。  
編集した NISLAB Wiki については、下記コマンドを実行することで、ローカルホストで実行することができます。

```zsh
# ローカルホストで実行
npm start

# 下記アドレスを Chrome 等に貼り付けて表示確認できます
http://localhost:3000

# 実行を止めたい場合は
Control + C
```

### 編集完了後の公開手順

編集が完了したら、記事を公開するために下記コマンドを実行してください。

```zsh
# フォーマットを実行
npm run format

# 全てのファイルをインデックスに追加
git add .

# インデックスに追加したファイルをコミット
git commit -m "何を変更したのかコメントとしてここに記述"

# リモートリポジトリにアップロード
git push origin "作業開始時に指定したブランチ名"
```

GitHub 上で Pull Request する必要があります。  
先ほどアップロードしたブランチが GitHub 上に反映されていると思いますので、メインブランチへのプルリクエストを作成して、マージを行ってください。  
マージが完了すると、自動的にサイドバーが作成され、 <https://wiki.nislab.io/> に反映されます。（GitHub Actions が完了するまで、少々時間がかかります。）

## 仕組み

[この Wiki](https://wiki.nislab.io/) は、 [docsify](https://docsify.js.org/#/) を用いて開発されています。

> Docsify は、ドキュメント作成向けの SSG です。
> 超シンプルで HTML すらジェネレートせずに、 Markdown ファイル読み込んで Web サイトに表示します。

NISLAB Wiki は、git で管理されており、メインブランチへのマージをトリガーとして自動的にデプロイされます。
