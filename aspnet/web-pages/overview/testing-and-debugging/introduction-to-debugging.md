---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: Razor (디버깅 ASP.NET 웹 페이지) 사이트 소개 | Microsoft Docs
author: Rick-Anderson
description: 디버깅은 코드 페이지에서 오류를 찾아 수정 하는 프로세스입니다. 이 장에서는를 디버깅 하 고 analyz 하는 데 사용할 수 있는 몇 가지 도구와 기술을 보여 줍니다.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: ae7d871e56326610c043dc20fe6e0919e1b4ac89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506459"
---
# <a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a>Razor (디버깅 ASP.NET 웹 페이지) 사이트 소개

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 페이지를 디버그 하는 다양 한 방법을 설명 합니다. 디버깅은 코드 페이지에서 오류를 찾아 수정 하는 프로세스입니다.
>
> **학습 내용:**
>
> - 페이지를 분석 하 고 디버그 하는 데 도움이 되는 정보를 표시 하는 방법입니다.
> - Visual Studio에서 디버깅 도구를 사용 하는 방법
>
>
> 다음은이 문서에 도입 된 ASP.NET 기능입니다.
>
> - `ServerInfo` 도우미입니다.
> - 도우미를 `ObjectInfo` 합니다.
>
>
> ## <a name="software-versions"></a>소프트웨어 버전
>
>
> - ASP.NET 웹 페이지 (Razor) 3
> - Visual Studio 2013
>
>
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다. WebMatrix 3을 사용할 수 있지만 통합 디버거는 지원 되지 않습니다.

코드에서 오류 및 문제를 해결 하는 중요 한 측면은 처음에는 피해 야 합니다. 이렇게 하려면 오류를 발생 시킬 수 있는 코드 섹션을 `try/catch` 블록에 배치 하면 됩니다. 자세한 내용은 [Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=202890)의 오류 처리에 대 한 섹션을 참조 하세요.

`ServerInfo` 도우미는 페이지를 호스팅하는 웹 서버 환경에 대 한 정보의 개요를 제공 하는 진단 도구입니다. 또한 브라우저에서 페이지를 요청할 때 전송 되는 HTTP 요청 정보를 표시 합니다. `ServerInfo` 도우미는 현재 사용자 id, 요청을 수행한 브라우저의 유형 등을 표시 합니다. 이러한 종류의 정보는 일반적인 문제를 해결 하는 데 도움이 될 수 있습니다.

1. *ServerInfo*라는 새 웹 페이지를 만듭니다.
2. 페이지 끝에서 닫는 `</body>` 태그 바로 앞에 `@ServerInfo.GetHtml()`를 추가 합니다.

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    페이지의 아무 곳에 나 `ServerInfo` 코드를 추가할 수 있습니다. 그러나이를 끝에 추가 하면 다른 페이지 콘텐츠와 별도로 출력을 유지 하 여 읽기 쉽게 만들 수 있습니다.

    > [!NOTE]
    >
    > **중요** 웹 페이지를 프로덕션 서버로 이동 하기 전에 웹 페이지에서 진단 코드를 제거 해야 합니다. 이는 `ServerInfo` 도우미 뿐만 아니라 페이지에 코드를 추가 하는 것과 관련 된이 문서의 다른 진단 기술에도 적용 됩니다. 이러한 유형의 정보는 악의적인 의도를 가진 사용자에 게 유용할 수 있으므로 웹 사이트 방문자에 게 서버 이름, 사용자 이름, 서버 경로 및 비슷한 세부 정보에 대 한 정보를 표시 하지 않으려고 합니다.
