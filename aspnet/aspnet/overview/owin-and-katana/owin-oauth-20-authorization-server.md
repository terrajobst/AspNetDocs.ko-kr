---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 권한 부여 서버 | Microsoft Docs
author: hongyes
description: 이 자습서에서는 OWIN OAuth 미들웨어를 사용 하 여 OAuth 2.0 권한 부여 서버를 구현 하는 방법을 안내 합니다. 이것은 outlin만을 지 원하는 고급 자습서입니다.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: 39c78ee57f791a94af7a5fb66c3ac42d7239760f
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000681"
---
# <a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="5accd-104">OWIN OAuth 2.0 권한 부여 서버</span><span class="sxs-lookup"><span data-stu-id="5accd-104">OWIN OAuth 2.0 Authorization Server</span></span>

<span data-ttu-id="5accd-105">[OAuth 2.0 프레임 워크](http://tools.ietf.org/html/rfc6749) 를 사용 하면 타사 앱에서 HTTP 서비스에 대 한 제한 된 액세스 권한을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5accd-105">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="5accd-106">클라이언트는 리소스 소유자의 자격 증명을 사용 하 여 보호 된 리소스에 액세스 하는 대신 특정 범위, 수명 및 기타 액세스 특성을 나타내는 문자열인 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5accd-106">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="5accd-107">액세스 토큰은 리소스 소유자의 승인으로 권한 부여 서버에 의해 타사 클라이언트에 발급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5accd-107">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="5accd-108">OWIN는 .NET 웹 서버와 웹 응용 프로그램 간의 표준 인터페이스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5accd-108">OWIN defines a standard interface between .NET web servers and web applications.</span></span> <span data-ttu-id="5accd-109">OWIN 인터페이스의 목표는 서버 및 응용 프로그램을 분리 하 고, .NET 웹 개발을 위한 간단한 모듈 개발을 장려 하 고, 개방형 표준으로 .NET 웹 개발 도구의 오픈 소스 에코 시스템을 촉진 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5accd-109">The goal of the OWIN interface is to decouple server and application, encourage the development of simple modules for .NET web development, and, by being an open standard, stimulate the open source ecosystem of .NET web development tools.</span></span>

<span data-ttu-id="5accd-110">자세한 내용은 [OWIN](http://owin.org/) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5accd-110">For more information, see [OWIN](http://owin.org/)</span></span>
