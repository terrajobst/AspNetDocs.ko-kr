---
ms.openlocfilehash: 568fa161b27e554fd8b474670b8f9a7ec2f39f45
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047130"
---
<span data-ttu-id="dc0b7-101">다음 표에서는 ASP.NET Core 코드 생성기 매개 변수를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0b7-101">The following table details the ASP.NET Core code generator parameters:</span></span>

| <span data-ttu-id="dc0b7-102">매개 변수</span><span class="sxs-lookup"><span data-stu-id="dc0b7-102">Parameter</span></span>               | <span data-ttu-id="dc0b7-103">설명</span><span class="sxs-lookup"><span data-stu-id="dc0b7-103">Description</span></span>|
| ----------------- | ------------ |
| <span data-ttu-id="dc0b7-104">-m</span><span class="sxs-lookup"><span data-stu-id="dc0b7-104">-m</span></span>  | <span data-ttu-id="dc0b7-105">모델의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0b7-105">The name of the model.</span></span> |
| <span data-ttu-id="dc0b7-106">-dc</span><span class="sxs-lookup"><span data-stu-id="dc0b7-106">-dc</span></span>  | <span data-ttu-id="dc0b7-107">데이터 컨텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0b7-107">The data context.</span></span> |
| <span data-ttu-id="dc0b7-108">-udl</span><span class="sxs-lookup"><span data-stu-id="dc0b7-108">-udl</span></span> | <span data-ttu-id="dc0b7-109">기본 레이아웃을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0b7-109">Use the default layout.</span></span> |
| <span data-ttu-id="dc0b7-110">--relativeFolderPath</span><span class="sxs-lookup"><span data-stu-id="dc0b7-110">--relativeFolderPath</span></span> | <span data-ttu-id="dc0b7-111">뷰를 만들기 위한 상태 출력 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0b7-111">The relative output folder path to create the views.</span></span> |
| <span data-ttu-id="dc0b7-112">--useDefaultLayout</span><span class="sxs-lookup"><span data-stu-id="dc0b7-112">--useDefaultLayout</span></span> | <span data-ttu-id="dc0b7-113">보기에는 기본 레이아웃을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0b7-113">The default layout should be used for the views.</span></span> |
| <span data-ttu-id="dc0b7-114">--referenceScriptLibraries</span><span class="sxs-lookup"><span data-stu-id="dc0b7-114">--referenceScriptLibraries</span></span> | <span data-ttu-id="dc0b7-115">편집 및 만들기 페이지에 `_ValidationScriptsPartial`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0b7-115">Adds `_ValidationScriptsPartial` to Edit and Create pages</span></span> |

<span data-ttu-id="dc0b7-116">`h` 스위치를 사용하여 `aspnet-codegenerator controller` 명령에 대한 도움말을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0b7-116">Use the `h` switch to get help on the `aspnet-codegenerator controller` command:</span></span>

```console
dotnet aspnet-codegenerator controller -h
```