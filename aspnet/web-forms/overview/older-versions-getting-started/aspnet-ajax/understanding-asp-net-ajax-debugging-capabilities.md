---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
title: ASP.NET AJAX 디버깅 기능 이해 | Microsoft Docs
author: scottcate
description: 코드를 디버깅 하는 기능은 사용 하는 기술에 관계 없이 모든 개발자가 잡고에 포함 해야 하는 기술입니다. 많은 개발자가 ...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 7f9380c6-19f7-4c82-a019-916ec6dffc9c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
msc.type: authoredcontent
ms.openlocfilehash: 08ced380f3551407d757524dbc84b5feeeb5482b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74601682"
---
# <a name="understanding-aspnet-ajax-debugging-capabilities"></a>ASP.NET AJAX 디버깅 기능 이해

[Scott cate cda (](https://github.com/scottcate)

[PDF 다운로드](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial06_Debugging_MS_Ajax_Applications_cs.pdf)

> 코드를 디버깅 하는 기능은 사용 하는 기술에 관계 없이 모든 개발자가 잡고에 포함 해야 하는 기술입니다. 대부분의 개발자는 Visual Studio .NET 또는 Web Developer Express를 사용 하 여 VB.NET 또는 C# 코드를 사용 하는 ASP.NET 응용 프로그램을 디버그 하는 데 익숙해져 있지만 JavaScript와 같은 클라이언트 쪽 코드를 디버깅 하는 데 매우 유용 하다는 것을 인식 하지 못합니다. .NET 응용 프로그램을 디버깅 하는 데 사용 되는 것과 동일한 유형의 기술을 AJAX 사용 응용 프로그램 및 더욱 구체적으로 ASP.NET AJAX 응용 프로그램에도 적용할 수 있습니다.

## <a name="debugging-aspnet-ajax-applications"></a>ASP.NET AJAX 응용 프로그램 디버깅

Dan Wahlin

코드를 디버깅 하는 기능은 사용 하는 기술에 관계 없이 모든 개발자가 잡고에 포함 해야 하는 기술입니다. 사용 가능한 다양 한 디버깅 옵션을 이해 하면 프로젝트에 상당한 시간을 절약할 수 있으며 몇 가지 문제를 초래할 수 있습니다. 대부분의 개발자는 Visual Studio .NET 또는 Web Developer Express를 사용 하 여 VB.NET 또는 C# 코드를 사용 하는 ASP.NET 응용 프로그램을 디버그 하는 데 익숙해져 있지만 JavaScript와 같은 클라이언트 쪽 코드를 디버깅 하는 데 매우 유용 하다는 것을 인식 하지 못합니다. .NET 응용 프로그램을 디버깅 하는 데 사용 되는 것과 동일한 유형의 기술을 AJAX 사용 응용 프로그램 및 더욱 구체적으로 ASP.NET AJAX 응용 프로그램에도 적용할 수 있습니다.

이 문서에서는 Visual Studio 2008 및 기타 여러 도구를 사용 하 여 ASP.NET AJAX 응용 프로그램을 디버그 하 여 버그 및 기타 문제를 빠르게 찾을 수 있는 방법을 알아봅니다. 이 토론에는 디버깅을 위해 Internet Explorer 6 이상을 사용 하도록 설정 하 고, Visual Studio 2008 및 스크립트 탐색기를 사용 하 여 코드를 단계별로 실행 하 고, 웹 개발 도우미와 같은 기타 무료 도구를 사용 하는 방법을 설명 합니다. 또한 Firebug 확장을 사용 하 여 Firefox에서 ASP.NET AJAX 응용 프로그램을 디버깅 하는 방법에 대해 알아봅니다 .이를 통해 다른 도구 없이 브라우저에서 직접 JavaScript 코드를 단계별로 진행할 수 있습니다. 마지막으로 추적 및 코드 어설션 문과 같은 다양 한 디버깅 작업에 도움이 될 수 있는 ASP.NET AJAX 라이브러리의 클래스에 대해 소개 합니다.

Internet Explorer에 표시 된 페이지를 디버그 하기 전에 디버깅을 위해 사용 하도록 설정 하기 위해 수행 해야 하는 몇 가지 기본 단계가 있습니다. 시작 하기 위해 수행 해야 하는 몇 가지 기본 설정 요구 사항을 살펴보겠습니다.

## <a name="configuring-internet-explorer-for-debugging"></a>디버깅을 위해 Internet Explorer 구성

대부분의 사용자는 Internet Explorer와 함께 표시 되는 웹 사이트에서 발생 하는 JavaScript 문제를 보지 않습니다. 사실, 평균 사용자에 게 오류 메시지가 나타나는 경우 수행할 작업을 알아야 합니다. 따라서 브라우저에서 디버깅 옵션이 기본적으로 해제 되어 있습니다. 그러나 디버깅을 설정 하 고 새 AJAX 응용 프로그램을 개발할 때 사용 하도록 설정 하는 것은 매우 간단 합니다.

디버깅 기능을 사용 하도록 설정 하려면 Internet Explorer 메뉴에서 도구 인터넷 옵션으로 이동 하 고 고급 탭을 선택 합니다. 검색 섹션 내에서 다음 항목이 선택 취소 되어 있는지 확인 합니다.

- 스크립트 디버깅 사용 안 함 (Internet Explorer)
- 스크립트 디버깅 사용 안 함 (기타)

필수는 아니지만 응용 프로그램을 디버깅 하려는 경우 페이지의 JavaScript 오류가 즉시 표시 되 고 명확 하 게 표시 되는 것이 좋습니다. "모든 스크립트 오류에 대 한 알림 표시" 확인란을 선택 하 여 메시지 상자에서 모든 오류를 강제로 표시할 수 있습니다. 응용 프로그램을 개발 하는 동안이 옵션을 설정 하는 것이 좋지만 JavaScript 오류가 발생할 가능성이 매우 양호 하므로 다른 웹 사이트를 확인 하는 경우에도 신속 하 게 방해가 될 수 있습니다.

그림 1에는 디버깅을 위해 제대로 구성 된 후 Internet Explorer 고급 대화 상자가 표시 되어야 하는 내용이 나와 있습니다.

[디버깅을 위해 Internet Explorer를 구성 하는 ![.](understanding-asp-net-ajax-debugging-capabilities/_static/image2.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image1.png)

**그림 1**: 디버깅을 위해 Internet Explorer 구성  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image3.png))

디버깅이 설정 되 면 스크립트 디버거 라는 보기 메뉴에 새 메뉴 항목이 표시 됩니다. 다음 문을 사용 하 여 두 가지 옵션을 사용할 수 있습니다. 열기를 선택 하면 Visual Studio 2008에서 페이지를 디버깅 하 라는 메시지가 표시 됩니다 (Visual Web Developer Express는 디버깅에도 사용할 수 있음). Visual Studio .NET이 현재 실행 중인 경우 해당 인스턴스를 사용 하도록 선택 하거나 새 인스턴스를 만들 수 있습니다. 다음 문으로 나누기를 선택 하면 JavaScript 코드가 실행 될 때 페이지를 디버그 하 라는 메시지가 표시 됩니다. 페이지의 onLoad 이벤트에서 JavaScript 코드를 실행 하는 경우 페이지를 새로 고쳐 디버그 세션을 트리거할 수 있습니다. 단추를 클릭 한 후 JavaScript 코드가 실행 되 면 단추가 클릭 된 후 즉시 디버거가 실행 됩니다.

> [!NOTE]
> Windows Vista에서 UAC (사용자 Access Control)를 사용 하도록 설정 하 고 Visual Studio 2008을 관리자 권한으로 실행 하도록 설정한 경우에는 연결 하 라는 메시지가 표시 되 면 Visual Studio가 프로세스에 연결 되지 않습니다. 이 문제를 해결 하려면 먼저 Visual Studio를 시작 하 고 해당 인스턴스를 사용 하 여 디버깅 합니다.

다음 섹션에서는 Visual Studio 2008 내에서 직접 ASP.NET AJAX 페이지를 디버깅 하는 방법을 보여 주지만, 페이지가 이미 열려 있고 더 자세히 조사 하려는 경우에는 Internet Explorer 스크립트 디버거 옵션을 사용 하면 유용 합니다.

## <a name="debugging-with-visual-studio-2008"></a>Visual Studio 2008을 사용 하 여 디버깅

Visual Studio 2008는 전 세계 개발자가 매일 .NET 응용 프로그램을 디버깅 하는 데 사용 하는 디버깅 기능을 제공 합니다. 기본 제공 디버거를 사용 하면 코드를 단계별로 실행 하 고, 개체 데이터를 보고, 특정 변수를 감시 하 고, 호출 스택 뿐만 아니라 훨씬 더 많은 기능을 모니터링할 수 있습니다. VB.NET 또는 C# 코드를 디버그 하는 것 외에도 디버거는 ASP.NET AJAX 응용 프로그램을 디버깅 하는 데 유용 하며 JavaScript 코드를 한 줄씩 단계별로 실행할 수 있습니다. 다음 세부 정보는 Visual Studio 2008을 사용 하 여 응용 프로그램을 디버깅 하는 전반적인 프로세스를 제공 하는 대신 클라이언트 쪽 스크립트 파일을 디버그 하는 데 사용할 수 있는 기술에 초점을 discourse.

Visual Studio 2008에서 페이지를 디버깅 하는 과정은 여러 가지 방법으로 시작할 수 있습니다. 먼저 이전 섹션에서 설명한 Internet Explorer 스크립트 디버거 옵션을 사용할 수 있습니다. 이는 페이지가 브라우저에 이미 로드 되어 있고 디버깅을 시작 하려는 경우에 효과적입니다. 또는 솔루션 탐색기에서 .aspx 페이지를 마우스 오른쪽 단추로 클릭 하 고 메뉴에서 시작 페이지로 설정을 선택할 수 있습니다. ASP.NET 페이지를 디버깅 하는 데 익숙한 경우 이전에이 작업을 수행 했을 수 있습니다. F5 키를 누르면 페이지를 디버그할 수 있습니다. 그러나 일반적으로 VB.NET 또는 C# 코드에서 원하는 위치에 중단점을 설정할 수 있지만 다음에 표시 되는 것 처럼 JavaScript를 사용 하는 경우도 있습니다.

*Embedded 및 외부 스크립트*

Visual Studio 2008 디버거는 외부 JavaScript 파일과 다른 페이지에 포함 된 JavaScript를 처리 합니다. 외부 스크립트 파일을 사용 하 여 파일을 열고 선택한 줄에 중단점을 설정할 수 있습니다. 코드 편집기 창 왼쪽에 있는 회색 트레이 영역에서를 클릭 하 여 중단점을 설정할 수 있습니다. JavaScript가 `<script>` 태그를 사용 하 여 페이지에 직접 포함 되어 있는 경우 회색 트레이 영역을 클릭 하 여 중단점을 설정 하는 것은 옵션이 아닙니다. 포함 된 스크립트 줄에 중단점을 설정 하려고 하면 "이는 중단점의 올바른 위치가 아닙니다." 라는 경고가 발생 합니다.

코드를 외부 .js 파일로 이동 하 고 &lt;스크립트&gt; 태그의 src 특성을 사용 하 여 참조 하면이 문제를 해결할 수 있습니다.

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample1.html)]

