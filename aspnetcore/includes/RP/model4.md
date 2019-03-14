---
ms.openlocfilehash: 5ed24cd8a7e880a496d0c0295f7c1fb07f0e1032
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035990"
---
<span data-ttu-id="51d70-101">다음 표에서는 ASP.NET Core 코드 생성기 매개 변수를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="51d70-101">The following table details the ASP.NET Core code generator parameters:</span></span>

| <span data-ttu-id="51d70-102">매개 변수</span><span class="sxs-lookup"><span data-stu-id="51d70-102">Parameter</span></span>               | <span data-ttu-id="51d70-103">설명</span><span class="sxs-lookup"><span data-stu-id="51d70-103">Description</span></span>|
| ----------------- | ------------ |
| <span data-ttu-id="51d70-104">-m</span><span class="sxs-lookup"><span data-stu-id="51d70-104">-m</span></span>  | <span data-ttu-id="51d70-105">모델의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="51d70-105">The name of the model.</span></span> |
| <span data-ttu-id="51d70-106">-dc</span><span class="sxs-lookup"><span data-stu-id="51d70-106">-dc</span></span>  | <span data-ttu-id="51d70-107">사용할 `DbContext` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="51d70-107">The `DbContext` class to use.</span></span> |
| <span data-ttu-id="51d70-108">-udl</span><span class="sxs-lookup"><span data-stu-id="51d70-108">-udl</span></span> | <span data-ttu-id="51d70-109">기본 레이아웃을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51d70-109">Use the default layout.</span></span> |
| <span data-ttu-id="51d70-110">-outDir</span><span class="sxs-lookup"><span data-stu-id="51d70-110">-outDir</span></span> | <span data-ttu-id="51d70-111">뷰를 만들기 위한 상태 출력 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="51d70-111">The relative output folder path to create the views.</span></span> |
| <span data-ttu-id="51d70-112">--referenceScriptLibraries</span><span class="sxs-lookup"><span data-stu-id="51d70-112">--referenceScriptLibraries</span></span> | <span data-ttu-id="51d70-113">편집 및 만들기 페이지에 `_ValidationScriptsPartial`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51d70-113">Adds `_ValidationScriptsPartial` to Edit and Create pages</span></span> |

<span data-ttu-id="51d70-114">`h` 스위치를 사용하여 `aspnet-codegenerator razorpage` 명령에 대한 도움말을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d70-114">Use the `h` switch to get help on the `aspnet-codegenerator razorpage` command:</span></span>

```console
dotnet aspnet-codegenerator razorpage -h
```
