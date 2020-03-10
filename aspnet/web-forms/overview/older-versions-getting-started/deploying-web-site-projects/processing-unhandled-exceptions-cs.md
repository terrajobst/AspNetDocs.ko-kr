---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs
title: 처리 되지 않은 예외C#처리 () | Microsoft Docs
author: rick-anderson
description: 프로덕션의 웹 응용 프로그램에서 런타임 오류가 발생 하는 경우 개발자에 게 알리고 오류를 기록 하 여 la에서 진단할 수 있도록 하는 것이 중요 합니다.
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 5bc1afd5-2484-4528-b158-ab218ba150e8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs
msc.type: authoredcontent
ms.openlocfilehash: 27d827238d944f86cd913d2b8ecd12729b99f391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510659"
---
# <a name="processing-unhandled-exceptions-c"></a>처리되지 않은 예외 처리(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[예제 코드 살펴보기 및 다운로드](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs/samples) ([다운로드 방법](/aspnet/core/tutorials/index#how-to-download-a-sample))

> 프로덕션의 웹 응용 프로그램에서 런타임 오류가 발생 하는 경우 나중에 진단할 수 있도록 개발자에 게 알리고 오류를 기록 하는 것이 중요 합니다. 이 자습서에서는 ASP.NET에서 런타임 오류를 처리 하 고, 처리 되지 않은 예외가 ASP.NET 런타임에 버블링 될 때마다 사용자 지정 코드를 실행 하는 한 가지 방법을 보여 줍니다.

## <a name="introduction"></a>소개

ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생 하면 ASP.NET 런타임으로 버블링 되어 `Error` 이벤트를 발생 시키고 적절 한 오류 페이지가 표시 됩니다. 오류 페이지에는 다음과 같은 세 가지 유형이 있습니다. 런타임 오류 노란색 화면 (YSOD)은 예외 정보입니다. 및 사용자 지정 오류 페이지. [이전 자습서](displaying-a-custom-error-page-cs.md) 에서는 원격 사용자에 대 한 사용자 지정 오류 페이지를 사용 하도록 응용 프로그램을 구성 하 고 로컬에서 방문 하는 사용자에 대 한 예외 정보를 구성 했습니다.

사이트의 모양과 느낌을 일치 시키는 사람이 친숙 한 사용자 지정 오류 페이지를 사용 하면 기본 런타임 오류 메시지가 표시 되지만 사용자 지정 오류 페이지를 표시 하는 것은 포괄적인 오류 처리 솔루션의 한 부분입니다. 프로덕션 환경에서 응용 프로그램에 오류가 발생 하는 경우 개발자에 게 예외의 원인을 unearth 하 고 해결할 수 있도록 오류에 대 한 알림이 표시 되는 것이 중요 합니다. 또한 나중에 오류를 검사 하 고 진단할 수 있도록 오류의 세부 정보를 기록해 야 합니다.

이 자습서에서는 처리 되지 않은 예외에 대 한 세부 정보에 액세스 하 여 개발자에 게 알릴 수 있도록 하는 방법을 보여 줍니다. 이 자습서를 수행 하는 두 가지 자습서에서는 약간의 구성 후 개발자가 런타임 오류를 자동으로 알리고 세부 정보를 기록 하는 오류 로깅 라이브러리를 탐색 합니다.

> [!NOTE]
> 이 자습서에서 검사 한 정보는 처리 되지 않은 예외를 고유 하거나 사용자 지정 된 방식으로 처리 해야 하는 경우에 가장 유용 합니다. 예외를 기록 하 고 개발자에 게 알려야 하는 경우에는 오류 로깅 라이브러리를 사용 하 여 이동 해야 합니다. 다음 두 자습서에서는 이러한 두 라이브러리에 대 한 개요를 제공 합니다.

## <a name="executing-code-when-theerrorevent-is-raised"></a>`Error`이벤트가 발생할 때 코드 실행

