grunt-fontmin-ex
===
HTMLから自動でサブセット文字列を抽出し、フォントをサブセットします。

このREADMEは概ね元の英語のファイルから翻訳した文書です。はっきり言っておかしな日本語だと思いますが、ご了承ください。

## tamainaによる変更

* CSS出力はなくなりました
  * `@font-face`はCSSに自分で書いてください。
* **woff2**出力に対応しました。
  * **ttf2woff2**を利用します。
  * ビルドのために**node-gyp**が必要です。
* 日本語のREADME(これ)を追加しました。
  * 英語が苦手なので。

## 対応フォントタイプ

### 入力

ttf, ttc, otf, woff, woff2

### 出力

ttf, woff, woff2

## 使い方

1.  ~~~
    npm install grunt-fontmin-ex --save-dev
    ~~~
2. Gruntfile.jsに設定します

###  設定
```JavaScript
grunt.initConfig({
  fontmin: {
    options: {
      dest:    'www-bin/fonts/',  // デフォルトは './'
      basedir: 'fonts/'           // デフォルトは './'
      types:   ['ttf','woff','woff2'] // デフォルト
    },
    'Source-hans*.otf': {
      /* getText: (html) => string_of_characters_to_include; サブセット文字列
       * 設定しなければ、html2textで処理します
       */
      getText: getBody,
      src:  'www-bin/**/*.html'
    },
    'cn-cursive.ttf': {
      getText: getHeadings,
      src:  'www-bin/**/*.html'
    }
  }
})

grunt.loadNpmTasks('grunt-fontmin')
```

### オプション (全てのタスク)
* dest:
  * フォントファイルを出力するディレクトリを指定します。末尾に/が必要です。
  * デフォルト: `./`
* basedir:
  * フォントファイルを入力するディレクトリを指定します。末尾に/が必要です。
  * デフォルト: `./`
* types:
  * ***`Array`***
  * 出力するフォントの種類です。
  * 'ttf', 'woff', 'woff2' のなかから選びます。

### ターゲットオプション
* Grantのターゲットの名前
  * 読み込むフォントファイルのパスを指定します。オプションで指定したbasedirからの相対的なパスを書きます。
  * 書かれたパスは[`grunt.file.expand()` →リファレンス](http://js.studio-kingdom.com/grunt/api/grunt_file#9)で読み込まれます。
* src:
  * フォントのサブセット文字列を確定するため、HTMLなどを読み込みます。
  * Gruntfileのファイル指定記法が利用できます。
  * ファイルはgetText関数で処理されます。
* getText:
  * filter ***`function`***
    * `(htmlContent)` => ***`string`***_of_chars_to_include;
  * フィルター関数です。
    * srcで指定したファイル群の内容が入力され、サブセット文字列を返す関数です。
  * 自分で記述できますが、何も記述がなければ`html2text`で処理します。

## 情報

* 入力と出力でファイルの名前を変える機能は用意されていません。
* **ライセンス上再頒布可能なフォントを利用してください。**  
  * [中国語のフリーフォントまとめサイト](http://zenozeng.github.io/Free-Chinese-Fonts/)から検討できます。
  * 私は過去に[汎用的なWebFontセット](https://tmin.xyz/The-Japanese-Web-Fonts/)を作成しました。
    * かなが特徴的なフォントは、すでにサブセットされています。
    * [コンセプトページ](https://tmin.xyz/The-Japanese-Web-Fonts/easy)的な何か

## ライセンス
MITライセンス (C) wacky6
MITライセンス (C) tamaina