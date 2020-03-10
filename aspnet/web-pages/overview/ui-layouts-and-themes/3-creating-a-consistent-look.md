---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: ASP.NET 웹 페이지 (Razor) 사이트에서 일관 된 레이아웃 만들기 | Microsoft Docs
author: Rick-Anderson
description: '사이트에 대 한 웹 페이지를 보다 효율적으로 만들 수 있도록 웹 사이트에 대 한 콘텐츠 (예: 머리글 및 바닥글)의 재사용 가능한 블록을 만들 수 있습니다.'
ms.author: riande
ms.date: 03/10/2014
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 3f63ce68ae4c13970ac0df196167ace0b22b592c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509099"
---
# <a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 일관 된 레이아웃 만들기

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 레이아웃 페이지를 사용 하 여 다시 사용할 수 있는 콘텐츠 블록 (예: 머리글 및 바닥글)을 만들고 사이트의 모든 페이지에 대해 일관 된 모양을 만드는 방법을 설명 합니다.
> 
> **학습 내용:** 
> 
> - 헤더 및 바닥글과 같은 재사용 가능한 콘텐츠 블록을 만드는 방법
> - 레이아웃을 사용 하 여 사이트의 모든 페이지에 대해 일관 된 모양을 만드는 방법
> - 런타임에 데이터를 레이아웃 페이지에 전달 하는 방법입니다.
> 
> 다음은이 문서에 도입 된 ASP.NET 기능입니다.
> 
> - 콘텐츠 블록-여러 페이지에 삽입할 HTML 형식 콘텐츠를 포함 하는 파일입니다.
> - 웹 사이트 페이지에서 공유할 수 있는 HTML 형식 콘텐츠를 포함 하는 페이지인 레이아웃 페이지
> - `RenderPage`, `RenderBody`및 `RenderSection` 메서드로, 페이지 요소를 삽입할 위치를 ASP.NET에 게 알립니다.
> - 콘텐츠 블록과 레이아웃 페이지 간에 데이터를 공유할 수 있도록 하는 `PageData` 사전입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.

## <a name="about-layout-pages"></a>레이아웃 페이지 정보

대부분의 웹 사이트에는 머리글 및 바닥글과 같이 모든 페이지에 표시 되는 콘텐츠 또는 사용자에 게 로그인 여부를 알려 주는 상자가 있습니다. ASP.NET를 사용 하면 일반 웹 페이지와 마찬가지로 텍스트, 마크업 및 코드를 포함할 수 있는 콘텐츠 블록을 사용 하 여 별도의 파일을 만들 수 있습니다. 그런 다음 정보를 표시할 사이트의 다른 페이지에 콘텐츠 블록을 삽입할 수 있습니다. 이렇게 하면 동일한 콘텐츠를 모든 페이지에 복사 하 여 붙여 넣을 필요가 없습니다. 이와 같은 일반적인 콘텐츠를 만들면 사이트를 더 쉽게 업데이트할 수 있습니다. 콘텐츠를 변경 해야 하는 경우에는 단일 파일만 업데이트 하면 내용이 삽입 된 모든 위치에 변경 내용이 반영 됩니다.

다음 다이어그램에서는 콘텐츠 블록의 작동 방식을 보여 줍니다. 브라우저에서 웹 서버의 페이지를 요청 하면 ASP.NET는 기본 페이지에서 `RenderPage` 메서드가 호출 된 지점에 콘텐츠 블록을 삽입 합니다. 그러면 완료 된 (병합 된) 페이지가 브라우저에 전송 됩니다.

![RenderPage 메서드가 참조 된 페이지를 현재 페이지에 삽입 하는 방법을 보여 주는 개념적 다이어그램입니다.](3-creating-a-consistent-look/_static/image1.jpg)

이 절차에서는 별도의 파일에 있는 두 개의 콘텐츠 블록 (헤더 및 바닥글)을 참조 하는 페이지를 만듭니다. 사이트의 모든 페이지에서 동일한 콘텐츠 블록을 사용할 수 있습니다. 완료 되 면 다음과 같은 페이지를 얻게 됩니다.

