---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
title: 데이터 저장소 옵션 (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: e51fcecb-cb33-4f9e-8428-6d2b3d0fe1bf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
msc.type: authoredcontent
ms.openlocfilehash: f97d973d87db895441f813376d757a8a2e94b255
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585926"
---
# <a name="data-storage-options-building-real-world-cloud-apps-with-azure"></a>데이터 저장소 옵션 (Azure를 사용 하 여 실제 클라우드 앱 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

대부분의 사람들은 관계형 데이터베이스에 사용 되며 클라우드 앱을 디자인할 때 다른 데이터 저장소 옵션을 간과 하는 경향이 있습니다. [Nosql](http://en.wikipedia.org/wiki/NoSQL) (비관계형) 데이터베이스에서 관계형 데이터베이스 보다 더 효율적으로 작업을 처리할 수 있기 때문에 결과는 만족 스 럽 지 않을 수 있습니다. 고객이 중요 한 데이터 저장소 문제를 해결 하는 데 도움을 요청 하는 경우 NoSQL 옵션 중 하나가 더 잘 작동 하는 관계형 데이터베이스가 있기 때문에 종종 있습니다. 이러한 상황에서 고객은 프로덕션에 앱을 배포 하기 전에 NoSQL 솔루션을 구현 하는 경우 더 나은 성능을 향상 시킬 수 있습니다.

반면, NoSQL 데이터베이스에서 모든 작업을 충분히 수행 하거나 충분히 사용할 수 있다고 가정 하는 것은 실수입니다. 모든 데이터 저장소 작업에 대해 가장 적합 한 데이터 관리 옵션은 없습니다. 다른 데이터 관리 솔루션은 여러 작업에 대해 최적화 됩니다. 대부분의 실제 클라우드 앱은 다양 한 데이터 저장소 요구 사항을 가지 며 여러 데이터 저장소 솔루션을 조합 하 여 가장 효과적으로 처리 하는 경우가 많습니다.

이 장의 목적은 클라우드 앱에서 사용할 수 있는 데이터 저장소 옵션을 광범위 하 게 이해 하 고 시나리오에 적합 한 옵션을 선택 하는 방법에 대 한 기본 지침을 제공 하는 것입니다. 응용 프로그램을 개발 하기 전에 사용자에 게 제공 되는 옵션을 알고 있으며 해당 장점과 약점을 고려 하는 것이 가장 좋습니다. 평면을 비행 하는 동안 jet 엔진을 변경 하는 것 처럼 프로덕션 앱에서 데이터 저장소 옵션을 변경 하는 것은 매우 어려울 수 있습니다.

## <a name="data-storage-options-on-azure"></a>Azure의 데이터 저장소 옵션

클라우드를 사용 하면 다양 한 관계형 및 NoSQL 데이터 저장소를 비교적 쉽게 사용할 수 있습니다. Azure에서 사용할 수 있는 데이터 저장소 플랫폼은 다음과 같습니다.

![](data-storage-options/_static/image1.png)

다음 표에서는 네 가지 유형의 NoSQL 데이터베이스를 보여 줍니다.

- [키/값 데이터베이스](https://msdn.microsoft.com/library/dn313285.aspx#sec7) 는 각 키 값에 대해 직렬화 된 단일 개체를 저장 합니다. 이는 지정 된 키 값에 대해 하나의 항목을 가져오려는 많은 양의 데이터를 저장 하는 데 유용 하며 항목의 다른 속성을 기반으로 쿼리할 필요가 없습니다.

    [Azure Blob storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/) 는 폴더 및 파일 이름에 해당 하는 키 값을 사용 하 여 클라우드의 파일 저장소와 같은 기능을 하는 키/값 데이터베이스입니다. 파일 내용에서 값을 검색 하는 것이 아니라 폴더 및 파일 이름으로 파일을 검색 합니다.

    [Azure 테이블 저장소](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/) 는 키/값 데이터베이스 이기도 합니다. 각 값을 *엔터티* (파티션 키와 행 키로 식별 되는 행과 유사) 라고 하며 여러 *속성* (열과 유사 하지만 테이블의 모든 엔터티가 동일한 열을 공유 해야 하는 것은 아님)을 포함 합니다. 키가 아닌 열에 대 한 쿼리는 매우 비효율적 이므로 피해 야 합니다. 예를 들어 단일 사용자에 대 한 정보를 저장 하는 하나의 파티션이 있는 사용자 프로필 데이터를 저장할 수 있습니다. 사용자 이름, 암호 해시, 생년월일 등의 데이터를 한 엔터티의 개별 속성에 저장 하거나 동일한 파티션에 있는 별도의 엔터티에 저장할 수 있습니다. 그러나 지정 된 생년월일 범위를 가진 모든 사용자를 쿼리하지는 않지만 프로필 테이블과 다른 테이블 간에 조인 쿼리를 실행할 수 없습니다. 테이블 저장소는 관계형 데이터베이스 보다 확장성이 뛰어나고 비용이 저렴 하지만 복잡 한 쿼리 또는 조인을 사용 하지 않습니다.
- [Documentdatabases](https://msdn.microsoft.com/library/dn313285.aspx#sec8) 는 값이 *문서인*키/값 데이터베이스입니다. 여기에서 "Document"는 Word 또는 Excel 문서에서 사용 되지 않지만 자식 문서 일 수 있는 명명 된 필드 및 값의 컬렉션을 의미 합니다. 예를 들어 주문 기록 테이블에서 주문 문서에 주문 번호, 주문 날짜 및 고객 필드가 있을 수 있습니다. 그리고 고객 필드에는 이름 및 주소 필드가 있을 수 있습니다. 데이터베이스는 필드 데이터를 XML, YAML, JSON 또는 BSON과 같은 형식으로 인코딩합니다. 또는 일반 텍스트를 사용할 수 있습니다. 키/값 데이터베이스와는 별도로 문서 데이터베이스를 설정 하는 기능 중 하나는 키가 아닌 필드를 쿼리하고 쿼리를 보다 효율적으로 만들기 위해 보조 인덱스를 정의 하는 기능입니다. 이 기능을 통해 문서 데이터베이스를 문서 키 값 보다 더 복잡 한 조건에 따라 데이터를 검색 해야 하는 응용 프로그램에 더 적합 하 게 만들 수 있습니다. 예를 들어 판매 주문 기록 문서 데이터베이스에서 제품 ID, 고객 ID, 고객 이름 등의 다양 한 필드를 쿼리할 수 있습니다. [MongoDB](http://www.mongodb.org/) 은 인기 있는 문서 데이터베이스입니다.
- [열 패밀리 데이터베이스](https://msdn.microsoft.com/library/dn313285.aspx#sec9) 는 데이터 저장소를 열 패밀리 라는 관련 열 컬렉션으로 구조화 하는 데 사용할 수 있는 키/값 데이터 저장소입니다. 예를 들어 인구 조사 데이터베이스에는 개인의 이름 (first, middle, last)에 대해 한 개의 열 그룹, 사용자 주소에 대 한 그룹 한 개, 개인의 프로필 정보에 대 한 그룹 한 개 (DOB, 성별 등)가 있을 수 있습니다. 그런 다음 데이터베이스는 각 열 패밀리를 별도의 파티션에 저장 하 고 한 사용자의 모든 데이터를 동일한 키와 관련 시킬 수 있습니다. 그러면 모든 이름 및 주소 정보도 읽을 필요 없이 모든 프로필 정보를 읽을 수 있습니다. [Cassandra](http://cassandra.apache.org/) 은 인기 있는 열 패밀리 데이터베이스입니다.
- [그래프 데이터베이스](https://msdn.microsoft.com/library/dn313285.aspx#sec10) 는 개체 및 관계의 컬렉션으로 정보를 저장 합니다. 그래프 데이터베이스의 목적은 응용 프로그램에서 개체의 네트워크와 개체 간의 관계를 트래버스하는 쿼리를 효율적으로 수행할 수 있도록 하는 것입니다. 예를 들어, 개체는 인적 자원 데이터베이스의 직원 일 수 있으며 "Scott에 게 직접 또는 간접적으로 작업 하는 모든 직원 찾기"와 같은 쿼리를 용이 하 게 할 수 있습니다. [Neo4j](http://www.neo4j.org/) 은 인기 있는 그래프 데이터베이스입니다.

NoSQL 옵션은 관계형 데이터베이스에 비해 구조화 되지 않은 데이터를 저장 하 고 분석 하는 데 훨씬 더 큰 확장성과 비용 효율성을 제공 합니다. 단점은 관계형 데이터베이스의 풍부한 queryability 강력한 데이터 무결성 기능을 제공 하지 않기 때문입니다. NoSQL은 조인 쿼리를 수행할 필요가 없는 많은 볼륨이 포함 된 IIS 로그 데이터에 적합 합니다. NoSQL은 절대 데이터 무결성이 필요 하 고 다른 계정 관련 데이터에 대 한 많은 관계를 포함 하는 은행 거래에 적합 하지 않습니다.

NoSQL 데이터베이스의 확장성과 관계형 데이터베이스의 queryability 및 트랜잭션 무결성을 결합 하는 [newsql](http://en.wikipedia.org/wiki/NewSQL) 이라는 새로운 범주의 데이터베이스 플랫폼도 있습니다. NewSQL 데이터베이스는 분산 저장소 및 쿼리 처리를 위해 설계 되었으며,이는 종종 "OldSQL" 데이터베이스에서 구현 하기 어렵습니다. [NuoDB](http://www.nuodb.com/) 은 Azure에서 사용할 수 있는 newsql 데이터베이스의 예입니다.

<a id="hadoop"></a>
## <a name="hadoop-and-mapreduce"></a>Hadoop 및 MapReduce

NoSQL 데이터베이스에 저장할 수 있는 많은 양의 데이터는 적시에 효율적으로 분석 하기가 어려울 수 있습니다. 이렇게 하려면 [MapReduce](http://en.wikipedia.org/wiki/MapReduce) 기능을 구현 하는 [Hadoop](http://hadoop.apache.org/) 과 같은 프레임 워크를 사용할 수 있습니다. 기본적으로 MapReduce 프로세스는 다음과 같습니다.

- 데이터 저장소에서 데이터 저장소를 선택 하 여 처리 해야 하는 데이터의 크기를 제한 합니다. 예를 들어 출생 연도를 기준으로 사용자의 구성을을 알고 싶으면 사용자 프로필 데이터 저장소에서 출생 연도만 선택 합니다.
- 데이터를 파트로 분할 하 고 처리를 위해 다른 컴퓨터로 보냅니다. 컴퓨터 A에서 1950-1959 날짜가 있는 사용자 수를 계산 하 고, 컴퓨터 B를 1960-1969로 계산 합니다. 이 컴퓨터 그룹을 *Hadoop 클러스터*라고 합니다.
- 파트에 대 한 처리가 완료 된 후 각 파트의 결과를 다시 배치 합니다. 이제 각 출생 연도의 사용자 수와이 전체 목록의 백분율 계산 작업을 비교적 간단 하 게 관리할 수 있습니다.

Azure에서 [HDInsight](https://azure.microsoft.com/services/hdinsight/) 를 사용 하면 Hadoop의 기능을 사용 하 여 빅 데이터에서 새로운 정보를 처리 하 고 분석 하 고 얻을 수 있습니다. 예를 들어이를 사용 하 여 웹 서버 로그를 분석할 수 있습니다.

- 저장소 계정에 대 한 웹 서버 로깅을 사용 하도록 설정 합니다. 그러면 응용 프로그램에 대 한 모든 HTTP 요청에 대 한 로그를 Blob Service에 쓰도록 Azure가 설정 됩니다. Blob Service는 기본적으로 클라우드 파일 저장소 이며 HDInsight와 원활 하 게 통합 됩니다.

    ![Blob Storage에 기록](data-storage-options/_static/image2.png)
- 앱이 트래픽을 가져오는 경우 웹 서버 IIS 로그는 Blob 저장소에 기록 됩니다.

    ![웹 서버 로그](data-storage-options/_static/image3.png)
- 포털에서 **새로** 만들기 **Data Services** - 를 클릭 하 - **hdinsight** - **빠른 생성**을 클릭 하 고 hdinsight 클러스터 이름, 클러스터 크기 (hdinsight 클러스터 데이터 노드 수) 및 hdinsight 클러스터에 대 한 사용자 이름 및 암호를 지정 합니다.

    ![HDInsight](data-storage-options/_static/image4.png)

이제 MapReduce 작업을 설정 하 여 로그를 분석 하 고 다음과 같은 질문에 대 한 답을 얻을 수 있습니다.

- 앱이 가장 또는 최소 트래픽을 가져오는 시간
- 내 트래픽이 들어오는 국가는 무엇 인가요?
- 내 트래픽이 들어오는 영역의 평균 환경 수입은 무엇 인가요? (IP 주소로 전 수입을 제공 하는 공용 데이터 집합이 있으며, 웹 서버 로그의 IP 주소와 일치 시킬 수 있습니다.)
- 환경 수입은 사이트의 특정 페이지 또는 제품과 상관 관계가 있습니다.

이러한 질문에 대 한 답변을 사용 하 여 고객이 관심이 나 특정 제품을 구매할 가능성이 있는 경우 광고를 대상으로 지정할 수 있습니다.

[모두 자동화 단원](automate-everything.md)에서 설명한 대로 포털에서 수행할 수 있는 대부분의 기능은 자동화 될 수 있으며, HDInsight 분석 작업 설정 및 실행을 포함 합니다. 일반적인 HDInsight 스크립트에는 다음 단계가 포함 될 수 있습니다.

- HDInsight 클러스터를 프로 비전 하 고 Blob storage 입력에 대 한 저장소 계정에 연결 합니다.
- MapReduce 작업 실행 파일 (jar 또는 .exe 파일)을 HDInsight 클러스터에 업로드 합니다.
- Blob 저장소에 출력 데이터를 저장 하는 MapReduce를 제출 합니다.
- 작업이 완료 될 때까지 기다립니다.
- HDInsight 클러스터를 삭제 합니다.
- Blob 저장소에서 출력에 액세스 합니다.

이를 모두 수행 하는 스크립트를 실행 하 여 HDInsight 클러스터가 프로 비전 되는 시간을 최소화 하 여 비용을 최소화 합니다.

<a id="paasiaas"></a>
## <a name="platform-as-a-service-paas-versus-infrastructure-as-a-service-iaas"></a>PaaS (Platform as a Service)와 IaaS (Infrastructure as a Service) 비교

위에 나열 된 데이터 저장소 옵션에는 PaaS (Platform as a Service) 및 IaaS (Infrastructure as a Service) 솔루션이 모두 포함 되어 있습니다. PaaS는 하드웨어 및 소프트웨어 인프라를 관리 하 고 서비스를 사용 하는 것을 의미 합니다. SQL Database는 Azure의 PaaS 기능입니다. 데이터베이스를 요청 하면 Azure에서 Vm을 설정 및 구성 하 고 데이터베이스를 설정 합니다. Vm에 직접 액세스할 수 없으며 관리할 필요가 없습니다. IaaS는 데이터 센터 인프라에서 실행 되는 Vm을 설정 하 고, 구성 하 고, 관리 하는 것을 의미 합니다. 일반적인 VM 구성을 위해 미리 구성 된 VM 이미지의 갤러리를 제공 합니다. 예를 들어 Windows Server 2008, Windows Server 2012, BizTalk Server, Oracle WebLogic 서버, Oracle Database 등에 대해 미리 구성 된 VM 이미지를 설치할 수 있습니다.

Azure에서 제공 하는 PaaS 데이터 솔루션은 다음과 같습니다.

- Azure SQL Database (이전의 SQL Azure). SQL Server 기반 클라우드 관계형 데이터베이스입니다.
- Azure 테이블 저장소. 키/값 NoSQL 데이터베이스입니다.
- Azure Blob storage. 클라우드의 파일 저장소입니다.

IaaS의 경우 VM에 로드할 수 있는 모든 항목을 실행할 수 있습니다. 예를 들면 다음과 같습니다.

- 관계형 데이터베이스 (예: SQL Server, Oracle, MySQL, SQL Compact, SQLite 또는 Postgres)
- Memcached, Redis, Cassandra 및 Riak와 같은 키/값 데이터 저장소입니다.
- HBase와 같은 열 데이터 저장소
- MongoDB, RavenDB 및와 같은 문서 데이터베이스
- Neo4j와 같은 그래프 데이터베이스입니다.

![Azure의 데이터 저장소 옵션](data-storage-options/_static/image5.png)

IaaS 옵션은 거의 무제한 데이터 저장소 옵션을 제공 하며, 미리 구성 된 이미지를 사용 하 여 Vm을 만들 수 있기 때문에 대부분의 기능을 사용 하는 것이 매우 쉽습니다. 예를 들어 관리 포털에서 **Virtual Machines**로 이동 하 여 **이미지** 탭을 클릭 하 고 **VM 서비스 찾아보기**를 클릭 합니다.

![VM 서비스 검색](data-storage-options/_static/image6.png)

그러면 [미리 구성 된 vm 이미지](http://www.hanselman.com/blog/Over400VirtualMachineImagesOfOpenSourceSoftwareStacksInTheVMDepotAzureGallery.aspx)의 목록이 표시 되 고 MongoDB, Neo4J, Redis, Cassandra 또는와 같은 미리 설치 된 데이터베이스 관리 시스템이 있는 이미지에서 vm을 만들 수 있습니다.

![VM 서비스의 MongoDB](data-storage-options/_static/image7.png)

Azure는 IaaS 데이터 저장소 옵션을 최대한 쉽게 사용할 수 있도록 하지만, PaaS 제품은 많은 이점을 제공 하므로 많은 시나리오에서 더 비용 효율적이 고 실용적으로 활용할 수 있습니다.

- Vm을 만들 필요가 없으며 포털 또는 스크립트를 사용 하 여 데이터 저장소를 설정 하기만 하면 됩니다. 200 테라바이트 데이터 저장소를 원하는 경우 단추를 클릭 하거나 명령을 실행 하 고 사용할 준비가 된 시간 (초)을 선택할 수 있습니다.
- 서비스에서 사용 하는 Vm을 관리 하거나 패치할 필요가 없습니다. Microsoft에서 자동으로 작업을 수행 합니다.-확장 또는 고가용성을 위한 인프라 설정에 대해 걱정할 필요가 없습니다. Microsoft에서 모든 것을 처리 합니다.
- 라이선스를 구매할 필요가 없습니다. 라이선스 요금은 서비스 요금에 포함 되어 있습니다.
- 사용한 만큼만 요금을 지불 하면 됩니다.

Azure의 PaaS 데이터 저장소 옵션에는 타사 공급자가 제공 하는 기능이 포함 되어 있습니다. 예를 들어 Azure 스토어에서 [MongoLab 추가 기능](https://azure.microsoft.com/documentation/articles/store-mongolab-web-sites-dotnet-store-data-mongodb/) 을 선택 하 여 MongoDB Database as a Service를 프로 비전 할 수 있습니다.

## <a name="choosing-a-data-storage-option"></a>데이터 저장소 옵션 선택

모든 시나리오에 적합 한 방법은 없습니다. 이 기술이 답 이라고 표시 되는 경우에는 다른 솔루션이 서로 다른 솔루션을 최적화 하기 때문에 가장 먼저 질문 해야 합니다. 관계형 모델에는 확실 한 이점이 있습니다. 그 이유는 이러한 이유 때문입니다. 그러나 NoSQL 솔루션을 사용 하 여 해결할 수 있는 SQL에는 하위 쪽도 있습니다.

종종 가장 잘 작동 하는 것은 단일 솔루션에서 SQL 및 NoSQL을 사용 하는 compositional 접근 방식입니다. 사용자가 NoSQL을 수용 하는 [경우에도](http://basho.com/riak/) 사용자가 수행 하는 작업을 확인 하는 경우 여러 가지 nosql 프레임 워크를 사용 하는 경우가 종종 있습니다. 이러한 프레임 워크는 서로 다른 여러 nosql 프레임 [워크를 사용](http://wiki.apache.org/couchdb/Introduction) [하 고 있습니다](http://redis.io/). NoSQL을 광범위 하 게 사용 하는 Facebook도 서비스의 각 부분에 대해 서로 다른 NoSQL 프레임 워크를 사용 합니다. 데이터 저장소 접근 방식을 혼합 하 고 일치 시킬 수 있는 유연성은 여러 데이터 솔루션을 사용 하 고 단일 앱에 통합할 수 있기 때문에 클라우드에 적합 한 작업 중 하나입니다.

다음은 방법을 선택할 때 고려할 몇 가지 질문입니다.

| 데이터 의미 체계 | -핵심 데이터 저장소 및 데이터 액세스 의미 체계 (관계형 데이터 나 비구조적 데이터를 저장 하나요?) 미디어 파일과 같은 구조화 되지 않은 데이터는 blob storage에 가장 적합 합니다. 제품, 재고, 공급 업체, 고객 주문 등의 관련 데이터 컬렉션은 관계형 데이터베이스에 가장 적합 합니다. |
| --- | --- |
| 쿼리 지원 | -데이터를 얼마나 쉽게 쿼리할 수 있나요? -어떤 유형의 질문을 효율적으로 확인할 수 있나요? 키/값 데이터 저장소는 키 값이 지정 된 단일 행을 가져오는 데 매우 유용 하지만 복잡 한 쿼리에는 적합 하지 않습니다. 특정 한 사용자에 대 한 데이터를 항상 가져오는 사용자 프로필 데이터 저장소의 경우 키/값 데이터 저장소가 제대로 작동 합니다. 다양 한 제품 특성에 따라 다른 그룹화를 가져오려는 제품 카탈로그의 경우 관계형 데이터베이스가 더 효율적으로 작동할 수 있습니다. NoSQL 데이터베이스는 대량의 데이터를 효율적으로 저장할 수 있지만, 앱이 데이터를 쿼리 하는 방법에 대해 데이터베이스를 구성 해야 하며, 이렇게 하면 임시 쿼리를 수행 하기가 더 어려워집니다. 관계형 데이터베이스를 사용 하면 거의 모든 종류의 쿼리를 작성할 수 있습니다. |
| 함수 프로젝션 | -질문, 집계 등은 서버 쪽에서 실행할 수 있나요? SQL의 테이블에서 SELECT COUNT (\*)를 실행 하는 경우 서버에서 모든 작업을 효율적으로 수행 하 고 찾고 있는 수를 반환 합니다. 집계를 지원 하지 않는 NoSQL 데이터 저장소에서 동일한 계산을 원하는 경우 비효율적인 "제한 없음 쿼리" 이며 시간 초과 될 수 있습니다. 쿼리가 성공 하더라도 서버에서 클라이언트로 모든 데이터를 검색 하 고 클라이언트의 행 수를 계산 해야 합니다. -사용할 수 있는 식의 언어 또는 종류는 무엇 인가요? 관계형 데이터베이스를 사용 하면 SQL을 사용할 수 있습니다. Azure 테이블 저장소와 같은 일부 NoSQL 데이터베이스를 사용 하는 경우 [OData](http://www.odata.org/)를 사용 하 고, 기본 키를 필터링 하 고 프로젝션을 가져옵니다 (사용 가능한 필드의 하위 집합 선택). |
| 확장성의 용이성 | -데이터를 얼마나 자주 크기 조정 해야 하나요? -플랫폼에서 기본적으로 확장을 구현 합니까? -용량 (크기 및 처리량)을 추가/제거 하는 것이 얼마나 쉬운지? 관계형 데이터베이스와 테이블은 확장 가능 하도록 자동 분할 되지 않으므로 특정 제한 사항 이상으로 확장 하기가 어렵습니다. Azure 테이블 저장소와 같은 NoSQL 데이터 저장소는 기본적으로 모든 항목을 분할 하 고 파티션을 추가 하는 데는 거의 제한이 없습니다. Table Storage 최대 200 테라바이트까지 쉽게 확장할 수 있지만 Azure SQL Database의 최대 데이터베이스 크기는 500 기가바이트입니다. 관계형 데이터를 여러 데이터베이스로 분할 하 여 크기를 조정할 수 있지만 해당 모델을 지원 하도록 응용 프로그램을 설정 하려면 많은 프로그래밍 작업이 필요 합니다. |
| 계측 및 관리 효율성 | -플랫폼을 계측, 모니터링 및 관리 하는 것이 얼마나 쉬운지 확인 합니다. 데이터 저장소의 상태 및 성능에 대 한 정보를 지속적으로 파악 해야 하므로 플랫폼에서 무료로 제공 하는 메트릭과 사용자가 직접 개발 해야 하는 사항을 파악 해야 합니다. |
| 작업 | -Azure에서 플랫폼을 배포 하 고 실행 하는 것이 얼마나 쉬운지 확인 하세요. PaaS? IaaS? 용? Table Storage 및 SQL Database은 Azure에서 쉽게 설정할 수 있습니다. Azure PaaS 솔루션을 기본 제공 하지 않는 플랫폼에는 더 많은 노력이 필요 합니다. |
| API 지원 | -플랫폼을 쉽게 사용할 수 있게 해 주는 API를 사용할 수 있나요? Azure Table Service의 경우 .NET 4.5 비동기 프로그래밍 모델을 지 원하는 .NET API를 포함 하는 SDK가 있습니다. .NET 앱을 작성 하는 경우 API가 없는 다른 키/값 열 데이터 저장소 플랫폼과 비교 하 여 Azure Table Service에 대 한 코드를 작성 하 고 테스트 하는 것이 훨씬 쉽습니다. |
| 트랜잭션 무결성 및 데이터 일관성 | -데이터 일관성을 보장 하기 위해 플랫폼이 트랜잭션을 지원 하는 것이 중요 한가요? 전송 된 대량 전자 메일을 추적 하기 위해 데이터 플랫폼의 트랜잭션 또는 참조 무결성에 대 한 자동 지원 보다 성능 및 낮은 데이터 저장소 비용이 더 중요할 수 있으므로 Azure Table Service를 선택 하는 것이 좋습니다. 은행 계좌 잔액 또는 구매 주문을 추적 하는 경우 강력한 트랜잭션 보장을 제공 하는 관계형 데이터베이스 플랫폼을 선택 하는 것이 더 좋습니다. |
| 비즈니스 연속성 | -백업, 복원 및 재해 복구의 용이성 더 빨리 또는 나중에 프로덕션 데이터가 손상 되 고 실행 취소 함수가 필요 합니다. 관계형 데이터베이스는 특정 시점으로 복원 하는 기능과 같은 보다 세분화 된 복원 기능을 포함 하는 경우가 많습니다. 고려 하 고 있는 각 플랫폼에서 사용할 수 있는 복원 기능을 이해 하는 것이 중요 한 요소입니다. |
| Cost | -두 개 이상의 플랫폼에서 데이터 작업을 지원할 수 있는 경우 어떻게 비용이 어떻게 비교 되나요? 예를 들어 ASP.NET Identity 사용 하는 경우 Azure Table Service 또는 Azure SQL Database에 사용자 프로필 데이터를 저장할 수 있습니다. SQL Database의 풍부한 쿼리 기능이 필요 하지 않은 경우에는 지정 된 저장소 양에 비해 비용이 훨씬 줄어들기 때문에 Azure 테이블을 부분적으로 선택할 수 있습니다. |

일반적으로 데이터 저장소 솔루션을 선택 하기 전에 이러한 각 범주에 있는 질문에 대 한 답변을 알고 있는 것이 좋습니다.

또한 일부 플랫폼에서 다른 플랫폼 보다 더 잘 지원할 수 있는 특정 요구 사항이 워크 로드에 있을 수 있습니다. 예를 들면 다음과 같습니다.:

- 응용 프로그램에 감사 기능이 필요 한가요?
- 데이터 수명 요구 사항: 자동화 된 보관 또는 제거 기능이 필요 한가요?
- 특수 보안 요구 사항이 있나요? 예를 들어 데이터에 PII (개인적으로 식별이 가능한 정보)가 포함 되어 있지만 PII가 쿼리 결과에서 제외 되도록 할 수 있어야 합니다.
- 규정 또는 기술적인 이유로 클라우드에 저장할 수 없는 일부 데이터가 있는 경우 온-프레미스 저장소와의 통합을 용이 하 게 하는 클라우드 데이터 저장소 플랫폼이 필요할 수 있습니다.

## <a name="demo--using-sql-database-in-azure"></a>데모 – Azure에서 SQL Database 사용

Fix It 앱은 관계형 데이터베이스를 사용 하 여 작업을 저장 합니다. [모든 항목 자동화 단원](automate-everything.md) 에 표시 된 환경 만들기 Windows PowerShell 스크립트는 두 개의 SQL Database 인스턴스를 만듭니다. 포털에서 **SQL 데이터베이스** 탭을 클릭 하 여 이러한 항목을 볼 수 있습니다.

![포털의 SQL 데이터베이스](data-storage-options/_static/image8.png)

포털을 사용 하 여 쉽게 데이터베이스를 만들 수 있습니다.

**새로 만들기--Data Services** -- **SQL Database** -- **빠른 생성**을 클릭 하 고, 데이터베이스 이름을 입력 하거나, 계정에 이미 있는 서버를 선택 하거나, 새로 만들기를 클릭 하 고 **SQL Database 만들기**를 클릭 합니다.

![새 SQL Database](data-storage-options/_static/image9.png)

몇 초 정도 기다렸다가 Azure에서 데이터베이스를 사용할 준비가 되었습니다.

![새 SQL Database 만들어짐](data-storage-options/_static/image10.png)

따라서 Azure는 몇 초 내에 온-프레미스 환경에서 수행 하는 데 하루 또는 일주일 이상 걸릴 수 있습니다. 또는 관리 API를 사용 하 여 쉽게 데이터베이스를 자동으로 만들 수 있으므로 응용 프로그램이 프로그래밍 된 경우에만 여러 데이터베이스에 데이터를 분산 하 여 동적으로 확장할 수 있습니다.

이는 플랫폼별 모델의 예입니다. 서버를 관리할 필요는 없습니다. 백업에 대해 걱정 하지 않아도 됩니다. 고가용성에서 실행 중입니다. 데이터베이스의 데이터는 3 개의 서버에 자동으로 복제 됩니다. 컴퓨터가 중지 되 면 자동으로 장애 조치 (failover) 되 고 데이터가 손실 됩니다. 서버에 정기적으로 패치가 적용 되므로 걱정할 필요가 없습니다.

단추를 클릭 하면 필요한 정확한 연결 문자열이 표시 되 고 새 데이터베이스를 사용 하 여 즉시 시작할 수 있습니다.

![연결 문자열](data-storage-options/_static/image11.png)

대시보드는 사용 된 연결 기록과 저장소의 양을 보여 줍니다.

![SQL Database 대시보드](data-storage-options/_static/image12.png)

포털에서 또는 SQL Server Management Studio (SSMS) 및 Visual Studio tools SQL Server 개체 탐색기 (SSOX) 및 서버 탐색기를 포함 하 여 이미 익숙한 SQL Server 도구를 사용 하 여 데이터베이스를 관리할 수 있습니다.

![SSOX](data-storage-options/_static/image13.png)

또 다른 좋은 점은 가격 책정 모델입니다. 무료 20mb 데이터베이스를 사용 하 여 개발을 시작할 수 있으며 프로덕션 데이터베이스는 매달 약 $5에 시작 됩니다. 최대 용량이 아니라 데이터베이스에 실제로 저장 된 데이터의 양에 대해서만 비용을 지불 합니다. 라이선스를 구입할 필요가 없습니다.

SQL Database은 쉽게 확장할 수 있습니다. Fix It 앱의 경우 자동화 스크립트에서 만든 데이터베이스는 1 4gb에 있습니다. 150 4gb 크기를 조정 하려는 경우 포털로 이동 하 여 해당 설정을 변경 하거나 REST API 명령을 실행 하 고, 데이터를 배포할 수 있는 150 4gb 데이터베이스가 있을 수 있습니다.

![SQL Database 버전 및 크기](data-storage-options/_static/image14.png)

이는 인프라를 빠르고 쉽게 사용 하 고 즉시 사용 하기 시작 하는 클라우드 기능입니다.

Fix It 앱은 멤버 자격 (인증 및 권한 부여) 및 데이터에 대 한 두 개의 SQL 데이터베이스를 사용 하며,이를 프로 비전 하 고 크기를 조정 하는 데 필요한 모든 작업을 수행 해야 합니다. 이전에는 Windows PowerShell 스크립트를 통해 데이터베이스를 프로 비전 하는 방법을 알아보았습니다. 이제 포털에서 작업을 수행 하는 방법을 살펴보았습니다.

## <a name="entity-framework-versus-direct-database-access-using-adonet"></a>ADO.NET를 사용 하 여 데이터베이스에 대 한 직접 액세스 및 Entity Framework

Fix It 앱은 Entity Framework를 사용 하 여 이러한 데이터베이스에 액세스 하며 .NET 응용 프로그램에 대해 Microsoft에서 권장 하는 ORM (개체-관계형 매퍼)을 사용 합니다. ORM은 개발자의 생산성을 용이 하 게 하는 훌륭한 도구 이지만 일부 시나리오에서는 생산성이 저하 될 수 있습니다. 실제 클라우드 앱에서는 EF를 사용 하거나 직접 ADO.NET를 사용 하도록 선택 하지 않습니다. 둘 다 사용 합니다. 데이터베이스에서 작동 하는 코드를 작성 하는 대부분의 경우, 최대 성능 가져오기는 중요 하지 않으며 Entity Framework를 사용 하 여 얻을 수 있는 간소화 된 코딩 및 테스트 기능을 활용할 수 있습니다. EF 오버 헤드로 인해 성능이 저하 되지 않는 경우 저장 프로시저를 호출 하 여 ADO.NET를 사용 하 여 고유한 쿼리를 작성 하 고 실행할 수 있습니다.

데이터베이스에 액세스 하는 데 사용 하는 방법에 관계 없이 "데이터 전송량"를 최대한 최소화 하는 것이 좋습니다. 즉, 수십 개 또는 수백 개의 작은 쿼리 결과 집합에 필요한 모든 데이터를 가져올 수 있는 경우 일반적으로 더 좋습니다. 예를 들어 학생 및 등록 된 강의를 나열 해야 하는 경우 일반적으로 하나의 쿼리에서 학생을 가져오고 각 학생의 교육 과정에 대해 별도의 쿼리를 실행 하는 대신 하나의 조인 쿼리로 모든 데이터를 가져오는 것이 좋습니다.

## <a name="sql-databases-and-the-entity-framework-in-the-fix-it-app"></a>Fix It 앱의 SQL database 및 Entity Framework

Fix It 앱에서 Entity Framework `DbContext` 클래스에서 파생 되는 `FixItContext` 클래스는 데이터베이스를 식별 하 고 데이터베이스의 테이블을 지정 합니다. 컨텍스트는 태스크에 대 한 엔터티 집합 (테이블)을 지정 하 고, 코드는 연결 문자열 이름을 컨텍스트에 전달 합니다. 이 이름은 web.config 파일에 정의 된 연결 문자열을 참조 합니다.

[!code-csharp[Main](data-storage-options/samples/sample1.cs?highlight=4,8)]

*Web.config 파일의* 연결 문자열은 appdb로 이름이 지정 됩니다 (여기서는 로컬 개발 데이터베이스를 가리키기).

[!code-xml[Main](data-storage-options/samples/sample2.xml?highlight=3)]

Entity Framework `FixItTask` 엔터티 클래스에 포함 된 속성을 기반으로 *Fixittasks* 테이블을 만듭니다. 이 클래스는 단순 POCO (일반 이전 CLR 개체) 클래스 이며이 클래스는 Entity Framework에서 상속 되거나 종속성이 없는 것을 의미 합니다. 그러나이를 기반으로 테이블을 만들고이를 사용 하 여 CRUD (만들기-읽기-업데이트-삭제) 작업을 실행 하는 방법을 알고 Entity Framework.

[!code-csharp[Main](data-storage-options/samples/sample3.cs)]

![FixItTasks 테이블](data-storage-options/_static/image15.png)

Fix It 앱은 데이터 저장소에서 작업 하는 CRUD 작업에 사용 하는 리포지토리 인터페이스를 포함 합니다.

[!code-csharp[Main](data-storage-options/samples/sample4.cs)]

리포지토리 메서드는 모두 async 이므로 완전히 비동기 방식으로 모든 데이터 액세스를 수행할 수 있습니다.

리포지토리 구현은 LINQ 쿼리 뿐만 아니라 삽입, 업데이트 및 삭제 작업을 비롯 하 여 데이터 작업을 수행 하기 위해 비동기 메서드 Entity Framework를 호출 합니다. Fix It 작업을 조회 하는 코드의 예는 다음과 같습니다.

[!code-csharp[Main](data-storage-options/samples/sample5.cs)]

여기에서 몇 가지 타이밍 및 오류 로깅 코드도 확인할 수 있습니다 .이에 대해서는 나중에 [모니터링 및 원격 분석 챕터](monitoring-and-telemetry.md)에서 살펴볼 것입니다.

<a id="sqliaas"></a>
## <a name="choosing-sql-database-paas-versus-sql-server-in-a-vm-iaas-in-azure"></a>Azure의 VM (IaaS)에서 SQL Database (PaaS) 및 SQL Server 선택

SQL Server 및 Azure SQL Database에 대 한 좋은 점은 두 가지 모두에 대 한 핵심 프로그래밍 모델이 동일 하다는 것입니다. 두 환경 모두에서 동일한 기술을 대부분 사용할 수 있습니다. 개발에 SQL Server 데이터베이스를 사용 하 고 클라우드에서 SQL Database 인스턴스를 사용할 수도 있습니다 .이는 It 앱을 수정 하는 방법입니다.

대 안으로, IaaS Vm에 설치 하 여 온-프레미스에서 실행 하는 클라우드에서 동일한 SQL Server를 실행할 수 있습니다. 일부 레거시 응용 프로그램의 경우 VM에서 SQL Server를 실행 하는 것이 더 나은 솔루션 일 수 있습니다. SQL Server 데이터베이스는 전용 VM에서 실행 되기 때문에 공유 서버에서 실행 되는 SQL Database 데이터베이스 보다 더 많은 리소스를 사용할 수 있습니다. 즉, SQL Server 데이터베이스가 더 커질 수 있으며 여전히 잘 수행 될 수 있습니다. 일반적으로 데이터베이스 크기와 테이블 크기가 작을수록 사용 사례가 PaaS (SQL Database)에 대해 더 효율적으로 작동 합니다.

다음은 두 모델 중에서 선택 하는 방법에 대 한 몇 가지 지침입니다.

| Azure SQL Database (PaaS) | 가상 컴퓨터 (IaaS)의 SQL Server |
| --- | --- |
| **장점** -vm을 만들거나 관리할 필요가 없으며, OS 또는 SQL을 업데이트 하거나 패치할 필요가 없습니다. Azure는 사용자를 위해이를 수행 합니다. -데이터베이스 수준 SLA를 사용 하 여 기본 제공 되는 고가용성 -사용한 양만큼만 요금을 지불 하기 때문에 TCO (총 소유 비용)가 부족 합니다 (라이선스 필요 없음). -많은 수의 작은 데이터베이스를 처리 하는 데 적합 합니다 (&lt;= 500 GB). -쉽게 확장할 수 있도록 새 데이터베이스를 동적으로 만들 수 있습니다. | ***전문가*** -온-프레미스 SQL Server와 호환 가능 합니다. -VM 수준 SLA를 사용 하 여 2 개 이상의 Vm에서 [AlwaysOn을 통해 SQL Server 고가용성](https://www.microsoft.com/sqlserver/solutions-technologies/mission-critical-operations/high-availability.aspx) 을 구현할 수 있습니다. -SQL을 관리 하는 방법을 완전히 제어할 수 있습니다. -이미 소유 하 고 있는 SQL 라이선스를 다시 사용 하거나 1 시간을 기준으로 요금을 지불할 수 있습니다. -더 적거나 큰 (1TB 이상) 데이터베이스를 처리 하는 데 적합 합니다. |
| **단점** -온-프레미스 SQL Server ( [CLR 통합](https://technet.microsoft.com/library/ms131102.aspx), [tde](https://technet.microsoft.com/library/bb934049.aspx), [압축 지원](https://technet.microsoft.com/library/cc280449.aspx), [SQL Server Reporting Services](https://technet.microsoft.com/library/ms159106.aspx)등)에 비해 몇 가지 기능 간격이 며 데이터베이스 크기 제한은 500gb입니다. | ***단점*** -업데이트/패치 (OS 및 SQL)는 사용자의 책임을 생성 하 고 관리 합니다. 즉, 디스크 IOPS (초당 입력/출력 작업)는 약 8000 (16 개의 데이터 드라이브를 통해)로 제한 됩니다. |

VM에서 SQL Server를 사용 하려는 경우 고유한 SQL Server 라이선스를 사용 하거나 1 시간 단위로 요금을 지불할 수 있습니다. 예를 들어 포털에서 또는 REST API를 통해 SQL Server 이미지를 사용 하 여 새 VM을 만들 수 있습니다.

![SQL Server를 사용 하 여 VM 만들기](data-storage-options/_static/image16.png)

![SQL Server VM 이미지 목록](data-storage-options/_static/image17.png)

SQL Server 이미지를 사용 하 여 VM을 만들 때 VM 사용에 따라 시간당 SQL Server 라이선스 비용을 평가 합니다. 몇 달 동안만 실행 되는 프로젝트의 경우 시간 단위로 요금을 지불 하는 것이 더 저렴 합니다. 프로젝트를 몇 년 동안 지속 한다고 생각 하는 경우 정상적으로 라이선스를 구입 하는 것이 더 저렴 합니다.

## <a name="summary"></a>요약

클라우드 컴퓨팅을 사용 하면 응용 프로그램의 요구 사항에 가장 적합 한 데이터 저장소 접근 방식을 조합 하 고 일치 시킬 수 있습니다. 새 응용 프로그램을 작성 하는 경우 응용 프로그램이 늘어날 때 계속 해 서 잘 작동 하는 방식을 선택 하기 위해 여기에 나열 된 질문에 대해 신중 하 게 생각 합니다. [다음 장에서](data-partitioning-strategies.md) 는 여러 데이터 저장소 접근 방식을 결합 하는 데 사용할 수 있는 몇 가지 분할 전략을 설명 합니다.

## <a name="resources"></a>자료

자세한 내용은 다음 리소스를 참조하세요.

데이터베이스 플랫폼 선택:

- [확장성이 뛰어난 솔루션에 대 한 데이터 액세스: SQL, NoSQL 및 Polyglot 지 속성 사용](https://aka.ms/dag-doc). 클라우드 응용 프로그램에 사용할 수 있는 다양 한 종류의 데이터 저장소를 심층적으로 다루는 Microsoft 패턴 및 관행을 기준으로 한 전자 서적입니다.
- [Microsoft 패턴 및 사례-Azure 지침](https://msdn.microsoft.com/library/ff898430.aspx) 데이터 일관성 입문, 데이터 복제 및 동기화 지침, 인덱스 테이블 패턴, 구체화 된 뷰 패턴을 참조 하세요.
- [BASE: Acid 대안](http://queue.acm.org/detail.cfm?id=1394128)입니다. 데이터 일관성과 확장성 간의 장단점에 대 한 문서입니다.
- [7 주 동안의 7 주 데이터베이스: 최신 데이터베이스와 NoSQL 이동에 대 한 가이드](https://www.amazon.com/Seven-Databases-Weeks-Modern-Movement/dp/1934356921)입니다. Eric Redmond 및 승 Wilson를 통합 합니다. 현재 사용할 수 있는 데이터 저장소 플랫폼의 범위를 소개 하는 데 매우 권장 됩니다.

SQL Server와 SQL Database 중에서 선택 합니다.

- [프리미엄 미리 보기 SQL Database 지침을](https://msdn.microsoft.com/library/windowsazure/dn369873.aspx)제공 합니다. SQL Database Premium 소개 및 SQL Database Web 및 Business edition에서 선택 하는 시기에 대 한 지침을 제공 합니다.
- [지침 및 제한 사항 (Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx). SQL Database에서 지원 하지 않는 기능 SQL Server에 초점을 맞춘 SQL Database의 제한 사항에 대 한 설명서에 연결 되는 포털 페이지입니다.
- [Azure Virtual Machines에서 SQL Server](https://msdn.microsoft.com/library/windowsazure/jj823132.aspx)합니다. Azure에서 SQL Server를 실행 하는 방법에 대 한 설명서에 연결 되는 포털 페이지입니다.
- [Scott Guthrie는 Azure의 SQL 데이터베이스에 대해 설명](https://azure.microsoft.com/documentation/videos/sql-in-azure-scottgu/)합니다. Scott Guthrie의 SQL Database에 대 한 6 분 비디오 소개.
- [Azure Virtual Machines에서 SQL Server에 대 한 응용 프로그램 패턴 및 개발 전략](https://msdn.microsoft.com/library/windowsazure/dn574746.aspx)

ASP.NET 웹 앱의 Entity Framework 및 SQL Database 사용

- [MVC 5를 사용 하 여 EF 6 시작](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) EF를 사용 하 고 데이터베이스를 Azure에 배포 하 고 SQL Database 하는 MVC 앱을 빌드하는 과정을 안내 하는 9 부 자습서 시리즈입니다.
- [Visual Studio를 사용 하 여 웹 배포를 ASP.NET](../../../../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). EF Code First를 사용 하 여 데이터베이스를 배포 하는 방법에 대해 자세히 설명 하는 12 부 자습서 시리즈입니다.
- [멤버 자격, OAuth 및 SQL Database가 포함 된 보안 ASP.NET MVC 5 앱을 Azure 웹 사이트에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)합니다. 인증을 사용 하는 웹 앱을 만들고, 멤버 자격 데이터베이스에 응용 프로그램 테이블을 저장 하 고, 데이터베이스 스키마를 수정 하 고, 앱을 Azure에 배포 하는 과정을 안내 하는 단계별 자습서입니다.
- [ASP.NET Data Access Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282414). EF 및 SQL Database을 사용 하기 위한 리소스에 대 한 링크입니다.

Azure에서 MongoDB 사용:

- [MongoLab-Azure의 MongoDB](http://msopentech.com/opentech-projects/mongolab-mongodb-on-windows-azure/). Azure에서 MongoDB를 실행 하는 방법에 대 한 설명서를 위한 포털 페이지입니다.
- [Azure의 가상 머신에서 실행 되는 MongoDB에 연결 하는 azure 웹 사이트를 만듭니다](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-store-data-mongodb-vm/). ASP.NET 웹 응용 프로그램에서 MongoDB 데이터베이스를 사용 하는 방법을 보여 주는 단계별 자습서입니다.

HDInsight (Azure의 Hadoop):

- [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/). [Azure](https://azure.microsoft.com/) 웹 사이트에서 HDInsight 설명서를 참조 하세요.
- [Hadoop 및 HDInsight: Azure의 빅 데이터](https://msdn.microsoft.com/magazine/dn385705.aspx). Azure에서 Hadoop을 소개 하는 Bruno Terkaly 및 Ricardo Villalobos의 MSDN Magazine 문서입니다.
- [Microsoft 패턴 및 사례-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx) MapReduce 패턴을 참조 하세요.

> [!div class="step-by-step"]
> [이전](single-sign-on.md)
> [다음](data-partitioning-strategies.md)
