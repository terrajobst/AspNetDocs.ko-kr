---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: AJAX 컨트롤 도구 키트 시작 (VB) | Microsoft Docs
author: microsoft
description: AJAX 컨트롤 도구 키트 사용을 시작 하기 위해 알아야 하는 모든 내용을 알아보세요.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: ff614308555b31710b11f408e12e9a6fadbf98d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497141"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a>AJAX 컨트롤 도구 키트 시작(VB)

[Microsoft](https://github.com/microsoft) 에서

> AJAX 컨트롤 도구 키트 사용을 시작 하기 위해 알아야 하는 모든 내용을 알아보세요.

AJAX 컨트롤 도구 키트에는 ASP.NET 응용 프로그램에서 사용할 수 있는 30 개 이상의 무료 컨트롤이 포함 되어 있습니다. 이 자습서에서는 AJAX 컨트롤 도구 키트를 다운로드 하 고 Visual Studio/Visual Web Developer Express 도구 상자에 toolkit 컨트롤을 추가 하는 방법에 대해 알아봅니다.

## <a name="downloading-the-ajax-control-toolkit"></a>AJAX 컨트롤 도구 키트 다운로드

[AJAX 컨트롤 도구 키트](http://devexpress.com/act) 는 ASP.NET 커뮤니티와 ASP.NET 팀의 구성원이 개발한 오픈 소스 프로젝트입니다.

[AJAX 컨트롤 도구 키트 다운로드 ![](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

**그림 01**: AJAX 컨트롤 도구 키트 다운로드 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))

파일을 다운로드 한 후 파일의 차단을 해제 해야 합니다. 파일을 마우스 오른쪽 단추로 클릭 하 고 속성을 선택한 다음 **차단 해제** 단추를 클릭 합니다 (그림 2 참조).

[AJAX 컨트롤 도구 키트 ZIP 파일 차단 해제 ![](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

**그림 02**: AJAX 컨트롤 도구 키트 ZIP 파일 차단 해제 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))

파일의 차단을 해제 한 후 파일의 압축을 풀 수 있습니다. 파일을 마우스 오른쪽 단추로 클릭 하 고 **모두 추출** 메뉴 옵션을 선택 합니다. 이제 도구 키트를 Visual Studio/Visual Web Developer 도구 상자에 추가할 준비가 되었습니다.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>도구 상자에 AJAX 컨트롤 도구 키트 추가

AJAX 컨트롤 도구 키트를 사용 하는 가장 쉬운 방법은 Visual Studio/Visual Web Developer 도구 상자에 도구 키트를 추가 하는 것입니다 (그림 3 참조). 이렇게 하면 도구 키트 컨트롤을 사용 하려고 할 때 페이지로 끌어 놓기만 하면 됩니다.

[![AJAX 컨트롤 도구 키트가 도구 상자에 표시 됩니다.](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

**그림 03**: AJAX 컨트롤 도구 키트가 도구 상자에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)).

먼저 AJAX 컨트롤 도구 키트 탭을 도구 상자에 추가 해야 합니다. 다음 단계를 수행합니다.

1. 메뉴 옵션 파일, 새 웹 사이트를 선택 하 여 새 ASP.NET 웹 사이트를 만듭니다. 솔루션 탐색기 창에서 default.aspx를 두 번 클릭 하 여 편집기에서 파일을 엽니다.
2. 일반 탭 아래의 도구 상자를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가 탭** 을 선택 합니다 (그림 4 참조).
3. AJAX Control Toolkit 이라는 새 탭을 입력 합니다.

[새 탭을 추가 ![](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

**그림 04**: 새 탭 추가 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))

그런 다음 새 탭에 AJAX 컨트롤 도구 키트 컨트롤을 추가 해야 합니다. 다음 단계를 따르세요.

- AJAX 컨트롤 도구 키트 탭 아래를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 항목 선택을 선택 합니다 **(그림 5 참조)** .
- AJAX 컨트롤 도구 키트의 압축을 푼 위치로 이동 하 여 AjaxControlToolkit 어셈블리를 선택 합니다.

[도구 상자에 추가할 항목을 선택 ![](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

**그림 05**: 도구 상자에 추가할 항목 선택 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))

이러한 단계를 완료 한 후 도구 상자에 모든 도구 키트 컨트롤이 표시 됩니다.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>새 버전의 Toolkit로 업그레이드

이전 버전의 도구 키트를 사용 중이 고 이제 이후 버전으로 이동 해야 하는 경우 권장 되는 단계는 다음과 같습니다.

- 이진 파일-AjaxControlToolkit 어셈블리의 이전 버전을 웹 사이트 Bin 폴더에서 삭제 합니다.
- 도구 상자 항목-AJAX 컨트롤 도구 키트 탭을 삭제 하 고 위의 단계에 따라 AjaxControlToolkit 어셈블리의 새 버전으로 탭을 다시 만듭니다.

> [!div class="step-by-step"]
> [이전](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [다음](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