![RenderPage 메서드에 대 한 호출을 포함 하는 페이지를 실행 하 여 발생 하는 브라우저의 페이지를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image2.png)

1. 웹 사이트의 루트 폴더에서 *Index. cshtml*라는 파일을 만듭니다.
2. 기존 태그를 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. 루트 폴더에서 *Shared*라는 폴더를 만듭니다.

    > [!NOTE]
    > *공유*된 폴더의 웹 페이지 간에 공유 되는 파일을 저장 하는 것이 일반적인 방법입니다.
4. *공유* 폴더에서 *\_헤더. cshtml*라는 파일을 만듭니다.
5. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    파일 이름은 *\_헤더. cshtml*이며, 접두사로 밑줄 (\_)을 사용 합니다. ASP.NET 이름이 밑줄로 시작 하는 경우 브라우저에 페이지를 보내지 않습니다. 이렇게 하면 사용자가 이러한 페이지를 직접 요청 (실수로 또는 그렇지 않은 경우) 할 수 없습니다. 사용자가 해당 페이지 &#8212; 를 다른 페이지에 삽입 하는 것을 엄격 하 게 요청할 수 없도록 하기 때문에 콘텐츠 블록이 있는 페이지의 이름을 지정할 때 밑줄을 사용 하는 것이 좋습니다.
6. *공유* 폴더에서 *\_Footer* 라는 파일을 만들고 콘텐츠를 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. *Index. cshtml* 페이지에서 다음과 같이 `RenderPage` 메서드에 대 한 두 호출을 추가 합니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    웹 페이지에 콘텐츠 블록을 삽입 하는 방법을 보여 줍니다. `RenderPage` 메서드를 호출 하 여 해당 위치에 삽입 하려는 내용의 파일 이름을 전달 합니다. 여기에서 *\_헤더* 의 내용을 삽입 합니다. cshtml 및 *\_Footer* 파일에는 *인덱스 cshtml* 파일.
8. 브라우저에서 *Index. cshtml* 페이지를 실행 합니다. (WebMatrix의 **파일** 작업 영역에서 파일을 마우스 오른쪽 단추로 클릭 한 다음 **브라우저에서 시작**을 선택 합니다.)
9. 브라우저에서 페이지 소스를 봅니다. 예를 들어 Internet Explorer에서 페이지를 마우스 오른쪽 단추로 클릭 한 다음 **소스 보기**를 클릭 합니다.

    이렇게 하면 브라우저에 전송 된 웹 페이지 태그를 볼 수 있습니다 .이 태그는 인덱스 페이지 태그를 콘텐츠 블록과 결합 합니다. 다음 예에서는 *Index. cshtml*에 대해 렌더링 되는 페이지 원본을 보여 줍니다. *Index. cshtml* 에 삽입 된 `RenderPage`에 대 한 호출은 머리글 및 바닥글 파일의 실제 콘텐츠로 대체 되었습니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a>레이아웃 페이지를 사용 하 여 일관 된 모양 만들기

지금까지 여러 페이지에 동일한 콘텐츠를 포함 하는 것이 쉽습니다. 사이트를 일관 되 게 찾는 방법은 레이아웃 페이지를 사용 하는 것입니다. 레이아웃 페이지는 웹 페이지의 구조를 정의 하지만 실제 콘텐츠는 포함 하지 않습니다. 레이아웃 페이지를 만든 후에는 콘텐츠를 포함 하는 웹 페이지를 만든 다음 레이아웃 페이지에 연결할 수 있습니다. 이러한 페이지가 표시 되 면 레이아웃 페이지에 따라 형식이 지정 됩니다. 이 경우 레이아웃 페이지는 다른 페이지에 정의 된 콘텐츠에 대 한 일종의 템플릿 역할을 합니다.

레이아웃 페이지는 `RenderBody` 메서드에 대 한 호출을 포함 한다는 점을 제외 하 고 HTML 페이지와 동일 합니다. 레이아웃 페이지에서 `RenderBody` 메서드의 위치에 따라 콘텐츠 페이지의 정보가 포함 될 위치가 결정 됩니다.

