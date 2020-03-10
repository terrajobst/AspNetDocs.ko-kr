---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
title: '반복 #2 – 응용 프로그램 모양 만들기 (C#) | Microsoft Docs'
author: microsoft
description: 이 반복에서는 기본 ASP.NET MVC 뷰 마스터 페이지 및 css 스타일 시트를 수정 하 여 응용 프로그램의 모양을 개선 합니다.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1173feb-11ee-4017-8f3f-86599ea6ae13
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
msc.type: authoredcontent
ms.openlocfilehash: 246cb4b4668339cc4b7e4e03ea005102c6a2a5c3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487313"
---
# <a name="iteration-2--make-the-application-look-nice-c"></a>반복 #2 – 응용 프로그램 모양 만들기 (C#)

[Microsoft](https://github.com/microsoft) 에서

[코드 다운로드](iteration-2-make-the-application-look-nice-cs/_static/contactmanager_2_cs1.zip)

> 이 반복에서는 기본 ASP.NET MVC 뷰 마스터 페이지 및 css 스타일 시트를 수정 하 여 응용 프로그램의 모양을 개선 합니다.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Contact Management ASP.NET MVC 응용 프로그램 빌드 (C#)

이 자습서 시리즈에서는 전체 연락처 관리 응용 프로그램을 처음부터 끝까지 빌드 합니다. 연락처 관리자 응용 프로그램을 사용 하면 연락처 정보 (이름, 전화 번호 및 전자 메일 주소)를 사용자 목록으로 저장할 수 있습니다.

여러 반복을 통해 응용 프로그램을 빌드합니다. 각 반복을 통해 응용 프로그램을 점진적으로 개선 합니다. 이 여러 반복 방법의 목표는 각 변경의 이유를 이해할 수 있게 하는 것입니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서는 가장 간단한 방법으로 연락처 관리자를 만듭니다. 기본 데이터베이스 작업 (만들기, 읽기, 업데이트 및 삭제 (CRUD))에 대 한 지원을 추가 합니다.

- 반복 #2-응용 프로그램을 멋지게 만듭니다. 이 반복에서는 기본 ASP.NET MVC 뷰 마스터 페이지 및 css 스타일 시트를 수정 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-양식 유효성 검사를 추가 합니다. 세 번째 반복에서는 기본 폼 유효성 검사를 추가 합니다. 사용자가 필요한 양식 필드를 완료 하지 않고 양식을 전송 하지 못하도록 합니다. 또한 전자 메일 주소 및 전화 번호의 유효성을 검사 합니다.

- 반복 #4-응용 프로그램이 느슨하게 결합 되도록 합니다. 이 네 번째 반복에서는 몇 가지 소프트웨어 디자인 패턴을 활용 하 여 연락처 관리자 응용 프로그램을 보다 쉽게 유지 관리 하 고 수정할 수 있습니다. 예를 들어 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램을 리팩터링 합니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서는 단위 테스트를 추가 하 여 응용 프로그램을 더 쉽게 유지 관리 하 고 수정할 수 있도록 합니다. Microsoft는 데이터 모델 클래스를 모의 하 고 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 빌드 했습니다.

- 반복 #6-테스트 기반 개발을 사용 합니다. 이 여섯 번째 반복에서는 단위 테스트를 먼저 작성 하 고 단위 테스트에 대 한 코드를 작성 하 여 응용 프로그램에 새 기능을 추가 합니다. 이 반복에서는 연락처 그룹을 추가 합니다.

- 반복 #7-Ajax 기능을 추가 합니다. 일곱 번째 반복에서는 Ajax에 대 한 지원을 추가 하 여 응용 프로그램의 응답성과 성능을 향상 시킵니다.

## <a name="this-iteration"></a>이 반복

이 반복의 목표는 연락처 관리자 응용 프로그램의 모양을 개선 하는 것입니다. 현재 연락처 관리자는 기본 ASP.NET MVC 보기 마스터 페이지와 css 스타일 시트를 사용 합니다 (그림 1 참조). 이는 잘못 된 것은 아니지만 다른 모든 ASP.NET MVC 웹 사이트와 마찬가지로 연락처 관리자를 확인 하려고 합니다. 이러한 파일을 사용자 지정 파일로 바꾸려고 합니다.

[새 프로젝트 대화 상자 ![](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)

**그림 01**: ASP.NET MVC 응용 프로그램의 기본 모양 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image2.png))

이 반복에서는 응용 프로그램의 시각적 디자인을 개선 하는 두 가지 방법을 설명 합니다. 먼저 ASP.NET MVC 디자인 갤러리를 활용 하 여 무료 ASP.NET MVC 디자인 템플릿을 다운로드 하는 방법을 보여 줍니다. ASP.NET MVC 디자인 갤러리를 사용 하면 작업을 수행 하지 않고 전문적인 웹 응용 프로그램을 만들 수 있습니다.

ASP.NET MVC 디자인 갤러리에서 연락처 관리자 응용 프로그램에 대 한 템플릿을 사용 하지 않기로 결정 했습니다. 대신 전문 디자인 회사에서 만든 사용자 지정 디자인이 있습니다. 이 자습서의 두 번째 부분에서는 전문적인 디자인 회사로 작업 하 여 최종 ASP.NET MVC 디자인을 만드는 방법에 대해 설명 합니다.

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC 디자인 갤러리

ASP.NET MVC 디자인 갤러리는 Microsoft에서 제공 하는 무료 리소스입니다. ASP.NET MVC 갤러리는 다음 주소에 있습니다.

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC 디자인 갤러리는 ASP.NET MVC 프로젝트에서를 사용 하기 위해 특별히 만든 무료 웹 사이트 디자인의 컬렉션을 호스팅합니다. 디자인은 커뮤니티의 구성원이 업로드 합니다. 갤러리 방문자는 즐겨 찾는 디자인에 응답할 수 있습니다 (그림 2 참조).

[새 프로젝트 대화 상자 ![](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)

**그림 02**: ASP.NET MVC 디자인 갤러리 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image4.png))

