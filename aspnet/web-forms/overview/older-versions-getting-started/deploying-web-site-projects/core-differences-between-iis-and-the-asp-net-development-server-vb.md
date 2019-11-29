---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-vb
title: IIS와 ASP.NET 개발 서버의 핵심 차이점 (VB) | Microsoft Docs
author: rick-anderson
description: ASP.NET 응용 프로그램을 로컬로 테스트할 때 ASP.NET Development 웹 서버를 사용 하 고 있을 수 있습니다. 그러나 프로덕션 웹 사이트는 pow.
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 090e9205-52f3-4d72-ae31-44775b8b8421
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-vb
msc.type: authoredcontent
ms.openlocfilehash: 880bb403e671446a77d7eebccf578a1dc714d1f9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586489"
---
# <a name="core-differences-between-iis-and-the-aspnet-development-server-vb"></a>IIS와 ASP.NET 개발 서버의 결정적 차이(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_06_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial06_WebServerDiff_vb.pdf)

> ASP.NET 응용 프로그램을 로컬로 테스트할 때 ASP.NET Development 웹 서버를 사용 하 고 있을 수 있습니다. 그러나 프로덕션 웹 사이트는 주로 제공 되는 IIS입니다. 이러한 웹 서버에서 요청을 처리 하는 방법 간에는 몇 가지 차이점이 있으며 이러한 차이로 인해 중요 한 결과가 발생할 수 있습니다. 이 자습서에서는 몇 가지 germane 차이점을 살펴봅니다.

## <a name="introduction"></a>소개

