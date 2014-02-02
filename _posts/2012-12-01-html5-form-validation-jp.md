---
title: HTML5 Form Validation のカスタマイズ
author: Tomomi Imura
layout: post
permalink: /blog/2012/12/01/html5-form-validation-jp/
topsy_short_url:
  - http://is.gd/rjtuZT
  - http://is.gd/rjtuZT
dsq_thread_id:
  - 2067761307
categories:
  - CSS
  - Firefox
  - HTML5
  - IE
  - Japanese
  - Mobile
  - Nokia
  - Opera
  - UI/UX
  - WebKit
---
*Note: This article is written in Japanese for <a href="http://www.adventar.org/calendars/27" target="_blank">HTML5 Advent Calendar 2012</a>. If you&#8217;d like to read this article in English, you can read the original post I wrote on [November 21]({% post_url 2012-11-21-html5-form-validation %}). (The article was originally written for: <a href="http://www.developer.nokia.com/Blogs/Code/2012/11/21/creating-a-custom-html5-form-validation/" target="_blank">Nokia Code Blog</a>). 
Thank you.*

* * *

師走です。早いものですね。さて、<a href="http://www.adventar.org/calendars/27" target="_blank">HTML5 Advent Calendar 2012</a> ２日目を書かせてもらうことになりました。元々この記事は <a href="http://www.developer.nokia.com/Blogs/Code/2012/11/21/creating-a-custom-html5-form-validation/" target="_blank">Nokia Code Blog</a> の一記事として私が１１月２１日に書いたものなのですが、クロスポスト可ということなので、せっかくですので今回はその日本語版として記事にしてみました。というわけで、HTML5 Form Validation CSS3、ウェブフォント、JavaScript を使ったカスタマイズ方法について書いています。

以前までならばユーザの入力フィールドの検証（バリデーション）は JavaScript もしくはサーバサイドで専用のロジックを書かねばばらなかったわけですが、HTML5 からは仕様に組み込まれるようになったために非常に簡単にできるようになりました。実装されるようになってかれこれ１年ほど経っているのですがその間に Internet Explorer など、サポートされるブラウザも増えてきました。まずこのバリデーションカスタム化についてのこの記事を読む前に、必須課目として HTML5 から新たに加わったフォームのインプット要素についての理解が必要ですので、基本を<a href="http://www.html5.jp/tag/elements/input.html" title="Form input 要素" target="_blank">ここ</a>や<a href="http://ascii.jp/elem/000/000/693/693899/" title="HTML5でこんなに変わったinput要素を徹底解説" target="_blank">ここ</a>などでおさらいをしておいてください。さらにバリデーションについての全般的な内容については、白石 俊平さんの書かれた、<a href="http://www.atmarkit.co.jp/fwcr/design/benkyo/html5appli09/01.html"　titile="HTML5で仕様になった入力値チェック＋便利な3Tips" target="_blank">「HTML5で仕様になった入力値チェック＋便利な3Tips」</a>が非常にわかりやすいと思います。

## フォームバリデーションの基本

例えば必須入力のフィールドが空の状態で送信された場合の検証。これは HTML5 では `<input>` に `required` 属性を加えるだけで、下のように非常に簡単に書くことができます。

```html 
<form> 
  <input type="text" required> 
  <input type="submit" value="Submit"> 
</form> 
```

単純な<a title="JS Fiddle" href="http://jsfiddle.net/girlie_mac/X6Uuc/" target="_blank">デモ</a>を書いたので試してみてください。仕様がサポートされているブラウザ上でフィールドを空のまま送信するとエラーメッセージが表示、もしくはエラーを示す UI が現れます。  
下のスクリーンショットは、左がデスクトップ IE10 （英語版）のデフォルト、右が IE10 モバイルの UI です。  

<img style="vertical-align: top" src="/assets/images/articles/2012/12/screenshot-basic-ie10.png" alt="Basic form validation (IE10)" width="255" height="125" /> <img style="vertical-align: top;margin: 9px 0 0 20px" src="/assets/images/articles/2012/12/screenshot-basic-ie10m.png" alt="Basic form validation (IE10 Mobile)" width="250" height="68" />  

IE10 モバイル版では、エラーメッセージの吹き出しが表示されず、空フィールドの枠が赤く表示されただけの仕様になっているのですが、そのフィールドが focus された状態でバーチャルキーボードが現れるので、ユーザビリティは損なわれていないようです。

このメッセージや吹き出しの UI は、ブラウザや環境言語によって異なります。下の画像は日本語版の Chrome から。  
<img src="/assets/images/articles/2012/12/screenshot-basic-chrome-jp.png" alt="Basic form validation (Chrome JP)" width="301" height="96" />

それでは、これから 1) パターンマッチング、2) CSS3 でのビジュアル効果、3) カスタムのエラーメッセージ設定、を使ってフルカスタマイズしてみましょう。

## パターンマッチング

