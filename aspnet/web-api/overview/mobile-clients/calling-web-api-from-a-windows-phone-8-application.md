---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: Windows Phone 8 응용 프로그램에서 Web API 호출 (C#)-ASP.NET 4.x
author: rmcmurray
description: '코드를 사용한 자습서: Windows Phone 8 응용 프로그램에 책 카탈로그를 제공 하는 ASP.NET 4.x에 ASP.NET Web API 응용 프로그램을 만듭니다.'
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498215"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a>Windows Phone 8 애플리케이션에서 Web API 호출(C#)

[Robert McMurray](https://github.com/rmcmurray)

이 자습서에서는 Windows Phone 8 응용 프로그램에 책 카탈로그를 제공 하는 ASP.NET Web API 응용 프로그램으로 구성 되는 완전 한 종단 간 시나리오를 만드는 방법에 대해 알아봅니다.

### <a name="overview"></a>개요

ASP.NET Web API와 같은 RESTful 서비스는 서버 쪽 및 클라이언트 쪽 응용 프로그램에 대 한 아키텍처를 추상화 하 여 개발자를 위한 HTTP 기반 응용 프로그램 만들기를 간소화 합니다. 통신을 위한 전용 소켓 기반 프로토콜을 만드는 대신 웹 API 개발자는 응용 프로그램에 대 한 필수 HTTP 메서드 (예: GET, POST, PUT, DELETE)를 게시 하 고 클라이언트 응용 프로그램 개발자만을 사용 해야 합니다. 응용 프로그램에 필요한 HTTP 메서드입니다.

이 종단 간 자습서에서는 Web API를 사용 하 여 다음 프로젝트를 만드는 방법에 대해 설명 합니다.

- [이 자습서의 첫 번째 부분](#STEP1)에서는 책 카탈로그를 관리 하기 위한 모든 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업을 지 원하는 ASP.NET Web API 응용 프로그램을 만듭니다. 이 응용 프로그램은 MSDN의 [샘플 Xml 파일 (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) 을 사용 합니다.
- [이 자습서의 두 번째 부분](#STEP2)에서는 Web API 응용 프로그램에서 데이터를 검색 하는 대화형 Windows Phone 8 응용 프로그램을 만듭니다.

#### <a name="prerequisites"></a>사전 요구 사항

- Windows Phone 8 SDK가 설치 된 Visual Studio 2013
- Hyper-v가 설치 된 64 비트 시스템의 Windows 8 이상
- 추가 요구 사항 목록은 [WINDOWS PHONE SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) 다운로드 페이지의 *시스템 요구 사항* 섹션을 참조 하세요.

> [!NOTE]
> Web API와 로컬 시스템의 Windows Phone 8 프로젝트 간의 연결을 테스트 하려는 경우 테스트 환경을 설정 하려면 *[Windows Phone 8 에뮬레이터를 로컬 컴퓨터의 웹 Api 응용 프로그램에 연결](https://go.microsoft.com/fwlink/?LinkId=324014)* 문서의 지침을 따라야 합니다.

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a>1 단계: Web API 서 점 프로젝트 만들기

이 종단 간 자습서의 첫 번째 단계는 모든 CRUD 작업을 지 원하는 Web API 프로젝트를 만드는 것입니다. 이 자습서의 [2 단계](#STEP2) 에서는이 솔루션에 Windows Phone 응용 프로그램 프로젝트를 추가 합니다.

1. **Visual Studio 2013**를 엽니다.
2. **파일**, **새로 만들기**, **프로젝트**를 차례로 클릭 합니다.
3. **새 프로젝트** 대화 상자가 표시 되 면 **설치 됨**, **템플릿**, **C#시각적 개체**, **웹**을 차례로 확장 합니다.

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                확장 하려면 이미지를 클릭 합니다.                                                                |

4. **ASP.NET 웹 응용 프로그램**을 강조 표시 하 고 프로젝트 이름으로 서 **점** 을 입력 한 다음 **확인**을 클릭 합니다.
5. **새 ASP.NET 프로젝트** 대화 상자가 표시 되 면 **Web API** 템플릿을 선택 하 고 **확인**을 클릭 합니다.

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                확장 하려면 이미지를 클릭 합니다.                                                                |

6. Web API 프로젝트가 열리면 프로젝트에서 샘플 컨트롤러를 제거 합니다.

    1. 솔루션 탐색기에서 **컨트롤러** 폴더를 확장 합니다.
    2. **ValuesController.cs** 파일을 마우스 오른쪽 단추로 클릭 한 다음 **삭제**를 클릭 합니다.
    3. 삭제를 확인 하는 메시지가 표시 되 면 **확인** 을 클릭 합니다.
7. Web API 프로젝트에 XML 데이터 파일을 추가 합니다. 이 파일에는 서 점 카탈로그의 내용이 포함 됩니다.

   1. 솔루션 탐색기에서 **App\_Data** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 항목**을 클릭 합니다.
   2. **새 항목 추가** 대화 상자가 표시 되 면 **XML 파일** 템플릿을 강조 표시 합니다.
   3. **Books.xml**파일의 이름을 지정한 다음 **추가**를 클릭 합니다.
   4. **Books.xml** 파일을 열면 파일의 코드를 MSDN의 sample **.xml** 파일에 있는 xml로 바꿉니다. 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. XML 파일을 저장 하 고 닫습니다.

8. 웹 API 프로젝트에 서 점 모델을 추가 합니다. 이 모델은 응용 프로그램 응용 프로그램에 대 한 CRUD (만들기, 읽기, 업데이트 및 삭제) 논리를 포함 합니다.

   1. 솔루션 탐색기에서 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **클래스**를 클릭 합니다.
   2. **새 항목 추가** 대화 상자가 표시 되 면 클래스 파일의 이름을 **BookDetails.cs**로 지정한 다음 **추가**를 클릭 합니다.
   3. **BookDetails.cs** 파일이 열리면 파일의 코드를 다음으로 바꿉니다. 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. **BookDetails.cs** 파일을 저장 하 고 닫습니다.

9. 웹 작업 컨트롤러를 웹 API 프로젝트에 추가 합니다.

   1. 솔루션 탐색기에서 **컨트롤러** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **컨트롤러**를 클릭 합니다.
   2. **스 캐 폴드 추가** 대화 상자가 표시 되 면 **Web API 2 컨트롤러-비어 있음**을 강조 표시 하 고 **추가**를 클릭 합니다.
   3. **컨트롤러 추가** 대화 상자가 표시 되 면 컨트롤러 이름을 **bookscontroller**로 지정한 다음 **추가**를 클릭 합니다.
   4. **BooksController.cs** 파일이 열리면 파일의 코드를 다음으로 바꿉니다. 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. **BooksController.cs** 파일을 저장 하 고 닫습니다.

10. 웹 API 응용 프로그램을 빌드하여 오류를 확인 합니다.

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a>2 단계: Windows Phone 8 서 점 카탈로그 프로젝트 추가

이 종단 간 시나리오의 다음 단계는 Windows Phone 8 용 카탈로그 응용 프로그램을 만드는 것입니다. 이 응용 프로그램은 기본 사용자 인터페이스에 대 한 *Windows Phone 데이터 바인딩된 앱* 템플릿을 사용 하며,이 자습서의 [1 단계](#STEP1) 에서 만든 웹 API 응용 프로그램을 데이터 원본으로 사용 합니다.

1. 솔루션 탐색기에서의 서 **점** 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 프로젝트**를 클릭 합니다.
2. **새 프로젝트** 대화 상자가 표시 되 면 **설치 됨**, **C#시각적 개체**를 차례로 확장 한 다음 **Windows Phone**합니다.
3. **데이터 바인딩된 앱 Windows Phone**강조 표시 하 고 이름으로 **bookcatalog** 를 입력 한 다음 **확인**을 클릭 합니다.
4. Json.NET NuGet 패키지를 **Bookcatalog** 프로젝트에 추가 합니다.

    1. 솔루션 탐색기에서 **Bookcatalog** 프로젝트에 대 한 **참조** 를 마우스 오른쪽 단추로 클릭 한 다음 **NuGet 패키지 관리**를 클릭 합니다.
    2. **NuGet 패키지 관리** 대화 상자가 표시 되 면 **온라인** 섹션을 확장 하 고 **nuget.org**를 강조 표시 합니다.
    3. 검색 필드에 **Json.NET** 를 입력 하 고 검색 아이콘을 클릭 합니다.
    4. 검색 결과에서 **Json.NET** 를 강조 표시 하 고 **설치**를 클릭 합니다.
    5. 설치가 완료 되 면 **닫기**를 클릭 합니다.
5. Bookdetails 프로젝트에 **Bookdetails** 모델 을 추가 합니다. 여기에는 클래스의 일반 모델 (:)이 포함 됩니다.

   1. 솔루션 탐색기에서 **Bookcatalog** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 폴더**를 클릭 합니다.
   2. 새 폴더의 이름을 **모델**로 합니다.
   3. 솔루션 탐색기에서 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **클래스**를 클릭 합니다.
   4. **새 항목 추가** 대화 상자가 표시 되 면 클래스 파일의 이름을 **BookDetails.cs**로 지정한 다음 **추가**를 클릭 합니다.
   5. **BookDetails.cs** 파일이 열리면 파일의 코드를 다음으로 바꿉니다. 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. **BookDetails.cs** 파일을 저장 하 고 닫습니다.

6. **MainViewModel.cs** 클래스를 업데이트 하 여 서 점 웹 API 응용 프로그램과 통신 하는 기능을 포함 합니다.

   1. 솔루션 탐색기에서 **Viewmodels** 폴더를 확장 한 다음 **MainViewModel.cs** 파일을 두 번 클릭 합니다.
   2. **MainViewModel.cs** 파일이 열리면 파일의 코드를 다음으로 바꿉니다. `apiUrl` 상수 값을 Web API의 실제 URL로 업데이트 해야 합니다. 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. **MainViewModel.cs** 파일을 저장 하 고 닫습니다.

7. **Mainpage** 파일을 업데이트 하 여 응용 프로그램 이름을 사용자 지정 합니다.

   1. 솔루션 탐색기에서 **Mainpage .xaml** 파일을 두 번 클릭 합니다.
   2. **Mainpage .xaml** 파일을 열면 다음 코드 줄을 찾습니다. 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. 해당 줄을 다음으로 바꿉니다. 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. **Mainpage .xaml** 파일을 저장 한 후 닫습니다.

8. **DetailsPage** 파일을 업데이트 하 여 표시 된 항목을 사용자 지정 합니다.

   1. 솔루션 탐색기에서 **DetailsPage** 파일을 두 번 클릭 합니다.
   2. **DetailsPage** 파일이 열리면 다음 코드 줄을 찾습니다. 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. 해당 줄을 다음으로 바꿉니다. 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. **DetailsPage** 파일을 저장 하 고 닫습니다.

9. 오류를 확인 하는 Windows Phone 응용 프로그램을 빌드합니다.

### <a name="step-3-testing-the-end-to-end-solution"></a>3 단계: 종단 간 솔루션 테스트

이 자습서의 *전제 조건* 섹션에서 설명한 것 처럼 로컬 시스템에서 web api와 Windows Phone 8 프로젝트 간의 연결을 테스트할 때 테스트 환경을 설정 하려면 *[로컬 컴퓨터에서 Web api 응용 프로그램에 Windows Phone 8 에뮬레이터 연결](https://go.microsoft.com/fwlink/?LinkId=324014)* 문서에 설명 된 지침을 따라야 합니다.

테스트 환경을 구성한 후에는 Windows Phone 응용 프로그램을 시작 프로젝트로 설정 해야 합니다. 이렇게 하려면 솔루션 탐색기에서 **Bookcatalog** 응용 프로그램을 강조 표시 하 고 **시작 프로젝트로 설정**을 클릭 합니다.

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| 확장 하려면 이미지를 클릭 합니다. |

F5 키를 누르면 Visual Studio에서 Windows Phone 에뮬레이터를 모두 시작 합니다 .이 에뮬레이터는 웹 API에서 응용 프로그램 데이터를 검색 하는 동안&quot; &quot;를 표시 합니다.

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| 확장 하려면 이미지를 클릭 합니다. |

모든 작업이 성공 하면 카탈로그가 표시 됩니다.

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| 확장 하려면 이미지를 클릭 합니다. |

책 제목을 누르면 응용 프로그램에 책 설명이 표시 됩니다.

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| 확장 하려면 이미지를 클릭 합니다. |

응용 프로그램이 Web API와 통신할 수 없는 경우 다음과 같은 오류 메시지가 표시 됩니다.

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| 확장 하려면 이미지를 클릭 합니다. |

오류 메시지를 탭 하면 오류에 대 한 추가 정보가 표시 됩니다.

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 확장 하려면 이미지를 클릭 합니다.                                                                 |
