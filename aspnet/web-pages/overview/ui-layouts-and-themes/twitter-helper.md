---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: ASP.NET 웹 페이지 Twitter 도우미 | Microsoft Docs
author: Rick-Anderson
description: 이 항목 및 응용 프로그램에서는 WebMatrix 3 프로젝트에 Twitter 도우미를 추가 하는 방법을 보여 줍니다. Twitter 도우미 코드를 포함 하 고 도우미를 호출 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518621"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a><span data-ttu-id="43849-104">ASP.NET 웹 페이지와 Twitter 도우미</span><span class="sxs-lookup"><span data-stu-id="43849-104">Twitter Helper with ASP.NET Web Pages</span></span>

<span data-ttu-id="43849-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="43849-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43849-106">Twitter 도우미는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43849-106">Twitter Helpers are obsolete.</span></span> <span data-ttu-id="43849-107">웹 사이트용 Twitter의 최신 engagement 도구는 [웹 사이트에 대 한 Twitter 개요](https://developer.twitter.com/en/docs/twitter-for-websites/overview)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="43849-107">For Twitter's latest engagement tools for websites, see [Twitter for Websites Overview](https://developer.twitter.com/en/docs/twitter-for-websites/overview).</span></span>

> <span data-ttu-id="43849-108">이 항목 및 응용 프로그램에서는 WebMatrix 3 프로젝트에 Twitter 도우미를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43849-108">This topic and application show how to add a Twitter Helper to your WebMatrix 3 project.</span></span> <span data-ttu-id="43849-109">Twitter 도우미 코드를 포함 하 고 도우미 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43849-109">It contains the Twitter Helper code and shows how to call the helper methods.</span></span>
> 
> <span data-ttu-id="43849-110">Tian 파일에 대 한이 코드는 Microsoft의 **이동** 에 의해 개발 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="43849-110">This code for the Twitter.cshtml file was developed by **Tian Pan** of Microsoft.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="43849-111">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="43849-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="43849-112">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="43849-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="43849-113">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="43849-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="introduction"></a><span data-ttu-id="43849-114">소개</span><span class="sxs-lookup"><span data-stu-id="43849-114">Introduction</span></span>

<span data-ttu-id="43849-115">이 항목에서는 응용 프로그램에 Twitter 도우미를 추가 하 고 Razor 구문를 사용 하 여 도우미 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43849-115">This topic demonstrates how to add a Twitter Helper to your application and use Razor syntax to call the helper methods.</span></span> <span data-ttu-id="43849-116">Twitter 도우미를 사용 하면 응용 프로그램에 Twitter 단추와 위젯을 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43849-116">The Twitter Helper makes it easy to incorporate Twitter buttons and widgets in your application.</span></span> <span data-ttu-id="43849-117">사용자의 타임 라인 또는 해시 태그에 대 한 검색 결과와 같은 Twitter 위젯을 사용 하려면 먼저 [twitter에서 위젯을](https://twitter.com/settings/widgets)만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43849-117">To use a Twitter widget, such as a user's timeline or the search results for a hashtag, you must first create the [widget on Twitter](https://twitter.com/settings/widgets).</span></span> <span data-ttu-id="43849-118">위젯을 만든 후에는 위젯 id를 받게 됩니다. 위젯을 표시 하는 도우미 메서드를 호출할 때이 위젯 id를 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="43849-118">After creating your widget, you will receive a widget id. You pass this widget id as a parameter when calling the helper methods that show widget.</span></span>

<span data-ttu-id="43849-119">이 항목은 Twitter API 버전 1.1에 대해 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="43849-119">This topic was written for version 1.1 of the Twitter API.</span></span> <span data-ttu-id="43849-120">Twitter API가 변경 되 면 프로젝트에 Twitter 도우미 코드를 직접 추가 하 여 도우미 코드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43849-120">By directly adding the Twitter Helper code to your project, you can update the helper code if the Twitter API changes.</span></span>

<span data-ttu-id="43849-121">WebMatrix 설치에 대 한 자세한 내용은 [ASP.NET 웹 페이지 2 소개-시작 하기](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="43849-121">For information about installing WebMatrix, see [Introducing ASP.NET Web Pages 2 - Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span></span>

## <a name="add-twitter-helper-to-your-project"></a><span data-ttu-id="43849-122">프로젝트에 Twitter 도우미 추가</span><span class="sxs-lookup"><span data-stu-id="43849-122">Add Twitter Helper to your project</span></span>

<span data-ttu-id="43849-123">Twitter 도우미를 추가 하려면 먼저 **App\_Code** 라는 폴더를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="43849-123">To add the Twitter Helper, first, add a folder named **App\_Code** to your project.</span></span> <span data-ttu-id="43849-124">그런 다음 **Twitter. cshtml**라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43849-124">Then, create a file named **Twitter.cshtml**.</span></span>

![App_Code 폴더](twitter-helper/_static/image1.png)

<span data-ttu-id="43849-126">Twitter의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="43849-126">Replace the default code in Twitter.cshtml with the following code.</span></span>

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a><span data-ttu-id="43849-127">웹 페이지에서 Twitter 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="43849-127">Call Twitter methods from your web pages</span></span>

<span data-ttu-id="43849-128">다음 예제에서는 프로젝트의 페이지에서 Twitter 도우미 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43849-128">The following example shows how to use the Twitter Helper methods from a page in your project.</span></span> <span data-ttu-id="43849-129">프로젝트에서 매개 변수 값을 요구 사항과 관련 된 값으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43849-129">In your project, you will want to replace the parameter values with values that are relevant to your needs.</span></span> <span data-ttu-id="43849-130">제공 된 위젯 id를 사용 하 여 메서드의 작동 방식을 탐색할 수 있지만 프로젝트의 위젯을 직접 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43849-130">You can use the provided widget ids to explore how the methods work, but you will want to generate your own widgets for your project.</span></span>

<span data-ttu-id="43849-131">아래에 표시 된 매개 변수 중 일부가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43849-131">Not all of the parameters shown below are required.</span></span> <span data-ttu-id="43849-132">선택적 매개 변수는 단추 또는 위젯이 표시 되는 방식을 사용자 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43849-132">The optional parameters are used to customize how the button or widget is displayed.</span></span> <span data-ttu-id="43849-133">예를 들어 팔 로우 단추를 사용 하려면 사용자 이름만 입력 하면 됩니다. 그러나이 예에서는 팔로 워 수를 포함 하는 방법 및 단추와 언어의 크기를 지정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43849-133">For example, the Follow Button only requires the user name to follow, but the example shows how to include the number of followers, and how specify the size of the button and the language.</span></span>

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a><span data-ttu-id="43849-134">결과 확인</span><span class="sxs-lookup"><span data-stu-id="43849-134">See the results</span></span>

<span data-ttu-id="43849-135">위의 코드는 다음과 같은 단추 및 위젯을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="43849-135">The above code produces the following buttons and widgets.</span></span> <span data-ttu-id="43849-136">이러한 단추와 위젯은 스크린샷이 아닌 완벽 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="43849-136">These buttons and widgets are fully-functional, not screenshots.</span></span> <span data-ttu-id="43849-137">Language 매개 변수가 **es**로 설정 되었으므로 다음 단추가 스페인어로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43849-137">The Follow Button is displayed in Spanish because the language parameter was set to **es**.</span></span>

### <a name="follow-button"></a><span data-ttu-id="43849-138">팔 로우 단추</span><span class="sxs-lookup"><span data-stu-id="43849-138">Follow Button</span></span>

<span data-ttu-id="43849-139">[@aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="43849-139">[Follow @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="tweet-button"></a><span data-ttu-id="43849-140">트 윗 단추</span><span class="sxs-lookup"><span data-stu-id="43849-140">Tweet Button</span></span>

<span data-ttu-id="43849-141">[트 윗](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="43849-141">[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="user-timeline-profile"></a><span data-ttu-id="43849-142">사용자 타임 라인 (프로필)</span><span class="sxs-lookup"><span data-stu-id="43849-142">User Timeline (Profile)</span></span>

<span data-ttu-id="43849-143">[트 윗 @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="43849-143">[Tweets by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="favorites"></a><span data-ttu-id="43849-144">즐겨찾기</span><span class="sxs-lookup"><span data-stu-id="43849-144">Favorites</span></span>

<span data-ttu-id="43849-145">[@Microsoft`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>` 즐겨찾기 트 윗](https://twitter.com/Microsoft/favorites)</span><span class="sxs-lookup"><span data-stu-id="43849-145">[Favorite Tweets by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="list"></a><span data-ttu-id="43849-146">목록</span><span class="sxs-lookup"><span data-stu-id="43849-146">List</span></span>

<span data-ttu-id="43849-147">[@Microsoft/MS\_소비자\_밴드에서 트 윗](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="43849-147">[Tweets from @Microsoft/MS\_Consumer\_Bands](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="search"></a><span data-ttu-id="43849-148">검색</span><span class="sxs-lookup"><span data-stu-id="43849-148">Search</span></span>

<span data-ttu-id="43849-149">[&quot;#asp .net&quot;에 대 한 트 윗](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="43849-149">[Tweets about &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>
