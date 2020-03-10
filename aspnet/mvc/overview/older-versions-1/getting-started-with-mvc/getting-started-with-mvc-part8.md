---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: 모델에 열 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437225"
---
# <a name="adding-a-column-to-the-model"></a>모델에 열 추가

[Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다. [ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.

이 섹션에서는 데이터베이스의 스키마를 변경 하 고 응용 프로그램 내에서 변경 내용을 처리 하는 방법을 단계별로 설명 합니다.

동영상 테이블에 "등급" 열을 추가 해 보겠습니다. IDE로 돌아가서 데이터베이스 탐색기를 클릭 합니다. 동영상 테이블을 마우스 오른쪽 단추로 클릭 하 고 테이블 정의 열기를 선택 합니다.

아래 표시 된 것 처럼 "등급" 열을 추가 합니다. 지금은 등급이 없으므로 열에서 null을 허용할 수 있습니다. 저장을 클릭합니다.

[동영상 테이블 편집 ![](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)

그런 다음 솔루션 탐색기로 돌아가서 영화 .edmx 파일 (\Stoml 폴더에 있습니다)을 엽니다. 디자인 화면 (흰색 영역)을 마우스 오른쪽 단추로 클릭 하 고 데이터베이스에서 모델 업데이트를 선택 합니다.

[![영화-Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)

그러면 "업데이트 마법사"가 시작 됩니다. 내 새로 고침 탭을 클릭 하 고 마침을 클릭 합니다. 그런 다음 새 열을 사용 하 여 동영상 모델 클래스를 업데이트 합니다.

![업데이트 마법사 (2)](getting-started-with-mvc-part8/_static/image5.png)

마침을 클릭 하면 모델의 영화 엔터티에 새 등급 열이 추가 된 것을 볼 수 있습니다.

[![Movie 엔터티](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)

데이터베이스 모델에 열을 추가 했지만 뷰에서는 열을 알 수 없습니다.

## <a name="update-views-with-model-changes"></a>모델 변경 내용으로 뷰 업데이트

몇 가지 방법으로 보기 템플릿을 업데이트 하 여 새 등급 열을 반영할 수 있습니다. 뷰 추가 대화 상자를 통해 이러한 뷰를 생성 했으므로 삭제 하 고 다시 만들 수 있습니다. 그러나 일반적으로 사용자는 초기 스 캐 폴드 생성에서 보기 템플릿을 수정 했으며 Create에 대 한 ID 필드와 마찬가지로 필드를 수동으로 추가 하거나 삭제 하려고 합니다.

\Views\Movies\Index.aspx 템플릿을 열고 &lt;번째&gt;등급&lt;/th&gt;를 동영상 테이블의 헤드에 추가 합니다. 장르 뒤에 광산을 추가 했습니다. 그런 다음 동일한 열 위치에서 아래쪽으로 줄을 추가 하 여 새 등급을 출력 합니다.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

최종 Index .aspx 템플릿은 다음과 같습니다.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

\Views\Movies\Create.aspx 템플릿을 열고 새 등급 속성에 대 한 레이블 및 텍스트 상자를 추가 하겠습니다.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

최종 .aspx 템플릿은 다음과 같이 표시 되 고 여기에 있는 동안 브라우저의 제목 및 보조 &lt;h2&gt; 제목을 "동영상 만들기"와 같이 변경해 보겠습니다.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

앱을 실행 하면 데이터베이스에서 만들기 페이지에 추가 된 새 필드가 생성 됩니다. 새 영화 (이번에는 등급)를 추가 하 고 만들기를 클릭 합니다.

[동영상 ![만들기-Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)

만들기를 클릭 하면 새 동영상이 데이터베이스의 새 등급 열로 나열 된 인덱스 페이지로 전송 됩니다.

[![동영상 목록-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)

이 기본 자습서에서는 컨트롤러를 만들어 뷰와 연결 하 고 하드 코드 된 데이터를 전달 하기 시작 했습니다. 그런 다음 데이터베이스를 만들고 디자인 하 고 일부 데이터를 저장 했습니다. 데이터베이스에서 데이터를 검색 하 여 HTML 테이블에 표시 했습니다. 그런 다음 사용자가 웹 응용 프로그램 내에서 데이터베이스 자체에 데이터를 추가할 수 있는 만들기 폼을 추가 했습니다. 유효성 검사를 추가 하 고 클라이언트 쪽에서 JavaScript를 사용 하 여 유효성 검사를 수행 했습니다. 마지막으로 새 데이터 열을 포함 하도록 데이터베이스를 변경 하 고 두 페이지를 업데이트 하 여 새 데이터를 만들고 표시 합니다.

이제 ASP.NET MVC에 대해 자세히 학습할 수 있는 많은 비디오와 [https://asp.net/mvc](https://asp.net/mvc) 리소스 뿐만 아니라 중간 수준 자습서 "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)"로 이동 하는 것이 좋습니다.

마음껏 즐기세요!

- Twitter의 Scott Hanselman [http://hanselman.com](http://hanselman.com) 및 [@shanselman](http://twitter.com/shanselman) 입니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part7.md)
