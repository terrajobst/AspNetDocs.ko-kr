---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-cs
title: FTP 클라이언트를 사용 하 여 사이트 배포C#() | Microsoft Docs
author: rick-anderson
description: ASP.NET 응용 프로그램을 배포 하는 가장 간단한 방법은 필요한 파일을 개발 환경에서 프로덕션 환경으로 수동으로 복사 하는 것입니다. Thi...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: a3599cf7-8474-4006-954a-3bc693736b66
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-cs
msc.type: authoredcontent
ms.openlocfilehash: a3474650939ee220b3fd712e9f5a6cf3db11db09
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438947"
---
# <a name="deploying-your-site-using-an-ftp-client-c"></a>FTP 클라이언트를 사용하여 사이트 배포(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_03_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial03_DeployingViaFTP_cs.pdf)

> ASP.NET 응용 프로그램을 배포 하는 가장 간단한 방법은 필요한 파일을 개발 환경에서 프로덕션 환경으로 수동으로 복사 하는 것입니다. 이 자습서에서는 FTP 클라이언트를 사용 하 여 데스크톱에서 웹 호스트 공급자로 파일을 가져오는 방법을 보여 줍니다.

## <a name="introduction"></a>소개

이전 자습서에는 간단한 책 리뷰 ASP.NET 웹 응용 프로그램이 도입 되었습니다 .이 응용 프로그램은 몇 가지 ASP.NET 페이지, 마스터 페이지, 사용자 지정 기본 `Page` 클래스, 많은 이미지 및 3 개의 CSS 스타일 시트로 구성 되어 있습니다. 이제이 응용 프로그램을 웹 호스트 공급자에 배포할 준비가 되었습니다 .이 시점에서 인터넷에 연결 된 모든 사용자가 응용 프로그램에 액세스할 수 있습니다.

