---
uid: identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
title: 멤버 자격 및 사용자 프로필에 대 한 유니버설 공급자 데이터를C#ASP.NET Identity ()-ASP.NET 4.x로 마이그레이션
author: rustd
description: 이 자습서에서는 기존 응용 프로그램의 Universal Providers을 사용 하 여 만든 사용자 및 역할 데이터와 사용자 프로필 데이터를 마이그레이션하는 데 필요한 단계를 설명 합니다.
ms.author: riande
ms.date: 12/13/2013
ms.custom: seoapril2019
ms.assetid: 2e260430-d13c-4658-bd05-e256fc0d63b8
msc.legacyurl: /identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 31f02a0cec3c531c45c37b7aad8456e01e80b5ea
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456116"
---
# <a name="migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity-c"></a>멤버 자격 및 사용자 프로필의 범용 공급자 데이터를 ASP.NET Identity로 마이그레이션(C#)

by [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Robert McMurray](https://github.com/rmcmurray), [suiJoshi](https://github.com/suhasj)

> 이 자습서에서는 기존 응용 프로그램의 Universal Providers 사용 하 여 만든 사용자 및 역할 데이터와 사용자 프로필 데이터를 ASP.NET Identity 모델로 마이그레이션하는 데 필요한 단계에 대해 설명 합니다. 여기에서 설명 하는 방법을 사용 하 여 사용자 프로필 데이터를 마이그레이션할 수도 있습니다.

Visual Studio 2013 릴리스에서는 ASP.NET 팀이 새로운 ASP.NET Identity 시스템을 도입 했으며, [여기](../../index.md)에서 해당 릴리스에 대 한 자세한 내용을 확인할 수 있습니다. [SQL 멤버 자격에서 새 id 시스템으로](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)웹 응용 프로그램을 마이그레이션하는 문서에 따라이 문서에서는 사용자 및 역할 관리를 위한 공급자 모델을 따르는 기존 응용 프로그램을 새 id 모델로 마이그레이션하는 단계를 설명 합니다. 이 자습서에서는 주로 사용자 프로필 데이터를 마이그레이션하여 새 시스템에 원활 하 게 후크 하는 방법에 중점을 둡니다. SQL 멤버 자격에 대 한 사용자 및 역할 정보 마이그레이션은 유사 합니다. 프로필 데이터 마이그레이션에 대 한 접근 방식은 SQL 멤버 자격을 포함 하는 응용 프로그램 에서도 사용할 수 있습니다.

예를 들어 공급자 모델을 사용 하는 Visual Studio 2012을 사용 하 여 만든 웹 앱으로 시작 합니다. 그런 다음 프로필 관리에 대 한 코드를 추가 하 고, 사용자를 등록 하 고, 사용자에 대 한 프로필 데이터를 추가 하 고, 데이터베이스 스키마를 마이그레이션하고, 사용자 및 역할 관리를 위해 Id 시스템을 사용 하도록 응용 프로그램을 변경 합니다. 마이그레이션을 테스트 하면 Universal Providers를 사용 하 여 만든 사용자가 로그인 할 수 있어야 하 고 새 사용자가 등록할 수 있어야 합니다.

> [!NOTE]
> [https://github.com/suhasj/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations)에서 전체 샘플을 찾을 수 있습니다.

## <a name="profile-data-migration-summary"></a>프로필 데이터 마이그레이션 요약

마이그레이션을 시작 하기 전에 공급자 모델에 프로필 데이터를 저장 하는 환경을 살펴보겠습니다. 응용 프로그램 사용자에 대 한 프로필 데이터는 여러 가지 방법으로 저장 될 수 있으며, Universal Providers와 함께 제공 되는 기본 제공 프로필 공급자를 사용 하는 중에 가장 일반적입니다. 단계는 다음과 같습니다.

1. 프로필 데이터를 저장 하는 데 사용 되는 속성이 있는 클래스를 추가 합니다.
2. ' ProfileBase '를 확장 하는 클래스를 추가 하 고 사용자에 대 한 위의 프로필 데이터를 가져오는 메서드를 구현 합니다.
3. *Web.config* 파일에서 기본 프로필 공급자를 사용 하도록 설정 하 고 프로필 정보에 액세스 하는 데 사용할 #2 단계에서 선언 된 클래스를 정의 합니다.

프로필 정보는 데이터베이스의 ' 프로필 ' 테이블에 serialize 된 xml 및 이진 데이터로 저장 됩니다.

새 ASP.NET Identity 시스템을 사용 하도록 응용 프로그램을 마이그레이션한 후 프로필 정보는 deserialize 되어 사용자 클래스의 속성으로 저장 됩니다. 그런 다음 각 속성을 사용자 테이블의 열에 매핑할 수 있습니다. 여기서의 장점은 속성에 액세스할 때 데이터 정보를 serialize/deserialize 할 필요 없이 사용자 클래스를 사용 하 여 직접 작업을 수행할 수 있다는 것입니다.

## <a name="getting-started"></a>시작하기

1. Visual Studio 2012에서 새로운 ASP.NET 4.5 Web Forms 응용 프로그램을 만듭니다. 현재 샘플에서는 Web Forms 템플릿을 사용 하지만 MVC 응용 프로그램도 사용할 수 있습니다.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.jpg)
2. 프로필 정보를 저장할 새 ' 모델 ' 폴더 만들기  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.png)
3. 예를 들어 사용자의 생년월일, 구/군/시 및 무게를 프로필에 저장 하도록 합니다. Height 및 weight는 ' PersonalStats ' 라는 사용자 지정 클래스로 저장 됩니다. 프로필을 저장 하 고 검색 하려면 ' ProfileBase '를 확장 하는 클래스가 필요 합니다. 프로필 정보를 가져오고 저장 하는 새 ' AppProfile ' 클래스를 만들어 보겠습니다.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample1.cs)]
4. *Web.config 파일에서* profile을 사용 하도록 설정 합니다. #3 단계에서 만든 사용자 정보를 저장/검색 하는 데 사용할 클래스 이름을 입력 합니다.

    [!code-xml[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample2.xml)]
