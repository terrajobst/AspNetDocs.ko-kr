---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[방법:] ASP.NET 페이지에서 HTML을 대체 하려면 응답. 필터 속성을 사용 합니다. | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서 Chris Pel는 응답 속성을 사용 하 여 페이지로 전송 되는 HTML을 가로채 고 변경 하는 방법을 보여 줍니다. 먼저 샘플 페이지를 만듭니다.
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 2ebd9162f81f5270c92c6b8d55e2d2dad4660701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487997"
---
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a>[방법:] ASP.NET 페이지에서 HTML을 대체 하려면 응답. 필터 속성을 사용 합니다.

사람- [Chris pel](https://twitter.com/chrispels)

이 비디오에서 Chris Pel는 응답 속성을 사용 하 여 페이지로 전송 되는 HTML을 가로채 고 변경 하는 방법을 보여 줍니다. 첫째, 몇 가지 간단한 텍스트를 사용 하 여 샘플 페이지를 만듭니다. 그런 다음 사용자 지정 스트림 클래스가 생성 됩니다 .이 클래스는 현재 스트림이 사용자의 브라우저로 전송 될 대체 스트림으로 사용 됩니다. 해당 사용자 지정 스트림 클래스에서 페이지의 콘텐츠는 스트림에서 검색 되어 변경 된 다음 응답 스트림에 기록 됩니다. 이 사용자 지정 스트림 클래스에서 Write 메서드는 기본 응답 스트림의 HTML을 대체 하도록 사용자 지정 되므로 사용자의 브라우저에 전송 되는 내용이 변경 됩니다. 마지막으로, 새 스트림 클래스는 페이지의 Load 이벤트를\_하 여 페이지 콘텐츠를 변경 하는 메커니즘을 제공 하는 Load 이벤트에 할당 됩니다.

[&#9654;비디오 보기 (13 분)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
