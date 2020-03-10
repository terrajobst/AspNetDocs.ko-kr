---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: 웹 배포에 적합 한 접근 방식 선택 | Microsoft Docs
author: jrjlee
description: 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상으로 작업 하는 경우 다음을 수행 하는 데 사용할 수 있는 세 가지 주요 방법이 있습니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13f784dd8e6404806104d56b026b3c41ca178892
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441425"
---
# <a name="choosing-the-right-approach-to-web-deployment"></a>웹 배포에 적합한 접근 방식 선택

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상으로 작업 하는 경우 패키지 된 웹 응용 프로그램을 웹 서버에 가져오는 데 사용할 수 있는 세 가지 주요 방법이 있습니다. 다음 작업 중 하나를 수행할 수 있습니다.
> 
> - 대상 서버에서 *웹 Deployment Agent 서비스* ("원격 에이전트" 라고도 함)를 대상으로 지정 하 여 원격 위치에서 응용 프로그램을 배포 합니다.
> - 주문형 웹 배포 ("임시 에이전트" 라고도 함)를 사용 하 여 원격 위치에서 응용 프로그램을 배포 합니다.
> - 대상 서버에서 *IIS 웹 배포 처리기* 를 대상으로 지정 하 여 원격 위치에서 응용 프로그램을 배포 합니다.
> - 웹 패키지를 대상 서버에 수동으로 복사 하 여 IIS 관리자를 통해 가져오는 방법으로 응용 프로그램을 배포 합니다.
> 
> 대상 웹 서버를 구성 하는 방법은 사용 하려는 배포 방법에 따라 달라 집니다. 이 항목은 배포에 적합 한 방법을 결정 하는 데 도움이 됩니다.

이 표에서는 각 배포 방법의 주요 장점과 단점을 가장 일반적으로 각 접근 방식에 맞는 시나리오와 함께 보여 줍니다.

| 접근 방식 | 장점 | 단점 | 일반적인 시나리오 |
| --- | --- | --- | --- |
| 원격 에이전트 | 설정 하는 것이 쉽습니다. 웹 응용 프로그램 및 콘텐츠를 정기적으로 업데이트 하는 데 적합 합니다. | 사용자는 대상 서버의 관리자 여야 합니다. 사용자는 대체 자격 증명을 제공할 수 없습니다. | 개발 환경. 테스트 환경. |
| 임시 에이전트 | 대상 컴퓨터에 웹 배포를 설치할 필요가 없습니다. 웹 배포의 최신 버전이 자동으로 사용 됩니다. | 사용자는 대상 서버의 관리자 여야 합니다. 사용자는 대체 자격 증명을 제공할 수 없습니다. | 개발 환경. 테스트 환경. |
| 웹 배포 처리기 | 관리자가 아닌 사용자는 콘텐츠를 배포할 수 있습니다. 웹 응용 프로그램 및 콘텐츠를 정기적으로 업데이트 하는 데 적합 합니다. | 설정 하는 것은 훨씬 더 복잡 합니다. | 스테이징 환경. 인트라넷 프로덕션 환경. 호스팅된 환경. |
| 오프 라인 배포 | 설정 하기가 매우 쉽습니다. 격리 된 환경에 적합 합니다. | 서버 관리자는 매번 웹 패키지를 수동으로 복사 하 여 가져와야 합니다. | 인터넷 연결 프로덕션 환경. 격리 된 네트워크 환경. |

## <a name="using-the-remote-agent"></a>원격 에이전트 사용

대상 서버의 기본 설정을 사용 하 여 웹 배포를 설치 하는 경우 웹 Deployment Agent 서비스 ("원격 에이전트")가 자동으로 설치 되 고 시작 됩니다. 기본적으로 원격 에이전트는 다음 주소에 HTTP 끝점을 노출 합니다.

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]

> [!NOTE]
> [*Server*]를 웹 서버의 컴퓨터 이름, 웹 서버에 대 한 IP 주소 또는 웹 서버로 확인 되는 호스트 이름으로 바꿀 수 있습니다.

서버 관리자는이 끝점 주소를 지정 하 여 개발자 컴퓨터 또는 빌드 서버와 같은 원격 위치에서 웹 패키지를 배포할 수 있습니다. 예를 들어 Fabrikam, i n c .의 Matt Hink에서 개발자 컴퓨터에 동료 관리자. Mvc 웹 응용 프로그램 프로젝트를 빌드 했다고 가정 합니다. 빌드 프로세스는 패키지를 설치 하는 데 필요한 웹 배포 명령을 포함 하는 *.deploy. .cmd* 파일과 함께 웹 패키지를 생성 합니다. Matt가 TESTWEB1 서버에서 서버 관리자 인 경우 개발자 컴퓨터에서이 명령을 실행 하 여 테스트 웹 서버에 웹 응용 프로그램을 배포할 수 있습니다.

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]