코드를 외부 파일로 이동 하는 것이 옵션이 아니거나 가치가 더 많은 작업이 필요한 경우는 어떻게 되나요? 편집기를 사용 하 여 중단점을 설정할 수는 없지만 디버깅을 시작 하려는 코드에 직접 디버거 문을 추가할 수 있습니다. ASP.NET AJAX 라이브러리에서 사용할 수 있는 Sys.debug 클래스를 사용 하 여 디버깅을 강제로 시작할 수도 있습니다. 이 문서의 뒷부분에 나오는 Sys. Debug 클래스에 대해 자세히 설명 합니다.

`debugger` 키워드를 사용 하는 예제는 목록 1에 나와 있습니다. 이 예제에서는 업데이트 함수를 호출 하기 전에 디버거가 즉시 중단 되도록 합니다.

**나열 1. 디버거 키워드를 사용 하 여 Visual Studio .NET 디버거가 중단 되도록 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample2.js)]

디버거 문이 적중 되 면 Visual Studio .NET을 사용 하 여 페이지를 디버깅 하 라는 메시지가 표시 되 고 코드를 단계별로 실행할 수 있습니다. 이 작업을 수행 하는 동안 페이지에 사용 된 ASP.NET AJAX 라이브러리 스크립트 파일에 액세스 하는 데 문제가 발생할 수 있으므로 Visual Studio를 사용 하는 방법을 살펴보겠습니다. NET의 스크립트 탐색기