사용자가 ASP.NET 응용 프로그램을 방문할 때마다 브라우저가 웹 사이트로 요청을 보냅니다. 요청 된 리소스에 대 한 콘텐츠를 생성 하 고 반환 하기 위해 ASP.NET 런타임과 조정 되는 웹 서버 소프트웨어에서 해당 요청을 선택 합니다. [**I** 인터넷 **I** nformation **S** ervices (IIS)](http://en.wikipedia.org/wiki/Internet_Information_Services) 는 Windows server에 대 한 일반적인 인터넷 기반 기능을 제공 하는 서비스 모음입니다. IIS는 프로덕션 환경에서 응용 프로그램을 ASP.NET 하는 데 가장 일반적으로 사용 되는 웹 서버입니다. 웹 호스트 공급자가 ASP.NET 응용 프로그램을 제공 하는 데 사용 하는 웹 서버 소프트웨어를 사용 하는 것이 가장 큽니다. Iis는 IIS를 설치 하 고 적절 하 게 구성 해야 하지만 개발 환경에서 웹 서버 소프트웨어로 사용 될 수도 있습니다.

ASP.NET 개발 서버은 개발 환경에 대 한 대체 웹 서버 옵션입니다. 이는와 함께 제공 되며 Visual Studio에 통합 되어 있습니다. 웹 응용 프로그램이 IIS를 사용 하도록 구성 되어 있지 않으면 Visual Studio 내에서 웹 페이지를 처음 방문할 때 ASP.NET 개발 서버 자동으로 시작 되어 웹 서버로 사용 됩니다. 배포 해야 하는 [*파일 결정*](determining-what-files-need-to-be-deployed-vb.md) 자습서에서 만든 데모 웹 응용 프로그램은 모두 IIS를 사용 하도록 구성 되지 않은 파일 시스템 기반 웹 응용 프로그램 이었습니다. 따라서 Visual Studio 내에서 이러한 웹 사이트 중 하나를 방문 하는 경우 ASP.NET 개발 서버 사용 됩니다.

완벽 한 환경에서 개발 및 프로덕션 환경은 동일 합니다. 그러나 이전 자습서에서 설명한 대로 환경에서 서로 다른 구성 설정을 설정 하는 것은 드문 일이 아닙니다. 환경에서 다른 웹 서버 소프트웨어를 사용 하면 응용 프로그램을 배포할 때 고려해 야 하는 다른 변수가 추가 됩니다. 이 자습서에서는 IIS와 ASP.NET 개발 서버의 주요 차이점에 대해 설명 합니다. 이러한 차이로 인해 개발 환경에서 완벽를 실행 하는 코드가 예외를 throw 하거나 프로덕션 환경에서 실행 될 때 다르게 동작 하는 시나리오가 있습니다.

## <a name="security-context-differences"></a>보안 컨텍스트 차이점

웹 서버 소프트웨어는 들어오는 요청을 처리할 때마다 해당 요청을 특정 보안 컨텍스트와 연결 합니다. 이 보안 컨텍스트 정보는 운영 체제에서 요청에 허용 되는 작업을 확인 하는 데 사용 됩니다. 예를 들어, ASP.NET 페이지에는 디스크의 파일에 일부 메시지를 기록 하는 코드가 포함 될 수 있습니다. 이 ASP.NET 페이지를 오류 없이 실행 하려면 보안 컨텍스트에 해당 파일에 대 한 쓰기 권한이 있는 적절 한 파일 시스템 수준 권한이 있어야 합니다.

ASP.NET 개발 서버는 들어오는 요청을 현재 로그온 한 사용자의 보안 컨텍스트와 연결 합니다. 관리자 권한으로 데스크톱에 로그온 한 경우 ASP.NET 개발 서버에서 제공 하는 ASP.NET 페이지에는 관리자와 동일한 액세스 권한이 부여 됩니다. 그러나 IIS에서 처리 하는 ASP.NET 요청은 특정 컴퓨터 계정과 연결 됩니다. 기본적으로 웹 호스트 공급자는 각 고객에 대해 고유한 계정을 구성 했더라도 IIS 버전 6 및 7에서 네트워크 서비스 컴퓨터 계정을 사용 합니다. 그 외의 웹 호스트 공급자는이 컴퓨터 계정에 대해 제한 된 권한을 부여 했을 수 있습니다. 결과적으로 개발 환경에서 오류 없이 실행 되는 웹 페이지가 있지만 프로덕션 환경에서 호스팅될 때 권한 부여 관련 예외가 생성 될 수 있습니다.

이러한 유형의 오류를 작업에 표시 하려면 책 리뷰 웹 사이트에서 사용자에 게 *ASP.NET 3.5에* 대 한 교육을 받은 가장 최근 날짜와 시간을 저장 하는 파일을 만드는 페이지를 만들어 보세요. 이를 수행 하려면 `~/Tech/TYASP35.aspx` 페이지를 열고 `Page_Load` 이벤트 처리기에 다음 코드를 추가 합니다.

[!code-vb[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample1.vb)]

> [!NOTE]
> [`File.WriteAllText` 메서드](https://msdn.microsoft.com/library/system.io.file.writealltext.aspx) 는 새 파일 (없는 경우)을 만든 다음 지정 된 내용을 해당 파일에 씁니다. 파일이 이미 있는 경우 기존 콘텐츠를 덮어씁니다.

다음으로 ASP.NET 개발 서버를 사용 하 여 개발 환경에서 *ASP.NET 3.5에* 대 한 학습 설명 페이지를 방문 하세요. 웹 응용 프로그램의 루트 디렉터리에 있는 텍스트 파일을 만들고 수정할 수 있는 적절 한 권한이 있는 계정으로 컴퓨터에 로그온 한 경우에는 책 검토가 이전과 동일 하지만 페이지를 방문할 때마다 날짜 및 시간과 사용자의 IP 주소가 `LastTYASP35Access.txt` 파일에 저장 되는 것으로 간주 됩니다. 브라우저에서이 파일을 가리킵니다. 그림 1에 표시 된 것과 비슷한 메시지가 표시 됩니다.

[텍스트 파일에 책 검토를 방문한 마지막 날짜와 시간이 포함 되어 ![&lt;](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image2.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image1.png)

**그림 1**: 책 리뷰를 마지막으로 방문한 날짜와 시간을 포함 하는 텍스트 파일 ([전체 크기 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image3.png))

프로덕션에 웹 응용 프로그램을 배포 하 고 24 시간 책 검토 페이지 *에서 호스팅된 학습 ASP.NET 3.5* 을 방문 하세요. 이 시점에서 그림 2에 표시 된 오류 메시지 또는 일반 책 검토 페이지가 표시 되어야 합니다. 일부 웹 호스트 공급자는 익명 ASP.NET 컴퓨터 계정에 대 한 쓰기 권한을 부여 합니다 .이 경우 페이지는 오류 없이 작동 합니다. 그러나 웹 호스트 공급자가 익명 계정에 대 한 쓰기 액세스를 금지 하면 `TYASP35.aspx` 페이지에서 현재 날짜와 시간을 `LastTYASP35Access.txt` 파일에 쓰려고 할 때 [`UnauthorizedAccessException` 예외가](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) 발생 합니다.

[![IIS에서 사용 하는 기본 컴퓨터 계정에 파일 시스템에 쓸 수 있는 권한이 없습니다.](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image5.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image4.png)

**그림 2**: IIS에서 사용 하는 기본 컴퓨터 계정에 파일 시스템에 대 한 쓰기 권한이 없는 경우 ([전체 크기 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image6.png))

좋은 소식은 대부분의 웹 호스트 공급자에 게 웹 사이트에서 파일 시스템 사용 권한을 지정할 수 있는 사용 권한 도구를 사용 하는 것입니다. 익명 ASP.NET 계정에 루트 디렉터리에 대 한 쓰기 액세스 권한을 부여한 다음, 책 검토 페이지를 다시 방문 합니다. 필요한 경우에는 웹 호스트 공급자에 게 기본 ASP.NET 계정에 대 한 쓰기 권한을 부여 하는 방법에 대 한 지원을 요청 하십시오. 이번에는 페이지가 오류 없이 로드 되 고 `LastTYASP35Access.txt` 파일을 성공적으로 만들어야 합니다.

여기서는 ASP.NET 개발 서버이 IIS와 다른 보안 컨텍스트에서 작동 하기 때문에 파일 시스템을 읽거나, Windows 이벤트 로그에 쓰거나, Windows에서 읽거나 쓸 수 있는 페이지가 ASP.NET 수 있습니다.  레지스트리는 개발 시 예상 대로 작동 하지만 프로덕션 환경에서는 예외를 생성 합니다. 공유 웹 호스팅 환경에 배포할 웹 응용 프로그램을 빌드하는 경우 이벤트 로그 또는 Windows 레지스트리를 읽거나 쓰지 마십시오. 또한 프로덕션 환경에서 적절 한 폴더에 대 한 읽기 및 쓰기 권한을 부여 해야 할 수 있으므로 파일 시스템에서 읽거나 쓰는 ASP.NET 페이지를 기록해 둡니다.

## <a name="differences-on-serving-static-content"></a>정적 콘텐츠 서비스의 차이점

IIS와 ASP.NET 개발 서버의 또 다른 핵심 차이점은 정적 콘텐츠에 대 한 요청을 처리 하는 방법입니다. ASP.NET 페이지, 이미지 또는 JavaScript 파일에 관계 없이 ASP.NET 개발 서버에 들어오는 모든 요청은 ASP.NET 런타임에 의해 처리 됩니다. 기본적으로 IIS는 ASP.NET 리소스 (예: ASP.NET 웹 페이지, 웹 서비스 등)에 대 한 요청이 들어올 때만 ASP.NET 런타임을 호출 합니다. 정적 콘텐츠, CSS 파일, JavaScript 파일, PDF 파일, ZIP 파일 및 이와 같은에 대 한 요청은 ASP.NET 런타임을 사용 하지 않고 IIS에 의해 검색 됩니다. 정적 콘텐츠를 제공할 때 IIS에 ASP.NET 런타임과 함께 작동 하도록 지시할 수 있습니다. 자세한 내용은이 자습서의 "IIS 7을 사용 하 여 정적 파일에 대 한 폼 기반 인증 및 URL 인증 수행" 섹션을 참조 하세요.

ASP.NET 런타임은 인증 (요청자 식별) 및 권한 부여 (요청자에 게 요청 된 콘텐츠를 볼 수 있는 권한이 있는지 확인)를 포함 하 여 요청 된 콘텐츠를 생성 하는 여러 단계를 수행 합니다. 널리 사용 되는 형태의 인증은 *폼 기반 인증*입니다. 일반적으로 사용자는 웹 페이지의 텍스트 상자에 사용자 이름 및 암호를 입력 하 여 해당 자격 증명을 입력 합니다. 자격 증명의 유효성을 검사할 때 웹 사이트는 사용자의 브라우저에 *인증 티켓* 쿠키를 저장 합니다 .이 쿠키는 웹 사이트에 대 한 모든 후속 요청과 함께 전송 되며 사용자를 인증 하는 데 사용 됩니다. 또한 특정 폴더에 액세스할 수 있거나 액세스할 수 없는 사용자를 지정 하는 *URL 권한 부여* 규칙을 지정할 수 있습니다. 많은 ASP.NET 웹 사이트는 폼 기반 인증 및 URL 권한 부여를 사용 하 여 사용자 계정을 지원 하 고 인증 된 사용자 또는 특정 역할에 속한 사용자만 액세스할 수 있는 사이트의 일부를 정의 합니다.

> [!NOTE]
> ASP에 대 한 철저 한 검사 NET의 폼 기반 인증, URL 권한 부여 및 기타 사용자 계정 관련 기능에 대해서는 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)를 확인 하세요.

양식 기반 권한 부여를 사용 하 여 사용자 계정을 지원 하 고 URL 권한 부여를 사용 하 여 인증 된 사용자만 허용 하도록 구성 된 폴더가 있는 웹 사이트를 생각해 보세요. 이 폴더에는 ASP.NET 페이지와 PDF 파일이 포함 되어 있으며 인증 된 사용자만 이러한 PDF 파일을 볼 수 있다고 가정 합니다.

방문자가 브라우저의 주소 표시줄에 URL을 직접 입력 하 여 이러한 PDF 파일 중 하나를 보려고 하면 어떻게 되나요? 확인을 위해 책 리뷰 사이트에서 새 폴더를 만들고, 일부 PDF 파일을 추가 하 고, 익명 사용자가이 폴더를 방문 하지 못하도록 URL 권한 부여를 사용 하도록 사이트를 구성 하겠습니다. 데모 응용 프로그램을 다운로드 하는 경우 `PrivateDocs` 라는 폴더를 만들고 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) 에서 PDF를 추가 하는 것을 확인할 수 있습니다 (방법 맞춤!). `PrivateDocs` 폴더에는 익명 사용자를 거부할 URL 권한 부여 규칙을 지정 하는 `Web.config` 파일도 포함 되어 있습니다.

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample2.xml)]

