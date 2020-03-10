---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: ASP.NET 웹 페이지 (Razor) 사이트에서 자산 묶음 및 축소 | Microsoft Docs
author: microsoft
description: 번들 및 축소는 사이트를 더 빠르게 만드는 방법입니다. 묶음을 사용 하면 여러 JavaScript (.js) 파일이 나 여러 css 스타일 시트를 결합할 수 있습니다.
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 5e42111ad71ec65581e56c73822e23ecd5fcbd58
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516179"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="c9b94-104">ASP.NET 웹 페이지(Razor) 사이트에서 자산 묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="c9b94-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="c9b94-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="c9b94-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c9b94-106">번들 및 축소는 사이트를 더 빠르게 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b94-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="c9b94-107">묶음을 사용 하면 여러 JavaScript ( *.js*) 파일이 나 여러 개의 css 스타일 시트 파일 ( *.css*)을 결합 하 여 한 번에 하나의 단위로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b94-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="c9b94-108">축소 squeezes 다른 유형의 압축을 수행 하 여 다운로드 한 파일을 가능한 한 작게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9b94-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="c9b94-109">필요한 요소를 포함 하는 패키지를 Microsoft WebMatrix에서 아직 사용할 수 없기 때문에 ASP.NET 웹 페이지 2의 RC 릴리스는 묶음 및 축소를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b94-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="c9b94-110">불편을 끼쳐드려 죄송합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b94-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="c9b94-111">패키지는 ASP.NET 웹 페이지 2 및 WebMatrix 2의 최종 릴리스에서 제공 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b94-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
