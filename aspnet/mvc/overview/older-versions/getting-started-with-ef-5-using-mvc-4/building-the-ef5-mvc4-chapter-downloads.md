---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: EF 5 MVC 4 자습서에 대 한 장 다운로드 빌드 | Microsoft Docs
author: Rick-Anderson
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 10237af40e3914b65e5181f17555697e86adea4b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457858"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a>EF 5 MVC 4 자습서에 대 한 장 다운로드 빌드

[Rick Anderson](https://twitter.com/RickAndMSFT)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.

## <a name="building-the-chapter-downloads"></a>챕터 다운로드 빌드

1. 프로젝트 샘플 zip 파일을 다운로드 하 고 압축을 풉니다. 압축을 푼 다운로드 패키지에는 각 챕터를 완료 하기 위한 추가 zip 파일이 있습니다.
2. 원하는 zip 파일을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 한 다음 **차단 해제** 단추를 클릭 합니다.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. 파일의 압축을 풉니다.
4. Visual Studio를 시작 하려면이 파일을 두 번 *클릭 합니다.*
5. **도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 차례로 클릭 합니다.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. 패키지 관리자 콘솔 (PMC)에서 **복원**을 클릭 합니다.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. Visual Studio를 끝냅니다.
8. Visual Studio를 다시 시작 하 고 위의 단계에서 닫은 솔루션 파일을 엽니다.
9. 패키지 관리자 콘솔 (PMC)에서 `Update-Database` 명령을 입력 합니다.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > 다음 오류가 표시되는 경우  
    >   
    >  *' 업데이트-데이터베이스 ' 라는 용어는 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램의 이름으로 인식 되지 않습니다. 이름의 철자를 확인 하거나, 경로가 포함 된 경우 경로가 올바른지 확인 한 후 다시 시도 하십시오.*  
    > Visual Studio를 종료 하 고 다시 시작 합니다.

    각 마이그레이션이 실행 된 후 초기값 메서드가 실행 됩니다. 이제 앱을 실행할 수 있습니다.

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [이전](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