실제로 웹 배포 실행 파일은 컴퓨터 이름을 제공 하는 경우 원격 에이전트의 끝점 주소를 유추할 수 있으므로 Matt는 다음과 같이 입력 해야 합니다.

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]

> [!NOTE]
> 명령줄 구문에 대 한 자세한 내용과 *. .cmd* 파일을 배포 하는 방법에 대 한 웹 배포 자세한 내용은 [방법: Deploy. .Cmd 파일을 사용 하 여 배포 패키지 설치](https://msdn.microsoft.com/library/ff356104.aspx)를 참조 하세요.

원격 에이전트는 원격 위치에서 콘텐츠를 배포 하는 간단한 방법을 제공 하며이 접근 방식은 한 번의 클릭으로 또는 자동화 된 배포에서 제대로 작동할 수 있습니다. 그러나 배포 명령을 실행 하는 사용자는 도메인 관리자 이거나 대상 서버에서 로컬 관리자 그룹의 구성원 이어야 합니다. 또한 원격 에이전트가 기본 인증을 지원 하지 않으므로 명령줄에서 대체 자격 증명을 전달할 수 없습니다.

원격 에이전트는 개발 또는 테스트 시나리오에서 배포 하는 데 유용한 방법을 제공 합니다 .이는 개발자가 테스트 서버 환경에 대해 전체 관리자 제어를 사용 하는 것이 일반적이 지 않으며 일반적으로 응용 프로그램을 다시 빌드하고 다시 배포 하는 것입니다. 자주. 그러나이 방법은 일반적으로 스테이징 또는 프로덕션 환경에서 허용 되는 수준이 낮습니다.

원격 에이전트 방법을 사용 하는 시나리오의 종단 간 예제는 [시나리오: 웹 배포용 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)을 참조 하세요.

## <a name="using-the-temp-agent"></a>임시 에이전트 사용

배포에 대 한 임시 에이전트 접근 방식은 원격 에이전트 방법과 유사 합니다. 그러나 원격 에이전트 방법과 달리 대상 웹 서버에 웹 배포를 설치할 필요가 없습니다. 대신 배포를 수행 하는 경우 웹 배포은 대상 서버에 임시 버전의 웹 배포 에이전트 서비스를 설치 하 고이를 사용 하 여 IIS에 콘텐츠를 배포 합니다. 배포가 완료 되 면 모든 임시 파일이 제거 됩니다.

임시 에이전트 공급자 설정을 사용 하려면 배포 명령에 **/g** 플래그를 추가 합니다.

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]

> [!NOTE]
> 서비스가 실행 되 고 있지 않은 경우에도 대상 컴퓨터에 웹 배포 에이전트 서비스가 설치 되어 있으면 임시 에이전트를 사용할 수 없습니다.

이 방법의 장점은 대상 서버에 웹 배포 설치를 유지 관리할 필요가 없다는 것입니다. 또한 원본 컴퓨터와 대상 컴퓨터의 웹 배포 동일한 버전의를 실행 하 고 있는지 확인 하지 않아도 됩니다. 그러나이 접근 방식은 원격 에이전트와 동일한 보안 주체 제한이 적용 됩니다. 즉, 콘텐츠를 배포 하기 위해 대상 서버에서 로컬 관리자 여야 하며 NTLM 인증만 지원 됩니다. 또한 임시 에이전트 방법을 사용 하려면 대상 환경에 대해 훨씬 더 많은 초기 구성이 필요 합니다.

임시 에이전트 사용에 대 한 자세한 내용은 [방법: 배포 .Cmd 파일을 사용 하 여 배포 패키지 설치](https://msdn.microsoft.com/library/ff356104.aspx) 및 [요청 시 웹 배포](https://technet.microsoft.com/library/ee517345(WS.10).aspx)를 참조 하세요.

## <a name="using-the-web-deploy-handler"></a>웹 배포 처리기 사용

IIS 7 이상에서는 웹 배포 IIS 웹 배포 처리기를 통한 대체 배포 방법을 제공 합니다. 웹 배포 처리기는 사용자가 원격 위치에서 IIS 웹 사이트를 관리할 수 있도록 설계 된 IIS WMSvc (웹 관리 서비스)와 긴밀 하 게 통합 됩니다.

기본적으로 원격 에이전트는 다음 주소에 HTTP 끝점을 노출 합니다.

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]

> [!NOTE]
> [*Server*]를 웹 서버의 컴퓨터 이름, 웹 서버에 대 한 IP 주소 또는 웹 서버로 확인 되는 호스트 이름으로 바꿀 수 있습니다.

