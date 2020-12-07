---
ms.openlocfilehash: 189b2d2b8499de3bf22deb117b410278307f5ed2
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584668"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="4adb8-101">このチュートリアルでは、Microsoft Graph API を使用してユーザーの予定表情報を取得する、クライアント側の Blazor WebAssembly を構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4adb8-101">This tutorial teaches you how to build a client-side Blazor WebAssembly app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="4adb8-102">完成したチュートリアルをダウンロードするだけで済む場合は、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-blazor-clientside)をダウンロードするか、クローンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="4adb8-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-blazor-clientside).</span></span> <span data-ttu-id="4adb8-103">アプリ ID と secret を使用してアプリを構成する方法については、 **demo** フォルダーの README ファイルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4adb8-103">See the README file in the **demo** folder for instructions on configuring the app with an app ID and secret.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4adb8-104">前提条件</span><span class="sxs-lookup"><span data-stu-id="4adb8-104">Prerequisites</span></span>

<span data-ttu-id="4adb8-105">このチュートリアルを開始する前に、開発用のコンピューターに [.Net CORE SDK](https://dotnet.microsoft.com/download) をインストールしておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="4adb8-105">Before you start this tutorial, you should have the [.NET Core SDK](https://dotnet.microsoft.com/download) installed on your development machine.</span></span> <span data-ttu-id="4adb8-106">SDK を持っていない場合は、「ダウンロードオプション」の前のリンクを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4adb8-106">If you do not have the SDK, visit the previous link for download options.</span></span>

<span data-ttu-id="4adb8-107">また、Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントを所有している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4adb8-107">You should also have either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span> <span data-ttu-id="4adb8-108">Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="4adb8-108">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="4adb8-109">[新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。</span><span class="sxs-lookup"><span data-stu-id="4adb8-109">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="4adb8-110">[Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="4adb8-110">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4adb8-111">このチュートリアルは、.NET Core SDK version 3.1.402 を使用して作成されています。</span><span class="sxs-lookup"><span data-stu-id="4adb8-111">This tutorial was written with .NET Core SDK version 3.1.402.</span></span> <span data-ttu-id="4adb8-112">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。</span><span class="sxs-lookup"><span data-stu-id="4adb8-112">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="feedback"></a><span data-ttu-id="4adb8-113">フィードバック</span><span class="sxs-lookup"><span data-stu-id="4adb8-113">Feedback</span></span>

<span data-ttu-id="4adb8-114">このチュートリアルに関するフィードバックは、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-blazor-clientside)に記入してください。</span><span class="sxs-lookup"><span data-stu-id="4adb8-114">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-blazor-clientside).</span></span>
