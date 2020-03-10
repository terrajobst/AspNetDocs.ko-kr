---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: ASP.NET Identity-ASP.NET 4.x의 사용자에 대 한 기본 키를 변경 합니다.
author: Rick-Anderson
description: Visual Studio 2013에서 기본 웹 응용 프로그램은 사용자 계정에 대 한 키에 문자열 값을 사용 합니다. ASP.NET Identity를 사용 하 여의 형식을 변경할 수 있습니다.
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472265"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a>ASP.NET Identity에서 사용자의 기본 키 변경

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> Visual Studio 2013에서 기본 웹 응용 프로그램은 사용자 계정에 대 한 키에 문자열 값을 사용 합니다. ASP.NET Identity를 사용 하 여 데이터 요구 사항에 맞게 키 유형을 변경할 수 있습니다. 예를 들어 키의 형식을 문자열에서 정수로 변경할 수 있습니다.
> 
> 이 항목에서는 기본 웹 응용 프로그램으로 시작 하 고 사용자 계정 키를 정수로 변경 하는 방법을 보여 줍니다. 동일한 수정 작업을 사용 하 여 프로젝트에서 모든 형식의 키를 구현할 수 있습니다. 기본 웹 응용 프로그램에서 이러한 변경을 수행 하는 방법을 보여 주지만, 사용자 지정 된 응용 프로그램에 비슷한 수정을 적용할 수 있습니다. MVC 또는 Web Forms 작업할 때 필요한 변경 내용을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - 업데이트 2 이상 Visual Studio 2013
> - ASP.NET Identity 2.1 이상

이 자습서의 단계를 수행 하려면 Visual Studio 2013 업데이트 2 이상 및 ASP.NET 웹 응용 프로그램 템플릿에서 만든 웹 응용 프로그램이 있어야 합니다. 템플릿은 업데이트 3에서 변경 되었습니다. 이 항목에서는 업데이트 2 및 업데이트 3에서 템플릿을 변경 하는 방법을 보여 줍니다.

이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