이벤트는 흥미로운 요소가 발생 했음을 알리는 메커니즘과 다른 개체가 응답으로 코드를 실행 하는 데 사용할 수 있는 메커니즘을 개체에 제공 합니다. ASP.NET 개발자는 이벤트 측면에서 생각 하는 데 익숙할 것입니다. 방문자가 특정 단추를 클릭할 때 코드를 실행 하려는 경우 해당 단추의 `Click` 이벤트에 대 한 이벤트 처리기를 만들고 코드를 저장 합니다. 처리 되지 않은 예외가 발생할 때마다 ASP.NET 런타임이 [`Error` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx) 를 발생 시키는 경우 오류 세부 정보를 기록 하는 코드는 이벤트 처리기로 이동 합니다. 하지만 `Error` 이벤트에 대 한 이벤트 처리기를 만들려면 어떻게 해야 하나요?

`Error` 이벤트는 요청 수명 동안 HTTP 파이프라인의 특정 단계에서 발생 하는 [`HttpApplication` 클래스](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) 의 여러 이벤트 중 하나입니다. 예를 들어, `HttpApplication` 클래스의 [`BeginRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx) 는 모든 요청을 시작할 때 발생 합니다. 보안 모듈에서 요청자를 식별 한 경우 해당 [`AuthenticateRequest` 이벤트가](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx) 발생 합니다. 이러한 `HttpApplication` 이벤트는 페이지 개발자에 게 요청 수명의 다양 한 지점에서 사용자 지정 논리를 실행 하는 방법을 제공 합니다.

`HttpApplication` 이벤트에 대 한 이벤트 처리기는 `Global.asax`라는 특수 파일에 배치할 수 있습니다. 웹 사이트에서이 파일을 만들려면 이름이 `Global.asax`인 전역 응용 프로그램 클래스 템플릿을 사용 하 여 웹 사이트의 루트에 새 항목을 추가 합니다.

[![](processing-unhandled-exceptions-cs/_static/image2.png)](processing-unhandled-exceptions-cs/_static/image1.png)

**그림 1**: 웹 응용 프로그램에 `Global.asax` 추가  
([전체 크기 이미지를 보려면 클릭](processing-unhandled-exceptions-cs/_static/image3.png))

Visual Studio에서 만든 `Global.asax` 파일의 내용과 구조는 WAP (웹 응용 프로그램 프로젝트)를 사용 하는지 또는 WSP (웹 사이트 프로젝트)를 사용 하는지에 따라 약간 다릅니다. WAP를 사용 하면 `Global.asax` 두 개의 개별 파일 (`Global.asax` 및 `Global.asax.cs`으로 구현 됩니다. `Global.asax` 파일에는 `.cs` 파일을 참조 하는 `@Application` 지시문이 포함 되어 있지 않습니다. 관심 있는 이벤트 처리기는 `Global.asax.cs` 파일에 정의 되어 있습니다. WSPs의 경우, `Global.asax`한 파일만 만들어지고 이벤트 처리기는 `<script runat="server">` 블록에 정의 됩니다.

Visual Studio의 전역 응용 프로그램 클래스 템플릿에 의해 WAP에서 만든 `Global.asax` 파일에는 각각 `Application_BeginRequest`, `Application_AuthenticateRequest`및 `Application_Error`이라는 이벤트 처리기가 포함 됩니다 .이 처리기는 각각 `HttpApplication`, `BeginRequest`, `AuthenticateRequest`에 대 한 이벤트 처리기입니다.`Error` `Application_Start`, `Session_Start`, `Application_End`및 `Session_End`이라는 이벤트 처리기도 있습니다 .이 이벤트 처리기는 웹 응용 프로그램이 시작 될 때, 새 세션이 시작 될 때, 응용 프로그램이 종료 될 때 및 세션이 종료 될 때 발생 하는 이벤트 처리기입니다. Visual Studio에서 WSP에 만든 `Global.asax` 파일에는 `Application_Error`, `Application_Start`, `Session_Start`, `Application_End`및 `Session_End` 이벤트 처리기만 포함 됩니다.

> [!NOTE]
> ASP.NET 응용 프로그램을 배포 하는 경우 프로덕션 환경에 `Global.asax` 파일을 복사 해야 합니다. 이 코드는 프로젝트의 어셈블리로 컴파일되기 때문에 WAP에서 만든 `Global.asax.cs` 파일을 프로덕션에 복사할 필요가 없습니다.

Visual Studio의 전역 응용 프로그램 클래스 템플릿으로 만든 이벤트 처리기는 완전 하지 않습니다. 이벤트 처리기 `Application_EventName`이름을 지정 하 여 `HttpApplication` 이벤트에 대 한 이벤트 처리기를 추가할 수 있습니다. 예를 들어 `Global.asax` 파일에 다음 코드를 추가 하 여 [`AuthorizeRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)에 대 한 이벤트 처리기를 만들 수 있습니다.

