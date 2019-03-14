---
ms.openlocfilehash: 476580d4bc2435f73ef37c5344ab7fea4b67b9b8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57032500"
---
<span data-ttu-id="d2607-101">다음 명령을 실행하여 HTTPS 개발 인증서를 신뢰합니다.</span><span class="sxs-lookup"><span data-stu-id="d2607-101">Trust the HTTPS development certificate by running the following command:</span></span>

```console
dotnet dev-certs https --trust
```

<span data-ttu-id="d2607-102">이전 명령으로 인해 다음 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2607-102">The preceding command displays the following dialog:</span></span>

![보안 경고 대화 상자](~/getting-started/_static/cert.png)

<span data-ttu-id="d2607-104">개발 인증서를 신뢰하는 데 동의하는 경우 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2607-104">Select **Yes** if you agree to trust the development certificate.</span></span>

<span data-ttu-id="d2607-105">자세한 내용은 [ASP.NET Core HTTPS 개발 인증서 신뢰](xref:security/enforcing-ssl#trust-the-aspnet-core-https-development-certificate-on-windows-and-macos)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2607-105">See [Trust the ASP.NET Core HTTPS development certificate](xref:security/enforcing-ssl#trust-the-aspnet-core-https-development-certificate-on-windows-and-macos) for more information.</span></span>