novel-builder
=============

篠宮樹里「絵子よ、Web小説の執筆を補助するツールをNode.jsで作ってみたぞ」  
瀬尾絵子「何でもJavaScriptでやりたいんだねー……」

## Description

このツールは、Node.jsプロジェクトとして作成された小説に、下記の機能を追加します。

* 小説の原稿をePubや各種小説投稿サイト向けの原稿に変換する機能

## Usage

樹里「ではさっそく、このツールの使い方……というか、Node.jsプロジェクトとして小説を執筆する方法について解説していこう」  
絵子「お願いします」  

### 準備

#### Node.jsをインストールする

樹里「まず最初にやるべき事は、[Node.js](https://nodejs.org/ja/)のインストールだ」  
絵子「そりゃ、これがないと動かないからねー」  

#### Node.jsプロジェクトを作成する

樹里「次に、Node.jsプロジェクトを作成しよう」  
絵子「お、難しそうだね」  
樹里「そんな事はない。ディレクトリをひとつ作るだけだ」  
絵子「それだけ？」  
樹里「ああ。その代わり、ディレクトリ名は半角英数字、ハイフン、アンダーバーのみを使用したほうがいい」  
絵子「日本語は使わないほうがいいのね」  
樹里「ちなみに、私達の活躍を書いたWeb小説『[恋に落ちるコード.js](https://github.com/8novels/jk-meets-js)』の
プロジェクト名は`jk-meets-js`だ」  
絵子「あ、そんな名前だったんだ」  

#### package.jsonを作成する

樹里「続いて、これがNode.jsプロジェクトであることを宣言するファイル、`package.json`を作成しよう」  
絵子「ここをNode.jsプロジェクトとする！」  
樹里「ちゃんと専用のコマンドが用意されている。ターミナルで作成したディレクトリに移動し、次のコマンドを入力しよう」  

```
npm init
```

絵子「英文が表示されたね」  
樹里「必要なプロパティを対話形式で入力していくのだが、とりあえずエンターキーを押していけば完了する」  
絵子「それでいいの？」  
樹里「もちろん、それぞれの意味は理解しておいたほうがいい。特にライセンスの部分などはな。だが、最初はそれでいいだろう」  
絵子「はーい」  

#### ツールをインストールする

樹里「さて、プロジェクトが作成できたところで、いよいよ主役の登場だ」  
絵子「いよっ、待ってました！」  
樹里「本ツール『novel-builder』をインストールするためのコマンドがこれだ」  

```
npm install novel-builder --save
```

樹里「ちなみに`--save`オプションをつけることで`package.json`に必要な情報を追記してくれる」  
絵子「なるほど」  

#### package.jsonを編集する

樹里「では、出来上がった`package.json`を開いてみよう」  
絵子「おーぷん！」  
樹里「先程`npm init`で指定した各種設定がJSON形式で記述されている」  
絵子「ほんとだ。`name`とか`version`とか書いてあるね」  
樹里「ちなみにインストールしたnovel-builderの情報は`dependencies`に書かれている」  
絵子「おー、あるある」  
樹里「この`package.json`の任意の場所に、下記の情報を手動で追加する必要がある」  

```
  "config": {
    "epub_title": "恋に落ちるコード.js",
    "epub_author": "足羽川永都",
    "epub_publisher": "8novels",
    "epub_lang": "ja",
    "epub_tocTitle": "目次",
    "epub_appendChapterTitles": false
  },
  "scripts": {
    "novel-build": "novel-build",
    "novel-build-epub": "novel-build-epub",
    "novel-build-narou": "novel-build-narou",
    "novel-build-note": "novel-build-note",
    "novel-build-novelabo": "novel-build-novelabo"
  },
```

樹里「`config`の部分は、EPUBを出力する際に必要な設定だ。題名や著者名などを指定している」  
絵子「はーい」  
樹里「`scripts`の部分は、コマンド名と実行されるコマンドとを対比したものだ。あとで詳しく説明する」  
絵子「はーい」  

#### 必要なツールを追加インストールする

樹里「さて、準備の仕上げとして、次のコマンドで必要なツールを追加インストールしよう」  

```
npm install
```

樹里「`node_modules`ディレクトリ内に、動作に必要なパッケージ群が追加インストールされる」  
絵子「ほんとだ。サブディレクトリがたくさんできてる」  
樹里「これで環境は整った。次は……」

### 原稿を書く

絵子「ま、これが一番大事だよね。当たり前だけど」  
樹里「そうなんだが、いくつかルールがある」  

* すべての原稿は、`episodes`ディレクトリ内に保存する。
* 原稿は、Markdown形式で記述し、「001.md」「002.md」…のように連番となるよう保存する。
* ルビの記法は[青空文庫注記形式](https://www.aozora.gr.jp/aozora-manual/index-input.html#markup)とする。

樹里「それから、EPUBの表紙に使用する画像を用意する必要がある」  
絵子「そっか、表紙も大事だもんね」  
樹里「プロジェクトディレクトリの直下に`cover.jpeg`という名前で保存すること。もちろん、EPUBを作成しない場合は不要だ」  

### ファイル変換機能(build)を使用する

樹里「さて、原稿は書けたか？」  
絵子「書けたよー。いやー、苦労した」  
樹里「では、さっそくツールを起動してみよう」  

```
npm run novel-build
```

樹里「コマンドを入力すると、`dist`ディレクトリが作成され、変換された原稿が出力される」  
絵子「おー、すごい」  
樹里「この`novel-build`の部分が、先程`package.json`の`scripts`の記述と対応している。つまり……」

```
"b": "novel-build"
```

樹里「……と書けば、`npm run b`と入力するだけで`novel-build`コマンドが実行されるわけだ」  
絵子「ほほう」  
樹里「では、実際に何が出力されるのか説明しよう」

#### コマンドの説明

##### novel-build

下記全てのファイルを一度に出力します。

##### novel-build-epub

`dist`ディレクトリに、EPUBファイルを出力します。  
`package.json`の`config`の記述、および`cover.jpeg`ファイルが存在しないとエラーになります。

##### novel-build-narou

`dist/narou`ディレクトリに、小説家になろう向けの原稿をプレーンテキストで出力します。  
カクヨム・エブリスタにも対応しています。

* ルビ記法はそのまま出力します。

##### novel-build-note

`dist/note`ディレクトリに、note向けの原稿をプレーンテキストで出力します。  

* ルビ記法を括弧書きに変換します。

##### novel-build-novelabo

`dist/novelabo`ディレクトリに、ノベラボ向けの原稿をプレーンテキストで出力します。  

* 縦書き表示で見栄えがいいように、英数字を全角に変換します。
* ルビ記法はそのまま出力します。


樹里「以上で説明は終了だ。さっそく小説を公開してみよう」  
絵子「よーし、やるぞー！」  

## Requirement

このツールは、下記のライブラリを使用しています。

* [epub-gen](https://www.npmjs.com/package/epub-gen)
* [fs-extra](https://www.npmjs.com/package/fs-extra)
* [markdown-it](https://www.npmjs.com/package/markdown-it)

## Todo

- [ ] 対応する形式を増やす(ハーメルン、アルファポリス、etc)
- [ ] EPUB変換時に全角スペースが消失する問題の対応
- [ ] 自動フォーマット機能(全角インデント挿入等)の実装
- [ ] 画像出力機能の実装
- [ ] READMEに「`package.json`に記述するライセンス表記について」を追記
- [ ] READMEに「.gitignoreの書き方」を追記
- [ ] READMEにmarkdown-itのオプション指定方法を追記

## Author

[8amjp](https://github.com/8amjp)
