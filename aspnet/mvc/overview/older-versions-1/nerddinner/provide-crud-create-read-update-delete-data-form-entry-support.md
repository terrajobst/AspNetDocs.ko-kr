---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원 |을 제공 합니다. Microsoft Docs
author: microsoft
description: 5 단계에서는 Dinners 편집, 만들기 및 삭제에 대 한 지원을 사용 하도록 설정 하 여 DinnersController 클래스를 추가로 수행 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: b3123af9a1477bc496a0d229d628510fc202b6d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468917"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>CRUD(만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원 제공

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 5 단계입니다.
> 
> 5 단계에서는 Dinners 편집, 만들기 및 삭제에 대 한 지원을 사용 하도록 설정 하 여 DinnersController 클래스를 추가로 수행 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner 5 단계: 양식 만들기, 업데이트, 삭제 시나리오

컨트롤러 및 보기를 소개 하 고이를 사용 하 여 Dinners on 사이트에 대 한 목록/세부 정보 환경을 구현 하는 방법을 살펴보았습니다. 다음 단계에서는 Dinners를 사용 하 여이 클래스를 추가 하 고 편집, 만들기 및 삭제를 지원 합니다.

### <a name="urls-handled-by-dinnerscontroller"></a>DinnersController에서 처리 하는 Url

이전에는 두 가지 Url ( */Dinners* 및 */Dinners/Details/[id])* 에 대 한 지원을 구현 하는 작업 메서드를 dinnerscontroller에 추가 했습니다.

| **URL** | **동사** | **용도** |
| --- | --- | --- |
| */Dinners/* | GET | 예정 된 dinners의 HTML 목록을 표시 합니다. |
| */Dinners/Details/[id]* | GET | 특정 dinner a에 대 한 세부 정보를 표시 합니다. |

이제 */Dinners/Edit/[id]* , */Dinners/Create*및 */Dinners/Delete/[id]* 의 세 가지 추가 url을 구현 하는 작업 메서드를 추가 합니다. 이러한 Url을 사용 하면 기존 Dinners 편집, 새 Dinners 만들기, Dinners 삭제를 지원할 수 있습니다.

이러한 새 Url을 사용 하 여 HTTP GET 및 HTTP POST 동사 상호 작용을 모두 지원 합니다. 이러한 Url에 대 한 HTTP GET 요청은 데이터의 초기 HTML 보기 ("편집"의 경우 Dinner data로 채워진 폼, "만들기"의 경우 빈 폼, "delete"의 경우 삭제 확인 화면)를 표시 합니다. 이러한 Url에 대 한 HTTP POST 요청은 microsoft의 데이터베이스에서 데이터를 저장/업데이트/삭제 합니다.

| **URL** | **동사** | **용도** |
| --- | --- | --- |
| */Dinners/Edit/[id]* | GET | Dinner data로 채워진 편집 가능한 HTML 폼을 표시 합니다. |
| POST | 특정 Dinner a의 폼 변경 내용을 데이터베이스에 저장 합니다. |
| */Dinners/Create* | GET | 사용자가 새 Dinners를 정의할 수 있도록 하는 빈 HTML 양식을 표시 합니다. |
| POST | 새 Dinner를 만들고 데이터베이스에 저장 합니다. |
| */Dinners/Delete/[id]* | GET | 삭제 확인 화면을 표시 합니다. |
| POST | 데이터베이스에서 지정 된 dinner a를 삭제 합니다. |

### <a name="edit-support"></a>지원 편집

"편집" 시나리오를 구현 하는 것부터 시작 해 보겠습니다.

#### <a name="the-http-get-edit-action-method"></a>HTTP-GET 편집 동작 메서드입니다.

먼저 편집 작업 메서드의 HTTP "GET" 동작을 구현 합니다. 이 메서드는 */Dinners/Edit/[id]* URL이 요청 될 때 호출 됩니다. 구현은 다음과 같습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

위의 코드에서는 d Innerrepository를 사용 하 여 Dinner object를 검색 합니다. 그런 다음 Dinner object를 사용 하 여 뷰 템플릿을 렌더링 합니다. 명시적으로 템플릿 이름을 *view ()* 도우미 메서드에 전달 하지 않았으므로 규칙 기반 기본 경로를 사용 하 여 뷰 템플릿을 확인 합니다./Views/Dinners/Edit.aspx.

이제이 뷰 템플릿을 만들어 보겠습니다. 편집 메서드를 마우스 오른쪽 단추로 클릭 하 고 "뷰 추가" 상황에 맞는 메뉴 명령을 선택 하 여이 작업을 수행 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

"뷰 추가" 대화 상자 내에서 Dinner object를 뷰 템플릿에 모델로 전달 하 고 "Edit" 템플릿을 자동으로 스 캐 폴드 선택 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

"추가" 단추를 클릭 하면 Visual Studio는 "\Views\Dinners" 디렉터리 내에 새 ".aspx" 파일 보기 템플릿 파일을 추가 합니다. 또한 아래와 같이 초기 "Edit" 스 캐 폴드 구현으로 채워진 코드 편집기 내에서 새로운 "Edit .aspx" 보기 템플릿을 엽니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

