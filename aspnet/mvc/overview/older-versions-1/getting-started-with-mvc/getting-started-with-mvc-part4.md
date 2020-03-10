---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: 데이터베이스 만들기 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469673"
---
# <a name="creating-a-database"></a>데이터베이스 만들기

[Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다. [ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.

이 섹션에서는 영화 데이터를 저장 하 고 검색 하는 데 사용할 새 SQL Express 데이터베이스를 만듭니다. Visual Web Developer IDE 내에서 보기 |를 선택 합니다. 서버 탐색기. 데이터 연결을 마우스 오른쪽 단추로 클릭 하 고 연결 추가 ...를 클릭 합니다.

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

데이터 소스 선택 대화 상자에서 Microsoft SQL Server를 선택 하 고 계속을 선택 합니다.

![](getting-started-with-mvc-part4/_static/image2.png)

연결 추가 대화 상자에서 서버 이름으로 ".\SQLEXPRESS"를 입력 하 고 새 데이터베이스의 이름으로 "영화"를 입력 합니다.

[연결 추가 대화 상자 ![](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)

확인을 클릭 하면 해당 데이터베이스를 만들 것인지 묻는 메시지가 표시 됩니다. 예를 선택 합니다.

[영화를 만들 ![있나요?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)

이제 서버 탐색기에서 빈 데이터베이스를 가져왔습니다.

![새 테이블 추가](getting-started-with-mvc-part4/_static/image7.png)

테이블을 마우스 오른쪽 단추로 클릭 하 고 테이블 추가를 클릭 합니다. 테이블 디자이너 표시 됩니다. Id, 제목, ReleaseDate, 장르 및 가격에 대 한 열을 추가 합니다. ID 열을 마우스 오른쪽 단추로 클릭 하 고 기본 키 설정을 클릭 합니다. 디자인 영역은 다음과 같습니다.

[![데이터베이스 테이블 편집기](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)

또한 Id 열을 선택 하 고 아래의 열 속성 아래에서 "Id 사양"을 "예"로 변경 합니다.

[![IsIdentity 속성](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)

작업이 완료 되 면 도구 모음에서 저장 아이콘을 클릭 하거나 파일을 선택 합니다. | 메뉴에서를 저장 하 고 테이블 이름을 "**Movie**" (단수형)로 합니다. 데이터베이스와 테이블이 있습니다.

[![이름 선택](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)

서버 탐색기로 돌아가서 동영상 테이블을 마우스 오른쪽 단추로 클릭 한 다음 "테이블 데이터 표시"를 선택 합니다. 데이터베이스에 일부 데이터가 있도록 몇 가지 영화를 입력 합니다.

[데이터베이스 테이블 편집 ![](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)

## <a name="creating-a-model"></a>모델 만들기

이제 IDE의 오른쪽에 있는 솔루션 탐색기로 다시 전환 하 고, 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 |를 선택 합니다. 새 항목입니다.

[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)

새 데이터베이스에서 엔터티 모델을 만들어 보겠습니다. 이렇게 하면 데이터베이스 내에서 데이터를 쉽게 쿼리하고 조작할 수 있는 클래스 집합이 프로젝트에 추가 됩니다. 대화 상자 왼쪽의 데이터 노드를 선택 하 고 ADO.NET 엔터티 데이터 모델 항목 템플릿을 선택 합니다. 이름을 동영상과 .edmx로 합니다.

[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)

"추가" 단추를 클릭 합니다. 그러면 "엔터티 데이터 모델 마법사"가 시작 됩니다.

팝업 되는 새 대화 상자에서 데이터베이스에서 생성을 선택 합니다. 방금 데이터베이스를 만들었으므로 새 데이터베이스와 해당 테이블에 대 한 Entity Framework에만 알려 드리겠습니다. 다음을 클릭 하 여 데이터베이스 연결을 웹 응용 프로그램의 구성에 저장 합니다. 이제 테이블 및 동영상 확인란을 선택 하 고 마침을 클릭 합니다.

[![엔터티 데이터 모델 마법사](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)

이제 Entity Framework Designer에서 새 동영상 테이블을 확인 하 고 코드에서 액세스할 수 있습니다.

[![영화-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)

디자인 화면에서 "동영상" 클래스를 볼 수 있습니다. 이 클래스는 데이터베이스의 "동영상" 테이블에 매핑되고 그 안의 각 속성은 테이블이 있는 열에 매핑됩니다. "Movie" 클래스의 각 인스턴스는 "Movie" 테이블 내의 행에 해당 합니다.

Entity Framework에서 사용 하는 기본 명명 및 매핑 규칙을 원하지 않는 경우 Entity Framework 디자이너를 사용 하 여 변경 하거나 사용자 지정할 수 있습니다. 이 응용 프로그램의 경우 기본값을 사용 하 고 파일을 있는 그대로 저장 합니다.

이제 몇 가지 실제 데이터로 작업 하겠습니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part3.md)
> [다음](getting-started-with-mvc-part5.md)
