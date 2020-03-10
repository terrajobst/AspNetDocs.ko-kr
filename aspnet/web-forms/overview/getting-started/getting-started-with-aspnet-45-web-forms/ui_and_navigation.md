---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
title: UI 및 탐색 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 5c76891d-e515-4885-b576-76bd2c494efe
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
msc.type: authoredcontent
ms.openlocfilehash: ac1dcaf1ba911fdcaeb3845c6836ec771733d93e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522905"
---
# <a name="ui-and-navigation"></a>UI 및 탐색

[Erik Reitan](https://github.com/Erikre)

[정문 장난감 샘플 프로젝트 (C#) 다운로드](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013 for Web을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. [소스 코드를 포함 C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 하는 Visual Studio 2013 프로젝트는이 자습서 계열과 함께 사용할 수 있습니다.

이 자습서에서는 기본 웹 응용 프로그램의 UI를 수정 하 여 정문 장난감 스토어 front 응용 프로그램의 기능을 지원 합니다. 또한 단순 및 데이터 바인딩 탐색을 추가 합니다. 이 자습서는 이전 자습서 인 "데이터 액세스 계층 만들기"를 기반으로 하며, 정문 장난감 자습서 시리즈의 일부입니다.

## <a name="what-youll-learn"></a>학습할 내용:

- 정문 장난감 스토어 front 응용 프로그램의 기능을 지원 하도록 UI를 변경 하는 방법입니다.
- 페이지 탐색을 포함 하도록 HTML5 요소를 구성 하는 방법입니다.
- 데이터 기반 컨트롤을 만들어 특정 제품 데이터로 이동 하는 방법
- Entity Framework Code First를 사용 하 여 만든 데이터베이스의 데이터를 표시 하는 방법입니다.

ASP.NET Web Forms를 사용 하 여 웹 응용 프로그램에 대 한 동적 콘텐츠를 만들 수 있습니다. 각 ASP.NET 웹 페이지는 정적 HTML 웹 페이지와 비슷한 방식으로 만들어지며 (서버 기반 처리를 포함 하지 않는 페이지) ASP.NET 웹 페이지에는 ASP.NET에서 인식할 수 있는 추가 요소와 페이지가 실행 될 때 HTML을 생성 하는 프로세스가 포함 됩니다.

정적 HTML 페이지 ( *.htm* 또는 *.html* 파일)를 사용 하 여 서버는 파일을 읽고 그대로 브라우저에 전송 하 여 `Web` 요청을 전달 합니다. 반면, 누군가가 ASP.NET 웹 페이지 ( *.aspx* 파일)를 요청 하는 경우 페이지는 웹 서버에서 프로그램으로 실행 됩니다. 페이지가 실행 되는 동안 값 계산, 데이터베이스 정보 읽기 또는 쓰기, 다른 프로그램 호출 등 웹 사이트에 필요한 모든 작업을 수행할 수 있습니다. 출력으로 페이지는 HTML의 요소와 같은 태그를 동적으로 생성 하 고이 동적 출력을 브라우저에 보냅니다.

## <a name="modifying-the-ui"></a>UI 수정

*Default.aspx 페이지를* 수정 하 여이 자습서 시리즈를 계속 합니다. 응용 프로그램을 만드는 데 사용 되는 기본 템플릿으로 이미 설정 된 UI를 수정 합니다. Web Forms 응용 프로그램을 만들 때 일반적으로 수행 하는 수정 유형이 있습니다. 제목을 변경 하 고 일부 내용을 바꾸고 불필요 한 기본 콘텐츠를 제거 하 여이 작업을 수행 합니다.

1. 을 열거나 *default.aspx 페이지로 전환 합니다.*
2. 페이지가 **디자인** 뷰에 표시 되 면 **소스** 뷰로 전환 합니다.
3. `@Page` 지시어의 페이지 맨 위에서 아래 노란색으로 강조 표시 된 것 처럼 `Title` 특성을 "시작"으로 변경 합니다. 

    [!code-aspx[Main](ui_and_navigation/samples/sample1.aspx?highlight=1)]
4. 또한 *default.aspx 페이지에서* 태그가 아래와 같이 표시 되도록 `<asp:Content>` 태그에 포함 된 모든 기본 콘텐츠를 바꿉니다. 

    [!code-aspx[Main](ui_and_navigation/samples/sample2.aspx)]
5. **파일** 메뉴에서 default.aspx **저장** 을 선택 하 여 *default.aspx 페이지를 저장 합니다.*

   그러면 생성 *되는 default.aspx 페이지가* 다음과 같이 표시 됩니다. 

[!code-aspx[Main](ui_and_navigation/samples/sample3.aspx)]

이 예제에서는 `@Page` 지시문의 `Title` 특성을 설정 했습니다. HTML이 브라우저에 표시 되 면 서버 코드 `<%: Page.Title %>` `Title` 특성에 포함 된 내용으로 확인 됩니다.

예제 페이지에는 ASP.NET 웹 페이지를 구성 하는 기본 요소가 포함 되어 있습니다. 이 페이지에는 HTML 페이지에서와 같이 ASP.NET 관련 된 요소와 함께 정적 텍스트가 포함 되어 있습니다. *Default.aspx 페이지에* 포함 된 콘텐츠는이 자습서의 뒷부분에서 설명 하는 마스터 페이지 콘텐츠와 통합 됩니다.

### <a name="page-directive"></a>@Page 지시문

ASP.NET Web Forms에는 일반적으로 페이지에 대 한 페이지 속성 및 구성 정보를 지정할 수 있는 지시문이 포함 되어 있습니다. 지시문은 ASP.NET에서 페이지를 처리 하는 방법에 대 한 지침으로 사용 되지만 브라우저에 전송 된 태그의 일부로 렌더링 되지 않습니다.

가장 일반적으로 사용 되는 지시문은 다음을 포함 하 여 페이지에 대 한 다양 한 구성 옵션을 지정할 수 있는 `@Page` 지시문입니다.

1. 페이지의 코드에 대 한 서버 프로그래밍 언어 (예: C#)입니다.
2. 페이지가 페이지에서 직접 서버 코드를 포함 하는 페이지 (단일 파일 페이지) 인지 여부 또는 별도의 클래스 파일에 있는 코드를 포함 하는 페이지 (코드를 포함 하는 페이지) 인지 여부입니다.
3. 페이지가 연결 된 마스터 페이지를 포함 하 고 있으므로 콘텐츠 페이지로 처리 되어야 하는지 여부입니다.
4. 디버깅 및 추적 옵션입니다.

페이지에 `@Page` 지시어를 포함 하지 않거나 지시문에 특정 설정이 포함 되어 있지 않은 경우에는 설정이 *web.config 구성 파일이* 나 *machine.config* 구성 파일에서 상속 됩니다. Machine.config *파일은* 컴퓨터에서 실행 되는 모든 응용 프로그램에 추가 구성 설정을 제공 합니다.

> [!NOTE] 
> 
> Machine.config *는 가능한* 모든 구성 설정에 대 한 세부 정보도 제공 합니다.

### <a name="web-server-controls"></a>웹 서버 컨트롤

대부분의 ASP.NET Web Forms 응용 프로그램에서는 사용자가 단추, 텍스트 상자, 목록 등의 페이지와 상호 작용할 수 있도록 하는 컨트롤을 추가 합니다. 이러한 웹 서버 컨트롤은 HTML 단추와 입력 요소와 유사 합니다. 그러나 서버에서 처리 되므로 서버 코드를 사용 하 여 속성을 설정할 수 있습니다. 이러한 컨트롤은 또한 서버 코드에서 처리할 수 있는 이벤트를 발생 시킵니다.

서버 컨트롤은 페이지가 실행 될 때 ASP.NET에서 인식 하는 특수 구문을 사용 합니다. ASP.NET 서버 컨트롤의 태그 이름은 `asp:` 접두사로 시작 합니다. 이를 통해 ASP.NET는 이러한 서버 컨트롤을 인식 하 고 처리할 수 있습니다. 컨트롤이 .NET Framework의 일부가 아닌 경우에는 접두사가 다를 수 있습니다. ASP.NET 서버 컨트롤에는 `asp:` 접두사 외에도 `runat="server"` 특성과 서버 코드에서 컨트롤을 참조 하는 데 사용할 수 있는 `ID` 포함 됩니다.

페이지가 실행 될 때 ASP.NET는 서버 컨트롤을 식별 하 고 해당 컨트롤과 연결 된 코드를 실행 합니다. 대부분의 컨트롤은 브라우저에 표시 될 때 일부 HTML 또는 기타 태그를 페이지에 렌더링 합니다.

### <a name="server-code"></a>서버 코드

대부분의 ASP.NET Web Forms 응용 프로그램에는 페이지가 처리 될 때 서버에서 실행 되는 코드가 포함 됩니다. 위에서 설명한 것 처럼 서버 코드를 사용 하 여 ListView 컨트롤에 데이터를 추가 하는 것과 같은 다양 한 작업을 수행할 수 있습니다. ASP.NET는, Visual Basic, j # 등을 비롯 하 C#여 서버에서 실행할 수 있는 여러 언어를 지원 합니다.

ASP.NET는 웹 페이지에 대 한 서버 코드를 작성 하기 위한 두 가지 모델을 지원 합니다. 단일 파일 모델에서 페이지의 코드는 여는 태그에 `runat="server"` 특성이 포함 된 script 요소에 있습니다. 또는 별도의 클래스 파일에서 페이지에 대 한 코드를 만들 수 있습니다. 이러한 코드는 코드 숨김이 모델 이라고 합니다. 이 경우 ASP.NET Web Forms 페이지에는 일반적으로 서버 코드가 포함 되지 않습니다. 대신, `@Page` 지시문에는 *.aspx* 페이지를 연결 된 코드 숨김이 있는 파일과 연결 하는 정보가 포함 되어 있습니다.

`@Page` 지시문에 포함 된 `CodeBehind` 특성은 별도 클래스 파일의 이름을 지정 하 고, `Inherits` 특성은 페이지에 해당 하는 코드를 포함 하는 파일 내에서 클래스의 이름을 지정 합니다.

### <a name="updating-the-master-page"></a>마스터 페이지 업데이트

ASP.NET Web Forms에서 마스터 페이지를 통해 애플리케이션의 페이지에 대한 일관된 레이아웃을 만들 수 있습니다. 단일 마스터 페이지는 애플리케이션의 모든 페이지(또는 페이지 그룹)에 대해 원하는 모양과 느낌 및 표준 동작을 정의합니다. 그런 다음 위에서 설명한 대로 표시 하려는 콘텐츠가 포함 된 개별 콘텐츠 페이지를 만들 수 있습니다. 사용자가 콘텐츠 페이지를 요청하면 ASP.NET이 마스터 페이지에 해당 페이지를 병합하여 콘텐츠 페이지의 콘텐츠와 마스터 페이지의 레이아웃을 결합하는 출력을 생성합니다.

새 사이트에는 모든 페이지에 표시할 단일 로고가 필요 합니다. 이 로고를 추가 하려면 마스터 페이지에서 HTML을 수정 하면 됩니다.

1. **솔루션 탐색기**에서 **Site.Master** 페이지를 찾아서 엽니다.
2. 페이지가 **디자인** 뷰에 있으면 **원본** 뷰로 전환 합니다.
3. 노란색으로 강조 표시 된 태그를 **수정 하거나 추가** 하 여 마스터 페이지를 업데이트 합니다. 

    [!code-aspx[Main](ui_and_navigation/samples/sample4.aspx?highlight=9,49,76-81,87)]

이 HTML은 나중에 추가 하는 웹 응용 프로그램의 *Images* 폴더에서 *로고나* 이라는 이미지를 표시 합니다. 마스터 페이지를 사용 하는 페이지가 브라우저에 표시 되 면 로고가 표시 됩니다. 사용자가 로고를 클릭 하면 *default.aspx* 페이지로 다시 이동 합니다. HTML 앵커 태그 `<a>` 이미지 서버 컨트롤을 래핑하고 링크의 일부로 이미지를 포함할 수 있도록 합니다. 앵커 태그의 `href` 특성은 웹 사이트의 루트 "`~/`"를 링크 위치로 지정 합니다. 기본적으로 사용자가 웹 사이트의 루트를 탐색할 때 *default.aspx 페이지가 표시* 됩니다. **이미지** `<asp:Image>` 서버 컨트롤에는 브라우저에 표시 될 때 HTML로 렌더링 되는 `BorderStyle`와 같은 추가 속성이 포함 됩니다.

### <a name="master-pages"></a>마스터 페이지

마스터 페이지는 정적 텍스트, HTML 요소 및 서버 컨트롤을 포함할 수 있는 미리 정의 된 레이아웃의 확장명이 .master (예: *site.master*) 인 ASP.NET 파일입니다. 마스터 페이지는 일반적인 *.aspx* 페이지에 사용 되는 `@Page` 지시문을 대체 하는 특별 한 `@Master` 지시문으로 식별 됩니다.

`@Master` 지시문 외에도 마스터 페이지에는 페이지에 대 한 모든 최상위 HTML 요소 (예: `html`, `head`및 `form`)가 포함 되어 있습니다. 예를 들어 위에서 추가한 마스터 페이지에서 레이아웃에 HTML `table`를 사용 하 고, 회사 로고에 대 한 `img` 요소, 정적 텍스트 및 서버 컨트롤을 사용 하 여 사이트의 공통 멤버 자격을 처리할 수 있습니다. HTML 및 ASP.NET 요소를 마스터 페이지의 일부로 사용할 수 있습니다.

모든 페이지에 표시 되는 정적 텍스트 및 컨트롤 외에도 마스터 페이지에는 **ContentPlaceHolder** 컨트롤이 하나 이상 포함 되어 있습니다. 이러한 자리 표시자 컨트롤은 대체 가능한 콘텐츠가 표시 되는 영역을 정의 합니다. 그러면 대체 가능한 콘텐츠가 **콘텐츠 서버 컨트롤을 사용** 하 여 *default.aspx*와 같은 콘텐츠 페이지에 정의 됩니다.

#### <a name="adding-image-files"></a>이미지 파일 추가

위에서 언급 한 로고 이미지를 모든 제품 이미지와 함께 웹 응용 프로그램에 추가 해야 브라우저가 브라우저에 표시 될 때 볼 수 있습니다.

#### <a name="download-from-msdn-samples-site"></a>MSDN 샘플 사이트에서 다운로드:

[ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작-동 장난감](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)

다운로드에는 샘플 응용 프로그램을 만드는 데 사용 되는 *WingtipToys (자산)* 폴더의 리소스가 포함 되어 있습니다.

1. 아직 수행 하지 않은 경우 MSDN 샘플 사이트에서 위의 링크를 사용 하 여 압축 된 샘플 파일을 다운로드 합니다.
2. 다운로드 한 후 .zip 파일을 열고 콘텐츠를 컴퓨터의 로컬 폴더에 복사 합니다.
3. *WingtipToys-자산* 폴더를 찾아 엽니다.
4. 끌어서 놓기를 통해 로컬 폴더의 *카탈로그* 폴더를 Visual Studio의 **솔루션 탐색기** 에 있는 웹 응용 프로그램 프로젝트의 루트에 복사 합니다. 

    ![UI 및 탐색-파일 복사](ui_and_navigation/_static/image1.png)
5. 그런 다음 **솔루션 탐색기** 에서 **WingtipToys** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **새 폴더**&gt; **추가** -를 선택 하 여 *이미지* 라는 새 폴더를 만듭니다.
6. **파일 탐색기** 의 *WingtipToys* 폴더에 있는 *로고 .jpg* 파일을 Visual Studio의 **솔루션 탐색기** 에 있는 웹 응용 프로그램 프로젝트의 *Images* 폴더로 복사 합니다.
7. 새 파일이 표시 되지 않는 경우 **솔루션 탐색기** 위쪽의 **모든 파일 표시** 옵션을 클릭 하 여 파일 목록을 업데이트 합니다.  
  
    이제 **솔루션 탐색기** 업데이트 된 프로젝트 파일을 표시 합니다. 

    ![UI 및 탐색-솔루션 탐색기](ui_and_navigation/_static/image2.png)

### <a name="adding-pages"></a>페이지 추가

웹 응용 프로그램에 탐색을 추가 하기 전에 먼저 탐색 하는 두 개의 새 페이지를 추가 합니다. 이 자습서 시리즈의 뒷부분에서는 이러한 새 페이지에 대 한 제품 및 제품 세부 정보를 표시 합니다.

1. **솔루션 탐색기**에서 **WingtipToys**을 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 항목**을 클릭 합니다.   
 **새 항목 추가** 대화 상자가 표시됩니다.
2. 왼쪽의 **Visual C#**  -&gt; **웹** 템플릿 그룹을 선택 합니다. 그런 다음 중간 목록에서 **마스터 페이지로 웹 폼** 을 선택 하 고 이름을 *ProductList*로 바꿉니다. 

    ![UI 및 탐색-새 항목 추가 대화 상자](ui_and_navigation/_static/image3.png)
3. 마스터 페이지를 새로 만든 *.aspx* 페이지에 연결 **하려면 site.master를 선택 합니다** . 

    ![UI 및 탐색-마스터 페이지 선택](ui_and_navigation/_static/image4.png)
4. 이와 동일한 단계를 수행 하 여 다음과 같은 추가 페이지를 추가 *합니다.*

### <a name="updating-bootstrap"></a>부트스트랩 업데이트 중

Visual Studio 2013 프로젝트 템플릿은 Twitter를 사용 하 여 생성 된 레이아웃 및 테마 프레임 워크인 [부트스트랩](http://getbootstrap.com/)을 사용 합니다. 부트스트랩은 CSS3를 사용 하 여 반응 형 디자인을 제공 합니다. 즉, 레이아웃이 여러 브라우저 창 크기에 맞게 동적으로 조정 될 수 있습니다. 부트스트랩의 테마 기능을 사용 하 여 응용 프로그램의 모양과 느낌을 쉽게 변경할 수도 있습니다. 기본적으로 Visual Studio 2013의 ASP.NET 웹 응용 프로그램 템플릿은 부트스트랩을 NuGet 패키지로 포함 합니다.

이 자습서에서는 부트스트랩 CSS 파일을 대체 하 여 정문 장난감 응용 프로그램의 모양과 느낌을 변경 합니다.

1. **솔루션 탐색기**에서 *콘텐츠* 폴더를 엽니다.
2. *부트스트랩 .css* 파일을 마우스 오른쪽 단추로 클릭 하 고 이름을 *bootstrap-original*로 바꿉니다.
3. *Bootstrap-original를* *로 이름을* 바꿉니다.
4. **솔루션 탐색기**에서 *콘텐츠* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **파일 탐색기에서 폴더 열기**를 선택 합니다.  
   파일 탐색기가 표시 됩니다. 다운로드 한 부트스트랩 CSS 파일을이 위치에 저장 합니다.
5. 브라우저에서 [https://bootswatch.com/3/](https://bootswatch.com/3/)로 이동 합니다.
6. 사용자 테마가 표시 될 때까지 브라우저 창을 스크롤합니다. 

    ![UI 및 탐색-Cerulean 테마](ui_and_navigation/_static/image5.png)
7. *부트스트랩 .css* 파일 및 *부트스트래핑. min .css* 파일을 모두 *Content* 폴더로 다운로드 합니다. 이전에 연 **파일 탐색기** 창에 표시 되는 콘텐츠 폴더에 대 한 경로를 사용 합니다.
8. **솔루션 탐색기**맨 위에 있는 **Visual Studio** 에서 **모든 파일 표시** 옵션을 선택 하 여 콘텐츠 폴더에 새 파일을 표시 합니다. 

    ![UI 및 탐색-솔루션 탐색기](ui_and_navigation/_static/image6.png)

   **Content** 폴더에 두 개의 새 CSS 파일이 표시 되지만 각 파일 이름 옆에 있는 아이콘은 회색으로 표시 됩니다. 이는 파일이 프로젝트에 아직 추가 되지 않았음을 의미 합니다.
9. *부트스트랩 .css* 및 *부트스트래핑.* m a m. m i m 파일을 마우스 오른쪽 단추로 클릭 하 고 **프로젝트에 포함**을 선택 합니다.   
   이 자습서의 뒷부분에서 정문 장난감 응용 프로그램을 실행 하면 새 UI가 표시 됩니다.

> [!NOTE] 
> 
> ASP.NET 웹 응용 프로그램 템플릿은 프로젝트의 루트에 있는 *번들 .config* 파일을 사용 하 여 부트스트랩 CSS 파일의 경로를 저장 합니다.

### <a name="modifying-the-default-navigation"></a>기본 탐색 수정

응용 프로그램의 모든 페이지에 대 한 기본 탐색은 *사이트 마스터* 페이지에 있는 순서가 지정 되지 않은 탐색 목록 요소를 변경 하 여 수정할 수 있습니다.

1. **솔루션 탐색기**에서 *사이트 마스터* 페이지를 찾아 엽니다.
2. 노란색으로 강조 표시 된 추가 탐색 링크를 아래 표시 된 순서가 지정 되지 않은 목록에 추가 합니다.   

    [!code-html[Main](ui_and_navigation/samples/sample5.html?highlight=5)]

위의 HTML에서 볼 수 있듯이 링크 `href` 특성 `<a>` 앵커 태그를 포함 하 `<li>` 각 줄 항목을 수정 했습니다. 각 `href`는 웹 응용 프로그램의 페이지를 가리킵니다. 브라우저에서 사용자가 이러한 링크 (예: **제품**) 중 하나를 클릭 하면 `href` (예: **ProductList**)에 포함 된 페이지로 이동 됩니다. 이 자습서의 끝 부분에서 응용 프로그램을 실행 합니다.

> [!NOTE] 
> 
> 물결표 (`~`) 문자는 `href` 경로가 프로젝트의 루트에서 시작 하도록 지정 하는 데 사용 됩니다.

### <a name="adding-a-data-control-to-display-navigation-data"></a>탐색 데이터를 표시 하는 데이터 컨트롤 추가

다음에는 데이터베이스의 모든 범주를 표시 하는 컨트롤을 추가 합니다. 각 범주는 *ProductList* 페이지에 대 한 링크 역할을 합니다. 사용자가 브라우저에서 범주 링크를 클릭 하면 제품 페이지로 이동 하 여 선택한 범주와 관련 된 제품만 확인 합니다.

**ListView** 컨트롤을 사용 하 여 데이터베이스에 포함 된 모든 범주를 표시 합니다. 마스터 페이지에 **ListView** 컨트롤을 추가 하려면 다음을 수행 합니다.

1. *Site.master* 페이지에서 앞서 추가한 `id="TitleContent"`를 포함 하는 `<div>` 요소 **뒤** 에 다음 강조 표시 된 `<div>` 요소를 추가 합니다.  

    [!code-aspx[Main](ui_and_navigation/samples/sample6.aspx?highlight=7-21)]

이 코드는 데이터베이스의 모든 범주를 표시 합니다. **ListView** 컨트롤은 각 범주 이름을 링크 텍스트로 표시 하 고, 범주 `ID`를 포함 하는 쿼리 문자열 값을 사용 하 여 *ProductList* 페이지에 대 한 링크를 포함 합니다. **ListView** 컨트롤에서 `ItemType` 속성을 설정 하 여 `ItemTemplate` 노드 내에서 데이터 바인딩 `Item` 식을 사용할 수 있고 컨트롤이 강력한 형식으로 설정 됩니다. IntelliSense를 사용 하 여 `CategoryName`를 지정 하는 것과 같은 `Item` 개체의 세부 정보를 선택할 수 있습니다. 이 코드는 데이터 바인딩 식을 표시 하는 컨테이너 `<%#: %>` 안에 포함 되어 있습니다. (:)을 추가 합니다. `<%#` 접두사의 끝에는 데이터 바인딩 식의 결과가 HTML로 인코딩됩니다. 결과가 HTML로 인코딩된 경우 응용 프로그램은 XSS (사이트 간 스크립트 삽입) 및 HTML 삽입 공격 으로부터 더 잘 보호 됩니다.

> [!NOTE] 
> 
> **팁**
> 
> 개발 중에를 입력 하 여 코드를 추가 하는 경우 강력한 형식의 데이터 컨트롤이 IntelliSense를 기준으로 사용 가능한 멤버를 표시 하기 때문에 개체의 유효한 멤버를 찾을 수 있습니다. IntelliSense는 속성, 메서드 및 개체와 같은 코드를 입력할 때 상황에 맞는 코드를 선택 합니다.

다음 단계에서는 `GetCategories` 메서드를 구현 하 여 데이터를 검색 합니다.

### <a name="linking-the-data-control-to-the-database"></a>데이터베이스에 데이터 컨트롤 연결

데이터 컨트롤에 데이터를 표시 하려면 데이터 컨트롤을 데이터베이스에 연결 해야 합니다. 링크를 만들려면 *Site.Master.cs* 파일의 코드를 수정할 수 있습니다.

1. **솔루션 탐색기**에서 *site.master* 페이지를 마우스 오른쪽 단추로 클릭 한 다음 **코드 보기**를 클릭 합니다. *Site.Master.cs* 파일이 편집기에서 열립니다.
2. *Site.Master.cs* 파일의 시작 부분에서 포함 된 모든 네임 스페이스가 다음과 같이 표시 되도록 두 개의 네임 스페이스를 추가 합니다.  

    [!code-csharp[Main](ui_and_navigation/samples/sample7.cs?highlight=8-9)]
3. 다음과 같이 강조 표시 된 `GetCategories` 메서드를 `Page_Load` 이벤트 처리기 뒤에 추가 합니다.  

    [!code-csharp[Main](ui_and_navigation/samples/sample8.cs?highlight=6-11)]

위의 코드는 마스터 페이지를 사용 하는 페이지가 브라우저에서 로드 될 때 실행 됩니다. 이 자습서의 앞부분에서 추가한 `ListView` 컨트롤 ("categoryList")은 모델 바인딩을 사용 하 여 데이터를 선택 합니다. `ListView` 컨트롤의 태그에서 컨트롤의 `SelectMethod` 속성을 위에 표시 된 `GetCategories` 메서드로 설정 합니다. `ListView` 컨트롤은 페이지 수명 주기에서 적절 한 시간에 `GetCategories` 메서드를 호출 하 고 반환 된 데이터를 자동으로 바인딩합니다. 데이터 바인딩에 대 한 자세한 내용은 다음 자습서를 통해 설명 합니다.

### <a name="running-the-application-and-creating-the-database"></a>응용 프로그램 실행 및 데이터베이스 만들기

이 자습서 시리즈의 앞부분에서 이니셜라이저 클래스 ("global.asax.cs")를 만들고이 클래스를 파일에 지정 했습니다. *Global.asax.cs* 파일에 포함 된 `Application_Start` 메서드가 이니셜라이저 클래스를 호출 하기 때문에 Entity Framework는 응용 프로그램이 처음으로 실행 될 때 데이터베이스를 생성 합니다. 이니셜라이저 클래스는이 자습서 시리즈의 앞부분에서 추가한 모델 클래스 (`Category` 및 `Product`)를 사용 하 여 데이터베이스를 만듭니다.

1. **솔루션 탐색기**에서 *default.aspx 페이지를* 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 선택 합니다.
2. Visual Studio에서 **f5**키를 누릅니다.   
 이 첫 번째 실행 중에 모든 항목을 설정 하는 데 약간의 시간이 걸립니다.   
    ![UI 및 탐색 브라우저 창](ui_and_navigation/_static/image7.png)  
 응용 프로그램을 실행 하면 응용 프로그램이 컴파일되고 *wingtiptoys* 라는 데이터베이스가 *App\_Data* 폴더에 생성 됩니다. 브라우저에 범주 탐색 메뉴가 표시 됩니다. 이 메뉴는 데이터베이스에서 범주를 검색 하 여 생성 되었습니다. 다음 자습서에서는 탐색을 구현 합니다.
3. 실행 중인 응용 프로그램을 중지 하려면 브라우저를 닫습니다.

### <a name="reviewing-the-database"></a>데이터베이스 검토

*Web.config* 파일을 열고 연결 문자열 섹션을 확인 합니다. 연결 문자열의 `AttachDbFilename` 값이 웹 응용 프로그램 프로젝트의 `DataDirectory`를 가리키는 것을 확인할 수 있습니다. `|DataDirectory|` 값은 프로젝트의 *응용 프로그램\_데이터* 폴더를 나타내는 예약 된 값입니다. 이 폴더에는 엔터티 클래스에서 만들어진 데이터베이스가 있습니다.

[!code-xml[Main](ui_and_navigation/samples/sample9.xml)]

> [!NOTE] 
> 
> *앱\_데이터* 폴더가 표시 되지 않거나 폴더가 비어 있는 경우 **새로 고침** 아이콘을 선택 하 고 **솔루션 탐색기** 창의 맨 위에 있는 **모든 파일 표시** 아이콘을 선택 합니다. 사용 가능한 모든 아이콘을 표시 하려면 **솔루션 탐색기** 창의 너비를 확장 해야 할 수 있습니다.

이제 **서버 탐색기** 창을 사용 하 여 *wingtiptoys* 데이터베이스 파일에 포함 된 데이터를 검사할 수 있습니다.

1. *앱\_데이터* 폴더를 확장 합니다. *응용 프로그램\_데이터* 폴더가 표시 되지 않는 경우 위의 참고 사항을 참조 하세요.
2. *Wingtiptoys* 데이터베이스 파일이 표시 되지 않으면 **새로 고침** 아이콘을 선택 하 고 **솔루션 탐색기** 창의 맨 위에 있는 **모든 파일 표시** 아이콘을 선택 합니다.
3. *Wingtiptoys* 데이터베이스 파일을 마우스 오른쪽 단추로 클릭 하 고 **열기**를 선택 합니다.  
    **서버 탐색기** 표시 됩니다. 

    ![UI 및 탐색-서버 탐색기](ui_and_navigation/_static/image8.png)
4. *테이블* 폴더를 확장합니다.
5. **Products**테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시**를 선택 합니다.  
 **Products** 테이블이 표시 됩니다. 

    ![UI 및 탐색-제품 테이블](ui_and_navigation/_static/image9.png)
6. 이 보기를 사용 하면 **Products** 테이블의 데이터를 직접 보고 수정할 수 있습니다.
7. **Products** 테이블 창을 닫습니다.
8. **서버 탐색기**에서 **Products** 테이블을 다시 마우스 오른쪽 단추로 클릭 하 고 **테이블 정의 열기**를 선택 합니다.  
 **Products** 테이블의 데이터 디자인이 표시 됩니다. 

    ![UI 및 탐색-제품 디자인](ui_and_navigation/_static/image10.png)
9. **T-sql** 탭에 테이블을 만드는 데 사용 된 SQL DDL 문이 표시 됩니다. **디자인** 탭에서 UI를 사용 하 여 스키마를 수정할 수도 있습니다.
10. **서버 탐색기**에서 **WingtipToys** database를 마우스 오른쪽 단추로 클릭 하 고 **연결 닫기**를 선택 합니다.   
 Visual Studio에서 데이터베이스를 분리 하 여 데이터베이스 스키마를이 자습서 시리즈의 뒷부분에서 수정할 수 있습니다.
11. **서버 탐색기** 창 맨 아래에 있는 **솔루션 탐색기** 탭을 선택 하 여 **솔루션 탐색기**로 돌아갑니다.

## <a name="summary"></a>요약

이 시리즈의 자습서에서는 몇 가지 기본 UI, 그래픽, 페이지 및 탐색을 추가 했습니다. 또한 이전 자습서에서 추가한 데이터 클래스에서 데이터베이스를 만든 웹 응용 프로그램을 실행 했습니다. 데이터베이스를 직접 확인 하 여 데이터베이스의 *Products* 테이블 내용을 볼 수도 있습니다. 다음 자습서에서는 데이터베이스에서 데이터 항목 및 세부 정보를 표시 합니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지  프로그래밍 소개](https://msdn.microsoft.com/library/ms178125.aspx)  
[ASP.NET 웹 서버 컨트롤 개요](https://msdn.microsoft.com/library/zsyt68f1.aspx)   
[CSS 자습서](http://www.w3schools.com/css/default.asp)

> [!div class="step-by-step"]
> [이전](create_the_data_access_layer.md)
> [다음](display_data_items_and_details.md)
