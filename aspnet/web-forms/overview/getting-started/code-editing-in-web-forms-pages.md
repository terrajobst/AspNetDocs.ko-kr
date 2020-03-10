---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: Visual Studio 2013의 코드 편집 ASP.NET Web Forms Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 3473ad476fbbebc58e12586334b4600f57cf17ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513641"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a>Visual Studio 2013의 코드 편집 ASP.NET Web Forms

[Erik Reitan](https://github.com/Erikre)

많은 ASP.NET Web Form 페이지에서 Visual Basic, C#또는 다른 언어로 코드를 작성 합니다. Visual Studio의 코드 편집기는 오류를 방지 하는 동시에 코드를 신속 하 게 작성 하는 데 도움이 될 수 있습니다. 또한 편집기에서는 재사용 가능한 코드를 만들어 수행 해야 하는 작업의 양을 줄이는 방법을 제공 합니다.

이 연습에서는 Visual Studio 코드 편집기의 다양 한 기능을 보여 줍니다.

이 연습에서는 다음 작업을 수행하는 방법을 배웁니다.

- 인라인 코딩 오류를 수정 합니다.
- 코드 리팩터링 및 이름 바꾸기
- 변수 및 개체의 이름을 바꿉니다.
- 코드 조각을 삽입 합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 연습을 완료하려면 다음이 필요합니다.

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 또는 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web). .NET Framework 자동으로 설치 됩니다. 

    > [!NOTE] 
    > 
    > Microsoft Visual Studio 2013 및 Microsoft Visual Studio Express 2013은이 자습서 시리즈 전체에서 Visual Studio 라고도 합니다.  
    >   
    > Visual Studio를 사용 하는 경우이 연습에서는 Visual Studio를 처음 시작할 때 **웹 개발** 설정 컬렉션을 선택 했다고 가정 합니다. 자세한 내용은 [방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)을 참조 하세요.

## <a name="creating-a-web-application-project-and-a-page"></a>웹 응용 프로그램 프로젝트 및 페이지 만들기

<a id="sectionToggle0"></a>

이 연습 부분에서는 웹 응용 프로그램 프로젝트를 만들고 여기에 새 페이지를 추가 합니다.

### <a name="to-create-a-web-application-project"></a>웹 응용 프로그램 프로젝트를 만들려면

1. Microsoft Visual Studio를 엽니다.
2. **파일** 메뉴에서 **새 프로젝트**를 선택합니다.  
    ![파일 메뉴](code-editing-in-web-forms-pages/_static/image1.png)

    **새 프로젝트** 대화 상자가 나타납니다.
3. 왼쪽에 있는  **C# Visual** -&gt; **웹** 템플릿 그룹 &gt; -**템플릿을** 선택 합니다.
4. 가운데 열에서 **ASP.NET 웹 애플리케이션** 템플릿을 선택합니다.
5. 프로젝트 이름을 ***BasicWebApp*** 로 하 고 **확인** 단추를 클릭 합니다.   
![새 프로젝트 대화 상자](code-editing-in-web-forms-pages/_static/image2.png)
6. 그런 다음 **Web Forms** 템플릿을 선택 하 고 **확인** 단추를 클릭 하 여 프로젝트를 만듭니다.  
![새 ASP.NET 프로젝트 대화 상자](code-editing-in-web-forms-pages/_static/image3.png)  

    Visual Studio는 Web Forms 템플릿을 기반으로 하는 미리 작성 된 기능을 포함 하는 새 프로젝트를 만듭니다.

## <a name="creating-a-new-aspnet-web-forms-page"></a>새 ASP.NET Web Forms 페이지 만들기

**ASP.NET 웹 응용 프로그램** 프로젝트 템플릿을 사용 하 여 새 Web Forms 응용 프로그램을 만드는 경우 Visual Studio는 *default.aspx*라는 ASP.NET 페이지 (Web Forms 페이지) 뿐만 아니라 다른 여러 파일 및 폴더도 추가 합니다. *Default.aspx 페이지를* 웹 응용 프로그램의 홈 페이지로 사용할 수 있습니다. 그러나이 연습에서는 새 페이지를 만들고 작업 합니다.

