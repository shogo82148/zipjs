# zip.jsとは
- JavaScriptでZIPデータを解凍するライブラリ

# ファイル一覧
- **zip.js**
  - 本体
- **sjis.js**
  - SJIS -> UTF-8 変換ライブラリ  
- **jsinflate.js**
  - GZIPデータの解凍ライブラリ [js-inflate](https://github.com/augustl/js-inflate/blob/master/js-inflate.js)  
    そのうち自分でも書くかもしれない
- **zip.min.js**
  - 上ファイルの統合/パッキング版

# 使い方

    // 予め zip.js, sjis.js, jsinflate.js か zip.min.js をロードしておく。

    Zip.inflate_file("example.zip", function (zip) {
      console.log(zip.files["test.txt"]);   // console.logすると大体の構成がわかる (説明が面倒なだけ)

      var image = zip.files["foo/bar.png"]; // ネストしたディレクトリ内のファイル
      console.log(image.modified());        // ファイル作成日時
      console.log(image.data);              // 圧縮済みデータ(バイト列)
      console.log(image.inflate());         // 展開されたデータ

      $("#image")                           // base64にエンコードしてdataスキームの形にすれば画像も表示可能
        .attr("src", "data:image/png;base64," + window.atob(image.inflate()));
    });

    // バイト列から解凍したい場合

    var zip = Zip.inflate([...]);
    console.log(zip.files["test.txt"].size);     // 圧縮後サイズ
    console.log(zip.files["test.txt"].fintSize); // 圧縮前サイズ

# まあ
- console.logしましょう。
