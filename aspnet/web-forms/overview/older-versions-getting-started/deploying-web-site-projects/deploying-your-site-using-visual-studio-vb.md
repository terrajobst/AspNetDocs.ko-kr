---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-vb
title: Visual Studio를 사용 하 여 사이트 배포 (VB) | Microsoft Docs
author: rick-anderson
description: Visual Studio에는 웹 사이트를 배포 하기 위한 도구가 포함 되어 있습니다. 이 자습서에서 이러한 도구에 대해 자세히 알아보세요.
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 977105f3-7987-4e50-8be7-afb53b4ca28a
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-vb
msc.type: authoredcontent
ms.openlocfilehash: 6c71e36a8a434947882cc767cd2f903ff6e8d422
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474623"
---
# <a name="deploying-your-site-using-visual-studio-vb"></a>Visual Studio를 사용하여 사이트 배포(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_04_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial04_DeployingViaVS_vb.pdf)

> Visual Studio에는 웹 사이트를 배포 하기 위한 도구가 포함 되어 있습니다. 이 자습서에서 이러한 도구에 대해 자세히 알아보세요.

## <a name="introduction"></a>소개

이전 자습서에서는 간단한 ASP.NET 웹 응용 프로그램을 웹 호스트 공급자에 배포 하는 방법을 살펴보았습니다. 특히이 자습서에서는 FileZilla와 같은 FTP 클라이언트를 사용 하 여 개발 환경에서 프로덕션 환경으로 필요한 파일을 전송 하는 방법을 살펴보았습니다. 또한 Visual Studio는 웹 호스트 공급자에 게 쉽게 배포할 수 있는 기본 제공 도구를 제공 합니다. 이 자습서에서는 FTP 또는 FrontPage Server Extensions를 사용 하 여 원격 웹 서버 간에 파일을 이동할 수 있는 웹 사이트 복사 도구의 두 가지 도구를 살펴봅니다. 및 게시 도구는 전체 웹 사이트를 지정 된 위치에 복사 합니다.

> [!NOTE]
> Visual Studio에서 제공 하는 기타 배포 관련 도구에는 [웹 설치 프로젝트](https://msdn.microsoft.com/library/wx3b589t.aspx) 및 [웹 배포 프로젝트](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) 추가 기능이 포함 됩니다. 웹 설치 프로젝트는 웹 사이트의 내용과 구성 정보를 단일 MSI 파일로 패키지 합니다. 이 옵션은 인트라넷 내에 배포 된 웹 사이트 또는 고객이 자신의 웹 서버에 설치 하는 미리 패키지 된 웹 응용 프로그램을 판매 하는 회사에 가장 유용 합니다. 웹 배포 프로젝트 추가 기능은 개발 환경 및 프로덕션 환경에 대 한 빌드 간의 구성 차이점을 쉽게 지정할 수 있게 해 주는 Visual Studio 추가 기능입니다. 웹 설치 프로젝트는이 자습서 시리즈에서 다루지 않습니다. 웹 배포 프로젝트는 [*개발 및 프로덕션 자습서 간의 일반적인 구성 차이점*](common-configuration-differences-between-development-and-production-vb.md) 에 요약 되어 있습니다.

## <a name="deploying-your-site-using-the-copy-web-site-tool"></a>웹 사이트 복사 도구를 사용 하 여 사이트 배포

Visual Studio의 웹 사이트 복사 도구는 독립 실행형 FTP 클라이언트와 기능적으로 비슷합니다. 간단히 말해서 웹 사이트 복사 도구를 사용 하 여 FTP 또는 FrontPage Server Extensions를 통해 원격 웹 사이트에 연결할 수 있습니다. FileZilla의 사용자 인터페이스와 마찬가지로, 웹 사이트 복사 사용자 인터페이스는 두 개의 창으로 구성 되어 있습니다. 왼쪽 창에는 로컬 파일이 표시 되 고 오른쪽 창에는 대상 서버에 있는 파일이 나열 됩니다.

> [!NOTE]
> 웹 사이트 복사 도구는 웹 사이트 프로젝트에만 사용할 수 있습니다. Visual Studio는 웹 응용 프로그램 프로젝트를 사용할 때이 도구를 제공 합니다.

웹 사이트 복사 도구를 사용 하 여 책 리뷰 응용 프로그램을 프로덕션에 게시 하는 방법을 살펴보겠습니다. 웹 사이트 복사 도구는 웹 사이트 프로젝트 모델을 사용 하는 프로젝트 에서만 작동 하기 때문에 BookReviewsWSP 프로젝트 에서만이 도구를 사용 하 여 검사할 수 있습니다. 해당 프로젝트를 엽니다.

솔루션 탐색기에서 웹 사이트 복사 아이콘을 클릭 하 여 웹 사이트 복사 도구 프로젝트를 시작 합니다 .이 아이콘은 그림 1에 원이 있습니다. 또는 웹 사이트 메뉴에서 웹 사이트 복사 옵션을 선택할 수 있습니다. 어느 방법을 사용 하 든 그림 1에 표시 된 웹 사이트 사용자 인터페이스 복사를 시작 합니다. 원격 서버에 연결 하기 때문에 그림 1의 왼쪽 창만 채워집니다.

[![웹 사이트 복사 도구의 사용자 인터페이스가 두 개의 창으로 구분 됩니다.](deploying-your-site-using-visual-studio-vb/_static/image2.png)](deploying-your-site-using-visual-studio-vb/_static/image1.png)

**그림 1**: 웹 사이트 복사 도구의 사용자 인터페이스는 두 개의 창으로 구분 됩니다 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-visual-studio-vb/_static/image3.png)).