배포 해야 하는 [*파일 결정*](determining-what-files-need-to-be-deployed-cs.md) 자습서의 토론에서 웹 호스트 공급자에 복사 해야 하는 파일을 알 수 있습니다. (복사 되는 파일은 응용 프로그램의 명시적 또는 자동 컴파일 여부에 따라 달라 집니다.) 하지만 개발 환경 (microsoft 데스크톱)에서 프로덕션 환경 (웹 호스트 공급자에서 관리 하는 웹 서버)까지 파일을 가져오는 방법은 무엇 인가요? [ **F** 파일 **T** ransfer **P** rotocol (FTP)](http://en.wikipedia.org/wiki/File_Transfer_Protocol) 는 네트워크를 통해 한 컴퓨터에서 다른 컴퓨터로 파일을 복사 하는 데 일반적으로 사용 되는 프로토콜입니다. 또 다른 옵션은 FrontPage Server Extensions (FPSE)입니다. 이 자습서에서는 독립 실행형 FTP 클라이언트 소프트웨어를 사용 하 여 개발 환경에서 프로덕션 환경으로 필요한 파일을 배포 하는 방법을 집중적으로 설명 합니다.

> [!NOTE]
> Visual Studio에는 FTP를 통해 웹 사이트를 게시 하기 위한 도구가 포함 되어 있습니다. 이러한 도구 뿐만 아니라 FPSE를 사용 하는 도구에 대 한 자세한 내용은 다음 자습서에서 다룹니다.

FTP를 사용 하 여 파일을 복사 하려면 개발 환경에 *ftp 클라이언트가* 필요 합니다. FTP 클라이언트는 설치 된 컴퓨터에서 *ftp 서버*를 실행 하는 컴퓨터에 파일을 복사 하도록 디자인 된 응용 프로그램입니다. 웹 호스트 공급자가 FTP를 통해 파일 전송을 지 원하는 경우에는 대부분 웹 서버에서를 실행 하는 FTP 서버가 있습니다. 사용할 수 있는 FTP 클라이언트 응용 프로그램은 여러 가지가 있습니다. 웹 브라우저가 FTP 클라이언트와 이중으로도 가능 합니다. 즐겨 사용 하는 FTP 클라이언트와이 자습서에서 사용 하는 것은 Windows, Linux 및 Mac에서 사용할 수 있는 무료 오픈 소스 FTP 클라이언트 [FileZilla](http://filezilla-project.org/). 그러나 모든 FTP 클라이언트는 작동 하지만 가장 편안한 모든 클라이언트를 자유롭게 사용할 수 있습니다.

함께 사용 하는 경우이 자습서 또는 후속 자습서를 완료 하기 전에 웹 호스트 공급자를 사용 하 여 계정을 만들어야 합니다. 이전 자습서에 설명 된 것 처럼 다양 한 가격, 기능 및 서비스 품질을 제공 하는 웹 호스트 공급자 회사의 gaggle 있습니다. 이 자습서 시리즈의 경우 웹 호스트 공급자로 [할인 ASP.NET](http://discountasp.net) 을 사용 하지만, 사이트를 개발 하는 ASP.NET 버전을 지 원하는 모든 웹 호스트 공급자와 함께 수행할 수 있습니다. ASP.NET 3.5를 사용 하 여 이러한 자습서를 만들었습니다. 또한이 자습서에서 FTP를 사용 하 여 웹 호스트 공급자에 파일을 복사 하 고 나중에 웹 호스트 공급자가 웹 서버에 대 한 FTP 액세스를 지원 해야 합니다. 거의 모든 웹 호스트 공급자는이 기능을 제공 하지만 등록 하기 전에 두 번 확인 해야 합니다.

## <a name="deploying-the-book-review-web-application-project"></a>서적 검토 웹 응용 프로그램 프로젝트 배포

BookReviewsWAP (웹 응용 프로그램 프로젝트 모델)를 사용 하 여 구현 되는 웹 응용 프로그램 및 BookReviewsWSP (웹 사이트 프로젝트 모델)의 두 가지 버전이 있습니다. 프로젝트 형식은 사이트가 자동 또는 명시적으로 컴파일 되었는지 여부와 해당 컴파일 모델에서 배포 해야 하는 파일을 결정 합니다. 따라서 BookReviewsWAP부터 시작 하 여 BookReviewsWAP 및 BookReviewsWSP 프로젝트를 개별적으로 배포 하는 것을 확인할 수 있습니다. 아직 수행 하지 않은 경우이 두 ASP.NET 응용 프로그램을 다운로드 하세요.

`BookReviewsWAP` 폴더로 이동한 다음 `BookReviewsWAP.sln` 파일을 두 번 클릭 하 여 BookReviewsWAP 프로젝트를 시작 합니다. 프로젝트를 배포 하기 전에 소스 코드의 변경 내용이 컴파일된 어셈블리에 포함 되도록 빌드하는 것이 중요 합니다. 프로젝트를 빌드하려면 빌드 메뉴로 이동 하 여 빌드 BookReviewsWAP 메뉴 옵션을 선택 합니다. 이렇게 하면 프로젝트의 소스 코드를 `Bin` 폴더에 배치 되는 단일 어셈블리 `BookReviewsWAP.dll`로 컴파일합니다.

이제 필요한 파일을 배포할 준비가 되었습니다. FTP 클라이언트를 시작 하 고 웹 호스트 공급자의 웹 서버에 연결 합니다. 웹 호스팅 회사에 등록 하면 ftp 서버에 연결 하는 방법에 대 한 정보를 전자 메일로 보낼 수 있습니다. 여기에는 FTP 서버에 대 한 주소와 사용자 이름 및 암호도 포함 됩니다.

데스크톱에서 웹 호스트 공급자의 루트 웹 사이트 폴더로 다음 파일을 복사 합니다. 웹 호스트 공급자의 웹 서버에 FTP를 만들면 루트 웹 사이트 디렉터리가 될 가능성이 높습니다. 그러나 일부 웹 호스트 공급자에는 웹 사이트 파일의 루트 폴더 역할을 하는 `www` 또는 `wwwroot` 라는 하위 폴더가 있습니다. 마지막으로, 파일을 FTPing 할 때 프로덕션 환경에서 해당 폴더 구조를 만들어야 할 수 있습니다 (`Bin` 폴더, `Fiction` 폴더, `Images` 폴더 등).

- `~/Default.aspx`
- `~/About.aspx`
- `~/Site.master`
- `~/Web.config`
- `~/Web.sitemap`
- `Styles` 폴더의 전체 내용
- `Images` 폴더 및 해당 하위 폴더의 전체 콘텐츠 (`BookCovers`)
- `~/Fiction/Default.aspx`
- `~/Fiction/Blaze.aspx`
- `~/Tech/Default.aspx`
- `~/Tech/CYOW.aspx`
- `~/Tech/TYASP35.aspx`
- `~/Bin/BookReviewsWAP.dll`

그림 1은 필요한 파일이 복사 된 후의 FileZilla를 보여 줍니다. FileZilla 로컬 컴퓨터의 왼쪽에 파일을 표시 하 고 원격 컴퓨터의 파일을 오른쪽에 표시 합니다. 그림 1에 나와 있는 것 처럼 ASP.NET 원본 코드 파일 (`About.aspx.cs`예:)은 로컬 컴퓨터에 있지만 (개발 환경), 명시적 컴파일을 사용할 때 코드 파일을 배포할 필요가 없기 때문에 웹 호스트 공급자 (프로덕션 환경)에 복사 되지 않았습니다.

> [!NOTE]
> 원본 코드 파일은 무시 되므로 프로덕션 서버에는 피해를 주지 않습니다. ASP.NET는 기본적으로 소스 코드 파일에 대 한 HTTP 요청을 금지 하므로 소스 코드 파일이 프로덕션 서버에 있는 경우에도 웹 사이트 방문자가 액세스할 수 없게 됩니다. 즉, 사용자가 `http://www.yoursite.com/Default.aspx.cs` 방문 하려고 하면 이러한 유형의 파일 (`.cs` 파일)이 사용할 수 없다는 것을 설명 하는 오류 페이지가 표시 됩니다.

[FTP 클라이언트를 사용 하 여 데스크톱에서 웹 호스트 공급자의 웹 서버로 필요한 파일을 복사 ![](deploying-your-site-using-an-ftp-client-cs/_static/image2.png)](deploying-your-site-using-an-ftp-client-cs/_static/image1.png)

**그림 1**: FTP 클라이언트를 사용 하 여 데스크톱에서 웹 호스트 공급자의 웹 서버로 필요한 파일 복사 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-an-ftp-client-cs/_static/image3.png))

사이트를 배포한 후에는 사이트를 테스트 하는 데 잠시 시간이 걸립니다. 도메인 이름을 구입 하 고 DNS 설정을 적절히 구성한 경우 도메인 이름을 입력 하 여 사이트를 방문할 수 있습니다. 또는 웹 호스트 공급자가 사이트에 대 한 URL을 제공 해야 합니다 .이 URL은 *accountname*처럼 보입니다. *webhostprovider*.com 또는 *webhostprovider*.com/*accountname* 예를 들어 할인 ASP.NET의 내 계정에 대 한 URL은 `http://httpruntime.web703.discountasp.net`입니다.

그림 2는 배포 된 책 리뷰 사이트를 보여 줍니다. 이 정보는 할인 ASP에서 볼 수 있습니다. `http://httpruntime.web703.discountasp.net`에서 순 서버. 이 시점에서 인터넷에 연결 된 모든 사용자는 웹 사이트를 볼 수 있습니다. 짐작할 수 있듯이 사이트는 개발 환경에서 테스트 하는 경우와 마찬가지로 표시 되 고 작동 합니다.

> [!NOTE]
> 응용 프로그램을 볼 때 오류가 발생 하는 경우 올바른 파일 집합을 배포 했는지 확인 합니다. 그런 다음 오류 메시지를 확인 하 여 문제에 대 한 단서를 표시 하는지 확인 합니다. 그런 다음 웹 호스트 회사의 기술 지원팀에 문의 하거나 [ASP.NET 포럼](https://forums.asp.net/)의 적절 한 포럼에 질문을 게시할 수 있습니다.

[![이제 인터넷에 연결 된 모든 사용자가 책 리뷰 사이트에 액세스할 수 있습니다.](deploying-your-site-using-an-ftp-client-cs/_static/image5.png)](deploying-your-site-using-an-ftp-client-cs/_static/image4.png)

**그림 2**: 이제 인터넷에 연결 된 모든 사용자가 책 리뷰 사이트에 액세스할 수 있음 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-an-ftp-client-cs/_static/image6.png))

## <a name="deploying-the-book-review-web-site-project"></a>서적 검토 웹 사이트 프로젝트 배포

BookReviewsWSP 웹 사이트 프로젝트와 같은 자동 컴파일을 사용 하는 ASP.NET 응용 프로그램을 배포 하는 경우 `Bin` 폴더에 컴파일된 어셈블리가 없습니다. 따라서 웹 응용 프로그램의 소스 코드 파일을 프로덕션 환경에 배포 해야 합니다. 이 프로세스를 살펴보겠습니다.

웹 응용 프로그램 프로젝트와 마찬가지로 응용 프로그램을 배포 하기 전에 먼저 빌드해야 합니다. 웹 사이트 프로젝트를 빌드하면 어셈블리가 생성 되지 않지만 페이지에서 컴파일 시간 오류가 있는지 확인 합니다. 사이트 방문자가 사용자를 대신 하 여 이러한 오류를 검색 하는 것이 더 좋습니다.

프로젝트를 성공적으로 빌드한 후에는 FTP 클라이언트를 사용 하 여 웹 호스트 공급자의 루트 웹 사이트 폴더에 다음 파일을 복사 합니다. 프로덕션 환경에서 해당 폴더 구조를 만들어야 할 수도 있습니다.

> [!NOTE]
> BookReviewsWAP 프로젝트를 이미 배포 했지만 여전히 BookReviewsWSP 프로젝트를 배포 하려는 경우 BookReviewsWAP를 배포할 때 업로드 된 웹 서버의 모든 파일을 삭제 한 다음 BookReviewsWSP에 대 한 파일을 배포 합니다.

- `~/Default.aspx`
- `~/Default.aspx.cs`
- `~/About.aspx`
- `~/About.aspx.cs`
- `~/Site.master`
- `~/Site.master.cs`
- `~/Web.config`
- `~/Web.sitemap`
- `Styles` 폴더의 전체 내용
- `Images` 폴더 및 해당 하위 폴더의 전체 콘텐츠 (`BookCovers`)
- `~/App_Code/BasePage.cs`
- `~/Fiction/Default.aspx`
- `~/Fiction/Default.aspx.cs`
- `~/Fiction/Blaze.aspx`
- `~/Fiction/Blaze.aspx.cs`
- `~/Tech/Default.aspx`
- `~/Tech/Default.aspx.cs`
- `~/Tech/CYOW.aspx`
- `~/Tech/CYOW.aspx.cs`
- `~/Tech/TYASP35.aspx`
- `~/Tech/TYASP35.aspx.cs`

그림 3에서는 필요한 파일을 복사한 후 FileZilla를 보여 줍니다. 여기에서 볼 수 있듯이 자동 컴파일을 사용할 때 코드 파일을 배포 해야 하기 때문에 `About.aspx.cs`와 같은 ASP.NET 원본 코드 파일은 로컬 컴퓨터 (개발 환경)와 웹 호스트 공급자 (프로덕션 환경)에 모두 있습니다.

[FTP 클라이언트를 사용 하 여 데스크톱에서 웹 호스트 공급자의 웹 서버로 필요한 파일을 복사 ![](deploying-your-site-using-an-ftp-client-cs/_static/image8.png)](deploying-your-site-using-an-ftp-client-cs/_static/image7.png)

**그림 3**: FTP 클라이언트를 사용 하 여 데스크톱에서 웹 호스트 공급자의 웹 서버로 필요한 파일 복사 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-an-ftp-client-cs/_static/image9.png))

사용자 환경은 응용 프로그램의 컴파일 모델에 의해 영향을 받지 않습니다. 웹 응용 프로그램 프로젝트 모델 또는 웹 사이트 프로젝트 모델을 사용 하 여 웹 사이트를 만들었는지 여부와 상관 없이 동일한 ASP.NET 페이지에 액세스할 수 있으며 이러한 페이지는 동일 하 게 표시 되 고 동작 합니다.

### <a name="updating-a-web-application-on-production"></a>프로덕션 환경에서 웹 응용 프로그램 업데이트

웹 응용 프로그램 개발 및 배포는 일회성 프로세스가 아닙니다. 예를 들어, 책 리뷰 웹 사이트를 만들 때 다양 한 페이지를 빌드하고 개인용 컴퓨터 (개발 환경)에 해당 코드를 작성 했습니다. 안정적인 특정 상태에 도달한 후에는 다른 사용자가 사이트를 방문 하 여 내 리뷰를 읽을 수 있도록 응용 프로그램을 배포 했습니다. 하지만 배포는이 사이트에서 내 개발의 끝을 표시 하지 않습니다. 책 리뷰를 추가 하거나 새로운 기능을 구현할 수 있습니다. 예를 들어 내 방문자에 게 책을 평가 하거나 자신의 의견을 남길 수 있습니다. 이러한 향상 된 기능은 개발 환경에서 개발 되 고 완료 되 면 배포 해야 합니다. 따라서 개발 및 배포는 순환 됩니다. 응용 프로그램을 개발 하 고 배포 합니다. 사이트가 실시간이 고 프로덕션 환경에 있는 동안 새로운 기능이 추가 되 고 시간이 지남에 따라 버그가 고정 되므로 응용 프로그램을 다시 배포 해야 합니다. 등으로 설정 합니다.

짐작할 수 있듯이, 웹 응용 프로그램을 다시 배포할 때 새 파일 및 변경 된 파일만 복사 하면 됩니다. 변경 되지 않은 페이지나 서버 또는 클라이언트 쪽 지원 파일을 다시 배포할 필요는 없습니다 (이 경우에는 피해 야 함).

> [!NOTE]
> 명시적 컴파일을 사용할 때는 언제 든 지 프로젝트에 새 ASP.NET 페이지를 추가 하거나 코드 관련 변경을 수행할 때 프로젝트를 다시 빌드해야 하므로 `Bin` 폴더의 어셈블리가 업데이트 됩니다. 따라서 프로덕션에서 웹 응용 프로그램을 업데이트할 때이 업데이트 된 어셈블리를 프로덕션에 복사 해야 합니다 (다른 신규 및 업데이트 된 콘텐츠와 함께).

또한 `Bin` 디렉터리의 `Web.config` 또는 파일에 대 한 변경 내용이 웹 사이트의 응용 프로그램 풀을 중지 하 고 다시 시작 한다는 것을 알고 있어야 합니다. 세션 상태가 `InProc` 모드 (기본값)를 사용 하 여 저장 되는 경우 이러한 키 파일이 수정 될 때마다 사이트 방문자의 세션 상태가 손실 됩니다. 이러한 문제를 방지 하려면 `StateServer` 또는 `SQLServer` 모드를 사용 하 여 세션을 저장 하는 것이 좋습니다. 이 항목에 대 한 자세한 내용은 [세션 상태 모드](https://msdn.microsoft.com/library/ms178586.aspx)를 참조 하세요.

마지막으로, 응용 프로그램을 다시 배포 하는 것은 프로덕션 환경에 복사 해야 하는 파일의 수와 크기에 따라 몇 초에서 몇 분 정도 걸릴 수 있다는 점에 유의 하세요. 이 시간 동안 사이트를 방문 하는 사용자는 오류 또는 이상한 동작이 발생할 수 있습니다. 응용 프로그램의 루트 디렉터리에 `App_Offline.htm` 라는 페이지를 추가 하 여 전체 응용 프로그램을 "해제" 할 수 있습니다 .이 페이지는 사용자에 게 해당 사이트가 유지 관리를 위해 작동 중단 되 고 곧 백업 될 것 이라는 것을 사용자에 게 설명 합니다. `App_Offline.htm` 파일이 있으면 ASP.NET 런타임은 들어오는 모든 요청을 해당 페이지로 리디렉션합니다.

## <a name="summary"></a>요약

웹 응용 프로그램을 배포 하는 경우 개발 환경에서 프로덕션 환경으로 필요한 파일을 복사 하는 작업이 수반 됩니다. 네트워크를 통해 파일을 전송 하는 가장 일반적인 방법은 FTP (파일 전송 프로토콜) 이며 대부분의 웹 호스트 공급자는 웹 서버에 대 한 FTP 액세스를 지원 합니다. 이 자습서에서는 FTP 클라이언트를 사용 하 여 필요한 파일을 웹 서버에 배포 하는 방법을 살펴보았습니다. 배포한 후에는 인터넷에 연결 된 모든 사용자가 웹 사이트를 방문할 수 있습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [앱\_오프 라인 .htm 및 "IE의 친숙 한 오류" 기능 해결](https://weblogs.asp.net/scottgu/App_5F00_Offline.htm-and-working-around-the-_2200_IE-Friendly-Errors_2200_-feature)
- [세션 상태 모드](https://msdn.microsoft.com/library/ms178586.aspx)

> [!div class="step-by-step"]
> [이전](determining-what-files-need-to-be-deployed-cs.md)
> [다음](deploying-your-site-using-visual-studio-cs.md)