[!code-cs[Main](processing-unhandled-exceptions-cs/samples/sample1.cs)]

마찬가지로, 필요 하지 않은 전역 응용 프로그램 클래스 템플릿으로 만든 모든 이벤트 처리기를 제거할 수 있습니다. 이 자습서에서는 `Error` 이벤트에 대 한 이벤트 처리기만 필요 합니다. `Global.asax` 파일에서 다른 이벤트 처리기를 제거 합니다.

> [!NOTE]
> *HTTP 모듈* 은 `HttpApplication` 이벤트에 대 한 이벤트 처리기를 정의 하는 또 다른 방법을 제공 합니다. HTTP 모듈은 웹 응용 프로그램 프로젝트 내에 직접 배치 되거나 별도의 클래스 라이브러리로 분리 될 수 있는 클래스 파일로 생성 됩니다. HTTP 모듈은 클래스 라이브러리로 분리 될 수 있으므로 `HttpApplication` 이벤트 처리기를 만들기 위한 보다 유연 하 고 재사용 가능한 모델을 제공 합니다. `Global.asax` 파일은 상주 하는 웹 응용 프로그램에만 적용 되는 반면 http 모듈은 어셈블리로 컴파일할 수 있습니다. 웹 사이트에 HTTP 모듈을 추가 하는 것은 `Bin` 폴더에 어셈블리를 놓고 `Web.config`에 모듈을 등록 하는 것 만큼 간단 합니다. 이 자습서는 HTTP 모듈을 만들고 사용 하는 것을 확인 하지는 않지만 다음 두 자습서에서 사용 되는 두 개의 오류 로깅 라이브러리는 HTTP 모듈로 구현 됩니다. HTTP 모듈의 이점에 대 한 자세한 배경 정보는 [Http 모듈 및 처리기를 사용 하 여 플러그형 ASP.NET 구성 요소 만들기](https://msdn.microsoft.com/library/aa479332.aspx)를 참조 하세요.

## <a name="retrieving-information-about-the-unhandled-exception"></a>처리 되지 않은 예외에 대 한 정보 검색

이 시점에서 `Application_Error` 이벤트 처리기를 사용 하는 global.asax 파일이 있습니다. 이 이벤트 처리기가 실행 될 때 개발자에 게 오류를 알리고 세부 정보를 기록해 야 합니다. 이러한 작업을 수행 하려면 먼저 발생 한 예외에 대 한 세부 정보를 확인 해야 합니다. 서버 개체의 [`GetLastError` 메서드](https://msdn.microsoft.com/library/system.web.httpserverutility.getlasterror.aspx) 를 사용 하 여 `Error` 이벤트를 발생 시킨 처리 되지 않은 예외에 대 한 세부 정보를 검색 합니다.

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample2.cs)]

`GetLastError` 메서드 `Exception`형식의 개체를 반환 합니다 .이 개체는 .NET Framework의 모든 예외에 대 한 기본 형식입니다. 그러나 위의 코드에서는 `GetLastError`에 의해 반환 되는 예외 개체를 `HttpException` 개체로 캐스팅 합니다. ASP.NET 리소스를 처리 하는 동안 예외가 발생 하 여 `Error` 이벤트가 발생 하는 경우 throw 된 예외가 `HttpException`에 래핑됩니다. 바뀌고 속성을 `InnerException` 사용 하 여 오류 이벤트를 발생 시키는 실제 예외를 가져옵니다. 존재 하지 않는 페이지에 대 한 요청과 같은 HTTP 기반 예외로 인해 `Error` 이벤트가 발생 한 경우에는 `HttpException` throw 되지만 내부 예외는 발생 하지 않습니다.

