---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
title: 웹 패키지 배포에 대 한 매개 변수 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 인터넷 정보 서비스 (IIS) 웹 응용 프로그램 이름, 연결 문자열 및 서비스 끝점과 같은 매개 변수 값을 설정 하는 방법에 대해 설명,...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 37947d79-ab1e-4ba9-9017-52e7a2757414
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
msc.type: authoredcontent
ms.openlocfilehash: f04ace98d81a33053b10cab7e40dbd75a6c0992c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438401"
---
# <a name="configuring-parameters-for-web-package-deployment"></a>웹 패키지 배포용 매개 변수 구성

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 원격 IIS 웹 서버에 웹 패키지를 배포할 때 인터넷 정보 서비스 (IIS) 웹 응용 프로그램 이름, 연결 문자열 및 서비스 끝점과 같은 매개 변수 값을 설정 하는 방법에 대해 설명 합니다.

웹 응용 프로그램 프로젝트를 빌드하면 빌드 및 패키징 프로세스에서 다음과 같은 세 가지 주요 파일을 생성 합니다.

- *[프로젝트 이름] .zip* 파일입니다. 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지입니다. 이 패키지에는 원격 IIS 웹 서버에서 웹 응용 프로그램을 다시 만드는 데 필요한 모든 어셈블리, 파일, 데이터베이스 스크립트 및 리소스가 포함 되어 있습니다.
- *[프로젝트 이름]. .cmd* 파일을 배포 합니다. 여기에는 원격 IIS 웹 서버에 웹 배포 패키지를 게시 하는 매개 변수가 있는 웹 배포 (Msdeploy.exe) 명령이 포함 됩니다.
- *[프로젝트 이름]입니다. SetParameters .xml* 파일. 이렇게 하면 Msdeploy.exe 명령에 매개 변수 값 집합이 제공 됩니다. 이 파일의 값을 업데이트 하 고 웹 패키지를 배포할 때 명령줄 매개 변수로 웹 배포에 전달할 수 있습니다.

> [!NOTE]
> 빌드 및 패키징 프로세스에 대 한 자세한 내용은 [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)을 참조 하세요.

*Setparameters .xml* 파일은 웹 응용 프로그램 프로젝트 파일 및 프로젝트 내 모든 구성 파일에서 동적으로 생성 됩니다. 프로젝트를 빌드하고 패키지할 때 WPP (웹 게시 파이프라인)는 대상 IIS 웹 응용 프로그램 및 모든 데이터베이스 연결 문자열과 같은 배포 환경 간에 변경 될 가능성이 높은 많은 변수를 자동으로 검색 합니다. 이러한 값은 웹 배포 패키지에서 자동으로 매개 변수화 되 고 *Setparameters .xml* 파일에 추가 됩니다. 예를 *들어 웹 응용* 프로그램 프로젝트의 web.config 파일에 연결 문자열을 추가 하면 빌드 프로세스에서이 변경 내용을 검색 하 고 그에 따라 *setparameters .xml* 파일에 항목을 추가 합니다.

많은 경우에는이 자동 매개 변수화로 충분 합니다. 그러나 사용자가 응용 프로그램 설정 또는 서비스 끝점 Url과 같은 배포 환경 간에 다른 설정을 변경 해야 하는 경우에는 배포 패키지에서 이러한 값을 매개 변수화 하 고 해당 항목을 *Setparameters .xml* 파일에 추가 하도록 WPP에 지시 해야 합니다. 다음 섹션에서는이 작업을 수행 하는 방법을 설명 합니다.

### <a name="automatic-parameterization"></a>자동 매개 변수화

웹 응용 프로그램을 빌드하고 패키지할 때 WPP는 다음과 같은 작업을 자동으로 매개 변수화 합니다.

- 대상 IIS 웹 응용 프로그램 경로 및 이름입니다.
- *Web.config 파일에* 있는 모든 연결 문자열
- 프로젝트 속성 페이지의 **SQL 패키지 및 게시** 탭에 추가 하는 모든 데이터베이스에 대 한 연결 문자열입니다.

예를 들어 매개 변수화 프로세스를 사용 하지 않고 [Contact manager](the-contact-manager-solution.md) 샘플 솔루션을 빌드하고 패키지 하는 경우, WPP는 다음과 같은 지 *속성과 파일을 생성 합니다.*

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample1.xml)]

이 경우 다음과 같습니다.

- **Iis 웹 응용 프로그램 이름** 매개 변수는 웹 응용 프로그램을 배포 하려는 iis 경로입니다. 기본값은 프로젝트 속성 페이지의 **패키지 및 게시 웹** 페이지에서 가져옵니다.
- **Applicationservices-Web.config 연결 문자열** 매개 변수가 *Web.config 파일의* **connectionStrings/add** 요소에서 생성 되었습니다. 응용 프로그램에서 멤버 자격 데이터베이스에 연결 하는 데 사용 해야 하는 연결 문자열을 나타냅니다. 여기에서 제공 하는 값은 배포 된 *web.config* 파일로 대체 됩니다. 기본값은 배포 전 *web.config* 파일에서 가져옵니다.

