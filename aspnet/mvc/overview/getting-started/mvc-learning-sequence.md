---
uid: mvc/overview/getting-started/mvc-learning-sequence
title: MVC 권장 자습서 및 문서 | Microsoft Docs
author: Rick-Anderson
description: 이 페이지에는 ASP.NET MVC 자습서에 대 한 링크와 이러한 자습서를 따르는 제안 된 시퀀스가 포함 되어 있습니다.
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 8513a57a-2d45-4d6b-881c-15a01c5cbb1c
msc.legacyurl: /mvc/overview/getting-started/mvc-learning-sequence
msc.type: authoredcontent
ms.openlocfilehash: 46b089a896c6b1b92437ff1f5488214a3a0a9838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487739"
---
# <a name="mvc-recommended-tutorials-and-articles"></a>MVC 권장 자습서 및 문서

[Rick Anderson](https://twitter.com/RickAndMSFT)

<a id="pwd"></a>
## <a name="getting-started"></a>시작하기

- [ASP.NET MVC 5 시작](introduction/getting-started.md) 이 11 부 시리즈는 시작 하기에 적합 합니다.
- [Pluralsight ASP.NET MVC 5 기본 사항](https://pluralsight.com/training/Player?author=scott-allen&amp;name=aspdotnet-mvc5-fundamentals-m1-introduction&amp;mode=live&amp;clip=0&amp;course=aspdotnet-mvc5-fundamentals) (비디오 과정)
- [ASP.NET MVC](https://channel9.msdn.com/Series/Introduction-to-ASP-NET-MVC) By Jon Galloway 및 Christopher Harrison 소개
- [ASP.NET MVC 5 응용 프로그램의 수명 주기](lifecycle-of-an-aspnet-mvc-5-application.md) ASP.NET MVC 5 앱의 수명 주기를 차트로 나타내는 PDF 문서입니다.

<a id="con"></a>
## <a name="working-with-data"></a>데이터 작업

- [MVC 5를 사용 하 여 EF 6 Code First 시작](getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Tom Dykstra의 수상 다이브가 EF에 깊이 있습니다.

<a id="wj"></a>
## <a name="security"></a>보안

- [Auth 및 SQL DB를 사용 하 여 ASP.NET MVC 앱을 만들고 Azure에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) 이 인기 있는 자습서에서는 간단한 앱을 만들고 멤버 자격 및 역할을 추가 하는 과정을 안내 합니다.
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서에서는 사용자가 Facebook, Twitter, LinkedIn, Microsoft, Google 등의 외부 인증 공급자에서 제공 하는 자격 증명으로 OAuth 2.0를 사용 하 여 로그인 할 수 있도록 하는 ASP.NET MVC 5 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다.
- [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) Id의 시리즈에서 첫 번째는 [확인 링크](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md#rsend)를 다시 보내는 코드를 포함 합니다.
- [SMS 및 전자 메일 2 단계 인증을 사용 하는 ASP.NET MVC 5 앱](../security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) Identity 시리즈의 두 번째입니다.
- [ASP.NET 및 Azure App Service에 암호와 기타 중요한 데이터를 배포하는 방법에 대한 모범 사례](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)
- ASP.NET Identity `isPersistent` 및 보안 쿠키를 [사용 하는 SMS 및 전자 메일을 사용 하는 2 단계 인증](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) , 사용자가 로그온 하기 전에 유효성이 검사 된 전자 메일 계정을 갖도록 요구 하는 코드, SignInManager에서 2fa 요구 사항을 확인 하는 방법 등이 있습니다.
- [계정 확인 및 암호 복구 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 사용자가 잊어버린 암호를 다시 설정 하도록 허용 하는 방법 등 [로그인을 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기, 전자 메일 확인 및 암호 재설정](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) 에서 찾을 수 없는 id에 대 한 세부 정보를 제공 합니다.

<a id="da"></a>
## <a name="azure"></a>Azure

- [Azure에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/) Azure에 배포 하는 방법에 대 한 간단한 자습서입니다.
- [Auth 및 SQL DB를 사용 하 여 ASP.NET MVC 앱을 만들고 Azure에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)

<a id="perf"></a>
## <a name="performance-and-debugging"></a>성능 및 디버깅

- [Glimpse를 사용하여 ASP.NET MVC 앱 프로파일링 및 디버깅](../performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse.md)