## <a name="using-visual-studio-net-windows-to-debug"></a>Visual Studio .NET Windows를 사용 하 여 디버그

디버그 세션이 시작 되 고 기본 F11 키를 사용 하 여 코드 탐색을 시작 하면 페이지에 사용 된 모든 스크립트 파일이 열려 있고 디버깅에 사용할 수 있는 경우를 제외 하 고 그림 2 참조에 표시 된 오류 대화 상자가 발생할 수 있습니다.

[디버깅에 사용할 수 있는 소스 코드가 없는 경우 표시 되는 ![오류 대화 상자입니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image5.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image4.png)

**그림 2**: 디버깅에 사용할 수 있는 소스 코드가 없는 경우 표시 되는 오류 대화 상자  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image6.png))

이 대화 상자는 Visual Studio .NET에서 페이지에서 참조 하는 일부 스크립트의 소스 코드를 가져오는 방법을 알 수 없기 때문에 표시 됩니다. 이는 처음에는 매우 어려울 수 있지만 간단한 해결 방법이 있습니다. 디버그 세션을 시작 하 고 중단점에 도달 하면 Visual Studio 2008 메뉴의 디버그 Windows 스크립트 탐색기 창으로 이동 하거나 Ctrl + Alt + N 바로 가기 키를 사용 합니다.

> [!NOTE]
> 스크립트 탐색기 메뉴가 표시 되지 않는 경우 **도구** > Visual Studio .net 메뉴에서 > **명령** **사용자 지정** 으로 이동 합니다. 범주 섹션에서 **디버그** 항목을 찾은 다음 클릭 하 여 사용 가능한 모든 메뉴 항목을 표시 합니다. 명령 목록에서 스크립트 탐색기로 스크롤한 다음 앞에서 언급 한 Windows 디버그 메뉴로 끕니다. 이렇게 하면 Visual Studio .NET을 실행할 때마다 스크립트 탐색기 메뉴 항목을 사용할 수 있게 됩니다.

스크립트 탐색기를 사용 하 여 페이지에 사용 된 모든 스크립트를 보고 코드 편집기에서 열 수 있습니다. 스크립트 탐색기가 열리면 현재 디버그 중인 .aspx 페이지를 두 번 클릭 하 여 코드 편집기 창에서 엽니다. 스크립트 탐색기에 표시 된 다른 모든 스크립트에 대해 동일한 작업을 수행 합니다. 모든 스크립트가 코드 창에 열려 있으면 F11 키를 누르고 다른 디버그 바로 가기 키를 사용 하 여 코드를 단계별로 실행 하면 됩니다. 그림 3에서는 스크립트 탐색기의 예를 보여 줍니다. 디버깅 중인 현재 파일 (Demo) 뿐만 아니라 ASP.NET AJAX ScriptManager가 페이지에 동적으로 삽입 하는 두 개의 사용자 지정 스크립트 및 두 개의 스크립트를 나열 합니다.

[![스크립트 탐색기를 사용 하면 페이지에 사용 되는 스크립트에 쉽게 액세스할 수 있습니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image8.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image7.png)

**그림 3**. 스크립트 탐색기를 사용 하면 페이지에서 사용 하는 스크립트에 쉽게 액세스할 수 있습니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image9.png))

페이지에서 코드를 단계별로 실행 하는 경우 다른 여러 창을 사용 하 여 유용한 정보를 제공할 수도 있습니다. 예를 들어 지역 창을 사용 하 여 페이지에서 사용 되는 다양 한 변수의 값을 확인 하 고, 직접 실행 창에서 특정 변수나 조건을 평가 하 고, 출력을 볼 수 있습니다. 출력 창을 사용 하 여이 문서의 뒷부분에서 설명 하는, 또는 Internet Explorer의 Debug. writeln 함수를 사용 하 여 작성 된 추적 문을 볼 수도 있습니다.

디버거를 사용 하 여 코드를 단계별로 실행 하면 코드에서 변수 위로 마우스를 가져가면 할당 된 값을 볼 수 있습니다. 그러나 스크립트 디버거는 특정 JavaScript 변수 위에 마우스를 놓았을 때 어떤 것도 표시 하지 않을 수 있습니다. 값을 보려면 코드 편집기 창에서 확인 하려는 문이나 변수를 강조 표시 한 다음 마우스를 누릅니다. 이 기법은 모든 상황에서 작동 하지는 않지만 지역 창과 같은 다른 디버그 창에서 찾을 필요 없이 값을 볼 수 있습니다.

