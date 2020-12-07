---
ms.openlocfilehash: 723f1d08b9d1085d47d0d5fac71da5371badc3d0
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584573"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="371c3-101">このセクションでは、ユーザーの予定表にイベントを作成する機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="371c3-101">In this section you will add the ability to create events on the user's calendar.</span></span>

1. <span data-ttu-id="371c3-102">**Newevent** という名前 **のディレクトリに** 新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="371c3-102">Create a new file in the **./Pages** directory named **NewEvent.razor** and add the following code.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/NewEvent.razor" id="NewEventFormSnippet":::

    <span data-ttu-id="371c3-103">これにより、ユーザーが新しいイベントの値を入力できるように、ページにフォームが追加されます。</span><span class="sxs-lookup"><span data-stu-id="371c3-103">This adds a form to the page so the user can enter values for the new event.</span></span>

1. <span data-ttu-id="371c3-104">ファイルの末尾に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="371c3-104">Add the following code to the end of the file.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/NewEvent.razor" id="NewEventCodeSnippet":::

    <span data-ttu-id="371c3-105">このコードの内容を検討してください。</span><span class="sxs-lookup"><span data-stu-id="371c3-105">Consider what this code does.</span></span>

    - <span data-ttu-id="371c3-106">これにより `OnInitializedAsync` 、認証されたユーザーのタイムゾーンを取得します。</span><span class="sxs-lookup"><span data-stu-id="371c3-106">In `OnInitializedAsync` it gets the authenticated user's time zone.</span></span>
    - <span data-ttu-id="371c3-107">では、 `CreateEvent` フォームからの値を使用して、新しい **Event** オブジェクトを初期化します。</span><span class="sxs-lookup"><span data-stu-id="371c3-107">In `CreateEvent` it initializes a new **Event** object using the values from the form.</span></span>
    - <span data-ttu-id="371c3-108">Graph SDK を使用して、ユーザーの予定表にイベントを追加します。</span><span class="sxs-lookup"><span data-stu-id="371c3-108">It uses the Graph SDK to add the event to the user's calendar.</span></span>

1. <span data-ttu-id="371c3-109">変更内容をすべて保存し、アプリを再起動します。</span><span class="sxs-lookup"><span data-stu-id="371c3-109">Save all of your changes and restart the app.</span></span> <span data-ttu-id="371c3-110">[ **カレンダー** ] ページで、[ **New event**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="371c3-110">On the **Calendar** page, select **New event**.</span></span> <span data-ttu-id="371c3-111">フォームに入力し、[ **作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="371c3-111">Fill in the form and choose **Create**.</span></span>

    ![新しいイベントフォームのスクリーンショット](images/create-event.png)