다음 코드는 `GetLastErrormessage`를 사용 하 여 `Error` 이벤트를 트리거한 예외에 대 한 정보를 검색 하 고 `HttpException`를 `lastErrorWrapper`라는 변수에 저장 합니다. 그런 다음 원래 예외의 형식, 메시지 및 스택 추적을 세 개의 문자열 변수에 저장 하 고, `lastErrorWrapper`이 `Error` 이벤트를 트리거한 실제 예외 (HTTP 기반 예외의 경우) 인지 아니면 요청을 처리 하는 동안 throw 된 예외에 대 한 래퍼 인지를 확인 합니다.

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample3.cs)]

이 시점에서 데이터베이스 테이블에 예외의 세부 정보를 기록 하는 코드를 작성 하는 데 필요한 모든 정보가 있습니다. 요청 된 페이지의 URL 및 현재 로그온 한 사용자의 이름과 같은 다른 유용한 정보를 비롯 하 여 각 오류 정보 (예: 유형, 메시지, 스택 추적 등)에 대 한 열이 포함 된 데이터베이스 테이블을 만들 수 있습니다. 그런 다음 `Application_Error` 이벤트 처리기에서 데이터베이스에 연결 하 여 테이블에 레코드를 삽입 합니다. 마찬가지로 전자 메일을 통해 오류를 개발자에 게 알리는 코드를 추가할 수 있습니다.

다음 두 자습서에서 검사 한 오류 로깅 라이브러리는 이러한 기능을 즉시 제공 하므로이 오류 로깅 및 알림을 직접 작성할 필요가 없습니다. 그러나 `Error` 이벤트가 발생 하 고 `Application_Error` 이벤트 처리기를 사용 하 여 오류 정보를 기록 하 고 개발자에 게 알릴 수 있도록 하려면 오류가 발생할 때 개발자에 게 알리는 코드를 추가 해 보겠습니다.

## <a name="notifying-a-developer-when-an-unhandled-exception-occurs"></a>처리 되지 않은 예외가 발생할 때 개발자에 게 알림

프로덕션 환경에서 처리 되지 않은 예외가 발생 하는 경우 오류를 평가 하 고 수행 해야 하는 작업을 결정할 수 있도록 개발 팀에 경고 하는 것이 중요 합니다. 예를 들어 데이터베이스에 연결 하는 동안 오류가 발생 하는 경우 연결 문자열을 다시 확인 하 고 웹 호스팅 회사에서 지원 티켓을 열어야 할 수도 있습니다. 프로그래밍 오류로 인해 예외가 발생 한 경우 나중에 이러한 오류를 방지 하기 위해 추가 코드 또는 유효성 검사 논리를 추가 해야 할 수 있습니다.

[`System.Net.Mail` 네임 스페이스](https://msdn.microsoft.com/library/system.net.mail.aspx) 의 .NET Framework 클래스를 사용 하면 전자 메일을 쉽게 보낼 수 있습니다. [`MailMessage` 클래스](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx) 는 전자 메일 메시지를 나타내며 `To`, `From`, `Subject`, `Body`및 `Attachments`와 같은 속성을 포함 합니다. `SmtpClass`는 지정 된 SMTP 서버를 사용 하 여 `MailMessage` 개체를 전송 하는 데 사용 됩니다. SMTP 서버 설정은 `Web.config file`의 [`<system.net>` 요소](https://msdn.microsoft.com/library/6484zdc1.aspx) 에서 프로그래밍 방식으로 또는 선언적으로 지정할 수 있습니다. ASP.NET 응용 프로그램에서 전자 메일 메시지를 보내는 방법에 대 한 자세한 내용은 [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)및 [시스템 .NET. 메일 FAQ](http://systemnetmail.com/)를 참조 하세요.

> [!NOTE]
> `<system.net>` 요소에는 전자 메일을 보낼 때 `SmtpClient` 클래스에서 사용 하는 SMTP 서버 설정이 포함 되어 있습니다. 웹 호스팅 회사에는 응용 프로그램에서 전자 메일을 보내는 데 사용할 수 있는 SMTP 서버가 있을 수 있습니다. 웹 응용 프로그램에서 사용 해야 하는 SMTP 서버 설정에 대 한 자세한 내용은 웹 호스트의 지원 섹션을 참조 하세요.

다음 코드를 `Application_Error` 이벤트 처리기에 추가 하 여 오류가 발생 하면 개발자에 게 전자 메일을 보냅니다.

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample4.cs)]

