---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: 데이터 전송 개체 만들기 (Dto) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445761"
---
# <a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="ca850-102">DTO(데이터 전송 개체) 만들기</span><span class="sxs-lookup"><span data-stu-id="ca850-102">Create Data Transfer Objects (DTOs)</span></span>

<span data-ttu-id="ca850-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ca850-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ca850-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="ca850-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="ca850-105">이제 web API는 데이터베이스 엔터티를 클라이언트에 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="ca850-106">클라이언트는 데이터베이스 테이블에 직접 매핑되는 데이터를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="ca850-107">그러나 이것이 항상 좋은 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-107">However, that's not always a good idea.</span></span> <span data-ttu-id="ca850-108">클라이언트에 보내는 데이터의 셰이프를 변경 하려는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="ca850-109">예를 들어, 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-109">For example, you might want to:</span></span>

- <span data-ttu-id="ca850-110">순환 참조를 제거 합니다 (이전 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="ca850-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="ca850-111">클라이언트가 볼 수 없는 특정 속성을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="ca850-112">페이로드 크기를 줄이기 위해 일부 속성을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="ca850-113">중첩 된 개체를 포함 하는 개체 그래프를 결합 하 여 클라이언트에 보다 편리 하 게 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="ca850-114">"과도 한 게시" 취약성을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="ca850-115">(오버 게시에 대 한 설명은 [모델 유효성 검사](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) 를 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="ca850-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="ca850-116">데이터베이스 계층에서 서비스 계층을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="ca850-117">이를 위해 DTO ( *데이터 전송 개체* )를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="ca850-118">DTO는 네트워크를 통해 데이터를 전송 하는 방법을 정의 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="ca850-119">설명서 엔터티를 사용 하 여 작동 하는 방식을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="ca850-120">모델 폴더에서 다음 두 개의 DTO 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="ca850-121">`BookDetailDto` 클래스에는 책 모델의 모든 속성이 포함 되어 있습니다. 단, `AuthorName`는 작성자 이름을 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-121">The `BookDetailDto` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="ca850-122">`BookDto` 클래스는 `BookDetailDto`속성의 하위 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-122">The `BookDto` class contains a subset of properties from `BookDetailDto`.</span></span>

<span data-ttu-id="ca850-123">다음으로 `BooksController` 클래스에서 두 개의 GET 메서드를 Dto를 반환 하는 버전으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="ca850-124">LINQ **Select** 문을 사용 하 여 Book 엔터티에서 dto로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="ca850-125">새 `GetBooks` 메서드에서 생성 된 SQL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="ca850-126">EF가 LINQ **select** 를 SQL select 문으로 변환 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="ca850-127">마지막으로 `PostBook` 메서드를 수정 하 여 DTO를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="ca850-128">이 자습서에서는 코드에서 수동으로 Dto로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="ca850-129">또 다른 옵션은 변환을 자동으로 처리 하는 [Automapper](http://automapper.org/) 와 같은 라이브러리를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ca850-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="ca850-130">[이전](part-4.md)
> [다음](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="ca850-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
