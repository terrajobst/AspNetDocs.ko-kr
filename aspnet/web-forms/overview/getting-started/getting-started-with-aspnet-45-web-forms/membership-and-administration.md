---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
title: 멤버 자격 및 관리 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 732a2316-e49f-4f72-becd-0cd72f14457e
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
msc.type: authoredcontent
ms.openlocfilehash: ab00bc90bfc767d06e747be6dfb973245b5aae88
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615465"
---
# <a name="membership-and-administration"></a>멤버 자격 및 관리

[Erik Reitan](https://github.com/Erikre)

[정문 장난감 샘플 프로젝트 (C#) 다운로드](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013 for Web을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. [소스 코드를 포함 C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 하는 Visual Studio 2013 프로젝트는이 자습서 계열과 함께 사용할 수 있습니다.

이 자습서에서는 정문 장난감 샘플 응용 프로그램을 업데이트 하 여 사용자 지정 역할을 추가 하 고 ASP.NET Identity를 사용 하는 방법을 보여 줍니다. 또한 사용자 지정 역할이 있는 사용자가 웹 사이트에서 제품을 추가 하 고 제거할 수 있는 관리 페이지를 구현 하는 방법도 보여 줍니다.

[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md) 는 ASP.NET 웹 응용 프로그램을 빌드하는 데 사용 되는 멤버 자격 시스템이 며 ASP.NET 4.5에서 사용할 수 있습니다. ASP.NET Identity는 Visual Studio 2013 Web Forms 프로젝트 템플릿에서 사용 되며 [ASP.NET MVC](../../../../mvc/index.md), [ASP.NET Web API](../../../../web-api/index.md)및 [ASP.NET 단일 페이지 응용 프로그램](../../../../single-page-application/index.md)에 대 한 템플릿을 사용 합니다. 빈 웹 응용 프로그램으로 시작 하는 경우 NuGet을 사용 하 여 ASP.NET Identity 시스템을 설치할 수도 있습니다. 그러나이 자습서 시리즈에서는 ASP.NET Identity 시스템을 포함 하는 **Web Forms**projecttemplate을 사용 합니다. ASP.NET Identity를 사용 하면 사용자 관련 프로필 데이터를 응용 프로그램 데이터와 쉽게 통합할 수 있습니다. 또한 ASP.NET Identity를 사용 하 여 응용 프로그램의 사용자 프로필에 대 한 지 속성 모델을 선택할 수 있습니다. Windows Azure Storage 테이블과 같은 *Nosql* 데이터 저장소를 포함 하 여 SQL Server 데이터베이스 또는 다른 데이터 저장소에 데이터를 저장할 수 있습니다.

이 자습서는 정문 장난감 tutorial 시리즈의 "PayPal Checkout and 결제" 라는 이전 자습서를 기반으로 합니다.

## <a name="what-youll-learn"></a>학습 내용:

- 코드를 사용 하 여 사용자 지정 역할 및 사용자를 응용 프로그램에 추가 하는 방법입니다.
- 관리 폴더 및 페이지에 대 한 액세스를 제한 하는 방법
- 사용자 지정 역할에 속한 사용자에 대 한 탐색을 제공 하는 방법입니다.
- 모델 바인딩을 사용 하 여 [DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx) 컨트롤을 제품 범주로 채우는 방법
- [FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx) 컨트롤을 사용 하 여 웹 응용 프로그램에 파일을 업로드 하는 방법입니다.
- 유효성 검사 컨트롤을 사용 하 여 입력 유효성 검사를 구현 하는 방법입니다.
- 응용 프로그램에서 제품을 추가 및 제거 하는 방법입니다.

## <a name="these-features-are-included-in-the-tutorial"></a>이러한 기능은 자습서에 포함 되어 있습니다.

- ASP.NET ID
- 구성 및 권한 부여
- 모델 바인딩
- 조심 스럽게 유효성 검사

ASP.NET Web Forms 멤버 자격 기능을 제공 합니다. 기본 템플릿을 사용 하 여 응용 프로그램을 실행할 때 즉시 사용할 수 있는 기본 제공 멤버 자격 기능을 사용할 수 있습니다. 이 자습서에서는 ASP.NET Identity를 사용 하 여 사용자 지정 역할을 추가 하 고 해당 역할에 사용자를 할당 하는 방법을 보여 줍니다. 관리 폴더에 대 한 액세스를 제한 하는 방법을 알아봅니다. 사용자 지정 역할이 있는 사용자가 제품을 추가 및 제거 하 고 제품을 추가한 후 미리 볼 수 있도록 하는 페이지를 관리 폴더에 추가 합니다.

## <a name="adding-a-custom-role"></a>사용자 지정 역할 추가

ASP.NET Identity를 사용 하 여 사용자 지정 역할을 추가 하 고 코드를 사용 하 여 해당 역할에 사용자를 할당할 수 있습니다.

1. **솔루션 탐색기**에서 *논리* 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 클래스를 만듭니다.
2. 새 클래스의 이름을 *RoleActions.cs*로 합니다.
3. 다음과 같이 표시 되도록 코드를 수정 합니다.  

    [!code-csharp[Main](membership-and-administration/samples/sample1.cs?highlight=8)]
4. **솔루션 탐색기**에서 *Global.asax.cs* 파일을 엽니다.
5. 다음과 같이 표시 되도록 노란색으로 강조 표시 된 코드를 추가 하 여 *Global.asax.cs* 파일을 수정 합니다.  

    [!code-csharp[Main](membership-and-administration/samples/sample2.cs?highlight=11,26-28)]
6. `AddUserAndRole` 빨간색으로 밑줄이 그어집니다. AddUserAndRole 코드를 두 번 클릭 합니다.  
   강조 표시 된 메서드의 시작 부분에 있는 "A" 문자에 밑줄이 표시 됩니다.
7. 문자 "A"를 마우스로 가리키고 `AddUserAndRole` 메서드에 대 한 메서드 스텁을 생성 하는 데 사용할 수 있는 UI를 클릭 합니다. 

    ![멤버 자격 및 관리-메서드 스텁 생성](membership-and-administration/_static/image1.png)
8. 다음 옵션을 클릭 합니다.  
    `Generate method stub for "AddUserAndRole" in "WingtipToys.Logic.RoleActions"`
9. *논리* 폴더에서 *RoleActions.cs* 파일을 엽니다.  
   `AddUserAndRole` 메서드가 클래스 파일에 추가 되었습니다.
10. `NotImplementedException`를 제거 하 고 노란색으로 강조 표시 된 코드를 추가 하 여 *RoleActions.cs* 파일을 수정 합니다. 그러면 다음과 같이 표시 됩니다.  

    [!code-csharp[Main](membership-and-administration/samples/sample3.cs?highlight=5-7,15-51)]

위의 코드는 먼저 멤버 자격 데이터베이스에 대 한 데이터베이스 컨텍스트를 설정 합니다. 또한 멤버 자격 데이터베이스는 *응용 프로그램\_Data* 폴더에 *.mdf* 파일로 저장 됩니다. 첫 번째 사용자가이 웹 응용 프로그램에 로그인 한 후에는이 데이터베이스를 볼 수 있습니다. 

> [!NOTE] 
> 
> 제품 데이터와 함께 멤버 자격 데이터를 저장 하려는 경우에는 위의 코드에서 제품 데이터를 저장 하는 데 사용한 것과 동일한 **DbContext** 를 사용 하는 것을 고려할 수 있습니다.

 *Internal* 키워드는 형식 (예: 클래스) 및 형식 멤버 (예: 메서드 또는 속성)에 대 한 액세스 한정자입니다. 내부 형식 또는 멤버는 동일한 어셈블리 *(.dll* 파일)에 포함 된 파일 내 에서만 액세스할 수 있습니다. 응용 프로그램을 빌드할 때 응용 프로그램을 실행할 때 실행 되는 코드를 포함 하는 어셈블리 파일 *(.dll*)이 만들어집니다. 

역할 관리를 제공 하는 `RoleStore` 개체는 데이터베이스 컨텍스트에 기반 하 여 생성 됩니다.

> [!NOTE] 
> 
> `RoleStore` 개체가 만들어지면 제네릭 `IdentityRole` 형식을 사용 합니다. 이는 `RoleStore` `IdentityRole` 개체만 포함할 수 있음을 의미 합니다. 또한 제네릭을 사용 하면 메모리의 리소스가 더 효율적으로 처리 됩니다.

그런 다음 `RoleManager` 개체는 방금 만든 `RoleStore` 개체를 기준으로 만들어집니다. `RoleManager` 개체는 `RoleStore`에 대 한 변경 내용을 자동으로 저장 하는 데 사용할 수 있는 역할 관련 API를 노출 합니다. `RoleManager` 코드에서 `<IdentityRole>` 제네릭 형식을 사용 하기 때문에 `IdentityRole` 개체만 포함할 수 있습니다.

`RoleExists` 메서드를 호출 하 여 멤버 자격 데이터베이스에 "canEdit" 역할이 있는지 여부를 확인 합니다. 그렇지 않으면 역할을 만듭니다.

`UserManager` 개체를 만드는 것은 `RoleManager` 컨트롤 보다 복잡 한 것 처럼 보이지만 거의 동일 합니다. 이는 여러 줄이 아닌 한 줄로 코딩 된 것입니다. 여기에서 전달 하는 매개 변수는 괄호 안에 포함 된 새 개체로 인스턴스화하는 것입니다.

다음으로 새 `ApplicationUser` 개체를 만들어 "canEditUser" 사용자를 만듭니다. 그런 다음 사용자를 성공적으로 만든 경우 사용자를 새 역할에 추가 합니다.

> [!NOTE] 
> 
> 오류 처리는이 자습서 시리즈의 뒷부분에 나오는 "ASP.NET 오류 처리" 자습서 중에 업데이트 됩니다.

다음 번에 응용 프로그램이 시작 되 면 "canEditUser" 라는 사용자가 응용 프로그램의 "canEdit" 라는 역할로 추가 됩니다. 이 자습서의 뒷부분에서 "canEditUser" 사용자로 로그인 하 여이 자습서에서 추가 하는 추가 기능을 표시 합니다. ASP.NET Identity에 대 한 API 세부 정보는 [Microsoft. n d m. Id 네임 스페이스](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx)를 참조 하세요. ASP.NET Identity 시스템을 초기화 하는 방법에 대 한 자세한 내용은 [AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs)를 참조 하세요.

### <a name="restricting-access-to-the-administration-page"></a>관리 페이지에 대 한 액세스 제한

정문 장난감 샘플 응용 프로그램을 사용 하면 익명 사용자와 로그인 한 사용자 모두 제품을 보고 구매할 수 있습니다. 그러나 사용자 지정 "canEdit" 역할이 있는 로그인 한 사용자는 제품을 추가 및 제거 하기 위해 제한 된 페이지에 액세스할 수 있습니다.

#### <a name="add-an-administration-folder-and-page"></a>관리 폴더 및 페이지 추가

다음에는 정문 장난감 sample 응용 프로그램의 사용자 지정 역할에 속하는 "canEditUser" 사용자에 대해 *Admin* 이라는 폴더를 만듭니다.

1. **솔루션 탐색기** 에서 프로젝트 이름 (**정문 장난감**)을 마우스 오른쪽 단추로 클릭 하 고 **새 폴더**&gt; **추가** -를 선택 합니다.
2. 새 폴더의 이름을 *Admin*으로 합니다.
3. *Admin* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가** -&gt; **새 항목**을 선택 합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
4. 왼쪽의 <strong>Visual C#</strong> -&gt; <strong>웹</strong> 템플릿 그룹을 선택 합니다. 중간 목록에서 <strong>마스터 페이지를 사용 하 여 Web Form</strong>을 선택 하 고 이름을 <em>adminpage .aspx</em><strong>로 지정한</strong> 다음 <strong>추가</strong>를 선택 합니다.
5. 마스터 페이지로 *site.master* 파일을 선택 하 고 **확인**을 선택 합니다.

#### <a name="add-a-webconfig-file"></a>Web.config 파일 추가

*관리자* 폴더에 *web.config 파일을* 추가 하면 폴더에 포함 된 페이지에 대 한 액세스를 제한할 수 있습니다.

1. *Admin* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** -&gt; **새 항목**을 선택 합니다.  
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 비주얼 C# 웹 템플릿 목록에서 가운데 목록에서 <strong>웹 구성 파일</strong>을 선택<strong>하 고</strong> <em>web.config의 기본</em>이름을 적용 한 다음 <strong>추가</strong>를 선택 합니다.
3. *Web.config* 파일의 기존 XML 콘텐츠를 다음으로 바꿉니다.  

    [!code-xml[Main](membership-and-administration/samples/sample4.xml)]

*Web.config 파일을* 저장 합니다. Web.config *파일은* 응용 프로그램의 "canedit" 역할에 속하는 사용자만 *Admin* 폴더에 포함 된 페이지에 액세스할 수 있도록 지정 합니다.

### <a name="including-custom-role-navigation"></a>사용자 지정 역할 탐색 포함

사용자 지정 "canEdit" 역할의 사용자가 응용 프로그램의 관리 섹션으로 이동할 수 있도록 하려면 *사이트 마스터* 페이지에 링크를 추가 해야 합니다. "CanEdit" 역할에 속한 사용자만 **관리자** 링크를 보고 관리 섹션에 액세스할 수 있습니다.

1. 솔루션 탐색기에서 *사이트 마스터* 페이지를 찾아 엽니다.
2. "CanEdit" 역할의 사용자에 대 한 링크를 만들려면 다음의 순서가 지정 되지 않은 목록 `<ul>` 요소에 노란색으로 강조 표시 된 태그를 추가 합니다. 그러면 목록이 다음과 같이 표시 됩니다.  

    [!code-html[Main](membership-and-administration/samples/sample5.html?highlight=2-3)]
3. *Site.Master.cs* 파일을 엽니다. 노란색으로 강조 표시 된 코드를 `Page_Load` 처리기에 추가 하 여 **관리** 링크를 "canedituser" 사용자 에게만 표시 되도록 합니다. `Page_Load` 처리기는 다음과 같이 표시 됩니다.   

    [!code-csharp[Main](membership-and-administration/samples/sample6.cs?highlight=3-6)]

페이지가 로드 되 면 코드는 로그인 한 사용자의 역할이 "canEdit" 인지 여부를 확인 합니다. 사용자가 "canEdit" 역할에 속하는 경우 *adminpage .aspx* 페이지에 대 한 링크를 포함 하는 span 요소가 표시 됩니다.

### <a name="enabling-product-administration"></a>제품 관리 사용

지금까지 "canEdit" 역할을 만들고 "canEditUser" 사용자, 관리 폴더 및 관리 페이지를 추가 했습니다. 관리 폴더 및 페이지에 대 한 액세스 권한을 설정 하 고 응용 프로그램에 "canEdit" 역할의 사용자에 대 한 탐색 링크를 추가 했습니다. 다음으로, "canEdit" 역할을 사용 하 여 사용자가 제품을 추가 및 제거할 수 있도록 하는 *AdminPage.aspx.cs* 코드에 태그를 추가 하 고 *이 페이지에* 코드를 추가 합니다.

1. **솔루션 탐색기**에서 *Admin* 폴더의 *adminpage* 파일을 엽니다.
2. 기존 태그를 다음으로 바꿉니다.  

    [!code-aspx[Main](membership-and-administration/samples/sample7.aspx)]
3. 그런 다음 *AdminPage.aspx.cs* 를 마우스 오른쪽 단추로 클릭 하 고 **코드 보기** *를 클릭* 하 여 코드 숨김으로 파일을 엽니다.
4. *AdminPage.aspx.cs* 코드 숨김으로 파일의 기존 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](membership-and-administration/samples/sample8.cs)]

*AdminPage.aspx.cs* 코드 숨김으로 입력 한 코드에서 `AddProducts` 라는 클래스는 데이터베이스에 제품을 추가 하는 실제 작업을 수행 합니다. 이 클래스는 아직 존재 하지 않으므로 지금 만듭니다.

1. **솔루션 탐색기**에서 *논리* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가** -&gt; **새 항목**을 선택 합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 왼쪽의 **Visual C#**  -&gt; **코드** 템플릿 그룹을 선택 합니다. 그런 다음 가운데 목록에서 **클래스**를 선택 하 고 이름을 *AddProducts.cs*로 지정한 다음   
   새 클래스 파일이 표시 됩니다.
3. 기존 코드를 다음으로 바꿉니다.  

    [!code-csharp[Main](membership-and-administration/samples/sample9.cs)]

*Adminpage .aspx* 페이지에서는 "canedit" 역할에 속한 사용자가 제품을 추가 및 제거할 수 있습니다. 새 제품을 추가 하면 해당 제품에 대 한 세부 정보가 유효성 검사 되 고 데이터베이스에 입력 됩니다. 새 제품은 웹 응용 프로그램의 모든 사용자가 즉시 사용할 수 있습니다.

#### <a name="unobtrusive-validation"></a>조심 스럽게 유효성 검사

사용자가 *adminpage .aspx* 페이지에 제공 하는 제품 세부 정보는 유효성 검사 컨트롤 (`RequiredFieldValidator` 및 `RegularExpressionValidator`)을 사용 하 여 유효성이 검사 됩니다. 이러한 컨트롤은 자동으로 방해 하지 않는 유효성 검사를 사용 합니다. 잘못 된 유효성 검사를 통해 유효성 검사 컨트롤이 클라이언트 쪽 유효성 검사 논리에 JavaScript를 사용할 수 있습니다. 즉, 페이지에서 유효성을 검사할 서버에 대 한 이동이 필요 하지 않습니다. 기본적으로 다음 구성 설정에 따라 *web.config 파일에* 포함 되지 않은 유효성 검사가 포함 됩니다.

[!code-xml[Main](membership-and-administration/samples/sample10.xml)]

#### <a name="regular-expressions"></a>정규식을 참조하세요.

**RegularExpressionValidator** 컨트롤을 사용 하 여 *adminpage .aspx* 페이지의 제품 가격에 대 한 유효성을 검사 합니다. 이 컨트롤은 연결 된 입력 컨트롤의 값 ("Add제품 가격" 텍스트 상자)이 정규식으로 지정 된 패턴과 일치 하는지 여부를 확인 합니다. 정규식은 패턴 일치 표기법으로, 특정 문자 패턴을 신속 하 게 찾고 일치 시킬 수 있습니다. **RegularExpressionValidator** 컨트롤에는 아래와 같이 가격 입력의 유효성을 검사 하는 데 사용 되는 정규식을 포함 하는 `ValidationExpression` 라는 속성이 포함 되어 있습니다.

[!code-aspx[Main](membership-and-administration/samples/sample11.aspx)]

#### <a name="fileupload-control"></a>FileUpload 컨트롤

입력 및 유효성 검사 컨트롤 외에도 **FileUpload** 컨트롤을 *adminpage .aspx* 페이지에 추가 했습니다. 이 컨트롤은 파일을 업로드 하는 기능을 제공 합니다. 이 경우 이미지 파일만 업로드할 수 있습니다. 코드 숨김이 파일 (*AdminPage.aspx.cs*)에서 `AddProductButton`를 클릭 하면 코드는 **FileUpload** 컨트롤의 `HasFile` 속성을 확인 합니다. 컨트롤에 파일이 있고 파일 확장명을 기반으로 하는 파일 형식이 허용 되는 *경우 이미지는 이미지 폴더와* 응용 프로그램의 *images/엄지* 화면 폴더에 저장 됩니다.

#### <a name="model-binding"></a>모델 바인딩

이 자습서 시리즈의 앞부분에서는 모델 바인딩을 사용 하 여 **ListView** 컨트롤, **양식 보기** 컨트롤, **GridView** 컨트롤 및 **DetailView** 컨트롤을 채웁니다. 이 자습서에서는 모델 바인딩을 사용 하 여 **DropDownList** 컨트롤을 제품 범주 목록으로 채웁니다.

*Adminpage .aspx* 파일에 추가 된 태그에는 `DropDownAddCategory`이라는 **DropDownList** 컨트롤이 포함 되어 있습니다.

[!code-aspx[Main](membership-and-administration/samples/sample12.aspx)]

모델 바인딩을 사용 하 여 `ItemType` 특성 및 `SelectMethod` 특성을 설정 하 여이 **DropDownList** 을 채웁니다. `ItemType` 특성은 컨트롤을 채울 때 `WingtipToys.Models.Category` 형식을 사용 하도록 지정 합니다. 이 자습서 시리즈의 시작 부분에서 `Category` 클래스 (아래 참조)를 만들어이 유형을 정의 했습니다. `Category` 클래스는 *Category.cs* 파일 내의 *모델* 폴더에 있습니다.

[!code-csharp[Main](membership-and-administration/samples/sample13.cs)]

**DropDownList** 컨트롤의 `SelectMethod` 특성은 코드 숨김이 파일 (*AdminPage.aspx.cs*)에 포함 된 `GetCategories` 메서드 (아래 참조)를 사용 하도록 지정 합니다.

[!code-csharp[Main](membership-and-administration/samples/sample14.cs)]

이 메서드는 `Category` 형식에 대해 쿼리를 평가 하는 데 `IQueryable` 인터페이스를 사용 하도록 지정 합니다. 반환 된 값은 페이지 (*adminpage*) 태그의 **DropDownList** 를 채우는 데 사용 됩니다.

목록의 각 항목에 대해 표시 되는 텍스트는 `DataTextField` 특성을 설정 하 여 지정 합니다. `DataTextField` 특성은 위에 표시 된 `Category` 클래스의 `CategoryName`를 사용 하 여 **DropDownList** 컨트롤의 각 범주를 표시 합니다. **DropDownList** 컨트롤에서 항목을 선택할 때 전달 되는 실제 값은 `DataValueField` 특성을 기반으로 합니다. `DataValueField` 특성은 `Category` 클래스에서 정의로 `CategoryID` 설정 됩니다 (위에 표시 됨).

### <a name="how-the-application-will-work"></a>응용 프로그램의 작동 방법

"CanEdit" 역할에 속하는 사용자가 페이지를 처음으로 탐색 하는 경우에는 `DropDownAddCategory`**DropDownList** 컨트롤이 위에서 설명한 대로 채워집니다. 또한 `DropDownRemoveProduct`**DropDownList** 컨트롤은 동일한 방법을 사용 하 여 제품으로 채워집니다. "CanEdit" 역할에 속하는 사용자는 범주 유형을 선택 하 고 제품 세부 정보 (**이름**, **설명**, **가격**및 **이미지 파일**)를 추가 합니다. "CanEdit" 역할에 속한 사용자가 **제품 추가** 단추를 클릭 하면 `AddProductButton_Click` 이벤트 처리기가 트리거됩니다. 코드 숨김이 파일 (*AdminPage.aspx.cs*)에 있는 `AddProductButton_Click` 이벤트 처리기는 이미지 파일이 허용 되는 파일 형식 *(.gif*, *.png*, *.jpeg*또는 *.jpg*)과 일치 하는지 확인 합니다. 그런 다음 이미지 파일은 정문 장난감 샘플 응용 프로그램의 폴더에 저장 됩니다. 그런 다음 새 제품이 데이터베이스에 추가 됩니다. 새 제품을 추가 하기 위해 `AddProducts` 클래스의 새 인스턴스가 만들어지고 이름이 지정 됩니다. `AddProducts` 클래스에는 `AddProduct`라는 메서드가 있으며 products 개체는이 메서드를 호출 하 여 데이터베이스에 제품을 추가 합니다.

[!code-csharp[Main](membership-and-administration/samples/sample15.cs)]

코드가 데이터베이스에 새 제품을 성공적으로 추가 하면 `ProductAction=add`쿼리 문자열 값을 사용 하 여 페이지가 다시 로드 됩니다.

[!code-csharp[Main](membership-and-administration/samples/sample16.cs)]

페이지가 다시 로드 되 면 쿼리 문자열이 URL에 포함 됩니다. 페이지를 다시 로드 하면 "canEdit" 역할에 속한 사용자가 *adminpage .aspx* 페이지의 **DropDownList** 컨트롤에서 즉시 업데이트를 볼 수 있습니다. 또한 URL을 사용 하 여 쿼리 문자열을 포함 하면 페이지에 "canEdit" 역할에 속하는 사용자에 게 성공 메시지가 표시 될 수 있습니다.

*Adminpage .aspx* 페이지가 다시 로드 되 면 `Page_Load` 이벤트가 호출 됩니다.

[!code-csharp[Main](membership-and-administration/samples/sample17.cs)]

`Page_Load` 이벤트 처리기는 쿼리 문자열 값을 확인 하 고 성공 메시지를 표시할지 여부를 결정 합니다.

## <a name="running-the-application"></a>응용 프로그램 실행

지금 응용 프로그램을 실행 하 여 쇼핑 카트에 항목을 추가, 삭제 및 업데이트할 수 있는 방법을 확인할 수 있습니다. 쇼핑 카트 합계는 쇼핑 카트에 있는 모든 항목의 총 비용을 반영 합니다.

1. 솔루션 탐색기에서 **F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.  
   브라우저가 열리고 *default.aspx 페이지가 표시 됩니다.*
2. 페이지 맨 위에 있는 **로그인** 링크를 클릭 합니다. 

    ![멤버 자격 및 관리-로그인 링크](membership-and-administration/_static/image2.png)

   *Login.aspx* 페이지가 표시 됩니다.
3. 다음 사용자 이름 및 암호를 사용 합니다.  
   사용자 이름: canEditUser@wingtiptoys.com  
   암호: Pa $ $word 1 

    ![멤버 자격 및 관리-로그인 페이지](membership-and-administration/_static/image3.png)
4. 페이지 아래쪽의 **로그인** 단추를 클릭 합니다.
5. 다음 페이지의 맨 위에서 **관리자** 링크를 선택 하 여 *adminpage .aspx* 페이지로 이동 합니다. 

    ![멤버 자격 및 관리-관리자 링크](membership-and-administration/_static/image4.png)
6. 입력 유효성 검사를 테스트 하려면 제품 세부 정보를 추가 하지 않고 **제품 추가** 단추를 클릭 합니다. 

    ![멤버 자격 및 관리-관리 페이지](membership-and-administration/_static/image5.png)

   필수 필드 메시지가 표시 됩니다.
7. 새 제품에 대 한 세부 정보를 추가한 다음 **제품 추가** 단추를 클릭 합니다. 

    ![멤버 자격 및 관리-제품 추가](membership-and-administration/_static/image6.png)
8. 위쪽 탐색 메뉴에서 **제품** 을 선택 하 여 추가한 새 제품을 확인 합니다. 

    ![멤버 자격 및 관리-새 제품 표시](membership-and-administration/_static/image7.png)
9. **관리자** 링크를 클릭 하 여 관리 페이지로 돌아갑니다.
10. 페이지의 **제품 제거** 섹션에서 **DropDownListBox**에 추가한 새 제품을 선택 합니다.
11. 응용 프로그램에서 새 제품을 제거 하려면 **제품 제거** 단추를 클릭 합니다. 

    ![멤버 자격 및 관리-제품 제거](membership-and-administration/_static/image8.png)
12. 상단 탐색 메뉴 **에서 제품을 선택 하** 여 제품이 제거 되었는지 확인 합니다.
13. 존재 하는 관리 모드로 **로그 오프** 를 클릭 합니다.   
    위쪽 탐색 창에는 더 이상 **관리** 메뉴 항목이 표시 되지 않습니다.

## <a name="summary"></a>요약

이 자습서에서는 사용자 지정 역할 및 사용자 지정 역할에 속하는 사용자를 추가 하 고, 관리 폴더와 페이지에 대 한 제한 된 액세스 권한을 추가 하 고, 사용자 지정 역할에 속하는 사용자에 대 한 탐색을 제공 했습니다. 모델 바인딩을 사용 하 여 **DropDownList** 컨트롤을 데이터로 채웁니다. **FileUpload** 컨트롤 및 유효성 검사 컨트롤을 구현 했습니다. 또한 데이터베이스에서 제품을 추가 및 제거 하는 방법을 배웠습니다. 다음 자습서에서는 ASP.NET 라우팅을 구현 하는 방법에 대해 알아봅니다.

## <a name="additional-resources"></a>추가 리소스

[Web.config-authorization 요소](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)  
[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)  
[멤버 자격, OAuth 및 SQL Database를 사용 하 여 Azure 웹 사이트에 보안 ASP.NET Web Forms 앱 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure-무료 평가판](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [이전](checkout-and-payment-with-paypal.md)
> [다음](url-routing.md)