- [Id 사용자 클래스에서 키의 형식 변경](#userclass)
- [키 유형을 사용 하는 사용자 지정 Id 클래스 추가](#customclass)
- [컨텍스트 클래스 및 사용자 관리자를 변경 하 여 키 유형 사용](#context)
- [키 유형을 사용 하도록 시작 구성 변경](#startup)
- [MVC 업데이트 2의 경우 키 유형을 전달 하도록 AccountController를 변경 합니다.](#mvcupdate2)
- [MVC 업데이트 3의 경우 키 유형을 전달 하도록 AccountController 및 ManageController를 변경 합니다.](#mvcupdate3)
- [업데이트 2를 사용 하는 Web Forms의 경우 키 유형을 전달 하도록 계정 페이지를 변경 합니다.](#webformsupdate2)
- [업데이트 3의 Web Forms에 대해 키 유형을 전달 하도록 계정 페이지를 변경 합니다.](#webformsupdate3)
- [응용 프로그램 실행](#run)
- [기타 참고 자료](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a>Id 사용자 클래스에서 키의 형식 변경

ASP.NET 웹 응용 프로그램 템플릿에서 만든 프로젝트에서 ApplicationUser 클래스가 사용자 계정에 대 한 키에 정수를 사용 하도록 지정 합니다. IdentityModels.cs에서 TKey 제네릭 매개 변수에 대 한 **int** 유형이 있는 IdentityUser에서 상속 하도록 applicationuser 클래스를 변경 합니다. 또한 아직 구현 하지 않은 사용자 지정 클래스의 이름을 전달 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

키의 형식을 변경 했지만 기본적으로 응용 프로그램의 나머지 부분에서는 키가 문자열인 것으로 가정 합니다. 문자열을 가정 하는 코드에서 키의 형식을 명시적으로 지정 해야 합니다.

**Applicationuser** 클래스에서 아래 강조 표시 된 코드에 표시 된 대로 int를 포함 하도록 **GenerateUserIdentityAsync** 메서드를 변경 합니다. 업데이트 3 템플릿을 포함 하는 Web Forms 프로젝트의 경우에는 이러한 변경이 필요 하지 않습니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a>키 유형을 사용 하는 사용자 지정 Id 클래스 추가

다른 Id 클래스 (예: IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore)는 여전히 문자열 키를 사용 하도록 설정 되어 있습니다. 키의 정수를 지정 하는 이러한 클래스의 새 버전을 만듭니다. 이러한 클래스에서 많은 구현 코드를 제공할 필요는 없으며 주로 int를 키로 설정 하기만 하면 됩니다.

IdentityModels.cs 파일에 다음 클래스를 추가 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a>컨텍스트 클래스 및 사용자 관리자를 변경 하 여 키 유형 사용

IdentityModels.cs에서 **ApplicationDbContext** 클래스의 정의를 변경 하 여 강조 표시 된 코드에 표시 된 대로 새로운 사용자 지정 클래스와 키에 대 한 **int** 를 사용 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

ThrowIfV1Schema 매개 변수는 더 이상 생성자에서 유효 하지 않습니다. ThrowIfV1Schema 값을 전달 하지 않도록 생성자를 변경 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

IdentityConfig.cs를 열고 새 사용자 저장소 클래스를 사용 하 여 데이터를 유지 하 고 키에 대해 **int** 를 사용 하도록 **applicationusermanger** 클래스를 변경 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

업데이트 3 템플릿에서 ApplicationSignInManager 클래스를 변경 해야 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a>키 유형을 사용 하도록 시작 구성 변경

Startup.Auth.cs에서 아래 강조 표시 된 것 처럼 OnValidateIdentity 코드를 바꿉니다. GetUserIdCallback 정의는 문자열 값을 정수로 구문 분석 합니다.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

프로젝트에서 **Getuserid** 메서드의 제네릭 구현을 인식 하지 못하는 경우 ASP.NET Identity NuGet 패키지를 버전 2.1으로 업데이트 해야 할 수 있습니다.

ASP.NET Identity에서 사용 하는 인프라 클래스를 많이 변경 했습니다. 프로젝트를 컴파일하는 경우 많은 오류가 발생 합니다. 다행히 나머지 오류는 모두 비슷합니다. Identity 클래스에는 키에 대 한 정수가 필요 하지만 컨트롤러 (또는 웹 폼)는 문자열 값을 전달 합니다. 각 경우에서 **Getuserid&lt;int&gt;** 를 호출 하 여 문자열에서로 변환 해야 합니다. 컴파일 중에 오류 목록에서 작업 하거나 아래 변경 사항을 따를 수 있습니다.

나머지 변경 내용은 만들고 있는 프로젝트의 형식 및 Visual Studio에 설치한 업데이트에 따라 달라 집니다. 다음 링크를 통해 관련 섹션으로 직접 이동할 수 있습니다.

- [MVC 업데이트 2의 경우 키 유형을 전달 하도록 AccountController를 변경 합니다.](#mvcupdate2)
- [MVC 업데이트 3의 경우 키 유형을 전달 하도록 AccountController 및 ManageController를 변경 합니다.](#mvcupdate3)
- [업데이트 2를 사용 하는 Web Forms의 경우 키 유형을 전달 하도록 계정 페이지를 변경 합니다.](#webformsupdate2)
- [업데이트 3의 Web Forms에 대해 키 유형을 전달 하도록 계정 페이지를 변경 합니다.](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a>MVC 업데이트 2의 경우 키 유형을 전달 하도록 AccountController를 변경 합니다.

AccountController.cs 파일을 엽니다. 다음 메서드를 변경 해야 합니다.

**ConfirmEmail** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

**메서드 분리**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

**Manage (ManageUserViewModel)** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

**LinkLoginCallback** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

**Removeaccountlist** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

**Haspassword** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

이제 [응용 프로그램을 실행](#run) 하 고 새 사용자를 등록할 수 있습니다.

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a>MVC 업데이트 3의 경우 키 유형을 전달 하도록 AccountController 및 ManageController를 변경 합니다.

AccountController.cs 파일을 엽니다. 다음 메서드를 변경 해야 합니다.

**ConfirmEmail** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

**Sendcode** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

ManageController.cs 파일을 엽니다. 다음 메서드를 변경 해야 합니다.

**Index** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

**Removelogin** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

**AddPhoneNumber** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

**EnableTwoFactorAuthentication** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

**DisableTwoFactorAuthentication** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

**VerifyPhoneNumber** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

**RemovePhoneNumber** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

**ChangePassword** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

**SetPassword** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

**ManageLogins** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

**LinkLoginCallback** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

**Haspassword** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

**HasPhoneNumber** 메서드

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

이제 [응용 프로그램을 실행](#run) 하 고 새 사용자를 등록할 수 있습니다.

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a>업데이트 2를 사용 하는 Web Forms의 경우 키 유형을 전달 하도록 계정 페이지를 변경 합니다.

업데이트 2에 Web Forms 다음 페이지를 변경 해야 합니다.

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

이제 [응용 프로그램을 실행](#run) 하 고 새 사용자를 등록할 수 있습니다.

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a>업데이트 3의 Web Forms에 대해 키 유형을 전달 하도록 계정 페이지를 변경 합니다.

업데이트 3의 Web Forms 경우 다음 페이지를 변경 해야 합니다.

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

**VerifyPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

**AddPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

**ManagePassword.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

**ManageLogins.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

**TwoFactorAuthenticationSignIn.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a>애플리케이션 실행

기본 웹 응용 프로그램 템플릿에 필요한 모든 변경을 완료 했습니다. 응용 프로그램을 실행 하 고 새 사용자를 등록 합니다. 사용자를 등록 한 후에는 AspNetUsers 테이블의 Id 열이 정수인 것을 알 수 있습니다.

![새 기본 키](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

이전에 다른 기본 키를 사용 하 여 ASP.NET Identity 테이블을 만든 경우 몇 가지 추가 변경 작업을 수행 해야 합니다. 가능 하면 기존 데이터베이스를 삭제 하면 됩니다. 웹 응용 프로그램을 실행 하 고 새 사용자를 추가할 때 올바른 디자인으로 데이터베이스를 다시 만듭니다. 삭제할 수 없는 경우 code first 마이그레이션을 실행 하 여 테이블을 변경 합니다. 그러나 새 정수 기본 키는 데이터베이스에서 SQL IDENTITY 속성으로 설정 되지 않습니다. Id 열을 id로 수동으로 설정 해야 합니다.

<a id="other"></a>
## <a name="other-resources"></a>기타 리소스

- [ASP.NET ID에 대한 사용자 지정 스토리지 공급자 개요](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [기존 웹 사이트를 SQL 멤버 자격에서 ASP.NET ID로 마이그레이션](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [멤버 자격 및 사용자 프로필에 대 한 유니버설 공급자 데이터를 ASP.NET Identity로 마이그레이션](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- 변경 된 기본 키가 있는 [샘플 응용 프로그램](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK)
