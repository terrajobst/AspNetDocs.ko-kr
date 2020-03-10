---
uid: whitepapers/denied-access-to-iis-directories
title: IIS 디렉터리에 대 한 액세스 거부 ASP.NET | Microsoft Docs
author: rick-anderson
description: 이 백서에서는 ASP.NET 응용 프로그램에 대 한 요청이 "DirectoryName 디렉터리에 대 한 액세스 거부" 오류를 반환 하는 경우 수행 해야 하는 작업에 대해 설명 합니다. 실패 ...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: a3a53aa88abbe1bcaaea7d691406800c8f9b988b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518573"
---
# <a name="aspnet-denied-access-to-iis-directories"></a><span data-ttu-id="eaa79-104">ASP.NET에서 IIS 디렉터리에 대한 액세스 거부</span><span class="sxs-lookup"><span data-stu-id="eaa79-104">ASP.NET Denied Access to IIS Directories</span></span>

> <span data-ttu-id="eaa79-105">이 백서에서는 ASP.NET 응용 프로그램에 대 한 요청이 " *DirectoryName* 디렉터리에 대 한 액세스 거부" 오류를 반환 하는 경우 수행 해야 하는 작업에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-105">This whitepaper describes what you must do if a request to your ASP.NET application returns the error, "Denied Access to *DirectoryName* directory.</span></span> <span data-ttu-id="eaa79-106">디렉터리 변경 내용 모니터링을 시작 하지 못했습니다. "</span><span class="sxs-lookup"><span data-stu-id="eaa79-106">Failed to start monitoring directory changes."</span></span>
> 
> <span data-ttu-id="eaa79-107">ASP.NET 1.0 및 ASP.NET 1.1에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-107">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="eaa79-108">이제 ASP.NET V1 RTM은 로컬 컴퓨터에서 "ASPNET" 계정으로 등록 된 낮은 권한의 windows 계정을 사용 하 여 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-108">ASP.NET V1 RTM now runs using a less privileged windows account - registered as the "ASPNET" account on a local machine.</span></span>

<span data-ttu-id="eaa79-109">일부 잠겨 있는 시스템에서이 계정에는 웹 사이트의 콘텐츠 디렉터리, 응용 프로그램 루트 디렉터리 또는 웹 사이트 루트 디렉터리에 대 한 읽기 보안 액세스 권한이 기본적으로 포함 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-109">On some locked down systems, this account may not by default have read security access to a website's content directories, the application root directory, or the web site root directory.</span></span> <span data-ttu-id="eaa79-110">이 경우 지정 된 웹 응용 프로그램에서 페이지를 요청할 때 다음 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-110">In this case you will receive the following error when requesting pages from a given web application:</span></span>

![](denied-access-to-iis-directories/_static/image1.jpg)

<span data-ttu-id="eaa79-111">이 문제를 해결 하려면 해당 디렉터리에 대 한 보안 권한을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-111">To fix this you will need to change the security permissions on the appropriate directories.</span></span>

<span data-ttu-id="eaa79-112">특히 ASP.NET에는 웹 사이트 루트에 대 한 ASPNET 계정 (예: c:\inetpub\wwwroot 또는 IIS에서 구성한 다른 사이트 디렉터리)에 대 한 읽기, 실행 및 목록 액세스 권한이 필요 합니다. 콘텐츠 디렉터리 및 응용 프로그램 루트 디렉터리 구성 파일 변경을 모니터링 하기 위해</span><span class="sxs-lookup"><span data-stu-id="eaa79-112">Specifically, ASP.NET requires read, execute, and list access for the ASPNET account for the web site root (for example: c:\inetpub\wwwroot or any alternative site directory you may have configured in IIS), the content directory and the application root directory in order to monitor for configuration file changes.</span></span> <span data-ttu-id="eaa79-113">응용 프로그램 루트는 IIS 관리 도구 (inetmgr)의 응용 프로그램 가상 디렉터리와 연결 된 폴더 경로에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-113">The application root corresponds to the folder path associated with the application virtual directory in the IIS Administration tool (inetmgr).</span></span>

