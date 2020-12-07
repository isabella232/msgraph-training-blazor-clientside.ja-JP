---
ms.openlocfilehash: 744df064e4fdc1bbf7821ae43a7b7878148902e9
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584683"
---
<!-- markdownlint-disable MD002 MD041 -->

まず、Blazor WebAssembly アプリを作成します。

1. プロジェクトを作成するディレクトリで、コマンドラインインターフェイス (CLI) を開きます。 次のコマンドを実行します。

    ```Shell
    dotnet new blazorwasm --auth SingleOrg -o GraphTutorial
    ```

    この `--auth SingleOrg` パラメーターにより、生成されたプロジェクトに、Microsoft identity platform による認証の構成が含まれるようになります。

1. プロジェクトが作成されたら、現在のディレクトリを **Graphtutorial** ディレクトリに変更し、CLI で次のコマンドを実行して、動作を確認します。

    ```Shell
    dotnet watch run
    ```

1. ブラウザーを開き、を参照し `https://localhost:5001` ます。 すべてが動作している場合は、"Hello, world!" と表示されます。 メッセージ。

> [!IMPORTANT]
> **Localhost** の証明書が信頼されていないことを示す警告が表示された場合は、.NET コア CLI を使用して開発証明書をインストールして信頼できます。 特定のオペレーティングシステムの手順については、「 [ASP.NET Core で HTTPS を強制](/aspnet/core/security/enforcing-ssl?view=aspnetcore-3.1) する」を参照してください。

## <a name="add-nuget-packages"></a>NuGet パッケージを追加する

に進む前に、後で使用する追加の NuGet パッケージをインストールします。

- [Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/): Microsoft Graph を呼び出すためのものです。
- Windows タイムゾーン識別子を IANA 識別子に変換するための[TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) 。

1. CLI で次のコマンドを実行して、依存関係をインストールします。

    ```Shell
    dotnet add package Microsoft.Graph --version 3.18.0
    dotnet add package TimeZoneConverter
    ```

## <a name="design-the-app"></a>アプリを設計する

このセクションでは、アプリケーションの基本的な UI 構造を作成します。

1. テンプレートによって生成されたサンプルページを削除します。 次のファイルを削除します。

    - **./_/カウンター**
    - **.////取得データ**
    - **./Shared/SurveyPrompt.razor**
    - **./wwwroot/sample-data/weather.js**

1. **/Wwwroot/index.html** を開き、終了タグの **直前に** 次のコードを追加し `</body>` ます。

    :::code language="html" source="../demo/GraphTutorial/wwwroot/index.html" id="BootStrapJSSnippet":::

    これにより、 [ブートストラップ](https://getbootstrap.com/docs/4.5/getting-started/introduction/) javascript ファイルが追加されます。

1. **/Wwwroot/css/app.css** を開き、次のコードを追加します。

    :::code language="css" source="../demo/GraphTutorial/wwwroot/css/app.css" id="CssSnippet":::

1. を開き、その内容を次のように置き換えます **。**

    :::code language="razor" source="../demo/GraphTutorial/Shared/NavMenu.razor" id="NavMenuSnippet":::

1. を開き、その内容を次のように置き換えます **。**

    :::code language="razor" source="../demo/GraphTutorial/Pages/Index.razor" id="IndexSnippet":::

1. を開き、その内容を次のように置き換えます **。**

    ```razor
    @using Microsoft.AspNetCore.Components.Authorization
    @using Microsoft.AspNetCore.Components.WebAssembly.Authentication

    @inject NavigationManager Navigation
    @inject SignOutSessionStateManager SignOutManager

    <AuthorizeView>
        <Authorized>
            <a class="text-decoration-none" data-toggle="dropdown" href="#" role="button">
                <img src="/img/no-profile-photo.png" class="nav-profile-photo rounded-circle align-self-center mr-2">
            </a>
            <div class="dropdown-menu dropdown-menu-right">
                <h5 class="dropdown-item-text mb-0">@context.User.Identity.Name</h5>
                <p class="dropdown-item-text text-muted mb-0">placeholder@contoso.com</p>
                <div class="dropdown-divider"></div>
                <button class="dropdown-item" @onclick="BeginLogout">Log out</button>
            </div>
        </Authorized>
        <NotAuthorized>
            <a href="authentication/login">Log in</a>
        </NotAuthorized>
    </AuthorizeView>

    @code{
        private async Task BeginLogout(MouseEventArgs args)
        {
            await SignOutManager.SetSignOutState();
            Navigation.NavigateTo("authentication/logout");
        }
    }
    ```

1. **Img** という名前の **./wwwroot** ディレクトリに新しいディレクトリを作成します。 このディレクトリに、選択した名前の **no-profile-photo.png** のイメージファイルを追加します。 この画像は、ユーザーが Microsoft Graph に写真を持たない場合にユーザーの写真として使用されます。

    > [!TIP]
    > これらのスクリーンショットに使用されているイメージは、 [GitHub](https://github.com/microsoftgraph/msgraph-training-blazor-clientside/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png)からダウンロードできます。

1. すべての変更を保存し、ページを更新します。

    ![デザインが変更されたホーム ページのスクリーンショット](./images/create-app-01.png)
