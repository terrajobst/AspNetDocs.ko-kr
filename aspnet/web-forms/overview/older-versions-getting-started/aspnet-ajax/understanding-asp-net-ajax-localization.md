---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: ASP.NET AJAX 지역화 이해 | Microsoft Docs
author: scottcate
description: 지역화는 특정 언어와 문화권에 대 한 지원을 디자인 하 고 응용 프로그램 또는 응용 프로그램 구성 요소에 통합 하는 프로세스입니다. Mic ...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 003e7939accd7a68dab97441b3d999bca835b85a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78456629"
---
# <a name="understanding-aspnet-ajax-localization"></a>ASP.NET AJAX 지역화 이해

[Scott cate cda (](https://github.com/scottcate)

[PDF 다운로드](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> 지역화는 특정 언어와 문화권에 대 한 지원을 디자인 하 고 응용 프로그램 또는 응용 프로그램 구성 요소에 통합 하는 프로세스입니다. Microsoft ASP.NET 플랫폼은 표준 .NET 지역화 모델을 통합 하 여 표준 ASP.NET 응용 프로그램의 지역화에 대 한 광범위 한 지원을 제공 합니다. Microsoft AJAX 프레임 워크는 지역화를 수행할 수 있는 다양 한 시나리오를 지원 하기 위해 통합 모델을 활용 합니다.

## <a name="introduction"></a>소개

Microsoft의 ASP.NET 기술은 개체 지향 및 이벤트 구동 프로그래밍 모델을 제공 하 고 컴파일된 코드의 장점을 결합 합니다. 그러나 해당 서버 쪽 처리 모델에는 기술에서 내재 된 몇 가지 단점이 있습니다 .이 중 상당수는 Microsoft AJAX 서비스를 캡슐화 하는 System.web. Extensions 네임 스페이스에 포함 된 새로운 기능을 통해 해결할 수 있습니다 .NET Framework 3.5. 이러한 확장은 이전에 ASP.NET 2.0 AJAX 확장의 일부로 사용할 수 있지만 이제 프레임 워크 기본 클래스 라이브러리의 일부로 제공 되는 다양 한 리치 클라이언트 기능을 사용 하도록 설정 합니다. 이 네임 스페이스의 컨트롤 및 기능에는 전체 페이지를 새로 고치지 않고도 페이지를 부분적으로 렌더링 하 고, 클라이언트 스크립트 (ASP.NET 프로 파일링 API 포함)를 통해 웹 서비스에 액세스 하는 기능을 포함 하 고, 다양 한 클라이언트 쪽 API를 사용 하 여 ASP.NET 서버측 컨트롤 집합에 표시 되는 컨트롤 스키마입니다.

이 백서에서는 Microsoft AJAX 프레임 워크 및 Microsoft AJAX 스크립트 라이브러리에 있는 지역화 기능을 검토 합니다. 지역화 지원에 대 한 비즈니스 요구 사항 및 웹의 지역화에 대 한 이미 통합 된 지원 검토를 검토 합니다. .NET Framework에서 제공 하는 응용 프로그램입니다. Microsoft AJAX 스크립트 라이브러리는 이미 .NET 응용 프로그램에서 사용 하는 .resx 파일 형식을 활용 합니다 .이 파일은 통합 된 IDE 지원과 공유 가능한 리소스 형식을 제공 합니다.

이 백서는 Microsoft Visual Studio 2008 베타 2 릴리스를 기반으로 합니다. 또한이 백서에서는 visual Web Developer Express가 아닌 Visual Studio 2008을 사용 하는 것으로 가정 하 고 Visual Studio의 사용자 인터페이스에 따라 연습을 제공 합니다. 일부 코드 샘플은 Visual Web Developer Express에서 사용할 수 없는 프로젝트 템플릿을 활용 합니다.

## <a name="the-need-for-localization"></a>*지역화에 대 한 필요성*

특히 엔터프라이즈 응용 프로그램 개발자 및 구성 요소 개발자는 문화권 및 언어 간의 차이점을 인식 하는 도구를 만드는 기능을 제공 하는 데 많은 도움이 될 것입니다. 클라이언트의 로캘에 맞게 조정 하는 기능을 사용 하 여 구성 요소를 디자인 하면 개발자 생산성이 향상 되 고 구성 요소가 전역적으로 작동 하도록 조정 하는 데 필요한 작업의 양이 줄어듭니다.

지역화는 특정 언어와 문화권에 대 한 지원을 디자인 하 고 응용 프로그램 또는 응용 프로그램 구성 요소에 통합 하는 프로세스입니다. Microsoft ASP.NET 플랫폼은 표준 .NET 지역화 모델을 통합 하 여 표준 ASP.NET 응용 프로그램의 지역화에 대 한 광범위 한 지원을 제공 합니다. Microsoft AJAX 프레임 워크는 지역화를 수행할 수 있는 다양 한 시나리오를 지원 하기 위해 통합 모델을 활용 합니다. Microsoft AJAX 프레임 워크를 사용 하 여 스크립트를 위성 어셈블리에 배포 하거나 정적 파일 시스템 구조를 활용 하 여 지역화할 수 있습니다.

## <a name="embedding-scripts-with-satellite-assemblies"></a>*위성 어셈블리를 포함 하는 스크립트 포함*

표준 .NET Framework 지역화 전략과 일치 하며, 리소스는 위성 어셈블리에 포함 될 수 있습니다. 위성 어셈블리는 이진 파일에 포함 된 기존 리소스에 비해 여러 가지 이점을 제공 합니다. 즉, 더 큰 이미지를 업데이트 하지 않고 모든 지역화를 업데이트할 수 있습니다. 추가 지역화는 위성 어셈블리를에 설치 하 여 간단히 배포할 수 있습니다 프로젝트 폴더와 위성 어셈블리는 주 프로젝트 어셈블리를 다시 로드 하지 않고 배포할 수 있습니다. 특히 ASP.NET 프로젝트에서이는 증분 업데이트에 사용 되는 시스템 리소스의 양을 크게 줄일 수 있고 프로덕션 웹 사이트 사용을 최소화 하기 때문에 유용 합니다.

스크립트는 컴파일 시간에 어셈블리에 포함 된 관리 되는 .resx 또는 컴파일된 .resources 파일에 포함 하 여 어셈블리에 포함 됩니다. 그런 다음 어셈블리 수준 특성을 통해 AJAX 런타임 생성 코드를 통해 스크립트 응용 프로그램에서 해당 리소스를 사용할 수 있게 됩니다.

*포함 된 스크립트 파일에 대 한 명명 규칙*

Microsoft AJAX 프레임 워크 스크립트 관리는 스크립트의 배포 및 테스트에 사용할 수 있는 다양 한 옵션을 지원 하며 이러한 옵션을 용이 하 게 하기 위한 지침이 제공 됩니다.

*디버깅을 용이 하 게 하려면:*

릴리스 (프로덕션) 스크립트는 파일 이름에 `.debug` 한정자를 포함 하지 않아야 합니다. 디버깅을 위해 디자인 된 스크립트는 파일 이름에 `.debug`를 포함 해야 합니다.

*지역화를 용이 하 게 하려면:*

중립 문화권 스크립트는 파일 이름에 문화권 식별자를 포함 하면 안 됩니다. 지역화 된 리소스를 포함 하는 스크립트의 경우 파일 이름에 ISO 언어 코드를 지정 해야 합니다. 예를 들어 `es-CO`은 스페인어, 특별구을 나타냅니다.

다음 표에서는 예제에 대 한 파일 명명 규칙을 요약 합니다.

| 파일 이름 | 의미 |
| --- | --- |
| Script.js | 릴리스 버전의 문화권 중립 스크립트입니다. |
| Script.debug.js | 디버그 버전의 문화권 중립 스크립트입니다. |
| Script.en-US.js | 릴리스 버전 영어, 미국 스크립트 |
| Script.debug.es-CO.js | 디버그 버전 스페인어, 특별구 스크립트입니다. |

## <a name="walkthrough-create-an-localized-embedded-script"></a>연습: 지역화 된 포함 스크립트 만들기

*참고:이 연습에서는 Visual Web Developer Express에 클래스 라이브러리 프로젝트용 프로젝트 템플릿이 포함 되어 있지 않으므로 Visual Studio 2008을 사용 해야 합니다.*

1. ASP.NET AJAX Extensions를 통합 하 여 새 웹 사이트 프로젝트를 만듭니다. 솔루션 내에서 LocalizingResources 라는 다른 프로젝트, 클래스 라이브러리 프로젝트를 만듭니다.
2. LocalizingResources 프로젝트와 DeletionResources 및 DeletionResources 라는 .resx 리소스 파일에 VerifyDeletion 라는 Jscript 파일을 추가 합니다. 전자는 문화권 중립 리소스를 포함 합니다. 후자는 스페인어 언어 리소스를 포함 합니다.
3. 다음 코드를 VerifyDeletion에 추가 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

JavaScript Regex 구문에 익숙하지 않은 경우, 단일 슬래시 내의 텍스트 (이전 예제에서는/FILENAME/)는 RegExp 개체를 나타냅니다. MSDN 라이브러리에는 광범위 한 JavaScript 참조가 포함 되어 있으며 JavaScript 네이티브 개체에 대 한 리소스는 온라인으로 찾을 수 있습니다.

1. DeletionResources에 다음 리소스 문자열을 추가 합니다. 

    **Verifydelete**: 파일 이름을 삭제 하 시겠습니까?

    **삭제**됨: 파일 이름이 삭제 되었습니다.

1. DeletionResources에 다음 리소스 문자열을 추가 합니다. 

    **Verifydelete**: Est seguro 쿼리 DESEE FILENAME을 참조 하십시오.

    **삭제 됨**: 파일 이름 se ha quitado.
2. AssemblyInfo 파일에 다음 코드 줄을 추가 합니다.

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. LocalizingResources 프로젝트에 대 한 참조를 System.web 및 System.web에 추가 합니다.
2. 웹 사이트 프로젝트에서 LocalizingResources 프로젝트에 대 한 참조를 추가 합니다.
3. Default.aspx의 웹 사이트 프로젝트 아래에서 다음 추가 태그로 ScriptManager 컨트롤을 업데이트 합니다.

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. Default.aspx에서 페이지의 아무 곳에 나이 태그를 포함 합니다.

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. F5 키를 누릅니다. 메시지가 표시 되 면 디버깅을 사용 하도록 설정 합니다. 페이지가 로드 되 면 삭제 단추를 누릅니다. 확인을 위해 컴퓨터에서 기본적으로 스페인어 언어 리소스를 선호 하도록 설정 하지 않은 경우 영어로 표시 됩니다.
2. 브라우저 창을 닫고 default.aspx로 돌아갑니다. @Page 헤더 지시문에서 auto for Culture 및 UICulture를 es로 바꿉니다. F5 키를 다시 눌러 브라우저에서 웹 응용 프로그램을 다시 시작 합니다. 이번에는 스페인어에서 파일을 삭제 하 라는 메시지가 표시 됩니다.

[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-localization/_static/image3.png))

[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-localization/_static/image6.png))

이 연습에서는 몇 가지 변형이 있습니다. 예를 들어 스크립트는 페이지를 로드 하는 동안 프로그래밍 방식으로 ScriptManager 컨트롤에 등록 될 수 있습니다.

## <a name="including-a-static-script-file-structure"></a>*정적 스크립트 파일 구조 포함*

배포에 정적 스크립트 파일을 사용 하는 경우 기본적인 .NET 지역화 체계를 사용 하는 경우의 몇 가지 이점이 손실 됩니다. 주로 표시 되는 스크립트 리소스 파일을 포함 하 여 자동으로 생성 된 형식이 손실 되는 것입니다. 예를 들어 위의 연습에서 리소스는 ScriptManager 컨트롤의 Message 라는 자동으로 생성 된 형식에 의해 노출 되었습니다.

그러나 정적 스크립트 파일 구조를 사용 하는 경우 몇 가지 이점이 있습니다. 위성 어셈블리를 다시 컴파일하거나 다시 배포 하지 않고도 업데이트를 수행할 수 있으며, 정적 파일 구조를 사용 하 여 포함 스크립트를 재정의 하 여 구성 요소와 함께 제공 되지 않을 수 있는 일부 기능을 통합할 수도 있습니다.

프로젝트를 컴파일하는 동안 스크립트 리소스를 자동으로 생성 하 여 버전 제어 문제를 방지 하는 것이 좋습니다. 광범위 한 스크립트 코드 베이스를 유지 관리 하는 경우 코드 변경 내용이 지역화 된 각 스크립트에 반영 되도록 하는 데 점점 더 어려워질 수 있습니다. 또는 프로젝트를 빌드하는 동안 파일을 병합 하 여 하나의 논리 스크립트와 여러 지역화 스크립트를 간단 하 게 유지 관리할 수 있습니다.

선언적으로 포함할 리소스가 없으므로 정적 스크립트 파일은 ScriptManager 컨트롤의 `<Scripts>` 태그의 자식으로 `<asp:ScriptElement>` 요소를 추가 하거나 런타임에 페이지에서 `ScriptManager` 컨트롤의 `Scripts` 속성에 `ScriptReference` 개체를 프로그래밍 방식으로 추가 하 여 참조 해야 합니다.

## <a name="the-scriptmanager-and-its-role-in-localization"></a>*지역화의 ScriptManager 및 해당 역할*

ScriptManager는 지역화 된 응용 프로그램에 대해 여러 가지 자동 동작을 사용 하도록 설정 합니다.

- 설정 및 명명 규칙에 따라 스크립트 파일을 자동으로 찾습니다. 예를 들어 디버깅 모드에서 디버그 사용 스크립트를 로드 하 고 브라우저의 사용자 인터페이스 선택에 따라 지역화 된 스크립트를 로드 합니다.
- 사용자 지정 문화권을 포함 하 여 문화권을 정의할 수 있습니다.
- HTTP를 통해 스크립트 파일을 압축할 수 있습니다.
- 스크립트를 캐시 하 여 많은 요청을 효율적으로 관리 합니다.
- 암호화 된 URL을 통해 파이프 하 여 스크립트에 간접 참조 계층을 추가 합니다.

스크립트 참조는 프로그래밍 방식으로 또는 선언적 태그를 통해 ScriptManager 컨트롤에 추가할 수 있습니다. 선언 태그는 웹 사이트 프로젝트 자체 이외의 어셈블리에 포함 된 스크립트를 사용할 때 특히 유용 합니다. 수정이 푸시 될 때 스크립트 이름이 변경 되지 않기 때문입니다.

## <a name="summary"></a>요약

웹 응용 프로그램이 성장 함에 도달 하면 더 광범위 한 문화와 커뮤니티에 도달할 수 있는 필요성이 비즈니스 모델의 핵심이 됩니다. 전자 상거래 웹 응용 프로그램은 외부 통화를 처리할 수 있어야 하 고, 콘텐츠 관리 시스템은 콘텐츠를 제공할 뿐만 아니라 다른 언어의 탐색 힌트와 양식 필드를 제공할 수 있어야 하며, 회사에서이 요구 사항을 알아야 합니다. 액세스할 수.

.NET Framework는 위성 어셈블리 및 XML 리소스 (.resx) 파일을 활용 하 여 리소스 문자열 및 이미지를 조회 하는 일관 된 방법을 제공 하는 풍부한 지역화 프레임 워크를 기본적으로 지원 합니다. Microsoft AJAX Framework 및 Microsoft AJAX 스크립트 라이브러리를 비롯 한 ASP.NET AJAX 확장은이 프로그래밍 모델을 클라이언트 쪽 코드에 대 한 지원을 제공 하 여 쉽게 리소스 문자열을 조회할 수 있도록 합니다. 위성 어셈블리는 파일 이름이 지정 된 명명 체계를 따르는 한 스크립트 리소스 (실제 .js 파일)를 ScriptResource. 이러한 지원을 통해 ASP.NET AJAX 확장은 스크립트와 응용 프로그램의 세계화를 단순화 합니다.

## <a name="bio"></a>*약력*

Scott Cate cda (는 1997부터 Microsoft 웹 기술을 사용 하 고 있으며 기술 자료 소프트웨어 솔루션에 초점을 맞춘 ASP.NET 기반 응용 프로그램을 전문적으로 작성 하는[www.myKB.com](http://www.myKB.com)(myKB.com)의 부사장입니다. Scott은 [scott.cate@myKB.com](mailto:scott.cate@myKB.com) 또는 [ScottCate.com](http://ScottCate.com) 의 블로그의 전자 메일을 통해 연락할 수 있습니다.

> [!div class="step-by-step"]
> [이전](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
> [다음](understanding-asp-net-ajax-web-services.md)
