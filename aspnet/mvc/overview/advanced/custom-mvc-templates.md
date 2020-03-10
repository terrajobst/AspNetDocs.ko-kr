---
uid: mvc/overview/advanced/custom-mvc-templates
title: 사용자 지정 MVC 템플릿 | Microsoft Docs
author: joeloff
description: 템플릿을 VSIX 확장으로 만듭니다.
ms.author: riande
ms.date: 12/10/2012
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 0603bc24e070e223551813f66a75889a2e46fd35
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499601"
---
# <a name="custom-mvc-template"></a><span data-ttu-id="3e74e-103">사용자 지정 MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="3e74e-103">Custom MVC Template</span></span>

<span data-ttu-id="3e74e-104">[Jacques Eloff](https://github.com/joeloff)</span><span class="sxs-lookup"><span data-stu-id="3e74e-104">by [Jacques Eloff](https://github.com/joeloff)</span></span>

<span data-ttu-id="3e74e-105">Visual Studio 2010에 대 한 MVC 3 Tools 업데이트 릴리스에는 MVC 프로젝트에 대 한 별도의 프로젝트 마법사가 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-105">The release of MVC 3 Tools Update for Visual Studio 2010 introduced a separate project wizard for MVC projects.</span></span> <span data-ttu-id="3e74e-106">변경 내용은 두 가지 요소에 의해 결정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-106">The change was driven by two factors.</span></span> <span data-ttu-id="3e74e-107">먼저 MVC 3의 새로운 템플릿이 도입 되었으며 Razor와 같은 추가 뷰 엔진을 지원 하 여 Visual Studio의 새 프로젝트 대화 상자를 overcrowding.</span><span class="sxs-lookup"><span data-stu-id="3e74e-107">First, the introduction of new templates in MVC 3 and support for additional view engines such as Razor lead to overcrowding the New Project dialog in Visual Studio.</span></span> <span data-ttu-id="3e74e-108">둘째, 고객은 확장성을 요청 하 고 새 MVC 프로젝트 마법사에서 이러한 요청에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-108">Second, customers had been asking for extensibility points and the new MVC project wizard would afford us the opportunity to respond to these requests.</span></span>

<span data-ttu-id="3e74e-109">사용자 지정 템플릿 추가는 레지스트리를 사용 하 여 MVC 프로젝트 마법사에 새 템플릿을 표시 하는 데 사용 되는 단절 프로세스 였습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-109">Adding custom templates was an arduous process that relied on using the registry to make new templates visible to the MVC project wizard.</span></span> <span data-ttu-id="3e74e-110">새 템플릿의 작성자는 설치 시 필요한 레지스트리 항목을 만들 수 있도록 MSI 내에이를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-110">The author of a new template had to wrap it inside an MSI to ensure that the necessary registry entries would be created at install time.</span></span> <span data-ttu-id="3e74e-111">대신, 사용 가능한 템플릿을 포함 하는 ZIP 파일을 만들고 최종 사용자가 필요한 레지스트리 항목을 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-111">The alternative was to make a ZIP file containing the template available and have the end-user create the required registry entries by hand.</span></span>

<span data-ttu-id="3e74e-112">앞서 언급 한 방법은 모두 적절 하지 않으므로 [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) 확장에서 제공 하는 기존 인프라 중 일부를 활용 하 여 Visual Studio 2012에 대 한 mvc 4부터 사용자 지정 mvc 템플릿을 더 쉽게 작성 하 고 배포 하 고 설치할 수 있도록 결정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-112">Neither of the aforementioned approaches is ideal so we decided to leverage some of the existing infrastructure provided by [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) extensions to make it easier to author, distribute and install custom MVC templates starting with MVC 4 for Visual Studio 2012.</span></span> <span data-ttu-id="3e74e-113">이 방법에서 제공 하는 몇 가지 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-113">Some of the benefits provided by this approach are:</span></span>

- <span data-ttu-id="3e74e-114">VSIX 확장에는 여러 언어 (C# 및 Visual Basic)와 여러 개의 뷰 엔진 (ASPX 및 Razor)을 지 원하는 여러 템플릿이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-114">A VSIX extension can contain multiple templates that support different languages (C# and Visual Basic) and multiple view engines (ASPX and Razor).</span></span>
- <span data-ttu-id="3e74e-115">VSIX 확장은 Express Sku를 비롯 한 여러 Sku의 Visual Studio를 대상으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-115">A VSIX extension can target multiple SKUs of Visual Studio including Express SKUs.</span></span>
- <span data-ttu-id="3e74e-116">[Visual Studio 갤러리](https://visualstudiogallery.msdn.microsoft.com/) 는 광범위 한 대상에 확장을 배포 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-116">The [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/) facilitates distributing the extension to a wide audience.</span></span>
- <span data-ttu-id="3e74e-117">VSIX 확장을 업그레이드 하 여 사용자 지정 템플릿에 대 한 수정 및 업데이트를 더 쉽게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-117">VSIX extensions can be upgraded making it easier to author corrections and updates to your custom templates.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e74e-118">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="3e74e-118">Prerequisites</span></span>

- <span data-ttu-id="3e74e-119">사용자는 .vstemplate 파일 등에 필요한 태그를 포함 하 여 프로젝트 템플릿 제작에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-119">Users need to be familiar with authoring project templates, including the required markup for vstemplate files, etc.</span></span>
- <span data-ttu-id="3e74e-120">사용자는 Visual Studio Professional 이상 버전이 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-120">Users will need to have Visual Studio Professional and higher installed.</span></span> <span data-ttu-id="3e74e-121">Express Sku는 VSIX 프로젝트 만들기를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-121">Express SKUs do not support creating VSIX projects.</span></span>
- <span data-ttu-id="3e74e-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) 가 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) installed.</span></span>

## <a name="example"></a><span data-ttu-id="3e74e-123">예제</span><span class="sxs-lookup"><span data-stu-id="3e74e-123">Example</span></span>

<span data-ttu-id="3e74e-124">첫 번째 단계는 C# 또는 Visual Basic를 사용 하 여 새 VSIX 프로젝트를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-124">The first step is to create a new VSIX project using either C# or Visual Basic.</span></span> <span data-ttu-id="3e74e-125">**파일 > 새 프로젝트**를 선택 하 고 왼쪽 창에서 **확장성** 을 클릭 한 다음 **VSIX 프로젝트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-125">Select **File > New Project**, then click **Extensibility** in the left pane and select the **VSIX Project**.</span></span>

![새 프로젝트](custom-mvc-templates/_static/image1.jpg)

<span data-ttu-id="3e74e-127">프로젝트를 만든 후 VSIX 디자이너가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-127">After the project is created, the VSIX designer will be opened.</span></span>

![프로젝트 디자이너 메타 데이터](custom-mvc-templates/_static/image2.jpg)

<span data-ttu-id="3e74e-129">디자이너를 사용 하 여 확장을 설치 하거나 Visual Studio에서 설치 된 확장 (**도구 > 확장 및 업데이트**)을 찾아볼 때 사용자에 게 표시 되는 확장의 일반 속성 중 일부를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-129">The designer can be used to edit some of the general properties of the extension that will be shown to users when they install the extension or browse the installed extensions in Visual Studio (**Tools > Extensions and Updates**).</span></span> <span data-ttu-id="3e74e-130">일반 정보를 완료 한 후에는 **설치 대상 탭**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-130">Once you have completed the general information click on the **Install Targets tab**.</span></span>

![프로젝트 디자이너 설치 대상](custom-mvc-templates/_static/image3.jpg)

<span data-ttu-id="3e74e-132">이 탭은 확장에서 지원 되는 Visual Studio의 Sku 및 버전을 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-132">This tab is used to specify the SKUs and versions of Visual Studio that are supported by your extension.</span></span> <span data-ttu-id="3e74e-133">**모든 사용자가** vsix의 컴퓨터별 설치를 사용 하도록 설정 하려면이 vsix에 대 한 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-133">Select the checkbox for **This VSIX is installed for all users** to enable per-machine installs of the VSIX.</span></span> <span data-ttu-id="3e74e-134">오른쪽에 있는 **새로 만들기** 단추를 클릭 하 여 VWD (Web Developer Express)와 같은 sku를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-134">Click on the **New** button on the right to add additional SKUs such as Web Developer Express (VWD).</span></span>

![새 설치 대상 추가](custom-mvc-templates/_static/image4.jpg)

<span data-ttu-id="3e74e-136">Professional, Premium 및 Ultimate를 모두 지원 하려는 경우에는 **Microsoft.VisualStudio.Pro**제품군에서 최소 sku를 선택 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-136">If you intend to support all the Professional and higher SKUs (Professional, Premium and Ultimate) you only need to select the minimum SKU in the family, **Microsoft.VisualStudio.Pro**.</span></span> <span data-ttu-id="3e74e-137">설치 대상을 완료 한 후 모든 변경 내용을 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-137">Remember to save all your changes once you have completed the Install Targets.</span></span>

![프로젝트 디자이너 설치 대상](custom-mvc-templates/_static/image5.jpg)

<span data-ttu-id="3e74e-139">**자산** 탭은 VSIX에 모든 콘텐츠 파일을 추가 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-139">The **Assets** tab is used to add all your content files to the VSIX.</span></span> <span data-ttu-id="3e74e-140">MVC에는 사용자 지정 메타 데이터가 필요 하므로 **자산** 탭을 사용 하 여 콘텐츠를 추가 하는 대신 VSIX 매니페스트 파일의 원시 XML을 편집 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-140">Since MVC requires custom metadata you will be editing the raw XML of the VSIX manifest file instead of using the **Assets** tab to add content.</span></span> <span data-ttu-id="3e74e-141">먼저 VSIX 프로젝트에 템플릿 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-141">Start by adding the template contents to the VSIX project.</span></span> <span data-ttu-id="3e74e-142">폴더와 콘텐츠의 구조가 프로젝트의 레이아웃을 반영 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-142">It is important that the structure of the folder and the contents mirror the layout of the project.</span></span> <span data-ttu-id="3e74e-143">아래 예제에는 기본 MVC 프로젝트 템플릿에서 파생 된 네 개의 프로젝트 템플릿이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-143">The example below contains four project templates that were derived from the Basic MVC project template.</span></span> <span data-ttu-id="3e74e-144">프로젝트 템플릿 (ProjectTemplates 폴더 아래의 모든 항목)을 구성 하는 모든 파일이 VSIX 프로젝트 파일의 **콘텐츠** itemgroup에 추가 되 고 아래 예제와 같이 각 항목에 **CopyToOutputDirectory** 및 **IncludeInVsix** 메타 데이터 집합이 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-144">Make sure that all the files that comprise your project template (everything underneath the ProjectTemplates folder) are added to the **Content** itemgroup in the VSIX project file and that each item contains the **CopyToOutputDirectory** and **IncludeInVsix** metadata set as shown in the example below.</span></span>

<span data-ttu-id="3e74e-145">&lt;Content는 =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="3e74e-145">&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span></span>

<span data-ttu-id="3e74e-146">&lt;CopyToOutputDirectory&gt;항상&lt;/CopyToOutputDirectory&gt;</span><span class="sxs-lookup"><span data-stu-id="3e74e-146">&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;</span></span>

<span data-ttu-id="3e74e-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span><span class="sxs-lookup"><span data-stu-id="3e74e-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span></span>

<span data-ttu-id="3e74e-148">&lt;/콘텐츠&gt;</span><span class="sxs-lookup"><span data-stu-id="3e74e-148">&lt;/Content&gt;</span></span>

<span data-ttu-id="3e74e-149">그렇지 않으면 VSIX를 빌드할 때 IDE에서 템플릿의 내용을 컴파일하려고 시도 하므로 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-149">If not, the IDE will try to compile the contents of the template when you build the VSIX and you will likely see an error.</span></span> <span data-ttu-id="3e74e-150">템플릿의 코드 파일에는 프로젝트 템플릿이 인스턴스화되어 IDE에서 컴파일할 수 없는 경우 Visual Studio에서 사용 하는 특수 [템플릿 매개 변수가](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) 포함 되어 있는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-150">Code files in templates often contain special [template parameters](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) used by Visual Studio when the project template is instantiated and therefore cannot be compiled in the IDE.</span></span>

![솔루션 탐색기](custom-mvc-templates/_static/image6.jpg)

<span data-ttu-id="3e74e-152">VSIX 디자이너를 닫은 다음 **솔루션 탐색기** 에서 **소스 확장명 .manifest** 파일을 마우스 오른쪽 단추로 클릭 하 고 **연결 프로그램** 을 선택 하 고 **XML (텍스트) 편집기** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-152">Close the VSIX designer, then right click on the **source.extension.manifest** file in **Solution Explorer** and select **Open With** and choose the **XML (Text) Editor** option.</span></span>

![연결 프로그램 대화 상자](custom-mvc-templates/_static/image7.jpg)

<span data-ttu-id="3e74e-154">**&lt;자산&gt;** 요소를 만들고 VSIX에 포함 되어야 하는 각 파일에 대 한 **&lt;Asset&gt;** 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-154">Create an **&lt;Assets&gt;** element and add an **&lt;Asset&gt;** element for each file that must be included in the VSIX.</span></span> <span data-ttu-id="3e74e-155">각 **&lt;Asset&gt;** 요소의 **Type** 특성은 **VisualStudio**로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-155">The **Type** attribute of each **&lt;Asset&gt;** element must be set to **Microsoft.VisualStudio.Mvc.Template**.</span></span> <span data-ttu-id="3e74e-156">MVC 프로젝트 마법사 에서만 이해 하는 사용자 지정 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-156">This is a custom namespace that only the MVC project wizard understands.</span></span> <span data-ttu-id="3e74e-157">매니페스트 파일의 구조와 레이아웃에 대 한 자세한 내용은 VSIX 2.0 스키마 설명서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3e74e-157">Refer to the VSIX 2.0 Schema documentation for additional information on the structure and layout of the manifest file.</span></span>

<span data-ttu-id="3e74e-158">VSIX에 파일을 추가 하는 것 만으로는 MVC 마법사를 사용 하 여 템플릿을 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-158">Just adding the files to the VSIX is not sufficient to register the templates with the MVC wizard.</span></span> <span data-ttu-id="3e74e-159">MVC 마법사에 템플릿 이름, 설명, 지원 되는 뷰 엔진 및 프로그래밍 언어와 같은 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-159">You need to provide information such as the template name, description, supported view engines and programming language to the MVC wizard.</span></span> <span data-ttu-id="3e74e-160">이 정보는 각 **.vstemplate** 파일에 대 한 **&lt;Asset&gt;** 요소와 연결 된 사용자 지정 특성으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-160">This information is carried in custom attributes associated with the **&lt;Asset&gt;** element for each **vstemplate** file.</span></span>

<span data-ttu-id="3e74e-161">&lt;Asset d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span><span class="sxs-lookup"><span data-stu-id="3e74e-161">&lt;Asset d:VsixSubPath=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span></span>

<span data-ttu-id="3e74e-162">=&quot;VisualStudio를 입력&quot;</span><span class="sxs-lookup"><span data-stu-id="3e74e-162">Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;</span></span>

<span data-ttu-id="3e74e-163">d:Source =&quot;파일&quot;</span><span class="sxs-lookup"><span data-stu-id="3e74e-163">d:Source=&quot;File&quot;</span></span>

<span data-ttu-id="3e74e-164">경로 =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span><span class="sxs-lookup"><span data-stu-id="3e74e-164">Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span></span>

<span data-ttu-id="3e74e-165">ProjectType =&quot;MVC&quot;</span><span class="sxs-lookup"><span data-stu-id="3e74e-165">ProjectType=&quot;MVC&quot;</span></span>

<span data-ttu-id="3e74e-166">Language =&quot;C#&quot;</span><span class="sxs-lookup"><span data-stu-id="3e74e-166">Language=&quot;C#&quot;</span></span>

<span data-ttu-id="3e74e-167">ViewEngine =&quot;Aspx&quot;</span><span class="sxs-lookup"><span data-stu-id="3e74e-167">ViewEngine=&quot;Aspx&quot;</span></span>

<span data-ttu-id="3e74e-168">TemplateId =&quot;MyMvcApplication&quot;</span><span class="sxs-lookup"><span data-stu-id="3e74e-168">TemplateId=&quot;MyMvcApplication&quot;</span></span>

<span data-ttu-id="3e74e-169">Title =&quot;사용자 지정 기본 웹 응용 프로그램&quot;</span><span class="sxs-lookup"><span data-stu-id="3e74e-169">Title=&quot;Custom Basic Web Application&quot;</span></span>

<span data-ttu-id="3e74e-170">Description = 기본 MVC 웹 응용 프로그램 (Razor)에서 파생 된 사용자 지정 템플릿을&quot;&quot;</span><span class="sxs-lookup"><span data-stu-id="3e74e-170">Description=&quot;A custom template derived from a Basic MVC web application (Razor)&quot;</span></span>

<span data-ttu-id="3e74e-171">Version =&quot;4.0&quot;/&gt;</span><span class="sxs-lookup"><span data-stu-id="3e74e-171">Version=&quot;4.0&quot;/&gt;</span></span>

<span data-ttu-id="3e74e-172">다음은 표시 해야 하는 사용자 지정 특성에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-172">Below is an explanation of the custom attributes that must be present:</span></span>

- <span data-ttu-id="3e74e-173">**ProjectType** 는 MVC로 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-173">**ProjectType** must be set to MVC.</span></span>
- <span data-ttu-id="3e74e-174">**Language** 는 템플릿에서 지 원하는 개발 언어를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-174">**Language** designates the development language supported by the template.</span></span> <span data-ttu-id="3e74e-175">유효한 값은 C# 또는 VB입니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-175">Valid values are either C# or VB.</span></span>
- <span data-ttu-id="3e74e-176">**Viewengine** 은 Aspx 또는 Razor와 같이 템플릿에서 지원 되는 뷰 엔진을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-176">**ViewEngine** designates the view engine supported by the template such as Aspx or Razor.</span></span> <span data-ttu-id="3e74e-177">이 필드에 대 한 사용자 지정 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-177">You can specify a custom value for this field.</span></span>
- <span data-ttu-id="3e74e-178">**TemplateId** 는 템플릿을 그룹화 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-178">**TemplateId** is used for grouping the templates.</span></span> <span data-ttu-id="3e74e-179">값이 기존 템플릿 ID와 일치 하는 경우 이전에 MVC 마법사에 등록 된 템플릿이 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-179">If the value matches an existing template ID it will be override templates previously registered with the MVC wizard.</span></span>
- <span data-ttu-id="3e74e-180">**제목** 각 프로젝트 템플릿 아래에서 MVC 마법사에 표시 되는 간단한 설명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-180">**Title** designates the short description displayed in the MVC wizard beneath each project template.</span></span>
- <span data-ttu-id="3e74e-181">**설명** 템플릿에 대 한 보다 자세한 설명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-181">**Description** designates a more verbose description of the template.</span></span>

<span data-ttu-id="3e74e-182">모든 파일을 매니페스트에 추가 하 고 저장 한 후에는 디자이너의 **자산** 탭에 모든 파일이 표시 되지만, **.vstemplate** 파일에 대 한 **&lt;자산&gt;** 요소에 추가한 사용자 지정 특성은 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-182">After you have added all the files to the manifest and saved it, you will notice that the **Assets** tab in the designer will display all the files, but not the custom attributes you added to the **&lt;Asset&gt;** elements for the **vstemplate** files.</span></span>

![프로젝트 디자이너 자산](custom-mvc-templates/_static/image8.jpg)

<span data-ttu-id="3e74e-184">이제 VSIX 프로젝트를 컴파일하여 설치 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-184">All that remains now is to compile the VSIX project and install it.</span></span>

<span data-ttu-id="3e74e-185">VSIX 확장을 테스트 하려는 컴퓨터에서 Visual Studio의 모든 인스턴스가 닫혀 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-185">Make sure that all instances of Visual Studio are closed on the machine where you intend to test the VSIX extension.</span></span> <span data-ttu-id="3e74e-186">Visual Studio는 시작 하는 동안 새 확장을 검색 하므로 VSIX를 설치 하는 동안 IDE가 열려 있으면 Visual Studio를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-186">Visual Studio scans for new extensions during startup, so if the IDE is open while installing a VSIX you will need to restart Visual Studio.</span></span> <span data-ttu-id="3e74e-187">탐색기에서 vsix 파일을 두 번 클릭 하 여 **Vsix 설치 관리자**를 시작 하 고 **설치** 를 클릭 한 다음 Visual Studio를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-187">In Explorer, double click on the VSIX file to launch the **VSIX Installer**, click **Install** and then launch Visual Studio.</span></span>

![VSIX 설치 관리자](custom-mvc-templates/_static/image9.jpg)

<span data-ttu-id="3e74e-189">메뉴에서 **도구 > 확장 및 업데이트** 를 선택 하 여 확장이 설치 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-189">From the menu, select **Tools > Extensions and Updates** to confirm that your extension was installed.</span></span> <span data-ttu-id="3e74e-190">확장을 설치 하는 동안 VSIX 설치 관리자에서 오류를 보고 한 경우 VSIX 설치 관리자 로그에서 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-190">If the VSIX Installer reported any errors during the installation of the extension you can view the VSIX Installer log for more information.</span></span> <span data-ttu-id="3e74e-191">일반적으로 로그는 확장을 설치한 사용자의 **% temp%** 폴더에 생성 됩니다 (예: **C:\Users\Bob\AppData\Local\Temp**).</span><span class="sxs-lookup"><span data-stu-id="3e74e-191">The log is usually created in the **%temp%** folder of the user that installed the extension, for example **C:\Users\Bob\AppData\Local\Temp**.</span></span>

![확장 및 업데이트](custom-mvc-templates/_static/image10.jpg)

<span data-ttu-id="3e74e-193">창을 닫은 후 mvc 4 프로젝트를 만들어 새 템플릿이 MVC 마법사에 표시 되는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-193">After closing the window you can create an MVC 4 project to see whether your new templates are shown in the MVC wizard.</span></span>

![새 ASP.NET MVC 4 프로젝트](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a><span data-ttu-id="3e74e-195">제한 사항</span><span class="sxs-lookup"><span data-stu-id="3e74e-195">Limitations</span></span>

1. <span data-ttu-id="3e74e-196">MVC 마법사는 지역화 된 사용자 지정 템플릿을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-196">The MVC wizard does not support localized custom templates.</span></span>
2. <span data-ttu-id="3e74e-197">사용자 지정 템플릿을 찾지 못하면 마법사에서 오류를 보고 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-197">The wizard will not report any errors if it fails to locate custom templates.</span></span> <span data-ttu-id="3e74e-198">필요한 사용자 지정 특성 중 하나가 없는 경우 템플릿은 마법사에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e74e-198">If any of the required custom attributes are absent, the template would simply be excluded from the Wizard.</span></span>
