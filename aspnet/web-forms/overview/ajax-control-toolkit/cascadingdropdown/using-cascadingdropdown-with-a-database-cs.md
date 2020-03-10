---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: 데이터베이스와 함께 CascadingDropDown 사용 (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 anoth에 연결 된 값을 로드 하도록 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: bcf453170d17807b4e3b2d2a8b545cba43139f89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483749"
---
# <a name="using-cascadingdropdown-with-a-database-c"></a>데이터베이스에 CascadingDropDown 사용(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)

> AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다. 이 작업을 수행 하려면 특수 웹 서비스를 만들어야 합니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다. 예를 들어, 한 목록에는 미국 주 목록이 제공 되며 다음 목록에는 해당 상태의 주 도시가 채워집니다. 이 작업을 수행 하려면 특수 웹 서비스를 만들어야 합니다.

## <a name="steps"></a>단계

먼저 데이터 원본이 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스와 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스는 Visual Studio 설치 (express edition 포함)의 선택적 부분이 며 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)에서 별도의 다운로드로 사용할 수도 있습니다. AdventureWorks 데이터베이스는 SQL Server 2005 샘플 및 예제 데이터베이스 ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)에서 다운로드)의 일부입니다. 데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))를 사용 하 고 `AdventureWorks.mdf` 데이터베이스 파일을 연결 하는 것입니다.

이 샘플에서는 SQL Server 2005 Express Edition 인스턴스가 `SQLEXPRESS` 호출 되 고 웹 서버와 같은 컴퓨터에 있는 것으로 가정 합니다. 이는 기본 설정 이기도 합니다. 설정이 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `ScriptManager` 컨트롤을 배치 해야 합니다 (&lt;`form`&gt; 요소 내).

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

다음 단계에서는 두 개의 DropDownList 컨트롤이 필요 합니다. 이 샘플에서는 AdventureWorks의 공급 업체 및 연락처 정보를 사용 합니다. 따라서 사용 가능한 공급 업체에 대 한 목록과 사용 가능한 연락처에 대 한 목록을 하나씩 만듭니다.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

그런 다음 페이지에 두 개의 CascadingDropDown extender를 추가 해야 합니다. 하나는 첫 번째 (공급 업체) 목록을 채우고 다른 하나는 두 번째 (연락처) 목록을 채웁니다. 다음 특성을 설정 해야 합니다.

- `ServicePath`: 목록 항목을 제공 하는 웹 서비스의 URL
- `ServiceMethod`: 목록 항목을 전달 하는 웹 메서드
- `TargetControlID`: 드롭다운 목록의 ID
- `Category`: 호출 시 웹 메서드에 제출 되는 범주 정보
- `PromptText`: 서버에서 목록 데이터를 비동기적으로 로드할 때 표시 되는 텍스트입니다.
- `ParentControlID`: (선택 사항) 현재 목록의 로드를 트리거하는 부모 드롭다운 목록입니다.

사용 되는 프로그래밍 언어에 따라 문제의 웹 서비스 이름이 변경 되지만 다른 모든 특성 값은 동일 합니다. 첫 번째 드롭다운 목록에 대 한 CascadingDropDown 요소는 다음과 같습니다.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

두 번째 목록의 control extender는 공급 업체 목록의 항목을 선택 하 여 연락처 목록에 있는 관련 된 요소를 로드 하도록 하는 `ParentControlID` 특성을 설정 해야 합니다.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

실제 작업은 웹 서비스에서 수행 되며 다음과 같이 설정 됩니다. `[ScriptService]` 특성이 사용 됩니다. 그렇지 않으면 AJAX ASP.NET는 클라이언트 쪽 스크립트 코드에서 웹 메서드에 액세스 하기 위한 JavaScript 프록시를 만들 수 없습니다.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

CascadingDropDown에서 호출 하는 웹 메서드의 시그니처는 다음과 같습니다.

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

따라서 반환 값은 컨트롤 Toolkit에서 정의 되는 `CascadingDropDownNameValue` 형식의 배열 이어야 합니다. `GetVendors()` 메서드는 구현 하기가 매우 쉽습니다. 코드는 AdventureWorks 데이터베이스에 연결 하 고 처음 25 개 공급 업체를 쿼리 합니다. `CascadingDropDownNameValue` 생성자의 첫 번째 매개 변수는 목록 항목의 캡션으로, 두 번째 매개 변수는 값 (HTML의 &lt;`option`&gt; 요소의 값 특성)입니다. 코드는 다음과 같습니다.

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

공급 업체에 대 한 연결 된 연락처를 가져오는 방법 (메서드 이름: `GetContactsForVendor()`)은 조금 더 까다롭습니다. 먼저 첫 번째 드롭다운 목록에서 선택한 공급 업체를 확인 해야 합니다. 컨트롤 도구 키트는 해당 작업에 대 한 도우미 메서드를 정의 합니다. `ParseKnownCategoryValuesString()` 메서드는 드롭다운 데이터가 포함 된 `StringDictionary` 요소를 반환 합니다.

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

보안상의 이유로이 데이터는 먼저 유효성을 검사 해야 합니다. 따라서 공급 업체 항목이 있는 경우 (첫 번째 CascadingDropDown 요소의 `Category` 속성이 `"Vendor"`)로 설정 되어 있기 때문에 선택한 공급 업체의 ID를 검색할 수 있습니다.

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

메서드의 나머지 부분은 매우 단순 합니다. 공급 업체의 ID는 해당 공급 업체에 대 한 모든 연결 된 연락처를 검색 하는 SQL 쿼리에 대 한 매개 변수로 사용 됩니다. 다시 한 번, 메서드는 `CascadingDropDownNameValue`형식의 배열을 반환 합니다.

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

ASP.NET 페이지를 로드 하 고, 잠시 후 공급 업체 목록이 25 개 항목으로 채워져 있습니다. 한 항목을 선택 하 고 두 번째 드롭다운 목록이 데이터로 채워지는 방식을 확인 합니다.

[첫 번째 목록이 자동으로 채워지는 ![](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)

첫 번째 목록이 자동으로 채워집니다 ([전체 크기 이미지를 보려면 클릭](using-cascadingdropdown-with-a-database-cs/_static/image3.png)).

[첫 번째 목록에서 선택한 항목에 따라 두 번째 목록이 채워집니다 ![](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)

첫 번째 목록의 선택 항목에 따라 두 번째 목록이 채워집니다 ([전체 크기 이미지를 보려면 클릭](using-cascadingdropdown-with-a-database-cs/_static/image6.png)).

> [!div class="step-by-step"]
> [이전](filling-a-list-using-cascadingdropdown-cs.md)
> [다음](presetting-list-entries-with-cascadingdropdown-cs.md)
