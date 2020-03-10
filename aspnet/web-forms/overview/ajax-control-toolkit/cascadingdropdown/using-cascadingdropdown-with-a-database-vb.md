---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
title: 데이터베이스와 함께 CascadingDropDown 사용 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 anoth에 연결 된 값을 로드 하도록 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 97a3d33c-c856-43f3-8acb-f1ccbc48221a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 4482aa18c4446ec8f5f160c423008398ea2e1d0d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430655"
---
# <a name="using-cascadingdropdown-with-a-database-vb"></a><span data-ttu-id="0e4de-103">데이터베이스에 CascadingDropDown 사용(VB)</span><span class="sxs-lookup"><span data-stu-id="0e4de-103">Using CascadingDropDown with a Database (VB)</span></span>

<span data-ttu-id="0e4de-104">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="0e4de-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0e4de-105">[코드 다운로드](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="0e4de-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1VB.pdf)</span></span>

> <span data-ttu-id="0e4de-106">AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="0e4de-107">이 작업을 수행 하려면 특수 웹 서비스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-107">In order for this to work, a special web service must be created.</span></span>

## <a name="overview"></a><span data-ttu-id="0e4de-108">개요</span><span class="sxs-lookup"><span data-stu-id="0e4de-108">Overview</span></span>

<span data-ttu-id="0e4de-109">AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="0e4de-110">예를 들어, 한 목록에는 미국 주 목록이 제공 되며 다음 목록에는 해당 상태의 주 도시가 채워집니다. 이 작업을 수행 하려면 특수 웹 서비스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="0e4de-111">단계</span><span class="sxs-lookup"><span data-stu-id="0e4de-111">Steps</span></span>

<span data-ttu-id="0e4de-112">먼저 데이터 원본이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-112">First of all, a data source is required.</span></span> <span data-ttu-id="0e4de-113">이 샘플에서는 AdventureWorks 데이터베이스와 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="0e4de-114">데이터베이스는 Visual Studio 설치 (express edition 포함)의 선택적 부분이 며 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)에서 별도의 다운로드로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="0e4de-115">AdventureWorks 데이터베이스는 SQL Server 2005 샘플 및 예제 데이터베이스 ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)에서 다운로드)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="0e4de-116">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))를 사용 하 고 `AdventureWorks.mdf` 데이터베이스 파일을 연결 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="0e4de-117">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스가 `SQLEXPRESS` 호출 되 고 웹 서버와 같은 컴퓨터에 있는 것으로 가정 합니다. 이는 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="0e4de-118">설정이 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="0e4de-119">ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `ScriptManager` 컨트롤을 배치 해야 합니다 (&lt;`form`&gt; 요소 내).</span><span class="sxs-lookup"><span data-stu-id="0e4de-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample1.aspx)]

<span data-ttu-id="0e4de-120">다음 단계에서는 두 개의 DropDownList 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="0e4de-121">이 샘플에서는 AdventureWorks의 공급 업체 및 연락처 정보를 사용 합니다. 따라서 사용 가능한 공급 업체에 대 한 목록과 사용 가능한 연락처에 대 한 목록을 하나씩 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample2.aspx)]

<span data-ttu-id="0e4de-122">그런 다음 페이지에 두 개의 CascadingDropDown extender를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="0e4de-123">하나는 첫 번째 (공급 업체) 목록을 채우고 다른 하나는 두 번째 (연락처) 목록을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="0e4de-124">다음 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-124">The following attributes must be set:</span></span>

- <span data-ttu-id="0e4de-125">`ServicePath`: 목록 항목을 제공 하는 웹 서비스의 URL</span><span class="sxs-lookup"><span data-stu-id="0e4de-125">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="0e4de-126">`ServiceMethod`: 목록 항목을 전달 하는 웹 메서드</span><span class="sxs-lookup"><span data-stu-id="0e4de-126">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="0e4de-127">`TargetControlID`: 드롭다운 목록의 ID</span><span class="sxs-lookup"><span data-stu-id="0e4de-127">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="0e4de-128">`Category`: 호출 시 웹 메서드에 제출 되는 범주 정보</span><span class="sxs-lookup"><span data-stu-id="0e4de-128">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="0e4de-129">`PromptText`: 서버에서 목록 데이터를 비동기적으로 로드할 때 표시 되는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-129">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>
- <span data-ttu-id="0e4de-130">`ParentControlID`: (선택 사항) 현재 목록의 로드를 트리거하는 부모 드롭다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-130">`ParentControlID`: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="0e4de-131">사용 되는 프로그래밍 언어에 따라 문제의 웹 서비스 이름이 변경 되지만 다른 모든 특성 값은 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="0e4de-132">첫 번째 드롭다운 목록에 대 한 CascadingDropDown 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample3.aspx)]

