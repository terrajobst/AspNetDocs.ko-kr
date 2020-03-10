---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: '8 부: 최종 페이지, 예외 처리 및 결론 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 8 부에서 연락처 페이지, 정보 페이지 및 예외를 추가 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474341"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a>8 부: 최종 페이지, 예외 처리 및 결론

만든 사람 [Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다. ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 8 부에서는 연락처 페이지, 정보 페이지 및 예외 처리를 추가 합니다. 이는 계열의 결론입니다.

## <a id="_Toc260221680"></a>연락처 페이지 (ASP.NET에서 전자 메일 보내기)

ContactUs 라는 새 페이지를 만듭니다.

디자이너를 사용 하 여 ToolkitScriptManager 및 AjaxControlToolkit의 편집기 컨트롤을 포함 하는 다음과 같은 특수 노트를 만듭니다. .

![](tailspin-spyworks-part-8/_static/image1.jpg)

"제출" 단추를 두 번 클릭 하 여 코드 뒤 파일에서 클릭 이벤트 처리기를 생성 하 고 연락처 정보를 전자 메일로 보내는 메서드를 구현 합니다.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

이 코드를 사용 하려면 web.config 파일에 메일을 보내는 데 사용할 SMTP 서버를 지정 하는 항목을 구성 섹션에 포함 해야 합니다.

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>정보 페이지

AboutUs 라는 페이지를 만들고 원하는 콘텐츠를 추가 합니다.

## <a id="_Toc260221682"></a>전역 예외 처리기

마지막으로, 응용 프로그램 전체에서 예외가 throw 되 고 콜드에서 웹 응용 프로그램에 처리 되지 않은 예외가 발생 하는 예측할 수 없는 상황이 발생 합니다.

처리 되지 않은 예외가 웹 사이트 방문자에 게 표시 되는 것을 원하지 않습니다.

![](tailspin-spyworks-part-8/_static/image2.jpg)

처리 되지 않은 사용자 환경 외에도 보안 문제가 발생할 수 있습니다.

이 문제를 해결 하기 위해 전역 예외 처리기를 구현 합니다.

이렇게 하려면 Global.asax 파일을 열고 미리 생성 된 다음 이벤트 처리기를 확인 합니다.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

다음과 같이 응용 프로그램\_오류 처리기를 구현 하는 코드를 추가 합니다.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

그런 다음, .aspx 이라는 페이지를 솔루션에 추가 하 고이 마크업 코드 조각을 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

이제 페이지\_Load 이벤트 처리기에서 요청 개체의 오류 메시지를 추출 합니다.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>끝낼

ASP.NET WebForms를 사용 하면 데이터베이스 액세스, 멤버 자격, AJAX 등의 복잡 한 웹 사이트를 쉽게 만들 수 있습니다. 매우 빠르게 합니다.

이 자습서에서는 사용자 고유의 ASP.NET WebForms 응용 프로그램 빌드를 시작 하는 데 필요한 도구를 제공 하는 데 도움을 바랍니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-7.md)