위의 코드는 매우 긴 반면, 대부분의 코드는 개발자에 게 전송 된 전자 메일에 표시 되는 HTML을 만듭니다. 이 코드는 `GetLastError` 메서드 (`lastErrorWrapper`)에서 반환 된 `HttpException`를 참조 하 여 시작 합니다. 요청에 의해 발생 한 실제 예외는 `lastErrorWrapper.InnerException`를 통해 검색 되며 변수 `lastError`에 할당 됩니다. 형식, 메시지 및 스택 추적 정보는 `lastError`에서 검색 되 고 세 개의 문자열 변수에 저장 됩니다.

그런 다음 `mm` 이라는 `MailMessage` 개체가 만들어집니다. 전자 메일 본문은 HTML 형식으로 표시 되며 요청 된 페이지의 URL, 현재 로그온 한 사용자의 이름 및 예외에 대 한 정보 (유형, 메시지 및 스택 추적)에 대 한 정보를 표시 합니다. `HttpException` 클래스에 대 한 유용한 정보 중 하나는 [GetHtmlErrorMessage 메서드](https://msdn.microsoft.com/library/system.web.httpexception.gethtmlerrormessage.aspx)를 호출 하 여 예외 정보 노랑 화면 죽음 (Ysod 화면을 만드는 데 사용 되는 HTML을 생성할 수 있다는 것입니다. 이 메서드는 예외 세부 정보 태그를 검색 하 고 첨부 파일로 전자 메일에 추가 하는 데 사용 됩니다. 한 가지 단어: `Error` 이벤트를 트리거한 예외가 HTTP 기반 예외 (예: 존재 하지 않는 페이지에 대 한 요청) 인 경우 `GetHtmlErrorMessage` 메서드는 `null`를 반환 합니다.

마지막 단계는 `MailMessage`를 보내는 것입니다. 이 작업을 수행 하려면 새 `SmtpClient` 메서드를 만들고 해당 `Send` 메서드를 호출 합니다.

> [!NOTE]
> 웹 응용 프로그램에서이 코드를 사용 하기 전에 `ToAddress` 값을 변경 하 고 상수를 support@example.com에서 오류 알림 전자 메일을 보내고 받아야 하는 전자 메일 주소로 `FromAddress` 합니다. 또한 `Web.config`의 `<system.net>` 섹션에서 SMTP 서버 설정을 지정 해야 합니다. 사용할 SMTP 서버 설정을 확인 하려면 웹 호스트 공급자에 게 문의 하십시오.

이 코드를 사용 하면 오류가 발생 하는 경우 개발자에 게 오류를 요약 하 고 YSOD을 포함 하는 전자 메일 메시지가 전송 됩니다. 앞의 자습서에서는 장르를 방문 하 고 `Genre.aspx?ID=foo`와 같이 querystring을 통해 잘못 된 `ID` 값을 전달 하 여 런타임 오류를 살펴보았습니다. `Global.asax` 파일을 사용 하 여 페이지를 방문 하면 이전 자습서와 동일한 사용자 환경이 생성 됩니다. 개발 환경에서 예외 정보 노란색 화면이 계속 표시 되는 반면, 프로덕션 환경에서는 사용자 지정 오류 페이지가 표시 됩니다. 이 기존 동작 외에도 개발자는 전자 메일을 받게 됩니다.

**그림 2** 에서는 `Genre.aspx?ID=foo`을 방문할 때 받은 전자 메일을 보여 줍니다. 전자 메일 본문은 예외 정보를 요약 하는 반면 `YSOD.htm` 첨부 파일에는 예외 정보 ( **그림 3**참조)에 표시 된 콘텐츠가 표시 됩니다.

[![](processing-unhandled-exceptions-cs/_static/image5.png)](processing-unhandled-exceptions-cs/_static/image4.png)

**그림 2**: 처리 되지 않은 예외가 있을 때마다 개발자에 게 전자 메일 알림이 전송 됨  
([전체 크기 이미지를 보려면 클릭](processing-unhandled-exceptions-cs/_static/image6.png))

[![](processing-unhandled-exceptions-cs/_static/image8.png)](processing-unhandled-exceptions-cs/_static/image7.png)

**그림 3**: 전자 메일 알림을 첨부 파일로 포함 하는 예외 정보  
([전체 크기 이미지를 보려면 클릭](processing-unhandled-exceptions-cs/_static/image9.png))

## <a name="what-about-using-the-custom-error-page"></a>사용자 지정 오류 페이지를 사용 하는 방법

이 자습서에서는 `Global.asax` 및 `Application_Error` 이벤트 처리기를 사용 하 여 처리 되지 않은 예외가 발생할 때 코드를 실행 하는 방법을 보여 주었습니다. 특히이 이벤트 처리기를 사용 하 여 개발자에 게 오류를 알립니다. 또한 데이터베이스에서 오류 세부 정보를 기록 하도록 확장할 수 있습니다. `Application_Error` 이벤트 처리기가 있으면 최종 사용자 환경에 영향을 주지 않습니다. 구성 된 오류 페이지가 계속 표시 됩니다. 오류 세부 정보, 런타임 오류 또는 사용자 지정 오류 페이지가 표시 됩니다.

사용자 지정 오류 페이지를 사용 하는 경우 `Global.asax` 파일 및 `Application_Error` 이벤트가 필요한 지 여부를 궁금해 합니다. 오류가 발생 하는 경우 사용자는 사용자 지정 오류 페이지가 표시 되므로 개발자에 게 알리는 코드를 추가 하 고 사용자 지정 오류 페이지의 코드 숨김으로 오류 정보를 기록 하는 이유는 무엇 인가요? 사용자 지정 오류 페이지의 코드 숨김이 클래스에 코드를 추가할 수 있지만 앞의 자습서에서 살펴본 기술을 사용할 때 `Error` 이벤트를 트리거한 예외의 세부 정보에 액세스할 수 없습니다. 사용자 지정 오류 페이지에서 `GetLastError` 메서드를 호출 하면 `Nothing`반환 됩니다.

이 동작은 사용자 지정 오류 페이지에 리디렉션을 통해 도달 하기 때문에 발생 합니다. 처리 되지 않은 예외가 ASP.NET 런타임에 도달 하면 ASP.NET 엔진은 `Application_Error` 이벤트 처리기를 실행 하는 `Error` 이벤트를 발생 시킨 다음 `Response.Redirect(customErrorPageUrl)`를 실행 하 여 사용자를 사용자 지정 오류 페이지로 *리디렉션합니다* . `Response.Redirect` 메서드는 HTTP 302 상태 코드를 사용 하 여 클라이언트에 응답을 보내고 브라우저가 새 URL, 즉 사용자 지정 오류 페이지를 요청 하도록 지시 합니다. 그러면 브라우저에서 자동으로이 새 페이지를 요청 합니다. 브라우저의 주소 표시줄이 사용자 지정 오류 페이지 URL로 변경 되기 때문에 오류가 발생 한 페이지와 별도로 사용자 지정 오류 페이지가 요청 되었음을 알 수 있습니다 ( **그림 4**참조).

[![](processing-unhandled-exceptions-cs/_static/image11.png)](processing-unhandled-exceptions-cs/_static/image10.png)

**그림 4**: 오류가 발생 하면 브라우저가 사용자 지정 오류 페이지 URL로 리디렉션됩니다.  
([전체 크기 이미지를 보려면 클릭](processing-unhandled-exceptions-cs/_static/image12.png))

결과적으로 서버에서 HTTP 302 리디렉션을 사용 하 여 응답할 때 처리 되지 않은 예외가 발생 한 요청이 종료 됩니다. 사용자 지정 오류 페이지에 대 한 후속 요청은 새 요청입니다. 이 시점에서 ASP.NET 엔진은 오류 정보를 삭제 하 고, 더욱이 이전 요청에서 처리 되지 않은 예외를 사용자 지정 오류 페이지에 대 한 새 요청과 연결할 수 없습니다. 이것은 `GetLastError` 사용자 지정 오류 페이지에서 호출 될 때 `null`를 반환 하는 이유입니다.

그러나 오류가 발생 한 동일한 요청 중에 사용자 지정 오류 페이지가 실행 될 수도 있습니다. [`Server.Transfer(url)`](https://msdn.microsoft.com/library/system.web.httpserverutility.transfer.aspx) 메서드는 지정 된 URL에 실행을 전송 하 고 동일한 요청 내에서이를 처리 합니다. `Application_Error` 이벤트 처리기의 코드를 사용자 지정 오류 페이지의 코드 숨김이 클래스로 이동 하 여 `Global.asax`에서 다음 코드로 바꿀 수 있습니다.

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample5.cs)]

