---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
title: 사용자 지정 경로 제약 조건 만들기 (VB) | Microsoft Docs
author: StephenWalther
description: Stephen Walther는 사용자 지정 경로 제약 조건을 만드는 방법을 보여 줍니다. 경로가 일치 하는 것을 방지 하는 간단한 사용자 지정 제약 조건을 구현 합니다.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 892edb27-1cc2-4eaf-8314-dbc2efc6228a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 2330708cf4a28180ce8a05f4696bf7a7a32092d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486791"
---
# <a name="creating-a-custom-route-constraint-vb"></a>사용자 지정 경로 제약 조건 만들기(VB)

[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther는 사용자 지정 경로 제약 조건을 만드는 방법을 보여 줍니다. 원격 컴퓨터에서 브라우저 요청을 수행할 때 경로가 일치 하지 않도록 하는 간단한 사용자 지정 제약 조건을 구현 합니다.

이 자습서의 목표는 사용자 지정 경로 제약 조건을 만드는 방법을 보여 주는 것입니다. 사용자 지정 경로 제약 조건을 사용 하면 일부 사용자 지정 조건이 일치 하지 않는 한 경로가 일치 하지 않도록 방지할 수 있습니다.

이 자습서에서는 Localhost 경로 제약 조건을 만듭니다. Localhost 경로 제약 조건은 로컬 컴퓨터에서 수행 된 요청만 일치 시킵니다. 인터넷을 통한 원격 요청이 일치 하지 않습니다.

IRouteConstraint 인터페이스를 구현 하 여 사용자 지정 경로 제약 조건을 구현 합니다. 이는 단일 메서드를 설명 하는 매우 간단한 인터페이스입니다.

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample1.vb)]

메서드는 부울 값을 반환 합니다. False를 반환 하는 경우 제약 조건과 연결 된 경로가 브라우저 요청과 일치 하지 않습니다.

Localhost 제약 조건은 목록 1에 포함 되어 있습니다.

**목록 1-LocalhostConstraint .vb**

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample2.vb)]

목록 1의 제약 조건은 HttpRequest 클래스에 의해 노출 된 IsLocal 속성을 활용 합니다. 요청의 IP 주소가 127.0.0.1 이거나 요청의 IP가 서버의 IP 주소와 동일한 경우이 속성은 true를 반환 합니다.

Global.asax 파일에 정의 된 경로 내에서 사용자 지정 제약 조건을 사용 합니다. 목록 2의 Global.asax 파일은 Localhost 제약 조건을 사용 하 여 로컬 서버에서 요청을 수행 하지 않는 한 관리 페이지를 요청 하지 못하도록 합니다. 예를 들어 원격 서버에서/Admin/DeleteAll에 대 한 요청을 수행할 수 없습니다.

**목록 2-global.asax**

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample3.vb)]

Localhost 제약 조건은 관리자 경로 정의에 사용 됩니다. 이 경로는 원격 브라우저 요청과 일치 하지 않습니다. 그러나 Global.asax에 정의 된 다른 경로는 동일한 요청과 일치할 수 있습니다. 제약 조건으로 인해 특정 경로는 Global.asax 파일에 정의 된 모든 경로가 아니라 요청과 일치 하지 않도록 해야 합니다.

기본 경로는 목록 2의 Global.asax 파일에서 주석으로 처리 되었습니다. 기본 경로를 포함 하는 경우 기본 경로는 관리 컨트롤러에 대 한 요청과 일치 합니다. 이 경우에는 요청이 관리자 경로와 일치 하지 않더라도 원격 사용자는 여전히 관리 컨트롤러의 작업을 호출할 수 있습니다.

> [!div class="step-by-step"]
> [이전](creating-a-route-constraint-vb.md)