생성 된 기본 "edit" 스 캐 폴드를 몇 가지 변경 하 고 편집 뷰 템플릿을 업데이트 하 여 아래 콘텐츠를 포함 하도록 합니다 (노출 하지 않으려는 일부 속성을 제거 함).

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

응용 프로그램을 실행 하 고 *"/Dinners/Edit/1"* URL을 요청 하면 다음 페이지가 표시 됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

뷰에서 생성 된 HTML 태그는 아래와 같습니다. 표준 HTML 이며, "저장" &lt;입력 형식 = "제출"/&gt; 단추가 푸시되 면 */Dinners/Edit/1* URL에 HTTP POST를 수행 하는 &lt;form&gt; 요소가 있습니다. HTML &lt;입력 형식 = "text"/&gt; 요소가 편집 가능한 각 속성에 대해 출력 되었습니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.beginform () 및 Html. TextBox () Html 도우미 메서드

"ValidationSummary (), Html.beginform (), Html. 텍스트 상자 () 및 Html. ValidationMessage ()를 사용 하 여" .aspx 편집 "보기 템플릿을 사용 합니다. 이러한 도우미 메서드는 미국의 HTML 태그를 생성 하는 것 외에도 기본 제공 오류 처리 및 유효성 검사를 지원 합니다.

##### <a name="htmlbeginform-helper-method"></a>Html.beginform () 도우미 메서드

Html.beginform () 도우미 메서드는 태그에서 HTML &lt;form&gt; 요소를 출력 하는 것입니다. 이 메서드를 사용 하는 경우 편집 .aspx 보기 템플릿에서 C# "using" 문을 적용 하 고 있음을 알 수 있습니다. 여는 중괄호는 콘텐츠&gt; &lt;폼의 시작을 나타내고, 닫는 중괄호는 &lt;&gt; 요소의 끝을 나타냅니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

또는 이와 같은 시나리오에서 "using" 문을 사용 하지 않는 경우 동일한 작업을 수행 하는 Html.beginform () 및 .Html () 조합을 사용할 수 있습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

매개 변수 없이 Html.beginform ()를 호출 하면이 메서드는 현재 요청의 URL에 대해 HTTP POST를 수행 하는 form 요소를 출력 합니다. 이렇게 하면 편집 뷰에서 *&lt;form action = "/Dinners/Edit/1" method = "post"&gt;* 요소가 생성 됩니다. 다른 URL에 게시 하려는 경우 Html.beginform ()에 명시적 매개 변수를 전달할 수도 있습니다.

##### <a name="htmltextbox-helper-method"></a>Html. TextBox () 도우미 메서드

편집 .aspx 뷰에서는 Html. TextBox () 도우미 메서드를 사용 하 &lt;입력 형식 = "text"/&gt; 요소를 출력 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

위의 Html. TextBox () 메서드는 단일 매개 변수를 사용 합니다 .이 매개 변수는 &lt;입력 형식 = "text"/&gt; 요소의 id/name 특성을 모두 지정 하 고 텍스트 상자 값을 채울 모델 속성을 지정 합니다. 예를 들어 편집 뷰에 전달 된 Dinner object에는 "Title" 속성 값 ".NET 퓨처"가 있으며 Html. TextBox ("Title") 메서드 호출 출력: *&lt;입력 id = "title" name = "title" type = "text" value = ".Net 퓨처"/&gt;* .

또는 첫 번째 Html. TextBox () 매개 변수를 사용 하 여 요소의 id/이름을 지정한 다음 두 번째 매개 변수로 사용할 값을 명시적으로 전달할 수 있습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

일반적으로 출력 되는 값에 대 한 사용자 지정 서식 지정을 수행 하는 것이 좋습니다. String.format () 정적 메서드 기본 제공 .NET은 이러한 시나리오에 유용 합니다. 편집 .aspx 뷰 템플릿에서는이를 사용 하 여 시간에 대 한 초를 표시 하지 않도록 EventDate 값 (DateTime 형식)의 형식을 지정 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

Html. TextBox ()의 세 번째 매개 변수는 선택적으로 추가 HTML 특성을 출력 하는 데 사용할 수 있습니다. 아래 코드 조각은 추가 크기 = "30" 특성과 class = "mycssclass" 특성을 &lt;입력 형식 = "text"/&gt; 요소에 렌더링 하는 방법을 보여 줍니다. "@" character because "클래스"를 사용 하 여 클래스 특성의 이름을 이스케이프 하는 방법은의 C#예약 된 키워드입니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>HTTP POST 편집 작업 메서드 구현

이제 HTTP-GET 버전의 편집 작업 메서드가 구현 되었습니다. 사용자가 */Dinners/Edit/1* URL을 요청 하면 다음과 같은 HTML 페이지가 표시 됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

"저장" 단추를 누르면 */Dinners/Edit/1* URL에 양식이 게시 되 고 HTTP post 동사를 사용 하 여 HTML &lt;입력&gt; 폼 값이 전송 됩니다. 이제 Dinner를 저장 하는 작업을 처리 하는 edit 작업 메서드의 HTTP POST 동작을 구현 해 보겠습니다.

