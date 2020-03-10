---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: ASP.NET 웹 페이지 (Razor) 사이트에 대 한 사이트 전체 동작 사용자 지정 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 페이지가 아니라 전체 웹 사이트 또는 전체 폴더에 대 한 설정을 만드는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: f05e05f725d9209bce283ce18659ae5efe4de2ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515249"
---
# <a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에 대 한 사이트 전체 동작 사용자 지정

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트의 페이지에 대 한 사이트 쪽 설정을 만드는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - 사이트의 모든 페이지에 대해 값 (전역 값 또는 도우미 설정)을 설정 하는 데 사용할 수 있는 코드를 실행 하는 방법입니다.
> - 폴더의 모든 페이지에 대 한 값을 설정 하는 데 사용할 수 있는 코드를 실행 하는 방법입니다.
> - 페이지 로드 전후에 코드를 실행 하는 방법입니다.
> - 오류를 중앙 오류 페이지로 보내는 방법
> - 폴더의 모든 페이지에 인증을 추가 하는 방법
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 3
> - ASP.NET 웹 도우미 라이브러리 (NuGet 패키지)
>   
> 
> ASP.NET 웹 도우미 라이브러리를 사용할 수 없다는 점을 제외 하 고이 자습서는 ASP.NET 웹 페이지 3 및 Visual Studio 2013 (또는 웹 Visual Studio Express 2013) 에서도 작동 합니다.

<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a>ASP.NET 웹 페이지에 대 한 웹 사이트 시작 코드 추가

ASP.NET 웹 페이지에서 작성 하는 코드의 대부분이 개별 페이지에 해당 페이지에 필요한 모든 코드가 포함 될 수 있습니다. 예를 들어, 페이지에서 전자 메일 메시지를 보내는 경우 해당 작업에 대 한 모든 코드를 단일 페이지에 넣을 수 있습니다. 여기에는 전자 메일을 보내기 위한 설정 (즉, SMTP 서버)을 초기화 하 고 전자 메일 메시지를 보내는 코드가 포함 될 수 있습니다.

그러나 일부 경우에는 사이트의 모든 페이지가 실행 되기 전에 일부 코드를 실행할 수 있습니다. 이는 사이트의 어디에서 나 사용할 수 있는 값 ( *전역 값*이라고 함)을 설정 하는 데 유용 합니다. 예를 들어 일부 도우미는 전자 메일 설정 또는 계정 키와 같은 값을 제공 해야 합니다. 이러한 설정을 전역 값으로 유지 하는 것이 편리할 수 있습니다.

사이트의 루트에 *\_AppStart* 라는 페이지를 만들어이 작업을 수행할 수 있습니다. 이 페이지가 있으면 사이트의 페이지가 처음 요청 될 때 실행 됩니다. 따라서 코드를 실행 하 여 전역 값을 설정 하는 것이 좋습니다. AppStart에는 밑줄 접두사가 *\_* 있기 때문에 ASP.NET는 사용자가 직접 요청 하는 경우에도 페이지를 브라우저로 보내지 않습니다.

다음 다이어그램에서는 *\_AppStart* 페이지가 작동 하는 방법을 보여 줍니다. 페이지에 대 한 요청이 들어오면이 요청이 사이트의 모든 페이지에 대 한 첫 번째 요청이 면 ASP.NET는 먼저 *\_AppStart* 페이지가 있는지 여부를 확인 합니다. 이 경우 *\_AppStart* 페이지의 모든 코드가 실행 되 고 요청한 페이지가 실행 됩니다.

