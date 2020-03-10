---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
title: 개발 및 프로덕션 간의 일반적인 구성 차이점 (VB) | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서는 개발 환경에서 프로덕션 환경으로 모든 관련 파일을 복사 하 여 웹 사이트를 배포 했습니다. 그러나 ...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 548e75f6-4d6c-4cb4-8da8-417915eb8393
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
msc.type: authoredcontent
ms.openlocfilehash: cc65af6eb4fca8b3b805e11e26da468a958a4221
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513251"
---
# <a name="common-configuration-differences-between-development-and-production-vb"></a>개발 환경과 프로덕션 환경의 일반적인 구성 차이(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial05_ConfigDifferences_vb.pdf)

> 이전 자습서에서는 개발 환경에서 프로덕션 환경으로 모든 관련 파일을 복사 하 여 웹 사이트를 배포 했습니다. 그러나 환경 간의 구성 차이가 있는 것이 일반적이 지 않으므로 각 환경에 고유한 Web.config 파일이 있어야 합니다. 이 자습서에서는 일반적인 구성 차이점을 검사 하 고 별도의 구성 정보를 유지 관리 하기 위한 전략을 살펴봅니다.

## <a name="introduction"></a>소개

마지막 두 자습서에서는 간단한 웹 응용 프로그램을 배포 하는 방법을 살펴보았습니다. [*Ftp 클라이언트를 사용 하 여 사이트 배포*](deploying-your-site-using-an-ftp-client-vb.md) 자습서에서는 독립 실행형 ftp 클라이언트를 사용 하 여 개발 환경에서 프로덕션까지 필요한 파일을 복사 하는 방법을 살펴보았습니다. 앞의 자습서 인 [*Visual studio를 사용 하 여 사이트 배포*](deploying-your-site-using-visual-studio-vb.md)에서 visual Studio의 웹 사이트 복사 도구 및 게시 옵션을 사용 하 여 배포를 살펴보았습니다. 두 자습서에서 프로덕션 환경의 모든 파일은 개발 환경에서 파일의 복사본 이었습니다. 그러나 프로덕션 환경의 구성 파일은 개발 환경의 구성 파일에 따라 달라 집니다. 웹 응용 프로그램의 구성은 `Web.config` 파일에 저장 되며 일반적으로 데이터베이스, 웹, 전자 메일 서버 등의 외부 리소스에 대 한 정보를 포함 합니다. 또한 처리 되지 않은 예외가 발생할 때 수행할 작업 과정과 같은 특정 상황에서 응용 프로그램의 동작을 확인 합니다.

웹 응용 프로그램을 배포할 때 올바른 구성 정보를 프로덕션 환경에서 종료 하는 것이 중요 합니다. 대부분의 경우 개발 환경의 `Web.config` 파일을 프로덕션 환경에 그대로 복사할 수 없습니다. 대신, `Web.config`의 사용자 지정 버전을 프로덕션에 업로드 해야 합니다. 이 자습서에서는 몇 가지 일반적인 구성 차이점을 간략하게 검토 합니다. 또한 환경 간에 서로 다른 구성 정보를 유지 관리 하는 몇 가지 기술이 요약 되어 있습니다.

## <a name="typical-configuration-differences-between-the-development-and-production-environments"></a>개발 환경과 프로덕션 환경의 일반적인 구성 차이점

`Web.config` 파일에는 ASP.NET 응용 프로그램에 대 한 구성 정보 모음이 포함 되어 있습니다. 이러한 구성 정보 중 일부는 환경에 관계 없이 동일 합니다. 예를 들어 `Web.config` 파일의 `<authentication>` 및 `<authorization>` 요소에서 확인 되는 인증 설정 및 URL 권한 부여 규칙은 일반적으로 환경에 관계 없이 동일 합니다. 그러나 외부 리소스에 대 한 정보와 같은 기타 구성 정보는 일반적으로 환경에 따라 다릅니다.

