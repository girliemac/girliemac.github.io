---
title: 'HTML5 File API &#038; XHR2 with Node.js Express'
author: Tomomi Imura
layout: post
permalink: /blog/2012/11/04/html5-file-api-xhr2-with-node-js-express/
topsy_short_url:
  - http://is.gd/vIAalt
categories:
  - Event
  - HTML5
  - Japanese
  - Node.js
---
*Note: This article is written in Japanese for <a href="http://atnd.org/events/33022" target="_blank">東京Node学園祭2012</a>. I may or may not re-post this in English later only when I feel like to.  
KTHXBAI*

![file upload demo screenshot][1]

こんにちは、そして（たぶん）はじめまして。GirlieMac! Blog 初の日本語の記事を「東京Node学園祭」のために書かせてもらう事になりました。私はサンフランシスコ在住なので残念ながら学園祭参加はできないのですが、ブログの参加で遠く離れたこの地で応援されていただきます。

先に説明しておきますが、私はフロントエンド、しかもモバイルの UX ディベロッパーなので Node.js の記事というとちょっと畑違いかもしれませんが、フロントエンド目線で HTML5 File API と XHR2 そして Node を一緒に使ってみた画像ファイルアップロードのチュートリアルを書いてみます。

ここで使われた HTML5 フィーチュアはまだブラウザによってはサポートされていません。したがってコンパティビリティについては <a href="http://caniuse.com/fileapi" target="_blank">Can I use File API?</a> と、<a href="http://caniuse.com/xhr2" target="_blank">Can I use XHR2?</a> でチェックしてみてください。

それでは、HTML5 File API を使って画像のローカルファイルを読み込んでみましょう。

まず、HTML マークアップ側で、フォームを作成します。  
`<input type="file">` エレメントを使います。ここでは、`accept` 属性を `image/*` と指定して画像ファイルのみを扱ってみましょう。

```html
<form id="uploadForm" enctype="multipart/form-data" method="post" action="/upload">
  <input type="file" accept="image/*" name="imagefile" id="imagefile">
  <input type="button" value="Upload" id="upoadButton">
</form>

<img id="preview">
```

JavaScript 側です。ユーザが画像を選択した際に `File` オブジェクトのリストを返します。

```javascript
document.getElementById('imagefile').addEventListener('change', function() {
  fileSelected();
}, false);
```

`FileReader` オブジェクトをインスタンスとして読み取ります。  
さてここで、`readAsDataURL()` を呼び、 `DataURL` を使ってアップロード前に画像プレビューを表示してみましょう。

```javascript
function fileSelected() {
  var localFile = document.getElementById('imagefile').files[0];
  var imgFmt = /^(image\/bmp|image\/gif|image\/jpeg|image\/png|image\/tiff)$/i;
  if (!imgFmt.test(localFile.type)) { 
    ...  // 画像ファイルではありません、というエラーメッセージなど
  }

  var preview = document.getElementById('preview');
  // 画像ファイルを data URL として読み取ります
  var reader = new FileReader();
  reader.readAsDataURL(localFile);
  reader.onload = function(e){
　　// e.target.result は DataURL を含みます
    preview.src = e.target.result;
  }
}
```

XMLHttpRequest オブジェクトを作ります。次のイベント（progress, load, error, abort）のイベントリスナーを登録し、XMLHttpRequest Level 2 でサポートされ始めた FormData を使ってデータを send() メソッドで POST します。

```javascript
document.getElementById('upoadButton').addEventListener('click', function() {
  startUpload();   
}, false);

function startUpload() {
  var formData = new FormData(document.getElementById('uploadForm'));
  var xhr = new XMLHttpRequest(); 

  xhr.upload.addEventListener('progress', uploadProgress, false);
  xhr.addEventListener('load', uploadFinish, false); 
  xhr.addEventListener('error', uploadError, false);
  xhr.addEventListener('abort', uploadAbort, false);
  xhr.open('POST', '/upload');
  xhr.send(formData);   
}

function uploadProgress() { ... }
```

さて、ここでやっと、Node.js の登場です。 Express を使ってファイルを指定先にアップロードしましょう。  
アップロードされたファイルの情報は req.files に含まれています。例えばファイルサイズ (byte) の情報は size プロパティ、ファイル名は name プロパティ、といった感じです。

app.js Server-side:

```javascript
/* Server configuration */
app.configure(function(){
  app.use(express.methodOverride());
  app.use(express.bodyParser({keepExtensions: true})); 
  app.use(express.static(__dirname + '/public'));
});
```

```javascript
var fs = require('fs'); 
app.post('/upload', function(req, res) {
  // 仮のファイル置き場
  var tmp_path = req.files.imagefile.path;
  // 実際のファイル置き場
  var target_path = './public/user/' + req.files.imagefile.name;
  // ファイルを仮の場所から移します
  fs.rename(tmp_path, target_path, function(err) {
    if (err) throw err;
    // 仮ファイルを削除します
    fs.unlink(tmp_path, function() {
    if (err) throw err;
      res.send('File uploaded to: ' + target_path + ' - ' + req.files.imagefile.size + ' bytes');
        });
    });
});
```

と、こんな感じです。かなりはしょりましたが大まかな流れがわかっていただけたでしょうか。

久々の日本語のブログでちょっと手こずってしまいましたが、楽しんでいただけたら幸いです。コードや説明に間違いを見つけたり感想があった場合は遠慮なくコメントください。コメントはスパム防止のために承認制にしてあるのですが時差もあるのでちょっと遅れるかもしれません。 

## References

*   W3C: <a href="http://www.w3.org/TR/FileAPI/" target="_blank">File API</a>
*   W3C: <a href="http://www.w3.org/TR/XMLHttpRequest/#interface-formdata" target="_blank">XMLHttpRequest Level 2 &#8211; FormData インターフェイス</a>
*   Node.js: <a href="http://expressjs.com/" target="_blank">Express</a>
*   Article: <a href="http://www.hacksparrow.com/handle-file-uploads-in-express-node-js.html" target="_blank">Handle File Uploads in Express</a>

 [1]: /assets/images/wp-content/uploads/2012/11/Screen-Shot-2012-11-04-at-12.33.35-AM.png "screenshot"