3. 페이지를 저장 하 고 브라우저에서 실행 합니다.

    ![디버깅-1](introduction-to-debugging/_static/image1.jpg)

    `ServerInfo` 도우미는 페이지에 4 개의 정보 테이블을 표시 합니다.

   - 서버 구성. 이 섹션에서는 컴퓨터 이름, 실행 중인 ASP.NET 버전, 도메인 이름 및 서버 시간을 포함 하 여 호스팅 웹 서버에 대 한 정보를 제공 합니다.
   - ASP.NET 서버 변수입니다. 이 섹션에서는 HTTP 변수 라고 하는 여러 HTTP 프로토콜 세부 정보 및 각 웹 페이지 요청에 포함 된 값에 대해 자세히 설명 합니다.
   - HTTP 런타임 정보입니다. 이 섹션에서는 웹 페이지가 실행 되는 Microsoft .NET Framework 버전, 경로, 캐시에 대 한 세부 정보 등에 대해 자세히 설명 합니다. ( [Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=202890)에서 살펴본 것 처럼 Razor 구문를 사용 하는 ASP.NET 웹 페이지은 Microsoft의 ASP.NET 웹 서버 기술을 기반으로 하며,이 기술은 .NET Framework 이라는 광범위 한 소프트웨어 개발 라이브러리를 기반으로 빌드됩니다.
   - 환경 변수. 이 섹션에서는 웹 서버에서 모든 로컬 환경 변수 및 해당 값의 목록을 제공 합니다.

     모든 서버 및 요청 정보에 대 한 전체 설명은이 문서의 범위를 벗어나서 `ServerInfo` 도우미가 많은 진단 정보를 반환 하는 것을 볼 수 있습니다. `ServerInfo`에서 반환 하는 값에 대 한 자세한 내용은 MSDN 웹 사이트의 Microsoft TechNet 웹 사이트 및 [IIS 서버 변수](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) 에서 [인식할 수 있는 환경 변수](https://technet.microsoft.com/library/dd560744(WS.10).aspx) 를 참조 하십시오.

## <a name="embedding-output-expressions-to-display-page-values"></a>출력 식을 포함 하 여 페이지 값 표시

코드에서 발생 하는 상황을 확인 하는 또 다른 방법은 출력 식을 페이지에 포함 하는 것입니다. 사용자가 알고 있는 대로 `@myVariable` 또는 `@(subTotal * 12)` 같은 항목을 페이지에 추가 하 여 변수 값을 직접 출력할 수 있습니다. 디버깅을 위해 코드의 전략적 지점에 이러한 출력 식을 저장할 수 있습니다. 이렇게 하면 페이지가 실행 될 때 키 변수 값 또는 계산 결과를 볼 수 있습니다. 디버깅이 완료 되 면 식을 제거 하거나 주석 처리를 수행할 수 있습니다. 이 절차에서는 포함 식을 사용 하 여 페이지를 디버깅 하는 일반적인 방법을 보여 줍니다.

1. *Outputexpression. cshtml*라는 새 WebMatrix 페이지를 만듭니다.
2. 페이지 콘텐츠를 다음으로 바꿉니다.

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    이 예에서는 `switch` 문을 사용 하 여 `weekday` 변수의 값을 확인 한 다음 해당 요일에 따라 다른 출력 메시지를 표시 합니다. 예제에서 첫 번째 코드 블록 내의 `if` 블록은 현재 평일 값에 1 일을 더하여 요일을 임의로 변경 합니다. 이는 설명을 위해 도입 된 오류입니다.
3. 페이지를 저장 하 고 브라우저에서 실행 합니다.

    페이지에 잘못 된 요일에 대 한 메시지가 표시 됩니다. 실제로 어떤 요일에 해당 하는 경우에는 1 일 후에 메시지가 표시 됩니다. 이 경우에는 코드가 잘못 된 날짜 값을 의도적으로 설정 하기 때문에 메시지를 해제 하는 이유를 알 수 있지만 실제로는 코드에서 문제가 발생 하는 위치를 파악 하는 것이 어려운 경우가 많습니다. 디버깅 하려면 `weekday`와 같은 키 개체 및 변수의 값을 확인 해야 합니다.
4. 코드의 주석으로 표시 된 두 위치에 표시 된 대로 `@weekday`를 삽입 하 여 출력 식을 추가 합니다. 이러한 출력 식에는 코드 실행의 해당 지점에 변수 값이 표시 됩니다.

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. 브라우저에서 페이지를 저장 하 고 실행 합니다.

    이 페이지에는 요일이 먼저 표시 된 후 업데이트 된 요일이 1 일을 더한 후 결과 `switch` 메시지가 표시 됩니다. 출력에 HTML `<p>` 태그를 추가 하지 않았기 때문에 두 변수 식 (`@weekday`)의 출력에는 일 사이에 공백이 없습니다. 식은 테스트용 으로만 사용할 수 있습니다.

    ![디버깅-2](introduction-to-debugging/_static/image2.jpg)

    이제 오류가 발생 한 위치를 확인할 수 있습니다. 코드에 `weekday` 변수를 처음 표시 하면 올바른 날짜를 표시 합니다. 이를 두 번째로 표시 하면 코드의 `if` 블록 다음에 1이 표시 됩니다. 평일 변수의 첫 번째와 두 번째 모양 사이에 문제가 발생 했음을 알 수 있습니다. 실제 버그 인 경우 이러한 종류의 방식을 사용 하면 문제를 일으킨 코드의 위치를 좁힐 수 있습니다.
6. 추가한 두 개의 출력 식을 제거 하 고 요일을 변경 하는 코드를 제거 하 여 페이지의 코드를 수정 합니다. 나머지 전체 코드 블록은 다음 예제와 같습니다.

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. 브라우저에서 페이지를 실행 합니다. 이번에는 실제 요일의 표시 되는 올바른 메시지가 표시 됩니다.

## <a name="using-the-objectinfo-helper-to-display-object-values"></a>ObjectInfo 도우미를 사용 하 여 개체 값 표시

`ObjectInfo` 도우미는 전달 하는 각 개체의 유형 및 값을 표시 합니다. 이를 사용 하 여 코드의 변수 및 개체 값을 볼 수 있으며 (예: 이전 예제의 출력 식 처럼) 개체에 대 한 데이터 형식 정보를 볼 수 있습니다.

1. 이전에 만든 *Outputexpression. cshtml* 라는 파일을 엽니다.
2. 페이지의 모든 코드를 다음 코드 블록으로 바꿉니다.

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. 브라우저에서 페이지를 저장 하 고 실행 합니다.

    ![디버깅-4](introduction-to-debugging/_static/image3.jpg)

    이 예제에서 `ObjectInfo` 도우미는 다음과 같은 두 항목을 표시 합니다.

   - 유형입니다. 첫 번째 변수의 경우 형식은 `DayOfWeek`입니다. 두 번째 변수의 경우 형식은 `String`입니다.
   - 값입니다. 이 경우에는 페이지에 이미 인사말 변수 값을 표시 하기 때문에 변수를 `ObjectInfo`에 전달 하면 값이 다시 표시 됩니다.

     더 복잡 한 개체의 경우 `ObjectInfo` 도우미가 기본적으로 추가 정보 &#8212; 를 표시할 수 있으며, 모든 개체 속성의 형식 및 값을 표시할 수 있습니다.

## <a name="using-debugging-tools-in-visual-studio"></a>Visual Studio에서 디버깅 도구 사용

보다 포괄적인 디버깅 환경을 위해 [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)를 사용 합니다. Visual Studio를 사용 하 여 코드에서 검사 하려는 줄에 중단점을 설정할 수 있습니다.

![중단점 설정](introduction-to-debugging/_static/image1.png)

웹 사이트를 테스트할 때 실행 중인 코드가 중단점에서 중단 됩니다.

![reach 중단점](introduction-to-debugging/_static/image2.png)

변수의 현재 값을 검사 하 고 코드를 한 줄씩 단계별로 진행할 수 있습니다.

![값 참조](introduction-to-debugging/_static/image3.png)

Visual Studio에서 통합 디버거를 사용 하 여 ASP.NET Razor 페이지를 디버그 하는 방법에 대 한 자세한 내용은 [Visual studio를 사용 하 여 프로그래밍 ASP.NET 웹 페이지 (Razor)](https://go.microsoft.com/fwlink/?LinkId=205854)를 참조 하세요.

## <a name="additional-resources"></a>추가 리소스

- [Visual Studio를 사용 하 여 프로그래밍 ASP.NET 웹 페이지 (Razor)](https://go.microsoft.com/fwlink/?LinkId=205854)
- [IIS 서버 변수](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) (MSDN)
- [인식 된 환경 변수](https://technet.microsoft.com/library/dd560744(WS.10).aspx) (TechNet)