먼저 오버 로드 된 "Edit" 작업 메서드를 ' AcceptVerbs ' 특성이 있는 "AcceptVerbs" 특성을 포함 하는이를 시작 합니다 .이 메서드는 HTTP POST 시나리오를 처리 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

[AcceptVerbs] 특성이 오버 로드 된 작업 메서드에 적용 되는 경우 ASP.NET MVC는 들어오는 HTTP 동사에 따라 적절 한 작업 메서드에 대 한 디스패치 요청을 자동으로 처리 합니다. */Dinners/Edit/[id]* url에 대 한 http POST 요청은 위의 edit 메서드로 이동 하 고, */Dinners/Edit/[id]* url에 대 한 다른 모든 http 동사 요청은 구현 된 첫 번째 편집 메서드로 이동 합니다 (`[AcceptVerbs]` 특성이 없음).

| **측면 토픽: HTTP 동사를 통해 구분 하는 이유** |
| --- |
| 요청은 HTTP 동사를 통해 단일 URL을 사용 하 고 해당 동작을 차별화 하는 이유를 알 수 있습니다. 편집 변경 내용을 로드 하 고 저장 하는 두 개의 별도 Url을 포함 하지 않는 이유는 무엇 인가요? 예:/Dinners/Edit/[id]를 표시 하 여 초기 양식과/Dinners/Save/[id]를 표시 하 여 저장 하려면 폼 게시를 처리 하 시겠습니까? 두 개의 개별 Url을 게시 하는 경우의 단점은/Dinners/Save/2에 게시 한 다음 입력 오류로 인해 HTML 양식을 다시 표시 해야 하는 경우 최종 사용자가 브라우저의 주소 표시줄에/Dinners/Save/2 URL을 포함 하는 것입니다 (폼이 게시 된 URL 이기 때문). 최종 사용자가이 다시 표시 페이지에 브라우저 즐겨찾기 목록에 책갈피를 추가 하거나 URL을 복사/붙여넣기 하 여 친구에 게 전자 메일을 보내면 해당 URL이 post 값에 의존 하기 때문에 나중에 작동 하지 않는 URL이 저장 됩니다. 단일 URL (예:/Dinners/Edit/[id])을 노출 하 고 HTTP 동사로 처리 하는 것을 구분 하 여 최종 사용자가 편집 페이지에 책갈피를 제공 하거나 URL을 다른 사용자에 게 보낼 수 있습니다. |

#### <a name="retrieving-form-post-values"></a>폼 게시 값 검색

HTTP POST "Edit" 메서드 내에서 게시 된 양식 매개 변수에 액세스할 수 있는 여러 가지 방법이 있습니다. 간단한 방법 중 하나는 컨트롤러 기본 클래스에서 Request 속성을 사용 하 여 양식 컬렉션에 액세스 하 고 게시 된 값을 직접 검색 하는 것입니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

특히 오류 처리 논리를 추가한 후에는 위의 접근 방법이 약간 자세한 정보를 표시 합니다.

이 시나리오에 대 한 더 나은 방법은 컨트롤러 기본 클래스에서 기본 제공 *UpdateModel ()* 도우미 메서드를 활용 하는 것입니다. 들어오는 폼 매개 변수를 사용 하 여 전달 하는 개체의 속성을 업데이트 하는 것을 지원 합니다. 리플렉션을 사용 하 여 개체의 속성 이름을 확인 한 다음 클라이언트에서 제출한 입력 값을 기반으로 값을 자동으로 변환 하 고 값을 할당 합니다.

UpdateModel () 메서드를 사용 하 여 다음 코드를 사용 하 여 HTTP-사후 편집 작업을 단순화할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

이제 */Dinners/Edit/1* URL을 방문 하 여 저녁의 제목을 변경할 수 있습니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

"저장" 단추를 클릭 하면 편집 작업에 폼 게시를 수행 하 고 업데이트 된 값이 데이터베이스에 유지 됩니다. 그러면 Dinner (새로 저장 된 값이 표시 됨)에 대 한 세부 정보 URL로 리디렉션됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>편집 오류 처리

현재 HTTP POST 구현은 오류가 발생 한 경우를 제외 하 고는 정상적으로 작동 합니다.

사용자가 양식을 편집 하는 실수를 하는 경우 양식이 수정 하도록 안내 하는 정보 오류 메시지와 함께 다시 표시 되는지 확인 해야 합니다. 여기에는 최종 사용자가 잘못 된 입력을 게시 하는 경우 (예: 잘못 된 날짜 문자열)와 입력 형식이 올바르지만 비즈니스 규칙 위반이 발생 하는 경우가 포함 됩니다. 오류가 발생 하면 폼은 사용자가 원래 입력 한 입력 데이터를 그대로 유지 하 여 변경 내용을 수동으로 다시 채워야 하지 않도록 해야 합니다. 이 프로세스는 양식이 성공적으로 완료 될 때까지 필요한 횟수 만큼 반복 됩니다.

