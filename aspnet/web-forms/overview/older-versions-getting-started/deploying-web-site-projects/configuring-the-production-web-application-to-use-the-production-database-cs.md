---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-cs
title: 프로덕션 데이터베이스를 사용 하도록 프로덕션 웹 응용 프로그램 구성 (C#) | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 설명 했 듯이, 개발 환경과 프로덕션 환경 간에 구성 정보가 다를 경우에는 일반적이 지 않습니다. ...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 0177dabd-d888-449f-91b2-24190cf5e842
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-cs
msc.type: authoredcontent
ms.openlocfilehash: 89941bb6db52316a259ad5f5577721e36f19bd84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512597"
---
# <a name="configuring-the-production-web-application-to-use-the-production-database-c"></a>프로덕션 데이터베이스를 사용하도록 프로덕션 웹 애플리케이션 구성(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_08_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial08_DBConfig_cs.pdf)

> 이전 자습서에서 설명 했 듯이, 개발 환경과 프로덕션 환경 간에 구성 정보가 다를 경우에는 일반적이 지 않습니다. 이는 데이터베이스 연결 문자열이 개발 환경과 프로덕션 환경 간에 다르므로 데이터 기반 웹 응용 프로그램의 경우 특히 그렇습니다. 이 자습서에서는 적절 한 연결 문자열을 더 자세히 포함 하도록 프로덕션 환경을 구성 하는 방법을 살펴봅니다.

## <a name="introduction"></a>소개

데이터 기반 웹 응용 프로그램은 일반적으로 프로덕션 환경에 있는 경우를 제외 하 고 개발 시 다른 데이터베이스를 사용 합니다. 웹 호스트 공급자가 호스트 하 고 로컬로 개발한 응용 프로그램의 경우 개발 데이터베이스는 일반적으로 개발자 컴퓨터에 있으며 프로덕션 데이터베이스는 웹 호스팅 회사 기능의 데이터베이스 서버에서 호스팅됩니다. 데이터 기반 웹 응용 프로그램을 배포 하려면 개발 데이터베이스를 프로덕션 데이터베이스 서버에 복사 해야 합니다. 이전 자습서에서는이 단계를 수행 하는 방법을 살펴보았습니다.

웹 응용 프로그램은 *연결 문자열* 의 정보를 사용 하 여 데이터베이스와의 연결을 설정 합니다. 일반적으로 `Web.config`에 저장 되는 연결 문자열은 데이터베이스 서버 이름, 데이터베이스 이름, 보안 컨텍스트 및 기타 정보를 지정 합니다. 웹 응용 프로그램에서 사용 하는 데이터베이스는 개발 또는 프로덕션 환경에서 웹 응용 프로그램이 실행 되 고 있는지 여부에 따라 달라 지므로 두 환경 간에 연결 문자열이 달라 야 합니다.

구성 정보는 개발 환경과 프로덕션 환경 간에 차이가 있는 경우가 종종 있습니다. *개발 및 프로덕션 자습서 간의 일반적인 구성 차이점* 에는 이러한 두 환경 간에 별도의 구성 정보를 유지 관리 하는 방법과 데이터베이스 연결 문자열에 대 한 간략 한 설명이 나와 있습니다. 이 자습서에서는 적절 한 연결 문자열을 더 자세히 포함 하도록 프로덕션 환경을 구성 하는 방법을 살펴봅니다.

## <a name="examining-the-connection-string-information"></a>연결 문자열 정보 검사

책 리뷰 웹 응용 프로그램에서 사용 하는 연결 문자열은 응용 프로그램 구성 파일 `Web.config`에 저장 됩니다. `Web.config`에는 [&lt;connectionStrings&gt;](https://msdn.microsoft.com/library/bf7sd233.aspx)이라는 연결 문자열을 저장 하기 위한 특수 섹션이 포함 되어 있습니다. 책 리뷰 웹 사이트의 `Web.config` 파일에는이 섹션에 정의 된 `ReviewsConnectionString`라는 하나의 연결 문자열이 있습니다.

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample1.xml)]

