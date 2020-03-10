---
uid: web-forms/videos/how-do-i/how-do-i-configure-email-notification-for-health-monitoring-on-an-aspnet-web-site
title: '[방법:] ASP.NET 웹 사이트에서 상태 모니터링에 대 한 전자 메일 알림 구성 | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서 Chris Pel는 ASP.NET 웹 사이트에서 상태 모니터링에 대 한 전자 메일 알림을 구성 하는 방법을 보여 줍니다. 먼저 전자 메일 전송을 구성 하는 방법을 참조 하세요.
ms.author: riande
ms.date: 09/11/2008
ms.assetid: 1fa884c0-582e-4dc6-abb6-a5ec70d43ffb
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-configure-email-notification-for-health-monitoring-on-an-aspnet-web-site
msc.type: video
ms.openlocfilehash: 8c6512cebfb141dbf2f4c19e614aac99ccd41dac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506777"
---
# <a name="how-do-i-configure-email-notification-for-health-monitoring-on-an-aspnet-web-site"></a><span data-ttu-id="f55fb-104">[방법:] ASP.NET 웹 사이트에서 상태 모니터링에 대 한 전자 메일 알림 구성</span><span class="sxs-lookup"><span data-stu-id="f55fb-104">[How Do I:] Configure Email Notification for Health Monitoring on an ASP.NET Web Site</span></span>

<span data-ttu-id="f55fb-105">사람- [Chris pel](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="f55fb-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="f55fb-106">이 비디오에서 Chris Pel는 ASP.NET 웹 사이트에서 상태 모니터링에 대 한 전자 메일 알림을 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f55fb-106">In this video Chris Pels shows how to configure email notification for health monitoring in an ASP.NET web site.</span></span> <span data-ttu-id="f55fb-107">먼저 web.config 파일의 &lt;emailSettings&gt; 요소를 사용 하 여 ASP.NET 웹 사이트에서 전자 메일 보내기를 구성 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f55fb-107">First, see how to configure the sending of email in an ASP.NET web site through the use of the &lt;emailSettings&gt; element in the web.config file.</span></span> <span data-ttu-id="f55fb-108">다음으로 상태 모니터링 이벤트에 대 한 전자 메일을 공급자로 보내는 SimpleMailWebEventProvider를 추가 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f55fb-108">Next, learn how to add the SimpleMailWebEventProvider which sends emails for health monitoring events as a provider.</span></span> <span data-ttu-id="f55fb-109">그런 다음 컴퓨터 수준 상태 모니터링 구성을 검사 하 여 전자 메일 알림과 함께 사용할 수 있는 표준 상태 모니터링 이벤트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fb-109">Then see the standard health monitoring events that can be used with email notification by examining the machine level health monitoring configuration.</span></span> <span data-ttu-id="f55fb-110">사용 가능한 이벤트를 검토 한 후 "모든 이벤트"를 전자 메일 공급자에 매핑하는 규칙 구현을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f55fb-110">After reviewing the available events see a rule implemented that maps the "All Events" to the email provider.</span></span> <span data-ttu-id="f55fb-111">웹 사이트를 시작할 때 여러 전자 메일이 Outlook에서 수신 될 때 전송 및 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55fb-111">Upon starting the web site several emails are then sent and examined when they are received in Outlook.</span></span> <span data-ttu-id="f55fb-112">마지막으로, 이벤트를 상태 모니터링 메일 공급자에 매핑할 수 있는 몇 가지 기본 원칙을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fb-112">Finally, some basic principles of which events might be mapped to the health monitoring email provider are discussed.</span></span>

[<span data-ttu-id="f55fb-113">&#9654;비디오 보기 (25 분)</span><span class="sxs-lookup"><span data-stu-id="f55fb-113">&#9654; Watch video (25 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-configure-email-notification-for-health-monitoring-on-an-aspnet-web-site)