ASP.NET MVC에는 오류 처리 및 양식 다시 표시를 용이 하 게 하는 몇 가지 유용한 기본 제공 기능이 포함 되어 있습니다. 이러한 기능을 작동 하는 것을 확인 하려면 다음 코드를 사용 하 여 편집 작업 메서드를 업데이트 해 보겠습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

위의 코드는 이제 작업에 대 한 try/catch 오류 처리 블록을 래핑하는 점을 제외 하 고 이전 구현과 비슷합니다. UpdateModel ()를 호출할 때 예외가 발생 하거나, (모델 내에서 규칙 위반으로 인해 저장 하려는 Dinner object가 잘못 된 경우 예외를 발생 시키는 경우 예외를 발생 시키는), 오류 처리 블록이 catch 됩니다. 실행할. 이 내에서 저녁 개체에 존재 하는 모든 규칙 위반을 반복 하 여 해당 개체를 ModelState 개체에 추가 합니다. (곧 논의 될 예정입니다.) 그런 다음 뷰를 다시 표시 합니다.

이 작업을 확인 하려면 응용 프로그램을 다시 실행 하 고 Dinner a를 편집한 다음 빈 제목, EventDate "위조"로 변경 하 고 country 값이 USA 인 영국 전화 번호를 사용 합니다. "저장" 단추를 누르면 HTTP POST Edit 메서드는 Dinner (오류가 있으므로)를 저장할 수 없으며 다음 양식을 다시 표시 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

응용 프로그램에는 훌륭한 오류 환경이 있습니다. 잘못 된 입력을 포함 하는 텍스트 요소는 빨간색으로 강조 표시 되 고 유효성 검사 오류 메시지는 최종 사용자에 게 표시 됩니다. 또한 폼은 사용자가 원래 입력 한 입력 데이터를 유지 하므로 모든 항목을 다시 쓸 필요가 없습니다.

그렇다면 어떻게 해야 하나요? 제목, EventDate 및 연락처 전화 텍스트 상자를 빨간색으로 강조 표시 하 고 원래 입력 된 사용자 값을 출력 하는 방법은 무엇 인가요? 그리고 오류 메시지가 위쪽의 목록에 어떻게 표시 되나요? 좋은 소식은 입력 유효성 검사 및 오류 처리 시나리오를 쉽게 해 주는 기본 제공 ASP.NET MVC 기능 중 일부를 사용 했기 때문입니다.

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>ModelState 및 유효성 검사 HTML 도우미 메서드 이해

컨트롤러 클래스에는 뷰에 전달 되는 모델 개체에 오류가 있음을 나타내는 방법을 제공 하는 "ModelState" 속성 컬렉션이 있습니다. ModelState 컬렉션 내의 오류 항목은 문제가 있는 모델 속성의 이름 (예: "제목", "EventDate" 또는 "연락처 전화")을 식별 하 고 사용자에 게 친숙 한 오류 메시지를 지정할 수 있도록 허용 합니다 (예: "제목 필요").

*UpdateModel ()* 도우미 메서드는 모델 개체의 속성에 양식 값을 할당 하는 동안 오류가 발생할 때 modelstate 컬렉션을 자동으로 채웁니다. 예를 들어 Dinner object의 EventDate 속성은 DateTime 형식입니다. UpdateModel () 메서드가 위의 시나리오에서 문자열 값 "위조"를 할당할 수 없는 경우 UpdateModel () 메서드는 해당 속성에서 할당 오류가 발생 했음을 나타내는 항목을 ModelState 컬렉션에 추가 했습니다.

또한 개발자는 "catch" 오류 처리 블록 내에서 수행 하는 것과 같은 방식으로 ModelState 컬렉션에 오류 항목을 명시적으로 추가 하는 코드를 작성할 수 있습니다 .이 블록의 활성 규칙 위반을 기반으로 하는 항목이 있는 저녁 개체:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>ModelState와 Html 도우미 통합

Html 도우미 메서드 Html. TextBox ()-출력을 렌더링할 때 ModelState 컬렉션을 확인 합니다. 항목에 대 한 오류가 있으면 사용자가 입력 한 값과 CSS 오류 클래스를 렌더링 합니다.

예를 들어, "편집" 뷰에서는 Html. TextBox () 도우미 메서드를 사용 하 여 Dinner object의 EventDate를 렌더링 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

오류가 발생 한 시나리오에서 뷰가 렌더링 되 면 Html. TextBox () 메서드는 ModelState 컬렉션을 확인 하 여 Dinner object의 "EventDate" 속성과 관련 된 오류가 있는지 확인 합니다. 전송 된 사용자 입력 ("위조")을 값으로 렌더링 한 오류가 발생 한 것을 확인 하 고, 생성 된 &lt;입력 형식 = "textbox"/&gt; 태그에 css 오류 클래스를 추가 했습니다.

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

Css 오류 클래스의 모양을 사용자 지정 하 여 원하는 대로 표시할 수 있습니다. 기본 CSS 오류 클래스 – "입력-유효성 검사-오류"는 *\content\site.xml* 스타일 시트에 정의 되어 있으며 아래와 같습니다.

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