연결 문자열-Data Source = .\SQLEXPRESS; AttachDbFilename = | DataDirectory | \Reviews.mdf; Integrated Security = True; User Instance = True-세미콜론으로 구분 되는 옵션/값 쌍과 각 옵션 및 등호 (=)로 구분 된 값으로 구성 된 여러 옵션 및 값으로 구성 됩니다. 이 연결 문자열에 사용 되는 네 가지 옵션은 다음과 같습니다.

- `Data Source`-데이터베이스 서버 위치 및 데이터베이스 서버 인스턴스 이름 (있는 경우)을 지정 합니다. 값 `.\SQLEXPRESS`는 데이터베이스 서버와 인스턴스 이름이 있는 예입니다. 기간은 데이터베이스 서버가 응용 프로그램과 동일한 컴퓨터에 있음을 지정 합니다. 인스턴스 이름이 `SQLEXPRESS`입니다.
- `AttachDbFilename`-데이터베이스 파일의 위치를 지정 합니다. 값에는 런타임에 응용 프로그램 `App_Data` 폴더의 전체 경로로 확인 되는 자리 표시자 `|DataDirectory|`포함 됩니다.
- `Integrated Security`-데이터베이스에 연결할 때 지정 된 사용자 이름/암호를 사용할지 (false) 또는 현재 Windows 계정 자격 증명 (true)를 사용할지 여부를 나타내는 부울 값입니다.
- `User Instance`-관리자가 아닌 사용자가 로컬 컴퓨터에 연결 하 고 SQL Server Express 버전 데이터베이스에 연결할 수 있는지 여부를 나타내는 SQL Server Express 버전에 해당 하는 구성 옵션입니다. 이 설정에 대 한 자세한 내용은 [SQL Server Express 사용자 인스턴스](https://msdn.microsoft.com/library/ms254504.aspx) 를 참조 하세요.

허용 되는 연결 문자열 옵션은 연결 하려는 데이터베이스 및 사용 중인 ADO.NET 데이터베이스 공급자에 따라 달라 집니다. 예를 들어 Microsoft SQL Server 데이터베이스에 연결 하기 위한 연결 문자열은 Oracle 데이터베이스에 연결 하는 데 사용 되는 연결과 다릅니다. 마찬가지로 SqlClient 공급자를 사용 하 여 Microsoft SQL Server 데이터베이스에 연결 하는 경우 OLE DB 공급자를 사용 하는 경우와 다른 연결 문자열을 사용 합니다.

사용할 수 있는 옵션에 대 한 리소스로 [ConnectionStrings.com](http://www.connectionstrings.com/) 와 같은 사이트를 사용 하 여 데이터베이스 연결 문자열을 직접 만들 수 있습니다. 그러나 보다 쉬운 방법은 Visual Studio의 서버 탐색기에 데이터베이스를 추가한 다음 속성 창에서 연결 문자열을 가져오는 것입니다. 를 사용 하 여 프로덕션 데이터베이스 서버에 대 한 연결 문자열을 생성 하는 데이 두 번째 기법을 사용 합니다.

Visual Studio를 열고 서버 탐색기 창으로 이동 합니다 (Visual Web Developer에서는이 창을 데이터베이스 탐색기 이라고 함). 데이터 연결 옵션을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 연결 추가 옵션을 선택 합니다. 그러면 그림 1에 표시 된 마법사가 나타납니다. 적절 한 데이터 원본을 선택 하 고 계속을 클릭 합니다.

[![서버 탐색기에 새 데이터베이스를 추가 하도록 선택 합니다.](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image2.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image1.jpg) 

**그림 1**: 서버 탐색기에 새 데이터베이스를 추가 하도록 선택 ([전체 크기 이미지를 보려면 클릭](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image3.jpg))

다음으로 다양 한 데이터베이스 연결 정보를 지정 합니다 (그림 2 참조). 웹 호스팅 회사에 등록 하는 경우 데이터베이스에 연결 하는 방법에 대 한 정보 (데이터베이스 서버 이름, 데이터베이스 이름, 데이터베이스에 연결 하는 데 사용할 사용자 이름 및 암호 등)를 제공 해야 합니다. 이 정보를 입력 한 후 확인을 클릭 하 여이 마법사를 완료 하 고 데이터베이스를 서버 탐색기에 추가 합니다.

[데이터베이스 연결 정보를 지정 ![](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image5.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image4.jpg) 

**그림 2**: 데이터베이스 연결 정보 지정 ([전체 크기 이미지를 보려면 클릭](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image6.jpg))

이제 프로덕션 환경 데이터베이스가 서버 탐색기에 나열 됩니다. 서버 탐색기에서 데이터베이스를 선택 하 고 속성 창로 이동 합니다. 여기에서 데이터베이스의 연결 문자열을 사용 하 여 연결 문자열 이라는 속성을 찾을 수 있습니다. 프로덕션에 Microsoft SQL Server 데이터베이스를 사용 하 고 SqlClient 공급자를 사용 하는 경우 연결 문자열은 다음과 같이 표시 됩니다.

<strong>데이터 원본 =<em>serverName</em>; 초기 카탈로그 =<em>databaseName</em>; 보안 정보 유지 = True; 사용자 ID =<em>사용자 이름</em>; 암호 =*암호</strong>*

여기서 *serverName*, *databaseName*, *username*및 *password* 는 웹 호스트 회사에서 제공 하는 데이터베이스 서버 이름, 데이터베이스 이름 및 사용자 이름 및 암호에 대 한 값을 포함 합니다.

## <a name="deploying-the-book-reviews-web-application"></a>책 리뷰 웹 응용 프로그램 배포

앞의 자습서에서는 개발 데이터베이스를 프로덕션 환경으로 복사 하는 과정을 단계별로 안내 했지만 데이터 기반 응용 프로그램 배포를 탐색 하지 않았습니다. 이 시점에서 프로덕션 환경에는 데이터베이스가 포함 되지만, 정적 검토가 포함 된 책 리뷰 응용 프로그램의 버전을 사용 하 고 있습니다. 업데이트 된 구성 정보와 함께 새로운 데이터 기반 응용 프로그램을 프로덕션 서버에 배포 해야 합니다.

잠시 개발 환경에서 프로덕션 환경으로 데이터 기반 응용 프로그램을 배포 합니다. 이 프로세스는 이전 자습서에 자세히 설명 되어 있습니다. 리프레셔가 필요한 경우 *FTP 클라이언트를 사용 하 여 웹 사이트 배포* 또는 *Visual Studio를 사용 하 여 웹 사이트 배포* 자습서를 참조 하세요. 프로덕션 환경에서 사용 되는 프로덕션 데이터베이스 연결 문자열을 확인 해야 합니다. 즉, 대체 `Web.config` 파일을 배포 해야 합니다. 특히이 수정 된 `Web.config` 파일 `<connectionStrings>` 요소는 프로덕션 데이터베이스 연결 문자열을 포함 해야 하며 다음과 같이 표시 되어야 합니다.

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample2.xml)]

`<connectionStrings>` 요소의 연결 문자열 이름은 같은 이름 (`ReviewsConnectionString`) 이지만 이제 개발 데이터베이스 연결 문자열 대신 프로덕션 데이터베이스 연결 문자열을 포함 합니다.

보다 정형화 된 배포 워크플로가 있는 경우를 배포 하기 전에 프로덕션 데이터베이스 연결 문자열을 사용 하도록 `Web.config` 파일을 수동으로 수정 하거나 (나중에 개발 데이터베이스 연결 문자열을 사용 하 여 다시 되돌립니다.) 배포 프로세스의 일부로 프로덕션 환경으로 업로드 되는 프로덕션 환경 구성 정보를 사용 하 여 별도의 `Web.config` 파일을 유지 관리 합니다.

> [!NOTE]
> 개발 데이터베이스 연결 문자열을 포함 하는 `Web.config` 파일을 실수로 배포 하는 경우 프로덕션의 응용 프로그램이 데이터베이스에 연결 하려고 하면 오류가 발생 합니다. 이 오류는 서버를 찾을 수 없거나 액세스할 수 없다는 메시지를 보고 하는 `SqlException`으로 매니페스트 됩니다.

사이트가 프로덕션 환경에 배포 되 면 브라우저를 통해 프로덕션 사이트를 방문 합니다. 데이터 기반 응용 프로그램을 로컬로 실행 하는 경우와 동일한 사용자 환경이 표시 됩니다. 물론 프로덕션 환경에서 웹 사이트를 방문 하는 경우이 사이트는 프로덕션 데이터베이스 서버에서 제공 되지만 개발 환경에서 웹 사이트를 방문 하면 개발 중인 데이터베이스를 사용 합니다. 그림 3에서는 프로덕션 환경에서 웹 사이트의 24 시간 검토 페이지에서 *ASP.NET 3.5을* 설명 합니다 (브라우저의 주소 표시줄에서 URL을 확인).

[이제 데이터 기반 응용 프로그램을 프로덕션 환경에서 사용할 수 ![.](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image8.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image7.jpg) 

**그림 3**: 이제 프로덕션 환경에서 데이터 기반 응용 프로그램을 사용할 수 있습니다. ([전체 크기 이미지를 보려면 클릭](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image9.jpg))

### <a name="storing-connection-strings-in-a-separate-configuration-file"></a>별도의 구성 파일에 연결 문자열 저장

개발 및 프로덕션 환경에 대 한 별도의 구성 정보를 유지 관리 하는 일반적인 방법은 두 가지 버전의 `Web.config`를 개발 환경에 대해 하나, 프로덕션 환경에 대 한 것입니다. 배포 시 적절 한 `Web.config` 버전을 프로덕션 환경으로 복사할 수 있습니다. 이상적으로이 프로세스는 배포 워크플로의 일부로 자동화 됩니다.

두 개의 별도 `Web.config` 파일을 유지 관리 하는 대신 필요에 따라 보다 세분화 된 차이를 제공할 수 있습니다. `Web.config` 파일을 구성 하는 요소는 `Web.config` 파일에서 참조 되는 외부 구성 파일에 정의 될 수 있습니다. 간단히 말해서 응용 프로그램에서 사용 하는 연결 문자열을 포함 하는 databaseConnectionStrings 파일을 참조 하는 두 환경 모두에 대해 하나의 `Web.config` 파일을 사용할 수 있으며 각 환경에 대해 고유 합니다. 서로 다른 구성 정보를 별도의 파일로 분리 하는 것이 tidier `Web.config` 파일을 제공 하 고 개발 환경과 프로덕션 환경 간의 구성 차이점을 보다 명확 하 게 설명 하는 것을 알게 되었습니다.

이 방법을 사용 하려면 먼저 `ConfigSections`이라는 웹 응용 프로그램에서 새 폴더를 만듭니다. 다음으로,이 새 폴더에 databaseConnectionStrings 및 databaseConnectionStrings 라는 두 개의 파일을 추가 합니다. 그런 다음 `Web.config`에서 `<connectionStrings>` 요소를 databaseConnectionStrings 및 databaseConnectionStrings 파일에 복사한 다음, 프로덕션 데이터베이스 연결 문자열을 지정 하도록 databaseConnectionStrings 파일의 연결 문자열을 수정 합니다. 예를 들어 databaseConnectionStrings 파일에는 개발 데이터베이스를 참조 하는 연결 문자열을 포함 하는 `<connectionStrings>` 요소만 포함 되어야 합니다.

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample3.xml)]

마찬가지로 databaseConnectionStrings 파일은 `<connectionStrings>` 요소만 포함 하 고 하나는 프로덕션 데이터베이스 연결 문자열을 포함 해야 합니다.

DatabaseConnectionStrings 파일의 복사본을 만들고 이름을 databaseConnectionStrings로 지정 합니다.

> [!NOTE]
> `connectionStrings.config` 또는 `dbInfo.config`와 같이 같은 경우 구성 파일의 이름을 databaseConnectionStrings 이외의 다른 이름으로 지정할 수 있습니다. 그러나 `.config` 파일이 기본적으로 ASP.NET 엔진에서 제공 되지 않으므로 `.config` 확장명으로 파일의 이름을 지정할 수 있습니다. `connectionStrings.txt`와 같이 파일 이름을 다른 이름으로 지정 하는 경우 사용자는 브라우저를 가리켜 파일의 내용을 [www.yoursite.com/ConfigSettings/connectionStrings.txt](http://www.yoursite.com/ConfigSettings/connectionStrings.txt) 하 고 볼 수 있습니다.

이 시점에서 `ConfigSections` 폴더는 세 개의 파일을 포함 해야 합니다 (그림 4 참조). DatabaseConnectionStrings 및 databaseConnectionStrings 파일은 각각 개발 및 프로덕션 환경에 대 한 연결 문자열을 포함 합니다. DatabaseConnectionStrings 파일에는 런타임에 웹 응용 프로그램에서 사용 하는 연결 문자열 정보가 포함 되어 있습니다. 따라서 databaseConnectionStrings 파일은 개발 환경에 있는 databaseConnectionStrings 파일과 동일 해야 하지만 프로덕션 환경에서는 databaseConnectionStrings 파일이와 동일 해야 합니다. databaseConnectionStrings.

[ConfigSections ![](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image11.jpg)](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image10.jpg) 

**그림 4**: configsections ([전체 크기 이미지를 보려면 클릭](configuring-the-production-web-application-to-use-the-production-database-cs/_static/image12.jpg))

이제 연결 문자열 저장소에 databaseConnectionStrings 파일을 사용 하도록 `Web.config`에 지시 해야 합니다. `Web.config`을 열고 기존 `<connectionStrings>` 요소를 다음과 같이 바꿉니다.

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-cs/samples/sample4.xml)]

