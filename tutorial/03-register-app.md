---
ms.openlocfilehash: 766f41b3d838130a5e0b64ba22425496eecb1c71
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584689"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="b9995-101">この演習では、Azure Active Directory 管理センターを使用して、新しい Azure AD web アプリケーション登録を作成します。</span><span class="sxs-lookup"><span data-stu-id="b9995-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="b9995-102">ブラウザーを開き、[Azure Active Directory 管理センター](https://aad.portal.azure.com)へ移動します。</span><span class="sxs-lookup"><span data-stu-id="b9995-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="b9995-103">**個人用アカウント** (別名: Microsoft アカウント)、または **職場/学校アカウント** を使用してログインします。</span><span class="sxs-lookup"><span data-stu-id="b9995-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="b9995-104">左側のナビゲーションで **[Azure Active Directory]** を選択し、それから **[管理]** で **[アプリの登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b9995-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="b9995-105">アプリの登録のスクリーンショット</span><span class="sxs-lookup"><span data-stu-id="b9995-105">A screenshot of the App registrations</span></span> ](./images/aad-portal-app-registrations.png)

1. <span data-ttu-id="b9995-106">**[新規登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b9995-106">Select **New registration**.</span></span> <span data-ttu-id="b9995-107">**[アプリケーションを登録]** ページで、次のように値を設定します。</span><span class="sxs-lookup"><span data-stu-id="b9995-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="b9995-108">`Blazor Graph Tutorial` に **[名前]** を設定します。</span><span class="sxs-lookup"><span data-stu-id="b9995-108">Set **Name** to `Blazor Graph Tutorial`.</span></span>
    - <span data-ttu-id="b9995-109">**[サポートされているアカウントの種類]** を **[任意の組織のディレクトリ内のアカウントと個人用の Microsoft アカウント]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="b9995-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="b9995-110">**[リダイレクト URI]** で、最初のドロップダウン リストを `Web` に設定し、それから `https://localhost:5001/authentication/login-callback` に値を設定します。</span><span class="sxs-lookup"><span data-stu-id="b9995-110">Under **Redirect URI**, set the first drop-down to `Web` and set the value to `https://localhost:5001/authentication/login-callback`.</span></span>

    ![[アプリケーションを登録する] ページのスクリーンショット](./images/aad-register-an-app.png)

1. <span data-ttu-id="b9995-112">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b9995-112">Select **Register**.</span></span> <span data-ttu-id="b9995-113">[ **Blazor Graph のチュートリアル** ] ページで、 **アプリケーション (クライアント) ID** の値をコピーして保存します。次の手順で必要になります。</span><span class="sxs-lookup"><span data-stu-id="b9995-113">On the **Blazor Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新しいアプリ登録のアプリケーション ID のスクリーンショット](./images/aad-application-id.png)

1. <span data-ttu-id="b9995-115">**[管理]** の下の **[認証]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b9995-115">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="b9995-116">暗黙的な **grant** セクションを見つけ、 **アクセストークン** と **ID トークン** を有効にします。</span><span class="sxs-lookup"><span data-stu-id="b9995-116">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="b9995-117">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b9995-117">Select **Save**.</span></span>