이 CSS 규칙은 다음과 같이 잘못 된 입력 요소를 강조 표시 한 것입니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Html.ValidationMessage() Helper Method

Html. ValidationMessage () 도우미 메서드를 사용 하 여 특정 모델 속성과 연결 된 ModelState 오류 메시지를 출력할 수 있습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

위의 코드 출력: *&lt;span class = "필드-유효성 검사-오류"&gt; 값 ' o n s '가 잘못 된&lt;/span&gt;*

또한 Html. ValidationMessage () 도우미 메서드는 개발자가 표시 되는 오류 텍스트 메시지를 재정의할 수 있도록 하는 두 번째 매개 변수를 지원 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

위의 코드 출력: *&lt;span class = "필드-유효성 검사-오류"&gt;\*&lt;/span&gt;* 는 eventdate 속성에 오류가 있을 때 기본 오류 텍스트 대신.

##### <a name="htmlvalidationsummary-helper-method"></a>Html.ValidationSummary() Helper Method

ValidationSummary () 도우미 메서드를 사용 하 여 ModelState 컬렉션에 있는 모든 자세한 오류 메시지의 &lt;l/&gt;&lt;/ul&gt; 목록과 함께 &lt;ul&gt;요약 오류 메시지를 렌더링할 수 있습니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

ValidationSummary () 도우미 메서드는 선택적 문자열 매개 변수를 사용 합니다 .이 매개 변수는 자세한 오류 목록 위에 표시할 요약 오류 메시지를 정의 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

필요에 따라 CSS를 사용 하 여 오류 목록 모양을 재정의할 수 있습니다.

#### <a name="using-a-addruleviolations-helper-method"></a>AddRuleViolations 도우미 메서드 사용

초기 HTTP POST 편집 구현은 해당 catch 블록 내에서 foreach 문을 사용 하 여 Dinner object의 규칙 위반을 반복 하 고 컨트롤러의 ModelState 컬렉션에 추가 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

ASP.NET MVC ModelStateDictionary 클래스에 도우미 메서드를 추가 하는 "ControllerHelpers" 클래스를 해당 프로젝트 내에 추가 하 여이 코드를 조금 더 깔끔하고 만들 수 있습니다. 이 확장 메서드는 RuleViolation 오류 목록으로 ModelStateDictionary을 채우는 데 필요한 논리를 캡슐화 할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

그런 다음이 확장 메서드를 사용 하 여이 확장 메서드를 사용 하 여 Dinner Rule 위반으로 ModelState 컬렉션을 채우는 HTTP POST 편집 작업 메서드를 업데이트할 수 있습니다.

#### <a name="complete-edit-action-method-implementations"></a>작업 메서드 구현 편집 완료

아래 코드는 편집 시나리오에 필요한 모든 컨트롤러 논리를 구현 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

편집 구현에 대 한 좋은 점은, 컨트롤러 클래스와 뷰 템플릿이 모두 Dinner model에서 적용 되는 특정 유효성 검사 또는 비즈니스 규칙에 대해 알고 있어야 한다는 것입니다. 나중에 모델에 추가 규칙을 추가할 수 있으며 컨트롤러 또는 뷰에서 코드를 변경 하 여 지원 하기 위해 수행할 필요가 없습니다. 코드를 최소한으로 변경 하 여 나중에 응용 프로그램 요구 사항을 쉽게 향상 시킬 수 있는 유연성을 제공 합니다.

### <a name="create-support"></a>지원 만들기

Microsoft는이 DinnersController 클래스의 "편집" 동작을 구현 했습니다. 이제에서 "만들기" 지원을 구현 하 여 사용자가 새 Dinners를 추가할 수 있도록 하겠습니다.

#### <a name="the-http-get-create-action-method"></a>HTTP-GET 작업 메서드

먼저 create action 메서드의 HTTP "GET" 동작을 구현 합니다. 이 메서드는 누군가가 */Dinners/Create* URL을 방문할 때 호출 됩니다. 구현은 다음과 같습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

위의 코드는 새 Dinner object를 만들고 나중에 1 주일 후에 EventDate 속성을 할당 합니다. 그런 다음 새 Dinner object를 기반으로 하는 뷰를 렌더링 합니다. *View ()* 도우미 메서드에 이름을 명시적으로 전달 하지 않았으므로 규칙 기반 기본 경로를 사용 하 여 뷰 템플릿을 확인 합니다./Views/Dinners/Create.aspx.

이제이 뷰 템플릿을 만들어 보겠습니다. 이렇게 하려면 만들기 작업 메서드 내에서 마우스 오른쪽 단추를 클릭 하 고 "뷰 추가" 상황에 맞는 메뉴 명령을 선택 합니다. "뷰 추가" 대화 상자 내에서 저녁 개체를 보기 템플릿에 전달 하 고 "만들기" 템플릿을 자동으로 스 캐 폴드 선택 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

"추가" 단추를 클릭 하면 Visual Studio가 "\Views\Dinners" 디렉터리에 새 스 캐 폴드 기반 "Create .aspx" 보기를 저장 하 고 IDE 내에서 엽니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

