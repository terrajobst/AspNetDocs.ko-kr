---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 소개 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469799"
---
# <a name="intro-to-aspnet-mvc"></a>ASP.NET MVC 소개

[Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)를 [사용 하 여](../../getting-started/introduction/getting-started.md) 이 자습서를 사용할 수 있는 경우 업데이트 된 버전입니다. 새 자습서에서는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.
>
>
> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다. [ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.

[Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)를 사용 하 여 첫 번째 ASP.NET MVC 웹 응용 프로그램을 만들어 보겠습니다. 영화를 만들고 나열 하는 데 도움이 되는 약간의 영화 목록 응용 프로그램을 만듭니다.

## <a name="what-youll-build"></a>만들 내용

빌드할 응용 프로그램의 두 스크린샷은 다음과 같습니다. 다양 한 열이 포함 된 간단한 영화 테이블이 있습니다.

[![동영상 목록-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

그리고 목록에 영화를 추가할 수 있도록 만들기 양식이 제공 됩니다.

[동영상 ![만들기-Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a>학습할 기술

이 자습서에서는 Visual Studio를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다. 다음 내용을 배웁니다.

- 새 ASP.NET MVC 프로젝트를 만드는 방법
- SQL Server를 사용 하 여 새 데이터베이스를 만드는 방법
- ASP.NET MVC 컨트롤러 및 뷰를 만드는 방법
- 데이터를 검색 하 고 표시 하는 방법
- 데이터를 편집 하 고 데이터 유효성 검사를 사용 하도록 설정 하는 방법
- 데이터베이스 스키마를 업데이트 하는 방법

## <a name="get-started"></a>시작

Visual Web Developer 2010 Express를 실행 하 여 시작 합니다 (지금부터 "VWD" 이라고 함). 그런 다음 시작 화면에서 새 프로젝트를 선택 합니다.

Visual Web Developer는 IDE 또는 통합 된 개발자 환경입니다. Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 IDE를 사용 하 여 응용 프로그램을 만듭니다. 사용자에 게 제공 되는 다양 한 옵션 및 파일을 선택 하는 데 사용 하는 메뉴를 보여 주는 도구 모음이 있습니다. 새 프로젝트입니다.

[Microsoft Visual Web Developer 2010 Express ![](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a>첫 번째 응용 프로그램 만들기

Visual Basic 또는 시각적 개체 C#를 사용 하 여 응용 프로그램을 만들 수 있습니다. 지금은 왼쪽에서 시각적 개체 C# 를 선택 하 고 "ASP.NET MVC 2 웹 응용 프로그램"을 선택 합니다. 프로젝트 이름을 "영화"로, 확인을 클릭 합니다.

[새 프로젝트 ![](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

오른쪽에는 응용 프로그램의 모든 파일 및 폴더를 표시 하는 솔루션 탐색기 있습니다. 가운데에 있는 큰 창에서는 코드를 편집 하 여 대부분의 시간을 소비 합니다. Visual Studio는 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하 여 작업을 수행 하는 응용 프로그램을 지금 수행 하지 않습니다. 이는 간단한 "Hello World! 프로젝트를 시작 하 고 응용 프로그램을 시작 하는 것이 좋습니다.

[Microsoft Visual Web Developer 2010 Express ![](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

도구 모음에 대 한 "재생" 단추를 선택 합니다.

![디버그](getting-started-with-mvc-part1/_static/image11.png)

프로그램을 컴파일하고 웹 브라우저에서 응용 프로그램을 시작 하는 오른쪽을 가리키는 녹색 화살표입니다.

*참고: 대신 키보드에서 F5 키를 누르거나 디버그-&gt;"디버그" 메뉴에서 디버깅 시작을 선택할 수 있습니다.*

이렇게 하면 Visual Web Developer에서 개발 웹 서버를 시작 하 고 웹 응용 프로그램을 실행 합니다 .이를 사용 하도록 설정 하는 데 필요한 구성 또는 수동 단계가 없습니다. 그런 다음 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 검색 하도록 구성 합니다. 아래에서 브라우저의 주소 표시줄에는 "localhost"가 표시 되 고 example.com와 같은 것은 아닙니다. Localhost는 항상 자신의 로컬 컴퓨터를 가리키지만 (이 경우 방금 빌드한 응용 프로그램을 실행 하는 경우).

[![홈페이지](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

기본적으로이 기본 템플릿은 방문할 두 페이지와 기본 로그인 페이지를 제공 합니다. 이 응용 프로그램의 작동 방식을 변경 하 고 프로세스에서 ASP.NET MVC에 대해 약간의 방법을 살펴보겠습니다. 브라우저를 닫고 일부 코드를 변경할 수 있습니다.

> [!div class="step-by-step"]
> [다음](getting-started-with-mvc-part2.md)