여기에서 설명 하는 기능 중 일부를 보여 주는 비디오 자습서는 [http://www.xmlforasp.net](http://www.xmlforasp.net)에서 볼 수 있습니다.

## <a name="debugging-with-web-development-helper"></a>웹 개발 도우미를 사용 하 여 디버깅

Visual Studio 2008 (및 Visual Web Developer Express 2008)은 매우 유용 하 게 사용할 수 있는 디버깅 도구 이지만 더 적은 수의 추가 옵션도 사용할 수 있습니다. 출시 될 최신 도구 중 하나는 웹 개발 도우미입니다. Microsoft의 Nikhil Kothari (Microsoft의 주요 ASP.NET AJAX 설계자)는 간단한 디버깅에서 HTTP 요청 및 응답 메시지를 볼 수 있는 다양 한 작업을 수행할 수 있는 훌륭한 도구를 작성 했습니다. 웹 개발 도우미는 [http://projects.nikhilk.net/Projects/WebDevHelper.aspx](http://projects.nikhilk.net/Projects/WebDevHelper.aspx)에서 다운로드할 수 있습니다.

웹 개발 도우미를 사용 하면 편리 하 게 사용할 수 있는 Internet Explorer 내에서 직접 사용할 수 있습니다. Internet Explorer 메뉴에서 도구 웹 개발 도우미를 선택 하 여 시작 합니다. 이렇게 하면 브라우저에서 HTTP 요청 및 응답 메시지 로깅과 같은 몇 가지 작업을 수행 하지 않아도 되므로 좋은 도구는 브라우저의 아래쪽 부분에서 열립니다. 그림 4에서는 웹 개발 도우미가 어떻게 작동 하 고 있는 것을 보여 줍니다.

[![웹 개발 도우미](understanding-asp-net-ajax-debugging-capabilities/_static/image11.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image10.png)

**그림 4**: 웹 개발 도우미 ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image12.png))

웹 개발 도우미는 Visual Studio 2008에서와 같이 코드를 한 줄씩 단계별로 실행 하는 데 사용 하는 도구가 아닙니다. 그러나이를 사용 하 여 추적 출력을 보거나 스크립트의 변수를 쉽게 평가 하거나 데이터를 탐색할 수 있습니다. ASP.NET AJAX 페이지와 서버 간에 전달 되는 데이터를 보는 데에도 매우 유용 합니다.

Internet Explorer에 웹 개발 도우미가 열리면 그림 4의 앞부분에 나와 있는 것 처럼 웹 개발 도우미 메뉴에서 스크립트 디버깅 사용 스크립트를 선택 하 여 스크립트 디버깅을 사용 하도록 설정 해야 합니다. 이를 통해 도구는 페이지가 실행 될 때 발생 하는 오류를 가로챌 수 있습니다. 또한 페이지에 출력 된 추적 메시지에 쉽게 액세스할 수 있습니다. 추적 정보를 보거나 스크립트 명령을 실행 하 여 페이지 내에서 다른 기능을 테스트 하려면 웹 개발 도우미 메뉴에서 스크립트 표시 스크립트 콘솔을 선택 합니다. 그러면 명령 창과 간단한 직접 실행 창에 액세스할 수 있습니다.

*추적 메시지 및 JSON 개체 데이터 보기*

직접 실행 창을 사용 하 여 스크립트 명령을 실행 하거나 페이지의 다른 함수를 테스트 하는 데 사용 되는 스크립트를 로드 하거나 저장할 수 있습니다. 명령 창에는 표시 되는 페이지에 의해 기록 된 추적 또는 디버그 메시지가 표시 됩니다. 목록 2에서는 Internet Explorer의 Debug. writeln 함수를 사용 하 여 추적 메시지를 작성 하는 방법을 보여 줍니다.

**목록 2. Debug 클래스를 사용 하 여 클라이언트 쪽 추적 메시지를 작성 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample3.js)]

LastName 속성이 Doe 값을 포함 하는 경우 웹 개발 도우미는 스크립트 콘솔의 명령 창에 "Person name: Doe" 라는 메시지를 표시 합니다 (디버깅이 사용 하도록 설정 된 것으로 가정). 웹 개발 도우미는 또한 추적 정보를 작성 하거나 JSON 개체의 내용을 보는 데 사용할 수 있는 페이지에 최상위 debugService 개체를 추가 합니다. 목록 3은 debugService 클래스의 추적 함수를 사용 하는 예를 보여 줍니다.

**목록 3. 웹 개발 도우미의 debugService 클래스를 사용 하 여 추적 메시지를 작성 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample4.js)]

DebugService 클래스의 유용한 기능은 Internet Explorer에서 디버깅을 사용 하도록 설정 하지 않은 경우에도 작동 하 여 웹 개발 도우미가 실행 중일 때 추적 데이터에 쉽게 액세스할 수 있도록 하는 것입니다. 도구를 사용 하 여 페이지를 디버그 하지 않는 경우에는 창에 대 한 호출 이후 추적 문이 무시 됩니다. debugService는 false를 반환 합니다.

DebugService 클래스를 사용 하면 웹 개발 도우미의 검사기 창을 사용 하 여 JSON 개체 데이터를 볼 수도 있습니다. 목록 4는 person 데이터를 포함 하는 간단한 JSON 개체를 만듭니다. 개체를 만든 후에는 debugService 클래스의 검사 함수를 호출 하 여 JSON 개체를 시각적으로 검사할 수 있습니다.

**목록 4. DebugService. 검사 함수를 사용 하 여 JSON 개체 데이터를 확인 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample5.js)]

페이지에서 또는 직접 실행 창을 통해 GetPerson () 함수를 호출 하면 그림 5와 같이 개체 검사기 대화 상자 창이 나타납니다. 개체 내의 속성은 강조 표시 하 고 값 텍스트 상자에 표시 된 값을 변경한 다음 업데이트 링크를 클릭 하 여 동적으로 변경할 수 있습니다. 개체 검사자를 사용 하면 간단 하 게 JSON 개체 데이터를 보고 속성에 다른 값을 적용 하 여 시험해 볼 수 있습니다.

*디버깅 오류*

웹 개발 도우미는 추적 데이터 및 JSON 개체를 표시 하도록 허용 하는 것 외에도 페이지의 디버깅 오류를 지원할 수 있습니다. 오류가 발생 하는 경우 다음 코드 줄을 계속 하거나 스크립트를 디버그 하 라는 메시지가 표시 됩니다 (그림 6 참조). 스크립트 오류 대화 상자 창에는 스크립트 내에서 문제가 발생 한 위치를 쉽게 식별할 수 있도록 줄 번호 뿐만 아니라 전체 호출 스택이 표시 됩니다.

[JSON 개체를 보려면 개체 검사기 창을 사용 하 여 ![합니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image14.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image13.png)

**그림 5**: 개체 검사기 창을 사용 하 여 JSON 개체 보기  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image15.png))