### <a name="to-add-a-page-to-the-web-application"></a>웹 응용 프로그램에 페이지를 추가 하려면

1. **솔루션 탐색기**에서 웹 응용 프로그램 이름을 마우스 오른쪽 단추로 클릭 하 고 (이 자습서에서는 응용 프로그램 이름이 **basicwebsite 사이트인**경우) **추가** -&gt; **새 항목**을 클릭 합니다.   
**새 항목 추가** 대화 상자가 표시됩니다.
2. 왼쪽의 **Visual C#**  -&gt; **웹** 템플릿 그룹을 선택 합니다. 그런 다음 중간 목록에서 **Web Form** 을 선택 하 고 이름을 *firstwebpage .aspx*로 표시 합니다.   
    ![새 항목 추가 대화 상자](code-editing-in-web-forms-pages/_static/image4.png)
3. **추가** 를 클릭 하 여 Web Forms 페이지를 프로젝트에 추가 합니다.  
 Visual Studio에서 새 페이지를 만들어 엽니다.
4. 그런 다음이 새 페이지를 기본 시작 페이지로 설정 합니다. **솔루션 탐색기**에서 *firstwebpage 페이지 .aspx* 이라는 새 페이지를 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 선택 합니다. 다음에이 응용 프로그램을 실행 하 여 진행 상황을 테스트할 때 브라우저에이 새 페이지가 자동으로 표시 됩니다.

## <a name="correcting-inline-coding-errors"></a>인라인 코딩 오류 수정

Visual Studio의 코드 편집기를 사용 하면 코드를 작성할 때 오류를 방지할 수 있으며 오류가 발생 한 경우 코드 편집기에서 오류를 수정 하는 데 도움이 됩니다. 이 연습 부분에서는 편집기에서 오류 수정 기능을 설명 하는 코드 줄을 작성 합니다.

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a>Visual Studio에서 간단한 코딩 오류를 해결 하려면

1. **디자인** 뷰에서 빈 페이지를 두 번 클릭 하 여 페이지에 대 한 **로드** 이벤트에 대 한 처리기를 만듭니다.   
   일부 코드를 작성 하는 위치로만 이벤트 처리기를 사용 합니다.
2. 처리기 내에 오류가 포함 된 다음 줄을 입력 하 **고 enter 키를 누릅니다.**

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   **Enter**키를 누르면 코드 편집기는 문제가 있는 코드 영역에서 녹색 및 빨강 밑줄 (일반적으로 &quot;물결 무늬&quot; 줄)을 배치 합니다. 녹색 밑줄은 경고를 나타냅니다. 빨간색 밑줄은 수정 해야 하는 오류를 나타냅니다. 

    `myStr` 위에 마우스 포인터를 놓으면 경고에 대해 알려 주는 도구 설명을 볼 수 있습니다. 또한 빨간색 밑줄 위에 마우스 포인터를 놓으면 오류 메시지가 표시 됩니다.

    다음 그림에서는 밑줄이 있는 코드를 보여 줍니다.

    ![디자인 뷰의 환영 텍스트](code-editing-in-web-forms-pages/_static/image5.png "디자인 뷰의 환영 텍스트")  
   줄의 끝에 세미콜론 `;`을 추가 하 여 오류를 수정 해야 합니다. 이 경고는 `myStr` 변수를 아직 사용 하지 않았음을 알려 줍니다.  

    > [!NOTE] 
    > 
    > Visual Studio에서 **도구** -&gt; **옵션** -&gt; **글꼴 및 색**을 선택 하 여 현재 코드 서식 설정을 볼 수 있습니다.

## <a name="refactoring-and-renaming"></a>리팩터링 및 이름 바꾸기

