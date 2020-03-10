---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: ASP.NET MVC 실행 프로세스 이해 | Microsoft Docs
author: microsoft
description: ASP.NET MVC 프레임 워크에서 브라우저 요청을 단계별로 처리 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435455"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>ASP.NET MVC 실행 프로세스 이해

[Microsoft](https://github.com/microsoft) 에서

> ASP.NET MVC 프레임 워크에서 브라우저 요청을 단계별로 처리 하는 방법을 알아봅니다.

ASP.NET MVC 기반 웹 응용 프로그램에 대 한 요청은 먼저 HTTP 모듈인 **Urlroutingmodule** 개체를 통과 합니다. 이 모듈에서는 요청을 구문 분석하고 경로 선택을 수행합니다. **Urlroutingmodule** 개체는 현재 요청과 일치 하는 첫 번째 경로 개체를 선택 합니다. 경로 개체는 **RouteBase**을 구현 하는 클래스 이며 일반적으로 **경로** 클래스의 인스턴스입니다. 경로가 일치 하지 않으면 **Urlroutingmodule** 개체는 아무 작업도 수행 하지 않으며 요청이 일반 ASP.NET 또는 IIS 요청 처리로 대체 될 수 있습니다.

선택한 **경로** 개체에서 **Urlroutingmodule** 개체는 **Route** 개체와 연결 된 **IRouteHandler** 개체를 가져옵니다. 일반적으로 MVC 응용 프로그램에서이는 **MvcRouteHandler**의 인스턴스입니다. **IRouteHandler** 인스턴스는 **IHttpHandler** 개체를 만들고 **ihttpcontext** 개체를 전달 합니다. 기본적으로 MVC에 대 한 **IHttpHandler** 인스턴스는 **MvcHandler** 개체입니다. 그런 다음 **MvcHandler** 개체는 궁극적으로 요청을 처리 하는 컨트롤러를 선택 합니다.

> [!NOTE]
> ASP.NET MVC 웹 응용 프로그램이 IIS 7.0에서 실행될 경우 MVC 프로젝트의 파일 확장명은 필요하지 않습니다. 그러나 IIS 6.0에서는 처리기의 요청에 따라 .mvc 파일 확장명을 ASP.NET ISAPI DLL에 매핑해야 합니다.

모듈 및 처리기는 ASP.NET MVC 프레임 워크에 대 한 진입점입니다. 두 클래스에서는 다음 작업을 수행합니다.

- MVC 웹 응용 프로그램에서 적절한 컨트롤러를 선택합니다.
- 특정 컨트롤러 인스턴스를 가져옵니다.
- 컨트롤러의 **Execute** 메서드를 호출 합니다.

다음은 MVC 웹 프로젝트에 대 한 실행 단계를 나열 합니다.

- 응용 프로그램에 대한 첫 번째 요청 받기 

    - Global.asax 파일에서 **경로** 개체는 **RouteTable** 개체에 추가 됩니다.
- 라우팅 수행 

    - **Urlroutingmodule** 모듈은 **RouteTable** 컬렉션에서 첫 번째로 일치 하는 **경로** 개체를 사용 하 여 **RouteData** 개체를 만든 다음이 개체를 사용 하 여 **RequestContext** (**ihttpcontext**) 개체를 만듭니다.
- MVC 요청 처리기 만들기 

    - **MvcRouteHandler** 개체는 **MvcHandler** 클래스의 인스턴스를 만들고 **RequestContext** 인스턴스로 전달 합니다.
- 컨트롤러 만들기 

    - **MvcHandler** 개체는 **RequestContext** 인스턴스를 사용 하 여 **IControllerFactory** 개체 (일반적으로 **defaultcontrollerfactory** 클래스의 인스턴스)를 식별 합니다 .이 개체는를 사용 하 여 컨트롤러 인스턴스를 만듭니다.
- 컨트롤러 실행- **MvcHandler** 인스턴스는 컨트롤러의 **execute** 메서드를 호출 합니다. |
- 작업 호출 

    - 대부분의 컨트롤러는 **컨트롤러** 기본 클래스에서 상속 합니다. 이렇게 하는 컨트롤러의 경우 컨트롤러와 연결 된 **Controlleractioninvoker** 개체는 호출할 컨트롤러 클래스의 작업 메서드를 결정 한 다음 해당 메서드를 호출 합니다.
- 결과 실행 

    - 일반적인 동작 메서드는 사용자 입력을 수신 하 고 적절 한 응답 데이터를 준비한 다음 결과 형식을 반환 하 여 결과를 실행할 수 있습니다. 실행할 수 있는 기본 제공 결과 형식에는 **viewresult** (뷰를 렌더링 하 고 가장 자주 사용 되는 결과 형식), **RedirectToRouteResult**, **redirectresult**, **contentresult**, **JsonResult**및 **EmptyResult**가 포함 됩니다.
