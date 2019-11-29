---
uid: webhooks/receiving/dependencies
title: ASP.NET WebHooks 수신기 종속성 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크에 받는 사람 종속성 및 종속성 주입.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564867"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET WebHooks 수신기 종속성

Microsoft ASP.NET 웹 후크는 종속성 주입을 염두에 두면 설계 되었습니다. 시스템의 대부분 종속성은 종속성 주입 엔진을 사용 하 여 대체 구현으로 바꿀 수 있습니다.

수신자 종속성 목록은 [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 를 참조 하세요. 종속성이 등록 되지 않은 경우 기본 구현이 사용 됩니다. 기본 구현 목록은 [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 를 참조 하세요.