사이트를 배포 하려면 먼저 웹 호스트 공급자에 연결 해야 합니다. 웹 사이트 복사 사용자 인터페이스의 위쪽에 있는 연결 단추를 클릭 합니다. 그러면 그림 2에 표시 된 웹 사이트 열기 대화 상자가 표시 됩니다.

왼쪽에서 네 가지 옵션 중 하나를 선택 하 여 대상 웹 사이트에 연결할 수 있습니다.

- **파일 시스템** -사이트를 컴퓨터에서 액세스할 수 있는 폴더 또는 네트워크 공유에 배포 하려면이 옵션을 선택 합니다.
- **로컬 iis** -컴퓨터에 설치 된 IIS 웹 서버에 사이트를 배포 하려면이 옵션을 사용 합니다.
- **Ftp 사이트** -ftp를 사용 하 여 원격 웹 사이트에 연결 합니다.
- **원격 사이트** -FrontPage Server Extensions를 사용 하 여 원격 웹 사이트에 연결 합니다.

대부분의 웹 호스트 공급자는 FTP를 지원 하지만 FrontPage 서버 확장 지원을 제공 하지 않습니다. 이러한 이유로 FTP 사이트 옵션을 선택한 다음 그림 2에 표시 된 것 처럼 연결 정보를 입력 했습니다.

[대상 웹 사이트를 지정 ![](deploying-your-site-using-visual-studio-vb/_static/image5.png)](deploying-your-site-using-visual-studio-vb/_static/image4.png)

**그림 2**: 대상 웹 사이트 지정 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-visual-studio-vb/_static/image6.png))

연결 하면 웹 사이트 복사 도구가 오른쪽 창의 원격 사이트에 있는 파일을 로드 하 고 각 파일의 상태 (새로 만들기, 삭제 됨, 변경 됨 또는 변경 되지 않음)를 표시 합니다. 로컬 사이트에서 원격 사이트로 파일을 복사 하거나 그 반대로 파일을 복사할 수 있습니다.

BookReviewsWSP 프로젝트에 새 페이지를 추가 하 고 배포 하 여 웹 사이트 복사 도구가 작동 하는 것을 볼 수 있게 합니다. `Privacy.aspx`이라는 루트 디렉터리에 Visual Studio에서 새 ASP.NET 페이지를 만듭니다. 페이지에서 마스터 페이지 `Site.master` 사용 하 고 사이트의 개인 정보 취급 방침을이 페이지에 추가 하도록 합니다. 그림 3에서는이 페이지를 만든 후의 Visual Studio를 보여 줍니다.

