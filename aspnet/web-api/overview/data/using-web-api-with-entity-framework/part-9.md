---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: 데이터베이스에 새 항목 추가 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448973"
---
# <a name="add-a-new-item-to-the-database"></a><span data-ttu-id="9a6a3-102">데이터베이스에 새 항목 추가</span><span class="sxs-lookup"><span data-stu-id="9a6a3-102">Add a New Item to the Database</span></span>

<span data-ttu-id="9a6a3-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9a6a3-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="9a6a3-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="9a6a3-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="9a6a3-105">이 섹션에서는 사용자가 새 책을 만드는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="9a6a3-106">Node.js에서 뷰 모델에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="9a6a3-107">Index cshtml에서 다음 태그를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="9a6a3-108">다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="9a6a3-109">이 태그는 새 작성자를 제출 하기 위한 폼을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="9a6a3-110">Author 드롭다운 목록의 값은 뷰 모델에서 관찰 가능한 `authors`에 대 한 데이터 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="9a6a3-111">다른 양식 입력의 경우 값은 뷰 모델의 `newBook` 속성에 데이터 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="9a6a3-112">양식의 제출 처리기는 `addBook` 함수에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="9a6a3-113">`addBook` 함수는 데이터 바인딩된 양식 입력의 현재 값을 읽어 JSON 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="9a6a3-114">그런 다음 `/api/books`에 JSON 개체를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9a6a3-115">[이전](part-8.md)
> [다음](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="9a6a3-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
