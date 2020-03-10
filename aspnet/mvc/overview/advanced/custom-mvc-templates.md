---
uid: mvc/overview/advanced/custom-mvc-templates
title: 사용자 지정 MVC 템플릿 | Microsoft Docs
author: joeloff
description: 템플릿을 VSIX 확장으로 만듭니다.
ms.author: riande
ms.date: 12/10/2012
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 0603bc24e070e223551813f66a75889a2e46fd35
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499601"
---
# <a name="custom-mvc-template"></a>사용자 지정 MVC 템플릿

[Jacques Eloff](https://github.com/joeloff)

Visual Studio 2010에 대 한 MVC 3 Tools 업데이트 릴리스에는 MVC 프로젝트에 대 한 별도의 프로젝트 마법사가 도입 되었습니다. 변경 내용은 두 가지 요소에 의해 결정 되었습니다. 먼저 MVC 3의 새로운 템플릿이 도입 되었으며 Razor와 같은 추가 뷰 엔진을 지원 하 여 Visual Studio의 새 프로젝트 대화 상자를 overcrowding. 둘째, 고객은 확장성을 요청 하 고 새 MVC 프로젝트 마법사에서 이러한 요청에 응답할 수 있습니다.

사용자 지정 템플릿 추가는 레지스트리를 사용 하 여 MVC 프로젝트 마법사에 새 템플릿을 표시 하는 데 사용 되는 단절 프로세스 였습니다. 새 템플릿의 작성자는 설치 시 필요한 레지스트리 항목을 만들 수 있도록 MSI 내에이를 래핑합니다. 대신, 사용 가능한 템플릿을 포함 하는 ZIP 파일을 만들고 최종 사용자가 필요한 레지스트리 항목을 직접 만들 수 있습니다.

앞서 언급 한 방법은 모두 적절 하지 않으므로 [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) 확장에서 제공 하는 기존 인프라 중 일부를 활용 하 여 Visual Studio 2012에 대 한 mvc 4부터 사용자 지정 mvc 템플릿을 더 쉽게 작성 하 고 배포 하 고 설치할 수 있도록 결정 했습니다. 이 방법에서 제공 하는 몇 가지 이점은 다음과 같습니다.

- VSIX 확장에는 여러 언어 (C# 및 Visual Basic)와 여러 개의 뷰 엔진 (ASPX 및 Razor)을 지 원하는 여러 템플릿이 포함 될 수 있습니다.
- VSIX 확장은 Express Sku를 비롯 한 여러 Sku의 Visual Studio를 대상으로 할 수 있습니다.
- [Visual Studio 갤러리](https://visualstudiogallery.msdn.microsoft.com/) 는 광범위 한 대상에 확장을 배포 하는 데 도움이 됩니다.
- VSIX 확장을 업그레이드 하 여 사용자 지정 템플릿에 대 한 수정 및 업데이트를 더 쉽게 작성할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

- 사용자는 .vstemplate 파일 등에 필요한 태그를 포함 하 여 프로젝트 템플릿 제작에 대해 잘 알고 있어야 합니다.
- 사용자는 Visual Studio Professional 이상 버전이 설치 되어 있어야 합니다. Express Sku는 VSIX 프로젝트 만들기를 지원 하지 않습니다.
- [Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) 가 설치 되었습니다.

## <a name="example"></a>예제

첫 번째 단계는 C# 또는 Visual Basic를 사용 하 여 새 VSIX 프로젝트를 만드는 것입니다. **파일 > 새 프로젝트**를 선택 하 고 왼쪽 창에서 **확장성** 을 클릭 한 다음 **VSIX 프로젝트**를 선택 합니다.

![새 프로젝트](custom-mvc-templates/_static/image1.jpg)

프로젝트를 만든 후 VSIX 디자이너가 열립니다.

![프로젝트 디자이너 메타 데이터](custom-mvc-templates/_static/image2.jpg)

디자이너를 사용 하 여 확장을 설치 하거나 Visual Studio에서 설치 된 확장 (**도구 > 확장 및 업데이트**)을 찾아볼 때 사용자에 게 표시 되는 확장의 일반 속성 중 일부를 편집할 수 있습니다. 일반 정보를 완료 한 후에는 **설치 대상 탭**을 클릭 합니다.

![프로젝트 디자이너 설치 대상](custom-mvc-templates/_static/image3.jpg)

이 탭은 확장에서 지원 되는 Visual Studio의 Sku 및 버전을 지정 하는 데 사용 됩니다. **모든 사용자가** vsix의 컴퓨터별 설치를 사용 하도록 설정 하려면이 vsix에 대 한 확인란을 선택 합니다. 오른쪽에 있는 **새로 만들기** 단추를 클릭 하 여 VWD (Web Developer Express)와 같은 sku를 추가 합니다.

![새 설치 대상 추가](custom-mvc-templates/_static/image4.jpg)

Professional, Premium 및 Ultimate를 모두 지원 하려는 경우에는 **Microsoft.VisualStudio.Pro**제품군에서 최소 sku를 선택 하기만 하면 됩니다. 설치 대상을 완료 한 후 모든 변경 내용을 저장 해야 합니다.

![프로젝트 디자이너 설치 대상](custom-mvc-templates/_static/image5.jpg)

**자산** 탭은 VSIX에 모든 콘텐츠 파일을 추가 하는 데 사용 됩니다. MVC에는 사용자 지정 메타 데이터가 필요 하므로 **자산** 탭을 사용 하 여 콘텐츠를 추가 하는 대신 VSIX 매니페스트 파일의 원시 XML을 편집 하 게 됩니다. 먼저 VSIX 프로젝트에 템플릿 콘텐츠를 추가 합니다. 폴더와 콘텐츠의 구조가 프로젝트의 레이아웃을 반영 하는 것이 중요 합니다. 아래 예제에는 기본 MVC 프로젝트 템플릿에서 파생 된 네 개의 프로젝트 템플릿이 포함 되어 있습니다. 프로젝트 템플릿 (ProjectTemplates 폴더 아래의 모든 항목)을 구성 하는 모든 파일이 VSIX 프로젝트 파일의 **콘텐츠** itemgroup에 추가 되 고 아래 예제와 같이 각 항목에 **CopyToOutputDirectory** 및 **IncludeInVsix** 메타 데이터 집합이 포함 되어 있는지 확인 합니다.

&lt;Content는 =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;

&lt;CopyToOutputDirectory&gt;항상&lt;/CopyToOutputDirectory&gt;

&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;

&lt;/콘텐츠&gt;

그렇지 않으면 VSIX를 빌드할 때 IDE에서 템플릿의 내용을 컴파일하려고 시도 하므로 오류가 표시 될 수 있습니다. 템플릿의 코드 파일에는 프로젝트 템플릿이 인스턴스화되어 IDE에서 컴파일할 수 없는 경우 Visual Studio에서 사용 하는 특수 [템플릿 매개 변수가](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) 포함 되어 있는 경우가 많습니다.

![솔루션 탐색기](custom-mvc-templates/_static/image6.jpg)

VSIX 디자이너를 닫은 다음 **솔루션 탐색기** 에서 **소스 확장명 .manifest** 파일을 마우스 오른쪽 단추로 클릭 하 고 **연결 프로그램** 을 선택 하 고 **XML (텍스트) 편집기** 옵션을 선택 합니다.

![연결 프로그램 대화 상자](custom-mvc-templates/_static/image7.jpg)

**&lt;자산&gt;** 요소를 만들고 VSIX에 포함 되어야 하는 각 파일에 대 한 **&lt;Asset&gt;** 요소를 추가 합니다. 각 **&lt;Asset&gt;** 요소의 **Type** 특성은 **VisualStudio**로 설정 해야 합니다. MVC 프로젝트 마법사 에서만 이해 하는 사용자 지정 네임 스페이스입니다. 매니페스트 파일의 구조와 레이아웃에 대 한 자세한 내용은 VSIX 2.0 스키마 설명서를 참조 하세요.

VSIX에 파일을 추가 하는 것 만으로는 MVC 마법사를 사용 하 여 템플릿을 등록할 수 없습니다. MVC 마법사에 템플릿 이름, 설명, 지원 되는 뷰 엔진 및 프로그래밍 언어와 같은 정보를 제공 해야 합니다. 이 정보는 각 **.vstemplate** 파일에 대 한 **&lt;Asset&gt;** 요소와 연결 된 사용자 지정 특성으로 전달 됩니다.

&lt;Asset d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;

=&quot;VisualStudio를 입력&quot;

d:Source =&quot;파일&quot;

경로 =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;

ProjectType =&quot;MVC&quot;

Language =&quot;C#&quot;

ViewEngine =&quot;Aspx&quot;

TemplateId =&quot;MyMvcApplication&quot;

Title =&quot;사용자 지정 기본 웹 응용 프로그램&quot;

Description = 기본 MVC 웹 응용 프로그램 (Razor)에서 파생 된 사용자 지정 템플릿을&quot;&quot;

Version =&quot;4.0&quot;/&gt;

다음은 표시 해야 하는 사용자 지정 특성에 대 한 설명입니다.

- **ProjectType** 는 MVC로 설정 되어야 합니다.
- **Language** 는 템플릿에서 지 원하는 개발 언어를 지정 합니다. 유효한 값은 C# 또는 VB입니다.
- **Viewengine** 은 Aspx 또는 Razor와 같이 템플릿에서 지원 되는 뷰 엔진을 지정 합니다. 이 필드에 대 한 사용자 지정 값을 지정할 수 있습니다.
- **TemplateId** 는 템플릿을 그룹화 하는 데 사용 됩니다. 값이 기존 템플릿 ID와 일치 하는 경우 이전에 MVC 마법사에 등록 된 템플릿이 재정의 됩니다.
- **제목** 각 프로젝트 템플릿 아래에서 MVC 마법사에 표시 되는 간단한 설명을 지정 합니다.
- **설명** 템플릿에 대 한 보다 자세한 설명을 지정 합니다.

모든 파일을 매니페스트에 추가 하 고 저장 한 후에는 디자이너의 **자산** 탭에 모든 파일이 표시 되지만, **.vstemplate** 파일에 대 한 **&lt;자산&gt;** 요소에 추가한 사용자 지정 특성은 표시 되지 않습니다.

![프로젝트 디자이너 자산](custom-mvc-templates/_static/image8.jpg)

이제 VSIX 프로젝트를 컴파일하여 설치 하면 됩니다.

VSIX 확장을 테스트 하려는 컴퓨터에서 Visual Studio의 모든 인스턴스가 닫혀 있는지 확인 합니다. Visual Studio는 시작 하는 동안 새 확장을 검색 하므로 VSIX를 설치 하는 동안 IDE가 열려 있으면 Visual Studio를 다시 시작 해야 합니다. 탐색기에서 vsix 파일을 두 번 클릭 하 여 **Vsix 설치 관리자**를 시작 하 고 **설치** 를 클릭 한 다음 Visual Studio를 시작 합니다.

![VSIX 설치 관리자](custom-mvc-templates/_static/image9.jpg)

메뉴에서 **도구 > 확장 및 업데이트** 를 선택 하 여 확장이 설치 되었는지 확인 합니다. 확장을 설치 하는 동안 VSIX 설치 관리자에서 오류를 보고 한 경우 VSIX 설치 관리자 로그에서 자세한 내용을 확인할 수 있습니다. 일반적으로 로그는 확장을 설치한 사용자의 **% temp%** 폴더에 생성 됩니다 (예: **C:\Users\Bob\AppData\Local\Temp**).

![확장 및 업데이트](custom-mvc-templates/_static/image10.jpg)

창을 닫은 후 mvc 4 프로젝트를 만들어 새 템플릿이 MVC 마법사에 표시 되는지 여부를 확인할 수 있습니다.

![새 ASP.NET MVC 4 프로젝트](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a>제한 사항

1. MVC 마법사는 지역화 된 사용자 지정 템플릿을 지원 하지 않습니다.
2. 사용자 지정 템플릿을 찾지 못하면 마법사에서 오류를 보고 하지 않습니다. 필요한 사용자 지정 특성 중 하나가 없는 경우 템플릿은 마법사에서 제외 됩니다.