디버그 옵션을 선택 하면 웹 개발 도우미의 직접 실행 창에서 직접 스크립트 문을 실행 하 여 변수 값을 보고 JSON 개체를 작성할 수 있습니다. 오류를 트리거한 동일한 작업을 다시 수행 하 고 Visual Studio 2008을 컴퓨터에서 사용할 수 있는 경우 이전 섹션에서 설명한 대로 코드를 한 줄씩 단계별로 실행할 수 있도록 디버그 세션을 시작 하 라는 메시지가 표시 됩니다.

[![웹 개발 도우미의 스크립트 오류 대화 상자](understanding-asp-net-ajax-debugging-capabilities/_static/image17.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image16.png)

**그림 6**: 웹 개발 도우미의 스크립트 오류 대화 상자 ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image18.png))

*요청 및 응답 메시지 검사*

ASP.NET AJAX 페이지를 디버깅 하는 동안 페이지와 서버 간에 전송 되는 요청 및 응답 메시지를 확인 하는 것이 유용한 경우가 많습니다. 메시지 내에서 콘텐츠를 보면 적절 한 데이터가 전달 되는지, 메시지 크기를 확인할 수 있습니다. 웹 개발 도우미는 데이터를 원시 텍스트 또는 좀 더 읽기 쉬운 형식으로 쉽게 볼 수 있도록 하는 뛰어난 HTTP 메시지로 거 기능을 제공 합니다.

ASP.NET AJAX 요청 및 응답 메시지를 보려면 웹 개발 도우미 메뉴에서 http 사용 http 로깅을 선택 하 여 HTTP로 거를 사용 하도록 설정 해야 합니다. 활성화 된 후에는 http Show HTTP Logs를 선택 하 여 액세스할 수 있는 HTTP 로그 뷰어에서 현재 페이지에서 보낸 모든 메시지를 볼 수 있습니다.

각 요청/응답 메시지에 전송 된 원시 텍스트를 보는 것은 매우 유용 하지만 (웹 개발 도우미의 옵션), 메시지 데이터를 보다 그래픽 형식으로 더 쉽게 볼 수 있는 경우도 있습니다. HTTP 로깅을 사용 하도록 설정 하 고 메시지가 기록 되 면 HTTP 로그 뷰어에서 메시지를 두 번 클릭 하 여 메시지 데이터를 볼 수 있습니다. 이렇게 하면 실제 메시지 내용 뿐만 아니라 메시지와 연결 된 모든 헤더를 볼 수 있습니다. 그림 7에서는 HTTP 로그 뷰어 창에 표시 되는 요청 메시지와 응답 메시지의 예를 보여 줍니다.

[HTTP 로그 뷰어를 사용 하 여 요청 및 응답 메시지 데이터를 확인 ![합니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image20.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image19.png)

**그림 7**: HTTP 로그 뷰어를 사용 하 여 요청 및 응답 메시지 데이터 보기  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image21.png))

HTTP 로그 뷰어는 JSON 개체를 자동으로 구문 분석 하 여 개체의 속성 데이터를 빠르고 쉽게 볼 수 있도록 하는 트리 뷰를 사용 하 여 표시 합니다. ASP.NET AJAX 페이지에서 UpdatePanel을 사용 하는 경우 뷰어는 그림 8에 표시 된 것 처럼 메시지의 각 부분을 개별 파트로 나눕니다. 이 기능을 사용 하면 원시 메시지 데이터를 보는 것과 비교 하 여 메시지의 내용을 더 쉽게 확인 하 고 이해할 수 있습니다.

[HTTP 로그 뷰어를 사용 하 여 본 UpdatePanel 응답 메시지를 ![합니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image23.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image22.png)

**그림 8**: HTTP 로그 뷰어를 사용 하 여 본 UpdatePanel 응답 메시지  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image24.png))