이 자습서를 작성할 때 갤러리에서 가장 인기 있는 디자인은 David Hauser에서 10 월 이라는 디자인입니다. ASP.NET MVC 프로젝트에 대해 다음 단계를 완료 하 여이 디자인을 사용할 수 있습니다.

1. **다운로드** 단추를 클릭 하 여 10 월 .zip 파일을 컴퓨터에 다운로드 합니다.
2. 다운로드 한 10 월 .zip 파일을 마우스 오른쪽 단추로 클릭 하 고 **차단 해제** 단추를 클릭 합니다 (그림 3 참조).
3. 10 월 이라는 폴더에 파일의 압축을 풉니다.
4. 10 월 폴더에 포함 된 DesignTemplate 폴더에서 모든 파일을 선택 하 고 파일을 마우스 오른쪽 단추로 클릭 한 다음 메뉴 옵션 **복사**를 선택 합니다.
5. Visual Studio 솔루션 탐색기 창에서 연락처 관리자 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **붙여넣기** 를 선택 합니다 (그림 4 참조).
6. Visual Studio 메뉴 옵션 **편집, 찾기 및 바꾸기, 빠른 바꾸기** 및 바꾸기 *[myprojectname]* 를 동료 *관리자* 로 선택 합니다 (그림 5 참조).

[새 프로젝트 대화 상자 ![](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)

**그림 03**: 웹에서 다운로드 한 파일 차단 해제 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image6.png))

[새 프로젝트 대화 상자 ![](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)

**그림 04**: 솔루션 탐색기에서 파일 덮어쓰기 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image8.png))

[새 프로젝트 대화 상자 ![](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)

**그림 05**: [ProjectName]을 (를) 연락처 관리자로 바꾸기 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image10.png))

이러한 단계를 완료 한 후에는 웹 응용 프로그램에서 새로운 디자인을 사용 합니다. 그림 6의 페이지는 10 월 설계를 사용 하는 연락처 관리자 응용 프로그램의 모양을 보여 줍니다.

[새 프로젝트 대화 상자 ![](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)

**그림 06**: 10 월 템플릿 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image12.png))

## <a name="creating-a-custom-aspnet-mvc-design"></a>사용자 지정 ASP.NET MVC 디자인 만들기

ASP.NET MVC 디자인 갤러리에는 다양 한 디자인 스타일을 선택 하는 것이 좋습니다. 갤러리는 ASP.NET MVC 응용 프로그램의 모양을 사용자 지정 하는 간편한 방법을 제공 합니다. 물론 갤러리에는 완전히 무료로 제공 되는 큰 이점이 있습니다.

그러나 웹 사이트에 대해 완전히 고유한 디자인을 만들어야 할 수도 있습니다. 이 경우 웹 사이트 디자인 회사에서 작업을 수행 하는 것이 좋습니다. 이 접근 방식을 사용 하 여 연락처 관리자 응용 프로그램을 디자인 하기로 결정 했습니다.

반복 #1에서 연락처 관리자를 압축 하 고 프로젝트를 디자인 회사에 보냅니다. Visual Studio를 소유 하지 않았습니다 (shame). 그러나 문제가 발생 하지 않았습니다. [https://www.asp.net](https://www.asp.net) 웹 사이트에서 Microsoft Visual web developer를 무료로 다운로드 하 고 Visual web Developer에서 연락처 관리자 응용 프로그램을 열 수 있습니다. 몇 일 후에 그림 7에서 디자인을 생성 했습니다.

[새 프로젝트 대화 상자 ![](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)

**그림 07**: ASP.NET MVC Contact Manager 디자인 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image14.png))

