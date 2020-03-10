---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Visual Studio를 사용 하 여 프로그래밍 ASP.NET 웹 페이지 (Razor) | Microsoft Docs
author: Rick-Anderson
description: 이 부록은 Visual Studio 2010 또는 Visual Web Developer 2010 Express를 사용 하 여 Razor 구문 ASP.NET 웹 페이지를 프로그래밍 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514295"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Visual Studio를 사용 하 여 프로그래밍 ASP.NET 웹 페이지 (Razor)

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Visual Studio 또는 Visual Web Developer Express를 사용 하 여 Razor (ASP.NET 웹 페이지) 웹 사이트를 프로그래밍 하는 방법을 설명 합니다.
>
> 학습할 내용
>
> - Visual Studio 버전에서 ASP.NET 웹 페이지 작업을 수행 하기 위해 필요한 항목 (있는 경우)입니다.
> - Visual Web Developer 2010 Express에 ASP.NET 웹 페이지에 대 한 지원을 추가 하는 방법입니다.
> - Visual Studio의 기능을 사용 하 여 IntelliSense 및 디버거를 비롯 한 ASP.NET Razor 페이지로 작업 하는 방법입니다.
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
>
> - ASP.NET 웹 페이지 (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> 이 자습서는 ASP.NET 웹 페이지 2, Visual Studio 2012, Visual Studio 2010 및 WebMatrix 2에도 적용 됩니다.

WebMatrix 또는 다른 많은 코드 편집기를 사용 하 여 Razor 구문 ASP.NET 웹 페이지를 프로그래밍할 수 있습니다. 모든 기능을 갖춘 IDE (통합 개발 환경) 인 Microsoft Visual Studio를 사용 하 여 웹 사이트 뿐만 아니라 여러 유형의 응용 프로그램을 만들 수 있는 강력한 도구 집합을 제공할 수도 있습니다. ASP.NET Razor 페이지로 작업 하려면 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)을 사용할 수 있습니다.

ASP.NET Razor 웹 페이지를 사용 하 여 프로그래밍 하기 위해 Visual Studio에서 제공 하는 두 가지 특히 유용한 기능은 다음과 같습니다.

- *IntelliSense*. Visual Studio에 기본 제공 되는 IntelliSense 기능은 WebMatrix에서 IntelliSense 보다 더 포괄적입니다.
- *디버거*. 디버거를 사용 하면 실행 중인 프로그램을 중지 하 고, 변수를 검사 하 고, 코드를 한 줄씩 단계별로 실행 하 여 코드 문제를 해결할 수 있습니다.

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>서로 다른 버전의 ASP.NET 웹 페이지에서 Visual Studio 사용

Visual Studio 2017에서 ASP.NET 웹 앱을 개발 하려면 **ASP.NET 및 웹 개발** 워크 로드를 설치 합니다.

Visual Studio 2012 및 Visual Studio 2013에는 ASP.NET 웹 페이지에 대 한 지원이 포함 됩니다. ASP.NET 웹 페이지를 지원 하기 위해 필요한 패키지는 Visual Studio를 설치할 때 설치 됩니다.

Visual Studio 2010는 기본적으로 ASP.NET 웹 페이지에 대 한 지원을 포함 하지 않습니다. Visual Studio 2010에서 ASP.NET 웹 페이지를 사용 하려면 ASP.NET MVC 패키지를 설치 해야 합니다. ASP.NET 웹 페이지 2를 다운로드 하려면 ASP.NET MVC 4를 설치 합니다.

다음 표에는 여러 버전의 Visual Studio에서 ASP.NET 웹 페이지에 대 한 지원이 요약 되어 있습니다.

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET 웹 페이지 2** | ASP.NET MVC 4 설치 | 들어 | 들어 |
| **ASP.NET 웹 페이지 3** |  | NuGet을 통해 ASP.NET 웹 페이지 3으로 업데이트 | 들어 |