웹 개발 도우미 외에도 요청 및 응답 메시지를 보는 데 사용할 수 있는 몇 가지 다른 도구가 있습니다. 또 다른 좋은 옵션은 [http://www.fiddlertool.com](http://www.fiddlertool.com)에서 무료로 제공 되는 Fiddler입니다. 여기서 Fiddler는 다루지 않지만 메시지 헤더와 데이터를 철저히 검사 해야 하는 경우에도 좋은 옵션입니다.

## <a name="debugging-with-firefox-and-firebug"></a>Firefox 및 Firebug를 사용 하 여 디버깅

Internet Explorer는 여전히 가장 널리 사용 되는 브라우저 이지만 Firefox와 같은 다른 브라우저는 널리 사용 되 고 있으며 더 많이 사용 되 고 있습니다. 따라서 Firefox 및 Internet Explorer에서 ASP.NET AJAX 페이지를 보고 디버그 하 여 응용 프로그램이 제대로 작동 하는지 확인할 수 있습니다. Firefox는 디버깅을 위해 Visual Studio 2008에 직접 연결할 수 없지만 페이지를 디버그 하는 데 사용할 수 있는 Firebug 이라는 확장이 있습니다. [http://www.getfirebug.com](http://www.getfirebug.com)로 이동 하 여 Firebug를 무료로 다운로드할 수 있습니다.

Firebug은 코드 줄을 단계별로 실행 하 고, 페이지 내에서 사용 되는 모든 스크립트에 액세스 하 고, DOM 구조를 보고, CSS 스타일을 표시 하 고, 페이지에서 발생 하는 이벤트를 추적 하는 데 사용할 수 있는 완전 한 기능을 갖춘 디버깅 환경을 제공 합니다. 일단 설치 되 면 Firefox 메뉴에서 도구 Firebug Open Firebug를 선택 하 여 Firebug에 액세스할 수 있습니다. 웹 개발 도우미와 마찬가지로 Firebug는 독립 실행형 응용 프로그램으로도 사용할 수 있지만 브라우저에서 직접 사용 됩니다.

Firebug가 실행 되 면 스크립트가 페이지에 포함 되는지 여부에 관계 없이 JavaScript 파일의 모든 줄에 중단점을 설정할 수 있습니다. 중단점을 설정 하려면 먼저 Firefox에서 디버그할 적절 한 페이지를 로드 합니다. 페이지가 로드 되 면 Firebug의 스크립트 드롭다운 목록에서 디버그할 스크립트를 선택 합니다. 페이지에서 사용 하는 모든 스크립트가 표시 됩니다. 중단점은 Visual Studio 2008에서 수행 해야 하는 것과 같은 방식으로 중단점이 이동 해야 하는 줄에서 Firebug의 회색 트레이 영역을 클릭 하 여 설정 합니다.

Firebug에서 중단점을 설정한 후에는 단추를 클릭 하거나 브라우저를 새로 고쳐 onLoad 이벤트를 트리거하기 위해 디버깅 해야 하는 스크립트를 실행 하는 데 필요한 작업을 수행할 수 있습니다. 중단점이 포함 된 줄에서 실행이 자동으로 중지 됩니다. 그림 9에서는 Firebug에서 트리거된 중단점의 예를 보여 줍니다.

[Firebug에서 중단점을 처리 하는 ![.](understanding-asp-net-ajax-debugging-capabilities/_static/image26.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image25.png)

**그림 9**: Firebug에서 중단점 처리  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image27.png))

중단점이 적중 되 면 화살표 단추를 사용 하 여 코드를 한 단계씩 실행 하거나 프로시저 단위로 실행 하거나 코드를 프로시저 단위로 실행 합니다. 코드를 단계별로 실행 하면 디버거의 오른쪽 부분에 스크립트 변수를 표시 하 여 개체에 대 한 값 및 드릴 다운을 확인할 수 있습니다. Firebug에는 디버깅 중인 현재 줄을 표시 하는 스크립트 실행 단계를 표시 하는 호출 스택 드롭다운 목록도 포함 되어 있습니다.

Firebug에는 다양 한 스크립트 문을 테스트 하 고 변수를 평가 하 고 추적 출력을 보는 데 사용할 수 있는 콘솔 창도 포함 되어 있습니다. Firebug 창의 맨 위에 있는 콘솔 탭을 클릭 하 여 액세스할 수 있습니다. 검사 탭을 클릭 하 여 디버그 중인 페이지를 "검사" 하 여 DOM 구조 및 내용을 볼 수도 있습니다. 검사기 창에 표시 되는 다른 DOM 요소 위에 마우스를 놓으면 페이지의 해당 부분이 강조 표시 되어 페이지에서 요소가 사용 되는 위치를 쉽게 확인할 수 있습니다. 지정 된 요소와 연결 된 특성 값은 다른 너비, 스타일 등을 요소에 적용 하 여 시험해 볼 수 있도록 "라이브"로 변경할 수 있습니다. 이 기능을 통해 소스 코드 편집기와 Firefox 브라우저 간을 지속적으로 전환 하 여 간단한 변경 내용이 페이지에 미치는 영향을 확인할 필요가 없습니다.

그림 10에서는 DOM 검사기를 사용 하 여 페이지에서 txtCountry 라는 텍스트 상자를 찾는 예를 보여 줍니다. Firebug 검사기를 사용 하 여 페이지에 사용 되는 CSS 스타일 뿐만 아니라 마우스 이동, 단추 클릭 등을 추적 하는 등의 이벤트를 볼 수도 있습니다.

[Firebug의 DOM 검사기를 사용 하 여 ![합니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image29.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image28.png)

**그림 10**: FIREBUG의 DOM 검사기 사용  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image30.png))

Firebug는 Firefox에서 직접 페이지를 신속 하 게 디버그 하는 간단한 방법을 제공 하 고 페이지 내에서 다양 한 요소를 검사 하는 데 유용한 도구를 제공 합니다.

## <a name="debugging-support-in-aspnet-ajax"></a>ASP.NET AJAX의 디버깅 지원

ASP.NET AJAX 라이브러리에는 AJAX 기능을 웹 페이지에 추가 하는 프로세스를 간소화 하는 데 사용할 수 있는 다양 한 클래스가 포함 되어 있습니다. 이러한 클래스를 사용 하 여 페이지 내에서 요소를 찾고 조작 하 고, 새 컨트롤을 추가 하 고, 웹 서비스를 호출 하 고, 이벤트를 처리할 수도 있습니다. ASP.NET AJAX 라이브러리에는 디버깅 페이지의 프로세스를 개선 하는 데 사용할 수 있는 클래스도 포함 되어 있습니다. 이 섹션에서는 Sys. Debug 클래스를 소개 하 고 응용 프로그램에서이 클래스를 사용할 수 있는 방법을 확인 합니다.

*Sys. Debug 클래스 사용*

Sys. Debug 클래스 (Sys 네임 스페이스에 있는 JavaScript 클래스)를 사용 하 여 추적 출력을 작성 하 고, 코드 어설션을 수행 하 고, 코드를 디버그 하 여 디버그할 수 있도록 강제할 수 있습니다. ASP.NET AJAX 라이브러리의 디버그 파일 (기본적으로 C:\Program Files\Microsoft NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0에 설치 됨)에서 광범위 하 게 사용 되어 조건부 테스트를 수행 합니다 ( 매개 변수를 함수에 올바르게 전달 하 고, 개체에 필요한 데이터를 포함 하 고, 추적 문을 쓸 수 있도록 하는 어설션 이라고 합니다.

Sys.debug 클래스는 표 1에 표시 된 대로 추적, 코드 어설션 또는 오류를 처리 하는 데 사용할 수 있는 여러 가지 다른 함수를 노출 합니다.

**표 1. Sys. Debug 클래스 함수입니다.**

| **함수 이름** | **설명** |
| --- | --- |
| assert (condition, message, displayCaller) | Condition 매개 변수가 true 임을 어설션 합니다. 테스트 중인 조건이 false 인 경우 메시지 상자는 메시지 매개 변수 값을 표시 하는 데 사용 됩니다. DisplayCaller 매개 변수가 true 이면 메서드는 호출자에 대 한 정보도 표시 합니다. |
| clearTrace () | 추적 작업에서 문 출력을 지웁니다. |
| fail (메시지) | 프로그램이 실행을 중지 하 고 디버거로 중단 되도록 합니다. 메시지 매개 변수를 사용 하 여 실패 이유를 제공할 수 있습니다. |
| 추적 (메시지) | 메시지 매개 변수를 추적 출력에 씁니다. |
| traceDump (개체, 이름) | 개체의 데이터를 읽을 수 있는 형식으로 출력 합니다. Name 매개 변수는 추적 덤프에 대 한 레이블을 제공 하는 데 사용할 수 있습니다. 덤프 되는 개체 내의 모든 하위 개체는 기본적으로 작성 됩니다. |

클라이언트 쪽 추적은 ASP.NET에서 사용할 수 있는 추적 기능과 거의 동일한 방식으로 사용할 수 있습니다. 응용 프로그램의 흐름을 중단 하지 않고 다른 메시지를 쉽게 볼 수 있습니다. 목록 5는 추적 로그에 쓰는 데 사용 하는 예를 보여 줍니다. trace 함수를 사용 합니다. 이 함수는 매개 변수로 서 써야 하는 메시지를 가져옵니다.

**목록 5. 사용 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample6.js)]

