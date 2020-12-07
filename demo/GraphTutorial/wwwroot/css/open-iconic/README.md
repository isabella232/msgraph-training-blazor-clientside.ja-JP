---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584572"
---
<a name="open-iconic-v111"></a>[<span data-ttu-id="30d27-101">アイコンを開く-1.1.1</span><span class="sxs-lookup"><span data-stu-id="30d27-101">Open Iconic v1.1.1</span></span>](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconic-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collection"></a><span data-ttu-id="30d27-102">開いている [アイコン] は、オープンソースの [アイコン](http://useiconic.com)の兄弟です。</span><span class="sxs-lookup"><span data-stu-id="30d27-102">Open Iconic is the open source sibling of [Iconic](http://useiconic.com).</span></span> <span data-ttu-id="30d27-103">これは、 &mdash; ブートストラップと基盤で使用する準備が整ったわずかなフットプリントを備えた、223アイコンのハイパー判読可能なコレクションです。</span><span class="sxs-lookup"><span data-stu-id="30d27-103">It is a hyper-legible collection of 223 icons with a tiny footprint&mdash;ready to use with Bootstrap and Foundation.</span></span> [<span data-ttu-id="30d27-104">コレクションを表示する</span><span class="sxs-lookup"><span data-stu-id="30d27-104">View the collection</span></span>](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a><span data-ttu-id="30d27-105">開いているアイコン</span><span class="sxs-lookup"><span data-stu-id="30d27-105">What's in Open Iconic?</span></span>

* <span data-ttu-id="30d27-106">223 8 ピクセルまでの判読可能になるように設計されたアイコン</span><span class="sxs-lookup"><span data-stu-id="30d27-106">223 icons designed to be legible down to 8 pixels</span></span>
* <span data-ttu-id="30d27-107">スーパーライト SVG ファイル-61.8 セット全体の場合は</span><span class="sxs-lookup"><span data-stu-id="30d27-107">Super-light SVG files - 61.8 for the entire set</span></span> 
* <span data-ttu-id="30d27-108">SVG スプライト &mdash; アイコンフォントのモダン置換</span><span class="sxs-lookup"><span data-stu-id="30d27-108">SVG sprite&mdash;the modern replacement for icon fonts</span></span>
* <span data-ttu-id="30d27-109">Webfont (EOT, OTF, SVG,, WOFF), PNG および Webfont 形式</span><span class="sxs-lookup"><span data-stu-id="30d27-109">Webfont (EOT, OTF, SVG, TTF, WOFF), PNG and WebP formats</span></span>
* <span data-ttu-id="30d27-110">CSS、LESS、SCSS、およびスタイラスの形式の webfont スタイルシート (ブートストラップおよび基盤のバージョンを含む)</span><span class="sxs-lookup"><span data-stu-id="30d27-110">Webfont stylesheets (including versions for Bootstrap and Foundation) in CSS, LESS, SCSS and Stylus formats</span></span>
* <span data-ttu-id="30d27-111">PNG および WebP ラスター画像 (8px、16px、24px、32px、48px、64px)</span><span class="sxs-lookup"><span data-stu-id="30d27-111">PNG and WebP raster images in 8px, 16px, 24px, 32px, 48px and 64px.</span></span>


## <a name="getting-started"></a><span data-ttu-id="30d27-112">はじめに</span><span class="sxs-lookup"><span data-stu-id="30d27-112">Getting Started</span></span>

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-icons-and-reference-sections"></a><span data-ttu-id="30d27-113">コードサンプルと、開いているアイコンを使用して作業を開始する必要がある場合は、 [アイコン](http://useiconic.com/open#icons) と [参照](http://useiconic.com/open#reference) セクションを確認してください。</span><span class="sxs-lookup"><span data-stu-id="30d27-113">For code samples and everything else you need to get started with Open Iconic, check out our [Icons](http://useiconic.com/open#icons) and [Reference](http://useiconic.com/open#reference) sections.</span></span>

### <a name="general-usage"></a><span data-ttu-id="30d27-114">一般的な使用法</span><span class="sxs-lookup"><span data-stu-id="30d27-114">General Usage</span></span>

#### <a name="using-open-iconics-svgs"></a><span data-ttu-id="30d27-115">オープンなアイコンの SVGs の使用</span><span class="sxs-lookup"><span data-stu-id="30d27-115">Using Open Iconic's SVGs</span></span>

<span data-ttu-id="30d27-116">SVGs のように、web 上にアイコンを表示する方法があると考えています。</span><span class="sxs-lookup"><span data-stu-id="30d27-116">We like SVGs and we think they're the way to display icons on the web.</span></span> <span data-ttu-id="30d27-117">開いたアイコンは基本的な SVGs であるため、その他のイメージのように表示することをお勧めします (属性を忘れないで `alt` ください)。</span><span class="sxs-lookup"><span data-stu-id="30d27-117">Since Open Iconic are just basic SVGs, we suggest you display them like you would any other image (don't forget the `alt` attribute).</span></span>

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a><span data-ttu-id="30d27-118">開いているアイコンの SVG スプライトの使用</span><span class="sxs-lookup"><span data-stu-id="30d27-118">Using Open Iconic's SVG Sprite</span></span>

