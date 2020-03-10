---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: ASP.NET 웹 페이지 (Razor) 사이트에 도우미 설치 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 도우미를 설치 하는 방법을 설명 합니다. 도우미는 다음에 대 한 코드 및 태그를 포함 하는 재사용 가능한 구성 요소입니다.
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518645"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 도우미 설치

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 도우미를 설치 하는 방법을 설명 합니다. *도우미* 는 지루한 또는 복잡할 수 있는 작업을 수행 하기 위한 코드와 태그를 포함 하는 재사용 가능한 구성 요소입니다.
> 
> 학습할 내용:
> 
> - WebMatrix 3을 사용 하 여 만든 웹 사이트에 도우미를 설치 하는 방법입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - WebMatrix 3

## <a name="overview-of-helpers"></a>도우미 개요

사용자가 웹 페이지에서 자주 수행 하려는 일부 작업에는 많은 코드가 필요 하거나 추가 정보가 필요 합니다. 데이터에 대 한 차트를 표시 하는 예제는 다음과 같습니다. 페이지에 Twitter "따르기" 단추 배치 웹 사이트에서 전자 메일 보내기 이미지 자르기 또는 크기 조정 사이트에 PayPal을 사용 합니다. 이러한 종류의 작업을 쉽게 수행할 수 있도록 ASP.NET 웹 페이지 *도우미*를 사용할 수 있습니다. 도우미는 사이트에 대해 설치 하는 구성 요소 이며, 한 줄 또는 두 개의 Razor 코드를 사용 하 여 일반적인 작업을 수행할 수 있습니다.

ASP.NET 웹 페이지에는 몇 가지 도우미가 내장 되어 있습니다. 그러나 NuGet 패키지 관리자를 사용 하 여 제공 되는 패키지 (추가 기능)에서 많은 도우미를 사용할 수 있습니다. NuGet을 사용 하면 설치할 패키지를 선택한 다음 설치의 모든 세부 정보를 처리할 수 있습니다.

## <a name="installing-a-helper-in-webmatrix-3"></a>WebMatrix 3에서 도우미 설치

1. WebMatrix 3에서 **NuGet** 단추를 클릭 합니다.

    ![WebMatrix의 NuGet 갤러리 대화 상자](installing-helpers/_static/image1.png)
2. NuGet 패키지 관리자를 시작 하 고 사용 가능한 패키지를 표시 합니다. 검색 상자에 설치 하려는 도우미에 대 한 키워드를 입력 합니다.

    ![WebMatrix의 NuGet 갤러리 대화 상자](installing-helpers/_static/image2.png)
3. 패키지를 선택 하 고 **설치**를 클릭 합니다. 패키지를 설치할지 묻는 메시지가 나타나면 **예** 를 클릭 하 고 약관에 동의 함을 표시 합니다.

     도우미를 처음 설치 하는 경우 NuGet은 도우미를 구성 하는 코드에 대 한 폴더를 웹 사이트에 만듭니다.
4. 도우미를 제거 하려면 **갤러리** 단추를 클릭 하 고 **설치 됨** 탭을 클릭 한 후에 제거할 패키지를 선택 합니다.

## <a name="installing-the-twitter-helper"></a>Twitter 도우미 설치

최신 버전의 Twitter API는 NuGet을 통해 설치 하는 Twitter 도우미와 호환 되지 않습니다. 대신, 프로젝트에서 Twitter 도우미를 설정 하는 방법에 대 한 자세한 내용은 WebMatrix를 사용 하는 [Twitter 도우미](twitter-helper.md) 항목을 참조 하세요.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지 2 소개-프로그래밍 기본 사항](../getting-started/introducing-razor-syntax-c.md)

[WebMatrix를 사용 하는 Twitter 도우미](twitter-helper.md)
