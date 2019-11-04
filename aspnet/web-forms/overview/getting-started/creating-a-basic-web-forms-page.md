---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: Visual Studio 2013를 사용 하 여 기본 ASP.NET 4.5 Web Forms 페이지 만들기
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 5d13a51128eecd92a82cfd06054448582a348e11
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445683"
---
# <a name="using-visual-studio-2013-to-create-a-basic-aspnet-45-web-forms-page"></a>Visual Studio 2013를 사용 하 여 기본 ASP.NET 4.5 Web Forms 페이지 만들기

[Erik Reitan](https://github.com/Erikre)

[!INCLUDE[](~/includes/rp.md)]

이 연습에서는 [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 의 웹 개발 환경에 대 한 소개와 [웹 Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web)를 제공 합니다. 이 연습에서는 간단한 ASP.NET Web Forms 페이지를 만드는 과정을 안내 하 고 새 페이지를 만들고 컨트롤을 추가 하 고 코드를 작성 하는 기본적인 기술을 보여 줍니다.

이 연습에서 설명하는 작업은 다음과 같습니다.

- 응용 프로그램 프로젝트 Web Forms 파일 시스템을 만듭니다.
- Visual Studio를 사용 하 여 직접 익숙해질.
- ASP.NET 페이지 만들기
- 컨트롤 추가
- 이벤트 처리기를 추가 합니다.
- Visual Studio에서 페이지를 실행 하 고 테스트 합니다.

## <a name="prerequisites"></a>Prerequisites

이 연습을 완료하려면 다음 사항이 필요합니다.

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 또는 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web). .NET Framework 자동으로 설치 됩니다. 

    > [!NOTE] 
    > 
    > Microsoft Visual Studio 2013 및 Microsoft Visual Studio Express 2013은이 자습서 시리즈 전체에서 Visual Studio 라고도 합니다.  
    >   
    > Visual Studio를 사용 하는 경우이 연습에서는 Visual Studio를 처음 시작할 때 **웹 개발** 설정 컬렉션을 선택 했다고 가정 합니다. 자세한 내용은 [방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)을 참조 하세요.

## <a name="creating-a-web-application-project-and-a-page"></a>웹 응용 프로그램 프로젝트 및 페이지 만들기

<a id="sectionToggle0"></a>

이 연습 부분에서는 웹 응용 프로그램 프로젝트를 만들고 여기에 새 페이지를 추가 합니다. 또한 HTML 텍스트를 추가 하 고 브라우저에서 페이지를 실행 합니다.

### <a name="to-create-a-web-application-project"></a>웹 응용 프로그램 프로젝트를 만들려면

1. Microsoft Visual Studio를 엽니다.
2. **파일** 메뉴에서 **새 프로젝트**를 선택합니다.  
    ![파일 메뉴](creating-a-basic-web-forms-page/_static/image1.png)

    **새 프로젝트** 대화 상자가 나타납니다.
3. 왼쪽에 있는  **C# Visual** -&gt; **웹** 템플릿 그룹 &gt; -**템플릿을** 선택 합니다.
4. 가운데 열에서 **ASP.NET 웹 응용 프로그램** 템플릿을 선택 합니다.
5. 프로젝트 이름을 ***BasicWebApp*** 로 하 고 **확인** 단추를 클릭 합니다.   
![새 프로젝트 대화 상자](creating-a-basic-web-forms-page/_static/image2.png)
6. 그런 다음 **Web Forms** 템플릿을 선택 하 고 **확인** 단추를 클릭 하 여 프로젝트를 만듭니다.  
![새 ASP.NET 프로젝트 대화 상자](creating-a-basic-web-forms-page/_static/image3.png)  

    Visual Studio는 Web Forms 템플릿을 기반으로 하는 미리 작성 된 기능을 포함 하는 새 프로젝트를 만듭니다. 이 도구는 *홈페이지로* *된 .Aspx 페이지* , *연락처 .aspx* 페이지를 제공할 뿐만 아니라 사용자를 등록 하 고 사용자의 웹 사이트에 로그인 할 수 있도록 자격 증명을 저장 하는 멤버 자격 기능도 포함 하 고 있습니다. 새 페이지를 만들면 기본적으로 Visual Studio에서 페이지의 HTML 요소를 볼 수 있는 **소스** 뷰에 페이지를 표시 합니다. 다음 그림에서는 *BasicWebApp*이라는 새 웹 페이지를 만든 경우 **소스** 뷰에서 볼 수 있는 내용을 보여 줍니다.  
    ![소스 뷰](creating-a-basic-web-forms-page/_static/image4.png)

### <a name="a-tour-of-the-visual-studio-web-development-environment"></a>Visual Studio 웹 개발 환경 둘러보기

페이지를 수정 하 여 계속 진행 하기 전에 Visual Studio 개발 환경을 익히는 것이 좋습니다. 다음 그림에서는 Visual Studio 및 웹에 대 한 Visual Studio Express에서 사용할 수 있는 창과 도구를 보여 줍니다.

> [!NOTE] 
> 
> 이 다이어그램은 기본 창 및 창 위치를 보여 줍니다. **보기** 메뉴를 사용 하 여 추가 창을 표시 하 고 기본 설정에 맞게 창을 다시 정렬 하 고 크기를 조정할 수 있습니다. 창 정렬이 이미 변경 된 경우 표시 되는 내용은 그림과 일치 하지 않습니다.

 Visual Studio 환경

![Visual Studio 환경](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a>웹 디자이너 숙지

위의 그림을 검토 하 고 가장 일반적으로 사용 되는 windows 및 도구에 대해 설명 하는 텍스트를 다음 목록과 일치 시킵니다. (표시 되는 모든 창 및 도구는 여기에 나열 되어 있지 않으며 앞의 그림에 표시 된 도구에만 표시 됩니다.)

- 모음만. 텍스트 서식 지정, 텍스트 찾기 등을 위한 명령을 제공 합니다. 일부 도구 모음은 **디자인** 뷰에서 작업 하는 경우에만 사용할 수 있습니다.
- **솔루션 탐색기** 창. 웹 응용 프로그램의 파일과 폴더를 표시 합니다.
- 문서 창. 탭 창에서 작업 하는 문서를 표시 합니다. 탭을 클릭 하 여 문서 간을 전환할 수 있습니다.
- **속성** 창. 페이지, HTML 요소, 컨트롤 및 기타 개체에 대 한 설정을 변경할 수 있습니다.
- 보기 탭. 동일한 문서에 대 한 다양 한 보기를 제공 합니다. **디자인** 뷰는 근접 한 WYSIWYG 편집 화면입니다. **원본** 뷰는 페이지에 대 한 HTML 편집기입니다. **분할** 뷰는 문서의 **디자인** 뷰와 **소스** 뷰를 모두 표시 합니다. 이 연습의 뒷부분에서 **디자인** 및 **소스** 뷰를 사용 하 게 됩니다. **디자인** 뷰에서 웹 페이지를 열려면 **도구** 메뉴에서 **옵션**을 클릭 하 고 **HTML 디자이너** 노드를 선택 하 고 옵션 **의 시작 페이지** 를 변경 합니다.
- **도구 상자**. 페이지로 끌어올 수 있는 컨트롤과 HTML 요소를 제공 합니다. **도구 상자** 요소는 일반적인 함수를 기준으로 그룹화 됩니다.
- S **Erver 탐색기**. 데이터베이스 연결을 표시 합니다. 서버 탐색기 표시 되지 않으면 보기 메뉴에서 서버 탐색기를 클릭 합니다.

### <a name="creating-a-new-aspnet-web-forms-page"></a>새 ASP.NET Web Forms 페이지 만들기

**ASP.NET 웹 응용 프로그램** 프로젝트 템플릿을 사용 하 여 새 Web Forms 응용 프로그램을 만드는 경우 Visual Studio는 *default.aspx*라는 ASP.NET 페이지 (Web Forms 페이지) 뿐만 아니라 다른 여러 파일 및 폴더도 추가 합니다. *Default.aspx 페이지를* 웹 응용 프로그램의 홈 페이지로 사용할 수 있습니다. 그러나이 연습에서는 새 페이지를 만들고 작업 합니다.

### <a name="to-add-a-page-to-the-web-application"></a>웹 응용 프로그램에 페이지를 추가 하려면

1. *Default.aspx 페이지를* 닫습니다. 이렇게 하려면 파일 이름을 표시 하는 탭을 클릭 한 다음 닫기 옵션을 클릭 합니다.
2. **솔루션 탐색기**에서 웹 응용 프로그램 이름을 마우스 오른쪽 단추로 클릭 하 고 (이 자습서에서는 응용 프로그램 이름이 **basicwebsite 사이트인**경우) **추가** -&gt; **새 항목**을 클릭 합니다.   
**새 항목 추가** 대화 상자가 표시됩니다.
3. 왼쪽의 **Visual C#**  -&gt; **웹** 템플릿 그룹을 선택 합니다. 그런 다음 중간 목록에서 **Web Form** 을 선택 하 고 이름을 *firstwebpage .aspx*로 표시 합니다.   
    새 항목 추가 대화 상자 ![](creating-a-basic-web-forms-page/_static/image6.png)
4. **추가** 를 클릭 하 여 웹 페이지를 프로젝트에 추가 합니다.  
Visual Studio에서 새 페이지를 만들어 엽니다.

### <a name="adding-html-to-the-page"></a>페이지에 HTML 추가

이 연습 부분에서는 페이지에 정적 텍스트를 추가 합니다.

### <a name="to-add-text-to-the-page"></a>페이지에 텍스트를 추가 하려면

1. 문서 창의 맨 아래에서 **디자인** 탭을 클릭 하 여 **디자인** 뷰로 전환 합니다.

    디자인 뷰 현재 페이지를 WYSIWYG와 유사한 방식으로 표시 합니다. 이 시점에서 페이지에 텍스트 또는 컨트롤이 없으므로 사각형을 윤곽선으로 표시 하는 파선을 제외 하 고 페이지가 비어 있습니다. 이 사각형은 페이지의 **div** 요소를 나타냅니다.
2. 파선으로 윤곽이 설정 된 사각형 내부를 클릭 합니다.
3. **Visual Web Developer 시작을** 입력 하 고 **enter** 키를 두 번 누릅니다.

    다음 그림은 **디자인** 뷰에서 입력 한 텍스트를 보여 줍니다.

    ![디자인 뷰의 환영 텍스트](creating-a-basic-web-forms-page/_static/image7.png "디자인 뷰의 환영 텍스트")
4. **원본** 뷰로 전환 합니다.

    **디자인** 뷰에서 입력할 때 만든 **소스** 뷰에서 HTML을 볼 수 있습니다.  
    정적 텍스트를 사용 하 여 웹 페이지 ![](creating-a-basic-web-forms-page/_static/image8.png)

### <a name="running-the-page"></a>페이지 실행

페이지에 컨트롤을 추가 하 여 계속 진행 하기 전에 먼저 실행할 수 있습니다.

### <a name="to-run-the-page"></a>페이지를 실행 하려면

1. **솔루션 탐색기**에서 *firstwebpage 페이지 .aspx* 을 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 선택 합니다.
2. **Ctrl + F5** 키를 눌러 페이지를 실행 합니다.

    페이지가 브라우저에 표시 됩니다. 만든 페이지의 파일 이름 확장명은 *.aspx*이지만 현재는 HTML 페이지와 같은 방식으로 실행 됩니다.

    브라우저에 페이지를 표시 하려면 **솔루션 탐색기** 페이지를 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 보기**를 선택할 수도 있습니다.
3. 웹 응용 프로그램을 중지 하려면 브라우저를 닫습니다.

## <a name="adding-and-programming-controls"></a>컨트롤 추가 및 프로그래밍

<a id="sectionToggle1"></a>

이제 페이지에 서버 컨트롤을 추가 합니다. 단추, 레이블, 텍스트 상자 및 기타 친숙 한 컨트롤과 같은 서버 컨트롤은 Web Forms 페이지에 대 한 일반적인 양식 처리 기능을 제공 합니다. 그러나 클라이언트가 아닌 서버에서 실행 되는 코드를 사용 하 여 컨트롤을 프로그래밍할 수 있습니다.

[단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤, [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 컨트롤 및 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 컨트롤을 페이지에 추가 하 고 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤에 대 한 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트를 처리 하는 코드를 작성 합니다.

### <a name="to-add-controls-to-the-page"></a>페이지에 컨트롤을 추가 하려면

1. **디자인 탭을** 클릭 하 여 **디자인** 뷰로 전환 합니다.
2. **Visual Web Developer 시작** 텍스트의 끝에 삽입 지점을 놓고 5 번 이상 **enter** 키를 눌러 **div** 요소 상자에 공간을 만듭니다.
3. **도구 상자**에서 **표준** 그룹이 아직 확장 되지 않은 경우 확장 합니다.  
왼쪽의 **도구 상자** 창을 확장 하 여이를 확인 해야 할 수도 있습니다.
4. [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 컨트롤을 페이지로 끌어 첫 번째 줄에서 **Visual Web Developer를 시작** 하는 **div** 요소 상자의 가운데에 놓습니다.
5. [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤을 페이지로 끌어와 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 컨트롤의 오른쪽에 놓습니다.
6. [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 컨트롤을 페이지로 끌어 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤 아래의 별도 줄에 놓습니다.
7. [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 컨트롤 위에 삽입 지점을 넣은 다음 **이름 입력:** 을 입력 합니다.

    이 정적 HTML 텍스트는 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) 컨트롤의 캡션입니다. 동일한 페이지에서 정적 HTML과 서버 컨트롤을 혼합할 수 있습니다. 다음 그림에서는 **디자인** 뷰에 세 개의 컨트롤이 표시 되는 방법을 보여 줍니다.

    ![디자인 뷰의 세 가지 컨트롤](creating-a-basic-web-forms-page/_static/image9.png "디자인 뷰의 3가지 컨트롤")

### <a name="setting-control-properties"></a>컨트롤 속성 설정

Visual Studio는 페이지의 컨트롤 속성을 설정 하는 다양 한 방법을 제공 합니다. 이 연습 부분에서는 **디자인** 뷰와 **소스** 뷰 모두에서 속성을 설정 합니다.

### <a name="to-set-control-properties"></a>컨트롤 속성을 설정 하려면

1. 먼저 **보기** 메뉴- **다른** 창 -&gt; **속성 창**에서&gt; 선택 하 여 **속성** 창을 표시 합니다. 또는 **F4** 를 선택 하 여 **속성** 창을 표시할 수 있습니다.
2. [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤을 선택한 다음 **속성** 창에서 **텍스트** 값을 **표시 이름**으로 설정 합니다. 입력 한 텍스트는 다음 그림과 같이 디자이너의 단추에 표시 됩니다.

    ![단추 텍스트 설정](creating-a-basic-web-forms-page/_static/image10.png "단추 텍스트 설정")
3. **원본** 뷰로 전환 합니다.

    **소스** 뷰는 서버 컨트롤에 대해 Visual Studio에서 만든 요소를 포함 하 여 페이지에 대 한 HTML을 표시 합니다. 태그는 **asp:** 접두사를 사용 하 고 **runat =&quot;server&quot;** 특성을 포함 한다는 점을 제외 하 고는 HTML과 같은 구문을 사용 하 여 컨트롤을 선언 합니다.

    컨트롤 속성은 특성으로 선언 됩니다. 예를 들어 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤의 [text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) 속성을 설정 하는 경우 1 단계에서는 실제로 컨트롤 태그의 **텍스트** 특성을 설정 했습니다.

    > [!NOTE] 
    > 
    > 모든 컨트롤이 **runat =&quot;server&quot;** 특성도 포함 하는 **form** 요소 내에 있습니다. **Runat =&quot;server&quot;** 특성 및 asp.net 태그의 **asp:** 접두사는 페이지가 실행 될 때 서버에서 ASP.NET에 의해 처리 되도록 컨트롤을 표시 합니다. **&lt;폼 runat =&quot;server&quot;&gt;** 및 **&lt;스크립트 runat =&quot;server&quot;&gt;** 요소가 브라우저에 변경 되지 않은 상태로 전송 됩니다. 따라서 ASP.NET 코드는 요소 내에 있어야 합니다. 여는 태그에 **runat =&quot;server&quot;** 특성이 포함 되어 있습니다.
4. 다음에는 [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 컨트롤에 추가 속성을 추가 합니다. **&lt;asp: label&gt;** 태그에서 **asp: label** 바로 뒤에 삽입 지점을 넣은 다음 **스페이스바**를 누릅니다.

    [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 컨트롤에 대해 설정할 수 있는 사용 가능한 속성 목록을 표시 하는 드롭다운 목록이 나타납니다. **IntelliSense**라고 하는이 기능을 사용 하면 페이지의 서버 컨트롤, HTML 요소 및 기타 항목의 구문을 사용 하 여 **소스** 뷰에 쉽게 연결할 수 있습니다. 다음 그림에서는 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 컨트롤의 **IntelliSense** 드롭다운 목록을 보여 줍니다.

    ![IntelliSense 특성](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense 특성")
5. **ForeColor** 를 선택 하 고 등호를 입력 합니다.

    IntelliSense는 색 목록을 표시 합니다.

    > [!NOTE] 
    > 
    > 코드를 볼 때 **CTRL + J** 를 눌러 언제 든 지 **IntelliSense** 드롭다운 목록을 표시할 수 있습니다.
6. **[레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** 컨트롤의 텍스트에 대 한 색을 선택 합니다. 흰색 배경에서 읽을 수 있을 정도로 어두운 색을 선택 해야 합니다.

    **ForeColor** 특성은 닫는 따옴표를 포함 하 여 선택한 색으로 완료 됩니다.

### <a name="programming-the-button-control"></a>Button 컨트롤 프로그래밍

이 연습에서는 사용자가 텍스트 상자에 입력 한 이름을 읽은 다음 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 컨트롤에 이름을 표시 하는 코드를 작성 합니다.

### <a name="add-a-default-button-event-handler"></a>기본 단추 이벤트 처리기 추가

1. **디자인** 뷰로 전환 합니다.
2. [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤을 두 번 클릭 합니다.

    기본적으로 Visual Studio는 코드 숨김으로 전환 하 고 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤의 기본 이벤트에 대 한 기본 이벤트 처리기 인 [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트를 만듭니다. 코드를 표시 하는 파일은 UI 태그 (예: HTML)를 서버 코드에서 분리 합니다 ( C#예:).   
   이 이벤트 처리기에 대 한 코드를 추가 하기 위해 커서가 배치 됩니다.

    > [!NOTE] 
    > 
    > **디자인** 뷰에서 컨트롤을 두 번 클릭 하는 것은 이벤트 처리기를 만들 수 있는 여러 방법 중 하나일 뿐입니다.
3. **Button1\_click** 이벤트 처리기 내에서 **Label1** 을 입력 한 다음 마침표 ( **.** )를 입력 합니다.

    레이블 (**Label1**)의 **ID** 다음에 마침표를 입력 하면 Visual Studio에서는 다음 그림과 같이 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 컨트롤에 사용할 수 있는 멤버 목록을 표시 합니다. 멤버는 일반적으로 속성, 메서드 또는 이벤트입니다.

    ![코드 보기의 IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "코드 보기의 IntelliSense")
4. 다음 코드 예제와 같이 읽도록 단추에 대 한 **Click** 이벤트 처리기를 마칩니다.

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. **솔루션 탐색기** 에서 *firstwebpage 페이지 .aspx* 을 마우스 오른쪽 단추로 클릭 하 고 **태그 보기**를 선택 하 여 HTML 태그의 **소스** 뷰를 보려면 다시 전환 합니다.
6. **&lt;asp: Button&gt;** 요소로 스크롤합니다. **&lt;asp: Button&gt;** 요소에는 이제 **Onclick =&quot;Button1 특성이 있습니다\_&quot;를 클릭** 합니다.

    이 특성은 이전 단계에서 코딩 한 처리기 메서드에 단추의 [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트를 바인딩합니다.

    이벤트 처리기 메서드에는 임의의 이름을 사용할 수 있습니다. 표시 되는 이름은 Visual Studio에서 만드는 기본 이름입니다. 중요 한 점은 HTML의 **OnClick** 특성에 사용 되는 이름이 코드 숨김으로 정의 된 메서드의 이름과 일치 해야 한다는 것입니다.

### <a name="running-the-page"></a>페이지 실행

이제 페이지에서 서버 컨트롤을 테스트할 수 있습니다.

### <a name="to-run-the-page"></a>페이지를 실행 하려면

1. **Ctrl + F5** 키를 눌러 브라우저에서 페이지를 실행 합니다. 오류가 발생 하는 경우 위의 단계를 다시 확인 합니다.
2. 텍스트 상자에 이름을 입력 하 고 **표시 이름** 단추를 클릭 합니다.

    입력 한 이름이 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 컨트롤에 표시 됩니다. 단추를 클릭 하면 페이지가 웹 서버에 게시 됩니다. 그런 다음 ASP.NET 페이지를 다시 만들고, 코드를 실행 하 고 (이 경우 [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤의 [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트 처리기 실행) 새 페이지를 브라우저에 보냅니다. 브라우저에서 상태 표시줄을 시청 하는 경우 단추를 클릭할 때마다 페이지에서 웹 서버에 대 한 왕복을 수행 하는 것을 확인할 수 있습니다.
3. 브라우저에서 페이지를 마우스 오른쪽 단추로 클릭 하 고 **소스 보기**를 선택 하 여 실행 중인 페이지의 원본을 확인 합니다.

    페이지 소스 코드에는 서버 코드가 없는 HTML이 표시 됩니다. 특히 **원본** 뷰에서 작업 하는 **&lt;asp:&gt;** 요소가 표시 되지 않습니다. 페이지가 실행 될 때 ASP.NET는 서버 컨트롤을 처리 하 고 컨트롤을 나타내는 함수를 수행 하는 페이지에 HTML 요소를 렌더링 합니다. 예를 들어 **&lt;asp: Button&gt;** 컨트롤은 HTML **&lt;입력 형식 =&quot;전송&quot;&gt;** 요소로 렌더링 됩니다.
4. 브라우저를 닫습니다.

## <a name="working-with-additional-controls"></a>추가 컨트롤 사용

<a id="sectionToggle2"></a>

이 연습 부분에서는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤을 사용 하 여 한 번에 한 달에 날짜를 표시 합니다. [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤은 작업 하는 단추, 텍스트 상자 및 레이블 보다 더 복잡 한 컨트롤이 며 서버 컨트롤의 추가 기능을 보여 줍니다.

이 섹션에서는 페이지에 [WebControls](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤을 추가 하 고 서식을 지정 합니다.

### <a name="to-add-a-calendar-control"></a>Calendar 컨트롤을 추가 하려면

1. Visual Studio에서 **디자인** 뷰로 전환 합니다.
2. **도구 상자**의 **표준** 섹션에서 [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤을 페이지로 끌어 다른 컨트롤이 포함 된 **div** 요소 아래에 놓습니다.

    달력의 스마트 태그 패널이 표시 됩니다. 패널에는 선택한 컨트롤에 대해 가장 일반적인 작업을 쉽게 수행할 수 있도록 하는 명령이 표시 됩니다. 다음 그림은 **디자인** 뷰에서 렌더링 되는 [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤을 보여 줍니다.

    ![디자인 뷰의 일정 컨트롤](creating-a-basic-web-forms-page/_static/image13.png "디자인 뷰의 Calendar 컨트롤")
3. 스마트 태그 패널에서 **자동 서식**을 선택 합니다.

    달력에 대 한 서식 지정 구성표를 선택할 수 있는 **자동 서식** 대화 상자가 표시 됩니다. 다음 그림에서는 [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤의 **자동 서식** 대화 상자를 보여 줍니다.

    ![자동 서식 대화 상자 (Calendar 컨트롤)](creating-a-basic-web-forms-page/_static/image14.png "자동 서식 대화 상자(Calendar 컨트롤)")
4. **구성표 선택** 목록에서 **단순** 을 선택 하 고 **확인**을 클릭 합니다.
5. **원본** 뷰로 전환 합니다.

    **&lt;asp: Calendar&gt;** 요소를 볼 수 있습니다. 이 요소는 앞에서 만든 단순 컨트롤의 요소 보다 훨씬 깁니다. 또한 다양 한 서식 설정을 나타내는 **&lt;WeekEndDayStyle&gt;** 와 같은 하위 요소도 포함 됩니다. 다음 그림에서는 **소스** 뷰의 [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤을 보여 줍니다. **소스** 뷰에 표시 되는 정확한 태그는 그림과 약간 다를 수 있습니다.

    ![소스 뷰의 Calendar 컨트롤](creating-a-basic-web-forms-page/_static/image15.png "소스 뷰의 Calendar 컨트롤")

### <a name="programming-the-calendar-control"></a>Calendar 컨트롤 프로그래밍

이 섹션에서는 [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤을 프로그래밍 하 여 현재 선택한 날짜를 표시 합니다.

### <a name="to-program-the-calendar-control"></a>Calendar 컨트롤을 프로그래밍 하려면

1. **디자인** 뷰에서 [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤을 두 번 클릭 합니다.

    새 이벤트 처리기가 만들어지고 *FirstWebPage.aspx.cs*이라는 코드 파일에 표시 됩니다.
2. 다음 코드를 사용 하 여 [Selectionchanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx) 이벤트 처리기를 완료 합니다.

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

    위의 코드는 레이블 컨트롤의 텍스트를 달력 컨트롤의 선택 된 날짜로 설정 합니다.

### <a name="running-the-page"></a>페이지 실행

이제 달력을 테스트할 수 있습니다.

### <a name="to-run-the-page"></a>페이지를 실행 하려면

1. **Ctrl + F5** 키를 눌러 브라우저에서 페이지를 실행 합니다.
2. 달력에서 날짜를 클릭 합니다.

    클릭 한 날짜가 [레이블](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) 컨트롤에 표시 됩니다.
3. 브라우저에서 페이지의 소스 코드를 봅니다.

    [달력](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) 컨트롤이 **테이블로**페이지에 렌더링 되었으며 각 날짜는 **td** 요소로 사용 됩니다.
4. 브라우저를 닫습니다.

## <a name="next-steps"></a>다음 단계

<a id="nextStepsToggle"></a>

이 연습에서는 Visual Studio 페이지 디자이너의 기본 기능을 보여 줍니다. 이제 Visual Studio에서 Web Forms 페이지를 만들고 편집 하는 방법을 이해 했으므로 다른 기능을 탐색 하는 것이 좋습니다. 예를 들어 다음을 수행 하는 것이 좋습니다.

- ASP.NET Web Forms에 대 한 자세한 내용은 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013를 시작](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)하는 단계별 자습서 시리즈를 수행 합니다.
- CSS 스타일 시트에 대해 자세히 알아보세요. 자세한 내용은 [CSS 개요 작업](https://msdn.microsoft.com/library/bb398931.aspx)을 참조 하세요.
