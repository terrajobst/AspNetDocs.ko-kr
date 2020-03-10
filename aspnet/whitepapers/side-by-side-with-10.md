---
uid: whitepapers/side-by-side-with-10
title: ASP.NET .NET Framework 1.0 및 1.1의 Side-by-side 실행 | Microsoft Docs
author: rick-anderson
description: 이 백서에서는 컴퓨터에 .NET 1.0 및 .NET 1.1를 모두 설치 하 여 ASP.NET 웹 응용 프로그램이 두 버전의 fram에서 실행 되도록 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513833"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a>.NET Framework 1.0 및 1.1의 ASP.NET Side-by-Side 실행

> 이 백서에서는 컴퓨터에 .NET 1.0 및 .NET 1.1를 모두 설치 하 여 ASP.NET 웹 응용 프로그램이 두 가지 버전의 프레임 워크에서 실행 될 수 있도록 하는 방법을 설명 합니다.
> 
> ASP.NET 1.0 및 ASP.NET 1.1에 적용 됩니다.

ASP.NET에서는 응용 프로그램을 동일한 컴퓨터에 설치 하 고 다른 버전의 .NET Framework를 사용 하는 경우 함께 실행 하는 것으로 간주 됩니다. 다음 항목에서는 side-by-side 실행을 위해 ASP.NET 응용 프로그램을 구성 하는 방법에 대해 설명 하 고 다음에 대 한 자세한 단계를 제공 합니다.