![[이미지]](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a>웹 사이트에 대 한 전역 값 설정

1. WebMatrix 웹 사이트의 루트 폴더에서 *AppStart\_* 라는 파일을 만듭니다. 파일은 사이트의 루트에 있어야 합니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    이 코드는 사이트의 모든 페이지에서 자동으로 사용할 수 있는 `AppState` 사전에 값을 저장 합니다. *\_AppStart* 파일에는 태그가 없습니다. 이 페이지는 코드를 실행 한 다음 원래 요청 된 페이지로 리디렉션합니다.

    > [!NOTE]
    > *\_AppStart* 파일에 코드를 넣을 때는 주의 해야 합니다. *\_AppStart* 파일의 코드에서 오류가 발생 하는 경우 웹 사이트가 시작 되지 않습니다.
3. 루트 폴더에서 *AppName. cshtml*이라는 새 페이지를 만듭니다.
4. 기본 태그와 코드를 다음으로 바꿉니다. 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    이 코드는 *\_AppStart* 페이지에서 설정한 `AppState` 개체에서 값을 추출 합니다.
5. 브라우저에서 *AppName* 페이지를 실행 합니다. (파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.) 이 페이지에는 전역 값이 표시 됩니다. 

    ![[이미지]](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a>도우미에 대 한 값 설정

*\_AppStart* 파일에 사용 하는 것은 사이트에서 사용 하 고 초기화 해야 하는 도우미에 대 한 값을 설정 하는 것입니다. 일반적인 예는 `WebMail` 도우미에 대 한 전자 메일 설정 및 `ReCaptcha` 도우미에 대 한 개인 및 공개 키입니다. 이와 같은 경우에 *\_AppStart* 에서 값을 한 번 설정할 수 있습니다. 그러면 해당 값이 사이트의 모든 페이지에 대해 이미 설정 된 것입니다.

이 절차에서는 `WebMail` 설정을 전역적으로 설정 하는 방법을 보여 줍니다. `WebMail` 도우미를 사용 하는 방법에 대 한 자세한 내용은 [ASP.NET 웹 페이지 사이트에 전자 메일 추가](../getting-started/11-adding-email-to-your-web-site.md)를 참조 하세요.

1. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)의 설명에 따라 웹 사이트에 ASP.NET 웹 도우미 라이브러리를 추가 합니다 (아직 추가 하지 않은 경우).
2. *\_AppStart* 파일이 아직 없는 경우 웹 사이트의 루트 폴더에서 *AppStart\_* 라는 파일을 만듭니다.
3. 다음 `WebMail` 설정을 *\_AppStart* 파일에 추가 합니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    코드에서 다음과 같은 전자 메일 관련 설정을 수정 합니다.

   - `your-SMTP-host`를 액세스할 수 있는 SMTP 서버의 이름으로 설정 합니다.
   - `your-user-name-here`를 SMTP 서버 계정에 대 한 사용자 이름으로 설정 합니다.
   - `your-account-password`를 SMTP 서버 계정의 암호로 설정 합니다.
   - `your-email-address-here`를 본인의 전자 메일 주소로 설정 합니다. 메시지가 전송 되는 전자 메일 주소입니다. (일부 전자 메일 공급자는 다른 `From` 주소를 지정 하는 것을 허용 하지 않으며 사용자 이름을 `From` 주소로 사용 합니다.)

     SMTP 설정에 대 한 자세한 내용은 [ASP.NET 웹 페이지 (razor) 사이트에서 전자 메일 보내기](https://go.microsoft.com/fwlink/?LinkID=202899) 및 [ASP.NET 웹 페이지 (Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)에서 전자 [메일 보내기와 관련 된 문제](https://go.microsoft.com/fwlink/?LinkId=253001#email) 문서에서 [전자 메일 설정 구성](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings) 을 참조 하세요.
4. *\_AppStart* 파일을 저장 하 고 닫습니다.
5. 웹 사이트의 루트 폴더에서 *Testemail. cshtml*라는 새 페이지를 만듭니다.
6. 기존 콘텐츠를 다음으로 바꿉니다. 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. 브라우저에서 *Testemail. cshtml* 페이지를 실행 합니다.
8. 필드를 입력 하 여 자신에 게 전자 메일 메시지를 보낸 다음 **보내기**를 클릭 합니다.
9. 전자 메일을 확인 하 여 메시지를 받았는지 확인 합니다.

이 예제의 중요 한 부분은 일반적으로 변경 되지 않는 설정 (예: SMTP 서버 이름 및 전자 메일 자격 증명)이 *\_AppStart* 파일에 설정 되어 있다는 것입니다. 이렇게 하면 전자 메일을 보내는 각 페이지에서 다시 설정할 필요가 없습니다. 어떤 이유로 이러한 설정을 변경 해야 하는 경우에는 페이지에서 개별적으로 설정할 수 있습니다. 페이지에서 받는 사람 및 전자 메일 메시지 본문과 같이 일반적으로 매번 변경 되는 값만 설정 합니다.

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a>폴더의 파일 전후에 코드 실행

*AppStart를\_* 사용 하 여 사이트의 페이지가 실행 되기 전에 코드를 작성 하는 것과 마찬가지로 특정 폴더의 모든 페이지가 실행 되기 전에 실행 되는 코드를 작성할 수 있습니다. 폴더의 모든 페이지에 대해 동일한 레이아웃 페이지를 설정 하거나 폴더의 페이지를 실행 하기 전에 사용자가 로그인 했는지 확인 하는 등의 작업을 수행 하는 경우에 유용 합니다.

특정 폴더의 페이지에 대해 *\_PageStart. cshtml*이라는 파일에 코드를 만들 수 있습니다. 다음 다이어그램에서는 *\_PageStart. cshtml* 페이지가 작동 하는 방법을 보여 줍니다. 페이지에 대 한 요청이 들어오면 ASP.NET는 먼저 *\_AppStart* 페이지를 확인 하 고이를 실행 합니다. 그런 다음 ASP.NET는 *\_PageStart. cshtml* 페이지가 있는지 여부를 확인 하 고, 있는 경우이를 실행 합니다. 그런 다음 요청 된 페이지를 실행 합니다.

*\_PageStart. cshtml* 페이지 내에서 처리 중에 `RunPage` 메서드를 포함 하 여 요청 된 페이지를 실행 하려는 위치를 지정할 수 있습니다. 이렇게 하면 요청 된 페이지가 실행 되기 전에 코드를 실행 한 후 다시 실행할 수 있습니다. `RunPage`를 포함 하지 않는 경우 *\_PageStart* 의 모든 코드가 실행 되 고 요청한 페이지가 자동으로 실행 됩니다.

![[이미지]](18-customizing-site-wide-behavior/_static/image3.jpg)

ASP.NET를 사용 하면 *\_PageStart. cshtml* 파일의 계층 구조를 만들 수 있습니다. 사이트의 루트 및 모든 하위 폴더에 *\_PageStart. cshtml* 파일을 배치할 수 있습니다. 페이지가 요청 되 면 최상위 수준 (사이트 루트에 가장 가까운)의 *\_PageStart. cshtml* 파일이 실행 된 다음, 다음 하위 폴더의 *\_pagestart. cshtml* 파일 및 요청이 요청 된 페이지를 포함 하는 폴더에 도달할 때까지 하위 폴더 구조에서 중단 됩니다. 해당 하는 모든 *\_PageStart. cshtml* 파일이 실행 된 후 요청 된 페이지가 실행 됩니다.

예를 들어 다음과 같은 *\_PageStart. cshtml* 파일 및 *기본값 cshtml* 파일의 조합을 사용할 수 있습니다.

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

*/Myfolder/default.cshtml*를 실행 하면 다음이 표시 됩니다.

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a>폴더의 모든 페이지에 대 한 초기화 코드 실행

*\_PageStart. cshtml* 파일은 단일 폴더에 있는 모든 파일에 대해 동일한 레이아웃 페이지를 초기화 하는 데 사용 하는 것이 좋습니다.

1. 루트 폴더에서 *Initpages*라는 새 폴더를 만듭니다.
2. 웹 사이트의 *Initpages* 폴더에서 이름이 *\_pagestart. cshtml* 인 파일을 만들고 기본 태그와 코드를 다음으로 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. 웹 사이트의 루트에서 *Shared*라는 폴더를 만듭니다.
4. *공유* 폴더에서 *Layout1\_* 라는 파일을 만들고 기본 태그와 코드를 다음으로 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. *Initpages* 폴더에서 *Content1* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. *Initpages* 폴더에서 *Content2* 이라는 다른 파일을 만들고 기본 태그를 다음으로 바꿉니다. 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. 브라우저에서 *Content1* 를 실행 합니다. 

    ![[이미지]](18-customizing-site-wide-behavior/_static/image4.jpg)

    *Content1* 페이지가 실행 되 면 *\_pagestart. cshtml* 파일은 `Layout`를 설정 하 고 `PageData["MyBackground"]`를 색으로 설정 합니다. *Content1*에서 레이아웃과 색이 적용 됩니다.
8. 브라우저에 *Content2* 를 표시 합니다. 

    두 페이지가 모두 동일한 레이아웃 페이지와 *\_PageStart. cshtml*에서 초기화 된 색을 사용 하기 때문에 레이아웃은 동일 합니다.

## <a name="using-_pagestartcshtml-to-handle-errors"></a>\_PageStart. cshtml를 사용 하 여 오류 처리

*\_PageStart. cshtml* 파일의 또 다른 용도는 폴더의 모든 *cshtml* 페이지에서 발생할 수 있는 프로그래밍 오류 (예외)를 처리 하는 방법을 만드는 것입니다. 이 예제에서는이 작업을 수행 하는 한 가지 방법을 보여 줍니다.

1. 루트 폴더에서 *Initcatch*라는 폴더를 만듭니다.
2. 웹 사이트의 *Initcatch* 폴더에서 이름이 *\_pagestart. cshtml* 인 파일을 만들고 기존 태그와 코드를 다음으로 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    이 코드에서는 `try` 블록 내에서 `RunPage` 메서드를 호출 하 여 요청 된 페이지를 명시적으로 실행 해 봅니다. 요청 된 페이지에서 프로그래밍 오류가 발생 하면 `catch` 블록 내의 코드가 실행 됩니다. 이 경우 코드는 페이지로 리디렉션되고 (*오류. cshtml*) URL의 일부로 오류가 발생 한 파일의 이름을 전달 합니다. (곧 페이지를 만듭니다.)
3. 웹 사이트의 *Initcatch* 폴더에서 다음과 같이 *file 이라는 파일* 을 만들고 기존 태그와 코드를 다음으로 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    이 예의 목적에 따라이 페이지에서 수행 하는 작업은 존재 하지 않는 데이터베이스 파일을 열려고 시도 하 여 의도적으로 오류를 생성 하는 것입니다.
4. 루트 폴더에서 *오류. cshtml* 라는 파일을 만들고 기존 태그와 코드를 다음으로 바꿉니다. 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    이 페이지에서 식 `@Request["source"]` URL에서 값을 가져와 표시 합니다.
5. 도구 모음에서 **저장**을 클릭 합니다.
6. 브라우저에서 *. cshtml* 를 실행 합니다. 

    ![[이미지]](18-customizing-site-wide-behavior/_static/image5.jpg)

    오류가 발생 했기 *때문에* *\_pagestart. cshtml* 페이지는 메시지를 표시 하는 *오류. cshtml* 파일로 리디렉션합니다.

    예외에 대 한 자세한 내용은 [Razor 구문을 사용한 ASP.NET 웹 페이지 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=251587)를 참조 하세요.

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-_pagestartcshtml-to-restrict-folder-access"></a>\_PageStart. cshtml를 사용 하 여 폴더 액세스 제한

*\_PageStart. cshtml* 파일을 사용 하 여 폴더의 모든 파일에 대 한 액세스를 제한할 수도 있습니다.

1. WebMatrix에서 **템플릿에서 사이트** 옵션을 사용 하 여 새 웹 사이트를 만듭니다.
2. 사용 가능한 템플릿에서 **스타터 사이트**를 선택 합니다.
3. 루트 폴더에서 이름이 *AuthenticatedContent*인 폴더를 만듭니다.
4. *AuthenticatedContent* 폴더에서 *\_이름이 pagestart. cshtml* 인 파일을 만들고 기존 태그와 코드를 다음으로 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    이 코드는 폴더의 모든 파일이 캐시 되는 것을 방지 하는 것으로 시작 합니다. 이는 사용자의 캐시 된 페이지를 다음 사용자가 사용할 수 없도록 하려는 공용 컴퓨터와 같은 시나리오에 필요 합니다. 그런 다음 코드는 사용자가 사이트에 로그인 했는지 여부를 확인 한 다음 폴더의 모든 페이지를 볼 수 있습니다. 사용자가 로그인 하지 않은 경우에는 코드가 로그인 페이지로 리디렉션됩니다. 로그인 페이지는 `ReturnUrl`라는 쿼리 문자열 값을 포함 하는 경우 원래 요청 된 페이지로 사용자를 반환할 수 있습니다.
5. AuthenticatedContent 폴더에 라는 새 페이지를 만듭니다 *.*
6. 기본 태그를 다음으로 바꿉니다.  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. 브라우저에서 *페이지* 탐색기를 실행 합니다. 이 코드는 사용자를 로그인 페이지로 리디렉션합니다. 로그인 하려면 먼저 등록 해야 합니다. 등록 하 고 로그인 한 후에는 페이지로 이동 하 여 해당 내용을 볼 수 있습니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

[Razor 구문을 사용한 ASP.NET 웹 페이지 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=251587)