`configSource` 특성은 `Web.config` 파일을 기준으로 하는 실제 경로를 지정 합니다. 외부 `.config` 파일이 `Web.config`와 동일한 디렉터리에 있는 경우이 특성을 `.config` 파일의 파일 이름으로 설정 합니다. 하위 디렉터리에 있는 경우 databaseConnectionStrings의 경우와 마찬가지로 백슬래시를 사용 하 여 폴더와 파일 이름을 구분 하는 하위 폴더를 지정 합니다 (예: ConfigSections\databaseConnectionStrings.config.).

이러한 수정을 통해 개발 및 프로덕션 환경에는 동일한 `Web.config` 파일이 포함 됩니다. 이제 유일한 차이점은 databaseConnectionStrings 파일입니다. DatabaseConnectionStrings 파일을 프로덕션에 복사 하 고 이름을 databaseConnectionStrings로 바꿉니다. 나중에 databaseConnectionStrings 파일로 만든 후 프로덕션 데이터베이스 연결 문자열을 변경 하 여 해당 파일을 프로덕션 환경으로 업로드 하 고 이름을 databaseConnectionStrings로 변경 해야 합니다.

> [!NOTE]
> 별도의 파일에 `Web.config` 요소에 대 한 정보를 지정 하 고 `configSource` 특성을 사용 하 여 `Web.config`내에서 해당 파일을 참조할 수 있습니다.

## <a name="summary"></a>요약

데이터 기반 응용 프로그램은 일반적으로 개발 및 프로덕션 환경에서 서로 다른 데이터베이스를 사용 합니다. 따라서 웹 응용 프로그램 구성에 저장 된 데이터베이스 연결 문자열은 환경에 따라 고유 해야 합니다. 이 자습서에서는 프로덕션 데이터베이스 연결 문자열을 확인 하는 방법과 두 환경에서 고유 연결 문자열 정보를 유지 관리 하는 방법을 살펴보았습니다.

행복 한 프로그래밍

#### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [연결 문자열 및 구성 파일](https://msdn.microsoft.com/library/ms254494.aspx)
- [데이터베이스 구성 문자열 정보 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [Web.config 파일에서 설정을 이동 합니다.](http://www.asp101.com/tips/index.asp?id=154)
- [&lt;connectionStrings&gt; 요소에 대 한 기술 설명서](https://msdn.microsoft.com/library/bf7sd233.aspx)

> [!div class="step-by-step"]
> [이전](deploying-a-database-cs.md)
> [다음](configuring-a-website-that-uses-application-services-cs.md)