또한 WPP는 생성 하는 배포 패키지에서 이러한 속성을 매개 변수화 합니다. 배포 패키지를 설치할 때 이러한 속성에 대 한 값을 제공할 수 있습니다. [수동으로 웹 패키지 설치](manually-installing-web-packages.md)에 설명 된 대로 IIS 관리자를 통해 패키지를 수동으로 설치 하는 경우 설치 마법사에서 매개 변수에 대 한 값을 제공 하 라는 메시지를 표시 합니다. [웹 패키지 배포](deploying-web-packages.md)에 설명 된 대로 *. deploy .cmd* 파일을 사용 하 여 패키지를 원격으로 설치 하는 경우에는 웹 배포이 *setparameters .xml* 파일을 확인 하 여 매개 변수 값을 제공 합니다. *Setparameters .xml* 파일의 값을 수동으로 편집 하거나 자동화 된 빌드 및 배포 프로세스의 일부로 파일을 사용자 지정할 수 있습니다. 이 프로세스에 대해서는이 항목의 뒷부분에서 자세히 설명 합니다.

### <a name="custom-parameterization"></a>사용자 지정 매개 변수화

더 복잡 한 배포 시나리오에서는 프로젝트를 배포 하기 전에 추가 속성을 매개 변수화 하는 것이 좋습니다. 일반적으로 대상 환경 마다 다를 수 있는 속성 및 설정을 매개 변수화 해야 합니다. 여기에는 다음이 포함 될 수 있습니다.

- *Web.config 파일의* 서비스 끝점입니다.
- *Web.config 파일의* 응용 프로그램 설정입니다.
- 사용자에 게 지정 하 라는 메시지를 표시 하려는 다른 모든 선언적 속성

이러한 속성을 매개 변수화 하는 가장 쉬운 방법은 웹 응용 프로그램 프로젝트의 루트 폴더에 *parameters .xml* 파일을 추가 하는 것입니다. 예를 들어 Contact manager 솔루션에서 파일 관리자 프로젝트는 루트 폴더에 *parameters .xml* 파일을 포함 합니다.

![](configuring-parameters-for-web-package-deployment/_static/image1.png)

이 파일을 열면 단일 **매개 변수** 항목이 포함 된 것을 볼 수 있습니다. 이 항목에서는 XPath (XML Path Language) 쿼리를 사용 하 여 web.config 파일에서 *웹* 서비스 WINDOWS COMMUNICATION FOUNDATION (WCF) 서비스의 끝점 URL을 찾고 매개 변수화 합니다.

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample2.xml)]

배포 패키지에서 끝점 URL을 매개 변수화 하는 것 외에도, WPP는 배포 패키지와 함께 생성 되는 *Setparameters .xml* 파일에 해당 항목을 추가 합니다.

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample3.xml)]

배포 패키지를 수동으로 설치 하는 경우 IIS 관리자는 자동으로 매개 변수화 된 속성과 함께 서비스 끝점 주소를 묻는 메시지를 표시 합니다. *.Deploy* 파일을 실행 하 여 배포 패키지를 설치 하는 경우 *setparameters .xml* 파일을 편집 하 여 자동으로 매개 변수화 된 속성에 대 한 값과 함께 서비스 끝점 주소에 대 한 값을 제공할 수 있습니다.

*매개 변수 .xml* 파일을 만드는 방법에 대 한 자세한 내용은 [방법: 패키지를 설치할 때 매개 변수를 사용 하 여 배포 설정 구성](https://msdn.microsoft.com/library/ff398068.aspx)을 참조 하세요. **Web.config 파일 설정에 대 한 배포 매개 변수를 사용 하도록** 명명 된 프로시저는 단계별 지침을 제공 합니다.

## <a name="modifying-the-setparametersxml-file"></a>SetParameters .xml 파일 수정

*.Deploy* 파일을 실행 하거나 명령줄&#x2014;에서 msdeploy.exe를 실행 하 여 웹 응용 프로그램 패키지를 수동으로&#x2014;배포 하려는 경우 배포 하기 전에 *setparameters .xml* 파일을 수동으로 편집 하는 것은 아무 작업도 수행 하지 않습니다. 그러나 엔터프라이즈급 솔루션에서 작업 하는 경우에는 더 크고 자동화 된 빌드 및 배포 프로세스의 일부로 웹 응용 프로그램 패키지를 배포 해야 할 수 있습니다. 이 시나리오에서는 *Setparameters .xml* 파일을 수정 하는 Microsoft Build Engine (MSBuild)가 필요 합니다. MSBuild **XmlPoke** 작업을 사용 하 여이 작업을 수행할 수 있습니다.

[Contact Manager 샘플 솔루션](the-contact-manager-solution.md) 은이 프로세스를 보여 줍니다. 다음 코드 예제는이 예제와 관련 된 세부 정보만 표시 하도록 편집 되었습니다.

> [!NOTE]
> 샘플 솔루션의 프로젝트 파일 모델에 대 한 광범위 한 개요와 일반적으로 사용자 지정 프로젝트 파일에 대 한 소개는 [프로젝트 파일 이해](understanding-the-project-file.md) 및 [빌드 프로세스 이해](understanding-the-build-process.md)를 참조 하세요.

첫째, 관심의 매개 변수 값은 환경 관련 프로젝트 파일 (예: *Env-Dev. proj*)에서 속성으로 정의 됩니다.

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample4.xml)]