새 디자인은 새 css 스타일 시트 파일과 새 뷰 마스터 페이지 파일의 두 가지 기본 파일로 구성 되어 있습니다. 보기 마스터 페이지에는 ASP.NET MVC 응용 프로그램의 보기에 대 한 레이아웃 및 공유 콘텐츠가 포함 됩니다. 예를 들어 마스터 보기 페이지에는 그림 7에 표시 된 머리글, 탐색 탭 및 바닥글이 포함 됩니다. 디자인 회사의 새 site.master 파일을 사용 하 여 Views\Shared 폴더에 기존 사이트. 마스터 뷰 마스터 페이지를 덮어썼습니다.

또한 디자인 회사는 새 css 스타일 시트 및 이미지 집합도 만들었습니다. 이러한 새 파일을 콘텐츠 폴더에 배치 하 고 기존 사이트 .css 파일을 덮어썼습니다. 모든 정적 콘텐츠를 Content 폴더에 두어야 합니다.

연락처 관리자에 대 한 새 디자인에는 연락처를 편집 및 삭제 하기 위한 이미지가 포함 되어 있습니다. 편집 및 삭제 이미지는 연락처의 HTML 테이블에서 각 연락처 옆에 표시 됩니다.

원래 이러한 링크는 HTML로 렌더링 되었습니다. Html.actionlink () 도우미는 다음과 같습니다.

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample1.aspx)]

Html.actionlink () 메서드는 이미지를 지원 하지 않습니다 .이 메서드는 보안상의 이유로 링크 텍스트를 인코딩합니다. 따라서 Html.actionlink () 호출을 Url에 대 한 호출로 바꿨습니다. 작업 ()은 다음과 같습니다.

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample2.aspx)]

Html.actionlink () 메서드는 전체 HTML 하이퍼링크를 렌더링 합니다. 반면에 Url. Action () 메서드는 &lt;&gt; 태그 없이 URL만 렌더링 합니다.

또한 새 디자인에는 선택 된 탭과 선택 하지 않은 탭이 모두 포함 되어 있습니다. 예를 들어 그림 8에서는 **새 연락처 만들기** 탭이 선택 되어 있고 **내 연락처** 탭이 선택 되어 있지 않습니다.

[새 프로젝트 대화 상자 ![](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)

**그림 08**: 선택 및 선택 하지 않은 탭 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-cs/_static/image16.png))

선택 된 탭과 선택 하지 않은 탭 모두 렌더링을 지원 하기 위해 MenuItemHelper 라는 사용자 지정 HTML 도우미를 만들었습니다. 이 도우미 메서드는 현재 컨트롤러 및 작업이 도우미에 전달 된 컨트롤러 및 작업 이름과 일치 하는지 여부에 따라 &lt;li&gt; 태그 또는 &lt;li class = "selected"&gt; 태그를 렌더링 합니다. MenuItemHelper에 대 한 코드는 목록 1에 포함 되어 있습니다.

**목록 1-Helpers\MenuItemHelper.cs**

[!code-csharp[Main](iteration-2-make-the-application-look-nice-cs/samples/sample3.cs)]

MenuItemHelper는 내부적으로 빌드하는 tagbuilder 클래스를 사용 하 여 &lt;li&gt; HTML 태그를 빌드합니다. 빌드하는 tagbuilder 클래스는 새 HTML 태그를 빌드해야 할 때마다 사용할 수 있는 매우 유용한 유틸리티 클래스입니다. 특성을 추가 하 고, CSS 클래스를 추가 하 고, Id를 생성 하 고, 태그 내부 HTML을 수정 하는 메서드를 포함 합니다.

## <a name="summary"></a>요약

이 반복에서는 ASP.NET MVC 응용 프로그램의 시각적 디자인을 개선 했습니다. 먼저 ASP.NET MVC 디자인 갤러리를 소개 했습니다. ASP.NET MVC 응용 프로그램에서 사용할 수 있는 ASP.NET MVC 디자인 갤러리에서 무료 디자인 템플릿을 다운로드 하는 방법을 배웠습니다.

다음으로 기본 css 스타일 시트 파일 및 마스터 뷰 페이지 파일을 수정 하 여 사용자 지정 디자인을 만드는 방법에 대해 설명 했습니다. 새 디자인을 지원 하기 위해 연락처 관리자 응용 프로그램을 약간 변경 해야 했습니다. 예를 들어 선택 된 탭과 선택 하지 않은 탭을 표시 하는 MenuItemHelper 라는 새 HTML 도우미를 추가 했습니다.

다음 반복에서는 유효성 검사의 매우 중요 한 주제를 살펴보겠습니다. 사용자가 사용자의 이름과 성 등의 필수 값을 제공 하지 않고 새 연락처를 만들 수 없도록 응용 프로그램에 유효성 검사 코드를 추가 합니다.

> [!div class="step-by-step"]
> [이전](iteration-1-create-the-application-cs.md)
> [다음](iteration-3-add-form-validation-cs.md)
