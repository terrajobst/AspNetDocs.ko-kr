---
uid: whitepapers/overview
title: 백서 | Microsoft Docs
author: rick-anderson
description: 이 페이지에서는 ASP.NET를 설치 및 구성 하는 데 도움이 되는 백서와 안전 하 고 빠르고 유연한 ASP.NET 응용 프로그램을 작성 하는 데 도움이 되는 백서를 찾을 수 있습니다.
ms.author: riande
ms.date: 11/15/2011
ms.assetid: d5e79470-01f2-4d65-8077-11c3e10a6784
msc.legacyurl: /whitepapers
msc.type: content
ms.openlocfilehash: 1a3a9fe5d685d4b38efe666fc88ff57016482ada
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520589"
---
# <a name="whitepapers"></a>백서

> 이 페이지에서는 ASP.NET를 설치 및 구성 하는 데 도움이 되는 백서와 안전 하 고 빠르고 유연한 ASP.NET 응용 프로그램을 작성 하는 데 도움이 되는 백서를 찾을 수 있습니다.
> 
> - [ASP.NET 4](#aspnet4)
> - [ASP.NET 보안 백서](#security)
> - [설치 및 설정 백서](#setup)
> - [SQL Server 백서](#sql)
> - [일반 백서](#general)

<a id="aspnet4"></a>
## <a name="aspnet-4"></a>ASP.NET 4

ASP.NET 4 및 Visual Studio 2010와 관련 된 정보입니다.

[ASP.NET MVC 4 릴리스 정보](mvc4-beta-release-notes.md "mvc4-릴리스 정보")

이 문서에서는 Visual Studio 2010 용 ASP.NET MVC 4 Developer Preview에 도입 된 새로운 기능 및 개선 사항 뿐만 아니라 설치 참고 사항 및 알려진 문제에 대해 설명 합니다.

[ASP.NET MVC 3 릴리스 정보](mvc3-release-notes.md "mvc3-릴리스 정보")

이 문서에서는 ASP.NET MVC 3에 도입 된 새로운 기능 및 개선 사항 뿐만 아니라 설치 참고 사항 및 알려진 문제에 대해 설명 합니다.

[ASP.NET 4 및 Visual Studio 2010 웹 개발 개요](aspnet4/index.md "aspnet4")

ASP.NET에 대 한 많은 흥미로운 변경 사항은 .NET Framework 버전 4에서 제공 됩니다. 이 문서는 이후 릴리스에 포함 된 여러 가지 새로운 기능에 대 한 개요를 제공 합니다.

[ASP.NET 4 Beta 2 주요 변경 내용](aspnet4/breaking-changes.md "주요 변경 내용")

이 문서에서는 ASP.NET 4 Beta 1 릴리스를 비롯 하 여 이전 릴리스를 사용 하 여 만든 응용 프로그램에 잠재적으로 영향을 줄 수 있는 .NET Framework 버전 4 베타 2 릴리스 (즉, ASP.NET 4 Beta 2 릴리스)에 대해 수행 된 변경 내용을 설명 합니다.

[ASP.NET MVC 2의 새로운 기능](what-is-new-in-aspnet-mvc.md "aspnet mvc의 새로운 기능")

이 문서에서는 ASP.NET MVC 2에 도입 된 새로운 기능 및 향상 된 기능에 대해 설명 합니다.

[ASP.NET MVC 1.0 애플리케이션을 ASP.NET MVC 2로 업그레이드](aspnet-mvc2-upgrade-notes.md "mvc2-업그레이드-참고")

ASP.NET MVC 2는 동일한 서버에 ASP.NET MVC 1.0와 나란히 설치할 수 있습니다. 이를 통해 응용 프로그램 개발자는 ASP.NET MVC 1.0 응용 프로그램을 ASP.NET MVC 2로 업그레이드할 시기를 유연 하 게 선택할 수 있습니다. 이 문서에서는 설명를 사용 하 여 수동으로 업그레이드 하는 방법과 Visual에서 마법사를 사용 하 여

<a id="security"></a>
## <a name="aspnet-security-whitepapers"></a>ASP.NET 보안 백서

보안은 인터넷 응용 프로그램의 중요 한 측면으로, 이러한 백서에서는 secure ASP.NET 응용 프로그램을 디자인 하 고 구현 하는 방법을 설명 합니다.

[보안을 위해 ASP.NET 2.0 응용 프로그램 계측](https://msdn.microsoft.com/library/ms998325.aspx)

이 방법에서는 사용자 지정 상태 모니터링 이벤트를 사용 하 여 ASP.NET 응용 프로그램을 계측 하 여 보안 관련 이벤트 및 작업을 추적 하는 방법을 보여 줍니다. ASP.NET 버전 2.0는 다양 한 표준에 대 한 계측을 포함 하는 상태 모니터링을 제공 합니다.

[ASP.NET 2.0에 대 한 보안 배포 검토 수행](https://msdn.microsoft.com/library/ms998367.aspx)

이 방법에서는 ASP.NET 2.0 응용 프로그램에 대 한 보안 배포 검토를 수행 하 여 부적절 한 구성 설정으로 인해 발생 하는 잠재적인 보안 취약점을 식별 하는 방법을 보여 줍니다. 대부분의 검토 프로세스에는 다음 작업이 포함 됩니다.

[ASP.NET 2.0의 역할에 대해 ADAM 사용](https://msdn.microsoft.com/library/ms998331.aspx)

이 방법에서는 ADAM (Active Directory 응용 프로그램 모드)을 사용 하 여 ASP.NET 역할을 저장 하는 ASP.NET 웹 사이트를 개발할 수 있는 방법을 보여 줍니다. ADAM 및 AzMan (권한 부여 관리자) 정책 저장소를 구성 하는 방법을 보여 줍니다. 새 역할을 만드는 방법

[ASP.NET 2.0에서 AzMan (권한 부여 관리자) 사용](https://msdn.microsoft.com/library/ms998336.aspx)

이 방법에서는 AzMan (권한 부여 관리자)를 ASP.NET 역할 관리자 API와 함께 사용 하 여 역할을 관리 하 고, 사용자 역할 멤버 자격을 확인 하 고, AzMan 정책 저장소에 대해 특정 작업을 수행 하도록 역할에 권한을 부여 하는 방법을 보여 줍니다. 방법 ...

[ASP.NET 2.0의 멤버 자격 사용](https://msdn.microsoft.com/library/ms998347.aspx)

이 방법에서는 ASP.NET 버전 2.0 응용 프로그램의 멤버 자격 기능을 사용 하는 방법을 보여 줍니다. 두 개의 서로 다른 멤버 자격 공급자 인 ActiveDirectoryMembershipProvider 및 SqlMembershipProvider를 사용 하는 방법을 보여 줍니다. 멤버 자격 기능 ...

[ASP.NET 2.0에서 역할 관리자 사용](https://msdn.microsoft.com/library/ms998314.aspx)

이 방법에서는 ASP.NET 2.0 역할 관리자를 사용 하는 방법을 보여 줍니다. 역할 관리자는 응용 프로그램에서 역할을 관리 하 고 역할 기반 권한 부여를 수행 하는 작업을 용이 하 게 합니다. ...에서 사용할 다양 한 역할 공급자를 구성 하는 방법을 보여 줍니다.

[ASP.NET 2.0에서 Windows 인증 사용](https://msdn.microsoft.com/library/ms998358.aspx)

이 방법에서는 ASP.NET 웹 응용 프로그램에서 Windows 인증을 구성 하 고 사용 하는 방법을 보여 줍니다. Windows 인증은 사용자가 Windows 도메인의 일부일 때마다 선호 되는 방법입니다. 이 방법을 사용 하면 기존 id 저장소를 사용할 수 있습니다.

[관리 코드에 대 한 보안 코드 검토 (기준 작업)를 수행 합니다.](https://msdn.microsoft.com/library/ms998364.aspx)

이 방법에서는 보안 코드 검토를 수행 하는 방법을 보여 줍니다. 이 모듈에서는 작업과 관련 된 단계와 결과를 분석 하는 방법을 보여 줍니다. "보안 질문 목록: 관리 코드 (.NET Framework 2.0)"를 사용 하 여이 방법을 사용 합니다.

[ASP.NET 2.0에 대 한 보안 배포 검토 수행](https://msdn.microsoft.com/library/ms998367.aspx)

이 방법에서는 ASP.NET 2.0 응용 프로그램에 대 한 보안 배포 검토를 수행 하 여 부적절 한 구성 설정으로 인해 발생 하는 잠재적인 보안 취약점을 식별 하는 방법을 보여 줍니다. 대부분의 검토 프로세스에는 다음 작업이 포함 됩니다.

[Windows 2000에 대 한 Kerberos 위임 구현](https://msdn.microsoft.com/library/aa302400.aspx)

Kerberos 위임을 사용 하면 응용 프로그램의 여러 물리적 계층에서 인증 된 id를 전달 하 여 다운스트림 인증 및 권한 부여를 지원할 수 있습니다. 이 방법으로이 작업을 수행 하는 데 필요한 구성 단계를 보여 줍니다.

[ASP.NET 2.0에서 가장 및 위임 사용](https://msdn.microsoft.com/library/ms998351.aspx)

이 방법에서는 ASP.NET 2.0 응용 프로그램에서 가장을 사용 하는 방법과 시기를 보여 줍니다. 기본적으로 가장이 해제 되 고 ASP.NET 웹 응용 프로그램의 프로세스 id를 사용 하 여 리소스에 액세스할 수 있습니다. 그러나 다음을 사용할 수 있습니다.

[디자인 타임에 웹 응용 프로그램에 대 한 위협 모델 만들기](https://msdn.microsoft.com/library/ms978527.aspx)

이 방법에서는 웹 응용 프로그램에 대 한 위협 모델을 만드는 방법을 설명 합니다. 위협 모델링 작업을 통해 보안 디자인을 모델링할 수 있으므로, 투자 하기 전에 잠재적인 보안 디자인 결점 및 취약성을 노출할 수 있습니다.

### <a name="forms-authentication"></a>폼 인증

[ASP.NET 2.0에서 폼 인증 보호](https://msdn.microsoft.com/library/ms998310.aspx)

이 방법에서는 ASP.NET 2.0 응용 프로그램에서 폼 인증을 안전 하 게 구성 하 고 사용 하는 방법을 보여 줍니다. 고려해 야 할 주요 요소는 인증 티켓의 보안을 유지 하 고 사용자 id 저장소를 보호 하 고 해당 저장소에 액세스 하는 것입니다. ...

[ASP.NET 2.0의 Active Directory에서 폼 인증 사용](https://msdn.microsoft.com/library/ms998360.aspx)

이 방법에서는 ActiveDirectoryMembershipProvider를 사용 하 여 Microsoft® Active Directory® 디렉터리 서비스에서 폼 인증을 사용 하는 방법을 보여 줍니다. 공급자를 구성 하 고 사용자를 만들고 인증 하는 방법을 보여 주는 방법 ...

[ASP.NET 2.0에서 여러 도메인의 Active Directory에 폼 인증 사용](https://msdn.microsoft.com/library/ms998345.aspx)

이 방법에서는 ActiveDirectoryMembershipProvider를 사용 하 여 Microsoft® Active Directory® 디렉터리 서비스에서 폼 인증을 사용 하는 방법을 보여 줍니다. 공급자를 구성 하 고 사용자를 만들고 인증 하는 방법을 보여 주는 방법 ...

[ASP.NET 2.0의 SQL Server에서 폼 인증 사용](https://msdn.microsoft.com/library/ms998317.aspx)

이 방법에서는 SQL Server 멤버 자격 공급자에서 폼 인증을 사용할 수 있는 방법을 보여 줍니다. SQL Server 사용 하는 폼 인증은 응용 프로그램의 사용자가 Windows 도메인에 속하지 않는 경우에 가장 적합 하며 그 결과,...

[ASP.NET 1.1에서 폼 인증을 사용 하 여 GenericPrincipal 개체 만들기](https://msdn.microsoft.com/library/aa302399.aspx)

이 방법에서는 폼 인증을 사용할 때 GenericPrincipal 및 FormsIdentity 개체를 만들고 처리 하는 방법을 보여 줍니다.

[ASP.NET 1.1의 Active Directory에서 폼 인증 사용](https://msdn.microsoft.com/library/aa302397.aspx)

이 방법 문서에서는 Active Directory 자격 증명 저장소에 대해 폼 인증을 구현 하는 방법을 보여 줍니다.

[ASP.NET 1.1의 SQL Server에서 폼 인증 사용](https://msdn.microsoft.com/library/aa302398.aspx)

이 방법에서는 SQL Server 자격 증명 저장소에 대해 폼 인증을 구현 하는 방법을 보여 줍니다. 또한 데이터베이스에 암호 다이제스트를 저장 하는 방법을 보여 줍니다.

### <a name="user-input-data-validation"></a>사용자 입력 데이터 유효성 검사

[요청 유효성 검사 - 스크립트 공격 방지](request-validation.md "요청-유효성 검사")

이 문서에서는 기본적으로 응용 프로그램에서 서버에 전송 된 인코딩되지 않은 HTML 콘텐츠를 처리 하지 못하도록 하는 ASP.NET의 요청 유효성 검사 기능에 대해 설명 합니다. 응용 프로그램이 ... 인 경우이 요청 유효성 검사 기능을 사용 하지 않도록 설정할 수 있습니다.

[ASP.NET에서 사이트 간 스크립팅 방지](https://msdn.microsoft.com/library/ms998274.aspx)

이 방법에서는 적절 한 입력 유효성 검사 기법을 사용 하 고 출력을 인코딩하여 ASP.NET 응용 프로그램을 사이트 간 스크립팅 공격 으로부터 보호 하는 방법을 보여 줍니다. 또한에서 사용할 수 있는 다른 여러 보호 메커니즘도 설명 합니다.

[ASP.NET의 SQL 삽입 으로부터 보호](https://msdn.microsoft.com/library/ms998271.aspx)

이 방법에서는 SQL 삽입 공격 으로부터 ASP.NET 응용 프로그램을 보호 하는 데 도움이 되는 여러 가지 방법을 보여 줍니다. 응용 프로그램에서 입력을 사용 하 여 동적 SQL 문을 생성 하거나 저장 프로시저를 사용 하 여에 연결할 때 SQL 삽입이 발생할 수 있습니다.

[정규식을 사용 하 여 ASP.NET에서 입력 제한](https://msdn.microsoft.com/library/ms998267.aspx)

이 방법에서는 ASP.NET 응용 프로그램 내에서 정규식을 사용 하 여 신뢰할 수 없는 입력을 제한할 수 있는 방법을 보여 줍니다. 정규식은 이름, 주소, 전화 번호 및 기타 사용자 정보와 같은 텍스트 필드의 유효성을 검사 하는 좋은 방법입니다. 다음을 사용할 수 있습니다.

### <a name="code-access-security"></a>코드 액세스 보안

[ASP.NET 2.0에서 코드 액세스 보안 사용](https://msdn.microsoft.com/library/ms998326.aspx)

이 방법에서는 응용 프로그램에 적합 한 신뢰 수준을 선택 하는 방법 및 필요한 경우 사용자 지정 신뢰 수준을 정의 하는 사용자 지정 ASP.NET 코드 액세스 보안 정책 파일을 만드는 방법을 보여 줍니다. 다른 코드 액세스 보안 신뢰를 사용할 수 있습니다.

[사용자 지정 암호화 권한 만들기](https://msdn.microsoft.com/library/aa302362.aspx)

이 방법에서는 Win32® DPAPI (데이터 보호 API)에서 제공 하는 관리 되지 않는 암호화 기능에 대 한 프로그래밍 방식의 액세스를 제어 하는 사용자 지정 코드 액세스 보안 권한을 만드는 방법을 설명 합니다. 관리 되는 DPAPI 래퍼에서이 사용자 지정 권한을 사용 합니다.

[코드 액세스 보안 정책을 사용 하 여 어셈블리 제한](https://msdn.microsoft.com/library/aa302361.aspx)

관리자는 코드 액세스 보안 정책을 구성 하 여 .NET Framework 코드 (어셈블리)의 작업을 제한할 수 있습니다. 이 방법에서는 파일 i/o를 수행 하 고 제한할 어셈블리의 기능을 제한 하는 코드 액세스 보안 정책을 구성 합니다.

### <a name="communications-security"></a>통신 보안

[웹 서버에서 SSL 설정](https://msdn.microsoft.com/library/aa302411.aspx)

클라이언트 응용 프로그램에서 https 연결을 지원 하려면 웹 서버를 SSL로 구성 해야 합니다. 이 방법에서는 웹 서버에서 SSL을 구성 하는 방법을 보여 줍니다.

[클라이언트 인증서 설정](https://msdn.microsoft.com/library/aa302412.aspx)

IIS는 클라이언트 인증서 인증을 지원 합니다. 이 방법에서는 클라이언트 인증서를 요구 하도록 웹 응용 프로그램을 구성 하는 방법을 보여 줍니다. 또한 클라이언트 컴퓨터에 인증서를 설치 하 고 웹 응용 프로그램을 호출할 때 사용 하는 방법을 보여 줍니다.

[포트 및 인증을 필터링 하는 데 IPSec 사용](https://msdn.microsoft.com/library/aa302366.aspx)

IPSec (인터넷 프로토콜 보안)은 서비스가 아니라 IP 기반 네트워크 트래픽에 대 한 암호화, 무결성 및 인증 서비스를 제공 하는 프로토콜입니다. IPSec에서 서버 간 보호를 제공 하기 때문에 IPSec을 사용 하 여 내부 위협에 대 한 카운터를 만들 수 있습니다.

[IPSec을 사용 하 여 두 서버 간에 보안 통신 제공](https://msdn.microsoft.com/library/aa302413.aspx)

IPSec은 Windows 2000에서 제공 되는 기술로, 두 서버 간에 암호화 된 채널을 만들 수 있습니다. IPSec을 사용 하 여 IP 트래픽을 필터링 하 고 서버를 인증할 수 있습니다. 이 방법에서는 보안 (암호화 됨)을 제공 하도록 IPSec을 구성 하는 방법을 보여 줍니다.

[SSL을 사용 하 여 SQL Server와의 통신 보호](https://msdn.microsoft.com/library/aa302414.aspx)

응용 프로그램에서 SQL Server 데이터베이스 서버로 전달 되는 데이터를 보호 하는 것이 중요 한 경우가 종종 있습니다. SQL Server를 사용 하 여 SSL을 사용 하 여 암호화 된 채널을 만들 수 있습니다. 이 방법에서는 데이터베이스 서버에 인증서를 설치 하는 방법을 보여 줍니다.

[ASP.NET 1.1의 클라이언트 인증서를 사용 하 여 웹 서비스 호출](https://msdn.microsoft.com/library/aa302408.aspx)

ASP.NET 웹 응용 프로그램 또는 Windows Forms 응용 프로그램에서 인증을 위해 웹 서비스에 클라이언트 인증서를 전달 하는 방법을 설명 하는 방법입니다. 로컬 컴퓨터 저장소 또는 사용자 저장소에 클라이언트 인증서를 설치할 수 있습니다. 조건

[ASP.NET 1.1의 SSL을 사용 하 여 웹 서비스 호출](https://msdn.microsoft.com/library/aa302409.aspx)

SSL (SSL(Secure Sockets Layer)) 암호화를 사용 하 여 웹 서비스와 전달 되는 메시지의 무결성과 기밀성을 보장할 수 있습니다. 이 방법에서는 웹 서비스에서 SSL을 사용 하는 방법을 보여 줍니다.

### <a name="cryptography"></a>암호화

[.NET 1.1에서 DPAPI 라이브러리 만들기](https://msdn.microsoft.com/library/aa302402.aspx)

이 방법에서는 데이터베이스 연결 문자열 및 계정 자격 증명과 같은 데이터를 암호화 하려는 응용 프로그램에 DPAPI 기능을 노출 하는 관리 되는 클래스 라이브러리를 만드는 방법을 보여 줍니다.

[.NET 1.1에서 암호화 라이브러리 만들기](https://msdn.microsoft.com/library/aa302405.aspx)

이 방법에서는 응용 프로그램에 대 한 암호화 기능을 제공 하기 위해 관리 되는 클래스 라이브러리를 만드는 방법을 보여 줍니다. 응용 프로그램에서 암호화 알고리즘을 선택할 수 있습니다. 지원 되는 알고리즘에는 DES, Triple DES, RC2 및 Rijndael이 포함 됩니다.

[ASP.NET 1.1에서 레지스트리에 암호화 된 연결 문자열을 저장 합니다.](https://msdn.microsoft.com/library/aa302406.aspx)

응용 프로그램은 연결 문자열 및 계정 자격 증명과 같은 암호화 된 데이터를 Windows 레지스트리에 저장 하도록 선택할 수 있습니다. 이 방법에서는 레지스트리에서 암호화 된 문자열을 저장 하 고 검색 하는 방법을 보여 줍니다.

[ASP.NET 1.1에서 DPAPI (컴퓨터 저장소) 사용](https://msdn.microsoft.com/library/aa302403.aspx)

이 방법에서는 ASP.NET 웹 응용 프로그램 또는 웹 서비스에서 DPAPI를 사용 하 여 중요 한 데이터를 암호화 하는 방법을 보여 줍니다.

[Enterprise Services에서 ASP.NET 1.1의 DPAPI (사용자 저장소) 사용](https://msdn.microsoft.com/library/aa302404.aspx)

이 방법에서는 ASP.NET 웹 응용 프로그램 또는 서비스에서 DPAPI를 사용 하 여 중요 한 데이터를 암호화 하는 방법을 보여 줍니다. 이러한 방법으로는 out of process Enterprise Services 구성 요소를 사용 해야 하는 사용자 저장소와 DPAPI를 사용 합니다.

<a id="setup"></a>
## <a name="installation-and-setup-whitepapers"></a>설치 및 설정 백서

이러한 백서에서는 서버에 ASP.NET를 설치 및 구성 하는 방법에 대 한 단계별 지침을 제공 합니다.

[ASP.NET 2.0 응용 프로그램에 대 한 서비스 계정 만들기](https://msdn.microsoft.com/library/ms998297.aspx)

이 방법에서는 ASP.NET 웹 응용 프로그램을 실행 하는 데 필요한 사용자 지정 최소 권한 서비스 계정을 만들고 구성 하는 방법을 보여 줍니다. 기본적으로 Microsoft Windows Server 2003 및 IIS 6.0의 ASP.NET 응용 프로그램은 기본 제공 네트워크 서비스를 사용 하 여 실행 됩니다.

[ASP.NET 2.0에서 여러 응용 프로그램을 호스팅할 때 보안 향상](https://msdn.microsoft.com/library/aa480478.aspx)

이 방법에서는 여러 응용 프로그램을 서로 격리 하 고 웹 호스팅 환경의 공유 시스템 리소스에서 격리 하는 방법을 보여 줍니다. 호스팅 환경은 여러 가지를 호스트 하는 ISP (인터넷 서비스 공급자)에서 제공 하는 웹 서버 일 수 있습니다.

[ASP.NET 2.0에서 보통 신뢰 사용](https://msdn.microsoft.com/library/ms998341.aspx)

이 방법에서는 보통 신뢰 수준에서 실행 되도록 ASP.NET 웹 응용 프로그램을 구성 하는 방법을 보여 줍니다. 동일한 서버에서 여러 응용 프로그램을 호스트 하는 경우 코드 액세스 보안 및 보통 신뢰 수준을 사용 하 여 응용 프로그램 격리를 제공할 수 있습니다. 설정 ...

[ASP.NET 2.0에서 네트워크 서비스 계정을 사용 하 여 리소스에 액세스 합니다.](https://msdn.microsoft.com/library/ms998320.aspx)

이 방법에서는 NT AUTHORITY\Network Service 컴퓨터 계정을 사용 하 여 로컬 및 네트워크 리소스에 액세스 하는 방법을 보여 줍니다. 기본적으로 Windows Server 2003에서 ASP.NET 응용 프로그램은이 계정의 id를 사용 하 여 실행 됩니다. 최소 권한 ...

[ASP.NET 2.0에서 프로토콜 전환 및 제한 된 위임 사용](https://msdn.microsoft.com/library/ms998355.aspx)

이 방법에서는 프로토콜 전환 및 제한 된 위임을 구성 하 고 사용 하 여 ASP.NET 응용 프로그램이 원래 호출자를 가장 하는 동안 네트워크 리소스에 액세스할 수 있도록 하는 방법을 보여 줍니다. Microsoft® Windows® 2000 운영 체제 ...

[.NET Framework 1.0 및 1.1의 ASP.NET Side-by-Side 실행](side-by-side-with-10.md "1\.0와 나란히")

이 백서에서는 컴퓨터에 .NET 1.0 및 .NET 1.1를 모두 설치 하 여 ASP.NET 웹 응용 프로그램이 두 가지 버전의 프레임 워크에서 실행 될 수 있도록 하는 방법을 설명 합니다.

[ASP.NET에서 IIS 디렉터리에 대한 액세스 거부](denied-access-to-iis-directories.md "iis 디렉터리에 대 한 액세스 거부")

이 백서에서는 ASP.NET 응용 프로그램에 대 한 요청이 " *DirectoryName* 디렉터리에 대 한 액세스 거부" 오류를 반환 하는 경우 수행 해야 하는 작업에 대해 설명 합니다. 디렉터리 변경 내용 모니터링을 시작 하지 못했습니다. "

[IIS 6.0에서 ASP.NET 1.1 실행](aspnet-and-iis6.md "aspnet 및 iis6")

Windows Server 2003에는 IIS 6.0과 ASP.NET 1.1가 모두 포함 되어 있지만 이러한 구성 요소는 기본적으로 사용 하지 않도록 설정 되어 있습니다. 이 백서에서는 IIS 6.0 및 ASP.NET 1.1를 사용 하도록 설정 하는 방법에 대해 설명 하 고, 최적을 얻기 위해 몇 가지 구성 설정을 권장 합니다.

[IE 용 보안 업데이트를 적용 한 후 ' 서버 응용 프로그램을 사용할 수 없음 ' 오류 수정](ms03-32-issue.md "ms03-32-문제")

이 문서에서는 Windows XP Professional에서 실행 되는 ASP.NET 1.0 응용 프로그램에 영향을 주는 Internet Explorer 용 MS03-32 보안 업데이트와 관련 된 문제를 해결 하는 패치를 설명 합니다.

[ASP.NET 1.1를 실행 하는 사용자 지정 계정 만들기](https://msdn.microsoft.com/library/aa302396.aspx)

ASP.NET 웹 응용 프로그램은 일반적으로 기본 제공 ASPNET 계정을 사용 하 여 실행 됩니다. 경우에 따라 사용자 지정 계정을 사용 하는 것이 좋습니다. 이 방법 문서에서는 ASP.NET 웹 응용 프로그램을 실행 하기 위해 최소 권한의 로컬 계정을 만드는 방법을 보여 줍니다. ...

### <a name="configuration"></a>구성

[ASP.NET 2.0에서 컴퓨터 키 구성](https://msdn.microsoft.com/library/ms998288.aspx)

이 방법에서는 Web.config 파일의 &lt;machineKey&gt; 요소에 대해 설명 하 고 ViewState, 폼 인증 티켓 및 역할 쿠키의 변조 방지 및 암호화를 제어 하도록 &lt;machineKey&gt; 요소를 구성 하는 방법을 보여 줍니다. ViewState가 서명 되었습니다 ...

[DPAPI를 사용 하 여 ASP.NET 2.0의 구성 섹션 암호화](https://msdn.microsoft.com/library/ms998280.aspx)

이 방법에서는 Windows DPAPI (데이터 보호 응용 프로그래밍 인터페이스)로 보호 되는 구성 공급자 및 Aspnet\_regiis .exe 도구를 사용 하 여 구성 파일의 섹션을 암호화 하는 방법을 보여 줍니다. Aspnet\_regiis .exe 도구를 사용 하 여 ...

[RSA를 사용 하 여 ASP.NET 2.0의 구성 섹션 암호화](https://msdn.microsoft.com/library/ms998283.aspx)

이 방법에서는 RSA로 보호 되는 구성 공급자와 Aspnet\_regiis .exe 도구를 사용 하 여 구성 파일의 섹션을 암호화 하는 방법을 보여 줍니다. Aspnet\_regiis .exe 도구를 사용 하 여 연결 문자열과 같은 중요 한 데이터를 암호화할 수 있습니다.

[ASP.NET 2.0에서 가장 및 위임 사용](https://msdn.microsoft.com/library/ms998351.aspx)

이 방법에서는 ASP.NET 2.0 응용 프로그램에서 가장을 사용 하는 방법과 시기를 보여 줍니다. 기본적으로 가장이 해제 되 고 ASP.NET 웹 응용 프로그램의 프로세스 id를 사용 하 여 리소스에 액세스할 수 있습니다. 그러나 다음을 사용할 수 있습니다.

<a id="sql"></a>
## <a name="sql-server-whitepapers"></a>SQL Server 백서

ASP.NET는 다양 한 데이터베이스에서 작동 하는 반면, 이러한 백서는 특히 SQL Server에 ASP.NET 응용 프로그램을 연결 하는 방법을 살펴봅니다.

[ASP.NET 2.0에서 SQL 인증을 사용 하 여 SQL Server에 연결](https://msdn.microsoft.com/library/ms998300.aspx)

이 방법에서는 데이터베이스 액세스 인증에서 네이티브 SQL 인증을 사용 하는 경우 ASP.NET 응용 프로그램을 Microsoft® SQL Server™에 안전 하 게 연결 하는 방법을 보여 줍니다. Windows 인증은 SQL Server에 연결 하는 데 권장 되는 방법입니다.

[ASP.NET 2.0에서 Windows 인증을 사용 하 여 SQL Server에 연결](https://msdn.microsoft.com/library/ms998292.aspx)

이 방법에서는 ASP.NET 버전 2.0 응용 프로그램의 Windows 서비스 계정을 사용 하 여 SQL Server 2000에 연결 하는 방법을 보여 줍니다. 자격 증명을 저장 하지 않기 때문에 가능 하면 SQL 인증 대신 Windows 인증을 사용 해야 합니다.

[SSL을 사용 하 여 SQL Server 2000과의 통신 보안 유지](https://msdn.microsoft.com/library/aa302414.aspx)

응용 프로그램에서 SQL Server 데이터베이스 서버로 전달 되는 데이터를 보호 하는 것이 중요 한 경우가 종종 있습니다. SQL Server를 사용 하 여 SSL을 사용 하 여 암호화 된 채널을 만들 수 있습니다. 이 방법에서는 데이터베이스 서버에 인증서를 설치 하는 방법을 보여 줍니다,...

<a id="general"></a>
## <a name="general-whitepapers"></a>일반 백서

다음 사례 연구에서는 기존 호스팅 환경에서 Microsoft Azure로 Microsoft의 .NET 커뮤니티 웹 사이트를 마이그레이션하는 데 사용 된 프로세스를 설명 합니다.

[Microsoft의 ASP.NET 및 IIS.NET 커뮤니티 웹 사이트를 Microsoft Azure으로 마이그레이션](https://go.microsoft.com/fwlink/?LinkId=400656)

이러한 백서에서는 ASP.NET 관련 된 다양 한 항목을 다룹니다.

[ASP.NET 2.0에서 상태 모니터링 사용](https://msdn.microsoft.com/library/ms998306.aspx)

이 방법에서는 상태 모니터링을 사용 하 여 사용자 지정 이벤트에 대 한 응용 프로그램을 계측 하는 방법을 보여 줍니다. 사용자 지정 상태 모니터링 이벤트를 만들려면 healthMonitoring에서 파생 되는 클래스를 만들고,&gt;를 &lt;구성 합니다.

[패치 관리 구현](https://msdn.microsoft.com/library/aa302364.aspx)

이 방법에서는 단일 또는 여러 서버를 최신 상태로 유지 하는 방법을 비롯 하 여 패치 관리에 대해 설명 합니다. Microsoft에서 다운로드할 수 있는 도구를 제외 하 고 추가 소프트웨어는 필요 하지 않습니다. 운영 및 보안 정책은 패치 관리를 채택 해야 합니다.

[Silverlight 3 SDK의 Silverlight 용 ASP.NET 서버 컨트롤](https://go.microsoft.com/fwlink/?LinkId=153377)

Silverlight 용 ASP.NET 서버 컨트롤 ("ASP.NET Silverlight 컨트롤") (ASP.NET MediaPlayer 및 Silverlight 컨트롤)은 silverlight SDK for Silverlight 버전 3에서 제거 되었습니다. 이 문서에서는 이러한 ASP.NET 작업을 수행 하는 개발자를 위한 지침을 제공 합니다.

[고성능 웹 응용 프로그램 빌드](https://devexpress.com/act)

ASP.NET Ajax 라이브러리의 새로운 기능을 사용 하 여 고성능 웹 응용 프로그램을 빌드하는 방법에 대해 알아봅니다.
