---
uid: web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
title: '[방법:] AJAX 페이지 업데이트의 메서드 중에서 선택 합니다. | Microsoft Docs'
author: JoeStagner
description: 이 비디오에서 Joe Stagner는 ASP.NET 응용 프로그램에서 AJAX 스타일 페이지 업데이트를 수행 하는 두 가지 기본 방법을 비교 합니다. 첫 번째 방법은 Upd를 사용 하는 것입니다.
ms.author: riande
ms.date: 07/09/2007
ms.assetid: a5e33a7d-ccb2-483f-a955-3d39f72ba4ec
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
msc.type: video
ms.openlocfilehash: 56e3ebfbe0b5af4234791136725de79e38171cc1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78420155"
---
# <a name="how-do-i-choose-between-methods-of-ajax-page-updates"></a><span data-ttu-id="c663d-105">[방법:] AJAX 페이지 업데이트의 메서드 중에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c663d-105">[How Do I:] Choose Between Methods of AJAX Page Updates?</span></span>

<span data-ttu-id="c663d-106">만든 사람 [Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="c663d-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="c663d-107">이 비디오에서 Joe Stagner는 ASP.NET 응용 프로그램에서 AJAX 스타일 페이지 업데이트를 수행 하는 두 가지 기본 방법을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="c663d-107">In this video Joe Stagner compares the two primary methods of performing AJAX-style page updates in an ASP.NET application.</span></span> <span data-ttu-id="c663d-108">첫 번째 방법은 UpdatePanel을 사용 하는 것입니다 .이 경우 클라이언트 쪽 이나 서버 쪽에서 추가 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c663d-108">The first method is to use an UpdatePanel, where no additional code needs to be written on either the client side or the server side.</span></span> <span data-ttu-id="c663d-109">UpdatePanel을 사용 하면 모든 항목이 자동으로 작동 한다는 이점도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c663d-109">The benefit of using the UpdatePanel is that everything works automatically.</span></span> <span data-ttu-id="c663d-110">클라이언트에서 AJAX 요청 및 응답에 포함 해야 할 많은 데이터가 필요 하 고 서버에서 전체 페이지 수명 주기를 실행 해야 한다는 것이 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c663d-110">The penalty is that at the client it requires a lot of data to be included in the AJAX request and response, and at the server it requires a full page lifecycle to be executed.</span></span> <span data-ttu-id="c663d-111">두 번째 방법은 네트워크 콜백을 사용 하는 것입니다 .이 경우 클라이언트 쪽과 서버 쪽 모두에 추가 코드를 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c663d-111">The second method is to use network callbacks, where additional code needs to be written on both the client side and the server side.</span></span> <span data-ttu-id="c663d-112">네트워크 콜백을 사용 하는 경우의 장점 중 하나는 클라이언트에서 AJAX 요청 및 응답에 포함 해야 하는 데이터가 거의 필요 하지 않으며 서버에서 호출 된 서비스 메서드만 실행 해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c663d-112">The benefit of using network callbacks is that at the client it requires very little data to be included in the AJAX request and response, and at the server it requires only the called service method to be executed.</span></span> <span data-ttu-id="c663d-113">Penality는 필요한 코드를 작성 하는 데 소요 되는 시간과 노력입니다.</span><span class="sxs-lookup"><span data-stu-id="c663d-113">The penality is the time and effort it takes to write the necessary code.</span></span> <span data-ttu-id="c663d-114">Joe는 AJAX 스타일 페이지 업데이트의 두 가지 기본 방법 중에서 무엇을 선택 하는 경우 고려해 야 할 사항에 대해 설명 하 여 비디오를 마무리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c663d-114">Joe concludes the video by discussing what you should consider when choosing between the two primary methods of AJAX-style page updates.</span></span> <span data-ttu-id="c663d-115">이 비디오에서는 ASP.NET AJAX 비디오를 사용 하 [여 시작 하는 방법](how-do-i-get-started-with-aspnet-ajax.md) 및 ASP.NET ajax 비디오를 사용 [하 여 클라이언트 쪽 네트워크 콜백을 만드는](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) 방법에 대 한 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c663d-115">(This video uses the code from the [How Do I Get Started with ASP.NET AJAX](how-do-i-get-started-with-aspnet-ajax.md) video and the [How Do I Make Client-Side Network Callbacks with ASP.NET AJAX](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) video.)</span></span>

[<span data-ttu-id="c663d-116">&#9654;비디오 보기 (11 분)</span><span class="sxs-lookup"><span data-stu-id="c663d-116">&#9654; Watch video (11 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-choose-between-methods-of-ajax-page-updates)

> [!div class="step-by-step"]
> <span data-ttu-id="c663d-117">[이전](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
> [다음](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span><span class="sxs-lookup"><span data-stu-id="c663d-117">[Previous](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
[Next](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span></span>
