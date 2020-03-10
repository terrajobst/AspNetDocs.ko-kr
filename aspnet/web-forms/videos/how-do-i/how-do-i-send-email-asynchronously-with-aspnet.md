---
uid: web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
title: '[방법:] ASP.NET를 사용 하 여 비동기적으로 전자 메일 보내기 | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서 Chris Pel는 ASP.NET에서 시스템 .Net. Mail 클래스를 사용 하 여 비동기 전자 메일 메시지를 보내는 방법을 보여 줍니다. 먼저 웹 si를 구성 하는 방법을 참조 하세요.
ms.author: riande
ms.date: 09/24/2008
ms.assetid: 77a5c8fa-ebb2-426d-b56b-a5a98a46b516
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
msc.type: video
ms.openlocfilehash: ea29823446cc1339003160bd3e945bde1af42473
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516173"
---
# <a name="how-do-i-send-email-asynchronously-with-aspnet"></a><span data-ttu-id="1a2d9-104">[방법:] ASP.NET를 사용 하 여 비동기적으로 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="1a2d9-104">[How Do I:] Send Email Asynchronously with ASP.NET</span></span>

<span data-ttu-id="1a2d9-105">사람- [Chris pel](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="1a2d9-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="1a2d9-106">이 비디오에서 Chris Pel는 ASP.NET에서 시스템 .Net. Mail 클래스를 사용 하 여 비동기 전자 메일 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d9-106">In this video, Chris Pels shows how to use the System.Net.Mail classes in ASP.NET to send an asynchronous email message.</span></span> <span data-ttu-id="1a2d9-107">먼저 web.config 파일의 &lt;mailSettings&gt; 요소를 사용 하 여 전자 메일을 보내도록 웹 사이트를 구성 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1a2d9-107">First, see how to configure a web site to send email using the &lt;mailSettings&gt; element in the web.config file.</span></span> <span data-ttu-id="1a2d9-108">다음으로 전자 메일 정보를 입력 하는 간단한 사용자 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d9-108">Next, create a simple user interface for entering email information.</span></span> <span data-ttu-id="1a2d9-109">그런 다음 Send-mailmessage 클래스를 사용 하 여 페이지에 대 한 코드 숨김으로 전자 메일 메시지를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d9-109">Then learn how to create use the MailMessage class to create an email message in the code behind for the page.</span></span> <span data-ttu-id="1a2d9-110">해당 프로세스의 일부로 전자 메일을 보낸 다음에 비동기 콜백에 대 한 이벤트 처리기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d9-110">As part of that process create an event handler for the asynchronous callback following the sending of the email.</span></span> <span data-ttu-id="1a2d9-111">이벤트 처리기에서 전자 메일 전송 프로세스에 대 한 정보를 제공 하는 AsynchCompletedEventArgs 클래스의 인스턴스를 사용 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1a2d9-111">In the event handler see how to use the instance of the AsynchCompletedEventArgs class which provides information about the email sending process.</span></span> <span data-ttu-id="1a2d9-112">마지막으로, 디버그 모드의 단계에 따라 테스트 전자 메일을 비동기적으로 보내고 프로세스에서 받은 실제 전자 메일을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d9-112">Finally, send a test email asynchronously, following the steps in the debug mode, and view the actual email received from the process.</span></span>

[<span data-ttu-id="1a2d9-113">&#9654;비디오 보기 (18 분)</span><span class="sxs-lookup"><span data-stu-id="1a2d9-113">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-email-asynchronously-with-aspnet)