[웹 사이트의 루트 폴더에 &lt;코드&gt;개인 정보 ![&lt;/code&gt; 라는 새 페이지를 추가 합니다.](deploying-your-site-using-visual-studio-vb/_static/image8.png)](deploying-your-site-using-visual-studio-vb/_static/image7.png)

**그림 3**: 웹 사이트의 루트 폴더에 `Privacy.aspx` 라는 새 페이지 추가 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-visual-studio-vb/_static/image9.png))

그런 다음 웹 사이트 복사 사용자 인터페이스로 돌아갑니다. 그림 4와 같이 왼쪽 창에는 이제 새 파일 `Policy.aspx` 및 `Policy.aspx.vb`포함 되어 있습니다. 또한 이러한 파일은 화살표 아이콘과 새 상태로 표시 됩니다 .이는 로컬 사이트에 있지만 원격 사이트에는 존재 하지 않음을 나타냅니다.

[![웹 사이트 복사 도구는 왼쪽 창의 새 &lt;코드&gt;개인 정보 .aspx&lt;/code&gt; 페이지를 포함 합니다.](deploying-your-site-using-visual-studio-vb/_static/image11.png)](deploying-your-site-using-visual-studio-vb/_static/image10.png)

**그림 4**: 웹 사이트 복사 도구는 왼쪽 창에 새 `Privacy.aspx` 페이지 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-visual-studio-vb/_static/image12.png))를 포함 합니다.

새 파일을 배포 하려면 해당 파일을 선택 하 고 화살표 아이콘을 클릭 하 여 원격 사이트로 전송 합니다. 전송이 `Policy.aspx` 완료 되 고 상태가 변경 되지 않은 로컬 및 원격 사이트에 `Policy.aspx.vb` 파일이 있습니다.

새 파일을 나열 하는 것과 함께 웹 사이트 복사 도구는 로컬 사이트와 원격 사이트 간에 다른 모든 파일을 강조 표시 합니다. 이 작업을 수행 하려면 `Privacy.aspx` 페이지로 돌아가 개인 정보 취급 방침에 몇 가지 추가 단어를 추가 하세요. 페이지를 저장 하 고 웹 사이트 복사 도구로 돌아갑니다. 그림 5와 같이 왼쪽 창의 `Privacy.aspx` 페이지는 원격 사이트와 동기화 되지 않았음을 나타내는 변경 됨 상태를 표시 합니다.

[웹 사이트 복사 도구 ![&lt;&gt;개인 정보 .aspx&lt;/code&gt; 페이지가 변경 되었음을 나타냅니다.](deploying-your-site-using-visual-studio-vb/_static/image14.png)](deploying-your-site-using-visual-studio-vb/_static/image13.png)

**그림 5**: 웹 사이트 복사 도구는 `Privacy.aspx` 페이지가 변경 되었음을 나타냅니다 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-visual-studio-vb/_static/image15.png)).

또한 웹 사이트 복사 도구는 마지막 복사 작업 이후 파일이 삭제 되었는지 여부를 나타냅니다. 로컬 프로젝트에서 `Privacy.aspx`를 삭제 하 고 웹 사이트 복사 도구를 새로 고칩니다. `Privacy.aspx` 및 `Privacy.aspx.vb` 파일은 왼쪽 창에는 그대로 남아 있지만 마지막 복사 작업 이후 제거 되었음을 나타내는 삭제 됨 상태가 표시 됩니다.

## <a name="publishing-a-web-application"></a>웹 응용 프로그램 게시

Visual Studio 내에서 웹 응용 프로그램을 배포 하는 또 다른 방법은 빌드 메뉴를 통해 액세스할 수 있는 게시 옵션을 사용 하는 것입니다. 게시 옵션은 응용 프로그램을 명시적으로 컴파일한 다음 지정 된 원격 사이트에 필요한 모든 파일을 복사 합니다. 곧 볼 수 있듯이 게시 옵션은 웹 사이트 복사 도구 보다 더 무딘 것입니다. 웹 사이트 복사 도구를 사용 하면 로컬 및 원격 사이트에 있는 파일을 검사 하 고 필요에 따라 개별 파일을 업로드 또는 다운로드할 수 있습니다. 게시 옵션은 전체 웹 응용 프로그램을 배포 합니다.