<span data-ttu-id="30d27-119">また、開いたアイコンは、1つの要求でセット内のすべてのアイコンを表示できる SVG スプライトにもあります。</span><span class="sxs-lookup"><span data-stu-id="30d27-119">Open Iconic also comes in a SVG sprite which allows you to display all the icons in the set with a single request.</span></span> <span data-ttu-id="30d27-120">ハッキングにならずにアイコンフォントのようになります。</span><span class="sxs-lookup"><span data-stu-id="30d27-120">It's like an icon font, without being a hack.</span></span>

<span data-ttu-id="30d27-121">SVG スプライトからのアイコンの追加は、使用しているものとは少し異なりますが、それでもケーキにすぎません。</span><span class="sxs-lookup"><span data-stu-id="30d27-121">Adding an icon from an SVG sprite is a little different than what you're used to, but it's still a piece of cake.</span></span> <span data-ttu-id="30d27-122">*ヒント: アイコンを簡単にスタイル設定できるようにするには、次のように汎用クラスを追加することをお勧めし* `<svg>` ます。*タグと、の異なるアイコンの一意のクラス名* `<use>`*タグ。*</span><span class="sxs-lookup"><span data-stu-id="30d27-122">*Tip: To make your icons easily style able, we suggest adding a general class to the* `<svg>` *tag and a unique class name for each different icon in the* `<use>` *tag.*</span></span>  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

<span data-ttu-id="30d27-123">サイズ変更アイコンには、基本的な CSS のみが必要です。</span><span class="sxs-lookup"><span data-stu-id="30d27-123">Sizing icons only needs basic CSS.</span></span> <span data-ttu-id="30d27-124">すべてのアイコンが四角形の形式になっているので、同じ `<svg>` 幅と高さのサイズのタグを設定するだけです。</span><span class="sxs-lookup"><span data-stu-id="30d27-124">All the icons are in a square format, so just set the `<svg>` tag with equal width and height dimensions.</span></span>

```
.icon {
  width: 16px;
  height: 16px;
}
```

<span data-ttu-id="30d27-125">アイコンを色分けするのはさらに簡単です。</span><span class="sxs-lookup"><span data-stu-id="30d27-125">Coloring icons is even easier.</span></span> <span data-ttu-id="30d27-126">必要なのは `fill` 、タグにルールを設定することだけです `<use>` 。</span><span class="sxs-lookup"><span data-stu-id="30d27-126">All you need to do is set the `fill` rule on the `<use>` tag.</span></span>

```
.icon-account-login {
  fill: #f00;
}
```

<span data-ttu-id="30d27-127">SVG スプライトの詳細については、 [Chris Coyier のガイド](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30d27-127">To learn more about SVG Sprites, read [Chris Coyier's guide](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span></span>

#### <a name="using-open-iconics-icon-font"></a><span data-ttu-id="30d27-128">開いているアイコンのアイコンフォントを使用する...</span><span class="sxs-lookup"><span data-stu-id="30d27-128">Using Open Iconic's Icon Font...</span></span>


##### <a name="with-bootstrap"></a><span data-ttu-id="30d27-129">...ブートストラップ付き</span><span class="sxs-lookup"><span data-stu-id="30d27-129">…with Bootstrap</span></span>

<span data-ttu-id="30d27-130">ブートストラップスタイルシートは、 `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="30d27-130">You can find our Bootstrap stylesheets in `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span></span>


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a><span data-ttu-id="30d27-131">...Foundation</span><span class="sxs-lookup"><span data-stu-id="30d27-131">…with Foundation</span></span>

<span data-ttu-id="30d27-132">基礎スタイルシートは、 `font/css/open-iconic-foundation.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="30d27-132">You can find our Foundation stylesheets in `font/css/open-iconic-foundation.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a><span data-ttu-id="30d27-133">...単独で</span><span class="sxs-lookup"><span data-stu-id="30d27-133">…on its own</span></span>

<span data-ttu-id="30d27-134">既定のスタイルシートは、 `font/css/open-iconic.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="30d27-134">You can find our default stylesheets in `font/css/open-iconic.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a><span data-ttu-id="30d27-135">ライセンス</span><span class="sxs-lookup"><span data-stu-id="30d27-135">License</span></span>

### <a name="icons"></a><span data-ttu-id="30d27-136">アイコン</span><span class="sxs-lookup"><span data-stu-id="30d27-136">Icons</span></span>

<span data-ttu-id="30d27-137">すべてのコード (SVG マークアップを含む) は、 [MIT ライセンス](http://opensource.org/licenses/MIT)の下にあります。</span><span class="sxs-lookup"><span data-stu-id="30d27-137">All code (including SVG markup) is under the [MIT License](http://opensource.org/licenses/MIT).</span></span>

### <a name="fonts"></a><span data-ttu-id="30d27-138">フォント</span><span class="sxs-lookup"><span data-stu-id="30d27-138">Fonts</span></span>

<span data-ttu-id="30d27-139">すべてのフォントは、 [Sil のライセンス](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web)の下にあります。</span><span class="sxs-lookup"><span data-stu-id="30d27-139">All fonts are under the [SIL Licensed](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span></span>
