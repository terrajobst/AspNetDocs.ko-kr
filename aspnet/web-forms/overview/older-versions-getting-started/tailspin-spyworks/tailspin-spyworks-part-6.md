---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: '6 부: ASP.NET 멤버 자격 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 6 부는 ASP.NET 멤버 자격을 추가 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454883"
---
# <a name="part-6-aspnet-membership"></a>6 부: ASP.NET 멤버 자격

만든 사람 [Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다. ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 6 부는 ASP.NET 멤버 자격을 추가 합니다.

## <a id="_Toc260221672"></a>ASP.NET 멤버 자격 사용

![](tailspin-spyworks-part-6/_static/image1.png)

보안을 클릭 합니다.

![](tailspin-spyworks-part-6/_static/image1.jpg)

폼 인증을 사용 하 고 있는지 확인 합니다.

![](tailspin-spyworks-part-6/_static/image2.jpg)

"사용자 만들기" 링크를 사용 하 여 두 명의 사용자를 만들 수 있습니다.

![](tailspin-spyworks-part-6/_static/image3.jpg)

완료 되 면 솔루션 탐색기 창을 참조 하 고 보기를 새로 고칩니다.

![](tailspin-spyworks-part-6/_static/image2.png)

ASPNETDB.MDF를 확인 합니다. MDF를 만들었습니다. 이 파일에는 멤버 자격과 같은 핵심 ASP.NET 서비스를 지 원하는 테이블이 포함 되어 있습니다.

이제 체크 아웃 프로세스의 구현을 시작할 수 있습니다.

먼저 CheckOut .aspx 페이지를 만듭니다.

체크 인 한 사용자만 체크 인 .aspx 페이지를 사용할 수 있으므로 로그인 한 사용자에 대 한 액세스를 제한 하 고 로그인 페이지에 로그인 하지 않은 사용자를 리디렉션할 수 있습니다.

이렇게 하려면 web.config 파일의 구성 섹션에 다음을 추가 합니다.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

ASP.NET Web Forms 응용 프로그램에 대 한 템플릿은 인증 섹션을 web.config 파일에 자동으로 추가 하 고 기본 로그인 페이지를 설정 합니다.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

사용자가 로그인 할 때 익명 쇼핑 카트를 마이그레이션하려면 로그인 .aspx 코드 뒤에 있는 파일을 수정 해야 합니다. 페이지\_Load 이벤트를 다음과 같이 변경 합니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

그런 다음 "LoggedIn" 이벤트 처리기를 추가 하 여 새로 로그인 한 사용자에 게 세션 이름을 설정 하 고 MyShoppingCart 클래스에서 MigrateCart 메서드를 호출 하 여 장바구니의 임시 세션 id를 사용자의 임시 세션 id로 변경 합니다. (.Cs 파일에서 구현 됨)

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

이와 같이 MigrateCart () 메서드를 구현 합니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

체크아웃할 때 쇼핑 카트 페이지에서와 마찬가지로 체크 아웃 페이지에서 EntityDataSource 및 GridView를 사용 합니다.

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

GridView 컨트롤은 MyList\_RowDataBound 바인딩된 "이벤트 처리기를 지정 하므로 다음과 같이 해당 이벤트 처리기를 구현 해 보겠습니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

이 방법은 각 행이 바인딩될 때 쇼핑 카트의 누계를 유지 하 고 GridView의 아래쪽 행을 업데이트 합니다.

이 단계에서는 배치할 주문에 대 한 "검토" 프레젠테이션을 구현 했습니다.

페이지\_Load 이벤트에 몇 줄의 코드를 추가 하 여 빈 카트 시나리오를 처리 해 보겠습니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

사용자가 "제출" 단추를 클릭 하면 제출 단추 클릭 이벤트 처리기에서 다음 코드가 실행 됩니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

주문 제출 프로세스의 "기타"는 MyShoppingCart 클래스의 SubmitOrder () 메서드를 통해 구현 됩니다.

SubmitOrder는 다음과 같습니다.

- 쇼핑 카트에 있는 모든 품목을 가져와 새 주문 레코드와 연결 된 OrderDetails 레코드를 만듭니다.
- 운송 날짜를 계산 합니다.
- 쇼핑 카트를 지웁니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

이 샘플 응용 프로그램의 목적에 따라 현재 날짜에 2 일을 추가 하 여 운송 날짜를 계산 합니다.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

이제 응용 프로그램을 실행 하면 쇼핑 프로세스를 처음부터 끝까지 테스트할 수 있습니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-5.md)
> [다음](tailspin-spyworks-part-7.md)