원격 에이전트 및 임시 에이전트에 대 한 웹 배포 처리기의 가장 큰 장점은 관리자가 아닌 사용자가 특정 IIS 웹 사이트에 응용 프로그램 및 콘텐츠를 배포할 수 있도록 IIS를 구성할 수 있다는 것입니다. 또한 웹 배포 처리기는 기본 인증을 지원 하므로 웹 배포 명령에서 매개 변수로 대체 자격 증명을 제공할 수 있습니다. 주요 단점은 웹 배포 처리기를 설정 하 고 구성 하는 것이 훨씬 복잡 하다는 것입니다.

비관리자 사용자의 경우 웹 관리 서비스 (WMSvc)를 사용 하면 사용자가 서버 수준 연결이 아닌 사이트 수준 연결을 사용 하 여 IIS에 연결할 수 있습니다. 특정 사이트에 액세스 하려면 끝점 주소에 사이트별 쿼리 문자열을 포함 하면 됩니다.

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]

예를 들어 빌드 프로세스가 성공적으로 완료 된 후에 웹 응용 프로그램을 스테이징 환경에 자동으로 배포 하도록 구성 되어 있다고 가정 합니다. 원격 에이전트 방법을 사용 하는 경우 대상 서버에서 빌드 프로세스 id를 관리자로 설정 해야 합니다. 이와 대조적으로 웹 배포 처리기 방법을 사용 하면&#x2014;**관리자가 아닌 사용자에** 게 특정 IIS 웹 사이트에 대&#x2014;한 사용 권한만 부여할 수 있으며,이 경우 빌드 프로세스는 이러한 자격 증명을 제공 하 여 웹 패키지를 배포할 수 있습니다.

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]

> [!NOTE]
> 웹 배포 명령줄 작업 및 구문에 대 한 자세한 내용은 [웹 배포 명령줄 참조](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)를 참조 하세요. *.Deploy* 파일을 사용 하는 방법에 대 한 자세한 내용은 [방법: 배포 파일을 사용 하 여 배포 패키지 설치](https://msdn.microsoft.com/library/ff356104.aspx)를 참조 하세요.

웹 배포 처리기는 스테이징 환경, 호스팅된 환경 및 인트라넷 기반 프로덕션 환경에서 배포 하는 데 유용한 방법을 제공 합니다 .이 환경에서는 서버에 대 한 원격 액세스를 사용할 수 있지만 관리자 자격 증명은 사용할 수 없습니다.

웹 배포 처리기 방법을 사용 하는 시나리오의 종단 간 예제는 [시나리오: 웹 배포용 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)을 참조 하세요.

## <a name="using-offline-deployment"></a>오프 라인 배포 사용

경우에 따라 원격 위치에서 IIS 웹 사이트에 응용 프로그램 및 콘텐츠를 배포 하는 것은 불가능 합니다. 예를 들어 원본 및 대상 컴퓨터가 격리 된 네트워크나 네트워크 세그먼트에 있거나 방화벽 정책에서 원격 액세스를 허용 하지 않을 수 있습니다.

이와 같은 시나리오에서는 웹 배포의 패키징 및 게시 기능을 계속 사용할 수 있습니다. 원격 위치에서는 사용할 수 없습니다. 대신 대상 서버의 관리자가 웹 패키지를 서버에 복사 하 고 IIS 관리자를 통해 가져와야 합니다.

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

오프 라인 배포 방식은 일반적으로 경계 네트워크의 서버가 내부 네트워크의 컴퓨터와 제한 된 연결을 가질 수 있는 인터넷 연결 프로덕션 환경에서 유용 합니다.

오프 라인 배포 방법을 사용 하는 시나리오의 종단 간 예제는 [시나리오: 웹 배포용 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)을 참조 하세요.

## <a name="further-reading"></a>추가 참고 자료

웹 배포 명령줄 작업 및 구문에 대 한 자세한 내용은 [웹 배포 명령줄 참조](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)를 참조 하세요. *.Deploy* 파일을 사용 하는 방법에 대 한 자세한 내용은 [방법: 배포 파일을 사용 하 여 배포 패키지 설치](https://msdn.microsoft.com/library/ff356104.aspx)를 참조 하세요.

원격 컴퓨터에서 웹 패키지를 배포할 수 있는 다양 한 방법에 대 한 일반적인 지침은 원격 [으로 웹 배포 사용](https://technet.microsoft.com/library/ee461175(WS.10).aspx)을 참조 하세요. 요청 시 웹 배포를 사용 하는 방법에 대 한 자세한 내용은 [주문형 웹 배포](https://technet.microsoft.com/library/ee517345(WS.10).aspx)을 참조 하세요.

> [!div class="step-by-step"]
> [이전](configuring-server-environments-for-web-deployment.md)
> [다음](scenario-configuring-a-test-environment-for-web-deployment.md)