- [설치 하는 동안 .NET Framework 버전 1.0에 대 한 웹 응용 프로그램의 매핑을 유지 합니다.](#1)
- [웹 응용 프로그램을 특정 버전의 .NET Framework에 매핑](#2)
- [웹 사이트에서 사용 하는 .NET Framework 버전 찾기](#3)

일반적으로 컴퓨터에서 구성 요소나 응용 프로그램을 업데이트 하면 이전 버전이 제거 되 고 최신 버전으로 대체 됩니다. 새 버전이 이전 버전과 호환 되지 않는 경우이는 일반적으로 구성 요소 또는 응용 프로그램을 사용 하는 다른 응용 프로그램을 중단 합니다. .NET Framework는 side-by-side 실행을 지원 합니다 .이를 통해 여러 버전의 어셈블리 또는 응용 프로그램을 동시에 같은 컴퓨터에 설치할 수 있습니다. 여러 버전을 동시에 설치할 수 있으므로 관리 되는 응용 프로그램은 다른 버전을 사용 하는 응용 프로그램에 영향을 주지 않고 사용할 버전을 선택할 수 있습니다.

기본적으로 .NET Framework 버전 1.1을 설치 하는 동안 모든 기존 ASP.NET 응용 프로그램은 최신 버전의 .NET Framework를 사용 하도록 자동으로 다시 구성 됩니다. ASP.NET 응용 프로그램을 기본적으로 .NET Framework 1.1으로 설정 하지 않으려는 경우 설치 하는 동안이를 방지 하는 방법을 알아보려면 [여기](#1) 를 클릭 하십시오.

1\.1 .NET Framework 웹 서버를 업데이트 하 고 하나 이상의 웹 응용 프로그램을 .NET Framework 1.0를 실행 하려면 인터넷 정보 서비스 (IIS) 스크립트 맵을 업데이트 해야 합니다. 스크립트 매핑은 특정 웹 응용 프로그램에 대 한 .aspx 파일 확장명을 .NET Framework 버전에 매핑하는 메커니즘입니다. 웹 응용 프로그램을 특정 버전의 .NET Framework에 매핑하는 방법을 알아보려면 [여기](#2) 를 클릭 하십시오.

인터넷 정보 관리자 또는 ASP.NET IIS 등록 도구 (Aspnet\_regiis .exe)를 사용 하 여 특정 웹 응용 프로그램을 실행 하는 .NET Framework 버전을 찾을 수 있습니다. 웹 사이트에서 사용 하는 .NET Framework 버전을 확인 하는 방법을 알아보려면 [여기](#3) 를 클릭 하십시오.

.NET Framework 1.1으로 마이그레이션하는 경우의 한 가지 가져오기 고려 사항은 .NET Framework의 각 버전이 자체 Machine.config 파일을 사용 한다는 것입니다. 따라서 web.config 파일을 변경 하는 경우에는 해당 변경 내용을 .NET Framework 1.1 Machine.config 파일로 마이그레이션해야 합니다.

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a>설치 하는 동안 .NET Framework 1.0에 대 한 웹 응용 프로그램의 매핑 유지 관리

기본적으로 모든 기존 ASP.NET 응용 프로그램은 설치 중에 자동으로 다시 구성 되어 최신 버전의 .NET Framework을 사용 합니다. 최신 버전의 .NET Framework을 사용 하 여 응용 프로그램은 새로운 릴리스에 포함 된 향상 된 기능 및 새로운 기능을 모두 활용할 수 있습니다. 이와 동시에 업데이트 되는 응용 프로그램을 세밀 하 게 제어할 수 있는 웹 관리자는 .NET Framework 설치 하는 동안 모든 기존 ASP.NET 응용 프로그램을 자동으로 다시 매핑할 수 없도록 할 수 있습니다.

전체 ASP.NET 응용 프로그램이 최신 버전의 .NET Framework 자동으로 다시 매핑 되지 않도록 웹 관리자는 Dotnetfx.exe 설치 프로그램과 함께/noaspupgrade 명령줄 옵션을 사용할 수 있습니다.

**ASP.NET 응용 프로그램의 전체 다시 매핑을 최신 버전으로 방지 하려면**

1. **시작**으로 이동합니다.
2. **실행**을 클릭 합니다.
3. **cmd**를 입력합니다.
4. **확인**을 클릭합니다.  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. 명령 프롬프트에서 다음 줄을 입력 하 여 .NET Framework 설치를 시작 합니다. **dotnetfx.exe/c: "install/noaspupgrade?**  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. Microsoft .NET Framework 1.1 설치에서 **예** 를 클릭 합니다. 그러면 .NET Framework 1.1의 설치 프로세스가 시작 됩니다.  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a>웹 응용 프로그램을 특정 버전의 .NET Framework에 매핑

각 버전의 .NET Framework에는 ASP.NET IIS 등록 도구 (Aspnet\_regiis) 버전이 포함 되어 있습니다. 이 도구를 사용 하면 관리자가 특정 버전의 .NET Framework에서 웹 응용 프로그램을 실행 하도록 지정할 수 있습니다. 이를 .NET Framework 버전의 웹 응용 프로그램에 매핑 이라고 합니다. 관리자는 웹 응용 프로그램과 연결 될 .NET Framework 버전에 해당 하는 Aspnet\_regiis .exe를 선택 해야 합니다. 예를 들어 웹 사이트에서 .NET Framework 1.1를 사용 하도록 지정 하려는 관리자는 .NET Framework 1.1과 함께 제공 되는 Aspnet\_를 사용 해야 합니다.

버전 1.0에 대 한 Aspnet\_regiis .exe는 다음 위치에 있습니다.

- C:\windows\ microsoft.net \framework\\**v v1.0.3705**\aspnet\_regiis

버전 1, 1에 대 한 Aspnet\_은 다음 위치에 있습니다.

- C:\windows\ microsoft.net \framework\\**v 1.1.4322**\aspnet\_regiis

Aspnet\_regiis는 웹 응용 프로그램을 매핑하는 스크립트에 대 한 두 가지 옵션을 제공 합니다.

- **-** 는 경로 및 해당 하위 디렉터리에 스크립트 맵을 설정 합니다.
- **-sn** 경로에 스크립트 맵을 설정 합니다.

경로는 W3SVC/ROOT/{WebSiteNumber}/{Application\_Name} 형식으로 정의 되는 웹 응용 프로그램 IIS 메타 데이터 경로를 정의 합니다. 예를 들어 기본 웹 사이트 아래에 있는 Portal 이라는 웹 응용 프로그램의 경우 메타 베이스 경로는 W3SVC/1/ROOT/Portal입니다.

![](side-by-side-with-10/_static/image4.gif)

메타 베이스 편집기 라는 도구를 사용 하 여 메타 베이스 경로를 가져올 수도 있습니다. 이 도구는 [https://support.microsoft.com/default.aspx?scid=kb; en-us; 232068](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068) 의 Microsoft 지원 사이트에서 다운로드할 수 있습니다.

- Aspnet\_regiis .exe/1/ROOT/Portal을 실행 하 여 포털 IIS 스크립트 맵과 해당 하위 응용 프로그램을 업데이트 합니다.  
  
    ![](side-by-side-with-10/_static/image5.gif)

- 포털의 하위 디렉터리에 있는 응용 프로그램에 영향을 주지 않고 포털 IIS 스크립트 맵을 업데이트 하려면 Aspnet-sn W3SVC/1/ROOT/Portal\_를 실행 합니다.  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a>웹 응용 프로그램에서 사용 하는 .NET Framework 버전 찾기

관리자는 Internet Service Manager를 사용 하 여 웹 사이트를 실행 하는 .NET Framework 버전을 찾을 수 있습니다. 서로 다른 운영 체제 버전은 인터넷 Service Manager를 다르게 시작 합니다. Service manager를 시작 하려면 아래 나열 된 단계를 따르세요.

**인터넷 Service Manager를 시작 하려면**

1. **시작**으로 이동합니다.
2. **실행**을 클릭 합니다.
3. **Inetmgr**을 입력 합니다.  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. 인터넷 Service Manager에서 보려는 .NET Framework의 버전을 포함 하는 웹 응용 프로그램을 선택 합니다.  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. 웹 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 **합니다.**  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. 속성 창에서 구성을 선택 **합니다.**  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. 응용 프로그램 매핑 테이블에서 **.aspx**를 선택 하 고 **편집**을 클릭 합니다.  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. **실행 파일** 텍스트 상자에서 스크롤하여 버전 디렉터리를 확인 합니다. 버전 디렉터리가 1.1.4322 인 경우 응용 프로그램은 .NET Framework 1.1에 매핑됩니다. 반대로 버전 디렉터리가 v v1.0.3705 인 경우 응용 프로그램은 .NET Framework 1.0에 매핑됩니다.  
  
    ![](side-by-side-with-10/_static/image12.gif)
