---
uid: webhooks/diagnostics/logging
title: ASP.NET 웹 후크 로깅 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크에 로그인 하는 방법입니다.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: a05b32c4a8f9577bcf6170bd19a9e440b1aeb75b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457585"
---
# <a name="aspnet-webhooks-logging"></a><span data-ttu-id="f6f96-103">ASP.NET 웹 후크 로깅</span><span class="sxs-lookup"><span data-stu-id="f6f96-103">ASP.NET WebHooks logging</span></span>

<span data-ttu-id="f6f96-104">Microsoft ASP.NET 웹 후크는 문제 및 문제를 보고 하는 방법으로 로깅을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f96-104">Microsoft ASP.NET WebHooks uses logging as a way of reporting issues and problems.</span></span> <span data-ttu-id="f6f96-105">기본적으로 로그는 다른 로그 스트림과 마찬가지로 [추적 수신기](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) 를 사용 하 여 관리 되 수 있는 [system.web. trace](https://msdn.microsoft.com/library/system.diagnostics.trace) 를 사용 하 여 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f96-105">By default logs are written using [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) where they can be manged using [Trace Listeners](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) like any other log stream.</span></span>

<span data-ttu-id="f6f96-106">웹 응용 프로그램을 Azure 웹 앱으로 배포할 때 로그가 자동으로 선택 되 고 다른 [시스템 진단과](https://msdn.microsoft.com/library/system.diagnostics.trace) 함께 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f96-106">When deploying your Web Application as an Azure Web App, the logs are automatically picked up and can be managed together with any other [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) logging.</span></span> <span data-ttu-id="f6f96-107">자세한 내용은 [Azure App Service에서 웹 앱에 대 한 진단 로깅 사용](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f6f96-107">For details, please see [Enable diagnostics logging for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span></span>

<span data-ttu-id="f6f96-108">또한 visual studio를 [사용 하 여 Azure App Service에서 웹 앱 문제 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)에 설명 된 대로 visual studio 내에서 직접 로그를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f96-108">In addition, logs can be obtained straight from inside Visual Studio as described in [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="redirecting-logs"></a><span data-ttu-id="f6f96-109">로그 리디렉션</span><span class="sxs-lookup"><span data-stu-id="f6f96-109">Redirecting Logs</span></span>

<span data-ttu-id="f6f96-110">[Log4Net](http://logging.apache.org/log4net/) 및 [nlog](http://nlog-project.org/)와 같이 [로그를 기록](https://msdn.microsoft.com/library/system.diagnostics.trace)하는 데 사용할 수 있는 대체 로깅 구현을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f96-110">Instead of writing logs to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace), it is possible to provide an alternate logging implementation that can log directly to a log manager such as [Log4Net](http://logging.apache.org/log4net/) and [NLog](http://nlog-project.org/).</span></span> <span data-ttu-id="f6f96-111">[ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) 의 구현을 제공 하 고 사용자가 선택한 종속성 주입 엔진에 등록 하기만 하면 웹 후크가 Microsoft ASP.NET 하 여 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6f96-111">Simply provide an implementation of [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) and register it with a dependency injection engine of your choice and it will get picked up by Microsoft ASP.NET WebHooks.</span></span> <span data-ttu-id="f6f96-112">자세한 내용은 [ASP.NET Web API 2에서 종속성 주입](https://www.asp.net/web-api/overview/advanced/dependency-injection) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f6f96-112">Please see [Dependency Injection in ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) for details.</span></span>
