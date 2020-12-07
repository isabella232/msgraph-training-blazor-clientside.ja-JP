---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584572"
---
<a name="open-iconic-v111"></a>[アイコンを開く-1.1.1](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconic-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collection"></a>開いている [アイコン] は、オープンソースの [アイコン](http://useiconic.com)の兄弟です。 これは、 &mdash; ブートストラップと基盤で使用する準備が整ったわずかなフットプリントを備えた、223アイコンのハイパー判読可能なコレクションです。 [コレクションを表示する](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a>開いているアイコン

* 223 8 ピクセルまでの判読可能になるように設計されたアイコン
* スーパーライト SVG ファイル-61.8 セット全体の場合は 
* SVG スプライト &mdash; アイコンフォントのモダン置換
* Webfont (EOT, OTF, SVG,, WOFF), PNG および Webfont 形式
* CSS、LESS、SCSS、およびスタイラスの形式の webfont スタイルシート (ブートストラップおよび基盤のバージョンを含む)
* PNG および WebP ラスター画像 (8px、16px、24px、32px、48px、64px)


## <a name="getting-started"></a>はじめに

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-icons-and-reference-sections"></a>コードサンプルと、開いているアイコンを使用して作業を開始する必要がある場合は、 [アイコン](http://useiconic.com/open#icons) と [参照](http://useiconic.com/open#reference) セクションを確認してください。

### <a name="general-usage"></a>一般的な使用法

#### <a name="using-open-iconics-svgs"></a>オープンなアイコンの SVGs の使用

SVGs のように、web 上にアイコンを表示する方法があると考えています。 開いたアイコンは基本的な SVGs であるため、その他のイメージのように表示することをお勧めします (属性を忘れないで `alt` ください)。

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a>開いているアイコンの SVG スプライトの使用

また、開いたアイコンは、1つの要求でセット内のすべてのアイコンを表示できる SVG スプライトにもあります。 ハッキングにならずにアイコンフォントのようになります。

SVG スプライトからのアイコンの追加は、使用しているものとは少し異なりますが、それでもケーキにすぎません。 *ヒント: アイコンを簡単にスタイル設定できるようにするには、次のように汎用クラスを追加することをお勧めし* `<svg>` ます。*タグと、の異なるアイコンの一意のクラス名* `<use>`*タグ。*  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

サイズ変更アイコンには、基本的な CSS のみが必要です。 すべてのアイコンが四角形の形式になっているので、同じ `<svg>` 幅と高さのサイズのタグを設定するだけです。

```
.icon {
  width: 16px;
  height: 16px;
}
```

アイコンを色分けするのはさらに簡単です。 必要なのは `fill` 、タグにルールを設定することだけです `<use>` 。

```
.icon-account-login {
  fill: #f00;
}
```

SVG スプライトの詳細については、 [Chris Coyier のガイド](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)を参照してください。

#### <a name="using-open-iconics-icon-font"></a>開いているアイコンのアイコンフォントを使用する...


##### <a name="with-bootstrap"></a>...ブートストラップ付き

ブートストラップスタイルシートは、 `font/css/open-iconic-bootstrap.{css, less, scss, styl}`


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a>...Foundation

基礎スタイルシートは、 `font/css/open-iconic-foundation.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a>...単独で

既定のスタイルシートは、 `font/css/open-iconic.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a>ライセンス

### <a name="icons"></a>アイコン

すべてのコード (SVG マークアップを含む) は、 [MIT ライセンス](http://opensource.org/licenses/MIT)の下にあります。

### <a name="fonts"></a>フォント

すべてのフォントは、 [Sil のライセンス](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web)の下にあります。
