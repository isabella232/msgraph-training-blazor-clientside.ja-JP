---
ms.openlocfilehash: f98548a1332417d92b126a2cb7499fea5306b34f
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584581"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="38f18-101">この演習では、Azure AD での認証をサポートするために、前の手順で作成したアプリケーションを拡張します。</span><span class="sxs-lookup"><span data-stu-id="38f18-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="38f18-102">これは、Microsoft Graph API を呼び出すのに必要な OAuth アクセス トークンを取得するために必要です。</span><span class="sxs-lookup"><span data-stu-id="38f18-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph API.</span></span>

1. <span data-ttu-id="38f18-103">**/Wwwroot/appsettings.jsを** 開きます。</span><span class="sxs-lookup"><span data-stu-id="38f18-103">Open **./wwwroot/appsettings.json**.</span></span> <span data-ttu-id="38f18-104">プロパティを追加 `GraphScopes` し、 `Authority` and の `ClientId` 値を次のように更新します。</span><span class="sxs-lookup"><span data-stu-id="38f18-104">Add a `GraphScopes` property and update the `Authority` and `ClientId` values to match the following.</span></span>

    :::code language="json" source="../demo/GraphTutorial/wwwroot/appsettings.example.json" highlight="3-4,7":::

    <span data-ttu-id="38f18-105">を `YOUR_APP_ID_HERE` アプリ登録のアプリケーション ID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="38f18-105">Replace `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="38f18-106">Git などのソース管理を使用している場合は、ファイル **のappsettings.js** をソース管理から除外して、アプリ ID が誤ってリークしないようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="38f18-106">If you're using source control such as git, now would be a good time to exclude the **appsettings.json** file from source control to avoid inadvertently leaking your app ID.</span></span>

    <span data-ttu-id="38f18-107">値に含まれる範囲を確認し `GraphScopes` ます。</span><span class="sxs-lookup"><span data-stu-id="38f18-107">Review the scopes included in the `GraphScopes` value.</span></span>

    - <span data-ttu-id="38f18-108">**User.** ユーザーのプロファイルと写真をアプリケーションが取得できるようにします。</span><span class="sxs-lookup"><span data-stu-id="38f18-108">**User.Read** allows the application to get the user's profile and photo.</span></span>
    - <span data-ttu-id="38f18-109">**MailboxSettings** を使用すると、アプリケーションは、ユーザーの優先タイムゾーンを含むメールボックスの設定を取得できます。</span><span class="sxs-lookup"><span data-stu-id="38f18-109">**MailboxSettings.Read** allows the application to get mailbox settings, which includes the user's preferred time zone.</span></span>
    - <span data-ttu-id="38f18-110">の場合、アプリケーションは、ユーザーの予定表の読み取りおよび書き込みを **行うことができます。**</span><span class="sxs-lookup"><span data-stu-id="38f18-110">**Calendars.ReadWrite** allows the application to read and write to the user's calendar.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="38f18-111">サインインの実装</span><span class="sxs-lookup"><span data-stu-id="38f18-111">Implement sign-in</span></span>

<span data-ttu-id="38f18-112">この時点で、.NET コアプロジェクトテンプレートには、サインインを有効にするためのコードが追加されています。</span><span class="sxs-lookup"><span data-stu-id="38f18-112">At this point the .NET Core project template has added the code to enable sign in.</span></span> <span data-ttu-id="38f18-113">ただし、このセクションでは、Microsoft Graph からユーザーの id に情報を追加することによって、利便性を向上させるためのコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="38f18-113">However, in this section you'll add additional code to improve the experience by adding information from Microsoft Graph to the user's identity.</span></span>

1. <span data-ttu-id="38f18-114">を開き、その内容を次のように置き換えます **。**</span><span class="sxs-lookup"><span data-stu-id="38f18-114">Open **./Pages/Authentication.razor** and replace its contents with the following.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/Authentication.razor" id="AuthenticationSnippet":::

    <span data-ttu-id="38f18-115">これにより、ログイン失敗時に認証プロセスによって返されたエラーメッセージが表示されなくなるという既定のエラーメッセージが置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="38f18-115">This replaces the default error message when login fails to display any error message returned by the authentication process.</span></span>

1. <span data-ttu-id="38f18-116">プロジェクトのルートに **Graph** という名前の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="38f18-116">Create a new directory in the root of the project named **Graph**.</span></span>

1. <span data-ttu-id="38f18-117">**GraphUserAccountFactory.cs** という名前のディレクトリに新しいファイルを作成し、次のコードを追加します **。**</span><span class="sxs-lookup"><span data-stu-id="38f18-117">Create a new file in the **./Graph** directory named **GraphUserAccountFactory.cs** and add the following code.</span></span>

    ```csharp
    using System.Security.Claims;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Components.WebAssembly.Authentication;
    using Microsoft.AspNetCore.Components.WebAssembly.Authentication.Internal;
    using Microsoft.Extensions.Logging;
    using Microsoft.Graph;

    namespace GraphTutorial.Graph
    {
        // Extends the AccountClaimsPrincipalFactory that builds
        // a user identity from the identity token.
        // This class adds additional claims to the user's ClaimPrincipal
        // that hold values from Microsoft Graph
        public class GraphUserAccountFactory
            : AccountClaimsPrincipalFactory<RemoteUserAccount>
        {
            private readonly IAccessTokenProviderAccessor accessor;
            private readonly ILogger<GraphUserAccountFactory> logger;

            public GraphUserAccountFactory(IAccessTokenProviderAccessor accessor,
                ILogger<GraphUserAccountFactory> logger)
            : base(accessor)
            {
                this.accessor = accessor;
                this.logger = logger;
            }

            public async override ValueTask<ClaimsPrincipal> CreateUserAsync(
                RemoteUserAccount account,
                RemoteAuthenticationUserOptions options)
            {
                // Create the base user
                var initialUser = await base.CreateUserAsync(account, options);

                // If authenticated, we can call Microsoft Graph
                if (initialUser.Identity.IsAuthenticated)
                {
                    try
                    {
                        // Add additional info from Graph to the identity
                        await AddGraphInfoToClaims(accessor, initialUser);
                    }
                    catch (AccessTokenNotAvailableException exception)
                    {
                        logger.LogError($"Graph API access token failure: {exception.Message}");
                    }
                    catch (ServiceException exception)
                    {
                        logger.LogError($"Graph API error: {exception.Message}");
                        logger.LogError($"Response body: {exception.RawResponseBody}");
                    }
                }

                return initialUser;
            }

            private async Task AddGraphInfoToClaims(
                IAccessTokenProviderAccessor accessor,
                ClaimsPrincipal claimsPrincipal)
            {
                // TEMPORARY: Get the token and log it
                var result = await accessor.TokenProvider.RequestAccessToken();

                if (result.TryGetToken(out var token))
                {
                    logger.LogInformation($"Access token: {token.Value}");
                }
            }
        }
    }
    ```

    <span data-ttu-id="38f18-118">このクラスは、 **AccountClaimsPrincipalFactory** クラスを拡張し、メソッドをオーバーライドし `CreateUserAsync` ます。</span><span class="sxs-lookup"><span data-stu-id="38f18-118">This class extends the **AccountClaimsPrincipalFactory** class and overrides the `CreateUserAsync` method.</span></span> <span data-ttu-id="38f18-119">現時点では、このメソッドは、デバッグのためにアクセストークンのみをログに記録します。</span><span class="sxs-lookup"><span data-stu-id="38f18-119">For now, this method only logs the access token for debugging purposes.</span></span> <span data-ttu-id="38f18-120">この手順の後半では、Microsoft Graph の呼び出しを実装します。</span><span class="sxs-lookup"><span data-stu-id="38f18-120">You'll implement the Microsoft Graph calls later in this exercise.</span></span>

1. <span data-ttu-id="38f18-121">**Program.cs** を開き、次のステートメントを `using` ファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="38f18-121">Open **./Program.cs** and add the following `using` statements at the top of the file.</span></span>

    ```csharp
    using Microsoft.AspNetCore.Components.WebAssembly.Authentication;
    using GraphTutorial.Graph;
    ```

1. <span data-ttu-id="38f18-122">内部 `Main` で、既存の `builder.Services.AddMsalAuthentication` 通話を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="38f18-122">Inside `Main`, replace the existing `builder.Services.AddMsalAuthentication` call with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Program.cs" id="AddMsalAuthSnippet":::

    <span data-ttu-id="38f18-123">このコードの内容を検討してください。</span><span class="sxs-lookup"><span data-stu-id="38f18-123">Consider what this code does.</span></span>

    - <span data-ttu-id="38f18-124">の値を `GraphScopes` **appsettings.js** から読み込み、msal プロバイダで使用される既定のスコープに各スコープを追加します。</span><span class="sxs-lookup"><span data-stu-id="38f18-124">It loads the value of `GraphScopes` from **appsettings.json** and adds each scope to the default scopes used by the MSAL provider.</span></span>
    - <span data-ttu-id="38f18-125">既存のアカウントファクトリを **GraphUserAccountFactory** クラスに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="38f18-125">It replaces the existing account factory with the **GraphUserAccountFactory** class.</span></span>

1. <span data-ttu-id="38f18-126">変更内容を保存し、アプリを再起動します。</span><span class="sxs-lookup"><span data-stu-id="38f18-126">Save your changes and restart the app.</span></span> <span data-ttu-id="38f18-127">ログインするには、 **ログイン** リンクを使用します。</span><span class="sxs-lookup"><span data-stu-id="38f18-127">Use the **Log in** link to log in.</span></span> <span data-ttu-id="38f18-128">要求されたアクセス許可を確認して承諾します。</span><span class="sxs-lookup"><span data-stu-id="38f18-128">Review and accept the requested permissions.</span></span>

1. <span data-ttu-id="38f18-129">アプリがウェルカムメッセージで更新されます。</span><span class="sxs-lookup"><span data-stu-id="38f18-129">The app refreshes with a welcome message.</span></span> <span data-ttu-id="38f18-130">ブラウザーの開発者ツールにアクセスし、[ **コンソール** ] タブを確認します。アプリは、アクセストークンをログに記録します。</span><span class="sxs-lookup"><span data-stu-id="38f18-130">Access your browser's developer tools and review the **Console** tab. The app logs the access token.</span></span>

    ![アクセストークンを表示する、ブラウザーの [開発者用ツール] ウィンドウのスクリーンショット](images/access-token.png)

## <a name="get-user-details"></a><span data-ttu-id="38f18-132">ユーザーの詳細情報を取得する</span><span class="sxs-lookup"><span data-stu-id="38f18-132">Get user details</span></span>

<span data-ttu-id="38f18-133">ユーザーがログインすると、Microsoft Graph からそのユーザーの情報を入手できます。</span><span class="sxs-lookup"><span data-stu-id="38f18-133">Once the user is logged in, you can get their information from Microsoft Graph.</span></span> <span data-ttu-id="38f18-134">このセクションでは、Microsoft Graph の情報を使用して、ユーザーの **ClaimsPrincipal** に追加のクレームを追加します。</span><span class="sxs-lookup"><span data-stu-id="38f18-134">In this section you'll use information from Microsoft Graph to add additional claims to the user's **ClaimsPrincipal**.</span></span>

1. <span data-ttu-id="38f18-135">**GraphClaimsPrincipalExtensions.cs** という名前のディレクトリに新しいファイルを作成し、次のコードを追加します **。**</span><span class="sxs-lookup"><span data-stu-id="38f18-135">Create a new file in the **./Graph** directory named **GraphClaimsPrincipalExtensions.cs** and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphClaimsPrincipalExtensions.cs" id="GraphClaimsExtensionsSnippet":::

    <span data-ttu-id="38f18-136">このコードでは、 **ClaimsPrincipal** クラスの拡張メソッドを実装します。これにより、クレームを取得し、Microsoft Graph オブジェクトからの値を設定することができます。</span><span class="sxs-lookup"><span data-stu-id="38f18-136">This code implements extension methods for the **ClaimsPrincipal** class that allow you to get and set claims with values from Microsoft Graph objects.</span></span>

1. <span data-ttu-id="38f18-137">**BlazorAuthProvider.cs** という名前のディレクトリに新しいファイルを作成し、次のコードを追加します **。**</span><span class="sxs-lookup"><span data-stu-id="38f18-137">Create a new file in the **./Graph** directory named **BlazorAuthProvider.cs** and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/BlazorAuthProvider.cs" id="BlazorAuthProviderSnippet":::

    <span data-ttu-id="38f18-138">このコードでは、microsoft Graph SDK の認証プロバイダを実装します。 **AspNetCore** パッケージによって提供される **IAccessTokenProviderAccessor** を使用してアクセストークンを取得します。</span><span class="sxs-lookup"><span data-stu-id="38f18-138">This code implements an authentication provider for the Microsoft Graph SDK that uses the **IAccessTokenProviderAccessor** provided by the **Microsoft.AspNetCore.Components.WebAssembly.Authentication** package to get access tokens.</span></span>

1. <span data-ttu-id="38f18-139">**GraphClientFactory.cs** という名前のディレクトリに新しいファイルを作成し、次のコードを追加します **。**</span><span class="sxs-lookup"><span data-stu-id="38f18-139">Create a new file in the **./Graph** directory named **GraphClientFactory.cs** and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphClientFactory.cs" id="GraphClientFactorySnippet":::

    <span data-ttu-id="38f18-140">このクラスは、 **BlazorAuthProvider** で構成される **graphserviceclient** を作成します。</span><span class="sxs-lookup"><span data-stu-id="38f18-140">This class creates a **GraphServiceClient** configured with the **BlazorAuthProvider**.</span></span>

1. <span data-ttu-id="38f18-141">**Program.cs** を開き、新しい **Httpclient** の **BaseAddress** をに変更します。 `"https://graph.microsoft.com"`</span><span class="sxs-lookup"><span data-stu-id="38f18-141">Open **./Program.cs** and change the **BaseAddress** of the new **HttpClient** to `"https://graph.microsoft.com"`.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Program.cs" id="HttpClientSnippet":::

1. <span data-ttu-id="38f18-142">行の前に次のコードを追加し `await builder.Build().RunAsync();` ます。</span><span class="sxs-lookup"><span data-stu-id="38f18-142">Add the following code before the `await builder.Build().RunAsync();` line.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Program.cs" id="AddGraphClientFactorySnippet":::

    <span data-ttu-id="38f18-143">これにより、 **Graphclientfactory** が、依存関係の挿入を介して利用できるようにするスコープ付きサービスとして追加されます。</span><span class="sxs-lookup"><span data-stu-id="38f18-143">This adds the **GraphClientFactory** as a scoped service that we can make available via dependency injection.</span></span>

1. <span data-ttu-id="38f18-144">/Graph/GraphUserAccountFactory.cs を開き、次のプロパティをクラスに追加します **。**</span><span class="sxs-lookup"><span data-stu-id="38f18-144">Open **./Graph/GraphUserAccountFactory.cs** and add the following property to the class.</span></span>

    ```csharp
    private readonly GraphClientFactory clientFactory;
    ```

1. <span data-ttu-id="38f18-145">**Graphclientfactory** パラメーターを取得し、それをプロパティに割り当てるように、コンストラクターを更新し `clientFactory` ます。</span><span class="sxs-lookup"><span data-stu-id="38f18-145">Update the constructor to take a **GraphClientFactory** parameter and assign it to the `clientFactory` property.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphUserAccountFactory.cs" id="ConstructorSnippet" highlight="2,7":::

1. <span data-ttu-id="38f18-146">既存の `AddGraphInfoToClaims` 関数を、以下の関数で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="38f18-146">Replace the existing `AddGraphInfoToClaims` function with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphUserAccountFactory.cs" id="AddGraphInfoToClaimsSnippet":::

    <span data-ttu-id="38f18-147">このコードの内容を検討してください。</span><span class="sxs-lookup"><span data-stu-id="38f18-147">Consider what this code does.</span></span>

    - <span data-ttu-id="38f18-148">[ユーザーのプロファイルを取得](https://docs.microsoft.com/graph/api/user-get)します。</span><span class="sxs-lookup"><span data-stu-id="38f18-148">It [gets the user's profile](https://docs.microsoft.com/graph/api/user-get).</span></span>
        - <span data-ttu-id="38f18-149">を使用 `Select` して、返されるプロパティを制限します。</span><span class="sxs-lookup"><span data-stu-id="38f18-149">It uses `Select` to limit which properties are returned.</span></span>
    - <span data-ttu-id="38f18-150">[ユーザーの写真を取得](https://docs.microsoft.com/graph/api/profilephoto-get)します。</span><span class="sxs-lookup"><span data-stu-id="38f18-150">It [gets the user's photo](https://docs.microsoft.com/graph/api/profilephoto-get).</span></span>
        - <span data-ttu-id="38f18-151">具体的には、ユーザーの写真の48x48 ピクセルバージョンを要求します。</span><span class="sxs-lookup"><span data-stu-id="38f18-151">It requests specifically the 48x48 pixel version of the user's photo.</span></span>
    - <span data-ttu-id="38f18-152">**ClaimsPrincipal** に情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="38f18-152">It adds the information to the **ClaimsPrincipal**.</span></span>

1. <span data-ttu-id="38f18-153">**/Shared/logindisplayrazor** を開き、次の変更を行います。</span><span class="sxs-lookup"><span data-stu-id="38f18-153">Open **./Shared/LoginDisplay.razor** and make the following changes.</span></span>

    - <span data-ttu-id="38f18-154">`/img/no-profile-photo.png`をに置き換え `@(context.User.GetUserGraphPhoto() ?? "/img/no-profile-photo.png")` ます。</span><span class="sxs-lookup"><span data-stu-id="38f18-154">Replace `/img/no-profile-photo.png` with `@(context.User.GetUserGraphPhoto() ?? "/img/no-profile-photo.png")`.</span></span>
    - <span data-ttu-id="38f18-155">`placeholder@contoso.com`をに置き換え `@context.User.GetUserGraphEmail()` ます。</span><span class="sxs-lookup"><span data-stu-id="38f18-155">Replace `placeholder@contoso.com` with `@context.User.GetUserGraphEmail()`.</span></span>

    ```razor
    ...
    <img src="@(context.User.GetUserGraphPhoto() ?? "/img/no-profile-photo.png")"
         class="nav-profile-photo rounded-circle align-self-center mr-2">

    ...

    <p class="dropdown-item-text text-muted mb-0">@context.User.GetUserGraphEmail()</p>
    ...
    ```

1. <span data-ttu-id="38f18-156">変更内容をすべて保存し、アプリを再起動します。</span><span class="sxs-lookup"><span data-stu-id="38f18-156">Save all of your changes and restart the app.</span></span> <span data-ttu-id="38f18-157">アプリにログインします。</span><span class="sxs-lookup"><span data-stu-id="38f18-157">Log into the app.</span></span> <span data-ttu-id="38f18-158">アプリは、トップメニューにユーザーの写真を表示するように更新されます。</span><span class="sxs-lookup"><span data-stu-id="38f18-158">The app updates to show the user's photo in the top menu.</span></span> <span data-ttu-id="38f18-159">ユーザーの写真を選択すると、ユーザーの名前、電子メールアドレス、および **ログアウトボタンを** 含むドロップダウンメニューが開きます。</span><span class="sxs-lookup"><span data-stu-id="38f18-159">Selecting the user's photo opens a drop-down menu with the user's name, email address, and a **Log out** button.</span></span>

    ![ユーザーの写真が表示されているアプリのスクリーンショット](images/user-photo.png)

    ![ドロップダウンメニューのスクリーンショット](images/user-info.png)
