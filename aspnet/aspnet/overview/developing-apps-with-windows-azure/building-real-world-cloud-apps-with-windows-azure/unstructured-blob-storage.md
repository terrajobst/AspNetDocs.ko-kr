---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
title: 비구조적 Blob Storage (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 03/30/2015
ms.assetid: 9f05ccb1-2004-4661-ad8b-c370e6c09c8e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
msc.type: authoredcontent
ms.openlocfilehash: 2afd4b5cf640eb97080de7e5280409f5e5347731
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583631"
---
# <a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a>비구조적 Blob Storage (Azure를 사용 하 여 실제 클라우드 앱 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

이전 장에서는 파티션 구성표를 살펴보고 Fix It 앱이 Azure Storage Blob 서비스에 이미지를 저장 하는 방법 및 Azure SQL Database에 다른 작업 데이터를 저장 하는 방법에 대해 설명 했습니다. 이 장에서는 Blob service에 대해 자세히 살펴보고 수정 It 프로젝트 코드에서 구현 되는 방법을 보여 줍니다.

## <a name="what-is-blob-storage"></a>Blob storage 란?

Azure Storage Blob 서비스는 클라우드에 파일을 저장 하는 방법을 제공 합니다. Blob service에는 로컬 네트워크 파일 시스템에 파일을 저장 하는 것 보다 많은 이점이 있습니다.

- 확장성이 매우 뛰어납니다. 단일 저장소 계정에는 [수백 tb](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx)를 저장할 수 있으며, 여러 저장소 계정을 사용할 수 있습니다. 가장 큰 Azure 고객 중 일부는 수백 개의 페타바이트을 저장 합니다. Microsoft SkyDrive는 blob storage를 사용 합니다.
- 내구성이 있습니다. Blob service에 저장 하는 모든 파일은 자동으로 백업 됩니다.
- 고가용성을 제공 합니다. [저장소에 대 한 SLA](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409) 는 선택한 지역 중복 옵션에 따라 99.9% 또는 99.99% 가동 시간을 약속 합니다.
- Azure의 PaaS (platform as a service) 기능입니다 .이는 사용 하는 실제 저장소 용량에 대해서만 요금을 지불 하는 파일을 저장 하 고 검색 하며, Azure는에 필요한 모든 Vm과 디스크 드라이브를 설정 및 관리 하는 것을 의미 합니다. 출력소.
- REST API를 사용 하거나 프로그래밍 언어 API를 사용 하 여 Blob service에 액세스할 수 있습니다. Sdk는 .NET, Java, Ruby 등에 사용할 수 있습니다.
- Blob service에 파일을 저장 하는 경우 인터넷을 통해 공개적으로 사용할 수 있도록 쉽게 설정할 수 있습니다.
- 권한 있는 사용자만 액세스할 수 있도록 Blob service의 파일을 보호 하거나, 제한 된 기간 동안만 사용자가 사용할 수 있도록 하는 임시 액세스 토큰을 제공할 수 있습니다.

Azure 용 응용 프로그램을 빌드할 때 언제 든 지 온-프레미스 환경에서 파일 (예: 이미지, 비디오, Pdf, 스프레드시트 등)로 이동 하는 많은 양의 데이터를 저장 하려고 합니다.--Blob service을 고려 합니다.

## <a name="creating-a-storage-account"></a>저장소 계정 만들기

Blob service 시작 하려면 Azure에서 저장소 계정을 만듭니다. 포털에서 **새로** 만들기 -- **Data Services** -- **저장소** -- **빠른 생성**을 클릭 하 고 URL 및 데이터 센터 위치를 입력 합니다. 데이터 센터 위치는 웹 앱과 동일 해야 합니다.

![저장소 계정 만들기](unstructured-blob-storage/_static/image1.png)

콘텐츠를 저장할 기본 지역을 선택 하면 [지역에서 복제](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage) 옵션을 선택 하는 경우 Azure는 국가의 다른 지역에 있는 다른 데이터 센터에 모든 데이터의 복제본을 만듭니다. 예를 들어 미국 서 부 데이터 센터를 선택 하는 경우 파일을 저장할 때 미국 서 부 데이터 센터로 이동 하지만, 백그라운드에서 Azure는 다른 미국 데이터 센터에도 복사 합니다. 한 국가의 지역에서 재해가 발생 하는 경우에도 데이터가 안전 하 게 보호 됩니다.

Azure는 지역 정치적 경계를 넘어 데이터를 복제 하지 않습니다. 기본 위치가 미국에 있는 경우 파일은 미국 내의 다른 지역에만 복제 됩니다. 기본 위치가 오스트레일리아 인 경우 파일은 오스트레일리아의 다른 데이터 센터로만 복제 됩니다.

물론 앞에서 살펴본 것 처럼 스크립트에서 명령을 실행 하 여 저장소 계정을 만들 수도 있습니다. 저장소 계정을 만드는 Windows PowerShell 명령은 다음과 같습니다.

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

저장소 계정을 만든 후 즉시 Blob service에 파일을 저장 하기 시작할 수 있습니다.

## <a name="using-blob-storage-in-the-fix-it-app"></a>Fix It 앱에서 Blob storage 사용

Fix It 앱을 사용 하면 사진을 업로드할 수 있습니다.

![Fix It 작업 만들기](unstructured-blob-storage/_static/image2.png)

**FixIt 만들기**를 클릭 하면 응용 프로그램이 지정 된 이미지 파일을 업로드 하 고 Blob service에 저장 합니다.

### <a name="set-up-the-blob-container"></a>Blob 컨테이너 설정

Blob service에 파일을 저장 하려면 *컨테이너* 를 저장 해야 합니다. Blob service 컨테이너는 파일 시스템 폴더에 해당 합니다. [모두 자동화 장에서](automate-everything.md) 검토 한 환경 만들기 스크립트는 저장소 계정을 만들지만 컨테이너를 만들지는 않습니다. 따라서 `PhotoService` 클래스의 `CreateAndConfigure` 메서드는 컨테이너가 아직 없는 경우 만듭니다. 이 메서드는 *global.asax*의 `Application_Start` 메서드에서 호출 됩니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

저장소 계정 이름 및 액세스 키는 *web.config* 파일의 `appSettings` 컬렉션에 저장 되며, `StorageUtils.StorageAccount` 메서드의 코드는 이러한 값을 사용 하 여 연결 문자열을 작성 하 고 연결을 설정 합니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

그런 다음 `CreateAndConfigureAsync` 메서드는 Blob service를 나타내는 개체와 Blob service에서 "images" 라는 컨테이너 (폴더)를 나타내는 개체를 만듭니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

"Images" 라는 컨테이너가 아직 존재 하지 않는 경우 (새 저장소 계정에 대해 처음으로 앱을 실행 하는 경우), 코드는 컨테이너를 만들고 사용 권한을 설정 하 여 공용으로 설정 합니다. 기본적으로 새 blob 컨테이너는 전용 이며 저장소 계정에 액세스할 수 있는 권한이 있는 사용자만 액세스할 수 있습니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a>업로드 된 사진을 Blob storage에 저장 합니다.

이미지 파일을 업로드 하 고 저장 하기 위해 앱은 `PhotoService` 클래스에서 `IPhotoService` 인터페이스와 인터페이스 구현을 사용 합니다. *PhotoService.cs* 파일에는 Blob service와 통신 하는 Fix It 앱의 모든 코드가 포함 되어 있습니다.

사용자가 **FixIt 만들기**를 클릭할 때 호출 되는 MVC 컨트롤러 메서드는 다음과 같습니다. 이 코드에서 `photoService`은 `PhotoService` 클래스의 인스턴스를 참조 하 고 `fixittask`는 새 작업에 대 한 데이터를 저장 하는 `FixItTask` 엔터티 클래스의 인스턴스를 참조 합니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

`PhotoService` 클래스의 `UploadPhotoAsync` 메서드는 업로드 된 파일을 Blob service에 저장 하 고 새 Blob을 가리키는 URL을 반환 합니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

`CreateAndConfigure` 메서드에서와 같이 코드는 저장소 계정에 연결 하 고 "images" blob 컨테이너를 나타내는 개체를 만듭니다. 단, 컨테이너는 이미 존재 한다고 가정 합니다.

그런 다음 새 GUID 값을 파일 확장명과 연결 하 여 업로드할 이미지에 대 한 고유 식별자를 만듭니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

그런 다음 blob 컨테이너 개체와 새 고유 식별자를 사용 하 여 blob 개체를 만들고 해당 개체에서 파일의 종류를 나타내는 특성을 설정한 다음 blob 개체를 사용 하 여 blob 저장소에 파일을 저장 합니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

마지막으로 blob를 참조 하는 URL을 가져옵니다. 이 URL은 데이터베이스에 저장 되며, Fix It 웹 페이지에서 업로드 된 이미지를 표시 하는 데 사용할 수 있습니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

이 URL은 FixItTask 테이블의 열 중 하나로 데이터베이스에 저장 됩니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

데이터베이스의 URL과 Blob 저장소의 이미지만 있으면 Fix It 앱은 데이터베이스가 작고 확장 가능 하 고 저렴 한 비용으로 유지 되 고, 저장소가 저렴 하 고 테라바이트 또는 페타바이트를 처리할 수 있는 위치에 저장 됩니다. 저장소 계정 하나는 수백 테라바이트의 수정 It 사진을 저장할 수 있으며, 사용한 만큼만 요금을 지불 하면 됩니다. 따라서 첫 번째 기가바이트에 대해 소규모 지불 9 센트을 시작 하 고 추가 기가바이트 당 잘라내거나 페니에 대 한 이미지를 더 추가할 수 있습니다.

### <a name="display-the-uploaded-file"></a>업로드 한 파일 표시

Fix It 응용 프로그램은 작업에 대 한 세부 정보가 표시 될 때 업로드 된 이미지 파일을 표시 합니다.

![사진으로 It 작업 세부 정보 수정](unstructured-blob-storage/_static/image3.png)

이미지를 표시 하려면 브라우저에 전송 된 HTML에 `PhotoUrl` 값을 포함 해야 합니다. 웹 서버와 데이터베이스는 주기를 사용 하 여 이미지를 표시 하지 않으며 이미지 URL에 대 한 몇 바이트의 서비스를 제공 합니다. 다음 Razor 코드에서 `Model`는 `FixItTask` 엔터티 클래스의 인스턴스를 참조 합니다.

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

표시 되는 페이지의 HTML을 살펴보면 blob storage에서 이미지를 직접 가리키는 URL이 다음과 같이 표시 됩니다.

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a>요약

Fix It 앱이 Blob service에 이미지를 저장 하 고 SQL database에 이미지 Url만 저장 하는 방법을 살펴보았습니다. Blob service를 사용 하 여 SQL 데이터베이스를 사용 하는 것 보다 훨씬 더 작게 유지 하 고, 거의 무제한의 태스크를 확장할 수 있으며, 많은 코드를 작성 하지 않고도 수행할 수 있습니다.

저장소 계정에는 수백 tb를 사용할 수 있으며, 저장소 비용은 매월 gb 당 약 3 센트 및 작은 트랜잭션 요금으로 시작 하는 SQL Database 저장소 보다 훨씬 저렴 합니다. 최대 용량에 대해서만 요금을 지불 하는 것은 아니지만, 실제로 저장 된 양에 대해서만 요금을 지불 하는 것이 좋습니다. 따라서 앱을 확장할 수는 있지만이 추가 용량에 대해서는 지불 하지 않습니다.

[다음 장에서](design-to-survive-failures.md) 는 클라우드 앱에서 오류를 정상적으로 처리할 수 있도록 하는 중요성에 대해 설명 합니다.

## <a name="resources"></a>자료

자세한 내용은 다음 리소스를 참조 하세요.

- [AZURE BLOB Storage를 소개](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/)합니다. Mike 목재의 블로그입니다.
- [.Net에서 Azure Blob Storage 서비스를 사용 하는 방법](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs) MicrosoftAzure.com 사이트에 대 한 공식 설명서입니다. Blob storage에 연결 하 고, 컨테이너를 만들고, blob을 업로드 하 고 다운로드 하는 방법을 보여 주는 코드 예제에 대 한 간략 한 소개입니다.
- [안전 하지 않음: 확장 가능 하 고 복원 가능한 Cloud Services 빌드](https://channel9.msdn.com/Series/FailSafe) 9 개 부분으로 구성 된 비디오 시리즈, Marc Mercuri 및 Mark Simm. Microsoft의 Microsoft CAT (고객 자문 팀) 경험을 통해 실제 고객과 함께 제공 되는 스토리를 통해 매우 편리 하 게 액세스할 수 있고 흥미로운 방식으로 높은 수준의 개념 및 아키텍처 원칙을 제공 합니다. Azure Storage 서비스 및 blob에 대 한 자세한 내용은 35:13에서 시작 하는 에피소드 5를 참조 하십시오.
- [Microsoft 패턴 및 사례-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx) Valet 키 패턴을 참조 하세요.

> [!div class="step-by-step"]
> [이전](data-partitioning-strategies.md)
> [다음](design-to-survive-failures.md)
