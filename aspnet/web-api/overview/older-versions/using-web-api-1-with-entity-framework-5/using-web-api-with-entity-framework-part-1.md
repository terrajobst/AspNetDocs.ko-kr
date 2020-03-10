---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: '1 부: 개요 및 프로젝트 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447935"
---
# <a name="part-1-overview-and-creating-the-project"></a>1 부: 개요 및 프로젝트 만들기

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

Entity Framework은 개체/관계형 매핑 프레임 워크입니다. 코드의 도메인 개체를 관계형 데이터베이스의 엔터티에 매핑합니다. 대부분의 경우에는 Entity Framework는 데이터베이스 계층에 대해 걱정할 필요가 없습니다. 코드는 개체를 조작 하 고 변경 내용은 데이터베이스에 유지 됩니다.

## <a name="about-the-tutorial"></a>자습서 정보

이 자습서에서는 간단한 스토어 응용 프로그램을 만듭니다. 응용 프로그램에는 두 가지 주요 부분이 있습니다. 일반 사용자는 제품을 확인 하 고 주문을 만들 수 있습니다.

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

관리자는 제품을 생성, 삭제 또는 편집할 수 있습니다.

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a>학습할 기술

다음 내용을 학습하게 됩니다.

- ASP.NET Web API에서 Entity Framework를 사용 하는 방법
- Node.js를 사용 하 여 동적 클라이언트 UI를 만드는 방법
- 웹 API에서 폼 인증을 사용 하 여 사용자를 인증 하는 방법입니다.

이 자습서는 자체 포함 되어 있지만 먼저 다음 자습서를 읽을 수 있습니다.

- [최초 ASP.NET 앱 API](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [CRUD 작업을 지 원하는 Web API 만들기](../creating-a-web-api-that-supports-crud-operations.md)

[ASP.NET MVC](../../../../mvc/index.md) 에 대 한 일부 지식이 도움이 될 수도 있습니다.

## <a name="overview"></a>개요

개략적인 수준에서 응용 프로그램의 아키텍처는 다음과 같습니다.

- ASP.NET MVC는 클라이언트에 대 한 HTML 페이지를 생성 합니다.
- ASP.NET Web API는 데이터에 대 한 CRUD 작업 (제품 및 주문)을 노출 합니다.
- Entity Framework는 Web C# API에 사용 되는 모델을 데이터베이스 엔터티로 변환 합니다.

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

다음 다이어그램은 응용 프로그램의 다양 한 계층에서 도메인 개체를 표시 하는 방법을 보여 줍니다. 데이터베이스 계층, 개체 모델 및 마지막으로 HTTP를 통해 클라이언트에 데이터를 전송 하는 데 사용 되는 통신 형식입니다.

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

Visual Web Developer Express 또는 전체 버전의 Visual Studio를 사용 하 여 tutorial 프로젝트를 만들 수 있습니다.

**시작** 페이지에서 **새 프로젝트**를 클릭 합니다.

**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다. **시각적 개체 C#** 에서 **웹**을 선택 합니다. 프로젝트 템플릿 목록에서 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다. 프로젝트 이름을 "제품 저장소"로 하 고 **확인**을 클릭 합니다.

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 을 선택 하 고 **확인**을 클릭 합니다.

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

"인터넷 응용 프로그램" 템플릿은 폼 인증을 지 원하는 ASP.NET MVC 응용 프로그램을 만듭니다. 지금 응용 프로그램을 실행 하는 경우 다음과 같은 몇 가지 기능이 이미 있습니다.

- 새 사용자는 오른쪽 위 모퉁이에 있는 "등록" 링크를 클릭 하 여 등록할 수 있습니다.
- 등록 된 사용자는 "로그인" 링크를 클릭 하 여 로그인 할 수 있습니다.

멤버 자격 정보는 자동으로 생성 되는 데이터베이스에 유지 됩니다. ASP.NET MVC의 폼 인증에 대 한 자세한 내용은 [연습: ASP.NET mvc에서 폼 인증 사용](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)을 참조 하세요.

## <a name="update-the-css-file"></a>CSS 파일 업데이트

이 단계는 외관상 이지만 페이지를 이전 스크린샷 처럼 렌더링 하 게 됩니다.

솔루션 탐색기에서 Content 폴더를 확장 하 고 이름이 Site .css 인 파일을 엽니다. 다음 CSS 스타일을 추가 합니다.

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [다음](using-web-api-with-entity-framework-part-2.md)
