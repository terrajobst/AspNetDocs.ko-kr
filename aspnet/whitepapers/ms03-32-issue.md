---
uid: whitepapers/ms03-32-issue
title: IE 용 보안 업데이트를 적용 한 후 ' 서버 응용 프로그램을 사용할 수 없음 ' 오류 수정 Microsoft Docs
author: rick-anderson
description: 이 문서에서는 ASP.NET 1.0 응용 프로그램에 영향을 주는 Internet Explorer 용 MS03-32 보안 업데이트와 관련 된 문제를 해결 하는 패치를 설명 합니다.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 1365eebb-bdf7-4a05-8d18-7f200531be55
msc.legacyurl: /whitepapers/ms03-32-issue
msc.type: content
ms.openlocfilehash: e0b6776cbfe22e341ac7105f03daac5074b480fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463457"
---
# <a name="fix-for-server-application-unavailable-error-after-applying-security-update-for-ie"></a>IE 보안 업데이트 적용 후 ‘서버 애플리케이션을 사용할 수 없음’ 오류에 대한 수정

> 이 문서에서는 Windows XP Professional에서 실행 되는 ASP.NET 1.0 응용 프로그램에 영향을 주는 Internet Explorer 용 MS03-32 보안 업데이트와 관련 된 문제를 해결 하는 패치를 설명 합니다.
> 
> ASP.NET 1.0 및 Windows XP Professional에 적용 됩니다.

Microsoft는 Windows XP에서 실행 되는 Internet Explorer 보안 패치 및 ASP.NET 1.0에 대 한 MS03-32 보안 업데이트와 관련 된 문제를 확인 했습니다. 이 패치는 수동으로 설치 하거나 Windows 업데이트 사이트에서 최신 중요 업데이트를 가져올 수 있습니다.

이 문제의 증상은 Windows XP 컴퓨터에 패치를 설치한 후 로컬 IIS 5.1 웹 서버에서 실행 되는 응용 프로그램에 대 한 모든 요청에 "서버 응용 프로그램을 사용할 수 없습니다." 라는 오류 메시지가 ASP.NET는 것입니다. 원격 웹 서버에 대 한 요청은 영향을 받지 않습니다.

이 문제는 Windows XP에서 ASP.NET 1.0를 실행 하는 설치에만 영향을 줍니다. Windows 2000 또는 Windows Server 2003를 실행 하는 컴퓨터에는 영향을 주지 않습니다. ASP.NET 1.1가 설치 된 Windows XP를 실행 하는 컴퓨터에도 영향을 주지 않습니다.

이 문제는 ASP.NET에 대 한 보안 버그가 **아닙니다** . ASP.NET 응용 프로그램 또는 서버에 대 한 악의적인 공격을 열거나 허용 **하지** 않습니다. 대신, 패치 자체에 의해 발생 하는 기능적 버그로 전적으로 발생 합니다.

이 문제에 대 한 영구적인 솔루션을 위해 노력 하 고 있습니다. 그 동안에는 문제에 대 한 해결 방법으로 다음 배치 파일을 실행할 수 있습니다. 배치 파일은 다음 작업을 수행 합니다.

1. IIS 및 ASP.NET state 서비스를 중지 합니다.
2. 알려진 임시 암호를 사용 하 여 ASPNET 계정을 삭제 하 고 다시 만듭니다.
3. Windows `runas` 명령을 사용 하 여 ASPNET 사용자 프로필을 만드는 실행 파일을 시작 합니다.
4. ASP.NET를 다시 등록 합니다. 계정에 대 한 새 임의의 암호를 만들고 기본 ASP.NET 액세스 제어 설정을 적용 합니다.
5. IIS 서비스를 다시 시작 합니다.

배치 파일에는 하드 코드 된 임시 암호 "<strong>1pass\@단어</strong>"가 포함 되어 있습니다 .이 암호는 배치 파일이 실행 될 때 runas 명령을 입력 하 라는 메시지가 표시 됩니다. Runas 명령이 완료 된 후에는 강력한 난수 값을 사용 하 여 ASPNET 계정 암호를 다시 만듭니다. 하드 코딩 된 암호가 사용자 환경의 암호 복잡성 요구 사항을 충족 하지 않으면 배치 파일이 실패할 수 있습니다. 해당 하는 경우 사용자 환경에 적합 한 다른 값으로 변경할 수 있습니다.

*> [!IMPORTANT]* ASPNET 계정에 대 한 사용자 지정 액세스 제어 설정 또는 데이터베이스 계정 권한을 추가한 경우에는이 배치 파일이 완료 된 후 다시 만들어야 합니다. 계정을 다시 만들 때 새 SID (보안 식별자)가 발생 하기 때문입니다.

*> [!IMPORTANT]* ASPNET 계정이 아닌 사용자 지정 계정을 사용 하 여 ASP.NET worker 프로세스를 실행 하는 경우이 배치 파일을 실행 하면 안 됩니다. 대신 대화형으로 로그인 하거나 해당 계정에 대 한 사용자 프로필을 만들 계정으로 runas 명령을 사용 해야 합니다.

배치 파일은 아래의 자동 압축 풀기 보관 파일에 포함 되어 있습니다. 이를 사용하려면:

1. 관리자 권한이 있는 계정으로 실행 해야 합니다.
2. [자동 압축 풀기 실행 파일을 다운로드 하 여 엽니다.](ms03-32-issue/_static/fixup1.exe)
3. C:\에 콘텐츠 추출
4. 실행 ...을 선택 합니다. 시작 메뉴에서을 입력 하 고 `cmd.exe`
5. 열기 명령 창에서 `c:\fixup.cmd`을 입력 합니다.
6. 메시지가 표시 되 면 암호로 <strong>1pass\@단어</strong> 를 입력 합니다.
7. 이전에 ASPNET 계정에 대 한 사용자 지정 액세스 제어 설정 또는 데이터베이스 계정 권한이 있는 경우 지금 이러한 설정을 다시 적용 해야 합니다.

이로 인해 불편을 정말 많습니다. 사용할 수 있게 될 때 추가 정보를 게시 합니다.

아래 행렬은이 문제의 영향을 받는 플랫폼 및 버전을 자세히 설명 합니다.

| .NET Framework | 플랫폼 | 관련 |
| --- | --- | --- |
| 버전 1.0 | Windows 2000 Professional | 예 |
| 버전 1.0 | Windows 2000 Server | 예 |
| 버전 1.0 | Windows XP Professional | yes |
| 버전 1.0 | Windows Server 2003 | 예 |
| 버전 1.0 | Windows XP Home with Cassini | 예 |
| 버전 1.1 | Windows 2000 Professional | 예 |
| 버전 1.1 | Windows 2000 Server | 예 |
| 버전 1.1 | Windows XP Professional | 예 |
| 버전 1.1 | Windows Server 2003 | 예 |
| 버전 1.1 | Windows XP Home with Cassini | 예 |

감사합니다.   
 ASP.NET 팀