이제 처리 되지 않은 예외가 발생 하면 `Application_Error` 이벤트 처리기가 HTTP 상태 코드를 기반으로 적절 한 사용자 지정 오류 페이지로 제어를 전송 합니다. 제어가 전송 되었으므로 사용자 지정 오류 페이지는 `Server.GetLastError` 통해 처리 되지 않은 예외 정보에 액세스할 수 있으며 개발자에 게 오류를 알리고 세부 정보를 기록할 수 있습니다. `Server.Transfer` 호출은 ASP.NET 엔진이 사용자를 사용자 지정 오류 페이지로 리디렉션하는 것을 중지 합니다. 대신 사용자 지정 오류 페이지의 내용이 오류를 생성 한 페이지에 대 한 응답으로 반환 됩니다.

## <a name="summary"></a>요약

ASP.NET 웹 응용 프로그램에서 처리 되지 않은 예외가 발생 하면 ASP.NET 런타임은 `Error` 이벤트를 발생 시키고 구성 된 오류 페이지를 표시 합니다. 오류 이벤트에 대 한 이벤트 처리기를 만들어 오류를 개발자에 게 알리거나 세부 정보를 기록 하거나 다른 방식으로 처리할 수 있습니다. `Error`와 같은 `HttpApplication` 이벤트에 대 한 이벤트 처리기를 만드는 방법에는 `Global.asax` 파일이 나 HTTP 모듈 등 두 가지가 있습니다. 이 자습서에서는 전자 메일 메시지를 통해 개발자에 게 오류를 알리는 `Global.asax` 파일에 `Error` 이벤트 처리기를 만드는 방법을 살펴보았습니다.