지정 된 원격 사이트에 필요한 모든 파일을 복사 하는 것 외에도 게시 옵션은 응용 프로그램을 명시적으로 컴파일합니다. 웹 응용 프로그램 프로젝트를 명시적으로 컴파일해야 하는 경우 웹 응용 프로그램 프로젝트에서 게시 옵션을 사용할 수 있습니다. 웹 사이트 프로젝트에도 게시 옵션을 사용할 수 있습니다. 배포 해야 하는 [*파일 결정*](determining-what-files-need-to-be-deployed-vb.md) 자습서에서 설명 했 듯이, 웹 사이트 프로젝트는 *사전 컴파일*이라고 하는 프로세스를 통해 명시적으로 컴파일할 수 있습니다. 이 자습서에서는 웹 응용 프로그램 프로젝트에서 게시 옵션을 사용 하는 방법을 집중적으로 설명 합니다. 이후 자습서에서는 미리 컴파일을 살펴보고,이 시점에서 웹 사이트 프로젝트와 함께 게시 옵션을 사용 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 게시 옵션은 웹 사이트 프로젝트와 웹 응용 프로그램 프로젝트 모두에 대해 Visual Studio에서 사용할 수 있지만, Visual Web Developer에서는 웹 응용 프로그램 프로젝트에 대 한 게시 옵션만 제공 합니다.

Publish 옵션을 사용 하 여 책 리뷰 응용 프로그램을 배포 하는 방법을 살펴보겠습니다. Visual Studio에서 BookReviewsWAP (웹 응용 프로그램 프로젝트)를 열어 시작 합니다. 게시 메뉴에서 Build BookReviewsWAP 프로젝트를 선택 합니다. 이렇게 하면 다른 구성 옵션 중에서 대상 위치를 묻는 대화 상자가 나타납니다 (그림 6 참조). 웹 사이트 복사 도구와 마찬가지로 로컬 폴더, IIS의 로컬 웹 사이트, FrontPage Server Extensions를 지 원하는 원격 웹 사이트 또는 FTP 서버 주소를 가리키는 위치를 입력할 수 있습니다. 원격 웹 서버의 파일을 배포 된 파일로 바꿀지 아니면 게시 하기 전에 원격 사이트의 모든 콘텐츠를 삭제할지를 선택할 수 있습니다. 복사할지 여부를 지정할 수도 있습니다.

- 프로젝트의 파일만 응용 프로그램을 실행 하는 데 필요 합니다 .이 경우 불필요 한 소스 코드 및 프로젝트 관련 파일이 생략 됩니다.
- 소스 코드 파일 및 Visual Studio 프로젝트 파일을 포함 하는 모든 프로젝트 파일 (예: 솔루션 파일)
- 소스 프로젝트 폴더의 모든 파일-프로젝트에 포함 되어 있는지 여부에 관계 없이 소스 프로젝트 폴더의 모든 파일을 복사 합니다.

또한 `App_Data` 폴더의 콘텐츠를 업로드 하는 옵션도 있습니다.

[대상 웹 사이트를 지정 ![](deploying-your-site-using-visual-studio-vb/_static/image17.png)](deploying-your-site-using-visual-studio-vb/_static/image16.png)

**그림 6**: 대상 웹 사이트 지정 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-visual-studio-vb/_static/image18.png))

책 리뷰 응용 프로그램의 경우 원격 사이트에는 웹 사이트 복사 도구를 통해 BookReviewsWSP 프로젝트를 복사할 때 배포 되는 파일이 포함 되어 있습니다. 따라서 모든 기존 콘텐츠를 삭제 하 여 Publish 옵션을 시작 해 보겠습니다. 또한 불필요 한 소스 코드 및 프로젝트 파일을 사용 하 여 프로덕션 환경에 복잡 한 것이 아니라 필요한 파일을 복사 하겠습니다. 이러한 옵션을 지정한 후 게시 단추를 클릭 합니다. 다음 몇 초 동안 Visual Studio는 필요한 파일을 대상 사이트에 배포 하 고 출력 창에 진행률을 표시 합니다.

그림 7에서는 게시 작업이 완료 된 후 FTP 사이트의 파일을 보여 줍니다. 태그 페이지와 필요한 서버 및 클라이언트 쪽 지원 파일만 업로드 됩니다.