Microsoft에서 생성 된 기본 "create" 스 캐 폴드 파일을 몇 가지 변경 하 고 아래와 같이 수정 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

이제 응용 프로그램을 실행 하 고 브라우저 내에서 *"/Dinners/Create"* URL에 액세스할 때 만들기 작업 구현에서 아래와 같은 UI를 렌더링 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>HTTP POST 만들기 작업 메서드 구현

만들기 작업 메서드의 HTTP GET 버전이 구현 되어 있습니다. 사용자가 [저장] 단추를 클릭 하면 */Dinners/Create* URL에 폼 게시를 수행 하 고 HTTP post 동사를 사용 하 여 HTML &lt;입력&gt; 양식 값을 전송 합니다.

이제 create action 메서드의 HTTP POST 동작을 구현 해 보겠습니다. 먼저 오버 로드 된 "Create" 작업 메서드를 ' AcceptVerbs ' 특성이 있는 "AcceptVerbs" 특성을 포함 하는 ' Create ' 작업 메서드를 추가 하 여 HTTP POST 시나리오를 처리 하는 것으로 시작 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

HTTP POST 사용 "만들기" 메서드 내에서 게시 된 양식 매개 변수에 액세스할 수 있는 여러 가지 방법이 있습니다.

한 가지 방법은 새 Dinner object를 만든 후 *UpdateModel ()* 도우미 메서드 (예: 편집 작업)를 사용 하 여 게시 된 폼 값으로 채우는 것입니다. 그런 다음,이를 데이터베이스에 추가 하 고 데이터베이스에 저장 한 다음 사용자를 세부 정보 작업으로 리디렉션하여 아래 코드를 사용 하 여 새로 만든 Dinner a를 표시할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

또는 Create () 작업 메서드가 Dinner object를 메서드 매개 변수로 사용 하는 방법을 사용할 수 있습니다. 그런 다음 ASP.NET MVC는 자동으로 새 Dinner object를 인스턴스화하고, 양식 입력을 사용 하 여 속성을 채우고, 작업 메서드에 전달 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

위의 작업 메서드는 ModelState. IsValid 속성을 확인 하 여 Dinner object가 폼 게시 값으로 채워져 있는지 확인 합니다. 입력 변환 문제가 있는 경우 false를 반환 하 고 (예: EventDate 속성의 "가짜" 문자열), 동작 메서드에서 폼을 다시 설정 하는 데 문제가 있는 경우 false를 반환 합니다.

입력 값이 유효 하면 작업 메서드는 새 Dinner를 추가 하 고이를 새 Dinner in을 d에 게 저장 합니다. 이 작업은 try/catch 블록 내에서 래핑하고 비즈니스 규칙 위반이 발생할 경우 폼을 다시 시작 합니다 .이 경우에는 예외가 발생 합니다.

동작에서이 오류 처리 동작을 확인 하기 위해 */Dinners/Create* URL을 요청 하 고 새 Dinner a에 대 한 세부 정보를 입력할 수 있습니다. 입력 또는 값이 잘못 되 면 아래와 같이 강조 표시 된 오류와 함께 만들기 양식이 다시 표시 됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

만들기 양식이 편집 양식과 정확히 동일한 유효성 검사 및 비즈니스 규칙을 어떻게 인식 하는지 확인 합니다. 이는 유효성 검사 및 비즈니스 규칙이 모델에서 정의 되었고 응용 프로그램의 UI 나 컨트롤러에 포함 되지 않았기 때문입니다. 즉, 나중에 유효성 검사 또는 비즈니스 규칙을 한 곳에서 변경/진화 하 고 응용 프로그램 전체에 적용 되도록 할 수 있습니다. 새 규칙을 자동으로 적용 하거나 기존 규칙에 대 한 수정 사항을 자동으로 적용 하도록 편집 또는 만들기 작업 메서드 내의 코드를 변경 하지 않아도 됩니다.

입력 값을 수정 하 고 "저장" 단추를 다시 클릭 하면, 해당 하는 경우에는 추가 작업이 성공 하 고 새 Dinner가 데이터베이스에 추가 됩니다. 그런 다음 */Dinners/Details/[id]* URL로 리디렉션됩니다. 여기에서 새로 만든 Dinner a에 대 한 세부 정보가 표시 됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>삭제 지원

이제 microsoft의 ' 삭제 ' 지원을 추가 해 보겠습니다.

#### <a name="the-http-get-delete-action-method"></a>HTTP-GET Delete 동작 메서드입니다.

먼저 delete 동작 메서드의 HTTP GET 동작을 구현 합니다. 이 메서드는 누군가가 */Dinners/Delete/[id]* URL을 방문할 때 호출 됩니다. 다음은 구현입니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

작업 메서드는 삭제할 Dinner a를 검색 하려고 합니다. Dinner exists가 있는 경우 Dinner object를 기준으로 뷰를 렌더링 합니다. 개체가 존재 하지 않거나 이미 삭제 된 경우 "Details" 작업 메서드에 대해 앞에서 만든 "NotFound" 뷰 템플릿을 렌더링 하는 뷰를 반환 합니다.