마지막으로, 루트 디렉터리의 web.config 파일을 업데이트 하 여 폼 기반 인증을 사용 하도록 웹 응용 프로그램을 구성 하 고 다음을 바꿉니다.

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample3.xml)]

바꿀 대상:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample4.xml)]

ASP.NET 개발 서버를 사용 하 여 사이트를 방문 하 고 브라우저의 주소 표시줄에서 PDF 파일 중 하나에 대 한 직접 URL을 입력 합니다. 이 자습서와 연결 된 웹 사이트를 다운로드 한 경우 URL은 다음과 같습니다. `http://localhost:portNumber/PrivateDocs/aspnet_tutorial01_Basics_vb.pdf`

주소 표시줄에이 URL을 입력 하면 브라우저에서 파일의 ASP.NET 개발 서버 요청을 보냅니다. ASP.NET 개발 서버은 처리를 위해 ASP.NET 런타임으로 요청을 전달 합니다. 아직 로그인 하지 않았으므로 `PrivateDocs` 폴더의 `Web.config` 익명 액세스를 거부 하도록 구성 되어 있기 때문에 ASP.NET 런타임은 자동으로 `Login.aspx` 로그인 페이지 (그림 3 참조)로 리디렉션합니다. 사용자를 로그인 페이지로 리디렉션하는 경우 ASP.NET는 사용자가 보려고 하는 페이지를 나타내는 querystring 매개 변수 `ReturnUrl`를 포함 합니다. 성공적으로 로그인 한 후에는이 페이지로 이동할 수 있습니다.

