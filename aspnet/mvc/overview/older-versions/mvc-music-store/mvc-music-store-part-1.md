---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: '1 부: 개요 및 파일 > 새 프로젝트 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 1 부에서는 개요와 파일 > 새 프로젝트를 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451283"
---
# <a name="part-1-overview-and-file-new-project"></a>1 부: 개요 및 파일 > 새 프로젝트

받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.  
>   
> MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 1 부에서는 개요와 파일&gt;새 프로젝트를 다룹니다.

## <a name="overview"></a>개요

MVC Music Store는 웹 개발을 위해 ASP.NET MVC 및 Visual Web Developer를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다. Microsoft는 느리게 시작 될 예정 이므로, 초급 수준의 웹 개발 환경을 사용할 수 있습니다.

빌드할 응용 프로그램은 간단한 음악 상점입니다. 응용 프로그램에는 쇼핑, 체크 아웃 및 관리의 세 가지 주요 부분이 있습니다.

![](mvc-music-store-part-1/_static/image1.jpg)

방문자는 장르별로 앨범을 탐색할 수 있습니다.

![](mvc-music-store-part-1/_static/image2.jpg)

단일 앨범을 보고 해당 바구니에 추가할 수 있습니다.

![](mvc-music-store-part-1/_static/image3.jpg)

해당 카트를 검토 하 여 더 이상 원하지 않는 항목을 제거할 수 있습니다.

![](mvc-music-store-part-1/_static/image4.jpg)

체크 아웃을 계속 하면 로그인 하거나 사용자 계정에 등록 하 라는 메시지가 표시 됩니다.

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

계정을 만든 후에는 배송 및 지불 정보를 입력 하 여 주문을 완료할 수 있습니다. 간단 하 게 유지 하기 위해 microsoft는 놀라운 프로 모션을 실행 하 고 있습니다. 프로 모션 코드를 "무료"로 입력 하면 모든 기능을 무료로 이용할 수 있습니다.

![](mvc-music-store-part-1/_static/image5.jpg)

주문 후에는 간단한 확인 화면이 표시 됩니다.

![](mvc-music-store-part-1/_static/image6.jpg)

고객 관련 페이지 외에도 관리자가 앨범을 만들고, 편집 하 고, 삭제할 수 있는 앨범 목록을 보여 주는 관리자 섹션을 작성 합니다.

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a>1. 파일&gt; 새 프로젝트

### <a name="installing-the-software"></a>소프트웨어 설치

이 자습서는 무료 Visual Web Developer 2010 Express (무료)를 사용 하 여 새 ASP.NET MVC 3 프로젝트를 만든 다음, 완벽 하 게 작동 하는 응용 프로그램을 만들기 위해 기능을 증분 방식으로 추가 하는 것으로 시작 합니다. 이 과정에서 데이터베이스 액세스, 폼 게시 시나리오, 데이터 유효성 검사, 페이지를 일관 되 게 유지 하기 위해 마스터 페이지 사용, 페이지 업데이트 및 유효성 검사, 사용자 로그인 등에 대해 설명 합니다.

단계별 지침을 따르거나 전체 응용 프로그램을 [MVC-음악 저장소](https://github.com/evilDave/MVC-Music-Store)에서 다운로드할 수 있습니다.

Visual Studio 2010 SP1 또는 Visual Web Developer 2010 Express SP1 (Visual Studio 2010의 무료 버전) 중 하나를 사용 하 여 응용 프로그램을 빌드할 수 있습니다. SQL Server Compact (무료)를 사용 하 여 데이터베이스를 호스팅합니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다.

- [Visual Studio Web Developer Express SP1 필수 구성 요소]
- [ASP.NET MVC 3 도구 업데이트]
- [SQL Server Compact 4.0]-런타임 및 도구 지원을 포함 합니다.

### <a name="creating-a-new-aspnet-mvc-3-project"></a>새 ASP.NET MVC 3 프로젝트 만들기

먼저 Visual Web Developer의 파일 메뉴에서 "새 프로젝트"를 선택 합니다. 그러면 새 프로젝트 대화 상자가 나타납니다.

![](mvc-music-store-part-1/_static/image5.png)

왼쪽의 시각적 C#&gt; 웹 템플릿 그룹을 선택 하 고 가운데 열에서 "ASP.NET MVC 3 웹 응용 프로그램" 템플릿을 선택 합니다. 프로젝트 이름을 MvcMusicStore로 하 고 확인 단추를 누릅니다.

![](mvc-music-store-part-1/_static/image8.jpg)

그러면 프로젝트에 대 한 MVC 특정 설정을 만들 수 있는 보조 대화 상자가 표시 됩니다. 다음을 선택 합니다.

프로젝트 템플릿-빈 선택

뷰 엔진-Razor 선택

HTML5 의미 체계 태그 사용-선택 됨

설정이 아래에 표시 되었는지 확인 한 다음 확인 단추를 누릅니다.

![](mvc-music-store-part-1/_static/image9.jpg)

그러면 프로젝트가 생성 됩니다. 오른쪽의 솔루션 탐색기에 응용 프로그램에 추가 된 폴더를 살펴보겠습니다.

![](mvc-music-store-part-1/_static/image10.jpg)

빈 MVC 3 템플릿은 완전히 비어 있지 않으며 기본 폴더 구조를 추가 합니다.

![](mvc-music-store-part-1/_static/image6.png)

ASP.NET MVC는 폴더 이름에 대해 다음과 같은 몇 가지 기본 명명 규칙을 사용 합니다.

| **폴더** | **용도** |
| --- | --- |
| **/컨트롤러** | 컨트롤러는 브라우저에서 입력에 응답 하 여 수행할 작업을 결정 하 고 사용자에 게 응답을 반환 합니다. |
| **/Views** | 보기에 UI 템플릿 포함 |
| **/모델** | 모델 데이터 저장 및 조작 |
| **/콘텐츠** | 이 폴더에는 이미지, CSS 및 기타 정적 콘텐츠가 저장 됩니다. |
| **/Scripts** | 이 폴더에는 JavaScript 파일이 저장 됩니다. |

ASP.NET MVC 프레임 워크는 기본적으로 "구성에 대 한 규칙" 방식을 사용 하 고 폴더 명명 규칙에 따라 몇 가지 기본 가정을 수행 하기 때문에 이러한 폴더는 빈 ASP.NET MVC 응용 프로그램에도 포함 되어 있습니다. 예를 들어, 컨트롤러는 코드에서 명시적으로이를 지정 하지 않고 Views 폴더에서 뷰를 찾습니다. 기본 규칙을 사용 하면 작성 해야 하는 코드의 양이 줄어들고 다른 개발자가 프로젝트를 보다 쉽게 이해할 수 있게 됩니다. 응용 프로그램을 빌드할 때 이러한 규칙을 자세히 설명 합니다.

> [!div class="step-by-step"]
> [다음](mvc-music-store-part-2.md)