목록 5에 표시 된 코드를 실행 하면 페이지에 추적 출력이 표시 되지 않습니다. 이를 확인 하는 유일한 방법은 Visual Studio .NET, 웹 개발 도우미 또는 Firebug에서 사용할 수 있는 콘솔 창을 사용 하는 것입니다. 페이지에 추적 출력을 표시 하려면 다음에 표시 된 것 처럼 TextArea 태그를 추가 하 고 id를 TraceConsole로 지정 해야 합니다.

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample7.html)]

페이지의 모든 TraceConsole 문은 TextArea에 기록 됩니다.

JSON 개체 내에 포함 된 데이터를 보려는 경우에는 traceDump 클래스의 함수를 사용할 수 있습니다. 이 함수는 추적 콘솔에 덤프 해야 하는 개체와 추적 출력에서 개체를 식별 하는 데 사용할 수 있는 이름을 포함 하 여 두 개의 매개 변수를 사용 합니다. 목록 6에서는 traceDump 함수를 사용 하는 예를 보여 줍니다.

**목록 6. TraceDump 함수를 사용 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample8.js)]

그림 11에서는 traceDump 함수 호출의 출력을 보여 줍니다. Person 개체의 데이터를 작성 하는 것 외에도 주소 하위 개체의 데이터를 작성 합니다.

추적 외에도 Sys. Debug 클래스를 사용 하 여 코드 어설션을 수행할 수 있습니다. 어설션은 응용 프로그램이 실행 되는 동안 특정 조건이 충족 되는지 테스트 하는 데 사용 됩니다. ASP.NET AJAX 라이브러리 스크립트의 디버그 버전에는 다양 한 조건을 테스트 하기 위한 여러 assert 문이 포함 되어 있습니다.

목록 7은 조건을 테스트 하기 위해 Sys.debug 함수를 사용 하는 예를 보여 줍니다. 이 코드는 Person 개체를 업데이트 하기 전에 Address 개체가 null 인지 여부를 테스트 합니다.

[traceDump 함수의 출력을 ![합니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image32.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image31.png)

**그림 11**: traceDump 함수의 출력  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image33.png))

**목록 7. Debug. assert 함수를 사용 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample9.js)]

평가할 조건, 어설션이 false를 반환 하는 경우 표시할 메시지, 호출자에 대 한 정보를 표시할지 여부를 포함 하 여 세 개의 매개 변수가 전달 됩니다. 어설션이 실패 하는 경우 세 번째 매개 변수가 true 인 경우 호출자 정보 뿐만 아니라 메시지가 표시 됩니다. 그림 12는 목록 7에 표시 되는 어설션이 실패 한 경우 표시 되는 오류 대화 상자의 예를 보여 줍니다.

처리할 마지막 함수는 Sys. Debug. fail입니다. 스크립트의 특정 줄에서 코드를 강제로 실행 하지 않으려면 JavaScript 응용 프로그램에서 일반적으로 사용 되는 디버거 문이 아닌 호출을 추가 하면 됩니다. Sys. fail. fail 함수는 다음에 표시 된 것 처럼 실패의 원인을 나타내는 단일 문자열 매개 변수를 허용 합니다.

[!code-css[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample10.css)]

[![. assert 오류 메시지입니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image35.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image34.png)

**그림 12**: Sys. assert 오류 메시지  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image36.png))

스크립트를 실행 하는 동안 Sys.debug 문이 발생 하면 message 매개 변수의 값이 Visual Studio 2008와 같은 디버그 응용 프로그램의 콘솔에 표시 되 고 응용 프로그램을 디버그 하 라는 메시지가 표시 됩니다. 이 방법이 매우 유용할 수 있는 한 가지 경우는 인라인 스크립트에서 Visual Studio 2008을 사용 하 여 중단점을 설정할 수 없지만 특정 줄에서 코드를 중지 하 여 변수 값을 검사할 수 있는 경우입니다.

*ScriptManager 컨트롤의 ScriptMode 속성 이해*

ASP.NET AJAX 라이브러리는 기본적으로 C:\Program Files\Microsoft ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0에 설치 된 디버그 및 릴리스 스크립트 버전을 포함 합니다. 디버그 스크립트는 깔끔하게 형식이 지정 되 고 쉽게 읽을 수 있으며, 릴리스 스크립트에는 공백이 제거 되 고 전체 크기를 최소화 하는 데에만 사용 되는 경우에만 Sys. Debug 클래스를 사용 합니다.

ASP.NET AJAX 페이지에 추가 된 ScriptManager 컨트롤은 web.config에서 컴파일 요소의 debug 특성을 읽어 로드할 라이브러리 스크립트 버전을 결정 합니다. 그러나 ScriptMode 속성을 변경 하 여 디버그 또는 릴리스 스크립트 (라이브러리 스크립트 또는 사용자 지정 스크립트)를 로드할지 여부를 제어할 수 있습니다. ScriptMode는 해당 멤버가 Auto, Debug, Release 및 Inherit를 포함 하는 ScriptMode 열거형을 허용 합니다.

