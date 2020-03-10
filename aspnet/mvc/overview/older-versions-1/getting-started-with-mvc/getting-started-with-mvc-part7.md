---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: 모델에 유효성 검사 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437279"
---
# <a name="adding-validation-to-the-model"></a>모델에 유효성 검사 추가

[Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다. [ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.

이 섹션에서는 응용 프로그램 내에서 입력 유효성 검사를 사용 하도록 설정 하는 데 필요한 지원을 구현 합니다. 데이터베이스 콘텐츠가 항상 정확한 지 확인 하 고, 유효 하지 않은 영화 데이터를 입력 하는 경우 최종 사용자에 게 유용한 오류 메시지를 제공 합니다. 먼저 Movie 클래스에 약간의 유효성 검사 논리를 추가 합니다.

모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 클래스 추가를 선택 합니다. 클래스 이름을 Movie로 합니다.

이전에 영화 엔터티 모델을 만들 때 IDE는 Movie 클래스를 만들었습니다. 실제로 Movie 클래스의 일부는 한 파일에 있을 수 있고 다른 파일에 포함 될 수 있습니다. 이를 Partial 클래스 라고 합니다. 다른 파일에서 Movie 클래스를 확장할 예정입니다.

시스템에 유효성 검사 힌트를 제공 하는 일부 특성을 가진 "버디 클래스"를 가리키는 부분 영화 클래스를 만듭니다. 필요에 따라 제목 및 가격을 표시 하 고 가격이 특정 범위 내에 포함 되도록 합니다. 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 클래스 추가를 선택 합니다. 클래스 이름을 Movie로 하 고 확인 단추를 클릭 합니다. 부분 동영상 클래스는 다음과 같습니다.

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

응용 프로그램을 다시 실행 하 고 가격이 100 보다 낮은 영화를 입력 해 보세요. 양식을 제출 하면 오류가 발생 합니다. 이 오류는 서버 쪽에서 catch 되며 폼이 게시 된 후에 발생 합니다. ASP.NET MVC의 기본 제공 HTML 도우미는 오류 메시지를 표시 하 고 텍스트 상자 요소 내에서 값을 유지 하는 데 충분 한지 확인 합니다.

[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)

이는 잘 작동 하지만 서버가 포함 되기 전에 클라이언트 쪽에서 즉시 사용자에 게 알릴 수 있는 것이 좋습니다.

JavaScript를 사용 하 여 클라이언트 쪽 유효성 검사를 수행할 수 있습니다.

## <a name="adding-client-side-validation"></a>클라이언트측 유효성 검사 추가

Movie 클래스에는 이미 일부 유효성 검사 특성이 있기 때문에 몇 가지 JavaScript 파일을 Create .aspx 뷰 템플릿에 추가 하 고 클라이언트 쪽 유효성 검사를 수행할 수 있도록 코드 줄을 추가 하기만 하면 됩니다.

VWD 내에서 Views/Movie 폴더로 이동 하 여 Create .aspx를 엽니다.

솔루션 탐색기에서 Scripts 폴더를 열고 다음 세 개의 스크립트를 &lt;head&gt; 태그 내에 끌어 옵니다.

- MicrosoftAjax.js
- MicrosoftMvcValidation.js

이러한 스크립트 파일이이 순서 대로 표시 되도록 합니다.

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

또한이 한 줄을 Html.beginform 위에 추가 합니다.

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

IDE 내에 표시 되는 코드는 다음과 같습니다.

[![영화-Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)

응용 프로그램을 실행 하 고/Movies/Create를 다시 방문 하 고 데이터를 입력 하지 않고 만들기를 클릭 합니다. 오류 메시지는 서버에 대 한 모든 방식으로 데이터를 전송 하는 데 연결 하는 페이지 플래시 없이 즉시 표시 됩니다. ASP.NET MVC는 이제 JavaScript를 사용 하 여 클라이언트와 서버에서 입력의 유효성을 검사 하기 때문입니다.

[![만들기-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)

좋은 방법입니다! 이제 데이터베이스에 열을 하나 더 추가 하겠습니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part6.md)
> [다음](getting-started-with-mvc-part8.md)
