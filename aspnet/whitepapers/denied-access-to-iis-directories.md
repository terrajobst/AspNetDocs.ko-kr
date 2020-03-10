---
uid: whitepapers/denied-access-to-iis-directories
title: IIS 디렉터리에 대 한 액세스 거부 ASP.NET | Microsoft Docs
author: rick-anderson
description: 이 백서에서는 ASP.NET 응용 프로그램에 대 한 요청이 "DirectoryName 디렉터리에 대 한 액세스 거부" 오류를 반환 하는 경우 수행 해야 하는 작업에 대해 설명 합니다. 실패 ...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: a3a53aa88abbe1bcaaea7d691406800c8f9b988b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518573"
---
# <a name="aspnet-denied-access-to-iis-directories"></a>ASP.NET에서 IIS 디렉터리에 대한 액세스 거부

> 이 백서에서는 ASP.NET 응용 프로그램에 대 한 요청이 " *DirectoryName* 디렉터리에 대 한 액세스 거부" 오류를 반환 하는 경우 수행 해야 하는 작업에 대해 설명 합니다. 디렉터리 변경 내용 모니터링을 시작 하지 못했습니다. "
> 
> ASP.NET 1.0 및 ASP.NET 1.1에 적용 됩니다.

이제 ASP.NET V1 RTM은 로컬 컴퓨터에서 "ASPNET" 계정으로 등록 된 낮은 권한의 windows 계정을 사용 하 여 실행 됩니다.

일부 잠겨 있는 시스템에서이 계정에는 웹 사이트의 콘텐츠 디렉터리, 응용 프로그램 루트 디렉터리 또는 웹 사이트 루트 디렉터리에 대 한 읽기 보안 액세스 권한이 기본적으로 포함 되지 않을 수 있습니다. 이 경우 지정 된 웹 응용 프로그램에서 페이지를 요청할 때 다음 오류가 표시 됩니다.

![](denied-access-to-iis-directories/_static/image1.jpg)

이 문제를 해결 하려면 해당 디렉터리에 대 한 보안 권한을 변경 해야 합니다.

특히 ASP.NET에는 웹 사이트 루트에 대 한 ASPNET 계정 (예: c:\inetpub\wwwroot 또는 IIS에서 구성한 다른 사이트 디렉터리)에 대 한 읽기, 실행 및 목록 액세스 권한이 필요 합니다. 콘텐츠 디렉터리 및 응용 프로그램 루트 디렉터리 구성 파일 변경을 모니터링 하기 위해 응용 프로그램 루트는 IIS 관리 도구 (inetmgr)의 응용 프로그램 가상 디렉터리와 연결 된 폴더 경로에 해당 합니다.

예를 들어 wwwroot 폴더에 있는 다음 응용 프로그램 계층 구조를 살펴보세요.

`C:\inetpub\wwwroot\myapp\default.aspx`

이 예의 경우 ASPNET 계정에는 myapp 및 wwwroot 디렉터리의 콘텐츠에 대해 위에서 정의한 읽기 권한이 있어야 합니다. 루트 폴더에 대해 상속 된 단일 ACL이 중첩 된 경우 두 디렉터리 모두에 대해 선택적으로 사용 될 수도 있습니다.

디렉터리에 사용 권한을 추가 하려면 다음 단계를 수행 합니다.

- Windows 탐색기를 사용 하 여 디렉터리로 이동 합니다.
- 디렉터리 폴더를 마우스 오른쪽 단추로 클릭 하 고 "속성"을 선택 합니다.
- 속성 대화 상자에서 "보안" 탭으로 이동 합니다.
- "추가" 단추를 클릭 하 고 컴퓨터 이름, ASPNET 계정 이름을 차례로 입력 합니다. 예를 들어 "webdev" 라는 컴퓨터에서 webdev\ASPNET를 입력 하 고 "OK"를 누릅니다.
- ASPNET 계정에 "읽기 &amp; 실행", "폴더 내용 나열" 및 "읽기" 확인란이 선택 되어 있는지 확인 합니다.
- 확인을 눌러 대화 상자를 닫고 변경 내용을 저장 합니다.

![](denied-access-to-iis-directories/_static/image2.jpg)

원하는 경우 이러한 변경 내용은 Windows와 함께 제공 되는 "cacls.exe" 도구나 스크립트를 사용 하 여 자동화할 수 있습니다. ASPNET 계정에 대 한 자세한 내용은 [FAQ 문서](https://go.microsoft.com/fwlink/?LinkId=5828)를 참조 하세요.

지정 된 웹 응용 프로그램에서 특정 폴더 또는 파일에 대 한 쓰기 또는 수정 권한을 사용 하는 경우 동일한 절차를 수행 하 고 "쓰기" 및/또는 "수정" 확인란을 선택 하 여이 권한을 부여할 수 있습니다.

모든 사용자 또는 사용자 그룹에 게 이러한 디렉터리 (기본 구성)에 대 한 읽기 액세스를 허용 하는 컴퓨터에서는 문제가 발생 하지 않으며 위의 단계가 필요 하지 않습니다.
