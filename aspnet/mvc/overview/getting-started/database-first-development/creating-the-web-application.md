---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: '자습서: ASP.NET MVC를 사용 하 여 EF Database First 용 웹 응용 프로그램 및 데이터 모델 만들기'
description: 이 자습서에서는 웹 응용 프로그램을 만들고 데이터베이스 테이블을 기반으로 데이터 모델을 생성 하는 방법을 집중적으로 설명 합니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499529"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a>자습서: ASP.NET MVC를 사용 하 여 EF Database First 용 웹 응용 프로그램 및 데이터 모델 만들기

 MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 사용자가 데이터베이스 테이블에 있는 데이터를 표시, 편집, 만들기 및 삭제할 수 있도록 하는 코드를 자동으로 생성 하는 방법을 보여 줍니다. 생성 된 코드는 데이터베이스 테이블의 열에 해당 합니다.

이 자습서에서는 웹 응용 프로그램을 만들고 데이터베이스 테이블을 기반으로 데이터 모델을 생성 하는 방법을 집중적으로 설명 합니다.

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * ASP.NET 웹앱 만들기
> * 모델 생성

## <a name="prerequisites"></a>사전 요구 사항

* [MVC 5를 사용 하 여 Entity Framework 6 Database First 시작 하기](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a>ASP.NET 웹앱 만들기

새 솔루션이 나 데이터베이스 프로젝트와 동일한 솔루션에서 Visual Studio에서 새 프로젝트를 만들고 **ASP.NET 웹 응용 프로그램** 템플릿을 선택 합니다. 프로젝트 이름을 **ContosoSite**로 합니다.

![프로젝트 만들기](creating-the-web-application/_static/image1.png)

**확인**을 클릭합니다.

새 ASP.NET 프로젝트 창에서 **MVC** 템플릿을 선택 합니다. 나중에 응용 프로그램을 클라우드에 배포 하기 때문에 지금은 **클라우드 옵션에서 호스트** 를 지울 수 있습니다. **확인** 을 클릭 하 여 응용 프로그램을 만듭니다.

프로젝트는 기본 파일 및 폴더를 사용 하 여 만들어집니다.

이 자습서에서는 Entity Framework 6을 사용 합니다. NuGet 패키지 관리 창을 통해 프로젝트의 Entity Framework 버전을 두 번 확인할 수 있습니다. 필요한 경우 Entity Framework 버전을 업데이트 합니다.

![버전 표시](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a>모델 생성

이제 데이터베이스 테이블에서 Entity Framework 모델을 만듭니다. 이러한 모델은 데이터 작업에 사용 하는 클래스입니다. 각 모델은 데이터베이스의 테이블을 미러링 하 고 테이블의 열에 해당 하는 속성을 포함 합니다.

**모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 및 **새 항목**을 선택 합니다.

새 항목 추가 창의 왼쪽 창에서 **데이터** 를 선택 하 고 가운데 창의 옵션에서 **엔터티 데이터 모델 ADO.NET** 합니다. 새 모델 파일의 이름을 **ContosoModel**로 합니다.

**추가**를 클릭합니다.

엔터티 데이터 모델 마법사에서 **데이터베이스의 EF Designer**를 선택 합니다.

**다음**을 클릭합니다.

개발 환경 내에서 데이터베이스 연결을 정의한 경우 이러한 연결 중 하나가 미리 선택 된 것을 볼 수 있습니다. 그러나이 자습서의 첫 번째 부분에서 만든 데이터베이스에 대 한 새 연결을 만들려고 합니다. **새 연결** 단추를 클릭 합니다.

연결 속성 창에서 데이터베이스가 생성 된 로컬 서버의 이름 (이 경우 **localdb) \ProjectsV13**)을 제공 합니다. 서버 이름을 제공한 후 사용 가능한 데이터베이스에서 해당 데이터를 선택 합니다.

![연결 속성 설정](creating-the-web-application/_static/image8.png)

**확인**을 클릭합니다.

이제 올바른 연결 속성이 표시 됩니다. Web.config 파일에서 연결에 기본 이름을 사용할 수 있습니다.

**다음**을 클릭합니다.

최신 버전의 Entity Framework을 선택 합니다.

**다음**을 클릭합니다.

세 테이블 모두에 대해 모델을 생성 하려면 **테이블** 을 선택 합니다.

**Finish**를 클릭합니다.

보안 경고가 표시 되 면 **확인** 을 선택 하 여 템플릿을 계속 실행 합니다.

데이터베이스 테이블에서 모델을 생성 하 고 테이블 간의 속성 및 관계를 보여 주는 다이어그램이 표시 됩니다.

![모델 다이어그램](creating-the-web-application/_static/image11.png)

이제 모델 폴더에는 데이터베이스에서 생성 된 모델과 관련 된 많은 새 파일이 포함 됩니다.

**ContosoModel.Context.cs** 파일은 **DbContext** 클래스에서 파생 되는 클래스를 포함 하며 데이터베이스 테이블에 해당 하는 각 모델 클래스에 대 한 속성을 제공 합니다. **Course.cs**, **Enrollment.cs**및 **Student.cs** 파일은 데이터베이스 테이블을 나타내는 모델 클래스를 포함 합니다. 스 캐 폴딩으로 작업할 때 컨텍스트 클래스와 모델 클래스를 모두 사용 합니다.

이 자습서를 진행 하기 전에 프로젝트를 빌드합니다. 다음 섹션에서는 데이터 모델을 기반으로 코드를 생성 하지만 프로젝트가 빌드되지 않은 경우 해당 섹션은 작동 하지 않습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * ASP.NET 웹 앱을 만들었습니다.
> * 생성 된 모델

데이터 모델을 기반으로 코드 생성을 만드는 방법을 알아보려면 다음 자습서로 이동 합니다.
> [!div class="nextstepaction"]
> [뷰 생성](generating-views.md)
