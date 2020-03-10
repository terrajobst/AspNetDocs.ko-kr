---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: HTML 편집기 컨트롤을 사용 어떻게 할까요?? (C#) | Microsoft Docs
author: microsoft
description: HTMLEditor은 도구 모음에서 단추를 통해 HTML 콘텐츠를 쉽게 만들고 편집할 수 있도록 하는 ASP.NET AJAX 컨트롤입니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: cb7d75b59b1361abeb6d3c38ad6e42e34d6e3f7b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78466607"
---
# <a name="how-do-i-use-the-html-editor-control-c"></a>HTML 편집기 컨트롤을 사용 어떻게 할까요?? (C#)

[Microsoft](https://github.com/microsoft) 에서

> HTMLEditor은 도구 모음에서 단추를 통해 HTML 콘텐츠를 쉽게 만들고 편집할 수 있도록 하는 ASP.NET AJAX 컨트롤입니다.

이 자습서의 목표는 AJAX 컨트롤 도구 키트에 포함 된 HTML 편집기 컨트롤의 개요를 제공 하는 것입니다. HTML 편집기에는 글꼴 크기 변경, 글꼴 선택, 배경색 변경, 전경색 수정, 링크 추가, 이미지 추가, 텍스트 맞춤 변경, 잘라내기, 복사 및 붙여넣기 작업 수행에 대 한 옵션이 포함 되어 있습니다 (그림 1 참조).

[HTML 편집기 ![](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)

**그림 01**: HTML 편집기 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-cs/_static/image2.png))

HTML 편집기를 사용 하면 디자인 모드를 사용 하 여 콘텐츠를 입력 하거나 HTML을 직접 입력할 수 있습니다. HTML 콘텐츠를 미리 볼 수 있는 옵션도 제공 됩니다 (그림 2 참조).

[![디자인, HTML 및 미리 보기 단추](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)

**그림 02**: 디자인, HTML 및 미리 보기 단추 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-cs/_static/image4.png))

이 자습서에서는 html 편집기를 표시 하는 방법, HTML 편집기에 표시 되는 도구 모음 단추를 사용자 지정 하는 방법 및 사이트 간 스크립팅 공격을 방지 하는 방법에 대해 알아봅니다.

## <a name="displaying-the-html-editor"></a>HTML 편집기 표시

ASP.NET 페이지에서 HTML 편집기를 사용 하려면 먼저 페이지에 ScriptManager 컨트롤을 추가 해야 합니다. ScriptManager 컨트롤은 Visual Studio/Visual Web Developer Express 도구 상자의 AJAX 확장 탭 아래에 있습니다.

페이지의 다른 컨트롤 앞에서 ScriptManager 컨트롤을 페이지 맨 위에 두어야 합니다. 예를 들어 서버 쪽 &lt;양식 열기&gt; 태그 바로 아래에이를 놓을 수 있습니다.

HTML 편집기 컨트롤은 나머지 AJAX 컨트롤 도구 키트 컨트롤과 함께 도구 상자에 있습니다. 편집기 컨트롤의 이름을 지정 합니다 (그림 3 참조).

[HTML 편집기 컨트롤 ![](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)

**그림 03**: HTML 편집기 컨트롤 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-cs/_static/image6.png))

HTML 편집기를 페이지로 끌어온 후에는 속성 시트에서 해당 속성을 설정할 수 있습니다. 예를 들어 일반적으로 Width 및 Height 속성을 설정 하려고 합니다. 목록 1은 HTML 편집기를 포함 하는 ASP.NET 페이지의 소스를 포함 합니다.

**목록 1-SimpleEditor .aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

목록 1의 페이지에는 HTML 편집기 컨트롤, 단추 컨트롤 및 리터럴 컨트롤이 포함 되어 있습니다. 단추를 클릭 하면 HTML 편집기의 내용이 리터럴 컨트롤에 표시 됩니다 (그림 4 참조).

[HTML 편집기를 사용 하 여 폼을 전송 ![](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)

**그림 04**: HTML 편집기를 사용 하 여 폼 제출 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-cs/_static/image8.png))

Html 편집기 콘텐츠 속성은 html 편집기에 입력 된 HTML 콘텐츠를 검색 하는 데 사용 됩니다. 이 HTML 콘텐츠에서 JavaScript를 포함할 수 있습니다. 다음 섹션에서는 JavaScript 삽입 공격을 방지 하는 방법에 대해 설명 합니다.

## <a name="customizing-the-html-editor-toolbar"></a>HTML 편집기 도구 모음 사용자 지정