Visual Studio 2010을 사용 하려면 [Visual studio 2010에서 ASP.NET 웹 페이지에 대 한 지원 설치](#vs2010support)를 참조 하세요.

## <a name="launching-visual-studio-from-webmatrix"></a>WebMatrix에서 Visual Studio 시작

WebMatrix에서 프로젝트를 시작 하 고 Visual Studio로 전환 하려는 경우 WebMatrix는 Visual Studio에서 프로젝트를 쉽게 열 수 있는 단추를 제공 합니다. 이 단추를 사용 하려면 컴퓨터에 Visual Studio가 설치 되어 있어야 합니다. 다음 이미지는 WebMatrix의 단추를 보여 줍니다.

![Visual Studio 시작](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

단추를 클릭 하면 Visual Studio에서 프로젝트가 열립니다. 문제 없이 WebMatrix와 Visual Studio 간을 전환할 수 있습니다. 다른 환경에서 파일이 변경 된 경우 알림이 표시 되며, 최신 변경 내용을 가져오려면 다시 로드 해야 합니다.

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Visual Studio에서 ASP.NET Razor 사이트 만들기

Visual Studio에서 ASP.NET Razor 웹 사이트를 만들려면 다음을 수행 합니다.

1. Visual Studio를 엽니다.
2. **파일** 메뉴에서 **새 웹 사이트**를 클릭 합니다.

    ![새 웹 사이트 만들기](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. **새 웹 사이트** 대화 상자에서 사용할 언어 (시각적 개체 C# 또는 Visual Basic)를 선택 합니다.
4. **ASP.NET 웹 사이트 (Razor)** 템플릿을 선택 합니다.

    ![razor 사이트](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. **확인**을 클릭합니다.

새 프로젝트가 존재 하 고 시작 하는 데 도움이 되는 몇 가지 기본 웹 페이지로 채워집니다.

### <a name="using-intellisense"></a>IntelliSense 사용

이제 사이트를 만들었으므로 Visual Studio에서 IntelliSense가 작동 하는 방법을 확인할 수 있습니다.

1. 방금 만든 웹 사이트에서 *기본. cshtml* 페이지를 엽니다.
2. 페이지의 `<h3>` 태그 뒤에 `@ServerInfo.` (점 포함)를 입력 합니다. IntelliSense는 드롭다운 목록에서 `ServerInfo` 도우미에 사용할 수 있는 메서드를 표시 하는 방법을 확인 합니다.

    ![메서드가](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. 목록에서 `GetHtml` 메서드를 선택 하 고 Enter 키를 누릅니다. IntelliSense는 메서드를 자동으로 채웁니다. 의 C#모든 메서드와 마찬가지로 메서드 뒤에 `()` 문자를 추가 해야 합니다. `GetHtml` 메서드의 완성 된 코드는 다음 예제와 같습니다.

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. Ctrl + F5 키를 눌러 페이지를 실행 합니다. 브라우저에 표시 되는 페이지는 다음과 같습니다.

    ![브라우저의 기본 페이지](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. 브라우저를 닫습니다.

### <a name="using-the-debugger"></a>디버거 사용

1. *기본 cshtml* 페이지의 맨 위에서 `Page.Title`로 시작 하는 줄 뒤에 다음 코드 줄을 추가 합니다.

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. 코드 왼쪽 편집기의 회색 여백에서 *중단점*을 추가 하기 위해이 새 줄 옆에 있는 다음을 클릭 합니다. 중단점은 해당 지점에서 프로그램의 실행을 중지 하 고 있는지 확인할 수 있도록 디버거에 알리는 마커입니다.

    ![중단점 설정](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. `ServerInfo.GetHtml` 메서드에 대 한 호출을 제거 하 고 그 자리에 `@myTime` 변수에 대 한 호출을 추가 합니다. 이 호출은 새 코드 줄에서 반환 된 현재 시간 값을 표시 합니다.
4. F5 키를 눌러 디버거에서 페이지를 실행 합니다. 설정 하는 중단점에서 페이지가 중지 됩니다. 다음 이미지는 편집기에서 중단점 (노란색)이 있는 페이지의 모양을 보여 줍니다.

    ![디버그 중단점](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. 디버그 도구 모음에서 한 **단계씩** 코드 실행 단추를 클릭 하거나 F11 키를 눌러 다음 코드 줄을 실행 합니다. 이 단추를 클릭할 때마다 실행을 다음 코드 줄로 이동 합니다.

    ![한 단계씩 코드 실행 단추](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. 마우스 포인터를 잡고 **지역** 및 **호출 스택** 창에 표시 된 값을 검사 하 여 `myTime` 변수의 값을 검사 합니다. Visual Studio에서 변수의 값을 표시 합니다.

    ![시간 값 표시](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. 변수 검사를 완료 하 고 코드를 단계별로 실행 하는 경우 F5 키를 눌러 각 줄에서 중지 하지 않고 페이지를 계속 실행 합니다. 모든 코드의 단계별 실행을 완료 하면 브라우저에 페이지가 표시 됩니다.

디버거에 대 한 자세한 내용 및 Visual Studio에서 코드를 디버깅 하는 방법에 대 한 자세한 내용은 [연습: Visual Web Developer에서 웹 페이지 디버깅](https://msdn.microsoft.com/library/z9e7w6cs.aspx)을 참조 하세요.

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>Visual Studio에서 ASP.NET MVC 프로젝트에서 Razor 사용

이 Razor 구문는 ASP.NET MVC 프로젝트 에서도 광범위 하 게 사용 됩니다. MVC는 동적 웹 사이트를 빌드하는 강력한 패턴 기반 방식입니다. ASP.NET 웹 페이지 사이트를 유지 관리 하기 어려운 경우 ASP.NET MVC 응용 프로그램으로 변환 하는 것이 좋습니다. MVC 응용 프로그램을 만드는 방법에 대 한 예제는 [ASP.NET MVC 5 시작](../../../mvc/overview/getting-started/introduction/getting-started.md)을 참조 하세요.

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Visual Studio 2010의 ASP.NET 웹 페이지에 대 한 지원 설치

이 섹션에서는 visual Web Developer Express 2010 및 Visual Studio 용 ASP.NET 웹 페이지 도구를 설치 하는 방법을 보여 줍니다.

1. 웹 플랫폼 설치 관리자가 아직 없는 경우 다음 URL에서 다운로드 합니다.

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. 웹 플랫폼 설치 관리자를 실행 합니다.
3. **제품** 탭을 클릭 합니다.

    ![WebPI 제품 탭](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. **ASP.NET MVC 4** (ASP.NET 웹 페이지 2)를 검색 한 다음 **추가**를 클릭 합니다. 이러한 제품에는 ASP.NET Razor 웹 사이트를 빌드하기 위한 Visual Studio 도구가 포함 되어 있습니다.

    ![WebPi 설치 옵션](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. 설치 **를 클릭 하** 여 설치를 완료 합니다.