5. ' Account ' 폴더에 web forms 페이지를 추가 하 여 사용자의 프로필 데이터를 가져오고 저장 합니다. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 ' 새 항목 추가 '를 선택 합니다. 마스터 페이지가 ' AddProfileData .aspx ' 인 새 webforms 페이지를 추가 합니다. ' MainContent ' 섹션에서 다음을 복사 합니다.

    [!code-html[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample3.html)]

   코드 뒤에 다음 코드를 추가 합니다.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample4.cs)]

   AppProfile 클래스가 정의 된 네임 스페이스를 추가 하 여 컴파일 오류를 제거 합니다.
6. 앱을 실행 하 고 사용자 이름 '**olduser '** 를 사용 하 여 새 사용자를 만듭니다. ' AddProfileData ' 페이지로 이동 하 여 사용자에 대 한 프로필 정보를 추가 합니다.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.png)

서버 탐색기 창을 사용 하 여 데이터가 ' 프로필 ' 테이블에 serialize 된 xml로 저장 되었는지 확인할 수 있습니다. Visual Studio의 ' 보기 ' 메뉴에서 ' 서버 탐색기 '를 선택 합니다. *Web.config 파일에* 정의 된 데이터베이스에 대 한 데이터 연결이 있어야 합니다. 데이터 연결을 클릭 하면 다른 하위 범주가 표시 됩니다. ' 테이블 '을 확장 하 여 데이터베이스의 여러 테이블을 표시 한 다음 ' 프로필 '을 마우스 오른쪽 단추로 클릭 하 고 ' 테이블 데이터 표시 '를 선택 하 여 프로필 테이블에 저장 된 프로필 데이터를 확인 합니다.

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.png)

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image4.png)

## <a name="migrating-database-schema"></a>데이터베이스 스키마 마이그레이션

기존 데이터베이스가 Id 시스템에서 작동 하도록 하려면 원본 데이터베이스에 추가한 필드를 지원 하도록 Id 데이터베이스의 스키마를 업데이트 해야 합니다. SQL 스크립트를 사용 하 여 새 테이블을 만들고 기존 정보를 복사 하 여이 작업을 수행할 수 있습니다. ' 서버 탐색기 ' 창에서 ' DefaultConnection '을 확장 하 여 테이블을 표시 합니다. 테이블을 마우스 오른쪽 단추로 클릭 하 고 ' 새 쿼리 '를 선택 합니다.

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image5.png)

[https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt) 에서 SQL 스크립트를 붙여넣고 실행 합니다. ' DefaultConnection '을 새로 고치면 새 테이블이 추가 된 것을 볼 수 있습니다. 테이블 내부의 데이터를 확인 하 여 정보가 마이그레이션 되었는지 확인할 수 있습니다.

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image6.png)

## <a name="migrating-the-application-to-use-aspnet-identity"></a>ASP.NET Identity 사용 하도록 응용 프로그램 마이그레이션

1. ASP.NET Identity에 필요한 Nuget 패키지를 설치 합니다.

    - Microsoft.AspNet.Identity.EntityFramework
    - Microsoft.AspNet.Identity.Owin
    - Microsoft.Owin.Host.SystemWeb
    - Microsoft.Owin.Security.Facebook
    - Microsoft.Owin.Security.Google
    - Microsoft.Owin.Security.MicrosoftAccount
    - Microsoft.Owin.Security.Twitter

   Nuget 패키지 관리에 대 한 자세한 내용은 여기를 참조 [하세요](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog) .