처리 되지 않은 예외를 고유 하거나 사용자 지정 된 방식으로 처리 해야 하는 경우 `Error` 이벤트 처리기를 만드는 것이 유용 합니다. 그러나 사용자 고유의 `Error` 이벤트 처리기를 만들어 예외를 기록 하거나 개발자에 게 알리기 위해 사용자의 시간을 가장 효율적으로 사용 하지 않는 것이 가장 효율적입니다. 다음 두 자습서에서는 이러한 두 라이브러리를 검사 합니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET HTTP 모듈 및 HTTP 처리기 개요](https://support.microsoft.com/kb/307985)
- [처리 되지 않은 예외에 대 한 적절 한 응답-처리 되지 않은 예외 처리](http://aspnet.4guysfromrolla.com/articles/091306-1.aspx)
- [`HttpApplication` 클래스 및 ASP.NET 응용 프로그램 개체](http://www.eggheadcafe.com/articles/20030211.asp)
- [ASP.NET의 HTTP 처리기 및 HTTP 모듈](http://www.15seconds.com/Issue/020417.htm)
- [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`Global.asax` 파일 이해](http://aspalliance.com/1114_Understanding_the_Globalasax_file.all)
- [HTTP 모듈 및 처리기를 사용 하 여 플러그형 ASP.NET 구성 요소 만들기](https://msdn.microsoft.com/library/aa479332.aspx)
- [ASP.NET `Global.asax` 파일 사용](http://articles.techrepublic.com.com/5100-10878_11-5771721.html)
- [`HttpApplication` 인스턴스 작업](https://msdn.microsoft.com/library/a0xez8f2.aspx)

> [!div class="step-by-step"]
> [이전](displaying-a-custom-error-page-cs.md)
> [다음](logging-error-details-with-asp-net-health-monitoring-cs.md)