리팩터링은 기능을 유지 하면서 이해 하 고 유지 관리 하기 쉽도록 코드를 재구성 하는 소프트웨어 방법입니다. 간단한 예제는 이벤트 처리기에서 코드를 작성 하 여 데이터베이스에서 데이터를 가져오는 것입니다. 페이지를 개발할 때 다양 한 처리기에서 데이터에 액세스 해야 하는 것을 알 수 있습니다. 따라서 페이지에서 데이터 액세스 메서드를 만들고 처리기의 메서드에 호출을 삽입 하 여 페이지의 코드를 리팩터링 합니다.

코드 편집기에는 다양 한 리팩터링 작업을 수행 하는 데 도움이 되는 도구가 포함 되어 있습니다. 이 연습에서는 변수의 이름을 바꾸고 메서드를 추출 하는 두 가지 리팩터링 기법을 사용 합니다. 기타 리팩터링 옵션으로는 필드 캡슐화, 지역 변수를 메서드 매개 변수로 승격, 메서드 매개 변수 관리 등이 있습니다. 이러한 리팩터링 옵션의 사용 가능 여부는 코드의 위치에 따라 달라 집니다.

### <a name="refactoring-code"></a>리팩터링 코드

일반적인 리팩터링 시나리오는 메서드와 같이 다른 멤버 내에 있는 코드에서 메서드를 생성 (추출) 하는 것입니다. 이렇게 하면 원래 멤버의 크기가 줄어들고 추출 된 코드를 다시 사용할 수 있습니다.

이 연습 부분에서는 몇 가지 간단한 코드를 작성 한 다음 해당 코드에서 메서드를 추출 합니다. 리팩터링은에 대해 C#지원 되므로 프로그래밍 언어로를 사용 C# 하는 페이지를 만듭니다.

### <a name="to-extract-a-method-in-a-c-page"></a>C# 페이지에서 메서드를 추출 하려면

1. **디자인** 뷰로 전환 합니다.
2. **도구 상자**의 **표준** 탭에서 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤을 페이지로 끌어 옵니다.
3. **단추** 컨트롤을 두 번 클릭 하 여 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트에 대 한 처리기를 만든 후 다음 강조 표시 된 코드를 추가 합니다.

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   이 코드는 **arraylist** 개체를 만들고 루프를 사용 하 여 값을 로드 한 다음 다른 루프를 사용 하 여 **arraylist** 개체의 내용을 표시 합니다.
4. **Ctrl + F5** 키를 눌러 페이지를 실행 한 후 **단추** 를 클릭 하 여 다음 출력이 표시 되는지 확인 합니다.   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. 코드 편집기로 돌아간 다음 이벤트 처리기에서 다음 줄을 선택 합니다.   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. 선택 항목을 마우스 오른쪽 단추로 클릭 하 고 **리팩터링**을 클릭 한 다음 **메서드 추출**을 선택 합니다. 

    **메서드 추출** 대화 상자가 나타납니다.
7. **새 메서드 이름** 상자에 **displayarray**를 입력 한 다음 **확인**을 클릭 합니다. 

    코드 편집기는 `DisplayArray`이라는 새 메서드를 만들고 루프의 원래 위치에 있는 **클릭** 처리기에 새 메서드에 대 한 호출을 삽입 합니다.

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. **Ctrl + F5** 키를 눌러 페이지를 다시 실행 하 고 **단추**를 클릭 합니다.

    페이지는 이전과 동일 하 게 작동 합니다. 이제 page 클래스의 어디에서 든 `DisplayArray` 메서드를 호출할 수 있습니다.

## <a name="renaming-variables"></a>변수 이름 바꾸기

변수 및 개체를 사용 하는 경우 코드에서 이미 참조 된 개체의 이름을 바꿀 수 있습니다. 그러나 참조 중 하나의 이름을 바꾸지 않으면 변수와 개체의 이름을 바꾸면 코드가 중단 될 수 있습니다. 따라서 리팩터링을 사용 하 여 이름을 바꿀 수 있습니다.

### <a name="to-use-refactoring-to-rename-a-variable"></a>리팩터링을 사용 하 여 변수 이름을 바꾸려면