2. 테이블의 기존 데이터로 작업 하려면 테이블에 다시 매핑하고 Id 시스템에 후크 하는 모델 클래스를 만들어야 합니다. Id 계약의 일부로 모델 클래스는 Id. Core dll에 정의 된 인터페이스를 구현 하거나, Microsoft. AspNet. i d. EntityFramework에서 사용할 수 있는 이러한 인터페이스의 기존 구현을 확장할 수 있습니다. 역할, 사용자 로그인 및 사용자 클레임에 대 한 기존 클래스를 사용 합니다. 샘플에 사용자 지정 사용자를 사용 해야 합니다. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 새 폴더 ' IdentityModels '을 만듭니다. 아래와 같이 새 ' User ' 클래스를 추가 합니다.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample5.cs)]

   이제 ' ProfileInfo '는 사용자 클래스의 속성입니다. 따라서 사용자 클래스를 사용 하 여 프로필 데이터를 직접 작업할 수 있습니다.

다운로드 원본 ( [https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) )에서 **IdentityModels** 및 **IdentityAccount** 폴더의 파일을 복사 합니다. 여기에는 ASP.NET Identity Api를 사용 하 여 사용자 및 역할을 관리 하는 데 필요한 나머지 모델 클래스와 새 페이지가 있습니다. 사용 되는 방법은 SQL 멤버 자격과 비슷하며 자세한 설명은 [여기](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)에서 찾을 수 있습니다.

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

## <a name="copying-profile-data-to-the-new-tables"></a>새 테이블에 프로필 데이터 복사

앞서 설명한 것 처럼 프로필 테이블에서 xml 데이터를 deserialize 하 고 AspNetUsers 테이블의 열에 저장 해야 합니다. 이전 단계에서 사용자 테이블에 새 열이 생성 되었으므로 이러한 열은 모두 필요한 데이터로 채웁니다. 이렇게 하려면 한 번 실행 되는 콘솔 응용 프로그램을 사용 하 여 사용자 테이블에서 새로 만든 열을 채웁니다.

1. 종료 하는 솔루션에서 새 콘솔 응용 프로그램을 만듭니다.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.jpg)
2. Entity Framework 패키지의 최신 버전을 설치 합니다.
3. 위에서 만든 웹 응용 프로그램을 콘솔 응용 프로그램에 대 한 참조로 추가 합니다. 이렇게 하려면 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 ' 참조 추가 ', 솔루션을 차례로 클릭 한 다음 프로젝트를 클릭 하 고 확인을 클릭 합니다.
4. Program.cs 클래스에서 아래 코드를 복사 합니다. 이 논리는 각 사용자에 대 한 프로필 데이터를 읽고 ' ProfileInfo ' 개체로 직렬화 한 후 다시 데이터베이스에 저장 합니다.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample6.cs)]

   사용 되는 일부 모델은 웹 응용 프로그램 프로젝트의 ' IdentityModels ' 폴더에 정의 되어 있으므로 해당 하는 네임 스페이스를 포함 해야 합니다.
5. 위의 코드는 이전 단계에서 만든 웹 응용 프로그램 프로젝트의 App\_Data 폴더에 있는 데이터베이스 파일에 대해 작동 합니다. 이를 참조 하려면 콘솔 응용 프로그램의 app.config 파일에서 web.config 파일의 연결 문자열을 웹 응용 프로그램의 web.config에 있는 연결 문자열로 업데이트 합니다. 또한 ' AttachDbFilename ' 속성에 전체 실제 경로를 제공 합니다.
6. 명령 프롬프트를 열고 위의 콘솔 응용 프로그램의 bin 폴더로 이동 합니다. 실행 파일을 실행 하 고 다음 이미지에 표시 된 것 처럼 로그 출력을 검토 합니다.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.jpg)
7. 서버 탐색기에서 ' AspNetUsers ' 테이블을 열고 속성이 포함 된 새 열의 데이터를 확인 합니다. 해당 속성 값으로 업데이트 해야 합니다.

## <a name="verify-functionality"></a>기능 확인

ASP.NET Identity를 사용 하 여 구현 되는 새로 추가 된 멤버 자격 페이지를 사용 하 여 이전 데이터베이스에서 사용자에 게 로그인 합니다. 사용자는 동일한 자격 증명을 사용 하 여 로그인 할 수 있어야 합니다. OAuth를 추가 하 고, 새 사용자를 만들고, 암호를 변경 하 고, 역할을 추가 하 고, 역할에 사용자를 추가 하는 등의 다른 기능을 사용해 봅니다.

이전 사용자 및 새 사용자에 대 한 프로필 데이터를 검색 하 여 사용자 테이블에 저장 해야 합니다. 이전 테이블은 더 이상 참조 되지 않습니다.

## <a name="conclusion"></a>결론

이 문서에서는 ASP.NET Identity에 대 한 멤버 자격을 위해 공급자 모델을 사용 하는 웹 응용 프로그램을 마이그레이션하는 프로세스를 설명 했습니다. 이 문서에서는 사용자가 Id 시스템에 후크 할 수 있도록 프로필 데이터를 추가로 마이그레이션 하는 방법을 설명 합니다. 앱을 마이그레이션할 때 발생 한 질문과 문제는 아래에 의견을 남겨 주세요.

*문서를 검토 하는 Rick Anderson 및 Robert McMurray에 감사 합니다.*
