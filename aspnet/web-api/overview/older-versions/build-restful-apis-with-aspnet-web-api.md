---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: ASP.NET Web API-ASP.NET 4.x를 사용 하 여 RESTful Api 빌드
author: rick-anderson
description: '실습: ASP.NET 4.x의 Web API를 사용 하 여 연락처 관리자 응용 프로그램에 대 한 간단한 REST API을 빌드합니다.'
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504269"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a>ASP.NET Web API를 사용 하 여 RESTful Api 빌드

[웹 캠프 팀](https://twitter.com/webcamps)

> 실습: ASP.NET 4.x의 Web API를 사용 하 여 연락처 관리자 응용 프로그램에 대 한 간단한 REST API을 빌드합니다. API를 사용 하는 클라이언트도 빌드합니다.

최근 몇 년 동안 HTTP는 HTML 페이지를 제공 하는 것이 아니라는 것이 분명 합니다. 또한 몇 가지 동사 (GET, POST 등) 뿐만 아니라 *uri* 및 *헤더*와 같은 몇 가지 간단한 개념을 사용 하 여 웹 api를 빌드하기 위한 강력한 플랫폼입니다. ASP.NET Web API은 HTTP 프로그래밍을 간소화 하는 구성 요소 집합입니다. ASP.NET MVC 런타임 위에 빌드되기 때문에 Web API는 HTTP의 하위 수준 전송 세부 정보를 자동으로 처리 합니다. 동시에 Web API는 HTTP 프로그래밍 모델을 자연스럽 게 노출 합니다. 사실 웹 API의 한 가지 목표는 HTTP의 현실에서 추상화 *하지 않는* 것입니다. 따라서 Web API는 유연 하 고 쉽게 확장할 수 있습니다.  REST 아키텍처 스타일은 http에 대 한 유일한 유효한 방법이 아니라 HTTP를 활용 하는 효과적인 방법으로 입증 되었습니다. 연락처 관리자는 연락처를 나열, 추가 및 제거 하는 RESTful를 노출 합니다. 

이 랩에서는 HTTP, REST에 대 한 기본적인 이해가 필요 하며, HTML, JavaScript 및 jQuery에 대 한 기본적인 작업 지식이 있다고 가정 합니다.
> 
> > [!NOTE]
> > ASP.NET 웹 사이트에는 [https://asp.net/web-api](https://asp.net/web-api)ASP.NET Web API 프레임 워크 전용 영역이 있습니다. 이 사이트는 Web API와 관련 된 최신 정보, 샘플 및 뉴스를 계속 제공 하므로, 거의 모든 장치 또는 개발 프레임 워크에서 사용할 수 있는 사용자 지정 웹 Api를 만드는 데 더 자세히 살펴보겠습니다.
> > 
> > ASP.NET MVC 4와 마찬가지로, 사용 가능한 종속성 주입 프레임 워크를 매우 쉽게 사용할 수 있도록 컨트롤러에서 서비스 계층을 분리 하는 측면에서 상당한 유연성을 제공 합니다. ASP.NET Web API MSDN에는 [여기](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)에서 다운로드할 수 있는 ASP.NET Web API 프로젝트에서 종속성 주입에 대 한 Ninject를 사용 하는 방법을 보여 주는 유용한 샘플이 있습니다.
> 
> 
> 모든 샘플 코드와 코드 조각은 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- RESTful Web API 구현
- HTML 클라이언트에서 API 호출

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 실습 실습을 완료 하려면 다음이 필요 합니다.

- [웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 B](#AppendixB) 를 참조 하세요.)

<a id="Setup"></a>
### <a name="setup"></a>설치 프로그램

**코드 조각 설치**

편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다. 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.

Visual Studio Code 코드 조각에 익숙하지 않은 경우이를 사용 하는 방법을 알아보려면 [부록 A: &quot;코드 조각&quot;사용](#AppendixA) 문서에서 부록을 참조할 수 있습니다.

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩에는 다음 연습이 포함 되어 있습니다.

1. [연습 1: 읽기 전용 웹 API 만들기](#Exercise1)
2. [연습 2: 읽기/쓰기 웹 API 만들기](#Exercise2)
3. [연습 3: HTML 클라이언트에서 Web API 사용](#Exercise3)

> [!NOTE]
> 각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다. 연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.

이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a>연습 1: 읽기 전용 웹 API 만들기

이 연습에서는 연락처 관리자에 대 한 읽기 전용 GET 메서드를 구현 합니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a>작업 1-API 프로젝트 만들기

이 작업에서는 새로운 ASP.NET 웹 프로젝트 템플릿을 사용 하 여 Web API 웹 응용 프로그램을 만듭니다.

1. **Visual Studio 2012 Express For Web**을 실행 하 여 **시작** 으로 이동 하 **VS Express for Web** 입력 한 다음 **enter**키를 누릅니다.
2. **파일** 메뉴에서 **새 프로젝트**를 선택 합니다. **시각적 개체 C# 를 선택 합니다. | 웹** 프로젝트 형식 트리 뷰에서 **ASP.NET MVC 4 웹 응용 프로그램** 프로젝트 형식을 선택 합니다. 프로젝트의 **이름을** " *연락처 관리자* "로 설정 하 고 **솔루션 이름을** *시작*으로 설정한 다음 **확인**을 클릭 합니다.

    ![새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트 만들기](build-restful-apis-with-aspnet-web-api/_static/image1.png "새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트 만들기")

    *새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트 만들기*
3. ASP.NET MVC 4 프로젝트 형식 대화 상자에서 **WEB API** 프로젝트 형식을 선택 합니다. **확인**을 클릭합니다.

    ![웹 API 프로젝트 형식 지정](build-restful-apis-with-aspnet-web-api/_static/image2.png "웹 API 프로젝트 형식 지정")

    *웹 API 프로젝트 형식 지정*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a>작업 2-연락처 관리자 API 컨트롤러 만들기

이 작업에서는 API 메서드가 상주할 컨트롤러 클래스를 만듭니다.

1. 프로젝트에서 **Controllers** 폴더에 있는 **ValuesController.cs** 라는 파일을 삭제 합니다.
2. 프로젝트의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 컨트롤러** 를 시작 합니다.

    ![프로젝트에 새 컨트롤러 추가](build-restful-apis-with-aspnet-web-api/_static/image3.png "프로젝트에 새 컨트롤러 추가")

    *프로젝트에 새 컨트롤러 추가*
3. 표시 되는 **컨트롤러 추가** 대화 상자의 템플릿 메뉴에서 **빈 API 컨트롤러** 를 선택 합니다. **Controller 클래스의**이름을 함께로 합니다. 그런 다음 추가를 클릭 **합니다.**

    ![컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러 만들기](build-restful-apis-with-aspnet-web-api/_static/image4.png "컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러 만들기")

    *컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러 만들기*
4. 다음 코드를 **연락처 컨트롤러**에 추가 합니다.

    (코드 조각- *WEB Api Lab-Ex01-Api 메서드 가져오기*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. **F5** 키를 눌러 애플리케이션을 디버그합니다. 웹 API 프로젝트에 대 한 기본 홈 페이지가 표시 됩니다.

    ![ASP.NET Web API 응용 프로그램의 기본 홈 페이지](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 응용 프로그램의 기본 홈 페이지")

    *ASP.NET Web API 응용 프로그램의 기본 홈 페이지*
6. Internet Explorer 창에서 **F12** 키를 눌러 **개발자 도구** 창을 엽니다. **네트워크** 탭을 클릭 한 다음 **캡처 시작** 단추를 클릭 하 여 창으로의 네트워크 트래픽 캡처를 시작 합니다.

    ![네트워크 탭을 열고 네트워크 캡처 시작](build-restful-apis-with-aspnet-web-api/_static/image6.png "네트워크 탭을 열고 네트워크 캡처 시작")

    *네트워크 탭을 열고 네트워크 캡처 시작*
7. URL을 브라우저의 주소 표시줄에 **/ci/cer&gt** 에 추가 하 고 enter 키를 누릅니다. 전송 세부 정보는 네트워크 캡처 창에 표시 됩니다. 응답의 MIME 형식은 **application/json**입니다. 기본 출력 형식이 JSON 인 방법을 보여 줍니다.

    ![네트워크 보기에서 Web API 요청 출력 보기](build-restful-apis-with-aspnet-web-api/_static/image7.png "네트워크 보기에서 Web API 요청 출력 보기")

    *네트워크 보기에서 Web API 요청 출력 보기*

    > [!NOTE]
    > 이 시점에서 Internet Explorer 10의 기본 동작은 사용자가 웹 API 호출로 인해 발생 하는 스트림을 저장 하거나 열지를 요청 하는 것입니다. 출력은 Web API URL 호출의 JSON 결과가 포함 된 텍스트 파일이 됩니다. 개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있으려면 대화 상자를 취소 하지 마십시오.
8. 이 API 호출의 응답에 대 한 자세한 내용을 보려면 **자세히 보기로 이동** 단추를 클릭 합니다.

    ![자세히 보기로 전환](build-restful-apis-with-aspnet-web-api/_static/image8.png "자세히 보기로 전환")

    *자세히 보기로 전환*
9. **응답 본문** 탭을 클릭 하 여 실제 JSON 응답 텍스트를 확인 합니다.

    ![네트워크 모니터에서 JSON 출력 텍스트 보기](build-restful-apis-with-aspnet-web-api/_static/image9.png "네트워크 모니터에서 JSON 출력 텍스트 보기")

    *네트워크 모니터에서 JSON 출력 텍스트 보기*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a>작업 3-연락처 모델 만들기 및 연락처 컨트롤러 보강

이 작업에서는 API 메서드가 상주할 컨트롤러 클래스를 만듭니다.

1. **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 클래스 ...** 상황에 맞는 메뉴에서.

    ![웹 응용 프로그램에 새 모델 추가](build-restful-apis-with-aspnet-web-api/_static/image10.png "웹 응용 프로그램에 새 모델 추가")

    *웹 응용 프로그램에 새 모델 추가*
2. **새 항목 추가** 대화 상자에서 새 파일의 이름을 **Contact.cs** 로 하 고 **추가를 클릭 합니다.**

    ![새 연락처 클래스 파일 만들기](build-restful-apis-with-aspnet-web-api/_static/image11.png "새 연락처 클래스 파일 만들기")

    *새 연락처 클래스 파일 만들기*
3. **Contact** 클래스에 다음 강조 표시 된 코드를 추가 합니다.

    (코드 조각- *WEB API Lab-Ex01 클래스*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. 연락처 **컨트롤러** 클래스에서 **Get** 메서드의 메서드 정의에 있는 단어 **문자열** 을 선택 하 고 *Contact*라는 단어를 입력 합니다. 단어가 입력 되 면 **연락처**의 시작 부분에 표시기가 표시 됩니다. **Ctrl** 키를 누른 채 마침표 (.) 키를 누르거나 마우스를 사용 하 여 아이콘을 클릭 하 여 코드 편집기에서 지원 대화 상자를 열고 모델 네임 스페이스에 대 한 **using** 지시문을 자동으로 채웁니다.

    ![네임 스페이스 선언에 Intellisense 지원 사용](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    *네임 스페이스 선언에 Intellisense 지원 사용*
5. **Get** 메서드에 대 한 코드를 수정 하 여 Contact model 인스턴스의 배열을 반환 합니다.

    (코드 조각- *웹 API 랩-Ex01-연락처 목록 반환*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. **F5** 키를 눌러 브라우저에서 웹 응용 프로그램을 디버깅 합니다. API의 응답 출력에 대 한 변경 내용을 보려면 다음 단계를 수행 합니다.

   1. 브라우저가 열리면 **F12** 키를 누른 상태로 개발자 도구가 아직 열리지 않습니다.
   2. **네트워크** 탭을 클릭 합니다.
   3. **캡처 시작** 단추를 누릅니다.
   4. 주소 표시줄의 URL에 URL 접미사/s a l i o n/ **연락처** 를 추가 하 고 **enter** 키를 누릅니다.
   5. **자세히 보기로 이동** 단추를 누릅니다.
   6. **응답 본문** 탭을 선택 합니다. 연락처 인스턴스 배열의 serialize 된 형식을 나타내는 JSON 문자열이 표시 되어야 합니다.

      ![복합 웹 API 메서드 호출의 JSON 직렬화 된 출력](build-restful-apis-with-aspnet-web-api/_static/image13.png "복합 웹 API 메서드 호출의 JSON 직렬화 된 출력")

      *복합 웹 API 메서드 호출의 JSON 직렬화 된 출력*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a>작업 4-서비스 계층으로 기능 압축 풀기

이 작업에서는 개발자가 서비스 기능을 컨트롤러 계층에서 분리 하 여 실제로 작업을 수행 하는 서비스의 재사용을 가능 하 게 하는 서비스 계층으로 기능을 추출 하는 방법을 보여 줍니다.

1. 솔루션 루트에서 새 폴더를 만들고 이름을 **Services**로 합니다. 이렇게 하려면 프로젝트 **관리자** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** | **새 폴더**를 선택한 다음 이름으로 *서비스*를 추가 합니다.

    ![서비스 폴더를 만드는 중](build-restful-apis-with-aspnet-web-api/_static/image14.png "서비스 폴더를 만드는 중")

    *서비스 폴더를 만드는 중*
2. **서비스** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 클래스 ...** 상황에 맞는 메뉴에서.

    ![서비스 폴더에 새 클래스 추가](build-restful-apis-with-aspnet-web-api/_static/image15.png "서비스 폴더에 새 클래스 추가")

    *서비스 폴더에 새 클래스 추가*
3. **새 항목 추가** 대화 상자가 나타나면 **새 클래스의** 이름을 같은 이름으로 만들고 **추가**를 클릭 합니다.

    ![연락처 리포지토리 서비스 계층에 대 한 코드를 포함 하는 클래스 파일 만들기](build-restful-apis-with-aspnet-web-api/_static/image16.png "연락처 리포지토리 서비스 계층에 대 한 코드를 포함 하는 클래스 파일 만들기")

    *연락처 리포지토리 서비스 계층에 대 한 코드를 포함 하는 클래스 파일 만들기*
4. **ContactRepository.cs** 파일에 using 지시문을 추가 하 여 모델 네임 스페이스를 포함 합니다.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. **ContactRepository.cs** 파일에 다음 강조 표시 된 코드를 추가 하 여 GetAllContacts 메서드를 구현 합니다.

    (코드 조각- *웹 API 랩-Ex01-연락처 리포지토리*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. **ContactController.cs** 파일이 아직 열려 있지 않으면 엽니다.
7. 다음 using 문을 파일의 네임 스페이스 선언 섹션에 추가 합니다.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. **ContactController.cs** 클래스에 다음 강조 표시 된 코드를 추가 하 여 나머지 클래스 멤버가 서비스 구현을 사용할 수 있도록 전용 필드를 리포지토리의 인스턴스를 나타내는 추가 합니다.

    (코드 조각- *WEB API Lab-Ex01-Contact Controller*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. 연락처 리포지토리 서비스를 사용 하도록 **Get** 메서드를 변경 합니다.

    (코드 조각- *WEB API Lab-Ex01-리포지토리를 통해 연락처 목록 반환*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. **연락처 컨트롤러**의 **Get** 메서드 정의에 중단점을 배치 합니다.

   ![Contact controller에 중단점 추가](build-restful-apis-with-aspnet-web-api/_static/image17.png "Contact controller에 중단점 추가")

   *Contact controller에 중단점 추가*
11. **F5** 키를 눌러 애플리케이션을 실행합니다.
12. 브라우저가 열리면 **F12** 키를 눌러 개발자 도구를 엽니다.
13. **네트워크** 탭을 클릭 합니다.
14. **캡처 시작** 단추를 클릭 합니다.
15. 주소 표시줄에 URL을 suffix **/api/contact** 와 함께 추가 하 고 **enter** 키를 눌러 api 컨트롤러를 로드 합니다.
16. **Get** 메서드가 실행을 시작 하면 Visual Studio 2012가 중단 됩니다.

   ![Get 메서드 내에서 중단](build-restful-apis-with-aspnet-web-api/_static/image18.png "Get 메서드 내에서 중단")

   *Get 메서드 내에서 중단*
17. 계속하려면 **F5** 키를 누릅니다.
18. 아직 포커스가 없는 경우 Internet Explorer로 돌아갑니다. 네트워크 캡처 창을 확인 합니다.

    ![웹 API 호출의 결과를 표시 하는 Internet Explorer의 네트워크 보기](build-restful-apis-with-aspnet-web-api/_static/image19.png "웹 API 호출의 결과를 표시 하는 Internet Explorer의 네트워크 보기")

    *웹 API 호출의 결과를 표시 하는 Internet Explorer의 네트워크 보기*
19. **자세히 보기로 이동** 단추를 클릭 합니다.
20. **응답 본문** 탭을 클릭 합니다. API 호출의 JSON 출력과 서비스 계층에서 검색 된 두 개의 연락처를 나타내는 방법을 확인 합니다.

    ![개발자 도구 창에서 Web API의 JSON 출력 보기](build-restful-apis-with-aspnet-web-api/_static/image20.png "개발자 도구 창에서 Web API의 JSON 출력 보기")

    *개발자 도구 창에서 Web API의 JSON 출력 보기*

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a>연습 2: 읽기/쓰기 웹 API 만들기

이 연습에서는 데이터 편집 기능을 사용 하도록 설정 하기 위해 contact manager의 POST 및 PUT 메서드를 구현 합니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a>작업 1-웹 API 프로젝트 열기

이 작업에서는 사용자 입력을 허용할 수 있도록 실습 1에서 만든 웹 API 프로젝트를 향상 시킬 준비를 합니다.

1. **Visual Studio 2012 Express For Web**을 실행 하 여 **시작** 으로 이동 하 **VS Express for Web** 입력 한 다음 **enter**키를 누릅니다.
2. **Source/Ex02-ReadWriteWebAPI/begin/** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
3. **서비스/연락처 리포지토리의 .cs** 파일을 엽니다.

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a>작업 2-연락처 리포지토리 구현에 데이터 지 속성 기능 추가

이 작업에서는 사용자 입력 및 새 연락처 인스턴스를 유지 하 고 허용할 수 있도록 연습 1에서 만든 Web API 프로젝트의 지 수 리포지토리 클래스를 확대 합니다.

1. 이 연습 뒷부분의 웹 서버 캐시 항목 키 이름 이름을 나타내는 다음 상수를 **연락처 리포지토리** 클래스에 추가 합니다.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. 다음 코드를 포함 하는 **연락처 리포지토리에** 생성자를 추가 합니다.

    (코드 조각- *WEB API Lab-Ex02 리포지토리 생성자*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. 아래와 같이 **Getallcontacts** 메서드에 대 한 코드를 수정 합니다.

    (코드 조각- *WEB API Lab-Ex02-모든 연락처 가져오기*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > 이 예제는 데모용 이며, 웹 서버의 캐시를 저장 미디어로 사용 하므로 세션 저장소 메커니즘 또는 요청 저장소 수명을 사용 하지 않고 여러 클라이언트에서 동시에 값을 사용할 수 있도록 합니다. Entity Framework, XML 저장소 또는 웹 서버 캐시를 사용 하는 기타 다양 한 항목을 사용할 수 있습니다.
4. 연락처를 저장 하는 작업을 수행 하려면 **SaveContact** 이라는 새 메서드를 지 수 **리포지토리** 클래스에 구현 합니다. **SaveContact** 메서드는 단일 **연락** 매개 변수를 사용 하 고 성공 또는 실패를 나타내는 부울 값을 반환 해야 합니다.

    (코드 조각- *WEB API Lab-Ex02-SaveContact 메서드 구현*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a>연습 3: HTML 클라이언트에서 Web API 사용

이 연습에서는 Web API를 호출 하는 HTML 클라이언트를 만듭니다. 이 클라이언트는 JavaScript를 사용 하 여 Web API와의 데이터 교환을 용이 하 게 하 고 HTML 태그를 사용 하 여 웹 브라우저에 결과를 표시 합니다.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a>작업 1-연락처 표시를 위한 GUI를 제공 하도록 인덱스 뷰 수정

이 태스크에서는 HTML 브라우저에서 기존 연락처 목록을 표시 하기 위한 요구 사항을 지원 하도록 웹 응용 프로그램의 기본 인덱스 뷰를 수정 합니다.

1. 아직 열려 있지 않은 경우 **Visual Studio 2012 Express For Web을** 엽니다.
2. **Source/Ex03-ConsumingWebAPI/begin/** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
3. **뷰/홈** 폴더에 있는 **인덱스 cshtml** 파일을 엽니다.
4. Div 요소 내에 있는 HTML 코드를 다음 코드와 같이 id **본문** 으로 바꿉니다.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. 다음 Javascript 코드를 파일의 맨 아래에 추가 하 여 웹 API에 대 한 HTTP 요청을 수행 합니다.

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. **ContactController.cs** 파일이 아직 열려 있지 않으면 엽니다.
7. **연락처 컨트롤러** 클래스의 **Get** 메서드에 중단점을 설정 합니다.

    ![API 컨트롤러의 Get 메서드에 중단점 배치](build-restful-apis-with-aspnet-web-api/_static/image21.png "API 컨트롤러의 Get 메서드에 중단점 배치")

    *API 컨트롤러의 Get 메서드에 중단점 배치*
8. **F5** 키를 눌러 프로젝트를 실행합니다. 브라우저에서 HTML 문서를 로드 합니다.

    > [!NOTE]
    > 응용 프로그램의 루트 URL을 탐색 하 고 있는지 확인 합니다.
9. 페이지가 로드 되 고 JavaScript가 실행 되 면 중단점에 도달 하 고 컨트롤러에서 코드 실행이 일시 중지 됩니다.

    ![VS Express for Web를 사용 하 여 웹 API 호출 디버깅](build-restful-apis-with-aspnet-web-api/_static/image22.png "VS Express for Web를 사용 하 여 웹 API 호출 디버깅")

    *Visual Studio 2012 Express for Web을 사용 하 여 웹 API 호출로 디버깅*
10. 중단점을 제거 하 고 **F5** 키를 누르거나 디버그 도구 모음의 **계속** 단추를 클릭 하 여 브라우저에서 보기를 계속 로드 합니다. 웹 API 호출이 완료 되 면 브라우저에서 목록 항목으로 표시 되는 웹 API 호출에서 반환 된 연락처가 표시 됩니다.

    ![브라우저에 목록 항목으로 표시 되는 API 호출의 결과](build-restful-apis-with-aspnet-web-api/_static/image23.png "브라우저에 목록 항목으로 표시 되는 API 호출의 결과")

    *브라우저에 목록 항목으로 표시 되는 API 호출의 결과*
11. 디버깅을 중지합니다.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a>작업 2-연락처를 만들기 위한 GUI를 제공 하도록 인덱스 보기 수정

이 태스크에서는 MVC 응용 프로그램의 인덱스 뷰를 계속 수정 합니다. 사용자 입력을 캡처하고 웹 API로 보내서 새 연락처를 만드는 양식이 HTML 페이지에 추가 되 고, GUI에서 날짜를 수집 하기 위해 새 Web API 컨트롤러 메서드가 생성 됩니다.

1. **ContactController.cs** 파일을 엽니다.
2. 다음 코드와 같이 **Post** 라는 컨트롤러 클래스에 새 메서드를 추가 합니다.

    (코드 조각- *WEB API 랩-Ex03-Post 메서드*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. 아직 열려 있지 않은 경우 Visual Studio에서 **이 파일을 엽니다.**
4. 이전 작업에서 추가한 순서가 지정 되지 않은 목록 바로 뒤의 파일에 아래 HTML 코드를 추가 합니다.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. 문서 아래쪽의 script 요소 내에서 다음 강조 표시 된 코드를 추가 하 여 단추 클릭 이벤트를 처리 합니다. 그러면 HTTP POST 호출을 사용 하 여 Web API에 데이터를 게시할 수 있습니다.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. **ContactController.cs**에서 **Post** 메서드에 중단점을 추가 합니다.
7. 브라우저에서 응용 프로그램을 실행 하려면 **f5** 키를 누릅니다.
8. 페이지가 브라우저에 로드 되 면 새 연락처 이름 및 Id를 입력 하 고 **저장** 단추를 클릭 합니다.

    ![브라우저에 로드 된 클라이언트 HTML 문서](build-restful-apis-with-aspnet-web-api/_static/image24.png "브라우저에 로드 된 클라이언트 HTML 문서")

    *브라우저에 로드 된 클라이언트 HTML 문서*
9. **Post** 메서드에서 디버거 창이 중단 되 면 **contact** 매개 변수의 속성을 확인 합니다. 값은 폼에 입력 한 데이터와 일치 해야 합니다.

    ![클라이언트에서 Web API로 전송 되는 Contact 개체입니다.](build-restful-apis-with-aspnet-web-api/_static/image25.png "클라이언트에서 Web API로 전송 되는 Contact 개체입니다.")

    *클라이언트에서 Web API로 전송 되는 Contact 개체입니다.*
10. **응답** 변수를 만들 때까지 디버거의 메서드를 단계별로 실행 합니다. 디버거의 **지역** 창에서 검사 하면 모든 속성이 설정 된 것을 볼 수 있습니다.

   ![디버거에서 만든 다음 응답](build-restful-apis-with-aspnet-web-api/_static/image26.png "디버거에서 만든 다음 응답")

   *디버거에서 만든 다음 응답*
11. **F5** 키를 누르거나 디버거에서 **계속** 을 클릭 하면 요청이 완료 됩니다. 브라우저로 다시 전환 하면 새 연락처가 연락처 **리포지토리** 구현에 의해 저장 된 연락처 목록에 추가 됩니다.

   ![브라우저에서 새 연락처 인스턴스가 성공적으로 생성 된 것을 반영 합니다.](build-restful-apis-with-aspnet-web-api/_static/image27.png "브라우저에서 새 연락처 인스턴스가 성공적으로 생성 된 것을 반영 합니다.")

   *브라우저에서 새 연락처 인스턴스가 성공적으로 생성 된 것을 반영 합니다.*

> [!NOTE]
> 또한 웹 배포를 사용 하 여이 응용 프로그램을 Azure에 배포할 수 있습니다 [. 부록 C: ASP.NET MVC 4 응용 프로그램 게시.](#AppendixC)

---

<a id="Summary"></a>
## <a name="summary"></a>요약

이 랩에서는 새로운 ASP.NET Web API 프레임 워크 및 프레임 워크를 사용 하 여 RESTful Web Api의 구현에 대해 소개 했습니다. 여기에서 다양 한 메커니즘을 사용 하 여 데이터 지 속성을 용이 하 게 하 고이 랩에서 예제로 제공 되는 간단한 것이 아니라 서비스를 제공 하는 새 리포지토리를 만들 수 있습니다. Web API는 HTTP 및 JSON 또는 XML을 지 원하는 언어로 작성 된 비 HTML 클라이언트 로부터의 통신을 사용 하도록 설정 하는 등의 다양 한 추가 기능을 지원 합니다. 일반적인 웹 응용 프로그램 외부에서 Web API를 호스트 하는 기능을 사용할 수도 있으며 사용자 고유의 serialization 형식을 만들 수도 있습니다.

ASP.NET 웹 사이트에는 [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api)ASP.NET Web API 프레임 워크 전용 영역이 있습니다. 이 사이트는 Web API와 관련 된 최신 정보, 샘플 및 뉴스를 계속 제공 하므로, 거의 모든 장치 또는 개발 프레임 워크에서 사용할 수 있는 사용자 지정 웹 Api를 만드는 데 더 자세히 살펴보겠습니다.

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>부록 A: 코드 조각 사용

코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다. 랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](build-restful-apis-with-aspnet-web-api/_static/image28.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")

*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a>키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)

1. 코드를 삽입할 위치에 커서를 놓습니다.
2. 조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.
3. IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.
4. 올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.
5. Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.

    ![코드 조각 이름 입력 시작](build-restful-apis-with-aspnet-web-api/_static/image29.png "코드 조각 이름 입력 시작")

    *코드 조각 이름 입력 시작*

    ![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](build-restful-apis-with-aspnet-web-api/_static/image30.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")

    *Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*

    ![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](build-restful-apis-with-aspnet-web-api/_static/image31.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")

    *Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a>마우스 (C#, VISUAL BASIC 및 XML)를 사용 하 여 코드 조각을 추가 하려면

1. 코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.
2. 코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.
3. 목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.

    ![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](build-restful-apis-with-aspnet-web-api/_static/image32.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")

    *코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*

    ![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](build-restful-apis-with-aspnet-web-api/_static/image33.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")

    *목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>부록 B: 웹에 대 한 Visual Studio Express 2012 설치

**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다. 다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> 제품 &quot;검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![Visual Studio Express 설치](build-restful-apis-with-aspnet-web-api/_static/image34.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.
8. 웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.

    ![VS Express for Web 타일](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    *VS Express for Web 타일*

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 C: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록에서는 azure Portal에서 새 웹 사이트를 만들고 랩에 따라 얻은 응용 프로그램을 게시 하 여 Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>작업 1-Azure 포털에서 새 웹 사이트 만들기

1. [Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 다음 트래픽이 증가 함에 따라 크기를 조정할 수 있습니다. [여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.

    ![Windows Azure Portal에 로그온 합니다.](build-restful-apis-with-aspnet-web-api/_static/image39.png "Windows Azure Portal에 로그온 합니다.")

    *포털에 로그온*
2. 명령 모음에서 **새로 만들기** 를 클릭 합니다.

    ![새 웹 사이트 만들기](build-restful-apis-with-aspnet-web-api/_static/image40.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. **Compute** | **웹 사이트**를 클릭 합니다. 그런 다음 **빠른 생성** 옵션을 선택 합니다. 새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.

    > [!NOTE]
    > Azure는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다. 빠른 생성 옵션을 사용 하면 포털 외부에서 완료 된 웹 응용 프로그램을 Azure에 배포할 수 있습니다. 데이터베이스를 설정 하는 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트 만들기](build-restful-apis-with-aspnet-web-api/_static/image41.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 **웹 사이트가** 만들어질 때까지 기다립니다.
5. 웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트로 이동](build-restful-apis-with-aspnet-web-api/_static/image42.png "새 웹 사이트로 이동")

    *새 웹 사이트로 이동*

    ![웹 사이트 실행 중](build-restful-apis-with-aspnet-web-api/_static/image43.png "웹 사이트 실행 중")

    *웹 사이트 실행 중*
6. 포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.

    ![웹 사이트 관리 페이지 열기](build-restful-apis-with-aspnet-web-api/_static/image44.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.

    > [!NOTE]
    > *게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Azure에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다. 게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 Azure에 웹 응용 프로그램을 게시 하기 위해 이러한 프로그램의 구성을 자동화 하는 게시 프로필 읽기를 지원 합니다.

    ![웹 사이트 게시 프로필을 다운로드 하는 중](build-restful-apis-with-aspnet-web-api/_static/image45.png "웹 사이트 게시 프로필을 다운로드 하는 중")

    *웹 사이트 게시 프로필을 다운로드 하는 중*
8. 알려진 위치에 게시 프로필 파일을 다운로드 합니다. 이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Azure에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.

    ![게시 프로필 파일을 저장 하는 중](build-restful-apis-with-aspnet-web-api/_static/image46.png "게시 프로필을 저장 하는 중")

    *게시 프로필 파일을 저장 하는 중*

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다. SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다. Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL database** | **Servers** | **서버 대시보드**. 만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다. 다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다. 이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.

    ![SQL Database 서버 대시보드](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다. 이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](build-restful-apis-with-aspnet-web-api/_static/image48.png) 단추를 클릭 합니다.

    ![클라이언트 IP 주소를 추가 하는 중](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    *클라이언트 IP 주소를 추가 하는 중*
3. **클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.

    ![변경 내용 확인](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    *변경 내용 확인*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션으로 돌아갑니다. **솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.

    ![응용 프로그램 게시](build-restful-apis-with-aspnet-web-api/_static/image51.png "응용 프로그램 게시")

    *웹 사이트 게시*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필을 가져오는 중](build-restful-apis-with-aspnet-web-api/_static/image52.png "게시 프로필을 가져오는 중")

    *게시 프로필을 가져오는 중*
3. **연결 유효성 검사**를 클릭 합니다. 유효성 검사가 완료 되 면 **다음**을 클릭 합니다.

    > [!NOTE]
    > 유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.

    ![연결 유효성 검사](build-restful-apis-with-aspnet-web-api/_static/image53.png "연결 유효성 검사")

    *연결 유효성 검사*
4. **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.

    ![웹 배포 구성](build-restful-apis-with-aspnet-web-api/_static/image54.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - **서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.
   - **사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 에 서버 관리자 로그인 암호를 입력 합니다.
   - 새 데이터베이스 이름 (예: *MVC4SampleDB*)을 입력 합니다.

     ![대상 연결 문자열 구성](build-restful-apis-with-aspnet-web-api/_static/image55.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 후 **OK**를 클릭합니다. 데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.

    ![데이터베이스 만들기](build-restful-apis-with-aspnet-web-api/_static/image56.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다. 그런 후 **Next** 를 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](build-restful-apis-with-aspnet-web-api/_static/image57.png "SQL Database를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. **미리 보기** 페이지에서 **게시**를 클릭 합니다.

    ![웹 응용 프로그램 게시](build-restful-apis-with-aspnet-web-api/_static/image58.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.

    ![Windows Azure에 게시 된 응용 프로그램](build-restful-apis-with-aspnet-web-api/_static/image59.png "Windows Azure에 게시 된 응용 프로그램")

    *Azure에 게시 된 응용 프로그램*