<span data-ttu-id="eaa79-114">예를 들어 wwwroot 폴더에 있는 다음 응용 프로그램 계층 구조를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="eaa79-114">For example, consider the following application hierarchy under the wwwroot folder.</span></span>

`C:\inetpub\wwwroot\myapp\default.aspx`

<span data-ttu-id="eaa79-115">이 예의 경우 ASPNET 계정에는 myapp 및 wwwroot 디렉터리의 콘텐츠에 대해 위에서 정의한 읽기 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-115">For this example, the ASPNET account needs the read permissions defined above for content in both the myapp and the wwwroot directory.</span></span> <span data-ttu-id="eaa79-116">루트 폴더에 대해 상속 된 단일 ACL이 중첩 된 경우 두 디렉터리 모두에 대해 선택적으로 사용 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-116">A single inherited ACL on the root folder can also be optionally used for both directories if they're nested.</span></span>

<span data-ttu-id="eaa79-117">디렉터리에 사용 권한을 추가 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-117">To add permissions to a directory, perform the following steps:</span></span>

- <span data-ttu-id="eaa79-118">Windows 탐색기를 사용 하 여 디렉터리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-118">Using the Windows explorer, navigate to the directory</span></span>
- <span data-ttu-id="eaa79-119">디렉터리 폴더를 마우스 오른쪽 단추로 클릭 하 고 "속성"을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-119">Right click on the directory folder and choose "Properties"</span></span>
- <span data-ttu-id="eaa79-120">속성 대화 상자에서 "보안" 탭으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-120">Navigate to the "Security" tab on the property dialog</span></span>
- <span data-ttu-id="eaa79-121">"추가" 단추를 클릭 하 고 컴퓨터 이름, ASPNET 계정 이름을 차례로 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-121">Click the "Add" button and enter the machine name followed by the ASPNET account name.</span></span> <span data-ttu-id="eaa79-122">예를 들어 "webdev" 라는 컴퓨터에서 webdev\ASPNET를 입력 하 고 "OK"를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-122">For example, on a machine named "webdev", you would enter webdev\ASPNET and hit "OK".</span></span>
- <span data-ttu-id="eaa79-123">ASPNET 계정에 "읽기 &amp; 실행", "폴더 내용 나열" 및 "읽기" 확인란이 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-123">Ensure that the ASPNET account has the "Read &amp; Execute", "List Folder Contents", and "Read" checkboxes checked.</span></span>
- <span data-ttu-id="eaa79-124">확인을 눌러 대화 상자를 닫고 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-124">Hit OK to dismiss the dialog and save the changes.</span></span>

![](denied-access-to-iis-directories/_static/image2.jpg)

<span data-ttu-id="eaa79-125">원하는 경우 이러한 변경 내용은 Windows와 함께 제공 되는 "cacls.exe" 도구나 스크립트를 사용 하 여 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-125">If desired, these changes can be automated using scripts or the "cacls.exe" tool that ships with Windows.</span></span> <span data-ttu-id="eaa79-126">ASPNET 계정에 대 한 자세한 내용은 [FAQ 문서](https://go.microsoft.com/fwlink/?LinkId=5828)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="eaa79-126">For more information on the ASPNET account, please see the [FAQ document](https://go.microsoft.com/fwlink/?LinkId=5828).</span></span>

<span data-ttu-id="eaa79-127">지정 된 웹 응용 프로그램에서 특정 폴더 또는 파일에 대 한 쓰기 또는 수정 권한을 사용 하는 경우 동일한 절차를 수행 하 고 "쓰기" 및/또는 "수정" 확인란을 선택 하 여이 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-127">If a given web application relies on having write or modify permissions to a particular folder or file, this can be granted by following the same procedure and checking the "Write" and/or "Modify" checkboxes.</span></span>

<span data-ttu-id="eaa79-128">모든 사용자 또는 사용자 그룹에 게 이러한 디렉터리 (기본 구성)에 대 한 읽기 액세스를 허용 하는 컴퓨터에서는 문제가 발생 하지 않으며 위의 단계가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa79-128">On machines that allow Everyone or the Users group read access to these directories (which is the default configuration), no issues will be encountered and the above steps will not be required.</span></span>
