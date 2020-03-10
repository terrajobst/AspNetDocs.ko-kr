---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: ColorPicker 컨트롤 Extender 사용 (VB) | Microsoft Docs
author: microsoft
description: ColorPicker는 팝업 컨트롤에서 UI를 사용 하 여 클라이언트측 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다. ASP.NET에 연결할 수 있습니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 77e2e3bc61a5e1498570959ca40acff83dc3fc82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446585"
---
# <a name="using-the-colorpicker-control-extender-vb"></a><span data-ttu-id="4418b-104">ColorPicker 컨트롤 Extender 사용 (VB)</span><span class="sxs-lookup"><span data-stu-id="4418b-104">Using the ColorPicker Control Extender (VB)</span></span>

<span data-ttu-id="4418b-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="4418b-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4418b-106">ColorPicker는 팝업 컨트롤에서 UI를 사용 하 여 클라이언트측 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="4418b-107">모든 ASP.NET TextBox 컨트롤에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="4418b-108">메서드.</span><span class="sxs-lookup"><span data-stu-id="4418b-108">It.</span></span>

<span data-ttu-id="4418b-109">이 자습서의 목표는 AJAX 컨트롤 Toolkit ColorPicker 컨트롤 extender를 사용 하는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="4418b-110">ColorPicker 컨트롤 extender는 색을 선택할 수 있는 팝업 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="4418b-111">ColorPicker는 사용자가 색을 선택할 수 있는 직관적인 사용자 인터페이스를 제공 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="4418b-112">ColorPicker 컨트롤 Extender를 사용 하 여 TextBox 컨트롤 확장</span><span class="sxs-lookup"><span data-stu-id="4418b-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="4418b-113">예를 들어 방문자가 사용자 지정 된 비즈니스 카드를 만들 수 있는 웹 사이트를 만들려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="4418b-114">방문자는 명함 텍스트를 입력 하 고 색을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="4418b-115">목록 1의 ASP.NET 페이지에는 txt, Text 및 Txt를 색으로 지정 된 두 개의 TextBox 컨트롤이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="4418b-116">양식을 제출 하면 선택한 값이 표시 됩니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="4418b-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>

