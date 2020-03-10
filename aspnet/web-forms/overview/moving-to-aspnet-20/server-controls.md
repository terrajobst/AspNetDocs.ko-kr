---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 서버 컨트롤 | Microsoft Docs
author: microsoft
description: ASP.NET 2.0는 다양 한 방식으로 서버 컨트롤을 향상 시킵니다. 이 모듈에서는 ASP.NET 2.0 및 Visual Studio 200와 같은 아키텍처 변경 사항을 설명 합니다.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: c02a633013f061c09141d4f98871848c011a799e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521093"
---
# <a name="server-controls"></a>서버 컨트롤

[Microsoft](https://github.com/microsoft) 에서

> ASP.NET 2.0는 다양 한 방식으로 서버 컨트롤을 향상 시킵니다. 이 모듈에서는 ASP.NET 2.0 및 Visual Studio 2005에서 서버 컨트롤을 처리 하는 방식에 대 한 아키텍처 변경 내용 중 일부를 설명 합니다.

ASP.NET 2.0는 다양 한 방식으로 서버 컨트롤을 향상 시킵니다. 이 모듈에서는 ASP.NET 2.0 및 Visual Studio 2005에서 서버 컨트롤을 처리 하는 방식에 대 한 아키텍처 변경 내용 중 일부를 설명 합니다.

## <a name="view-state"></a>상태 보기

ASP.NET 2.0에서 보기 상태의 주요 변화는 크기를 크게 줄이는 것입니다. 달력 컨트롤이 있는 페이지를 생각해 보세요. ASP.NET 1.1의 뷰 상태는 다음과 같습니다.

[!code-css[Main](server-controls/samples/sample1.css)]

이제 ASP.NET 2.0의 동일한 페이지에 대 한 뷰 상태입니다.

[!code-css[Main](server-controls/samples/sample2.css)]

매우 중요 한 변경 사항이 며, 해당 뷰 상태가 네트워크를 통해 앞뒤로 전달 되는 것을 고려 하 여 개발자에 게 상당한 성능 증가를 제공할 수 있습니다. 뷰 상태의 크기 감소는 내부적으로 처리 하는 방식 때문에 발생 합니다. 뷰 상태는 b a s e 64로 인코딩된 문자열입니다. ASP.NET 2.0에서 뷰 상태의 변화를 보다 잘 이해 하기 위해 위의 예제에서 디코딩된 값을 살펴보겠습니다.

디코딩된 1.1 뷰 상태는 다음과 같습니다.

[!code-css[Main](server-controls/samples/sample3.css)]

이는 약간 항목 처럼 보일 수 있지만 여기에는 패턴이 있습니다. ASP.NET 1.x에서는 단일 문자를 사용 하 여 &lt;&gt; 문자를 통해 데이터 형식 및 구분 된 값을 식별 했습니다. 위의 뷰 상태 샘플에서 "t"는 세 번째를 나타냅니다. 세 개는 ArrayLists 쌍을 포함 합니다. "l"은 ArrayList를 나타냅니다. 이러한 ArrayLists 중 하나에 값이 1 인 Int32 ("i")가 포함 되어 있고 다른 하나는 다른 세 가지를 포함 합니다. 세 번째에는 ArrayLists 등의 쌍이 포함 됩니다. 기억해 야 할 중요 한 점은 쌍을 포함 하는 Triplets를 사용 하 고, 문자를 통해 데이터 형식을 식별 하 고, &lt; 및 &gt; 문자를 구분 기호로 사용 한다는 것입니다.

ASP.NET 2.0에서 디코딩된 뷰 상태는 약간 다르게 보입니다.

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

디코딩된 뷰 상태의 모양이 크게 변경 된 것을 알 수 있습니다. 이러한 변경에는 여러 아키텍처 기초가 되 있습니다. ASP.NET 1.x의 뷰 상태는 LosFormatter를 사용 하 여 데이터를 serialize 했습니다. 2\.0에서는 새 ObjectStateFormatter 클래스를 사용 합니다. 이 클래스는 뷰 상태 및 컨트롤 상태를 직렬화 및 역직렬화 하는 데 도움이 되도록 특별히 설계 되었습니다. (컨트롤 상태는 다음 섹션에서 설명 합니다.) Serialization 및 deserialization을 수행 하는 방법을 변경 하면 많은 이점을 얻을 수 있습니다. 가장 많이 사용 되는 것은 TextWriter를 사용 하는 LosFormatter와 달리 ObjectStateFormatter는 BinaryWriter를 사용 한다는 점입니다. 이렇게 하면 ASP.NET 2.0에서 뷰 상태를 문자열 대신 일련의 바이트로 저장할 수 있습니다. 예를 들어 정수를 사용 합니다. ASP.NET 1.1에서는 정수에 4 바이트의 뷰 상태가 필요 합니다. ASP.NET 2.0에서는 동일한 정수에 1 바이트만 필요 합니다. 저장 되는 뷰 상태의 양을 줄이기 위해 기타 기능이 향상 되었습니다. 예를 들어 DateTime 값은 이제 문자열 대신 TickCount를 사용 하 여 저장 됩니다.

모든 것이 충분 하지 않은 것 처럼 1. x의 가장 강력한 뷰 상태 소비자 중 하나가 DataGrid 및 유사한 컨트롤 이라는 사실을 염두에 지불 했습니다. 뷰 상태에 관심이 있는 DataGrid와 같은 컨트롤의 주요 단점은 많은 양의 반복 되는 정보를 포함 하는 경우가 많습니다. ASP.NET 1.x에서 반복 되는 정보는 간단히 저장 된 후에도 더 커질 뷰 상태를 초래 합니다. ASP.NET 2.0에서는 새 IndexedString 클래스를 사용 하 여 이러한 데이터를 저장 합니다. 문자열이 반복 되 면 IndexedString의 토큰과 인덱스를 IndexedString 개체의 실행 테이블 내에 저장 합니다.

## <a name="control-state"></a>컨트롤 상태

개발자가 뷰 상태를 가진 주요 gripes 중 하나는 HTTP 페이로드에 추가한 크기입니다. 앞에서 설명한 것 처럼 뷰 상태의 가장 큰 소비자 중 하나는 DataGrid 컨트롤입니다. 많은 개발자가 DataGrid에서 생성 한 뷰 상태를 크게 방지 하기 위해 대부분의 개발자가 해당 컨트롤에 대 한 뷰 상태를 비활성화 했습니다. 아쉽게도 해당 솔루션이 항상 좋은 것은 아닙니다. ASP.NET 1.x의 뷰 상태에는 컨트롤의 올바른 기능에 필요한 데이터가 포함 되어 있지 않습니다. 또한 컨트롤의 UI 상태에 대 한 정보를 포함 합니다. 즉, DataGrid에서 페이지 매김을 허용 하려면 뷰 상태에 포함 된 모든 UI 정보가 필요 하지 않은 경우에도 뷰 상태를 사용 하도록 설정 해야 합니다. 이는 모두 또는 없음 시나리오입니다.

ASP.NET 2.0에서 컨트롤 상태는 컨트롤 상태 소개를 통해 문제를 해결 합니다. 컨트롤 상태에는 컨트롤의 적절 한 기능에 반드시 필요한 데이터가 포함 되어 있습니다. 뷰 상태와는 달리 컨트롤 상태를 비활성화할 수 없습니다. 따라서 컨트롤 상태에 저장 되는 데이터를 신중 하 게 제어 하는 것이 중요 합니다.

> [!NOTE]
> 컨트롤 상태는 \_\_VIEWSTATE 숨김 폼 필드의 뷰 상태와 함께 유지 됩니다.

이 비디오는 뷰 상태 및 컨트롤 상태를 보여 주는 연습입니다.

![](server-controls/_static/image1.png)

[전체 화면 비디오 열기](server-controls/_static/state1.wmv)

서버 컨트롤에서 컨트롤 상태를 읽고 쓰도록 하려면 세 가지 단계를 수행 해야 합니다.

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>1 단계: RegisterRequiresControlState 메서드 호출

RegisterRequiresControlState 메서드는 컨트롤이 컨트롤 상태를 유지 해야 함을 ASP.NET에 게 알립니다. 등록 되는 컨트롤인 컨트롤의 인수 하나를 사용 합니다.

요청에서 요청에 대 한 등록이 유지 되지 않는다는 점에 유의 해야 합니다. 따라서 컨트롤이 컨트롤 상태를 유지 해야 하는 경우 모든 요청에 대해이 메서드를 호출 해야 합니다. OnInit에서 메서드를 호출 하는 것이 좋습니다.

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>2 단계: SaveControlState 재정의

SaveControlState 메서드는 마지막 포스트백 이후 컨트롤의 컨트롤 상태 변경 내용을 저장 합니다. 컨트롤의 상태를 나타내는 개체를 반환 합니다.

## <a name="step-3-override-loadcontrolstate"></a>3 단계: LoadControlState 재정의

LoadControlState 메서드는 저장 된 상태를 컨트롤에 로드 합니다. 메서드는 컨트롤의 저장 된 상태를 포함 하는 Object 형식의 인수 하나를 사용 합니다.

## <a name="full-xhtml-compliance"></a>전체 XHTML 준수

웹 개발자는 웹 응용 프로그램에서 표준의 중요도를 알고 있습니다. 표준 기반 개발 환경을 유지 하기 위해 ASP.NET 2.0는 완전히 XHTML 규격을 준수 합니다. 따라서 모든 태그는 HTML 4.0 이상을 지 원하는 브라우저의 XHTML 표준에 따라 렌더링 됩니다.

ASP.NET 1.1의 DOCTYPE 정의는 다음과 같습니다.

[!code-html[Main](server-controls/samples/sample6.html)]

ASP.NET 2.0에서 기본 DOCTYPE 정의는 다음과 같습니다.

[!code-html[Main](server-controls/samples/sample7.html)]

을 선택 하는 경우 구성 파일의 xhtmlConformance 노드를 통해 기본 XHTML 준수를 변경할 수 있습니다. 예를 들어 web.config 파일의 다음 노드는 XHTML 규격을 XHTML 1.0 Strict로 변경 합니다.

[!code-xml[Main](server-controls/samples/sample8.xml)]

을 선택 하는 경우 다음과 같이 ASP.NET 1.x에서 사용 되는 레거시 구성을 사용 하도록 ASP.NET를 구성할 수도 있습니다.

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>어댑터를 사용 하 여 적응 렌더링

ASP.NET 1.x에서 구성 파일에는 HttpBrowserCapabilities 개체를 채운 &lt;browserCaps&gt; 섹션이 포함 되어 있습니다. 이 개체를 통해 개발자는 특정 요청을 만들고 코드를 적절 하 게 렌더링 하는 장치를 확인할 수 있습니다. ASP.NET 2.0에서는 모델이 개선 되었으며 이제 새 ControlAdapter 클래스를 사용 합니다. ControlAdapter 클래스는 컨트롤의 수명 주기에 있는 이벤트를 재정의 하 고 사용자 에이전트의 기능에 따라 컨트롤의 렌더링을 제어 합니다. 특정 사용자 에이전트의 기능은 c:\windows\microsoft.net\framework\v2.0.에 저장 된 브라우저 정의 파일 (확장명이 .browser 인 파일)에 의해 정의 됩니다.\*\*\*\*\Config\om\oml 폴더입니다.

> [!NOTE]
> ControlAdapter 클래스는 추상 클래스입니다.

1\.x의 &lt;browserCaps&gt; 섹션과 마찬가지로 브라우저 정의 파일은 정규식을 사용 하 여 요청 하는 브라우저를 식별 하기 위해 사용자 에이전트 문자열을 구문 분석 합니다. 사용자 에이전트에 대 한 특정 기능을 정의 합니다. ControlAdapter는 Render 메서드를 통해 컨트롤을 렌더링 합니다. 따라서 Render 메서드를 재정의 하는 경우 기본 클래스에서 Render를 호출 하면 안 됩니다. 이렇게 하면 렌더링은 어댑터에 대해 한 번, 컨트롤 자체에 대해 한 번만 실행 될 수 있습니다.

## <a name="developing-a-custom-adapter"></a>사용자 지정 어댑터 개발

ControlAdapter에서 상속 하 여 사용자 지정 어댑터를 개발할 수 있습니다. 또한 페이지에 어댑터를 필요로 하는 경우에는 추상 클래스 PageAdapter에서 상속할 수 있습니다. 사용자 지정 어댑터에 컨트롤을 매핑하는 것은 브라우저 정의 파일의 &lt;controlAdapters&gt; 요소를 통해 수행 됩니다. 예를 들어 브라우저 정의 파일의 다음 XML은 메뉴 컨트롤을 MenuAdapter 클래스에 매핑합니다.

[!code-html[Main](server-controls/samples/sample10.html)]

이 모델을 사용 하 여 컨트롤 개발자가 특정 장치나 브라우저를 대상으로 하는 것은 매우 쉽습니다. 또한 개발자는 모든 장치에서 페이지가 렌더링 되는 방식을 완전히 제어할 수 있습니다.

## <a name="per-device-rendering"></a>장치 단위 렌더링

ASP.NET 2.0의 서버 컨트롤 속성은 브라우저 관련 접두사를 사용 하 여 장치별로 지정할 수 있습니다. 예를 들어 아래 코드는 페이지를 검색 하는 데 사용 되는 장치에 따라 레이블의 텍스트를 변경 합니다.

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

이 레이블을 포함 하는 페이지가 Internet Explorer에서 검색 되 면 레이블에 "Internet Explorer에서 검색 하 고 있습니다." 라는 텍스트가 표시 됩니다. Firefox에서 페이지를 검색 하면 레이블에 "Firefox에서 검색 하 고 있습니다." 라는 텍스트가 표시 됩니다. 다른 모든 장치에서 페이지를 검색 하면 "알 수 없는 장치에서 검색 하 고 있습니다."가 표시 됩니다. 이 특수 구문을 사용 하 여 모든 속성을 지정할 수 있습니다.

## <a name="setting-focus"></a>포커스 설정

ASP.NET 1.x 개발자는 특정 컨트롤에 초기 포커스를 설정 하는 방법에 대해 자주 묻는 메시지를 표시 합니다. 예를 들어 로그인 페이지에서 페이지가 처음 로드 될 때 사용자 ID 텍스트 상자가 포커스를 가져오도록 하는 것이 유용 합니다. ASP.NET 1.x에서이 작업을 수행 하려면 일부 클라이언트 쪽 스크립트를 작성 해야 합니다. 이러한 스크립트는 간단한 작업 이지만 SetFocus 메서드 덕분에 ASP.NET 2.0에서는 더 이상 필요 하지 않습니다. SetFocus 메서드는 포커스를 받아야 하는 컨트롤을 나타내는 인수 하나를 사용 합니다. 이 인수는 컨트롤의 클라이언트 ID (문자열) 또는 서버 컨트롤의 이름을 컨트롤 개체로 사용할 수 있습니다. 예를 들어 페이지가 처음 로드 될 때 txtUserID 라는 TextBox 컨트롤에 초기 포커스를 설정 하려면 페이지\_로드에 다음 코드를 추가 합니다.

[!code-csharp[Main](server-controls/samples/sample12.cs)]

--또는

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0는 Webresource.axd 처리기 (이전에 설명)를 사용 하 여 포커스를 설정 하는 클라이언트 쪽 함수를 렌더링 합니다. 클라이언트 쪽 함수의 이름은 다음과 같이 WebForm\_AutoFocus입니다.

[!code-html[Main](server-controls/samples/sample14.html)]

또는 컨트롤에 대 한 포커스 메서드를 사용 하 여 해당 컨트롤에 대 한 초기 포커스를 설정할 수 있습니다. 포커스 메서드는 컨트롤 클래스에서 파생 되 고 모든 ASP.NET 2.0 컨트롤에서 사용할 수 있습니다. 유효성 검사 오류가 발생 하는 경우에도 포커스를 특정 컨트롤로 설정할 수 있습니다. 이에 대해서는 뒷부분에서 설명 합니다.

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2.0의 새 서버 컨트롤

다음은 ASP.NET 2.0의 새로운 서버 컨트롤입니다. 그 중 일부에 대 한 자세한 내용은 이후 모듈을 참조 하세요.

## <a name="imagemap-control"></a>ImageMap 컨트롤

ImageMap 컨트롤을 사용 하면 다시 게시를 시작 하거나 URL로 이동할 수 있는 이미지에 핫스팟을 추가할 수 있습니다. 사용할 수 있는 핫스팟 유형은 세 가지입니다. CircleHotSpot, RectangleHotSpot 및 PolygonHotSpot입니다. 핫스폿은 Visual Studio에서 컬렉션 편집기를 통해 또는 프로그래밍 방식으로 코드에서 추가 됩니다. 이미지에서 핫스팟을 그리는 데 사용할 수 있는 사용자 인터페이스는 없습니다. 핫스폿의 좌표와 크기 또는 반경을 선언적으로 지정 해야 합니다. 또한 디자이너에는 핫스폿이 시각적으로 표시 되지 않습니다. 핫스폿이 URL로 이동 하도록 구성 된 경우 URL은 핫스폿의 NavigateUrl 속성을 통해 지정 됩니다. 다시 게시 핫스폿의 경우 PostBackValue 속성을 사용 하면 서버 쪽 코드에서 검색할 수 있는 문자열을 다시 게시에 전달할 수 있습니다.

![Visual Studio의 핫스팟 컬렉션 편집기](server-controls/_static/image1.jpg)

**그림 1**: Visual Studio의 핫스팟 컬렉션 편집기

## <a name="bulletedlist-control"></a>BulletedList 컨트롤

BulletedList 컨트롤은 쉽게 데이터 바인딩할 수 있는 글머리 기호 목록입니다. 목록은 BulletStyle 속성을 통해 정렬 (번호 매기기) 하거나 순서가 지정 되지 않을 수 있습니다. 목록의 각 항목은 ListItem 개체로 표시 됩니다.

![Visual Studio의 BulletedList 컨트롤](server-controls/_static/image1.gif)

**그림 2**: Visual Studio의 BulletedList 컨트롤

## <a name="hiddenfield-control"></a>HiddenField 컨트롤

HiddenField 컨트롤은 서버 쪽 코드에서 사용할 수 있는 값을 페이지에 추가 합니다. 숨겨진 폼 필드의 값은 일반적으로 게시 후에 변경 되지 않은 상태로 유지 될 것으로 예상 됩니다. 그러나 악의적인 사용자가 다시 게시 하기 전에 값을 변경할 수 있습니다. 이 경우 HiddenField 컨트롤은 ValueChanged 이벤트를 발생 시킵니다. HiddenField 컨트롤에 중요 한 정보가 있고 변경 되지 않은 상태로 유지 되도록 하려면 코드에서 ValueChanged 이벤트를 처리 해야 합니다.

## <a name="fileupload-control"></a>FileUpload 컨트롤

ASP.NET 2.0의 FileUpload 컨트롤을 사용 하면 ASP.NET 페이지를 통해 웹 서버에 파일을 업로드할 수 있습니다. 이 컨트롤은 몇 가지 예외를 제외 하 고 ASP.NET 1.x HtmlInputFile 클래스와 매우 비슷합니다. ASP.NET 1.x에서는 좋은 파일이 있는지 확인 하기 위해 PostedFile 속성을 null에 대해 확인 하는 것이 좋습니다. ASP.NET 2.0의 FileUpload 컨트롤은 같은 용도로 사용할 수 있는 새 HasFile 속성을 추가 하 고 좀 더 효율적입니다.

PostedFile 속성은 HttpPostedFile 개체에 계속 액세스할 수 있지만 이제 HttpPostedFile의 일부 기능을 FileUpload 컨트롤을 사용 하 여 기본적으로 사용할 수 있습니다. 예를 들어 업로드 된 파일을 ASP.NET 1.x에 저장 하려면 HttpPostedFile 개체에서 SaveAs 메서드를 호출 합니다. ASP.NET 2.0에서 FileUpload 컨트롤을 사용 하 여 FileUpload 컨트롤 자체에 대해 SaveAs 메서드를 호출 합니다.

2\.0 동작의 또 다른 중요 한 변경 내용 (및 가장 중요 한 변경 내용)은 더 이상 업로드 된 파일을 저장 하기 전에 메모리에 로드 하지 않아도 된다는 것입니다. 1\.x에서 업로드 된 모든 파일은 디스크에 기록 되기 전에 메모리에 완전히 저장 됩니다. 이 아키텍처는 대량 파일의 업로드를 방지 합니다.

ASP.NET 2.0에서는 httpRuntime 요소의 requestLengthDiskThreshold 특성을 사용 하 여 디스크에 기록 되기 전에 메모리의 버퍼에 보유 되는 킬로바이트 수를 구성할 수 있습니다.

**중요**: MSDN 설명서 (다른 곳에서 설명서)는이 값을 바이트 (킬로바이트)로 지정 하 고 기본값은 256로 지정 합니다. 값은 실제로 킬로바이트 단위로 지정 되며 기본값은 80입니다. 기본값 80K를 설정 하 여 버퍼가 대용량 개체 힙에서 끝나지 않도록 합니다.

## <a name="wizard-control"></a>마법사 컨트롤

패널을 사용 하거나 페이지에서 페이지로 전송 하 여 일련의 "페이지"로 정보를 수집 하려는 ASP.NET 개발자에 게 매우 일반적입니다. 그렇지 않은 경우에는 노력으로 인해 시간이 많이 소요 됩니다. 새 마법사 컨트롤은 사용자가 익숙한 마법사 인터페이스에서 선형 및 비선형 단계를 허용 하 여 문제를 해결 합니다. 마법사 컨트롤은 일련의 단계로 입력 폼을 표시 합니다. 각 단계는 컨트롤의 StepType 속성으로 지정 된 특정 유형입니다. 사용 가능한 단계 유형은 다음과 같습니다.

| **단계 유형** | **설명** |
| --- | --- |
| Auto | 마법사는 단계 계층 구조 내에서의 위치에 따라 단계 유형을 자동으로 결정 합니다. |
| 시작 | 첫 번째 단계는 주로 소개 문을 표시 하는 데 사용 됩니다. |
| 단계 | 일반적인 단계입니다. |
| Finish | 일반적으로 마법사를 완료 하는 단추를 표시 하는 데 사용 되는 최종 단계입니다. |
| 완료 | 성공 또는 실패에 대 한 통신 메시지를 표시 합니다. |

> [!NOTE]
> 마법사 컨트롤은 ASP.NET 컨트롤 상태를 사용 하 여 상태를 추적 합니다. 따라서 EnableViewState 속성은 단점이 없이 false로 설정할 수 있습니다.

이 비디오는 마법사 컨트롤의 연습입니다.

![](server-controls/_static/image2.png)

[전체 화면 비디오 열기](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>컨트롤 지역화

Localize 컨트롤은 리터럴 컨트롤과 비슷합니다. 그러나 Localize 컨트롤에는 추가 된 태그를 렌더링 하는 방법을 제어 하는 **모드** 속성이 있습니다. Mode 속성은 다음 값을 지원 합니다.

| **모드** | **설명** |
| --- | --- |
| 변환 | 태그는 요청을 만드는 브라우저의 프로토콜에 따라 변환 됩니다. |
| PassThrough | 태그가 있는 그대로 렌더링 됩니다. |
| 인코딩 | 컨트롤에 추가 된 태그는 HtmlEncode을 사용 하 여 인코딩됩니다. |

## <a name="multiview-and-view-controls"></a>MultiView 및 View 컨트롤

MultiView 컨트롤은 뷰 컨트롤의 컨테이너 역할을 하며 뷰 컨트롤은 다른 컨트롤에 대 한 컨테이너 (패널 컨트롤과 매우 유사) 역할을 합니다. MultiView 컨트롤의 각 뷰는 단일 뷰 컨트롤로 표시 됩니다. MultiView의 첫 번째 뷰 컨트롤은 보기 0, 두 번째는 보기 1입니다. MultiView 컨트롤의 ActiveViewIndex를 지정 하 여 뷰를 전환할 수 있습니다.

## <a name="substitution-control"></a>대체 컨트롤

대체 컨트롤은 ASP.NET 캐싱과 함께 사용 됩니다. 캐싱을 활용 하려는 경우 각 요청에서 업데이트 해야 하는 페이지의 일부 (즉, 캐시에서 제외 되는 페이지의 일부)를 사용 하는 경우 대체 구성 요소는 뛰어난 솔루션을 제공 합니다. 컨트롤은 실제로 출력을 렌더링 하지 않습니다. 대신 서버 쪽 코드의 메서드에 바인딩됩니다. 페이지가 요청 되 면 메서드가 호출 되 고 대체 컨트롤 대신 반환 된 태그가 렌더링 됩니다.

대체 컨트롤이 바인딩되는 메서드는 **MethodName** 속성을 통해 지정 됩니다. 해당 메서드는 다음 조건을 충족 해야 합니다.

- 이 메서드는 정적 (VB에서 공유) 방법 이어야 합니다.
- 이 클래스는 HttpContext 형식의 매개 변수 하나를 허용 합니다.
- 페이지의 컨트롤을 대체 해야 하는 태그를 나타내는 문자열을 반환 합니다.

대체 컨트롤에는 페이지의 다른 컨트롤을 수정할 수 있는 기능이 없지만 해당 매개 변수를 통해 현재 HttpContext에 액세스할 수 있습니다.

## <a name="gridview-control"></a>GridView 컨트롤

GridView 컨트롤은 DataGrid 컨트롤을 대체 합니다. 이 컨트롤은 이후 모듈에서 더 자세히 설명 합니다.

## <a name="detailsview-control"></a>DetailsView 컨트롤

DetailsView 컨트롤을 사용 하면 데이터 원본에서 단일 레코드를 표시 하 고 편집 하거나 삭제할 수 있습니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="formview-control"></a>FormView 컨트롤

FormView 컨트롤은 구성 가능한 인터페이스에서 datasource의 단일 레코드를 표시 하는 데 사용 됩니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="accessdatasource-control"></a>AccessDataSource 컨트롤

AccessDataSource 컨트롤은 Access 데이터베이스에 데이터를 바인딩하는 데 사용 됩니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="objectdatasource-control"></a>ObjectDataSource 컨트롤

ObjectDataSource 컨트롤은 3 계층 아키텍처를 지 원하는 데 사용 됩니다. 그러면 컨트롤이 데이터 소스에 직접 바인딩된 2 계층 모델과 달리 컨트롤이 중간 계층 비즈니스 개체에 데이터 바인딩될 수 있습니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="xmldatasource-control"></a>XmlDataSource 컨트롤

XmlDataSource 컨트롤은 XML 데이터 원본에 데이터를 바인딩하는 데 사용 됩니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="sitemapdatasource-control"></a>SiteMapDataSource 컨트롤

SiteMapDataSource 컨트롤은 사이트 맵 기반 사이트 탐색 컨트롤에 대 한 데이터 바인딩을 제공 합니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="sitemappath-control"></a>SiteMapPath 컨트롤

SiteMapPath 컨트롤은 일반적으로 breadcrumb 이라고 하는 일련의 탐색 링크를 표시 합니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="menu-control"></a>Menu 컨트롤

메뉴 컨트롤은 DHTML을 사용 하 여 동적 메뉴를 표시 합니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="treeview-control"></a>TreeView 컨트롤

TreeView 컨트롤은 데이터의 계층적 트리 뷰를 표시 하는 데 사용 됩니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="login-control"></a>Login 컨트롤

로그인 컨트롤은 웹 사이트에 로그인 하는 메커니즘을 제공 합니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="loginview-control"></a>LoginView 컨트롤

LoginView 컨트롤을 사용 하면 사용자의 로그인 상태에 따라 다른 템플릿을 표시할 수 있습니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="passwordrecovery-control"></a>PasswordRecovery 제어

PasswordRecovery 컨트롤은 ASP.NET 응용 프로그램 사용자가 잊어버린 암호를 검색 하는 데 사용 됩니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="loginstatus"></a>LoginStatus

LoginStatus 컨트롤은 사용자의 로그인 상태를 표시 합니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="loginname"></a>LoginName

LoginName 컨트롤은 ASP.NET 응용 프로그램에 로그인 한 후 사용자의 사용자 이름을 표시 합니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="createuserwizard"></a>CreateUserWizard

CreateUserWizard은 사용자가 ASP.NET 응용 프로그램에서 사용할 ASP.NET 멤버 자격 계정을 만들 수 있도록 하는 구성 가능한 마법사입니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="changepassword"></a>ChangePassword

ChangePassword 컨트롤을 사용 하면 사용자가 ASP.NET 응용 프로그램에 대 한 암호를 변경할 수 있습니다. 이후 모듈에서 더 자세히 설명 합니다.

## <a name="various-webparts"></a>다양 한 웹 파트

ASP.NET 2.0에는 다양 한 웹 파트 제공 됩니다. 이러한 내용은 이후 모듈에서 자세히 설명 합니다.
