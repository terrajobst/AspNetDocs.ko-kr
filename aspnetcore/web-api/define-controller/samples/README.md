---
ms.openlocfilehash: b6f39dd0dedb38961eb021cde355f7ec83283195
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024870"
---
# <a name="aspnet-core-web-api-controller-sample"></a><span data-ttu-id="eb700-101">ASP.NET Core Web API 컨트롤러 샘플</span><span class="sxs-lookup"><span data-stu-id="eb700-101">ASP.NET Core Web API Controller Sample</span></span>

<span data-ttu-id="eb700-102">이 샘플 앱은 다음 프로젝트로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb700-102">This sample app consists of the following projects:</span></span>

- <span data-ttu-id="eb700-103">\**WebApiSample.Api.22*: .NET Core 2.2를 대상으로 하는 ASP.NET Core 2.2 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="eb700-103">\**WebApiSample.Api.22*: An ASP.NET Core 2.2 project targeting .NET Core 2.2.</span></span>
- <span data-ttu-id="eb700-104">**WebApiSample.Api.21**: .NET Core 2.1을 대상으로 하는 ASP.NET Core 2.1 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="eb700-104">**WebApiSample.Api.21**: An ASP.NET Core 2.1 project targeting .NET Core 2.1.</span></span>
- <span data-ttu-id="eb700-105">**WebApiSample.Api.Pre21**: .NET Core 2.0을 대상으로 하는 ASP.NET Core 2.0 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="eb700-105">**WebApiSample.Api.Pre21**: An ASP.NET Core 2.0 project targeting .NET Core 2.0.</span></span>
- <span data-ttu-id="eb700-106">**WebApiSample.DataAccess**: Web API 2 프로젝트에 대 한 데이터 액세스 계층으로 제공 하는.NET Standard 2.0 클래스 라이브러리.</span><span class="sxs-lookup"><span data-stu-id="eb700-106">**WebApiSample.DataAccess**: A .NET Standard 2.0 class library serving as a data access tier for the 2 Web API projects.</span></span>

<span data-ttu-id="eb700-107">이 샘플에서는 다양한 Web API 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb700-107">This sample illustrates variations of Web API controller creation:</span></span>

- [<span data-ttu-id="eb700-108">ControllerBase에서 클래스 파생</span><span class="sxs-lookup"><span data-stu-id="eb700-108">Derive class from ControllerBase</span></span>](https://docs.microsoft.com/aspnet/core/web-api#derive-class-from-controllerbase)
- [<span data-ttu-id="eb700-109">ApiControllerAttribute로 클래스에 주석 달기</span><span class="sxs-lookup"><span data-stu-id="eb700-109">Annotate class with ApiControllerAttribute</span></span>](https://docs.microsoft.com/aspnet/core/web-api#annotate-class-with-apicontrollerattribute)