1. **Click** 이벤트 처리기에서 다음 줄을 찾습니다.

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. `alist`변수 이름을 마우스 오른쪽 단추로 클릭 하 고 **리팩터링**을 선택한 다음 **이름 바꾸기**를 선택 합니다.

    **이름 바꾸기** 대화 상자가 나타납니다.
3. **새 이름** 상자에 **ArrayList1** 을 입력 하 고 **참조 변경 내용 미리 보기** 확인란을 선택 했는지 확인 합니다. 그런 후 **OK**를 클릭합니다.

    **변경 내용 미리 보기** 대화 상자가 나타나고 이름을 바꿀 변수에 대 한 모든 참조를 포함 하는 트리가 표시 됩니다.
4. **적용** 을 클릭 하 여 **변경 내용 미리 보기** 대화 상자를 닫습니다.

    사용자가 선택한 인스턴스에 대해 구체적으로 참조 하는 변수는 이름이 바뀝니다. 그러나 다음 줄에 `alist` 변수는 이름이 바뀌지 않습니다.

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    이 줄의 `alist` 변수는 이름을 바꾼 `alist` 변수의 값과 동일한 값을 나타내지 않으므로 이름이 바뀌지 않습니다. `DisplayArray` 선언에서 `alist` 변수는 해당 메서드에 대 한 지역 변수입니다. 이는 리팩터링을 사용 하 여 변수 이름을 바꾸는 것은 단순히 편집기에서 찾기 및 바꾸기 작업을 수행 하는 것과는 다른 것을 보여 줍니다. 리팩터링은 작업 중인 변수의 의미 체계에 대 한 정보로 변수 이름을 바꿉니다.

## <a name="inserting-snippets"></a>조각 삽입

Web Forms 개발자가 자주 수행 해야 하는 많은 코딩 태스크가 있기 때문에 코드 편집기는 코드 조각 라이브러리 또는 미리 작성 된 코드 블록을 제공 합니다. 이러한 코드 조각을 페이지에 삽입할 수 있습니다.

Visual Studio에서 사용 하는 각 언어는 코드 조각을 삽입 하는 방법에 약간의 차이가 있습니다. 코드 조각을 삽입 하는 방법에 대 한 자세한 내용은 [Visual Basic IntelliSense 코드 조각](https://msdn.microsoft.com/library/18yz4be4.aspx)을 참조 하세요. 시각적 개체 C#에 코드 조각을 삽입 하는 방법에 대 한 자세한 내용은 [ C# 시각적 코드 조각](https://msdn.microsoft.com/library/z41h7fat.aspx)을 참조 하세요.

## <a name="next-steps"></a>다음 단계

이 연습에서는 코드에서 오류를 수정 하 고, 코드를 리팩터링 하 고, 변수 이름을 바꾸고, 코드 조각을 코드에 삽입 하기 위한 Visual Studio 2010 코드 편집기의 기본 기능을 보여 줍니다. 편집기의 추가 기능을 통해 응용 프로그램을 빠르고 쉽게 개발할 수 있습니다. 예를 들면 다음과 같습니다.

- Intellisense의 기능 (예: IntelliSense 옵션 수정, 코드 조각 관리 및 온라인으로 코드 조각 검색)에 대해 자세히 알아보세요. 자세한 내용은 [IntelliSense 사용](https://msdn.microsoft.com/library/hcw1s69b.aspx)을 참조하세요.
- 사용자 고유의 코드 조각을 만드는 방법을 알아봅니다. 자세한 내용은 [IntelliSense 코드 조각 만들기 및 사용](https://msdn.microsoft.com/library/ms165392.aspx) 을 참조 하세요.
- 코드 조각의 Visual Basic 특정 기능 (예: 코드 조각 사용자 지정 및 문제 해결)에 대해 자세히 알아보세요. 자세한 내용은 [Visual Basic IntelliSense 코드 조각](https://msdn.microsoft.com/library/18yz4be4.aspx) 을 참조 하세요.
- 리팩터링, 코드 조각 C#등 IntelliSense의 특정 기능에 대해 자세히 알아보세요. 자세한 내용은 [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)를 참조 하세요.