[![권한이 없는 사용자가 자동으로 로그인 페이지로 리디렉션됩니다.](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image8.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image7.png)

**그림 3**: 권한이 없는 사용자가 자동으로 로그인 페이지로 리디렉션됩니다 ([전체 크기 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image9.png)).

이제이를 프로덕션에서 어떻게 작동 하는지 살펴보겠습니다. 응용 프로그램을 배포 하 고 프로덕션의 `PrivateDocs` 폴더에 있는 Pdf 중 하나에 대 한 직접 URL을 입력 합니다. 그러면 브라우저에서 파일에 대 한 요청 IIS를 전송 하 라는 메시지가 표시 됩니다. 정적 파일이 요청 되기 때문에 IIS는 ASP.NET 런타임을 호출 하지 않고 파일을 검색 하 여 반환 합니다. 따라서 URL 권한 부여 검사를 수행 하지 않았습니다. 파일에 대 한 직접 URL을 알고 있는 사용자는 개인 PDF의 내용에 액세스할 수 있습니다.

[![익명 사용자는 파일에 대 한 직접 URL을 입력 하 여 개인 PDF 파일을 다운로드할 수 있습니다.](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image11.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image10.png)

**그림 4**: 익명 사용자는 파일에 대 한 직접 URL을 입력 하 여 개인 PDF 파일을 다운로드할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image12.png)).