삭제 작업 메서드 내에서 마우스 오른쪽 단추를 클릭 하 고 "뷰 추가" 상황에 맞는 메뉴 명령을 선택 하 여 "삭제" 뷰 템플릿을 만들 수 있습니다. "뷰 추가" 대화 상자 내에서 Dinner object를 뷰 템플릿에 모델로 전달 하 고 빈 템플릿을 만들도록 선택 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

"추가" 단추를 클릭 하면 Visual Studio에서 "\Views\Dinners" 디렉터리 내에 새 ".aspx" 보기 템플릿 파일을 추가 합니다. 템플릿에 HTML 및 코드를 추가 하 여 아래와 같은 삭제 확인 화면을 구현 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

위의 코드는 삭제할 Dinner of의 제목을 표시 하 고, 최종 사용자가 해당 내에서 "삭제" 단추를 클릭 하면/Dinners/Delete/[id] URL에 게시물을 수행 하는 &lt;form&gt; 요소를 출력 합니다.

응용 프로그램을 실행 하 고 유효한 Dinner object에 대 한 *"/Dinners/Delete/[id]"* URL에 액세스 하는 경우 아래와 같은 UI를 렌더링 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **사이드 토픽: POST를 수행 하는 이유는 무엇 인가요?** |
| --- |
| 사용자에 게 요청할 수 있습니다. 삭제 확인 화면 내에서&gt; &lt;양식을 만드는 데 필요한 이유는 무엇 인가요? 단순히 표준 하이퍼링크를 사용 하 여 실제 삭제 작업을 수행 하는 동작 메서드에 연결 하지 않는 이유는 무엇 인가요? 그 이유는 Url을 검색 하는 웹 크롤러 및 검색 엔진 으로부터 보호 하 고 링크를 팔 로우 할 때 실수로 데이터를 삭제 하기 때문입니다. HTTP-GET 기반 Url은 액세스/탐색에 "안전한" 것으로 간주 되며 HTTP POST를 따르지 않아야 합니다. 좋은 규칙은 항상 소거식 또는 데이터 수정 작업을 HTTP POST 요청 뒤에 배치 하는 것입니다. |

#### <a name="implementing-the-http-post-delete-action-method"></a>HTTP-사후 삭제 작업 메서드 구현

이제 삭제 확인 화면을 표시 하는 ' 삭제 작업 ' 메서드의 HTTP 가져오기 버전을 사용할 수 있습니다. 최종 사용자가 "삭제" 단추를 클릭 하면 */Dinners/Dinner/[id]* URL에 폼 게시가 수행 됩니다.

이제 다음 코드를 사용 하 여 delete 동작 메서드의 HTTP "POST" 동작을 구현 해 보겠습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

삭제 작업 메서드의 HTTP POST 버전은 삭제할 dinner object를 검색 하려고 시도 합니다. 이를 찾을 수 없는 경우 (이미 삭제 되었기 때문에) "NotFound" 템플릿을 렌더링 합니다. 저녁을 찾은 경우에는이를 d a d i 저장소에서 삭제 합니다. 그런 다음 "삭제 된" 템플릿을 렌더링 합니다.

"삭제 된" 템플릿을 구현 하려면 작업 메서드를 마우스 오른쪽 단추로 클릭 하 고 "뷰 추가" 상황에 맞는 메뉴를 선택 합니다. 보기의 이름을 "Deleted"로 지정 하 고 빈 템플릿 (강력한 형식의 모델 개체를 사용 하지 않음)으로 지정 합니다. 그런 다음 몇 가지 HTML 콘텐츠를 추가 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

이제 응용 프로그램을 실행 하 고 유효한 Dinner object에 대 한 *"/Dinners/Delete/[id]"* URL에 액세스할 때 아래와 같이 Dinner Delete 확인 화면이 렌더링 됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

"삭제" 단추를 클릭 하면 */Dinners/Delete/[id]* URL에 대 한 HTTP POST를 수행 하 여 데이터베이스에서 Dinner a를 삭제 하 고 "Deleted" 보기 템플릿을 표시 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>모델 바인딩 보안

ASP.NET MVC의 기본 제공 모델 바인딩 기능을 사용 하는 두 가지 다른 방법에 대해 설명 했습니다. 첫 번째는 UpdateModel () 메서드를 사용 하 여 기존 모델 개체의 속성을 업데이트 하 고, 두 번째는 ASP.NET MVC를 사용 하 여의 모델 개체를 동작 메서드 매개 변수로 전달 하는 것입니다. 두 기술 모두 매우 강력 하 고 매우 유용 합니다.

또한이 기능을 사용 하면 it 책임이 있습니다. 사용자 입력을 허용 하는 경우 항상 보안에 대해 paranoid 하는 것이 중요 하며,이는 개체를 폼 입력에 바인딩할 때에도 마찬가지입니다. HTML 및 JavaScript 주입 공격을 방지 하기 위해 사용자가 입력 한 값을 항상 HTML로 인코딩하고 SQL 삽입 공격에 주의 해야 합니다 (참고:이를 방지 하기 위해 매개 변수를 자동으로 인코딩하는 응용 프로그램에 대 한 LINQ to SQL를 사용 중입니다. 공격 유형). 클라이언트 쪽 유효성 검사에만 의존해 서는 안 되며 항상 서버 쪽 유효성 검사를 사용 하 여 가짜 값을 보내려고 시도 하는 해커 로부터 보호 해야 합니다.

