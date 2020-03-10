---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: CAPTCHA를 사용 하 여 봇에서 ASP.NET 웹 Razor 사용 방지 Microsoft Docs
author: microsoft
description: 이 문서에서는 ReCaptcha (보안 측정값)를 사용 하 여 자동 프로그램 (봇)이 ASP.NET 웹 페이지 (Razor)에서 작업을 수행 하지 못하도록 방지 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440195"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>CAPTCHA를 사용 하 여 봇에서 ASP.NET 웹 Razor를 사용 하지 못하도록 방지) 사이트

[Microsoft](https://github.com/microsoft) 에서

> 이 문서에서는 ReCaptcha (보안 측정값)를 사용 하 여 자동 프로그램 (봇)이 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 작업을 수행 하는 것을 방지 하는 방법을 설명 합니다.
> 
> **학습 내용:** 
> 
> - CAPTCHA 테스트를 사이트에 추가 하는 방법
> 
> 다음은이 문서에 도입 된 ASP.NET 기능입니다.
> 
> - `ReCaptcha` 도우미입니다.
> 
> > [!NOTE]
> > 이 문서의 정보는 ASP.NET 웹 페이지 1.0 및 웹 페이지 2에 적용 됩니다.

## <a name="about-captchas"></a>CAPTCHAs 정보

사용자가 사이트에 등록 하도록 하거나 이름 및 URL (예: 블로그 설명)을 입력 하는 경우에도 가짜 이름이 다를 수 있습니다. 이러한 기능은 일반적으로 찾을 수 있는 모든 웹 사이트에서 Url을 유지 하는 자동 프로그램 (봇)으로 남아 있습니다. (일반적으로 판매 하는 제품의 Url을 게시 하는 것이 일반적입니다.)

*CAPTCHA* 를 사용 하 여 사용자가 등록 하거나 사용자의 이름과 사이트를 입력 하는 경우 사용자의 유효성을 검사 하 여 사용자가 실제 사용자 인지 확인 하는 데 도움이 될 수 있습니다. CAPTCHA는 완전히 자동화 된 공용 Turing 테스트를 통해 컴퓨터와 사람을 구분 합니다. CAPTCHA는 사용자가 자동화 된 프로그램의 작업을 수행 하는 데 필요한 작업을 수행 하는 데 필요한 작업을 수행 하는 데 필요한 작업을 사용자에 게 요청 하는 *챌린지-응답* 테스트입니다. 가장 일반적인 유형의 CAPTCHA은 일부 왜곡 된 문자를 표시 하 고 입력 하 라는 메시지를 표시 합니다. 왜곡은 봇에서 문자를 해독할 수 있도록 하기 위한 것입니다.

## <a name="adding-a-recaptcha-test"></a>ReCaptcha 테스트 추가

ASP.NET 페이지에서 `ReCaptcha` 도우미를 사용 하 여 ReCaptcha 서비스 ([http://recaptcha.net](http://recaptcha.net))를 기반으로 하는 CAPTCHA 테스트를 렌더링할 수 있습니다. `ReCaptcha` 도우미는 페이지의 유효성을 검사 하기 전에 사용자가 올바르게 입력 해야 하는 두 개의 왜곡 된 단어로 이루어진 이미지를 표시 합니다. ReCaptcha.Net 서비스에서 사용자 응답의 유효성을 검사 합니다.

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net))에서 웹 사이트를 등록 합니다. 등록을 완료 하면 공개 키와 개인 키를 얻게 됩니다.
2. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).
3. *\_AppStart* 파일이 아직 없는 경우 웹 사이트의 루트 폴더에서 *AppStart\_* 라는 파일을 만듭니다.
4. 다음 `Recaptcha` 도우미 설정을 *\_AppStart* 파일에 추가 합니다. 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. 사용자 고유의 공개 키와 개인 키를 사용 하 여 `PublicKey` 및 `PrivateKey` 속성을 설정 합니다.
6. *\_AppStart* 파일을 저장 하 고 닫습니다.
7. 웹 사이트의 루트 폴더에서 *Recaptcha*라는 새 페이지를 만듭니다.
8. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. 브라우저에서 *Recaptcha* 페이지를 실행 합니다. `PrivateKey` 값이 유효 하면 페이지에 ReCaptcha 컨트롤과 단추가 표시 됩니다. *\_AppStart*에서 전역으로 키를 설정 하지 않은 경우 페이지에 오류가 표시 됩니다. 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. 테스트에 사용할 단어를 입력 합니다. ReCaptcha 테스트를 전달 하면 해당 효과에 대 한 메시지가 표시 됩니다. 그렇지 않으면 오류 메시지가 표시 되 고 ReCaptcha 컨트롤이 다시 표시 됩니다.

> [!NOTE]
> 컴퓨터가 프록시 서버를 사용 하는 도메인에 있는 경우 *web.config 파일의* `defaultproxy` 요소를 구성 해야 할 수 있습니다. 다음 예제에서는 ReCaptcha 서비스가 작동 하도록 구성 된 `defaultproxy` 요소가 *포함 된 web.config 파일을* 보여 줍니다.
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [ASP.NET 웹 페이지 사이트에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ReCaptcha 사이트](https://www.google.com/recaptcha)