데이터베이스 연결 문자열은 환경에 따라 달라 지는 구성 정보의 대표적인 예입니다. 웹 응용 프로그램이 데이터베이스 서버와 통신 하는 경우 먼저 연결을 설정 하 고 [연결 문자열](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)을 통해 수행 해야 합니다. 데이터베이스 연결 문자열을 웹 페이지나 데이터베이스에 연결 하는 코드에서 직접 하드 코드 할 수 있지만 연결 문자열 정보가 중앙의 단일 위치에 있도록 `Web.config`의 [`<connectionStrings>` 요소](https://msdn.microsoft.com/library/bf7sd233.aspx) 에 배치 하는 것이 가장 좋습니다. 프로덕션 환경에서 사용 하는 것 보다 개발 중에 다른 데이터베이스를 사용 하는 경우가 종종 있습니다. 따라서 연결 문자열 정보는 각 환경에 대해 고유 해야 합니다.

> [!NOTE]
> 이후 자습서에서는 데이터 기반 응용 프로그램을 배포 하는 방법에 대해 설명 합니다 .이 시점에서 데이터베이스 연결 문자열을 구성 파일에 저장 하는 방법에 대해 자세히 살펴보겠습니다.

개발 및 프로덕션 환경의 의도 된 동작은 크게 다릅니다. 개발 환경의 웹 응용 프로그램은 소규모 개발자 그룹에 의해 생성, 테스트 및 디버깅 됩니다. 프로덕션 환경에서는 여러 동시 사용자가 동일한 응용 프로그램을 방문 하 고 있습니다. ASP.NET에는 개발자가 응용 프로그램을 테스트 하 고 디버깅 하는 데 도움이 되는 다양 한 기능이 포함 되어 있지만 프로덕션 환경에서 성능 및 보안상의 이유로 이러한 기능을 사용 하지 않도록 설정 해야 합니다. 이러한 몇 가지 구성 설정을 살펴보겠습니다.

### <a name="configuration-settings-that-impact-performance"></a>성능에 영향을 주는 구성 설정

ASP.NET 페이지를 처음 방문 하는 경우 (또는 변경 후 처음으로) 해당 선언적 태그를 클래스로 변환 하 고이 클래스를 컴파일해야 합니다. 웹 응용 프로그램에서 자동 컴파일을 사용 하는 경우에도 페이지의 코드 숨김이 클래스를 컴파일해야 합니다. `Web.config` 파일의 [`<compilation>` 요소](https://msdn.microsoft.com/library/s10awwz0.aspx)를 통해 다양 한 컴파일 옵션을 구성할 수 있습니다.

Debug 특성은 `<compilation>` 요소에서 가장 중요 한 특성 중 하나입니다. `debug` 특성이 "true"로 설정 된 경우 컴파일된 어셈블리에는 Visual Studio에서 응용 프로그램을 디버그할 때 필요한 디버그 기호가 포함 됩니다. 그러나 디버그 기호는 어셈블리의 크기를 늘리고 코드를 실행할 때 추가 메모리 요구 사항을 적용 합니다. 또한 `debug` 특성이 "true"로 설정 된 경우 `WebResource.axd`에서 반환 되는 모든 콘텐츠가 캐시 되지 않습니다. 즉, 사용자가 페이지를 방문할 때마다 `WebResource.axd`에서 반환 된 정적 콘텐츠를 다시 다운로드 해야 합니다.

> [!NOTE]
> `WebResource.axd`는 서버 컨트롤에서 스크립트 파일, 이미지, CSS 파일 및 기타 콘텐츠와 같은 포함 된 리소스를 검색 하는 데 사용 하는 ASP.NET 2.0에 도입 된 기본 제공 HTTP 처리기입니다. `WebResource.axd` 작동 방법 및이를 사용 하 여 사용자 지정 서버 컨트롤에서 포함 된 리소스에 액세스 하는 방법에 대 한 자세한 내용은 [`WebResource.axd`를 사용 하 여 URL을 통해 포함 리소스에 액세스 ](http://aspnet.4guysfromrolla.com/articles/080906-1.aspx)를 참조 하세요.

`<compilation>` 요소의 `debug` 특성은 일반적으로 개발 환경에서 "true"로 설정 됩니다. 실제로이 특성은 웹 응용 프로그램을 디버깅 하기 위해 "true"로 설정 되어야 합니다. Visual Studio에서 ASP.NET 응용 프로그램을 디버깅 하려고 시도 하 고 `debug` 특성이 "false"로 설정 된 경우 Visual Studio는 `debug` 특성이 "true"로 설정 될 때까지 응용 프로그램을 디버그할 수 없다는 메시지를 표시 하 고이를 변경 하는 작업을 제공 합니다.

프로덕션 환경에서는 성능에 영향을 주므로 `debug` 특성을 "true"로 설정 **하면 안 됩니다** . 이 항목에 대 한 자세한 내용은 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 게시물, [프로덕션 ASP.NET 응용 프로그램 실행 안 함 `debug="true"` 사용 하도록 설정](https://weblogs.asp.net/scottgu/442448)을 참조 하세요.

### <a name="custom-errors-and-tracing"></a>사용자 지정 오류 및 추적

ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생 하면 다음 세 가지 중 하나가 발생 하는 시점까지 런타임에 버블링 됩니다.

- 일반 런타임 오류 메시지가 표시 됩니다. 이 페이지에서는 런타임 오류가 발생 했음을 사용자에 게 알려 주지만 오류에 대 한 세부 정보는 제공 하지 않습니다.
- 예외 정보 메시지가 표시 됩니다. 여기에는 방금 throw 된 예외에 대 한 정보가 포함 됩니다.
- 사용자 지정 오류 페이지가 표시 됩니다 .이 페이지는 사용자가 원하는 메시지를 표시 하는 ASP.NET 페이지입니다.

처리 되지 않은 예외가 발생 하는 경우는 `Web.config` 파일의 [`<customErrors>` 섹션](https://msdn.microsoft.com/library/h0hfz6fc.aspx)에 따라 다릅니다.

응용 프로그램을 개발 하 고 테스트할 때 브라우저에서 예외에 대 한 세부 정보를 확인 하는 데 도움이 됩니다. 그러나 프로덕션 환경에서 응용 프로그램에 예외 정보를 표시 하는 것은 보안상 위험할 수 있습니다. 또한 웹 사이트를 전문적 unflattering. 이상적으로, 처리 되지 않은 예외가 발생 하는 경우 개발 환경의 웹 응용 프로그램은 예외의 세부 정보를 표시 하 고, 프로덕션의 동일한 응용 프로그램은 사용자 지정 오류 페이지를 표시 합니다.

> [!NOTE]
> 기본 `<customErrors>` 섹션 설정은 localhost를 통해 페이지를 방문 하는 경우에만 예외 정보 메시지를 표시 하 고, 그렇지 않으면 일반 런타임 오류 페이지를 표시 합니다. 이는 적합 하지 않지만 기본 동작이 로컬이 아닌 방문자에 게 예외 정보를 노출 하지 않는다는 것을 알아야 합니다. 이후 자습서에서는 `<customErrors>` 섹션을 자세히 살펴보고 프로덕션에서 오류가 발생할 때 사용자 지정 오류 페이지를 표시 하는 방법을 보여 줍니다.

개발 중에 유용한 또 다른 ASP.NET 기능은 추적입니다. 추적 (설정 된 경우)은 들어오는 각 요청에 대 한 정보를 기록 하 고 최근 요청 정보를 볼 수 있는 특수 웹 페이지 `Trace.axd`를 제공 합니다. `Web.config`에서 [`<trace>` 요소](https://msdn.microsoft.com/library/6915t83k.aspx) 를 통해 추적을 설정 하 고 구성할 수 있습니다.

추적을 사용 하도록 설정 하면 프로덕션 환경에서 사용 하지 않도록 설정 되었는지 확인 합니다. 추적 정보에는 쿠키, 세션 데이터 및 기타 잠재적으로 중요 한 정보가 포함 되어 있으므로 프로덕션에서 추적을 사용 하지 않도록 설정 하는 것이 중요 합니다. 이는 기본적으로 추적 기능이 해제 되어 있고 localhost를 통해서만 `Trace.axd` 파일에 액세스할 수 있다는 것입니다. 개발에서 이러한 기본 설정을 변경 하는 경우 프로덕션 환경에서 다시 설정 되었는지 확인 합니다.

## <a name="techniques-for-maintaining-separate-configuration-information"></a>별도의 구성 정보를 유지 관리 하는 기술

개발 및 프로덕션 환경에서 다양 한 구성 설정을 유지 하면 배포 프로세스를 복잡 하 게 됩니다. 이전 두 자습서에서 배포 프로세스는 필요한 모든 파일을 개발 환경에서 프로덕션 환경으로 복사 하는 과정을 포함 하지만이 접근 방식은 두 환경에서 구성 정보가 동일한 경우에만 작동 합니다. 다양 한 구성 정보를 사용 하 여 응용 프로그램을 배포 하는 다양 한 기술이 있습니다. 호스팅된 웹 응용 프로그램에 대해 이러한 옵션 중 일부를 카탈로그로 만들어 보겠습니다.

### <a name="manually-deploying-the-production-environment-configuration-file"></a>프로덕션 환경 구성 파일 수동 배포

가장 간단한 방법은 두 가지 버전의 `Web.config` 파일을 유지 관리 하는 것입니다. 하나는 개발 환경을 위한 것이 고 다른 하나는 프로덕션 환경을 위한 것입니다. 프로덕션에 사이트를 배포 하려면 `Web.config` 파일을 *제외 하* 고 개발 환경의 프로덕션 서버에 모든 파일을 복사 해야 합니다. 대신 프로덕션 환경 관련 `Web.config` 파일이 프로덕션 환경에 복사 됩니다.

이 방법은 매우 정교 하지 않지만 구성 정보는 자주 변경 되지 않으므로 쉽게 구현할 수 있습니다. 단일 웹 서버에서 호스트 되 고 해당 구성 정보가 드물게 변경 되는 소규모 개발 팀이 있는 응용 프로그램에 가장 적합 합니다. 독립 실행형 FTP 클라이언트를 사용 하 여 응용 프로그램 파일을 수동으로 배포할 때에는이 기능을 사용 하는 것이 가장 좋습니다. Visual Studio의 웹 사이트 복사 도구 또는 게시 옵션을 사용 하는 경우 배포 하기 전에 먼저 배포 관련 `Web.config` 파일을 프로덕션 관련 파일로 바꾼 다음 배포가 완료 된 후 다시 교환 해야 합니다.

### <a name="change-the-configuration-during-the-build-or-deployment-process"></a>빌드 또는 배포 프로세스 중에 구성 변경

지금까지 논의를 통해 임시 빌드 및 배포 프로세스를 가정 했습니다. 많은 대규모 소프트웨어 프로젝트에는 오픈 소스, 홈 증가 또는 타사 도구를 사용 하는 보다 공식화 된 프로세스가 있습니다. 이러한 프로젝트의 경우 프로덕션에 푸시 되기 전에 구성 정보를 적절 하 게 수정 하도록 빌드 또는 배포 프로세스를 사용자 지정할 수 있습니다. [MSBuild](http://en.wikipedia.org/wiki/MSBuild), [NAnt](http://nant.sourceforge.net/)또는 다른 빌드 도구를 사용 하 여 웹 응용 프로그램을 빌드하는 경우 프로덕션 관련 설정을 포함 하도록 `Web.config` 파일을 수정 하는 빌드 단계를 추가할 수 있습니다. 또는 배포 워크플로를 통해 프로그래밍 방식으로 소스 제어 서버에 연결 하 고 적절 한 `Web.config` 파일을 검색할 수 있습니다.

프로덕션에 적절 한 구성 정보를 얻는 실제 접근 방식은 도구와 워크플로에 따라 크게 달라 집니다. 이와 같이이 항목에 대해 자세히 설명 하지 않습니다. MSBuild 또는 NAnt와 같은 인기 있는 빌드 도구를 사용 하는 경우 웹 검색을 통해 이러한 도구와 관련 된 배포 문서와 자습서를 찾을 수 있습니다.

### <a name="managing-configuration-differences-via-the-web-deployment-project-add-in"></a>웹 배포 프로젝트 추가 기능을 통한 구성 차이 관리

2006에서 Microsoft는 Visual Studio 2005 용 웹 개발 프로젝트 추가 기능을 릴리스 했습니다. Visual Studio 2008에 대 한 추가 기능이 2008에서 출시 되었습니다. 이 추가 기능을 사용 하면 ASP.NET 개발자가 웹 응용 프로그램 프로젝트와 함께 별도의 웹 배포 프로젝트를 만들 수 있습니다 .이 프로젝트는 빌드할 때 명시적으로 웹 응용 프로그램을 컴파일하고 로컬 출력 디렉터리에 배포할 파일을 복사 합니다. 웹 응용 프로그램 프로젝트는 내부적으로 MSBuild를 사용 합니다.

기본적으로 개발 환경의 `Web.config` 파일은 출력 디렉터리에 복사 되지만 웹 배포 프로젝트를 설정 하 여 다음을 사용자 지정할 수 있습니다.

다음과 같은 방법으로이 디렉터리에 복사 되는 구성 정보입니다.

- `Web.config` 파일 섹션 대체를 통해 바꿀 섹션과 대체 텍스트를 포함 하는 XML 파일을 지정 합니다.
- 외부 구성 소스 파일에 대 한 경로를 제공 합니다. 이 옵션을 선택 하면 웹 배포 프로젝트는 특정 `Web.config` 파일을 개발 환경에서 사용 되는 `Web.config` 파일이 아닌 출력 디렉터리에 복사 합니다.
- 웹 배포 프로젝트에 사용 되는 MSBuild 파일에 사용자 지정 규칙을 추가 합니다.

웹 응용 프로그램을 배포 하려면 웹 배포 프로젝트를 빌드한 다음 프로젝트의 출력 폴더에서 프로덕션 환경으로 파일을 복사 합니다.

웹 배포 프로젝트를 사용 하는 방법에 대 한 자세한 내용은 [MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx)의 4 월 2007 문제에서 [이 웹 배포 프로젝트](https://msdn.microsoft.com/magazine/cc163448.aspx) 를 확인 하거나이 자습서의 끝에 있는 추가 정보 섹션의 링크를 참조 하세요.

> [!NOTE]
> 웹 배포 프로젝트가 Visual Studio 추가 기능으로 구현 되 고 Visual Studio Express 버전 (Visual Web Developer 포함)이 추가 기능을 지원 하지 않기 때문에 Visual Web Developer에서 웹 배포 프로젝트를 사용할 수 없습니다.

## <a name="summary"></a>요약

개발 중인 웹 응용 프로그램의 외부 리소스 및 동작은 일반적으로 동일한 응용 프로그램이 프로덕션 환경에 있는 경우와 다릅니다. 예를 들어 데이터베이스 연결 문자열, 컴파일 옵션 및 처리 되지 않은 예외가 발생 하는 동작은 일반적으로 환경 마다 다릅니다. 배포 프로세스는 이러한 차이를 수용 해야 합니다. 이 자습서에서 설명한 대로 가장 간단한 방법은 대체 구성 파일을 프로덕션 환경에 수동으로 복사 하는 것입니다. 웹 배포 프로젝트 추가 기능을 사용 하거나 이러한 사용자 지정을 수용할 수 있는 보다 공식화 된 빌드 또는 배포 프로세스를 사용 하는 경우 보다 세련 된 솔루션을 사용할 수 있습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [연결 문자열 설명](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)
- [데이터베이스 연결 문자열 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [`debug="true"` 사용 하도록 설정 된 프로덕션 ASP.NET 응용 프로그램 실행 안 함](https://weblogs.asp.net/scottgu/Don_1920_t-run-production-ASP.NET-Applications-with-debug_3D001D20_true_1D20_-enabled)
- [처리 되지 않은 예외에 대 한 적절 한 응답-사용자에 게 친숙 한 오류 페이지 표시](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [방법: Visual Studio 2008 웹 배포 프로젝트 사용](../../../videos/how-do-i/how-do-i-use-a-visual-studio-2008-web-deployment-project.md)
- [데이터베이스 배포 시 키 구성 설정](http://aspnet.4guysfromrolla.com/articles/121008-1.aspx)
- [Visual studio 2008 웹 배포 프로젝트 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) | [Visual Studio 2005 웹 배포 프로젝트 다운로드](https://download.microsoft.com/download/9/4/9/9496adc4-574e-4043-bb70-bc841e27f13c/WebDeploymentSetup.msi)
- Vs [2008 웹 배포 프로젝트](https://weblogs.asp.net/scottgu/archive/2005/11/06/429723.aspx) | [Vs 2008 웹 배포 프로젝트 지원 출시](https://weblogs.asp.net/scottgu/archive/2008/01/28/vs-2008-web-deployment-project-support-released.aspx)
- [웹 배포 프로젝트](https://msdn.microsoft.com/magazine/cc163448.aspx)

> [!div class="step-by-step"]
> [이전](deploying-your-site-using-visual-studio-vb.md)
> [다음](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
