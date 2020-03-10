---
uid: signalr/overview/older-versions/hub-authorization
title: SignalR 허브에 대 한 인증 및 권한 부여 (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: 이 항목에서는 허브 메서드에 액세스할 수 있는 사용자 또는 역할을 제한 하는 방법에 대해 설명 합니다.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8182677c8931f060d98d17008b16ad545bee4e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450041"
---
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a><span data-ttu-id="78d47-103">SignalR 허브에 대한 인증 및 권한 부여(SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="78d47-103">Authentication and Authorization for SignalR Hubs (SignalR 1.x)</span></span>

<span data-ttu-id="78d47-104">[Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="78d47-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="78d47-105">이 항목에서는 허브 메서드에 액세스할 수 있는 사용자 또는 역할을 제한 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-105">This topic describes how to restrict which users or roles can access hub methods.</span></span>

## <a name="overview"></a><span data-ttu-id="78d47-106">개요</span><span class="sxs-lookup"><span data-stu-id="78d47-106">Overview</span></span>

<span data-ttu-id="78d47-107">이 항목에는 다음과 같은 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="78d47-108">권한 부여 특성</span><span class="sxs-lookup"><span data-stu-id="78d47-108">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="78d47-109">모든 허브에 대 한 인증 필요</span><span class="sxs-lookup"><span data-stu-id="78d47-109">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="78d47-110">사용자 지정 된 권한 부여</span><span class="sxs-lookup"><span data-stu-id="78d47-110">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="78d47-111">클라이언트에 인증 정보 전달</span><span class="sxs-lookup"><span data-stu-id="78d47-111">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="78d47-112">.NET 클라이언트에 대 한 인증 옵션</span><span class="sxs-lookup"><span data-stu-id="78d47-112">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="78d47-113">폼 인증을 사용 하는 쿠키</span><span class="sxs-lookup"><span data-stu-id="78d47-113">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="78d47-114">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="78d47-114">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="78d47-115">연결 헤더</span><span class="sxs-lookup"><span data-stu-id="78d47-115">Connection header</span></span>](#header)
    - [<span data-ttu-id="78d47-116">MSSQLSERVER에 대한 프로토콜 속성</span><span class="sxs-lookup"><span data-stu-id="78d47-116">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="78d47-117">권한 부여 특성</span><span class="sxs-lookup"><span data-stu-id="78d47-117">Authorize attribute</span></span>

<span data-ttu-id="78d47-118">SignalR는 허브 또는 메서드에 대 한 액세스 권한이 있는 사용자 또는 역할을 지정 하는 [권한 부여](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 특성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-118">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="78d47-119">이 특성은 `Microsoft.AspNet.SignalR` 네임 스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-119">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="78d47-120">허브 또는 허브의 특정 메서드에 `Authorize` 특성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-120">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="78d47-121">`Authorize` 특성을 허브 클래스에 적용 하면 지정 된 권한 부여 요구 사항이 허브의 모든 메서드에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-121">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="78d47-122">적용할 수 있는 다양 한 유형의 권한 부여 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-122">The different types of authorization requirements that you can apply are shown below.</span></span> <span data-ttu-id="78d47-123">`Authorize` 특성이 없으면 허브에 연결 된 클라이언트에서 허브의 모든 공용 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-123">Without the `Authorize` attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span>

<span data-ttu-id="78d47-124">웹 응용 프로그램에서 "Admin" 이라는 역할을 정의한 경우 해당 역할의 사용자만 다음 코드를 사용 하 여 허브에 액세스할 수 있도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-124">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="78d47-125">또는 아래와 같이 허브에 모든 사용자가 사용할 수 있는 하나의 메서드와 인증 된 사용자만 사용할 수 있는 두 번째 메서드를 포함 하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-125">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="78d47-126">다음 예에서는 다양 한 권한 부여 시나리오를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-126">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="78d47-127">`[Authorize]` – 인증 된 사용자만</span><span class="sxs-lookup"><span data-stu-id="78d47-127">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="78d47-128">`[Authorize(Roles = "Admin,Manager")]` – 지정 된 역할의 인증 된 사용자만</span><span class="sxs-lookup"><span data-stu-id="78d47-128">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="78d47-129">`[Authorize(Users = "user1,user2")]` – 지정 된 사용자 이름의 인증 된 사용자만</span><span class="sxs-lookup"><span data-stu-id="78d47-129">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="78d47-130">`[Authorize(RequireOutgoing=false)]` – 인증 된 사용자만 허브를 호출할 수 있지만, 서버에서 클라이언트로의 호출은 특정 사용자만 메시지를 보낼 수 있지만 다른 모든 사용자는 메시지를 받을 수 있는 경우와 같은 권한 부여로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-130">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="78d47-131">RequireOutgoing 속성은 허브 내의 개별 메서드가 아니라 전체 허브에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-131">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="78d47-132">RequireOutgoing가 false로 설정 되지 않은 경우 권한 부여 요구 사항을 충족 하는 사용자만 서버에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-132">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="78d47-133">모든 허브에 대 한 인증 필요</span><span class="sxs-lookup"><span data-stu-id="78d47-133">Require authentication for all hubs</span></span>

<span data-ttu-id="78d47-134">응용 프로그램을 시작할 때 [Requireauthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) 메서드를 호출 하 여 응용 프로그램의 모든 허브 및 허브 메서드에 대 한 인증을 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-134">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="78d47-135">여러 허브가 있고 모든 허브에 대 한 인증 요구 사항을 적용 하려는 경우이 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-135">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="78d47-136">이 방법을 사용 하면 역할, 사용자 또는 나가는 권한 부여를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-136">With this method, you cannot specify role, user, or outgoing authorization.</span></span> <span data-ttu-id="78d47-137">허브 메서드에 대 한 액세스는 인증 된 사용자로만 제한 되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-137">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="78d47-138">그러나 허브 또는 메서드에 권한 부여 특성을 적용 하 여 추가 요구 사항을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-138">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="78d47-139">특성에 지정 하는 요구 사항은 인증의 기본 요구 사항 외에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-139">Any requirement you specify in attributes is applied in addition to the basic requirement of authentication.</span></span>

<span data-ttu-id="78d47-140">다음 예제에서는 모든 허브 메서드를 인증 된 사용자로 제한 하는 global.asax 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-140">The following example shows a Global.asax file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="78d47-141">SignalR 요청이 처리 된 후에 `RequireAuthentication()` 메서드를 호출 하면 SignalR에서 `InvalidOperationException` 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-141">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="78d47-142">이 예외는 파이프라인이 호출 된 후 모듈을 HubPipeline에 추가할 수 없기 때문에 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-142">This exception is thrown because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="78d47-143">앞의 예제에서는 첫 번째 요청을 처리 하기 전에 한 번 실행 되는 `Application_Start` 메서드에서 `RequireAuthentication` 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-143">The previous example shows calling the `RequireAuthentication` method in the `Application_Start` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="78d47-144">사용자 지정 된 권한 부여</span><span class="sxs-lookup"><span data-stu-id="78d47-144">Customized authorization</span></span>

<span data-ttu-id="78d47-145">권한 부여가 결정 되는 방법을 사용자 지정 해야 하는 경우 `AuthorizeAttribute`에서 파생 되는 클래스를 만들고 [userauthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) 메서드를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-145">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="78d47-146">이 메서드는 요청을 완료할 수 있는 권한이 사용자에 게 있는지 여부를 확인 하기 위해 각 요청에 대해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-146">This method is called for each request to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="78d47-147">재정의 된 메서드에서 권한 부여 시나리오에 필요한 논리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-147">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="78d47-148">다음 예제에서는 클레임 기반 id를 통해 권한 부여를 적용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-148">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="78d47-149">클라이언트에 인증 정보 전달</span><span class="sxs-lookup"><span data-stu-id="78d47-149">Pass authentication information to clients</span></span>

<span data-ttu-id="78d47-150">클라이언트에서 실행 되는 코드에서 인증 정보를 사용 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-150">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="78d47-151">클라이언트에서 메서드를 호출할 때 필요한 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-151">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="78d47-152">예를 들어 채팅 응용 프로그램 메서드는 아래와 같이 메시지를 게시 하는 사람의 사용자 이름을 매개 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-152">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="78d47-153">또는 아래와 같이 인증 정보를 표시 하 고 해당 개체를 매개 변수로 전달 하는 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-153">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="78d47-154">악의적인 사용자가 해당 클라이언트의 요청을 모방 하는 데 사용할 수 있으므로 한 클라이언트의 연결 id를 다른 클라이언트에 전달 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-154">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="78d47-155">.NET 클라이언트에 대 한 인증 옵션</span><span class="sxs-lookup"><span data-stu-id="78d47-155">Authentication options for .NET clients</span></span>

<span data-ttu-id="78d47-156">인증 된 사용자로 제한 되는 허브와 상호 작용 하는 콘솔 앱과 같은 .NET 클라이언트가 있는 경우 쿠키, 연결 헤더 또는 인증서에서 인증 자격 증명을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-156">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="78d47-157">이 섹션의 예에서는 사용자를 인증 하는 다른 방법을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-157">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="78d47-158">완전 한 기능을 갖춘 SignalR 앱은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-158">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="78d47-159">SignalR를 사용 하는 .NET 클라이언트에 대 한 자세한 내용은 [허브 API 가이드-.Net 클라이언트](../guide-to-the-api/hubs-api-guide-net-client.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="78d47-159">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="78d47-160">쿠키</span><span class="sxs-lookup"><span data-stu-id="78d47-160">Cookie</span></span>

<span data-ttu-id="78d47-161">.NET 클라이언트가 ASP.NET Forms 인증을 사용 하는 허브와 상호 작용 하는 경우 연결에서 인증 쿠키를 수동으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-161">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="78d47-162">[HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) 개체의 `CookieContainer` 속성에 쿠키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-162">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="78d47-163">다음 예제에서는 웹 페이지에서 인증 쿠키를 검색 하 고 해당 쿠키를 연결에 추가 하는 콘솔 앱을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-163">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span> <span data-ttu-id="78d47-164">예제의 URL `https://www.contoso.com/RemoteLogin`은 만들어야 하는 웹 페이지를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-164">The URL `https://www.contoso.com/RemoteLogin` in the example points to a web page that you would need to create.</span></span> <span data-ttu-id="78d47-165">페이지는 게시 된 사용자 이름과 암호를 검색 하 고 자격 증명을 사용 하 여 사용자에 게 로그인을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-165">The page would retrieve the posted user name and password, and attempt to log in the user with the credentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="78d47-166">콘솔 앱은 다음 코드 숨김이 포함 된 빈 페이지를 참조할 수 있는 www.contoso.com/RemoteLogin에 자격 증명을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-166">The console app posts the credentials to www.contoso.com/RemoteLogin which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="78d47-167">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="78d47-167">Windows authentication</span></span>

<span data-ttu-id="78d47-168">Windows 인증을 사용 하는 경우 [defaultcredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) 속성을 사용 하 여 현재 사용자의 자격 증명을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-168">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="78d47-169">연결에 대 한 자격 증명을 DefaultCredentials의 값으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-169">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="78d47-170">연결 헤더</span><span class="sxs-lookup"><span data-stu-id="78d47-170">Connection header</span></span>

<span data-ttu-id="78d47-171">응용 프로그램에서 쿠키를 사용 하지 않는 경우 연결 헤더에 사용자 정보를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-171">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="78d47-172">예를 들어 연결 헤더에 토큰을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-172">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="78d47-173">그런 다음 허브에서 사용자의 토큰을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-173">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="78d47-174">인증서</span><span class="sxs-lookup"><span data-stu-id="78d47-174">Certificate</span></span>

<span data-ttu-id="78d47-175">클라이언트 인증서를 전달 하 여 사용자를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-175">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="78d47-176">연결을 만들 때 인증서를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-176">You add the certificate when creating the connection.</span></span> <span data-ttu-id="78d47-177">다음 예제에서는 연결에 클라이언트 인증서를 추가 하는 방법만 보여 줍니다. 전체 콘솔 앱은 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-177">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="78d47-178">이 클래스는 인증서를 만드는 여러 가지 방법을 제공 하는 [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d47-178">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
