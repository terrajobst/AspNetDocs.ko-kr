---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: .NET 클라이언트에서 OData 서비스 호출 (C#) | Microsoft Docs
author: MikeWasson
description: 이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다. 자습서 Visual Studio 2013에서 사용 되는 소프트웨어 버전 (Visual S와 함께 작동 ...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600373"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a><span data-ttu-id="d7124-104">.NET 클라이언트에서 OData 서비스 호출(C#)</span><span class="sxs-lookup"><span data-stu-id="d7124-104">Calling an OData Service From a .NET Client (C#)</span></span>

<span data-ttu-id="d7124-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d7124-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="d7124-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="d7124-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="d7124-107">이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-107">This tutorial shows how to call an OData service from a C# client application.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d7124-108">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="d7124-108">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="d7124-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (Visual Studio 2012에서 작동)</span><span class="sxs-lookup"><span data-stu-id="d7124-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (works with Visual Studio 2012)</span></span>
> - [<span data-ttu-id="d7124-110">WCF Data Services 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d7124-110">WCF Data Services Client Library</span></span>](https://msdn.microsoft.com/library/cc668772.aspx)
> - <span data-ttu-id="d7124-111">Web API 2.</span><span class="sxs-lookup"><span data-stu-id="d7124-111">Web API 2.</span></span> <span data-ttu-id="d7124-112">예제 OData 서비스는 Web API 2를 사용 하 여 작성 되지만 클라이언트 응용 프로그램은 Web API에 의존 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-112">(The example OData service is built using Web API 2, but the client application does not depend on Web API.)</span></span>

<span data-ttu-id="d7124-113">이 자습서에서는 OData 서비스를 호출 하는 클라이언트 응용 프로그램을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-113">In this tutorial, I'll walk through creating a client application that calls an OData service.</span></span> <span data-ttu-id="d7124-114">OData 서비스는 다음 엔터티를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-114">The OData service exposes the following entities:</span></span>

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

<span data-ttu-id="d7124-115">다음 문서에서는 Web API에서 OData 서비스를 구현 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-115">The following articles describe how to implement the OData service in Web API.</span></span> <span data-ttu-id="d7124-116">그러나이 자습서를 이해 하기 위해 읽을 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-116">(You don't need to read them to understand this tutorial, however.)</span></span>

- [<span data-ttu-id="d7124-117">Web API 2에서 OData 엔드포인트 만들기</span><span class="sxs-lookup"><span data-stu-id="d7124-117">Creating an OData Endpoint in Web API 2</span></span>](creating-an-odata-endpoint.md)
- [<span data-ttu-id="d7124-118">Web API 2의 OData 엔터티 관계</span><span class="sxs-lookup"><span data-stu-id="d7124-118">OData Entity Relations in Web API 2</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="d7124-119">Web API 2의 OData 작업</span><span class="sxs-lookup"><span data-stu-id="d7124-119">OData Actions in Web API 2</span></span>](odata-actions.md)

## <a name="generate-the-service-proxy"></a><span data-ttu-id="d7124-120">서비스 프록시를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-120">Generate the Service Proxy</span></span>

<span data-ttu-id="d7124-121">첫 번째 단계는 서비스 프록시를 생성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-121">The first step is to generate a service proxy.</span></span> <span data-ttu-id="d7124-122">서비스 프록시는 OData 서비스에 액세스 하기 위한 메서드를 정의 하는 .NET 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-122">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="d7124-123">프록시는 메서드 호출을 HTTP 요청으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-123">The proxy translates method calls into HTTP requests.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

<span data-ttu-id="d7124-124">Visual Studio에서 OData 서비스 프로젝트를 열어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-124">Start by opening the OData service project in Visual Studio.</span></span> <span data-ttu-id="d7124-125">IIS Express에서 로컬로 서비스를 실행 하려면 CTRL + F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-125">Press CTRL+F5 to run the service locally in IIS Express.</span></span> <span data-ttu-id="d7124-126">Visual Studio에서 할당 하는 포트 번호를 포함 하 여 로컬 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-126">Note the local address, including the port number that Visual Studio assigns.</span></span> <span data-ttu-id="d7124-127">프록시를 만들 때이 주소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-127">You will need this address when you create the proxy.</span></span>

<span data-ttu-id="d7124-128">그런 다음 Visual Studio의 다른 인스턴스를 열고 콘솔 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-128">Next, open another instance of Visual Studio and create a console application project.</span></span> <span data-ttu-id="d7124-129">콘솔 응용 프로그램은 OData 클라이언트 응용 프로그램이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-129">The console application will be our OData client application.</span></span> <span data-ttu-id="d7124-130">(서비스와 동일한 솔루션에 프로젝트를 추가할 수도 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="d7124-130">(You can also add the project to the same solution as the service.)</span></span>

> [!NOTE]
> <span data-ttu-id="d7124-131">나머지 단계는 콘솔 프로젝트를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-131">The remaining steps refer the console project.</span></span>

<span data-ttu-id="d7124-132">솔루션 탐색기에서 **참조** 를 마우스 오른쪽 단추로 클릭 하 고 **서비스 참조 추가**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-132">In Solution Explorer, right-click **References** and select **Add Service Reference**.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

<span data-ttu-id="d7124-133">**서비스 참조 추가** 대화 상자에서 OData 서비스의 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-133">In the **Add Service Reference** dialog, type the address of the OData service:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

<span data-ttu-id="d7124-134">여기서 *port* 는 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-134">where *port* is the port number.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

<span data-ttu-id="d7124-135">**네임 스페이스**에 "제품 서비스"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-135">For **Namespace**, type "ProductService".</span></span> <span data-ttu-id="d7124-136">이 옵션은 프록시 클래스의 네임 스페이스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-136">This option defines the namespace of the proxy class.</span></span>

<span data-ttu-id="d7124-137">**찾기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-137">Click **Go**.</span></span> <span data-ttu-id="d7124-138">Visual Studio는 OData 메타 데이터 문서를 읽어 서비스의 엔터티를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-138">Visual Studio reads the OData metadata document to discover the entities in the service.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

<span data-ttu-id="d7124-139">**확인** 을 클릭 하 여 프록시 클래스를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-139">Click **OK** to add the proxy class to your project.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a><span data-ttu-id="d7124-140">서비스 프록시 클래스의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-140">Create an Instance of the Service Proxy Class</span></span>

<span data-ttu-id="d7124-141">`Main` 메서드 내에서 다음과 같이 프록시 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-141">Inside your `Main` method, create a new instance of the proxy class, as follows:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

<span data-ttu-id="d7124-142">서비스를 실행 하는 실제 포트 번호를 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-142">Again, use the actual port number where your service is running.</span></span> <span data-ttu-id="d7124-143">서비스를 배포 하는 경우 라이브 서비스의 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-143">When you deploy your service, you will use the URI of the live service.</span></span> <span data-ttu-id="d7124-144">프록시를 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-144">You don't need to update the proxy.</span></span>

<span data-ttu-id="d7124-145">다음 코드에서는 요청 Uri를 콘솔 창에 출력 하는 이벤트 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-145">The following code adds an event handler that prints the request URIs to the console window.</span></span> <span data-ttu-id="d7124-146">이 단계는 필요 하지 않지만 각 쿼리에 대 한 Uri를 확인 하는 것이 흥미롭습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-146">This step isn't required, but it's interesting to see the URIs for each query.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a><span data-ttu-id="d7124-147">서비스 쿼리</span><span class="sxs-lookup"><span data-stu-id="d7124-147">Query the Service</span></span>

<span data-ttu-id="d7124-148">다음 코드는 OData 서비스에서 제품 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-148">The following code gets the list of products from the OData service.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

<span data-ttu-id="d7124-149">HTTP 요청을 보내거나 응답을 구문 분석 하는 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-149">Notice that you don't need to write any code to send the HTTP request or parse the response.</span></span> <span data-ttu-id="d7124-150">프록시 클래스는 **foreach** 루프에서 `Container.Products` 컬렉션을 열거할 때이를 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-150">The proxy class does this automatically when you enumerate the `Container.Products` collection in the **foreach** loop.</span></span>

<span data-ttu-id="d7124-151">응용 프로그램을 실행 하는 경우 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-151">When you run the application, the output should look like the following:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

<span data-ttu-id="d7124-152">ID로 엔터티를 가져오려면 `where` 절을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-152">To get an entity by ID, use a `where` clause.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

<span data-ttu-id="d7124-153">이 항목의 나머지 부분에서는 서비스를 호출 하는 데 필요한 코드를 비롯 하 여 전체 `Main` 함수를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-153">For the rest of this topic, I won't show the entire `Main` function, just the code needed to call the service.</span></span>

## <a name="apply-query-options"></a><span data-ttu-id="d7124-154">쿼리 옵션 적용</span><span class="sxs-lookup"><span data-stu-id="d7124-154">Apply Query Options</span></span>

<span data-ttu-id="d7124-155">OData는 필터링, 정렬, 페이지 데이터 등에 사용할 수 있는 [쿼리 옵션](../supporting-odata-query-options.md) 을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-155">OData defines [query options](../supporting-odata-query-options.md) that can be used to filter, sort, page data, and so forth.</span></span> <span data-ttu-id="d7124-156">서비스 프록시에서 다양 한 LINQ 식을 사용 하 여 이러한 옵션을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-156">In the service proxy, you can apply these options by using various LINQ expressions.</span></span>

<span data-ttu-id="d7124-157">이 섹션에서는 간단한 예를 보여 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-157">In this section, I'll show brief examples.</span></span> <span data-ttu-id="d7124-158">자세한 내용은 MSDN의 [LINQ 고려 사항 (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d7124-158">For more details, see the topic [LINQ Considerations (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) on MSDN.</span></span>

### <a name="filtering-filter"></a><span data-ttu-id="d7124-159">필터링 ($filter)</span><span class="sxs-lookup"><span data-stu-id="d7124-159">Filtering ($filter)</span></span>

<span data-ttu-id="d7124-160">필터링 하려면 `where` 절을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-160">To filter, use a `where` clause.</span></span> <span data-ttu-id="d7124-161">다음 예제에서는 제품 범주별로 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-161">The following example filters by product category.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

<span data-ttu-id="d7124-162">이 코드는 다음 OData 쿼리에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-162">This code corresponds to the following OData query.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

<span data-ttu-id="d7124-163">프록시는 `where` 절을 OData `$filter` 식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-163">Notice that the proxy converts the `where` clause into an OData `$filter` expression.</span></span>

### <a name="sorting-orderby"></a><span data-ttu-id="d7124-164">정렬 ($orderby)</span><span class="sxs-lookup"><span data-stu-id="d7124-164">Sorting ($orderby)</span></span>

<span data-ttu-id="d7124-165">정렬 하려면 `orderby` 절을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-165">To sort, use an `orderby` clause.</span></span> <span data-ttu-id="d7124-166">다음 예에서는 가격을 기준으로 내림차순으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-166">The following example sorts by price, from highest to lowest.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

<span data-ttu-id="d7124-167">해당 OData 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-167">Here is the corresponding OData request.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a><span data-ttu-id="d7124-168">클라이언트 쪽 페이징 ($skip 및 $top)</span><span class="sxs-lookup"><span data-stu-id="d7124-168">Client-Side Paging ($skip and $top)</span></span>

<span data-ttu-id="d7124-169">대량 엔터티 집합의 경우 클라이언트에서 결과 수를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-169">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="d7124-170">예를 들어 클라이언트에는 한 번에 10 개의 항목이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-170">For example, a client might show 10 entries at a time.</span></span> <span data-ttu-id="d7124-171">이를 *클라이언트 쪽 페이징*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-171">This is called *client-side paging*.</span></span> <span data-ttu-id="d7124-172">서버 [쪽 페이징은](../supporting-odata-query-options.md#server-paging)서버에서 결과 수를 제한 하는 역할도 합니다. 클라이언트 쪽 페이징을 수행 하려면 LINQ **Skip** 및 **Take** 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-172">(There is also [server-side paging](../supporting-odata-query-options.md#server-paging), where the server limits the number of results.) To perform client-side paging, use the LINQ **Skip** and **Take** methods.</span></span> <span data-ttu-id="d7124-173">다음 예에서는 첫 번째 40 결과를 건너뛰고 다음 10 개를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-173">The following example skips the first 40 results and takes the next 10.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

<span data-ttu-id="d7124-174">해당 OData 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-174">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a><span data-ttu-id="d7124-175">($Select)를 선택 하 고 확장 ($expand)</span><span class="sxs-lookup"><span data-stu-id="d7124-175">Select ($select) and Expand ($expand)</span></span>

<span data-ttu-id="d7124-176">관련 엔터티를 포함 하려면 `DataServiceQuery<t>.Expand` 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-176">To include related entities, use the `DataServiceQuery<t>.Expand` method.</span></span> <span data-ttu-id="d7124-177">예를 들어 각 `Product`에 대 한 `Supplier`를 포함 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-177">For example, to include the `Supplier` for each `Product`:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

<span data-ttu-id="d7124-178">해당 OData 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-178">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

<span data-ttu-id="d7124-179">응답의 셰이프를 변경 하려면 LINQ **select** 절을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-179">To change the shape of the response, use the LINQ **select** clause.</span></span> <span data-ttu-id="d7124-180">다음 예에서는 각 제품의 이름만 가져오며 다른 속성은 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-180">The following example gets just the name of each product, with no other properties.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

<span data-ttu-id="d7124-181">해당 OData 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-181">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

<span data-ttu-id="d7124-182">Select 절은 관련 엔터티를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-182">A select clause can include related entities.</span></span> <span data-ttu-id="d7124-183">이 경우에는 **확장**을 호출 하지 마십시오. 이 경우 프록시는 자동으로 확장을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-183">In that case, do not call **Expand**; the proxy automatically includes the expansion in this case.</span></span> <span data-ttu-id="d7124-184">다음 예에서는 각 제품의 이름과 공급자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-184">The following example gets the name and supplier of each product.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

<span data-ttu-id="d7124-185">해당 OData 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-185">Here is the corresponding OData request.</span></span> <span data-ttu-id="d7124-186">**$Expand** 옵션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-186">Notice that it includes the **$expand** option.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

<span data-ttu-id="d7124-187">$Select 및 $expand에 대 한 자세한 내용은 [WEB API 2에서 $select, $expand 및 $Value 사용](../using-select-expand-and-value.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d7124-187">For more information about $select and $expand, see [Using $select, $expand, and $value in Web API 2](../using-select-expand-and-value.md).</span></span>

## <a name="add-a-new-entity"></a><span data-ttu-id="d7124-188">새 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="d7124-188">Add a New Entity</span></span>

<span data-ttu-id="d7124-189">엔터티 집합에 새 엔터티를 추가 하려면 `AddToEntitySet`를 호출 합니다. 여기서 *EntitySet* 은 엔터티 집합의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-189">To add a new entity to an entity set, call `AddToEntitySet`, where *EntitySet* is the name of the entity set.</span></span> <span data-ttu-id="d7124-190">예를 들어 `AddToProducts`는 `Products` 엔터티 집합에 새 `Product`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-190">For example, `AddToProducts` adds a new `Product` to the `Products` entity set.</span></span> <span data-ttu-id="d7124-191">프록시를 생성할 때 WCF Data Services는 이러한 강력한 형식의 **AddTo** 메서드를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-191">When you generate the proxy, WCF Data Services automatically creates these strongly-typed **AddTo** methods.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

<span data-ttu-id="d7124-192">두 엔터티 간에 링크를 추가 하려면 **addlink** 및 **setlink** 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-192">To add a link between two entities, use the **AddLink** and **SetLink** methods.</span></span> <span data-ttu-id="d7124-193">다음 코드는 새 공급 업체와 새 제품을 추가한 다음 두 제품 간에 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-193">The following code adds a new supplier and a new product, and then creates links between them.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

<span data-ttu-id="d7124-194">탐색 속성이 컬렉션인 경우 **Addlink** 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-194">Use **AddLink** when the navigation property is a collection.</span></span> <span data-ttu-id="d7124-195">이 예에서는 공급자의 `Products` 컬렉션에 제품을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-195">In this example, we are adding a product to the `Products` collection on the supplier.</span></span>

<span data-ttu-id="d7124-196">탐색 속성이 단일 엔터티인 경우 **Setlink** 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-196">Use **SetLink** when the navigation property is a single entity.</span></span> <span data-ttu-id="d7124-197">이 예에서는 제품의 `Supplier` 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-197">In this example, we are setting the `Supplier` property on the product.</span></span>

## <a name="update--patch"></a><span data-ttu-id="d7124-198">업데이트/패치</span><span class="sxs-lookup"><span data-stu-id="d7124-198">Update / Patch</span></span>

<span data-ttu-id="d7124-199">엔터티를 업데이트 하려면 **Updateobject** 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-199">To update an entity, call the **UpdateObject** method.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

<span data-ttu-id="d7124-200">**SaveChanges**를 호출 하면 업데이트가 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-200">The update is performed when you call **SaveChanges**.</span></span> <span data-ttu-id="d7124-201">기본적으로 WCF는 HTTP MERGE 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-201">By default, WCF sends an HTTP MERGE request.</span></span> <span data-ttu-id="d7124-202">**PatchOnUpdate** 옵션은 HTTP 패치를 보내도록 WCF에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-202">The **PatchOnUpdate** option tells WCF to send an HTTP PATCH instead.</span></span>

> [!NOTE]
> <span data-ttu-id="d7124-203">패치 및 병합 이유</span><span class="sxs-lookup"><span data-stu-id="d7124-203">Why PATCH versus MERGE?</span></span> <span data-ttu-id="d7124-204">원래 HTTP 1.1 사양 ([RCF 2616](http://tools.ietf.org/html/rfc2616))이 "부분 업데이트" 의미 체계를 사용 하 여 http 메서드를 정의 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-204">The original HTTP 1.1 specification ([RCF 2616](http://tools.ietf.org/html/rfc2616)) did not define any HTTP method with "partial update" semantics.</span></span> <span data-ttu-id="d7124-205">부분 업데이트를 지원 하기 위해 OData 사양은 MERGE 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-205">To support partial updates, the OData specification defined the MERGE method.</span></span> <span data-ttu-id="d7124-206">2010에서 [RFC 5789](http://tools.ietf.org/html/rfc5789) 은 부분 업데이트에 대 한 PATCH 메서드를 정의 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-206">In 2010, [RFC 5789](http://tools.ietf.org/html/rfc5789) defined the PATCH method for partial updates.</span></span> <span data-ttu-id="d7124-207">WCF Data Services 블로그의이 [블로그 게시물](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) 에서 일부 기록을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-207">You can read some of the history in this [blog post](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) on the WCF Data Services Blog.</span></span> <span data-ttu-id="d7124-208">현재는 MERGE 보다 패치를 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-208">Today, PATCH is preferred over MERGE.</span></span> <span data-ttu-id="d7124-209">Web API 스 캐 폴딩에서 만든 OData 컨트롤러는 두 가지 방법을 모두 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-209">The OData controller created by the Web API scaffolding supports both methods.</span></span>

<span data-ttu-id="d7124-210">전체 엔터티 (의미 체계 배치)를 대체 하려면 **ReplaceOnUpdate** 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-210">If you want to replace the entire entity (PUT semantics), specify the **ReplaceOnUpdate** option.</span></span> <span data-ttu-id="d7124-211">이렇게 하면 WCF에서 HTTP PUT 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-211">This causes WCF to send an HTTP PUT request.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a><span data-ttu-id="d7124-212">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="d7124-212">Delete an Entity</span></span>

<span data-ttu-id="d7124-213">엔터티를 삭제 하려면 **DeleteObject**를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-213">To delete an entity, call **DeleteObject**.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a><span data-ttu-id="d7124-214">OData 동작 호출</span><span class="sxs-lookup"><span data-stu-id="d7124-214">Invoke an OData Action</span></span>

<span data-ttu-id="d7124-215">OData에서 [작업](odata-actions.md) 은 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되지 않는 서버 쪽 동작을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-215">In OData, [actions](odata-actions.md) are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span>

<span data-ttu-id="d7124-216">OData 메타 데이터 문서에서 작업을 설명 하지만 프록시 클래스에서 해당 작업에 대 한 강력한 형식의 메서드를 만들지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-216">Although the OData metadata document describes the actions, the proxy class does not create any strongly-typed methods for them.</span></span> <span data-ttu-id="d7124-217">제네릭 **Execute** 메서드를 사용 하 여 여전히 OData 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-217">You can still invoke an OData action by using the generic **Execute** method.</span></span> <span data-ttu-id="d7124-218">그러나 매개 변수의 데이터 형식과 반환 값을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-218">However, you will need to know the data types of the parameters and the return value.</span></span>

<span data-ttu-id="d7124-219">예를 들어 `RateProduct` 작업은 `Int32` 형식의 "등급" 이라는 매개 변수를 사용 하 고 `double`을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-219">For example, the `RateProduct` action takes parameter named "Rating" of type `Int32` and returns a `double`.</span></span> <span data-ttu-id="d7124-220">다음 코드에서는이 작업을 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-220">The following code shows how to invoke this action.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

<span data-ttu-id="d7124-221">자세한 내용은[서비스 작업 및 작업 호출](https://msdn.microsoft.com/library/hh230677.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d7124-221">For more information, see[Calling Service Operations and Actions](https://msdn.microsoft.com/library/hh230677.aspx).</span></span>

<span data-ttu-id="d7124-222">한 가지 옵션은 **컨테이너** 클래스를 확장 하 여 동작을 호출 하는 강력한 형식의 메서드를 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d7124-222">One option is to extend the **Container** class to provide a strongly typed method that invokes the action:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