<span data-ttu-id="0e4de-133">두 번째 목록의 control extender는 공급 업체 목록의 항목을 선택 하 여 연락처 목록에 있는 관련 된 요소를 로드 하도록 하는 `ParentControlID` 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample4.aspx)]

<span data-ttu-id="0e4de-134">실제 작업은 웹 서비스에서 수행 되며 다음과 같이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="0e4de-135">`[ScriptService]` 특성이 사용 됩니다. 그렇지 않으면 AJAX ASP.NET는 클라이언트 쪽 스크립트 코드에서 웹 메서드에 액세스 하기 위한 JavaScript 프록시를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample5.aspx)]

<span data-ttu-id="0e4de-136">CascadingDropDown에서 호출 하는 웹 메서드의 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample6.vb)]

<span data-ttu-id="0e4de-137">따라서 반환 값은 컨트롤 Toolkit에서 정의 되는 `CascadingDropDownNameValue` 형식의 배열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="0e4de-138">`GetVendors()` 메서드는 구현 하기가 매우 쉽습니다. 코드는 AdventureWorks 데이터베이스에 연결 하 고 처음 25 개 공급 업체를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="0e4de-139">`CascadingDropDownNameValue` 생성자의 첫 번째 매개 변수는 목록 항목의 캡션으로, 두 번째 매개 변수는 값 (HTML의 &lt;`option`&gt; 요소의 값 특성)입니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="0e4de-140">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-140">Here is the code:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample7.vb)]

<span data-ttu-id="0e4de-141">공급 업체에 대 한 연결 된 연락처를 가져오는 방법 (메서드 이름: `GetContactsForVendor()`)은 조금 더 까다롭습니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="0e4de-142">먼저 첫 번째 드롭다운 목록에서 선택한 공급 업체를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="0e4de-143">컨트롤 도구 키트는 해당 작업에 대 한 도우미 메서드를 정의 합니다. `ParseKnownCategoryValuesString()` 메서드는 드롭다운 데이터가 포함 된 `StringDictionary` 요소를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample8.vb)]

<span data-ttu-id="0e4de-144">보안상의 이유로이 데이터는 먼저 유효성을 검사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="0e4de-145">따라서 공급 업체 항목이 있는 경우 (첫 번째 CascadingDropDown 요소의 `Category` 속성이 `"Vendor"`)로 설정 되어 있기 때문에 선택한 공급 업체의 ID를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample9.vb)]

<span data-ttu-id="0e4de-146">메서드의 나머지 부분은 매우 단순 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="0e4de-147">공급 업체의 ID는 해당 공급 업체에 대 한 모든 연결 된 연락처를 검색 하는 SQL 쿼리에 대 한 매개 변수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="0e4de-148">다시 한 번, 메서드는 `CascadingDropDownNameValue`형식의 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample10.vb)]

<span data-ttu-id="0e4de-149">ASP.NET 페이지를 로드 하 고, 잠시 후 공급 업체 목록이 25 개 항목으로 채워져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="0e4de-150">한 항목을 선택 하 고 두 번째 드롭다운 목록이 데이터로 채워지는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e4de-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>

<span data-ttu-id="0e4de-151">[첫 번째 목록이 자동으로 채워지는 ![](using-cascadingdropdown-with-a-database-vb/_static/image2.png)](using-cascadingdropdown-with-a-database-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0e4de-151">[![The first list is filled automatically](using-cascadingdropdown-with-a-database-vb/_static/image2.png)](using-cascadingdropdown-with-a-database-vb/_static/image1.png)</span></span>

<span data-ttu-id="0e4de-152">첫 번째 목록이 자동으로 채워집니다 ([전체 크기 이미지를 보려면 클릭](using-cascadingdropdown-with-a-database-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="0e4de-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-vb/_static/image3.png))</span></span>

<span data-ttu-id="0e4de-153">[첫 번째 목록에서 선택한 항목에 따라 두 번째 목록이 채워집니다 ![](using-cascadingdropdown-with-a-database-vb/_static/image5.png)](using-cascadingdropdown-with-a-database-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="0e4de-153">[![The second list is filled according to the selection in the first list](using-cascadingdropdown-with-a-database-vb/_static/image5.png)](using-cascadingdropdown-with-a-database-vb/_static/image4.png)</span></span>

<span data-ttu-id="0e4de-154">첫 번째 목록의 선택 항목에 따라 두 번째 목록이 채워집니다 ([전체 크기 이미지를 보려면 클릭](using-cascadingdropdown-with-a-database-vb/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="0e4de-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0e4de-155">[이전](filling-a-list-using-cascadingdropdown-vb.md)
> [다음](presetting-list-entries-with-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0e4de-155">[Previous](filling-a-list-using-cascadingdropdown-vb.md)
[Next](presetting-list-entries-with-cascadingdropdown-vb.md)</span></span>