다음 다이어그램에서는 런타임에 콘텐츠 페이지 및 레이아웃 페이지를 결합 하 여 완성 된 웹 페이지를 생성 하는 방법을 보여 줍니다. 브라우저에서 콘텐츠 페이지를 요청 합니다. 콘텐츠 페이지에는 페이지 구조에 사용할 레이아웃 페이지를 지정 하는 코드가 있습니다. 레이아웃 페이지에서 `RenderBody` 메서드가 호출 되는 지점에 콘텐츠가 삽입 됩니다. 이전 섹션에서 수행한 것과 같은 방법으로 `RenderPage` 메서드를 호출 하 여 콘텐츠 블록을 레이아웃 페이지에 삽입할 수도 있습니다. 웹 페이지가 완료 되 면 브라우저에 전송 됩니다.

![RenderBody 메서드 호출을 포함 하는 페이지를 실행 하 여 발생 하는 브라우저의 페이지를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image3.jpg)

다음 절차에서는 레이아웃 페이지를 만들고 콘텐츠 페이지를 해당 페이지에 연결 하는 방법을 보여 줍니다.

1. 웹 사이트의 *공유* 폴더에서 *Layout1\_* 라는 파일을 만듭니다.
2. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    레이아웃 페이지에서 `RenderPage` 메서드를 사용 하 여 콘텐츠 블록을 삽입 합니다. 레이아웃 페이지는 `RenderBody` 메서드에 대 한 호출을 하나만 포함할 수 있습니다.
3. *공유* 폴더에서 *.header2\_* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. 루트 폴더에서 새 폴더를 만들고 이름을 *스타일*로 합니다.
5. *Styles* 폴더에서 이름이 *.css* 인 파일을 만들고 다음 스타일 정의를 추가 합니다.

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    이러한 스타일 정의는 레이아웃 페이지에서 스타일 시트를 사용 하는 방법을 보여 주기 위한 것입니다. 원하는 경우 이러한 요소에 대해 고유한 스타일을 정의할 수 있습니다.
6. 루트 폴더에서 *Content1* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    레이아웃 페이지를 사용 하는 페이지입니다. 페이지 맨 위에 있는 코드 블록은이 콘텐츠 형식을 지정 하는 데 사용할 레이아웃 페이지를 나타냅니다.
7. 브라우저에서 *Content1* 를 실행 합니다. 렌더링 된 페이지는 *\_Layout1* 에 정의 된 형식 및 스타일 시트와 *Content1*에 정의 된 텍스트 (내용)를 사용 합니다.

    ![[이미지]](3-creating-a-consistent-look/_static/image4.png)

    6 단계를 반복 하 여 동일한 레이아웃 페이지를 공유할 수 있는 추가 콘텐츠 페이지를 만들 수 있습니다.

    > [!NOTE]
    > 폴더의 모든 콘텐츠 페이지에 대해 동일한 레이아웃 페이지를 자동으로 사용할 수 있도록 사이트를 설정할 수 있습니다. 자세한 내용은 [ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)을 참조 하세요.

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a>여러 콘텐츠 섹션이 있는 레이아웃 페이지 디자인

콘텐츠 페이지에는 여러 섹션이 있을 수 있습니다 .이는 대체 가능한 콘텐츠가 있는 여러 영역이 있는 레이아웃을 사용 하려는 경우에 유용 합니다. 콘텐츠 페이지에서 각 섹션에 고유한 이름을 지정 합니다. 기본 섹션은 명명 되지 않은 상태로 남아 있습니다. 레이아웃 페이지에서 명명 되지 않은 (기본값) 섹션이 표시 되는 위치를 지정 하는 `RenderBody` 메서드를 추가 합니다. 그런 다음 명명 된 섹션을 개별적으로 렌더링 하기 위해 별도의 `RenderSection` 메서드를 추가 합니다.

