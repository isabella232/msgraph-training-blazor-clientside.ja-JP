---
ms.openlocfilehash: 9029486df6b08042681c0a1a67b156cbbd0381a0
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584671"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="0fc58-101">完了したプロジェクトを実行する方法</span><span class="sxs-lookup"><span data-stu-id="0fc58-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fc58-102">前提条件</span><span class="sxs-lookup"><span data-stu-id="0fc58-102">Prerequisites</span></span>

<span data-ttu-id="0fc58-103">このフォルダーで完了したプロジェクトを実行するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="0fc58-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="0fc58-104">開発用コンピューターにインストールされている [.Net コア SDK](https://dotnet.microsoft.com/download) 。</span><span class="sxs-lookup"><span data-stu-id="0fc58-104">The [.NET Core SDK](https://dotnet.microsoft.com/download) installed on your development machine.</span></span> <span data-ttu-id="0fc58-105">(**注:** このチュートリアルは、.NET Core SDK バージョン3.1.402 を使用して作成されています。</span><span class="sxs-lookup"><span data-stu-id="0fc58-105">(**Note:** This tutorial was written with .NET Core SDK version 3.1.402.</span></span> <span data-ttu-id="0fc58-106">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。)</span><span class="sxs-lookup"><span data-stu-id="0fc58-106">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="0fc58-107">Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントのいずれか。</span><span class="sxs-lookup"><span data-stu-id="0fc58-107">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="0fc58-108">Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="0fc58-108">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="0fc58-109">[新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。</span><span class="sxs-lookup"><span data-stu-id="0fc58-109">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="0fc58-110">[Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="0fc58-110">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="0fc58-111">Web アプリケーションを Azure Active Directory 管理センターに登録する</span><span class="sxs-lookup"><span data-stu-id="0fc58-111">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="0fc58-112">ブラウザーを開き、[Azure Active Directory 管理センター](https://aad.portal.azure.com)へ移動します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-112">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="0fc58-113">**個人用アカウント** (別名: Microsoft アカウント)、または **職場/学校アカウント** を使用してログインします。</span><span class="sxs-lookup"><span data-stu-id="0fc58-113">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="0fc58-114">左側のナビゲーションで **[Azure Active Directory]** を選択し、それから **[管理]** で **[アプリの登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-114">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="0fc58-115">アプリの登録のスクリーンショット</span><span class="sxs-lookup"><span data-stu-id="0fc58-115">A screenshot of the App registrations</span></span> ](../tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="0fc58-116">**[新規登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-116">Select **New registration**.</span></span> <span data-ttu-id="0fc58-117">**[アプリケーションを登録]** ページで、次のように値を設定します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-117">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="0fc58-118">`Blazor Graph Tutorial` に **[名前]** を設定します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-118">Set **Name** to `Blazor Graph Tutorial`.</span></span>
    - <span data-ttu-id="0fc58-119">**[サポートされているアカウントの種類]** を **[任意の組織のディレクトリ内のアカウントと個人用の Microsoft アカウント]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-119">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="0fc58-120">**[リダイレクト URI]** で、最初のドロップダウン リストを `Web` に設定し、それから `https://localhost:5001/authentication/login-callback` に値を設定します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-120">Under **Redirect URI**, set the first drop-down to `Web` and set the value to `https://localhost:5001/authentication/login-callback`.</span></span>

    ![[アプリケーションを登録する] ページのスクリーンショット](../tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="0fc58-122">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-122">Select **Register**.</span></span> <span data-ttu-id="0fc58-123">[ **Blazor Graph のチュートリアル** ] ページで、 **アプリケーション (クライアント) ID** の値をコピーして保存します。次の手順で必要になります。</span><span class="sxs-lookup"><span data-stu-id="0fc58-123">On the **Blazor Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新しいアプリ登録のアプリケーション ID のスクリーンショット](../tutorial/images/aad-application-id.png)

1. <span data-ttu-id="0fc58-125">**[管理]** の下の **[認証]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-125">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="0fc58-126">暗黙的な **grant** セクションを見つけ、 **アクセストークン** と **ID トークン** を有効にします。</span><span class="sxs-lookup"><span data-stu-id="0fc58-126">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="0fc58-127">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-127">Select **Save**.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="0fc58-128">サンプルを構成する</span><span class="sxs-lookup"><span data-stu-id="0fc58-128">Configure the sample</span></span>

1. <span data-ttu-id="0fc58-129">ファイルの **/GraphTutorial/wwwroot/appsettings.example.js** の名前を **appsettings.js** に変更します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-129">Rename the **/GraphTutorial/wwwroot/appsettings.example.json** file to **appsettings.json**.</span></span>

1. <span data-ttu-id="0fc58-130">**appsettings.js** を編集して `YOUR_APP_ID_HERE` 、アプリケーション ID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0fc58-130">Edit **appsettings.json** and replace `YOUR_APP_ID_HERE` with your application ID.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="0fc58-131">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="0fc58-131">Run the sample</span></span>

<span data-ttu-id="0fc58-132">CLI で、次のコマンドを実行してアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="0fc58-132">In your CLI, run the following command to start the application.</span></span>

```Shell
dotnet run
```