ScriptMode는 자동으로 기본값을 사용 하 여 ScriptManager가 web.config의 debug 특성을 확인 함을 의미 합니다. 디버그가 false 인 경우 ScriptManager가 ASP.NET AJAX 라이브러리 스크립트의 릴리스 버전을 로드 합니다. 디버그가 true 이면 스크립트의 디버그 버전이 로드 됩니다. ScriptMode 속성을 릴리스 또는 디버그로 변경 하면 디버그 특성이 web.config에 포함 된 값에 관계 없이 ScriptManager가 적절 한 스크립트를 로드 합니다. 목록 8에서는 ScriptManager 컨트롤을 사용 하 여 ASP.NET AJAX 라이브러리에서 디버그 스크립트를 로드 하는 예제를 보여 줍니다.

**목록 8. ScriptManager를 사용 하 여 디버그 스크립트 로드**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample11.aspx)]

목록 9에 표시 된 것 처럼 System.web.ui.scriptreference 구성 요소와 함께 ScriptManager의 Scripts 속성을 사용 하 여 고유한 사용자 지정 스크립트의 다른 버전 (디버그 또는 릴리스)을 로드할 수도 있습니다.

**목록 9. ScriptManager를 사용 하 여 사용자 지정 스크립트 로드**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample12.aspx)]

> [!NOTE]
> System.web.ui.scriptreference 구성 요소를 사용 하 여 사용자 지정 스크립트를 로드 하는 경우 스크립트의 맨 아래에 다음 코드를 추가 하 여 스크립트 로드가 완료 될 때 ScriptManager에 알려야 합니다.

[!code-csharp[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample13.cs)]

목록 9에 표시 된 코드는 사용자 스크립트의 디버그 버전을 검색 하도록 ScriptManager에 지시 하 여 사용자를 대신 하 여 사용자가 자동으로 찾도록 합니다. 사용자 파일을 찾을 수 없는 경우 오류가 발생 합니다.

ScriptManager 컨트롤에 설정 된 ScriptMode 속성의 값을 기반으로 사용자 지정 스크립트의 디버그 또는 릴리스 버전을 로드 하려는 경우 System.web.ui.scriptreference 컨트롤의 ScriptMode 속성이 상속 되도록 설정할 수 있습니다. 이렇게 하면 목록 10에 표시 된 것 처럼 ScriptManager의 ScriptMode 속성에 따라 적절 한 버전의 사용자 지정 스크립트가 로드 됩니다. ScriptManager 컨트롤의 ScriptMode 속성이 Debug로 설정 되어 있기 때문에 사용자의 페이지에서 사용자. b a. j a b 스크립트를 로드 하 여 사용 합니다.

**10. 사용자 지정 스크립트에 대 한 ScriptManager에서 ScriptMode 상속**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample14.aspx)]

ScriptMode 속성을 적절 하 게 사용 하면 응용 프로그램을 더 쉽게 디버깅 하 고 전체 프로세스를 간소화할 수 있습니다. 디버그 스크립트를 디버깅 목적으로 사용 하는 동안 코드 형식이 제거 된 후 ASP.NET AJAX 라이브러리의 릴리스 스크립트를 단계별로 실행 하 고 읽는 것은 어렵습니다.

## <a name="conclusion"></a>결론

Microsoft의 ASP.NET AJAX 기술은 최종 사용자의 전반적인 환경을 개선할 수 있는 AJAX 사용 응용 프로그램을 빌드하기 위한 견고한 기반을 제공 합니다. 그러나 모든 프로그래밍 기술과 마찬가지로 버그와 기타 응용 프로그램 문제가 발생 합니다. 사용 가능한 다양 한 디버깅 옵션을 알면 많은 시간을 절약 하 고 더 안정적으로 제품을 만들 수 있습니다.

이 문서에서는 Visual Studio 2008, 웹 개발 도우미 및 Firebug를 사용 하는 Internet Explorer를 포함 하 여 ASP.NET AJAX 페이지를 디버깅 하기 위한 여러 가지 방법에 대해 소개 했습니다. 이러한 도구를 사용 하면 변수 데이터에 액세스 하 고 코드를 한 줄씩 단계별로 실행 하 고 추적 문을 볼 수 있으므로 전체 디버깅 프로세스를 간소화할 수 있습니다. 설명 된 다양 한 디버깅 도구 외에도, 응용 프로그램에서 ASP.NET AJAX 라이브러리의 Sys.debug 클래스를 사용 하는 방법과 ScriptManager 클래스를 사용 하 여 스크립트의 디버그 또는 릴리스 버전을 로드 하는 방법도 살펴보았습니다.

## <a name="bio"></a>약력

Dan Wahlin (Microsoft에서 가장 중요 한 ASP.NET 및 XML Web Services)는 www.interfacett.com (인터페이스 기술 교육[)](http://www.interfacett.com)의 .net 개발 강사 및 아키텍처 컨설턴트입니다. Dan은 ASP.NET 개발자 웹 사이트 ([www.XMLforASP.NET](http://www.XMLforASP.NET))에 대 한 XML을 기반으로 하 고 있으며,이는 INETA 스피커의 기관에 있으며 여러 회의를 말합니다. Dan 공동 작성 Wrox (전문가 Windows DNA), ASP.NET: 팁, 자습서 및 코드 (Sams teach yourself), ASP.NET 1.1 Insider Solutions, ASP.NET (전문 Wrox 2.0 AJAX), ASP.NET 2.0 MVP 해킹 및 제작한 XML for ASP.NET 개발자 (sams teach yourself). 코드, 문서 또는 책을 작성 하지 않을 때 Dan은 음악을 작성 하 고 기록 하 고 아내 및 어린이와 함께 golf 및 농구를 재생 하는 것을 활용할.

Scott Cate cda (는 1997부터 Microsoft 웹 기술을 사용 하 고 있으며 기술 자료 소프트웨어 솔루션에 초점을 맞춘 ASP.NET 기반 응용 프로그램을 전문적으로 작성 하는[www.myKB.com](http://www.myKB.com)(myKB.com)의 부사장입니다. Scott은 [scott.cate@myKB.com](mailto:scott.cate@myKB.com) 또는 [ScottCate.com](http://ScottCate.com) 의 블로그의 전자 메일을 통해 연락할 수 있습니다.

> [!div class="step-by-step"]
> [이전](understanding-asp-net-ajax-web-services.md)