ASP.NET MVC의 바인딩 기능을 사용할 때 고려해 야 할 추가 보안 항목 중 하나는 사용자가 바인딩하는 개체의 범위입니다. 특히, 바인딩할 수 있는 속성의 보안 의미를 이해 하 고 최종 사용자가 업데이트 하기 위해 정말로 업데이트할 수 있는 속성만 허용 하는지 확인 해야 합니다.

기본적으로 UpdateModel () 메서드는 들어오는 폼 매개 변수 값과 일치 하는 모델 개체의 모든 속성을 업데이트 하려고 합니다. 마찬가지로 기본적으로 동작 메서드 매개 변수로 전달 되는 개체는 폼 매개 변수를 통해 설정 된 모든 속성을 가질 수 있습니다.

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>사용률에 대 한 바인딩 잠금

업데이트할 수 있는 속성의 명시적 "포함 목록"을 제공 하 여 사용 별로 바인딩 정책을 잠글 수 있습니다. 이 작업은 다음과 같이 UpdateModel () 메서드에 추가 문자열 배열 매개 변수를 전달 하 여 수행할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

동작 메서드 매개 변수로 전달 되는 개체는 다음과 같이 허용 되는 속성의 "포함 목록"을 지정할 수 있는 [Bind] 특성도 지원 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>형식에 대 한 바인딩 잠금

유형별 기준으로 바인딩 규칙을 잠글 수도 있습니다. 이렇게 하면 바인딩 규칙을 한 번 지정한 다음 모든 컨트롤러 및 작업 메서드에서 모든 시나리오 (UpdateModel 및 동작 메서드 매개 변수 시나리오 모두 포함)에 적용할 수 있습니다.

[Bind] 특성을 형식에 추가 하거나 응용 프로그램의 Global.asax 파일에 등록 하 여 형식당 하나의 형식 바인딩 규칙을 사용자 지정할 수 있습니다 (형식을 소유 하지 않는 시나리오에 유용). 그런 다음 Bind 특성의 Include 및 Exclude 속성을 사용 하 여 특정 클래스 또는 인터페이스에 대해 바인딩할 수 있는 속성을 제어할 수 있습니다.

여기서는 팀 간 Ddinner 응용 프로그램에서 Dinner class에 대해이 기술을 사용 하 고 바인딩 가능한 속성의 목록을 다음으로 제한 하는 [Bind] 특성을 추가 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

바인딩을 통해 RSVPs 컬렉션을 조작 하는 것을 허용 하지 않으며, 바인딩을 통해 DinnerID 또는 HostedBy 속성을 설정할 수 없습니다. 보안상의 이유로 작업 메서드 내에서 명시적 코드를 사용 하 여 이러한 특정 속성을 조작 합니다.

### <a name="crud-wrap-up"></a>CRUD 래핑

ASP.NET MVC에는 양식 게시 시나리오를 구현 하는 데 도움이 되는 다양 한 기본 제공 기능이 포함 되어 있습니다. Microsoft는 이러한 다양 한 기능을 사용 하 여 microsoft의 다양 한 기능을 통해 microsoft의

응용 프로그램을 구현 하는 모델 중심 접근 방법을 사용 하 고 있습니다. 즉, 모든 유효성 검사 및 비즈니스 규칙 논리가 모델 계층 내에서 정의 되 고 컨트롤러 또는 뷰 내에서 정의 되지 않습니다. 컨트롤러 클래스와 뷰 템플릿은 Dinner model 클래스에서 적용 하는 특정 비즈니스 규칙에 대 한 정보를 알지 못합니다.

이렇게 하면 응용 프로그램 아키텍처가 깨끗 하 게 유지 되 고 테스트 하기가 더 쉬워집니다. 향후 모델 계층에 비즈니스 규칙을 더 추가할 수 있으며, 컨트롤러 또는 뷰에서 *코드를 변경 하* 여 지원 하기 위해 수행할 필요가 없습니다. 이를 통해 향후 응용 프로그램을 개선 하 고 변경 하는 데 많은 민첩성을 제공할 예정입니다.

이제 microsoft의 DinnersController에서 Dinner 목록/세부 정보 뿐만 아니라 만들기, 편집 및 삭제 지원을 사용할 수 있습니다. 클래스에 대 한 전체 코드는 아래에서 찾을 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>다음 단계

이제 microsoft의 기본 CRUD (만들기, 읽기, 업데이트 및 삭제) 지원이 microsoft의 DinnersController 클래스 내에서 구현 되었습니다.

이제 ViewData 및 ViewModel 클래스를 사용 하 여 폼에서 훨씬 더 풍부한 UI를 사용 하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [다음](use-viewdata-and-implement-viewmodel-classes.md)
