---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Razor 및 비-JavaScript를 사용 하 여 MVC 3 응용 프로그램 만들기 | Microsoft Docs
author: microsoft
description: 사용자 목록 샘플 웹 응용 프로그램은 Razor 뷰 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 간단한 방법을 보여 줍니다. 응용 프로그램 샘플 ...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434999"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Razor 및 비간섭 JavaScript를 사용해 MVC 3 응용 프로그램 만들기

[Microsoft](https://github.com/microsoft) 에서

> 사용자 목록 샘플 웹 응용 프로그램은 Razor 뷰 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 간단한 방법을 보여 줍니다. 샘플 응용 프로그램은 ASP.NET MVC 버전 3 및 Visual Studio 2010에서 새 Razor 뷰 엔진을 사용 하 여 사용자 만들기, 표시, 편집 및 삭제와 같은 기능을 포함 하는 가상의 사용자 목록 웹 사이트를 만드는 방법을 보여 줍니다.
> 
> 이 자습서에서는 사용자 목록 샘플 ASP.NET MVC 3 응용 프로그램을 빌드하기 위해 수행 된 단계에 대해 설명 합니다. 및 VB 소스 코드를 C# 포함 하는 Visual Studio 프로젝트를 다운로드 하 여 [다운로드할](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)수 있습니다. 이 자습서에 대 한 질문이 있는 경우 [MVC 포럼](https://forums.asp.net/1146.aspx)에 게시 해 주세요.

## <a name="overview"></a>개요

빌드할 응용 프로그램은 간단한 사용자 목록 웹 사이트입니다. 사용자는 사용자 정보를 입력 하 고, 확인 하 고, 업데이트할 수 있습니다.

![샘플 사이트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

C# [여기](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)에서 VB 및 완료 된 프로젝트를 다운로드할 수 있습니다.

## <a name="creating-the-web-application"></a>웹 응용 프로그램 만들기

자습서를 시작 하려면 Visual Studio 2010을 열고 *ASP.NET MVC 3 웹 응용 프로그램* 템플릿을 사용 하 여 새 프로젝트를 만듭니다. 응용 프로그램의 이름을 Mvc3Razor&quot;로 &quot;합니다.

[새 MVC 3 프로젝트 ![](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

**새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**을 선택 하 고 Razor 뷰 엔진을 선택한 다음 **확인**을 클릭 합니다.

![새 ASP.NET MVC 3 프로젝트 대화 상자](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

이 자습서에서는 ASP.NET 멤버 자격 공급자를 사용 하지 않으므로 로그온 및 멤버 자격과 관련 된 모든 파일을 삭제할 수 있습니다. **솔루션 탐색기**에서 다음 파일 및 디렉터리를 제거 합니다.

- *Controllers\AccountController*
- *Models\AccountModels*
- *Views\Shared\\_LogOnPartial*
- *Views\Account* (및이 디렉터리의 모든 파일)

![고 개 Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<em>\_Layout</em> 파일을 편집 하 고 `logindisplay` 이라는 `<div>` 요소 내부의 태그를 로그인 사용 안 함&quot;<em>&quot;</em>메시지로 바꿉니다. 다음 예제에서는 새 태그를 보여 줍니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>모델 추가

**솔루션 탐색기**에서 *모델* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **클래스**를 클릭 합니다.

![새 사용자 Mdl 클래스](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

클래스 `UserModel` 이름을 지정합니다. *Usermodel* 파일의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

`UserModel` 클래스는 사용자를 나타냅니다. 클래스의 각 멤버에는 [dataannotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스의 [필수](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 특성으로 주석이 추가 됩니다. [Dataannotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스의 특성은 웹 응용 프로그램에 대 한 자동 클라이언트 및 서버 쪽 유효성 검사를 제공 합니다.

`HomeController` 클래스를 열고 `UserModel` 및 `Users` 클래스에 액세스할 수 있도록 `using` 지시문을 추가 합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

`HomeController` 선언 바로 뒤에 다음 주석과 `Users` 클래스에 대 한 참조를 추가 합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

`Users` 클래스는이 자습서에서 사용할 수 있는 간소화 된 메모리 내 데이터 저장소입니다. 실제 응용 프로그램에서는 데이터베이스를 사용 하 여 사용자 정보를 저장 합니다. 다음 예제에서는 `HomeController` 파일의 처음 몇 줄을 보여 줍니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

사용자 모델을 다음 단계에서 스 캐 폴딩 마법사에서 사용할 수 있도록 응용 프로그램을 빌드합니다.

## <a name="creating-the-default-view"></a>기본 보기 만들기

다음 단계는 사용자를 표시 하는 작업 메서드와 뷰를 추가 하는 것입니다.

기존 *Views\Home\Index* 파일을 삭제 합니다. 사용자를 표시 하는 새 *인덱스* 파일을 만듭니다.

`HomeController` 클래스에서 `Index` 메서드의 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

`Index` 메서드 내부를 마우스 오른쪽 단추로 클릭 한 다음 **뷰 추가**를 클릭 합니다.

![뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

**강력한 형식의 뷰 만들기** 옵션을 선택 합니다. **뷰 데이터 클래스**에 대해 **Mvc3Razor**를 선택 합니다. ( **데이터 클래스 보기** 상자에 **Mvc3Razor** 가 표시 되지 않으면 프로젝트를 빌드해야 합니다.) 뷰 엔진이 **Razor**로 설정 되어 있는지 확인 합니다. **콘텐츠 보기** 를 **목록** 으로 설정 하 고 **추가**를 클릭 합니다.

![인덱스 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

새 뷰는 `Index` 뷰에 전달 되는 사용자 데이터를 자동으로 스 캐 폴드 합니다. 새로 생성 된 *Views\Home\Index* 파일을 검사 합니다. **새로 만들기**, **편집**, **세부 정보**및 **삭제** 링크가 작동 하지 않지만 페이지의 나머지 부분은 작동 합니다. 페이지를 실행 합니다. 사용자 목록이 표시 됩니다.

![인덱스 페이지](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

다음 코드를 사용 하 여 *인덱스 cshtml* 파일을 열고 **편집**, **세부 정보**및 **삭제** 에 대 한 `ActionLink` 태그를 바꿉니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

사용자 이름은 **편집**, **세부 정보**및 **삭제** 링크에서 선택한 레코드를 찾는 ID로 사용 됩니다.

## <a name="creating-the-details-view"></a>세부 정보 보기 만들기

다음 단계는 사용자 세부 정보를 표시 하기 위해 `Details` 작업 메서드 및 보기를 추가 하는 것입니다.

![세부 정보](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

다음 `Details` 메서드를 홈 컨트롤러에 추가 합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

`Details` 메서드 내부를 마우스 오른쪽 단추로 클릭 한 다음 <strong>뷰 추가</strong>를 선택 합니다. <strong>데이터 클래스 보기</strong> 상자에 <strong>Mvc3Razor 모델이</strong>포함 되어 있는지<em>확인 합니다.</em> <strong>콘텐츠 보기</strong> 를 <strong>자세히</strong> 로 설정 하 고 <strong>추가</strong>를 클릭 합니다.

![세부 정보 보기 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

응용 프로그램을 실행 하 고 세부 정보 링크를 선택 합니다. 자동 스 캐 폴딩은 모델의 각 속성을 보여 줍니다.

![세부 정보](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>편집 뷰 만들기

다음 `Edit` 메서드를 home 컨트롤러에 추가 합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

이전 단계에서와 같이 뷰를 추가 하지만 **뷰 콘텐츠** 를 **편집**으로 설정 합니다.

![편집 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

응용 프로그램을 실행 하 고 사용자 중 하나의 성과 이름을 편집 합니다. `UserModel` 클래스에 적용 된 `DataAnnotation` 제약 조건을 위반 하는 경우 폼을 제출할 때 서버 코드에서 생성 된 유효성 검사 오류가 표시 됩니다. 예를 들어 Ann&quot; &quot;이름을 변경 하 여&quot;을 &quot;경우 양식을 제출할 때 다음 오류가 폼에 표시 됩니다.

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

이 자습서에서는 사용자 이름을 기본 키로 처리 합니다. 따라서 사용자 이름 속성은 변경할 수 없습니다. *편집. cshtml* 파일에서 `Html.BeginForm` 문 바로 뒤에 사용자 이름을 숨겨진 필드로 설정 합니다. 이렇게 하면 속성이 모델에 전달 됩니다. 다음 코드 조각에서는 `Hidden` 문을 배치 하는 방법을 보여 줍니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

사용자 이름에 대 한 `TextBoxFor` 및 `ValidationMessageFor` 태그를 `DisplayFor` 호출로 바꿉니다. `DisplayFor` 메서드는 속성을 읽기 전용 요소로 표시 합니다. 다음 예제에서는 전체 태그를 보여 줍니다. 원래 `TextBoxFor` 및 `ValidationMessageFor` 호출은 Razor 시작-주석 및 끝 주석 문자 (`@* *@`)로 주석 처리 됩니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>클라이언트 쪽 유효성 검사 사용

ASP.NET MVC 3에서 클라이언트 쪽 유효성 검사를 사용 하도록 설정 하려면 두 개의 플래그를 설정 하 고 세 개의 JavaScript 파일을 포함 해야 합니다.

응용 프로그램의 *web.config* 파일을 엽니다. 응용 프로그램 설정에서 `that ClientValidationEnabled` 및 `UnobtrusiveJavaScriptEnabled`이 true로 설정 되어 있는지 확인 합니다. 루트 web.config 파일의 다음 조각은 올바른 설정을 보여 *줍니다.*

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

`UnobtrusiveJavaScriptEnabled`를 true로 설정 하면 Ajax와 클라이언트의 유효성을 검사 하지 않아도 됩니다. 비 표시 유효성 검사를 사용 하는 경우 유효성 검사 규칙이 HTML5 특성으로 전환 됩니다. HTML5 특성 이름은 소문자, 숫자 및 대시로만 구성 될 수 있습니다.

`ClientValidationEnabled`를 true로 설정 하면 클라이언트 쪽 유효성 검사를 수행할 수 있습니다. 응용 프로그램 *web.config* 파일에서 이러한 키를 설정 하 여 전체 응용 프로그램에 대 한 클라이언트 유효성 검사 및 비 표시 JavaScript를 사용 하도록 설정 합니다. 다음 코드를 사용 하 여 개별 뷰나 컨트롤러 메서드에서 이러한 설정을 사용 하거나 사용 하지 않도록 설정할 수도 있습니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

또한 렌더링 된 뷰에 여러 JavaScript 파일을 포함 해야 합니다. 모든 뷰에 JavaScript를 포함 하는 쉬운 방법은 *Views\Shared\\_Layout* 파일에 추가 하는 것입니다. *\_Layout. cshtml* 파일의 `<head>` 요소를 다음 코드로 바꿉니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

처음 두 jQuery 스크립트는 Microsoft Ajax Content Delivery Network (CDN)에서 호스팅됩니다. Microsoft Ajax CDN을 활용 하 여 응용 프로그램의 첫 번째 적중 성능을 크게 향상 시킬 수 있습니다.

응용 프로그램을 실행 하 고 편집 링크를 클릭 합니다. 브라우저에서 페이지의 소스를 봅니다. 브라우저 소스는 데이터 유효성 검사를 위해 `data-val` 폼의 많은 특성을 보여 줍니다. 클라이언트 유효성 검사 및 문제가 없는 JavaScript를 사용 하는 경우 클라이언트 유효성 검사 규칙을 사용 하는 입력 필드에 `data-val="true"` 특성이 포함 되어 문제가 없는 클라이언트 유효성 검사를 트리거합니다. 예를 들어 모델의 `City` 필드가 [필수](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 특성으로 데코레이팅 되었으므로 다음 예제에 표시 된 HTML이 생성 됩니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

각 클라이언트 유효성 검사 규칙에 대해 양식이 `data-val-rulename="message"`된 특성이 추가 됩니다. 앞에 표시 된 `City` 필드 예제를 사용 하 여 필요한 클라이언트 유효성 검사 규칙은 `data-val-required` 특성을 생성 하 고 City 필드 &quot;메시지는&quot;필요 합니다. 응용 프로그램을 실행 하 고, 사용자 중 하나를 편집 하 고, `City` 필드의 선택을 취소 합니다. 필드에서 tab 키를 누르면 클라이언트 쪽 유효성 검사 오류 메시지가 표시 됩니다.

![도시 필요](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

마찬가지로, 클라이언트 유효성 검사 규칙의 각 매개 변수에 대해 양식이 `data-val-rulename-paramname=paramvalue`된 특성이 추가 됩니다. 예를 들어 `FirstName` 속성은 [Stringlength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성으로 주석이 지정 되 고 최소 길이는 3이 고 최대 길이는 8입니다. `length` 이라는 데이터 유효성 검사 규칙에는 매개 변수 이름 `max`와 매개 변수 값 8이 있습니다. 다음은 사용자 중 하나를 편집할 때 `FirstName` 필드에 대해 생성 되는 HTML을 보여 줍니다.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

클라이언트 유효성 검사에 대 한 자세한 내용은 ASP.NET MVC 3의 Wilson의 블로그 [에서 조심 스럽게 클라이언트 유효성 검사](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) 항목을 참조 하세요.

> [!NOTE]
> ASP.NET MVC 3 Beta에서는 때때로 클라이언트 쪽 유효성 검사를 시작 하기 위해 양식을 제출 해야 합니다. 최종 릴리스에서 변경 될 수 있습니다.

## <a name="creating-the-create-view"></a>만들기 뷰 만들기

다음 단계는 사용자가 새 사용자를 만들 수 있도록 하기 위해 `Create` 작업 메서드와 보기를 추가 하는 것입니다. 다음 `Create` 메서드를 홈 컨트롤러에 추가 합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

이전 단계에서와 같이 뷰를 추가 하지만 **뷰 콘텐츠** 를 **Create**로 설정 합니다.

![Create View](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

응용 프로그램을 실행 하 고, **만들기** 링크를 선택 하 고, 새 사용자를 추가 합니다. `Create` 메서드는 클라이언트 쪽 및 서버 쪽 유효성 검사를 자동으로 활용 합니다. &quot;이혜준 X&quot;와 같이 공백을 포함 하는 사용자 이름을 입력 해 봅니다. 사용자 이름 필드에서 tab 키를 누르면 클라이언트 쪽 유효성 검사 오류 (`White space is not allowed`)가 표시 됩니다.

## <a name="add-the-delete-method"></a>Delete 메서드 추가

자습서를 완료 하려면 home 컨트롤러에 다음 `Delete` 메서드를 추가 합니다.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

이전 단계에서와 같이 `Delete` 뷰를 추가 하 여 **뷰 콘텐츠** 를 **삭제**로 설정 합니다.

![보기 삭제](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

이제 유효성 검사를 사용 하는 간단 하지만 완전 한 기능의 ASP.NET MVC 3 응용 프로그램이 있습니다.
