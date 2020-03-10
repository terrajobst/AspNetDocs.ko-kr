---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 열린 리디렉션 공격 방지 (C#) | Microsoft Docs
author: jongalloway
description: 이 자습서에서는 ASP.NET MVC 응용 프로그램에서 open 리디렉션 공격을 방지 하는 방법을 설명 합니다. 이 자습서에서는 적용 된 변경 내용을 설명 합니다.
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: cfa635d4fd14d031993c5b452325cbe334f82dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432587"
---
# <a name="preventing-open-redirection-attacks-c"></a>오픈 리디렉션 공격 방지(C#)

받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )

> 이 자습서에서는 ASP.NET MVC 응용 프로그램에서 open 리디렉션 공격을 방지 하는 방법을 설명 합니다. 이 자습서에서는 ASP.NET MVC 3에서 AccountController에 적용 된 변경 내용에 대해 설명 하 고 기존 ASP.NET MVC 1.0 및 2 응용 프로그램에서 이러한 변경 사항을 적용 하는 방법을 보여 줍니다.

## <a name="what-is-an-open-redirection-attack"></a>개방형 리디렉션 공격 이란?

Querystring 또는 양식 데이터와 같은 요청을 통해 지정 된 URL로 리디렉션하는 모든 웹 응용 프로그램은 사용자를 안전 하 고 악의적인 URL로 리디렉션하는 변조 될 수 있습니다. 이러한 변조를 개방 리디렉션 공격 이라고 합니다.

응용 프로그램 논리가 지정 된 URL로 리디렉션되는 경우 항상 리디렉션 URL이 변조 되지 않았는지 확인 해야 합니다. ASP.NET MVC 1.0 및 ASP.NET MVC 2에 대 한 기본 AccountController에서 사용 되는 로그인은 오픈 리디렉션 공격에 취약 합니다. 다행히 기존 응용 프로그램을 업데이트 하 여 ASP.NET MVC 3 Preview의 수정을 사용할 수 있습니다.

취약성을 이해 하려면 기본 ASP.NET MVC 2 웹 응용 프로그램 프로젝트에서 로그인 리디렉션이 작동 하는 방식을 살펴보겠습니다. 이 응용 프로그램에서 [권한 부여] 특성이 있는 컨트롤러 작업을 방문 하려고 하면 권한이 없는 사용자가/svrvview 보기로 리디렉션됩니다. ReturnUrl에 대 한이 리디렉션에는 사용자가 성공적으로 로그인 한 후 원래 요청 된 URL로 반환 될 수 있도록 querystring 매개 변수가 포함 됩니다.

아래 스크린샷에서는 로그인 하지 않을 때/Cv/ps 뷰에 대 한 액세스 시도가 실패 하는 것을 볼 수 있습니다. ReturnUrl =% 2fAccount% 2fChangePassword% 2f.

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

**그림 01**: 열린 리디렉션이 있는 로그인 페이지

