---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: ASP.NET 웹 페이지 (Razor) 사이트에서 도우미 만들기 및 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 도우미를 만드는 방법을 설명 합니다. 도우미는 성능에 코드 및 태그를 포함 하는 다시 사용할 수 있는 구성 요소입니다.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454307"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 도우미 만들기 및 사용

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 도우미를 만드는 방법을 설명 합니다. *도우미* 는 지루한 또는 복잡할 수 있는 작업을 수행 하기 위한 코드와 태그를 포함 하는 재사용 가능한 구성 요소입니다.
> 
> **학습 내용:** 
> 
> - 간단한 도우미를 만들고 사용 하는 방법입니다.
> 
> 다음은이 문서에 도입 된 ASP.NET 기능입니다.
> 
> - `@helper` 구문입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.

## <a name="overview-of-helpers"></a>도우미 개요

사이트의 서로 다른 페이지에서 동일한 작업을 수행 해야 하는 경우 도우미를 사용할 수 있습니다. ASP.NET 웹 페이지에는 많은 도우미가 포함 되어 있으며 다운로드 하 고 설치할 수 있는 많은 기능이 있습니다. ASP.NET 웹 페이지의 기본 제공 도우미 목록은 [ASP.NET API 빠른 참조](https://go.microsoft.com/fwlink/?LinkId=202907)에 나열 되어 있습니다. 사용자의 요구를 충족 하는 기존 도우미가 없는 경우 사용자 고유의 도우미를 만들 수 있습니다.

도우미를 사용 하면 여러 페이지에서 공통 코드 블록을 사용할 수 있습니다. 페이지에서 일반적으로 일반 단락과 별도로 설정 된 메모 항목을 만들려고 한다고 가정 합니다. 노트는 테두리가 있는 상자로 스타일을 지정 하는 `<div>` 요소로 생성 될 것입니다. 메모를 표시 하려고 할 때마다 동일한 태그를 페이지에 추가 하는 대신 태그를 도우미로 패키지할 수 있습니다. 그런 다음 필요에 맞게 한 줄의 코드를 사용 하 여 메모를 삽입할 수 있습니다.

이와 같은 도우미를 사용 하면 각 페이지의 코드를 보다 간단 하 고 쉽게 읽을 수 있습니다. 또한 노트의 모양을 변경 해야 하는 경우에는 한 곳에서 태그를 변경할 수 있기 때문에 사이트를 더 쉽게 유지 관리할 수 있습니다.

## <a name="creating-a-helper"></a>도우미 만들기

이 절차에서는 설명 된 대로 메모를 만드는 도우미를 만드는 방법을 보여 줍니다. 이는 간단한 예제 이지만 사용자 지정 도우미에는 필요한 모든 태그 및 ASP.NET 코드가 포함 될 수 있습니다.

1. 웹 사이트의 루트 폴더에서 *App\_Code*라는 폴더를 만듭니다. ASP.NET에서 도우미와 같은 구성 요소에 대 한 코드를 넣을 수 있는 예약 된 폴더 이름입니다.
2. *앱\_코드* 폴더에서 새 *cshtml* 파일을 만들고 이름을 myororors로 만듭니다.
3. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    이 코드는 `@helper` 구문을 사용 하 여 `MakeNote`라는 새 도우미를 선언 합니다. 이 특정 도우미를 사용 하면 텍스트와 태그의 조합을 포함할 수 있는 `content` 매개 변수를 전달할 수 있습니다. 도우미는 `@content` 변수를 사용 하 여 메모 본문에 문자열을 삽입 합니다.

    파일 이름은 *myhelpers. cshtml*이지만 도우미의 이름은 `MakeNote`입니다. 단일 파일에 여러 사용자 지정 도우미를 넣을 수 있습니다.
4. 파일을 저장하고 닫습니다.

## <a name="using-the-helper-in-a-page"></a>페이지에서 도우미 사용

1. 루트 폴더에서 *TestHelper*라는 비어 있는 새 파일을 만듭니다.
2. 파일에 다음 코드를 추가합니다.

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    만든 도우미를 호출 하려면 `@`와 도우미가 있는 파일 이름, 점, 도우미 이름을 차례로 사용 합니다. *앱\_코드* 폴더에 여러 폴더가 있는 경우 `@FolderName.FileName.HelperName` 구문을 사용 하 여 모든 중첩 된 폴더 수준 내에서 도우미를 호출할 수 있습니다. 괄호 안에 인용 부호로 추가 하는 텍스트는 도우미가 웹 페이지에 있는 메모의 일부로 표시 하는 텍스트입니다.
3. 페이지를 저장 하 고 브라우저에서 실행 합니다. 도우미는 도우미를 호출한 경우 두 단락 사이에 메모 항목을 생성 합니다.

    ![브라우저의 페이지와 도우미가 지정 된 텍스트 주위에 상자를 넣는 태그를 생성 하는 방법을 보여 주는 스크린샷](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a>추가 리소스

[Razor 도우미로 서의 가로 메뉴](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)입니다. Mike Pope이 블로그 항목은 태그, CSS 및 코드를 사용 하 여 도우미로 가로 메뉴를 만드는 방법을 보여 줍니다.

[WebMatrix 및 ASP.NET MVC3에 대 한 ASP.NET 웹 페이지 도우미에서 HTML5 활용](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx) Sam Abraham이 블로그 항목에는 HTML5 `Canvas` 요소를 렌더링 하는 도우미가 표시 됩니다.

[WebMatrix의 @Helpers와 @Functions 간의 차이점](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)입니다. Mike Brind의이 블로그 항목에서는 구문 및 `@function` 구문과 각 구문을 사용 하는 경우 `@helper` 설명 합니다.
