---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437369"
---
# <a name="accessing-your-models-data-from-a-controller"></a>컨트롤러에서 모델의 데이터에 액세스

[Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다. [ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.

이 섹션에서는 새 Moviescontroller.cs 클래스를 만들고, 영화 데이터를 검색 하는 코드를 작성 하 고, 뷰 템플릿을 사용 하 여 브라우저에 다시 표시 합니다.

Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 Moviescontroller.cs을 만듭니다.

[컨트롤러 추가 ![](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)

이렇게 하면 프로젝트 내의 \Controllers 폴더 아래에 새 "MoviesController.cs" 파일이 만들어집니다. MovieController를 업데이트 하 여 새로 채워진 데이터베이스에서 동영상 목록을 검색 해 보겠습니다.

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

1984의 여름 이후에 릴리스된 영화만 검색 하도록 LINQ 쿼리를 수행 하 고 있습니다. 이 동영상 목록을 다시 렌더링 하려면 뷰 템플릿이 필요 하므로 메서드를 마우스 오른쪽 단추로 클릭 하 고 보기 추가를 선택 하 여 만듭니다.

보기 추가 대화 상자 내에서 보기 템플릿에&gt;&lt;목록을 전달 하 고 있는지를 표시 합니다. 보기 추가 대화 상자를 사용 하 여 "빈" 템플릿을 만들도록 선택한 이전 시간과 달리 이번에는 Visual Studio에서 일부 기본 콘텐츠를 사용 하 여 보기 템플릿을 자동으로 "스 캐 폴드" 하는 것을 알 수 있습니다. "콘텐츠 보기 드롭다운 메뉴에서" 목록 "항목을 선택 하 여이 작업을 수행 합니다.

새 클래스를 만든 경우 보기 추가 대화 상자에 표시 되도록 응용 프로그램을 컴파일해야 합니다.

![뷰 추가](getting-started-with-mvc-part5/_static/image3.png)

추가를 클릭 하면 시스템에서 영화 목록을 표시 하는 보기에 대 한 코드를 자동으로 생성 합니다. 이전에 Hello World 보기를 사용 했을 때와 같이 &lt;h2&gt; 제목을 "내 동영상 목록"과 같이 변경 하는 것이 좋습니다.

[![영화-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)

응용 프로그램을 실행 하 고 주소 표시줄에서/영화를 방문 합니다. 이제 컨트롤러 내부의 기본 쿼리를 사용 하 여 데이터베이스에서 데이터를 검색 하 고 영화에 대해 알고 있는 뷰로 데이터를 반환 했습니다. 그런 다음이 뷰는 동영상 목록을 회전 하 고 데이터 테이블을 만듭니다.

[![동영상 목록-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)

이 응용 프로그램을 사용 하 여 편집, 세부 정보 및 삭제 기능을 구현 하지 않으므로 스 캐 폴드 템플릿이 생성 하는 기본 링크가 필요 하지 않습니다. /Movies/Index.aspx 파일을 열고 제거 합니다.

다음은 이러한 변경을 수행한 후에 업데이트 된 뷰 템플릿이 표시 되는 대상에 대 한 소스 코드입니다.

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

필요 하지 않은 링크를 만들기 때문에이 예제에 대 한 링크를 삭제 합니다. 새 링크 만들기는 다음 단계와 같이 계속 유지 됩니다. 해당 열이 제거 되 면 앱의 모양은 다음과 같습니다.

[![동영상 목록-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)

이제 영화 데이터를 간단히 나열할 수 있습니다. 그러나 "새로 만들기" 링크를 클릭 하면 후크 되지 않으므로 오류가 발생 합니다. Create Action 메서드를 구현 하 고 사용자가 데이터베이스에 새 영화를 입력할 수 있도록 합니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part4.md)
> [다음](getting-started-with-mvc-part6.md)
