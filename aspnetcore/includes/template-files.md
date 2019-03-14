---
ms.openlocfilehash: eb2f83504129ae2b19ff5d85a2bc7d90293b43d6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043400"
---
* Startup.cs: [Startup 클래스](xref:fundamentals/startup) -클래스에는 응용 프로그램에 대 한 모든 요청을 처리 하는 요청 파이프라인을 구성 합니다.
* Program.cs: [클래스 프로그래밍](xref:fundamentals/index) 응용 프로그램의 주 진입점을 포함 하는 합니다.
* firstapp.csproj : [프로젝트 파일](/dotnet/articles/core/preview3/tools/csproj) ASP.NET Core 응용 프로그램에 대 한 MSBuild 프로젝트 파일 형식입니다. 프로젝트 간 참조가 NuGet 참조 및 기타 관련된 항목을 프로젝트입니다.
* appsettings.json / appsettings 합니다. Development.json: 환경 기본 앱 설정 구성 파일입니다. [구성 참조](xref:fundamentals/configuration/index)합니다.
* bower.json : Bower 패키지 종속성을 프로젝트에 대 한 합니다.
* .bowerrc : Bower 자산을 다운로드 하는 경우 구성 요소를 설치할 위치를 정의 하는 bower 구성 파일입니다.
* bundleconfig.json: 프런트 엔드 JavaScript 및 CSS 자산 묶음 및 축소에 대 한 구성 파일입니다.
* 레이아웃: Razor 뷰를 포함합니다. 보기는 앱의 UI(사용자 인터페이스)를 표시하는 구성 요소입니다. 일반적으로 이 UI는 모델 데이터를 표시합니다.
* 컨트롤러: MVC 컨트롤러를 처음에 포함 *HomeController.cs*합니다. 컨트롤러는 브라우저 요청을 처리 하는 클래스입니다.
* wwwroot: 웹 응용 프로그램 루트 폴더입니다.

자세한 내용은 참조 [MVC 패턴](xref:mvc/overview)합니다.
