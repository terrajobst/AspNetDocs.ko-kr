---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: Visual Studio 2013에서 스 캐 폴딩 ASP.NET | Microsoft Docs
author: Rick-Anderson
description: ASP.NET 스 캐 폴딩은 Visual Studio 2013에 포함 된 새로운 기능입니다.
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449567"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a>Visual Studio 2013에서 ASP.NET 스캐폴딩

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET 스 캐 폴딩은 Visual Studio 2013에 포함 된 새로운 기능입니다.

## <a name="overview"></a>개요

ASP.NET 스 캐 폴딩은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다. Visual Studio 2013 MVC 및 Web API 프로젝트용으로 미리 설치 된 코드 생성기를 포함 합니다. 데이터 모델과 상호 작용 하는 코드를 신속 하 게 추가 하려는 경우 프로젝트에 스 캐 폴딩을 추가 합니다. 스 캐 폴딩을 사용 하면 프로젝트에서 표준 데이터 작업을 개발 하는 데 걸리는 시간을 줄일 수 있습니다.

기본적으로 Visual Studio 2013는 Web Forms 프로젝트에 대 한 코드 생성을 지원 하지 않지만 프로젝트에 MVC 종속성을 추가 하거나 확장을 설치 하 여 Web Forms에서 스 캐 폴딩을 사용할 수 있습니다. 두 가지 방법은 다음과 같습니다.

Visual Studio 2013 업데이트 2 (현재 RC)는 시나리오 요구 사항에 맞게 ASP.NET 스 캐 폴딩을 확장 하는 기능을 제공 합니다. 이 기능을 사용 하면 사용자 지정 된 스 캐 폴딩 템플릿을 만들고이를 추가 하 여 새 스 캐 폴드 대화 상자를 추가할 수 있습니다. 사용자 지정 된 템플릿 내에서 스 캐 폴드 항목을 추가할 때 생성 되는 코드를 지정 합니다. 자세한 내용은 [Visual Studio에 대 한 사용자 지정 스 캐 폴더 만들기](https://go.microsoft.com/fwlink/p/?LinkId=395029)를 참조 하세요.

## <a name="prerequisites"></a>사전 요구 사항

ASP.NET 스 캐 폴딩을 사용 하려면 다음이 있어야 합니다.

- Microsoft Visual Studio 2013
- 웹 개발자 도구 (기본 Visual Studio 2013 설치의 일부)
- ASP.NET 웹 프레임 워크 및 도구 2013 (기본 Visual Studio 2013 설치의 일부)

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a>MVC 또는 Web API에 스 캐 폴드 항목 추가

스 캐 폴드를 추가 하려면 다음 그림에 표시 된 것 처럼 프로젝트 또는 프로젝트 내의 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** – **새 스 캐 폴드 항목**을 선택 합니다.

![스 캐 폴드 항목 추가](aspnet-scaffolding-overview/_static/image1.png)

**스 캐 폴드 추가** 창에서 추가할 스 캐 폴드의 유형을 선택 합니다.

![스 캐 폴드 유형 선택](aspnet-scaffolding-overview/_static/image2.png)

**컨트롤러 추가** 창에서는 Entity Framework 6에서 새로운 비동기 기능을 사용할지 여부를 비롯 하 여 컨트롤러를 생성 하는 옵션을 선택할 수 있습니다.

![컨트롤러 추가](aspnet-scaffolding-overview/_static/image3.png)

시나리오에 대 한 관련 클래스 및 페이지가 생성 됩니다. 예를 들어 다음 이미지는 동영상과 같은 모델 클래스에 대해 스 캐 폴딩을 통해 생성 된 MVC 컨트롤러 및 뷰를 보여 줍니다.

![만든 파일](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a>Web Forms에 스 캐 폴드 항목 추가

Web Forms 코드를 생성 하는 스 캐 폴딩을 추가 하려면 Visual Studio에 확장을 설치 하거나 MVC 종속성을 추가 해야 합니다. 두 방법 모두 아래에 표시 되지만 이러한 방법 중 하나를 수행 하기만 하면 됩니다.

### <a name="web-forms-scaffolding-extension"></a>Web Forms 스 캐 폴딩 확장

Web Forms 프로젝트에서 스 캐 폴딩을 사용할 수 있도록 하는 Visual Studio 확장을 설치할 수 있습니다. Visual Studio에서 **도구** , **확장 및 업데이트**를 차례로 선택 합니다. 이 대화 상자에서 **Web Forms 스 캐 폴딩**에 대 한 Visual Studio 갤러리를 검색 합니다.

![web forms 스 캐 폴딩 설치](aspnet-scaffolding-overview/_static/image5.png)

자세한 내용은 [Web Forms 스 캐 폴딩](https://go.microsoft.com/fwlink/p/?LinkId=396478)(영문)을 참조 하세요.

### <a name="mvc-dependencies"></a>MVC 종속성

MVC 종속성을 추가 하려면 **추가** - **새 스 캐 폴드 항목**을 선택 합니다. 스 캐 폴드 추가 창에서 아래와 같이 **MVC 종속성**을 선택 합니다.

![MVC 종속성 추가](aspnet-scaffolding-overview/_static/image6.png)

MVC 스 캐 폴딩에 대 한 두 가지 옵션이 있습니다. 최소 및 전체. 최소를 선택 하면 ASP.NET MVC에 대 한 NuGet 패키지 및 참조만 프로젝트에 추가 됩니다. 전체 옵션을 선택 하는 경우 최소 종속성 뿐만 아니라 MVC 프로젝트에 필요한 콘텐츠 파일이 추가 됩니다. 스 캐 폴딩을 쉽게 사용 하려면 전체 종속성을 선택 합니다.

![전체 종속성 선택](aspnet-scaffolding-overview/_static/image7.png)

종속성을 추가 하면 **readme.txt** 파일이 표시 됩니다. 이 파일의 지침에 따라 프로젝트가 제대로 작동 하는지 확인 합니다.

Readme.txt 파일의 단계를 완료 한 후에는 MVC 및 Web API에 대 한 이전 섹션에 표시 된 대로 새 스 캐 폴드 항목을 추가할 수 있습니다. 자동으로 생성 된 뷰와 컨트롤러는 프로젝트 내에서 제대로 작동 합니다.

## <a name="tutorials"></a>자습서

사용자 지정 스 캐 폴더를 만들려면 [Visual Studio 용 사용자 지정 스 캐 폴더 만들기](https://go.microsoft.com/fwlink/p/?LinkId=395029)를 참조 하세요.

생성 된 파일을 사용자 지정 하려면 [새 스 캐 폴드 항목 대화 상자에서 생성 된 파일을 사용자 지정 하는 방법](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx)을 참조 하세요.

**Database First 개발**에서 스 캐 폴딩 사용에 대 한 예제는 [ASP.NET MVC를 사용 하는 EF Database First](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md)를 참조 하세요.

**MVC** 프로젝트에서 스 캐 폴딩 사용에 대 한 예제는 [ASP.NET MVC 5 시작](../../../mvc/overview/getting-started/introduction/getting-started.md)을 참조 하세요.

**WEB api** 프로젝트에서 스 캐 폴딩을 사용 하는 예제는 [web Api 2에서 특성 라우팅을 사용 하 여 REST API 만들기](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md)를 참조 하세요.