[필요한 파일만 프로덕션 환경에 게시 된 ![](deploying-your-site-using-visual-studio-vb/_static/image20.png)](deploying-your-site-using-visual-studio-vb/_static/image19.png)

**그림 7**: 필요한 파일만 프로덕션 환경에 게시 ([전체 크기 이미지를 보려면 클릭](deploying-your-site-using-visual-studio-vb/_static/image21.png))

게시 옵션은 웹 사이트 복사 도구 보다 less 미묘한 도구입니다. 웹 사이트 복사 도구를 사용 하 여 로컬 및 원격 사이트에 있는 파일을 검사 하 고 어떻게 다른 지 확인할 수는 있지만 게시 옵션에서는 이러한 인터페이스를 제공 하지 않습니다. 또한 웹 사이트 복사 도구를 사용 하 여 일회용 변경을 수행 하 고 개별 파일을 업로드 하거나 삭제할 수 있습니다. 게시 옵션은 이러한 세부적인 제어를 허용 하지 않습니다. 대신 *전체* 응용 프로그램을 게시 합니다. 이 동작에는 장단점이 있습니다. Plus 쪽에서 게시 옵션을 사용할 때 중요 한 파일을 업로드 하는 것은 잊지 않습니다. 그러나 매우 큰 웹 사이트를 약간만 변경한 경우, 게시 옵션을 사용 하 여 해당 페이지를 업데이트할 수 없거나 수정 된 두 개를 업데이트할 수 없는 경우 어떻게 되나요? 대신 Visual Studio에서 전체 사이트를 배포 하는 동안 기다려야 합니다.

프로덕션 환경과 개발 환경 간에 콘텐츠가 다른 특정 파일이 있는 것이 일반적이 지 않습니다. 주요 예제는 응용 프로그램의 구성 파일인 `Web.config`입니다. 게시 옵션은 웹 응용 프로그램 파일을 무조건 복사 하기 때문에 프로덕션 환경의 사용자 지정 구성 파일을 개발 환경의 버전으로 덮어씁니다. 이후 자습서에서는이 항목에 대해 자세히 알아보고 이러한 차이점이 있는 경우 웹 응용 프로그램을 배포 하기 위한 팁을 제공 합니다.

## <a name="summary"></a>요약

웹 사이트를 배포 하려면 개발 환경에서 프로덕션 환경으로 필요한 파일을 복사 해야 합니다. 이전 자습서에서는 FileZilla와 같은 FTP 클라이언트를 사용 하 여 파일을 전송 하는 방법을 살펴보았습니다. 이 자습서에서는 웹 사이트 복사 도구 및 게시 옵션 이라는 두 가지 배포 도구를 Visual Studio에서 검사 했습니다. 웹 사이트 복사 도구는 로컬 컴퓨터의 파일과 지정 된 원격 컴퓨터를 사용 하 여 두 컴퓨터 간에 파일을 쉽게 업로드 하거나 다운로드할 수 있는 2 개의 빈 인터페이스가 있다는 점에서 FTP 클라이언트와 비슷합니다. 게시 옵션은 프로젝트를 명시적으로 컴파일한 다음 전체 응용 프로그램을 지정 된 대상에 배포 하는 더 많은 무딘 도구입니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [웹 사이트 복사 도구를 사용 하 여 웹 사이트 복사](https://msdn.microsoft.com/library/1cc82atw.aspx)
- [방법: 웹 사이트 복사 도구를 사용 하 여 웹 사이트 배포](../../../videos/how-do-i/how-do-i-deploy-a-web-site-using-the-copy-web-site-tool.md) (비디오)
- [방법: 웹 응용 프로그램 프로젝트 게시](https://msdn.microsoft.com/library/aa983453.aspx)
- [방법: 웹 사이트 게시](https://msdn.microsoft.com/library/20yh9f1b.aspx)
- [Visual Studio의 설치 및 배포 프로젝트](https://msdn.microsoft.com/library/wx3b589t.aspx)

> [!div class="step-by-step"]
> [이전](deploying-your-site-using-an-ftp-client-vb.md)
> [다음](common-configuration-differences-between-development-and-production-vb.md)
