---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'ASP.NET Web API에서 HTML 양식 데이터 보내기: 파일 업로드 및 Multipart MIME-ASP.NET 4.x'
author: MikeWasson
description: 이 자습서에서는 web API에 파일을 업로드 하는 방법을 보여 줍니다. 또한 다중 파트 MIME 데이터를 처리 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449213"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="3a286-104">ASP.NET Web API에서 HTML 양식 데이터 보내기: 파일 업로드 및 다중 파트 MIME</span><span class="sxs-lookup"><span data-stu-id="3a286-104">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>

<span data-ttu-id="3a286-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3a286-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="3a286-106">2 부: 파일 업로드 및 다중 파트 MIME</span><span class="sxs-lookup"><span data-stu-id="3a286-106">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="3a286-107">이 자습서에서는 web API에 파일을 업로드 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-107">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="3a286-108">또한 다중 파트 MIME 데이터를 처리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-108">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="3a286-109">[완료 된 프로젝트를 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-109">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>

<span data-ttu-id="3a286-110">다음은 파일을 업로드 하는 HTML 형식의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-110">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="3a286-111">이 폼에는 텍스트 입력 컨트롤과 파일 입력 컨트롤이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-111">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="3a286-112">양식에 파일 입력 컨트롤이 포함 되어 있는 경우 **enctype** 특성은 항상 다중 파트/폼 데이터&quot;&quot;해야 하며,이는 양식이 다중 파트 MIME 메시지로 전송 됨을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-112">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="3a286-113">다중 파트 MIME 메시지의 형식은 예제 요청을 살펴보면 이해 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-113">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="3a286-114">이 메시지는 각 폼 컨트롤에 대해 하나씩 두 *부분*으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-114">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="3a286-115">부분 경계는 대시로 시작 하는 선으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-115">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="3a286-116">부분 경계는 임의의 구성 요소 (&quot;41184676334&quot;)를 포함 하 여 경계 문자열이 메시지 파트 내에 실수로 표시 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-116">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>

<span data-ttu-id="3a286-117">각 메시지 파트에는 하나 이상의 헤더와 파트 내용이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-117">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="3a286-118">콘텐츠 처리 헤더에는 컨트롤 이름이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-118">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="3a286-119">파일의 경우 파일 이름도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-119">For files, it also contains the file name.</span></span>
- <span data-ttu-id="3a286-120">Content-type 헤더는 파트의 데이터를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-120">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="3a286-121">이 헤더를 생략 하면 기본값은 text/일반입니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-121">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="3a286-122">이전 예제에서 사용자는 content 형식이 image/jpeg; 인 GrandCanyon 라는 파일을 업로드 했습니다. 텍스트 입력 값은 여름 휴가&quot;&quot;되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-122">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="3a286-123">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="3a286-123">File Upload</span></span>

<span data-ttu-id="3a286-124">이제 다중 파트 MIME 메시지에서 파일을 읽는 Web API 컨트롤러를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-124">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="3a286-125">그러면 컨트롤러에서 파일을 비동기적으로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-125">The controller will read the files asynchronously.</span></span> <span data-ttu-id="3a286-126">Web API는 [작업 기반 프로그래밍 모델](https://msdn.microsoft.com/library/dd460693.aspx)을 사용 하 여 비동기 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-126">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="3a286-127">먼저 **async** 및 **wait** 키워드를 지 원하는 .NET Framework 4.5를 대상으로 하는 경우 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-127">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="3a286-128">컨트롤러 작업은 매개 변수를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-128">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="3a286-129">미디어 형식 포맷터를 호출 하지 않고 작업 내에서 요청 본문을 처리 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-129">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="3a286-130">**Ismultipartcontent** 메서드는 요청에 다중 파트 MIME 메시지가 포함 되어 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-130">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="3a286-131">그렇지 않으면 컨트롤러는 HTTP 상태 코드 415 (지원 되지 않는 미디어 형식)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-131">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="3a286-132">**Multipartformdatastreamprovider** 클래스는 업로드 된 파일에 대 한 파일 스트림을 할당 하는 도우미 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-132">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="3a286-133">다중 파트 MIME 메시지를 읽으려면 **ReadAsMultipartAsync** 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-133">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="3a286-134">이 메서드는 모든 메시지 파트를 추출 하 여 **Multipartformdatastreamprovider**에서 제공 하는 스트림에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-134">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="3a286-135">메서드가 완료 되 면 **Multipartfiledata** 개체의 컬렉션인 **filedata** 속성에서 파일에 대 한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-135">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="3a286-136">**Multipartfiledata. FileName** 은 파일을 저장 한 서버의 로컬 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-136">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="3a286-137">**Multipartfiledata. 헤더** 는 파트 헤더 (요청 헤더*아님* )를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-137">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="3a286-138">이를 사용 하 여 콘텐츠\_처리 및 콘텐츠 형식 헤더에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-138">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="3a286-139">이름에서 알 수 있듯이 **ReadAsMultipartAsync** 는 비동기 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-139">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="3a286-140">메서드가 완료 된 후 작업을 수행 하려면 [연속 작업](https://msdn.microsoft.com/library/ee372288.aspx) (.net 4.0) 또는 **wait** 키워드 (.net 4.5)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-140">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="3a286-141">이전 코드의 .NET Framework 4.0 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-141">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="3a286-142">양식 컨트롤 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="3a286-142">Reading Form Control Data</span></span>

<span data-ttu-id="3a286-143">앞에서 살펴본 HTML 폼에는 텍스트 입력 컨트롤이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-143">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="3a286-144">**Multipartformdatastreamprovider**의 **formdata** 속성에서 컨트롤의 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-144">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="3a286-145">**Formdata** 는 폼 컨트롤에 대 한 이름/값 쌍을 포함 하는 **NameValueCollection** 입니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-145">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="3a286-146">컬렉션에 중복 키가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-146">The collection can contain duplicate keys.</span></span> <span data-ttu-id="3a286-147">다음 형식을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-147">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="3a286-148">요청 본문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-148">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="3a286-149">이 경우 **Formdata** 컬렉션에는 다음과 같은 키/값 쌍이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a286-149">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="3a286-150">트립: 왕복</span><span class="sxs-lookup"><span data-stu-id="3a286-150">trip: round-trip</span></span>
- <span data-ttu-id="3a286-151">옵션: 비 중지</span><span class="sxs-lookup"><span data-stu-id="3a286-151">options: nonstop</span></span>
- <span data-ttu-id="3a286-152">옵션: 날짜</span><span class="sxs-lookup"><span data-stu-id="3a286-152">options: dates</span></span>
- <span data-ttu-id="3a286-153">좌석: 창</span><span class="sxs-lookup"><span data-stu-id="3a286-153">seat: window</span></span>