다음 다이어그램에서는 ASP.NET에서 여러 섹션으로 나뉜 콘텐츠를 처리 하는 방법을 보여 줍니다. 각 명명 된 섹션은 콘텐츠 페이지의 섹션 블록에 포함 되어 있습니다. (예제에서는 `Header` 이름이 지정 되 고 `List`. 프레임 워크는 `RenderSection` 메서드가 호출 된 지점의 레이아웃 페이지에 콘텐츠 섹션을 삽입 합니다. 명명 되지 않은 (기본) 섹션은 앞에서 살펴본 것 처럼 `RenderBody` 메서드가 호출 된 지점에 삽입 됩니다.

![RenderSection 메서드가 참조 섹션을 현재 페이지에 삽입 하는 방법을 보여 주는 개념적 다이어그램](3-creating-a-consistent-look/_static/image5.jpg)

이 절차에서는 여러 콘텐츠 섹션을 포함 하는 콘텐츠 페이지를 만드는 방법과 여러 콘텐츠 섹션을 지 원하는 레이아웃 페이지를 사용 하 여 렌더링 하는 방법을 보여 줍니다.

1. *공유* 폴더에서 *Layout2\_* 라는 파일을 만듭니다.
2. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    `RenderSection` 메서드를 사용 하 여 헤더 및 목록 섹션을 모두 렌더링 합니다.
3. 루트 폴더에서 *Content2* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    이 콘텐츠 페이지에는 페이지 맨 위에 있는 코드 블록이 포함 되어 있습니다. 각 명명 된 섹션은 section 블록에 포함 되어 있습니다. 페이지의 나머지 부분에는 기본 (명명 되지 않은) 콘텐츠 섹션이 포함 되어 있습니다.
4. 브라우저에서 *Content2* 를 실행 합니다.

    ![RenderSection 메서드 호출을 포함 하는 페이지를 실행 하 여 발생 하는 브라우저의 페이지를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image6.png)

## <a name="making-content-sections-optional"></a>콘텐츠 섹션 만들기 옵션

일반적으로 콘텐츠 페이지에서 만드는 섹션은 레이아웃 페이지에 정의 된 섹션과 일치 해야 합니다. 다음 중 하나가 발생 하는 경우 오류를 가져올 수 있습니다.

- 콘텐츠 페이지의 레이아웃 페이지에 해당 섹션이 없는 섹션이 있습니다.
- 레이아웃 페이지에 콘텐츠가 없는 섹션이 포함 되어 있습니다.
- 레이아웃 페이지에 동일한 섹션을 두 번 이상 렌더링 하려고 하는 메서드 호출이 포함 되어 있습니다.

그러나 레이아웃 페이지에서 섹션을 선택 사항으로 선언 하 여 명명 된 섹션에 대해이 동작을 재정의할 수 있습니다. 이렇게 하면 레이아웃 페이지를 공유할 수 있지만 특정 섹션에 대 한 콘텐츠가 없을 수도 있는 여러 콘텐츠 페이지를 정의할 수 있습니다.

1. Content2를 열고 다음 섹션을 제거 *합니다* .

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. 페이지를 저장 하 고 브라우저에서 실행 합니다. 콘텐츠 페이지에서 레이아웃 페이지에 정의 된 섹션에 대 한 콘텐츠 (헤더 섹션)를 제공 하지 않기 때문에 오류 메시지가 표시 됩니다.

    ![RenderSection 메서드를 호출 하는 페이지를 실행 하지만 해당 섹션이 제공 되지 않는 경우 발생 하는 오류를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image7.png)
3. *공유* 폴더에서 *\_Layout2* 페이지를 열고 다음 줄을 바꿉니다.

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    다음 코드와 바꿉니다.

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    또는 동일한 결과를 생성 하는 다음 코드 블록으로 이전 코드 줄을 바꿀 수 있습니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. 브라우저에서 *Content2* 페이지를 다시 실행 합니다. 브라우저에서이 페이지를 열어 둔 경우 새로 고칠 수 있습니다. 이번에는 헤더가 없더라도 페이지가 오류 없이 표시 됩니다.

## <a name="passing-data-to-layout-pages"></a>레이아웃 페이지에 데이터 전달

콘텐츠 페이지에서 레이아웃 페이지에 참조 해야 하는 데이터를 정의할 수 있습니다. 그렇다면 콘텐츠 페이지에서 레이아웃 페이지로 데이터를 전달 해야 합니다. 예를 들어 사용자의 로그인 상태를 표시 하거나 사용자 입력을 기준으로 콘텐츠 영역을 표시 하거나 숨길 수 있습니다.

콘텐츠 페이지에서 레이아웃 페이지로 데이터를 전달 하려면 콘텐츠 페이지의 `PageData` 속성에 값을 입력할 수 있습니다. `PageData` 속성은 페이지 간에 전달 하려는 데이터를 포함 하는 이름/값 쌍의 컬렉션입니다. 그러면 레이아웃 페이지에서 `PageData` 속성의 값을 읽을 수 있습니다.

다른 다이어그램은 다음과 같습니다. 이 항목에서는 ASP.NET가 `PageData` 속성을 사용 하 여 콘텐츠 페이지의 값을 레이아웃 페이지에 전달 하는 방법을 보여 줍니다. ASP.NET가 웹 페이지 빌드를 시작 하면 `PageData` 컬렉션을 만듭니다. 콘텐츠 페이지에서 `PageData` 컬렉션에 데이터를 저장 하는 코드를 작성 합니다. `PageData` 컬렉션의 값은 콘텐츠 페이지의 다른 섹션 또는 추가 콘텐츠 블록 에서도 액세스할 수 있습니다.

![콘텐츠 페이지가 PageData 사전을 채우고 해당 정보를 레이아웃 페이지에 전달 하는 방법을 보여 주는 개념적 다이어그램입니다.](3-creating-a-consistent-look/_static/image8.jpg)

다음 절차에서는 콘텐츠 페이지에서 레이아웃 페이지로 데이터를 전달 하는 방법을 보여 줍니다. 페이지가 실행 되 면 사용자가 레이아웃 페이지에 정의 된 목록을 숨기 거 나 표시할 수 있는 단추가 표시 됩니다. 사용자가 단추를 클릭 하면 `PageData` 속성에 true/false (부울) 값이 설정 됩니다. 레이아웃 페이지에서 해당 값을 읽고, false 인 경우 목록을 숨깁니다. 콘텐츠 페이지에서 **목록 숨기기** 단추 또는 **목록 표시** 단추를 표시할지 여부를 결정 하는 데에도이 값이 사용 됩니다.

![[이미지]](3-creating-a-consistent-look/_static/image9.jpg)

1. 루트 폴더에서 *Content3* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    이 코드는 두 개의 데이터를 웹 페이지의 제목 &#8212; `PageData` 속성에 저장 하 고 true 또는 false를 지정 하 여 목록을 표시할지 여부를 지정 합니다.

    ASP.NET를 사용 하면 코드 블록을 사용 하 여 조건적으로 페이지에 HTML 태그를 추가할 수 있습니다. 예를 들어 페이지 본문의 `if/else` 블록은 `PageData["ShowList"]` true로 설정 되었는지 여부에 따라 표시할 폼을 결정 합니다.
2. *공유* 폴더에서 *Layout3\_* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    레이아웃 페이지에는 `PageData` 속성에서 제목 값을 가져오는 `<title>` 요소의 식이 포함 되어 있습니다. 또한 `PageData` 속성의 `ShowList` 값을 사용 하 여 목록 콘텐츠 블록을 표시할지 여부를 결정 합니다.
3. *공유* 폴더에서 *\_List. cshtml* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. 브라우저에서 *Content3* 페이지를 실행 합니다. 페이지의 왼쪽에 목록이 표시 되 고 맨 아래에 **목록 숨기기** 단추가 표시 됩니다.

    ![목록을 포함 하는 페이지와 ' 목록 숨기기 ' 라고 표시 된 단추를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image10.png)
5. **목록 숨기기**를 클릭 합니다. 목록이 사라지고 단추가 **목록 표시**로 변경 됩니다.

    ![목록 및 ' Show List ' 단추를 포함 하지 않는 페이지를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image11.png)
6. **목록 표시** 단추를 클릭 하면 목록이 다시 표시 됩니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
