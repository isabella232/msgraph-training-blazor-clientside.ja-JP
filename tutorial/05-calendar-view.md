---
ms.openlocfilehash: 33bdb86a4a4af997c8ca522e23ec2f883fdeda88
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584692"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="42ba7-101">このセクションでは、Microsoft Graph をアプリケーションに追加して、現在の週のユーザーの予定表のビューを取得します。</span><span class="sxs-lookup"><span data-stu-id="42ba7-101">In this section you will further incorporate Microsoft Graph into the application to get a view of the user's calendar for the current week.</span></span>

## <a name="get-a-calendar-view"></a><span data-ttu-id="42ba7-102">予定表ビューを取得する</span><span class="sxs-lookup"><span data-stu-id="42ba7-102">Get a calendar view</span></span>

1. <span data-ttu-id="42ba7-103">**Calendar** という名前 **のディレクトリに** 新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="42ba7-103">Create a new file in the **./Pages** directory named **Calendar.razor** and add the following code.</span></span>

    ```razor
    @page "/calendar"
    @using Microsoft.Graph
    @using TimeZoneConverter

    @inject GraphTutorial.Graph.GraphClientFactory clientFactory

    <AuthorizeView>
        <Authorized>
            <!-- Temporary JSON dump of events -->
            <code>@graphClient.HttpProvider.Serializer.SerializeObject(events)</code>
        </Authorized>
        <NotAuthorized>
            <RedirectToLogin />
        </NotAuthorized>
    </AuthorizeView>

    @code{
        [CascadingParameter]
        private Task<AuthenticationState> authenticationStateTask { get; set; }

        private GraphServiceClient graphClient;
        private IList<Event> events = new List<Event>();
        private string dateTimeFormat;
    }
    ```

1. <span data-ttu-id="42ba7-104">次のコードをセクション内に追加し `@code{}` ます。</span><span class="sxs-lookup"><span data-stu-id="42ba7-104">Add the following code inside the `@code{}` section.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Pages/Calendar.razor" id="GetEventsSnippet":::

    <span data-ttu-id="42ba7-105">このコードの内容を検討してください。</span><span class="sxs-lookup"><span data-stu-id="42ba7-105">Consider what this code does.</span></span>

    - <span data-ttu-id="42ba7-106">ユーザーに追加されたカスタムクレームから、現在のユーザーのタイムゾーン、日付の形式、および時刻の形式を取得します。</span><span class="sxs-lookup"><span data-stu-id="42ba7-106">It gets the current user's time zone, date format, and time format from the custom claims added to the user.</span></span>
    - <span data-ttu-id="42ba7-107">ユーザーが優先するタイムゾーンで、現在の週の開始と終了を計算します。</span><span class="sxs-lookup"><span data-stu-id="42ba7-107">It calculates the start and end of the current week in the user's preferred time zone.</span></span>
    - <span data-ttu-id="42ba7-108">現在の週の Microsoft Graph から予定表ビューを取得します。</span><span class="sxs-lookup"><span data-stu-id="42ba7-108">It gets a calendar view from Microsoft Graph for the current week.</span></span>
        - <span data-ttu-id="42ba7-109">このヘッダーには、 `Prefer: outlook.timezone` Microsoft Graph が `start` 指定されたタイムゾーンのプロパティとプロパティを返すためのヘッダーが含まれてい `end` ます。</span><span class="sxs-lookup"><span data-stu-id="42ba7-109">It includes the `Prefer: outlook.timezone` header to cause Microsoft Graph to return the `start` and `end` properties in the specified time zone.</span></span>
        - <span data-ttu-id="42ba7-110">を使用して `Top(50)` 、応答で50イベントを要求します。</span><span class="sxs-lookup"><span data-stu-id="42ba7-110">It uses `Top(50)` to request up to 50 events in the response.</span></span>
        - <span data-ttu-id="42ba7-111">を使用して、 `Select(u => new {})` アプリによって使用されるプロパティのみを要求します。</span><span class="sxs-lookup"><span data-stu-id="42ba7-111">It uses `Select(u => new {})` to request just the properties used by the app.</span></span>
        - <span data-ttu-id="42ba7-112">を使用して `OrderBy("start/dateTime")` 、結果を開始時刻で並べ替えます。</span><span class="sxs-lookup"><span data-stu-id="42ba7-112">It uses `OrderBy("start/dateTime")` to sort the results by start time.</span></span>

1. <span data-ttu-id="42ba7-113">変更内容をすべて保存し、アプリを再起動します。</span><span class="sxs-lookup"><span data-stu-id="42ba7-113">Save all of your changes and restart the app.</span></span> <span data-ttu-id="42ba7-114">[ **予定表** ] ナビゲーション項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="42ba7-114">Choose the **Calendar** nav item.</span></span> <span data-ttu-id="42ba7-115">アプリには、Microsoft Graph から返されたイベントの JSON 表現が表示されます。</span><span class="sxs-lookup"><span data-stu-id="42ba7-115">The app displays a JSON representation of the events returned from Microsoft Graph.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="42ba7-116">結果の表示</span><span class="sxs-lookup"><span data-stu-id="42ba7-116">Display the results</span></span>

<span data-ttu-id="42ba7-117">これで、JSON ダンプをよりユーザーフレンドリなものに置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="42ba7-117">Now you can replace the JSON dump with something more user-friendly.</span></span>

1. <span data-ttu-id="42ba7-118">次の関数をセクション内に追加し `@code{}` ます。</span><span class="sxs-lookup"><span data-stu-id="42ba7-118">Add the following function inside the `@code{}` section.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Pages/Calendar.razor" id="FormatDateSnippet":::

    <span data-ttu-id="42ba7-119">このコードは ISO 8601 の日付文字列を取得し、それをユーザーの優先する日付と時刻の形式に変換します。</span><span class="sxs-lookup"><span data-stu-id="42ba7-119">This code takes an ISO 8601 date string and converts it into the user's preferred date and time format.</span></span>

1. <span data-ttu-id="42ba7-120">`<code>`要素内の要素を `<Authorized>` 次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="42ba7-120">Replace the `<code>` element inside the `<Authorized>` element with the following.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/Calendar.razor" id="CalendarViewSnippet":::

    <span data-ttu-id="42ba7-121">これにより、Microsoft Graph によって返されるイベントのテーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="42ba7-121">This creates a table of the events returned by Microsoft Graph.</span></span>

1. <span data-ttu-id="42ba7-122">変更内容を保存し、アプリを再起動します。</span><span class="sxs-lookup"><span data-stu-id="42ba7-122">Save your changes and restart the app.</span></span> <span data-ttu-id="42ba7-123">これで、 **予定表** ページがイベントのテーブルをレンダリングするようになります。</span><span class="sxs-lookup"><span data-stu-id="42ba7-123">Now the **Calendar** page renders a table of events.</span></span>

    ![イベントの表を表示するアプリのスクリーンショット](images/calendar-view.png)