<span data-ttu-id="4418b-117">[비즈니스 카드를 만들기 위한 단순 양식 ![](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4418b-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span></span>

<span data-ttu-id="4418b-118">**그림 01**: 회사 카드를 만드는 간단한 양식 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="4418b-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image2.png))</span></span>

<span data-ttu-id="4418b-119">**목록 1-CreateCard .aspx**</span><span class="sxs-lookup"><span data-stu-id="4418b-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

<span data-ttu-id="4418b-120">목록 1의 양식은 작동 하지만 뛰어난 사용자 환경을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="4418b-121">사용자가 텍스트 상자에 색을 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="4418b-122">사용자가 특별 한 색 (예: pea green의 오른쪽 음영)을 원하는 경우에는 사용자가 도움말이 없는 HTML 색 코드를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="4418b-123">ColorPicker 컨트롤 extender를 사용 하 여 더 나은 사용자 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="4418b-124">텍스트 상자 컨트롤에 포커스를 이동할 때 ColorPicker는 색 대화 상자를 표시 합니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="4418b-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>

<span data-ttu-id="4418b-125">[ColorPicker 컨트롤 Extender를 ![합니다.](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4418b-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span></span>

<span data-ttu-id="4418b-126">**그림 02**: Colorpicker 컨트롤 Extender ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="4418b-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image4.png))</span></span>

<span data-ttu-id="4418b-127">목록 1의 양식과 함께 ColorPicker 컨트롤 extender를 사용 하려면 두 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="4418b-128">페이지에 ScriptManager 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="4418b-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="4418b-129">페이지에 ColorPicker 컨트롤 extender 추가</span><span class="sxs-lookup"><span data-stu-id="4418b-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="4418b-130">ColorPicker를 사용 하려면 페이지에 ScriptManager를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="4418b-131">ScriptManager를 추가 하는 좋은 장소는 서버 쪽 &lt;양식&gt; 태그를 여는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="4418b-132">ScriptManager를 도구 상자에서 페이지로 끌어올 수 있습니다 (ScriptManager는 AJAX 확장 탭 아래에 있음).</span><span class="sxs-lookup"><span data-stu-id="4418b-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="4418b-133">또는 서버 쪽 양식 열기 태그 아래에서 소스 뷰에 다음 태그를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="4418b-134">&lt;asp: ScriptManager ID = "ScriptManager1" runat = "server"/&gt;</span><span class="sxs-lookup"><span data-stu-id="4418b-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="4418b-135">ColorPicker 컨트롤 extender를 페이지에 추가 하는 가장 쉬운 방법은 디자인 뷰입니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="4418b-136">Txt카드 색 텍스트 상자 위로 마우스를 가져가면 스마트 작업 옵션이 표시 되어 extender를 추가할 수 있습니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="4418b-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="4418b-137">이 옵션을 선택 하면 Extender 마법사가 나타납니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="4418b-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>

<span data-ttu-id="4418b-138">[extender를 추가 ![](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="4418b-138">[![Adding an extender](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span></span>

<span data-ttu-id="4418b-139">**그림 03**: extender 추가 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="4418b-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image6.png))</span></span>

<span data-ttu-id="4418b-140">[Extender 마법사를 사용 하 여 컨트롤 extender를 선택 ![](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="4418b-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="4418b-141">**그림 04**: extender 마법사를 사용 하 여 컨트롤 extender 선택 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="4418b-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image8.png))</span></span>

<span data-ttu-id="4418b-142">Colorpicker extender를 선택 하 여 ColorPicker 색 텍스트 상자를 ColorPicker extender로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="4418b-143">확인을 클릭하여 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="4418b-144">이러한 변경을 수행한 후에는 페이지의 소스가 목록 2 처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="4418b-145">**목록 2-CreateCard (ColorPicker 사용)**</span><span class="sxs-lookup"><span data-stu-id="4418b-145">**Listing 2 - CreateCard.aspx (with ColorPicker)**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

<span data-ttu-id="4418b-146">이제 페이지에 txtCardColor TextBox 컨트롤 바로 아래에 표시 되는 Color Kerextender 컨트롤이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="4418b-147">ColorPickerExtender 컨트롤은 색 선택 대화 상자를 표시 하도록 Txt의 색 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="4418b-148">단추를 사용 하 여 색 선택 대화 상자 시작</span><span class="sxs-lookup"><span data-stu-id="4418b-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="4418b-149">ColorPicker extender는 다음 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="4418b-150">PopupButtonId-색 선택 대화 상자를 표시 하는 페이지의 단추 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="4418b-151">PopupPosition-색 선택 대화 상자의 대상 컨트롤에 상대적인 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="4418b-152">가능한 값은 Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right 및 Left (기본값은 BottomLeft)입니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="4418b-153">SampleControlId-선택한 색을 표시 하는 컨트롤의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="4418b-154">SelectedColor-ColorPicker에서 선택한 첫 번째 색입니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="4418b-155">이러한 속성을 사용 하 여 색 선택 대화 상자를 표시 하는 방법과 선택한 색을 표시 하는 방법을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="4418b-156">목록 3의 페이지는 이러한 속성 중 일부를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="4418b-157">**목록 3-CreateCardButton**</span><span class="sxs-lookup"><span data-stu-id="4418b-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

<span data-ttu-id="4418b-158">목록 3의 페이지에는 선택 색 단추가 있습니다 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="4418b-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="4418b-159">이 단추를 클릭 하면 텍스트 상자 위에 색 선택 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="4418b-160">대화 상자에서 색을 선택 하면 선택한 색이 lblSample Label 컨트롤의 배경색으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="4418b-161">ColorPicker PopupButtonID 속성은 색 선택 단추를 ColorPicker extender와 연결 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="4418b-162">PopupButtonID 속성에 대 한 값을 제공 하면 대상 컨트롤에 포커스가 있을 때 색 선택 대화 상자가 더 이상 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="4418b-163">대화 상자를 표시 하려면 단추를 클릭 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="4418b-164">SampleControlID 속성은 선택 된 색을 표시 하는 컨트롤을 ColorPicker와 연결 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="4418b-165">ColorPicker는이 컨트롤의 배경색을 현재 선택 된 색으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>

<span data-ttu-id="4418b-166">[단추를 사용 하 여 색 선택 대화 상자를 표시 ![](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="4418b-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span></span>

<span data-ttu-id="4418b-167">**그림 05**: 단추를 사용 하 여 색 선택 대화 상자 표시 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="4418b-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image10.png))</span></span>

## <a name="summary"></a><span data-ttu-id="4418b-168">요약</span><span class="sxs-lookup"><span data-stu-id="4418b-168">Summary</span></span>

<span data-ttu-id="4418b-169">이 자습서에서는 ColorPicker 컨트롤 extender를 사용 하 여 팝업 색 선택 대화 상자를 표시 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="4418b-170">먼저 포커스가 TextBox 컨트롤로 이동 될 때 대화 상자를 표시할 수 있는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="4418b-171">다음으로 단추를 클릭할 때 색 선택 대화 상자를 표시 하는 단추를 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4418b-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4418b-172">이전</span><span class="sxs-lookup"><span data-stu-id="4418b-172">Previous</span></span>](using-the-colorpicker-control-extender-cs.md)
