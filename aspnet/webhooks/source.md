---
uid: webhooks/source
title: ASP.NET WebHooks 원본 코드 및 NuGet 패키지 | Microsoft Docs
author: rick-anderson
description: ASP.NET WebHooks 소스 코드 및 NuGet 패키지에 대 한 링크
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513911"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET WebHooks 소스 코드 및 NuGet 패키지

Microsoft ASP.NET 웹 후크는 Microsoft ASP.NET 된 모듈 패밀리의 일부 이며 [GitHub에서 오픈 소스 프로젝트로](https://github.com/aspnet/WebHooks)호스팅됩니다. 즉, 기여를 수락 하지만 끌어오기 요청을 제출 하기 전에 [기여 지침](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) 을 확인 하세요.

지금 읽고 있는이 온라인 설명서는 [GitHub에서 오픈 소스로](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) 도 호스트 되며 기여도 수락 합니다.

## <a name="nuget-packages"></a>NuGet 패키지

[NuGet 패키지](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) 는 다음 세 부분으로 구분 됩니다.

* [Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 발신자와 수신자 간에 공유 되는 공통 패키지입니다.

* [발신자](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 다른 사용자에 게 자체 webhook를 보내는 것을 지 원하는 패키지 집합입니다. Webhook 전송에 대 한 기능은 [웹 후크 전송](sending/senders.md)에 자세히 설명 되어 있습니다.

* [수신자](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): 다른 사용자 로부터 웹 후크를 수신 하는 것을 지 원하는 패키지 집합입니다. 웹 후크를 수신 하는 기능은 [웹 후크 수신](receiving/index.md)에 자세히 설명 되어 있습니다.
