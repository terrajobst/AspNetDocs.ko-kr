---
uid: webhooks/source
title: ASP.NET WebHooks 원본 코드 및 NuGet 패키지 | Microsoft Docs
author: rick-anderson
description: ASP.NET WebHooks 소스 코드 및 NuGet 패키지에 대 한 링크
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000711"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="33a94-103">ASP.NET WebHooks 소스 코드 및 NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="33a94-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="33a94-104">Microsoft ASP.NET 웹 후크는 Microsoft ASP.NET 된 모듈 패밀리의 일부 이며 [GitHub에서 오픈 소스 프로젝트로](https://github.com/aspnet/WebHooks)호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="33a94-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="33a94-105">즉, 기여를 수락 하지만 끌어오기 요청을 제출 하기 전에 [기여 지침](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) 을 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="33a94-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="33a94-106">지금 읽고 있는이 온라인 설명서는 [GitHub에서 오픈 소스로](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) 도 호스트 되며 기여도 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="33a94-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="33a94-107">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="33a94-107">NuGet packages</span></span>

<span data-ttu-id="33a94-108">[NuGet 패키지](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) 는 다음 세 부분으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33a94-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="33a94-109">[일반](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 발신자와 수신자 간에 공유 되는 공통 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="33a94-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="33a94-110">[보낸 사람](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 다른 사용자에 게 고유한 웹 후크를 보내는 것을 지 원하는 패키지 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="33a94-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="33a94-111">Webhook 전송에 대 한 기능은 [웹 후크 전송](sending/senders.md)에 자세히 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a94-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="33a94-112">[수신자](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): 다른 사용자 로부터 웹 후크를 수신 하는 것을 지 원하는 패키지 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="33a94-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="33a94-113">웹 후크를 수신 하는 기능은 [웹 후크 수신](receiving/index.md)에 자세히 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33a94-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