> [!NOTE]
> 사용자의 서버 환경에 맞는 환경 관련 프로젝트 파일을 사용자 지정 하는 방법에 대 한 지침은 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)을 참조 하세요.

그런 다음 *Publish. proj* 파일은 이러한 속성을 가져옵니다. 각 *Setparameters .xml* 파일은 *.deploy .cmd* 파일에 연결 되어 있기 때문에 프로젝트 파일에서 각 *. 배포* .cmd 파일을 호출 하기 때문에 프로젝트 파일은 각 *. .cmd* 파일에 대해 MSBuild *항목* 을 만들고 해당 속성을 *항목 메타 데이터로*정의 합니다.

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample5.xml)]

이 경우 다음과 같습니다.

- **ParametersXml** 메타 데이터 값은 *setparameters .xml* 파일의 위치를 나타냅니다.
- **Iiswebappname** 값은 웹 응용 프로그램을 배포 하려는 IIS 경로입니다.
- **MembershipDBConnectionString** 값은 멤버 자격 데이터베이스에 대 한 연결 문자열이 고 **MembershipDBConnectionName** 값은 *setparameters .xml* 파일에 있는 해당 매개 변수의 **name** 특성입니다.
- **Serviceendpointvalue** 값은 대상 서버에서 WCF 서비스의 끝점 주소이 고 **ServiceEndpointParamName** 값은 *setparameters .xml* 파일에 있는 해당 매개 변수의 name 특성입니다.

마지막으로 *게시. proj* 파일에서 게시 되지 않은 **Web패키지** 대상은 **XmlPoke** 작업을 사용 하 여 *setparameters .xml* 파일의 이러한 값을 수정 합니다.

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample6.xml)]

각 **XmlPoke** 작업은 다음과 같은 4 개의 특성 값을 지정 하는 것을 알 수 있습니다.

- **XmlInputPath** 특성은 수정 하려는 파일을 찾을 위치를 작업에 알려 줍니다.
- **Query** 특성은 변경 하려는 XML 노드를 식별 하는 XPath 쿼리입니다.
- **Value** 특성은 선택한 XML 노드에 삽입할 새 값입니다.
- **Condition** 특성은 작업을 실행 하거나 실행 하지 않아야 하는 조건입니다. 이러한 경우 조건이 있으면 *Setparameters .xml* 파일에 null 값 또는 빈 값을 삽입 하지 않도록 합니다.

## <a name="conclusion"></a>결론

이 항목에서는 *Setparameters .xml* 파일의 역할에 대해 설명 하 고 웹 응용 프로그램 프로젝트를 빌드할 때 생성 되는 방법에 대해 설명 했습니다. Xml 파일을 프로젝트에 추가 하 여 추가 설정을 매개 변수화 하는 방법에 대해 설명 *했습니다* . 또한 프로젝트 파일에서 **XmlPoke** 작업을 사용 하 여 더 크고 자동화 된 빌드 프로세스의 일부로 *setparameters .xml* 파일을 수정 하는 방법에 대해서도 설명 합니다.

다음 항목인 [웹 패키지 배포](deploying-web-packages.md)에서는 ..exe 파일을 실행 하거나 msdeploy.exe 명령을 직접 사용 하 여 웹 패키지를 배포할 수 있는 방법을 설명 *합니다.* 두 경우 모두 *Setparameters .xml* 파일을 배포 매개 변수로 지정할 수 있습니다.

## <a name="further-reading"></a>추가 참고 자료

웹 패키지를 만드는 방법에 대 한 자세한 내용은 [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)을 참조 하세요. 웹 패키지를 실제로 배포 하는 방법에 대 한 지침은 [웹 패키지 배포](deploying-web-packages.md)를 참조 하세요. *매개 변수 .xml* 파일을 만드는 방법에 대 한 단계별 연습은 [방법: 패키지를 설치할 때 매개 변수를 사용 하 여 배포 설정 구성](https://msdn.microsoft.com/library/ff398068.aspx)을 참조 하세요.

웹 배포 매개 변수화에 대 한 자세한 내용은 [작업에서 매개 변수화 웹 배포](https://go.microsoft.com/?linkid=9805119) (블로그 게시물)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](building-and-packaging-web-application-projects.md)
> [다음](deploying-web-packages.md)