`pattern` 属性では要素の値を正規表現と照合することができます。下は、6~12 文字のアルファベットと数字、句読点を含む文字セットを一致させる正規表現を使った例です。

```html 
<form> 
  <input id="username" type="text" pattern="[a-zA-Z0-9_-]{6,12}" autofocus required> 
  <input id="submit" type="submit" value="create"> 
</form> 
```

<a href="http://jsfiddle.net/girlie_mac/qe62z/" target="_blank"> <code>pattern</code> 属性のデモコード</a>を試してみてください。わざと無効になるように３桁の数字などを入力てみましょう。

## CSS3 ユーザインターフェイスセレクタ

CSS ではいくつかの、UI 要素状態を表す UI セレクタ（疑似クラスや疑似要素）があります。その例として、`:valid`, `invalid`, `in-range`, `out-of-range`, `required`, `optional`, `read-only`, `read-write` が挙げられます。  
これを使って、入力の有効/無効状態を赤と緑の色別に表示するようにしてみましょう。

```css 
:valid {
    color: green;
} 
:invalid {
    color: red;
} 
```

入力値が正しい形式に一致する時は緑、値が無効なときは入力値が赤で表示されます。<a href="http://jsfiddle.net/girlie_mac/Db7kg/" target="_blank">サンプル</a>で試してみましょう。

## ウェブフォントアイコンを使う

この上さらに、チェックマークのついたアイコンを表示させてみましょう。せっかくですので画像アイコンを使わず CSS3 をフル活用してウェブフォントを使った応用をやってみましょう。  
<img src="/assets/images/articles/2012/12/screenshot-valid-fonticon.png" alt="using webfont icon" width="269" height="73" />

ここでまた必須課目です！ここではちょっと変わった活用をしてみたいので、CSS3 ウェブフォントについてよくわからないという方は必ず先におさらいしておいてください。

さて、フリーのウェブフォントはいろいろあるのですが、ここでは <a href="http://icomoon.io/" target="_blank">IcoMoon</a> が配布している *Iconic* という絵フォントを使います。このサイトの、<a href="http://icomoon.io/app/" target="_blank">IcoMoon App</a> を使うとなんと自分の必要なものだけを選べ、それを軽量パッケージ化してくれるのです。

一旦フォントセットを作ったら、それを読み込む `@font-face` 規則を使って CSS を作成します。

```css
@font-face {
    font-family: 'iconic';
    src: url('webfonts/iconic.eot');
    src: url('webfonts/iconic.eot?#iefix') format('embedded-opentype'),
         url('webfonts/iconic.svg#iconic') format('svg'),
         url('webfonts/iconic.woff') format('woff'),
         url('webfonts/iconic.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
}
```

疑似クラス `:valid` と、疑似要素 `::after` (もしくは `::before`)を一緒に使うと入力値が無効であった時にエレメントの後ろ（または前に）コンテントを表示するとこができます。では後ろにフォントアイコンを表示させてみましょう。 

`input` 要素の後にアイコンを表示するのだから、`input` 要素と疑似クラスと疑似要素を全部一気につなげて `input:valid::after` としたいところですが、ちょっと待って！この `input` 要素 DOM にはドキュメントツリーコンテントがないので疑似要素をくっつけることができないのです。なのでここでは適当な要素、 `span` を使うことにします。

```html
<input id="username" type="text" pattern="[a-zA-Z0-9_-]{6,12}" autofocus required>
<span class="icon-validation" data-icon="&#xe000"></span> 
```

`data-*` 属性を使って絵フォント値を指定してみましょう。ここでは `span` 中に `data-icon` というカスタム属性を作成して IcoMoon で作成した特定のフォントのキャラクター値を指定しています。

```css
:valid + .icon-validation::before {
    content: attr(data-icon);
    color: green;
}
```

簡単な CSS ではありますがこの数行にはいろいろな意味を含んでいます。まず、`+` は Adjacent Sibling （隣接）セレクタ、直後に後続する要素のみ指定しています。そして疑似要素のコンテントは定義されたカスタムデータ属性を使っています。この HTML5 カスタムデータ属性 (`data-*`) は、DOM ステートを保ったまま少量のプライベートデータを保存できるのです。確かに絵フォントキャラクターを `::before` 疑似要素の、`content` プロパティで直接使うことはできるのですが、ルー大柴みたいに言ってみれば、この `data-*` を使ってデータバインディグする方法がセマンティックでベターだと思うぜ☆

## カスタムエラーの設定

エラーメッセージの表示をカスタマイズするには大まかに２つの方法があります。

では簡単な方法から。これは `title` 属性を使ったインラインテキストを表示させる方法で、ここで指定されたテキストはデフォルトのエラーメッセージに下に表示されます。したの画像は Opera 12 です。  
<img class="alignnone size-full wp-image-329" src="/assets/images/articles/2012/12/screenshot-custom-opera12.png" alt="" width="500" height="150" />