편집기에 표시 되는 단추를 정확 하 게 사용자 지정할 수 있습니다. 예를 들어 html 탭을 제거 하 여 사용자가 HTML 편집기를 HTML 모드로 전환 하지 못하게 할 수 있습니다. 또는 사용자가 포럼 메시지 게시에서 너무 큰 텍스트를 만들지 못하도록 글꼴 크기 드롭다운 목록을 제거할 수 있습니다 (그림 5 참조).

[사용자 지정 된 HTML 편집기 ![](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)

**그림 05**: 사용자 지정 된 HTML 편집기 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-cs/_static/image10.png))

기본 편집기 클래스에서 새 HTML 편집기를 파생 시켜 도구 모음 단추를 사용자 지정할 수 있습니다. 예를 들어 목록 2의 사용자 지정 편집기에는 굵게 및 기울임꼴의 도구 모음 단추만 포함 되어 있습니다. 다른 모든 도구 모음 단추는 제거 되었습니다. 또한 HTML 탭은 편집기의 맨 아래에서 제거 되었지만 디자인 및 미리 보기 탭도 있습니다.

**목록 2-앱\_Code\CustomEditor.cs**

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

클래스가 자동으로 컴파일되도록 앱\_코드 폴더에 목록 2의 클래스를 추가 해야 합니다. 앱\_코드 폴더가 웹 사이트에 없으면 폴더를 추가 하기만 하면 됩니다.

사용자 지정 편집기를 만든 후에는 일반 HTML 편집기를 추가할 때와 같은 방법으로 ASP.NET 페이지에 추가할 수 있습니다 (목록 3 참조).

**목록 3-ShowCustomEditor**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>XSS (교차 사이트 스크립팅) 공격 방지

사용자의 입력을 허용 하 고 웹 사이트에서 해당 입력을 다시 표시할 때마다 사이트 간 스크립팅 (XSS) 공격에 대해 웹 사이트를 열 수도 있습니다. 이론적으로 악의적인 해커가 입력이 다시 표시 될 때 실행 되는 JavaScript 코드를 제출할 수 있습니다. JavaScript는 사용자 암호 또는 기타 중요 한 정보를 도용 하는 데 사용할 수 있습니다.

일반적으로 웹 페이지에 표시 하기 전에 사용자가 검색 한 모든 입력을 HTML 인코딩으로 인코딩하여 XSS 공격을 쉽게 수행할 수 있습니다. 그러나 html 편집기의 출력을 HTML로 인코딩하면 &lt;스크립트&gt; 태그로 인코딩될 뿐만 아니라 모든 HTML 태그도 인코딩됩니다. 즉, 글꼴 유형, 글꼴 크기, 배경색 등의 모든 서식이 손실 됩니다.

암호, 신용 카드 번호 및 주민 등록 번호와 같은 사용자의 중요 한 정보를 수집 하는 경우에는 HTML 편집기를 사용 하 여 사용자가 검색 한 인코딩된 콘텐츠를 표시 하면 안 됩니다. Html 콘텐츠를 표시 하지 않는 경우에만 html 편집기를 사용 해야 합니다. 그렇지 않으면 신뢰할 수 있는 당사자가 HTML 콘텐츠를 웹 사이트로 전송 합니다.

예를 들어 블로그 응용 프로그램을 만드는 중 이라고 가정 합니다. 이 경우 블로그 게시물을 작성할 때 HTML 편집기를 사용 하는 것이 좋습니다. 블로그 게시물을 제출 하는 유일한 사용자 이며 악의적인 JavaScript를 전송 하지 않고 직접 신뢰 하는 것입니다. 그러나 익명 사용자가 주석을 게시할 수 있도록 허용 하는 경우 HTML 편집기를 사용 하는 것은 의미가 없습니다. 사용자가 암호와 같은 중요 한 정보를 제출 하는 상황에서는 특히 주의 해야 합니다. 악의적인 사용자가 암호를 가로채기 위한 올바른 JavaScript를 포함 하는 주석을 게시할 수 있습니다.

## <a name="summary"></a>요약

이 자습서에서는 AJAX 컨트롤 도구 키트에 포함 된 HTML 편집기 컨트롤에 대 한 간략 한 개요를 제공 했습니다. HTML 편집기를 사용 하 여 사용자의 풍부한 콘텐츠를 수락 하 고 해당 콘텐츠를 서버에 제출 하는 방법을 배웠습니다. HTML 편집기에 표시 되는 도구 모음 단추를 사용자 지정 하는 방법에 대해서도 설명 합니다. 마지막으로, HTML 편집기를 사용 하 여 잠재적으로 악의적인 입력을 허용할 때 교차 사이트 스크립팅 공격을 방지 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [다음](how-do-i-use-the-html-editor-control-vb.md)