### <a name="performing-forms-based-authentication-and-url-authentication-on-static-files-with-iis-7"></a>IIS 7을 사용 하 여 정적 파일에 대 한 폼 기반 인증 및 URL 인증 수행

권한 없는 사용자 로부터 정적 콘텐츠를 보호 하는 데 사용할 수 있는 몇 가지 기술이 있습니다. IIS 7에는 IIS의 워크플로를 ASP.NET 런타임의 워크플로로 결혼 하는 *통합 파이프라인이*도입 되었습니다. 간단히 말해서, IIS에 들어오는 모든 요청 (PDF 파일 등의 정적 콘텐츠 포함)을 ASP.NET 런타임의 인증 및 권한 부여 모듈로 호출 하도록 지시할 수 있습니다. 웹 호스트 공급자에 게 문의 하 여 통합 파이프라인을 사용 하도록 웹 사이트를 구성 하는 방법을 알아보세요.

IIS가 통합 파이프라인을 사용 하도록 구성 된 후에는 루트 디렉터리의 `Web.config` 파일에 다음 태그를 추가 합니다.

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample5.xml)]

이 태그는 IIS 7에 ASP.NET 기반 인증 및 권한 부여 모듈을 사용 하도록 지시 합니다. 응용 프로그램을 다시 배포한 다음 PDF 파일을 다시 방문 하세요. 이번에는 IIS에서 요청을 처리할 때 ASP.NET 런타임의 인증 및 권한 부여 논리에서 요청을 검사할 수 있는 기회를 제공 합니다. 인증 된 사용자만 `PrivateDocs` 폴더의 내용을 볼 수 있는 권한이 있기 때문에 익명 방문자가 자동으로 로그인 페이지로 리디렉션됩니다 (그림 3 참조).

> [!NOTE]
> 웹 호스트 공급자가 여전히 IIS 6을 사용 하 고 있는 경우 통합 파이프라인 기능을 사용할 수 없습니다. 한 가지 해결 방법은 HTTP 액세스를 금지 하는 폴더 (예: `App_Data`)에 개인 문서를 넣고 이러한 문서를 제공 하는 페이지를 만드는 것입니다. 이 페이지는 `GetPDF.aspx`호출 될 수 있으며 querystring 매개 변수를 통해 PDF 이름이 전달 됩니다. `GetPDF.aspx` 페이지는 먼저 사용자에 게 파일을 볼 수 있는 권한이 있는지 확인 하 고, 해당 하는 경우 [`Response.WriteFile(filePath)`](https://msdn.microsoft.com/library/system.web.httpresponse.writefile.aspx) 메서드를 사용 하 여 요청 된 PDF 파일의 콘텐츠를 요청 하는 클라이언트에 다시 보냅니다. 이 기법은 통합 파이프라인을 사용 하지 않으려는 경우 IIS 7에도 적용 됩니다.

## <a name="summary"></a>요약

프로덕션 환경의 웹 응용 프로그램은 Microsoft의 IIS 웹 서버 소프트웨어를 사용 하 여 호스팅됩니다. 그러나 개발 환경에서는 IIS 또는 ASP.NET 개발 서버를 사용 하 여 응용 프로그램을 호스트할 수 있습니다. 서로 다른 소프트웨어를 사용 하 여 혼합에 다른 변수를 추가 하기 때문에 두 환경에서 동일한 웹 서버 소프트웨어를 사용 하는 것이 가장 좋습니다. 그러나 ASP.NET 개발 서버를 사용 하면 개발 환경에서 편리 하 게 선택할 수 있습니다. 좋은 소식은 IIS와 ASP.NET 개발 서버 사이에는 몇 가지 근본적인 차이가 있다는 것입니다. 이러한 차이점을 알고 있는 경우 응용 프로그램의 작동을 보장 하는 데 도움이 되는 단계를 수행 하 고, 개발.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET와 IIS 7.0 통합](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)
- [IIS 7에서 모든 유형의 콘텐츠를 사용 하 여 ASP.NET 포럼 인증 사용](https://blogs.iis.net/bills/archive/2007/05/19/using-asp-net-forms-authentication-with-all-types-of-content-with-iis7-video.aspx) (비디오)
- [Visual Web Developer의 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx)

> [!div class="step-by-step"]
> [이전](common-configuration-differences-between-development-and-production-vb.md)
> [다음](deploying-a-database-vb.md)