```html
<input id="username" type="text" pattern="[a-zA-Z0-9_-]{6,12}" autofocus required 
       title="must be alphanumeric in 6-12 chars"> 
```

[このデモ][1]で自分で試してみてください。

フルカスタム仕様には、ちょっとだけ DOM スクリプティング（ってか JavaScript)を使います。 メッセージを含む DOM ノードの `validationMessage` プロパティ値を変更することによって `setCustomValidity` メソッドでカスタムメッセージを指定することができます。

フォーム要素ノード上で `checkValidity` メソッドが入力フィールドを検証した際にその値が無効であった場合、そのノードで `invalid` イベントが発生されます。なので、ここでイベントリスナを登録してそこで入力フィールドが空もしくはミスマッチかを調べてやればよいのです。

```javascript
input.addEventListener('invalid', function(e) {
    if(input.validity.valueMissing){
        e.target.setCustomValidity("PLZ CREATE A USERNAME, YO!"); 
    } else if(!input.validity.valid) {
        e.target.setCustomValidity("U R DOIN IT WRONG!"); 
    } 
}, false);
```

下の画像が Firefox 16 での結果です。  
<img src="/assets/images/articles/2012/12/screenshot-custom-ff16.png" alt="" width="250" height="121" />

`validity` プロパティは、 `value`、 `valueMissing`、 `typeMismatch` など、要素のバリデーション状態を boolean で示すプロパティを含む `ValidityState` オブジェクトを返します。（`ValidityState` についてもっと詳しく学びたい方のためにブログの最後にリンクを貼っておきます。）

<a href="http://jsfiddle.net/girlie_mac/te3Qd/" target="_blank">このデモ</a>で実際にどう動くか見てみてください。コードを fork して是非自分でもほかの `ValidityState` オブジェクト状態がどういったふうに動くのか確かめてみてください。  
JavaScript と `title` 属性を両方使うことも可能です。これも自分で試してみてください。

## Put Them All Together

さてここで<a href="https://dl.dropbox.com/u/1330446/validation.html" target="_blank">フルまとめデモ</a>を見てみましょう。Windows Phone 8 メトロ UI をちょっとまねたスタイルにしてみました。なのでモバイルからもぜひためしてみてね。

[<img src="/assets/images/articles/2012/12/form-val-demo-qr.png" alt="Demo URL QR" width="128" height="127" align="right" />][2]  
**http://goo.gl/xKj0X**

実は私が試してみたところ IE 10 にはちょっとした gotcha があるのです。まあ、IE なので落とし穴があって当たり前か、とも思うのですが。このデモの場合、どうもフィールドが unfocus するまでチェックマークアイコンが表示されないようなのです。テストした他のブラウザでは入力値が有効になり次第（このデモの場合、文字数が６文字になり次第）アイコンがちゃんと表示されます。

で、下の画像は Windows Phone 8 上の IE10 Mobile の実際のスクリーンショットです。

<img src="/assets/images/articles/2012/12/screenshot-ie10m.png" alt="screenshot of IE10 mobile" width="600" height="410" />

ちょっと端折った箇所もあるのでわかりにくい所もあったかもしれませんが、これからのフォーム UX の参考になっていただけえたらうれしいです。あ、あと最後に。フォールバックについて書きませんでしたが、バリデーションがすべてのブラウザに実装されているわけではないので実際は送信されたデータはサーバサイドでもしっかり管理することが大切です。当然といえば当然なのですが念のため。

ではよいお年を（ってちょっとまだ早いか）。

## Learn More

日本語

*   MSDN: <a href="http://msdn.microsoft.com/ja-jp/library/ie/hh673544(v=vs.85).aspx" target="_blank">フォーム (Windows)</a>
*   Adobe: <a href="http://www.adobe.com/jp/devnet/dreamweaver/articles/html5pack_css3_part4.html" target="_blank">HTML5&#038;CSS3入門 第4回 @font-face（ウェブフォント）の利用</a>

英語

*   WebPlatform.org: <a href="http://docs.webplatform.org/wiki/guides/html5_form_features" target="_blank">HTML5 form features</a>
*   Dive Into HTML5: <a href="http://diveintohtml5.info/forms.html" target="_blank">A Form of Madness</a>
*   W3C: <a href="http://www.w3.org/TR/css3-fonts/" target="_blank">CSS Fonts Module Level 3</a>
*   Six Revisions: <a href="http://sixrevisions.com/css/font-face-guide/" target="_blank">The Essential Guide to @font-face</a>
*   WebPlatform.org: <a href="http://docs.webplatform.org/wiki/css/selectors/pseudo-elements" target="_blank">Pseudo-elements</a>
*   MSDN: <a href="http://msdn.microsoft.com/en-us/library/windows/apps/hh466212.aspx" target="_blank">ValidityState object</a>

 [1]: http://jsfiddle.net/girlie_mac/vuP4n/
 [2]: https://dl.dropbox.com/u/1330446/validation.html