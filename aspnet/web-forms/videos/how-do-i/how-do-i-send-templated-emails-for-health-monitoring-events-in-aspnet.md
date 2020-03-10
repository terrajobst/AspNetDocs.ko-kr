---
uid: web-forms/videos/how-do-i/how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet
title: '[방법:] ASP.NET의 상태 모니터링 이벤트에 대 한 템플릿 기반 이메일 보내기 | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서 Chris Pel는 TemplatedEmailWebEventProvider에 대 한 템플릿을 활용 하는 상태 모니터링 이벤트가 발생 하는 경우 전자 메일을 보내는 데를 사용 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 09/18/2008
ms.assetid: 5c107c6e-9fb7-4206-bd3f-221cb0767f8a
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet
msc.type: video
ms.openlocfilehash: e7b929c6e186e59b43180e8f26cf0f8b4608328f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510485"
---
# <a name="how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet"></a><span data-ttu-id="88b7f-103">[방법:] ASP.NET의 상태 모니터링 이벤트에 대 한 템플릿 기반 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="88b7f-103">[How Do I:] Send Templated Emails for Health Monitoring Events in ASP.NET</span></span>

<span data-ttu-id="88b7f-104">사람- [Chris pel](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="88b7f-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="88b7f-105">이 비디오에서 Chris Pel는 전자 메일 콘텐츠에 대 한 템플릿을 활용 하는 상태 모니터링 이벤트가 발생 하는 경우 TemplatedEmailWebEventProvider를 사용 하 여 전자 메일을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="88b7f-105">In this video Chris Pels shows how to use the TemplatedEmailWebEventProvider to send emails when health monitoring events occur that utilize a template for the email content.</span></span> <span data-ttu-id="88b7f-106">먼저 web.config 파일의 &lt;공급자&gt; 및 &lt;규칙&gt; 요소를 구성 하 여 템플릿 기반 메일 사용을 구현 하 고 상태 모니터링 이벤트를 템플릿 기반 메일 공급자와 연결 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="88b7f-106">First, see how to configure the &lt;provider&gt; and &lt;rules&gt; elements in the web.config file to implement the use of templated email and associate a health monitoring event with the templated email provider.</span></span> <span data-ttu-id="88b7f-107">템플릿 기반 공급자가 구성 되 면를 사용 하 여 전자 메일 템플릿을 만드는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="88b7f-107">Once the templated provider is configured see how to create the email template using as standard .aspx page.</span></span> <span data-ttu-id="88b7f-108">TemplatedEmailWebEventProvider 페이지에 전달 되는 MailEventNotificaitonInfo 클래스에서 사용할 수 있는 정보를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="88b7f-108">Learn what information is available in the MailEventNotificaitonInfo class that is passed by the TemplatedEmailWebEventProvider to the template .aspx page.</span></span> <span data-ttu-id="88b7f-109">전자 메일 콘텐츠에 적절 한 정보를 포함 하는 데 사용할 수 있는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7f-109">See how it can be used to include whatever information is appropriate in the email content.</span></span> <span data-ttu-id="88b7f-110">마지막으로 상태 모니터링 이벤트에 대 한 응답으로 전자 메일을 보내는 테스트 웹 사이트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7f-110">Finally, view the test web site which sends emails in response to health monitoring events.</span></span> <span data-ttu-id="88b7f-111">그런 다음 템플릿을 기반으로 상태 모니터링 이벤트 정보를 포함 하는 받은 실제 전자 메일을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="88b7f-111">Then view the actual emails received that contain the health monitoring event information based upon the template.</span></span>

[<span data-ttu-id="88b7f-112">&#9654;비디오 보기 (25 분)</span><span class="sxs-lookup"><span data-stu-id="88b7f-112">&#9654; Watch video (25 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet)