ReturnUrl querystring 매개 변수의 유효성이 검사 되지 않으므로 공격자는 URL 주소를 매개 변수에 삽입 하도록 수정 하 여 열린 리디렉션 공격을 수행할 수 있습니다. 이를 보여 주기 위해 ReturnUrl 매개 변수를 [http://bing.com](http://bing.com)로 수정 하 여 결과 로그인 URL은/Account/LogOn 입니까? ReturnUrl =<http://www.bing.com/>. 사이트에 성공적으로 로그인 하면 [http://bing.com](http://bing.com)으로 리디렉션됩니다. 이 리디렉션의 유효성은 검사 되지 않으므로 사용자를 속이는 악의적인 사이트를 가리키도록 할 수 있습니다.

### <a name="a-more-complex-open-redirection-attack"></a>더 복잡 한 개방형 리디렉션 공격

공격자는 특정 웹 사이트에 로그인을 시도 하 고 있으며이로 인해 [피싱 공격](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)에 취약 하다는 것을 알고 있기 때문에 열린 리디렉션 공격은 특히 위험 합니다. 예를 들어 공격자는 암호 캡처를 시도 하 여 악의적인 전자 메일을 웹 사이트 사용자에 게 보낼 수 있습니다. 이 작업을 수행 하는 방법을 살펴보겠습니다. (오픈 리디렉션 공격 으로부터 보호 하도록 라이브 된 Ddddinner 사이트를 업데이트 했습니다.)

먼저 공격자는 위조 된 페이지로의 리디렉션을 포함 하는 회사 간 Ddinner의 로그인 페이지에 대 한 링크를 전송 합니다.

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

반환 URL은 dinner 이라는 단어에서 "n"이 누락 된 nerddiner.com를 가리킵니다. 이 예제에서는 공격자가 제어 하는 도메인입니다. 위의 링크에 액세스할 때 합법적인 NerdDinner.com 로그인 페이지로 이동 합니다.

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

**그림 02**: 열린 리디렉션이 있는 동료의 내부 로그인 페이지

올바르게 로그인 하면 ASP.NET MVC AccountController의 LogOn 동작이 returnUrl querystring 매개 변수에 지정 된 URL로 리디렉션됩니다. 이 경우 공격자가 입력 한 URL 이며 [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn)입니다. 매우 watchful 않는 한이는 특히 공격자가 위조 된 페이지가 합법적인 로그인 페이지와 정확히 일치 하는지 확인 하는 데 주의를 기울여야 했기 때문입니다. 이 로그인 페이지에는 다시 로그인을 요청 하는 오류 메시지가 포함 되어 있습니다. 미국 괴로운 암호를 잘못 입력 해야 합니다.

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

**그림 03**: 위조 되는 내부 로그인 화면

사용자 이름 및 암호를 다시 입력 하면 위조 된 로그인 페이지가 정보를 저장 하 고 합법적인 NerdDinner.com 사이트로 다시 전송 합니다. 이 시점에서 NerdDinner.com 사이트는 이미 인증 되었으므로 위조 된 로그인 페이지가 해당 페이지로 직접 리디렉션할 수 있습니다. 최종 결과는 공격자에 게 사용자 이름과 암호가 있으며 사용자에 게 제공 된 것을 인식 하지 못하는 것입니다.

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a>AccountController 로그온 작업에서 취약 한 코드 확인

ASP.NET MVC 2 응용 프로그램의 LogOn 동작에 대 한 코드는 다음과 같습니다. 성공적으로 로그인 되 면 컨트롤러는 returnUrl에 대 한 리디렉션을 반환 합니다. ReturnUrl 매개 변수에 대해 유효성 검사가 수행 되지 않는 것을 볼 수 있습니다.

**목록 1 – ASP.NET MVC 2 로그온 작업 `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

이제 ASP.NET MVC 3 로그온 동작에 대 한 변경 내용을 살펴보겠습니다. 이 코드는 `IsLocalUrl()`이라는 returnUrl 도우미 클래스에서 새 메서드를 호출 하 여 매개 변수의 유효성을 검사 하도록 변경 되었습니다.

**목록 2 – ASP.NET MVC 3 LogOn 작업 `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

이는 system.string 도우미 클래스에서 새 메서드를 호출 하 여 반환 URL 매개 변수의 유효성을 검사 하도록 변경 되었습니다 `IsLocalUrl()`.

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a>ASP.NET MVC 1.0 및 MVC 2 응용 프로그램 보호

IsLocalUrl () 도우미 메서드를 추가 하 고 returnUrl 매개 변수의 유효성을 검사 하기 위해 LogOn 작업을 업데이트 하 여 기존 ASP.NET MVC 1.0 및 2 응용 프로그램의 ASP.NET MVC 3 변경 내용을 활용할 수 있습니다.

UrlHelper IsLocalUrl () 메서드는 실제로 System.web. 웹 페이지에서 메서드를 호출 하는 것입니다 .이 유효성 검사는 ASP.NET 웹 페이지 응용 프로그램 에서도 사용 됩니다.

**목록 3 – ASP.NET MVC 3 UrlHelper의 IsLocalUrl () 메서드 `class`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

IsUrlLocalToHost 메서드는 4 목록에 표시 된 것 처럼 실제 유효성 검사 논리를 포함 합니다.

**목록 4 – IsUrlLocalToHost () 메서드를 System.web. 웹 페이지 RequestExtensions 클래스에서**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

ASP.NET MVC 1.0 또는 2 응용 프로그램에서는 IsLocalUrl () 메서드를 AccountController에 추가 하지만 가능한 경우 별도의 도우미 클래스에 추가 하는 것이 좋습니다. ASP.NET MVC 3 버전의 IsLocalUrl ()을 두 번 변경 하 여 AccountController 내에서 작동 하도록 합니다. 먼저 컨트롤러의 공용 메서드를 컨트롤러 작업으로 액세스할 수 있기 때문에 공용 메서드에서 private 메서드로 변경 합니다. 둘째, 응용 프로그램 호스트에 대해 URL 호스트를 확인 하는 호출을 수정 합니다. 이 호출은 UrlHelper 클래스에서 로컬 RequestContext 필드를 사용 합니다. 대신 사용 합니다. RequestContext. i n. i n. i n. . Url. 호스트. 다음 코드에서는 ASP.NET MVC 1.0 및 2 응용 프로그램에서 컨트롤러 클래스와 함께 사용 하기 위해 수정 된 IsLocalUrl () 메서드를 보여 줍니다.

**목록 5 – IsLocalUrl () 메서드 (MVC 컨트롤러 클래스에서 사용 하도록 수정 됨)**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

이제 IsLocalUrl () 메서드가 준비 되었으므로 다음 코드와 같이 LogOn 작업에서 호출 하 여 returnUrl 매개 변수의 유효성을 검사할 수 있습니다.

**목록 6 – returnUrl 매개 변수의 유효성을 검사 하는 업데이트 된 로그온 방법**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

이제 외부 반환 URL을 사용 하 여 로그인을 시도 하 여 열린 리디렉션 공격을 테스트할 수 있습니다. /Ss/LogOn을 사용 하겠습니다. ReturnUrl =<http://www.bing.com/>.

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

**그림 04**: 업데이트 된 로그온 작업 테스트

성공적으로 로그인 한 후에는 외부 URL이 아닌 Home/Index 컨트롤러 작업으로 리디렉션됩니다.

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

**그림 05**: 오픈 리디렉션 공격 패배

## <a name="summary"></a>요약

리디렉션 Url이 응용 프로그램에 대 한 URL에 매개 변수로 전달 되는 경우에는 열기 리디렉션 공격이 발생할 수 있습니다. ASP.NET MVC 3 템플릿에는 개방형 리디렉션 공격 으로부터 보호 하는 코드가 포함 되어 있습니다. ASP.NET MVC 1.0 및 2 응용 프로그램을 수정 하 여이 코드를 추가할 수 있습니다. ASP.NET 1.0 및 2 개 응용 프로그램에 로그인 할 때 개방 리디렉션 공격 으로부터 보호 하려면 IsLocalUrl () 메서드를 추가 하 고 LogOn 작업에서 returnUrl 매개 변수의 유효성을 검사 합니다.
