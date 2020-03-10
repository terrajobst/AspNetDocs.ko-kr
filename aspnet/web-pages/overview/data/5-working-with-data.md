---
uid: web-pages/overview/data/5-working-with-data
title: ASP.NET 웹 페이지 (Razor) 사이트에서 데이터베이스 작업 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 데이터베이스의 데이터에 액세스 하 고 ASP.NET 웹 페이지를 사용 하 여 표시 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 45e988d037465e59ad352bb9444af2c69fd3cd70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474041"
---
# <a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 데이터베이스 작업 소개

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Microsoft WebMatrix 도구를 사용 하 여 Razor (ASP.NET 웹 페이지) 웹 사이트에서 데이터베이스를 만드는 방법과 데이터를 표시, 추가, 편집 및 삭제할 수 있는 페이지를 만드는 방법을 설명 합니다.
> 
> **학습 내용:** 
> 
> - 데이터베이스를 만드는 방법
> - 데이터베이스에 연결 하는 방법
> - 웹 페이지에 데이터를 표시 하는 방법
> - 데이터베이스 레코드를 삽입, 업데이트 및 삭제 하는 방법입니다.
> 
> 다음은이 문서에 도입 된 기능입니다.
> 
> - Microsoft SQL Server Compact Edition 데이터베이스 작업
> - SQL 쿼리 작업
> - `Database` 클래스입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 2
>   
> 
> 이 자습서는 WebMatrix 3 에서도 작동 합니다. ASP.NET 웹 페이지 3과 Visual Studio 2013 (또는 웹의 경우 2013 Visual Studio Express)를 사용할 수 있습니다. 그러나 사용자 인터페이스는 다릅니다.

## <a name="introduction-to-databases"></a>데이터베이스 소개

일반적인 주소록을 상상해 보세요. 주소록의 각 항목에 대해 (즉, 각 사람에 대 한) 이름, 성, 주소, 전자 메일 주소 및 전화 번호와 같은 여러 정보를 사용할 수 있습니다.

이와 같이 데이터를 그림 하는 일반적인 방법은 행과 열이 있는 테이블입니다. 데이터베이스 용어로 각 행을 레코드 라고 합니다. 각 열 (필드 라고도 함)에는 각 데이터 형식에 대 한 값 (이름, 성 등)이 포함 되어 있습니다.

| **ID** | **FirstName** | **LastName** | **주소** | **Email** | **전화** |
| --- | --- | --- | --- | --- | --- |
| 1 | Jim | Abrus | 210 100th St SE Orcas WA 98031 | jim@contoso.com | 555 0100 |
| 2 | Terry | Adams | 1234 Main St. Seattle WA 99011 | terry@cohowinery.com | 555 0101 |

대부분의 데이터베이스 테이블에 대해 테이블에는 고객 번호, 계좌 번호 등과 같은 고유 식별자가 포함 된 열이 있어야 합니다. 이를 테이블의 *기본 키*라고 하며 테이블의 각 행을 식별 하는 데 사용 합니다. 이 예에서 ID 열은 주소록의 기본 키입니다.

데이터베이스에 대 한 기본적인 이해를 통해 간단한 데이터베이스를 만들고 데이터 추가, 수정 및 삭제와 같은 작업을 수행 하는 방법을 배울 준비가 되었습니다.

> [!TIP] 
> 
> **관계형 데이터베이스**
> 
> 텍스트 파일 및 스프레드시트를 비롯 한 다양 한 방법으로 데이터를 저장할 수 있습니다. 그러나 대부분의 비즈니스에서는 데이터가 관계형 데이터베이스에 저장 됩니다.
> 
> 이 문서는 데이터베이스에 대해 그다지 복잡 하지 않습니다. 그러나이에 대 한 이해를 최소화 하는 것이 유용할 수 있습니다. 관계형 데이터베이스에서 정보는 논리적으로 개별 테이블로 나뉩니다. 예를 들어 school 데이터베이스에는 학생 및 수업 제공을 위한 별도의 테이블이 포함 될 수 있습니다. 데이터베이스 소프트웨어 (예: SQL Server)는 테이블 간의 관계를 동적으로 설정할 수 있는 강력한 명령을 지원 합니다. 예를 들어 관계형 데이터베이스를 사용 하 여 일정을 만들기 위해 학생 및 수업 간의 논리적 관계를 설정할 수 있습니다. 별도의 테이블에 데이터를 저장 하면 테이블 구조의 복잡성이 줄어들고 테이블에 중복 데이터를 보관할 필요성이 줄어듭니다.

## <a name="creating-a-database"></a>데이터베이스 만들기

이 절차에서는 WebMatrix에 포함 된 SQL Server Compact 데이터베이스 디자인 도구를 사용 하 여 SmallBakery 라는 데이터베이스를 만드는 방법을 보여 줍니다. 코드를 사용 하 여 데이터베이스를 만들 수 있지만 WebMatrix와 같은 디자인 도구를 사용 하 여 데이터베이스와 데이터베이스 테이블을 만드는 것이 더 일반적입니다.

1. WebMatrix를 시작 하 고 빠른 시작 페이지에서 **템플릿에서 사이트**를 클릭 합니다.
2. **빈 사이트**를 선택 하 고 **사이트 이름** 상자에 "SmallBakery"를 입력 한 다음 **확인을**클릭 합니다. 사이트가 만들어지고 WebMatrix에 표시 됩니다.
3. 왼쪽 창에서 **데이터베이스** 작업 영역을 클릭 합니다.
4. 리본에서 **새 데이터베이스**를 클릭 합니다. 사이트와 같은 이름을 사용 하 여 빈 데이터베이스를 만듭니다.
5. 왼쪽 창에서 **SmallBakery** 노드를 확장 한 다음 **테이블**을 클릭 합니다.
6. 리본에서 **새 테이블**을 클릭 합니다. WebMatrix 테이블 디자이너를 엽니다.

    ![[이미지]](5-working-with-data/_static/image1.jpg)
7. **이름** 열을 클릭 하 고 &quot;Id&quot;을 입력 합니다.
8. **데이터 형식** 열에서 **int**를 선택 합니다.
9. **기본 키** 로 설정 하 고 **확인?** 옵션을 **예**로 설정 합니다.

    이름에서 알 수 있듯이 **은 기본 키** 로 데이터베이스에 테이블의 기본 키가 되도록 합니다. **Id는** 데이터베이스에 모든 새 레코드에 대 한 ID 번호를 자동으로 만들고 1부터 시작 하 여 다음 일련 번호를 할당 하도록 지시 합니다.
10. 다음 행을 클릭 합니다. 편집기에서 새 열 정의를 시작 합니다.
11. 이름 값에&quot;&quot;이름을 입력 합니다.
12. **데이터 형식**에서 &quot;nvarchar&quot;를 선택 하 고 길이를 50으로 설정 합니다. `nvarchar`의 *var* 부분은이 열에 대 한 데이터가 레코드에 대 한 레코드에 따라 달라질 수 있는 문자열이 되도록 데이터베이스에 지시 합니다. *N* 접두사는 *국가*를 나타내며,이 필드는 영문자 또는 쓰기 시스템 &#8212; 을 나타내는 문자 데이터를 보유할 수 있습니다. 즉, 필드에 유니코드 데이터가 포함 되어 있음을 나타냅니다.
13. **Null 허용** 옵션을 **아니요**로 설정 합니다. 이렇게 하면 *이름* 열이 비어 있지 않은 상태로 유지 됩니다.
14. 이와 동일한 프로세스를 사용 하 여 *Description*이라는 열을 만듭니다. **데이터 형식을** "nvarchar"로 설정 하 고 길이를 50로 설정 하 고 **null 허용** 을 false로 설정 합니다.
15. *Price*라는 열을 만듭니다. **데이터 형식을 "money"로** 설정 하 고 **null 허용** 을 false로 설정 합니다.
16. 맨 위에 있는 상자에서 Product&quot;&quot;테이블 이름을로 합니다.

    완료 되 면 정의가 다음과 같이 표시 됩니다.

    ![[이미지]](5-working-with-data/_static/image2.png)
17. Ctrl + S를 눌러 테이블을 저장 합니다.

## <a name="adding-data-to-the-database"></a>데이터베이스에 데이터 추가

이제이 문서의 뒷부분에서 작업할 몇 가지 샘플 데이터를 데이터베이스에 추가할 수 있습니다.

1. 왼쪽 창에서 **SmallBakery** 노드를 확장 한 다음 **테이블**을 클릭 합니다.
2. Product 테이블을 마우스 오른쪽 단추로 클릭 한 다음 **데이터**를 클릭 합니다.
3. 편집 창에서 다음 레코드를 입력 합니다.

    | **이름** | **설명** | **Price** |
    | --- | --- | --- |
    | 빵 | 매일 새로 구운. | 2.99 |
    | Strawberry 디저트 | 유기적 딸기를 사용 하 여 정원에서 만든 것입니다. | 9.99 |
    | Apple 원형 | 두 번째는 mom 원형에만 해당 됩니다. | 12.99 |
    | Pecan 원형 | Pecans 마음에 들면이는 사용자를 위한 것입니다. | 10.99 |
    | 레몬 원형 | 세계 최고의 lemons. | 11.99 |
    | 컵케이크 | 어린이와 어린이는이를 좋아합니다. | 7.99 |

    *Id* 열에는 아무것도 입력할 필요가 없습니다. *Id* 열을 만들 때 **Is Identity** 속성을 true로 설정 하면 자동으로 채워집니다.

    데이터 입력을 마치면 테이블 디자이너는 다음과 같이 표시 됩니다.

    ![[이미지]](5-working-with-data/_static/image3.jpg)
4. 데이터베이스 데이터를 포함 하는 탭을 닫습니다.

## <a name="displaying-data-from-a-database"></a>데이터베이스에서 데이터 표시

데이터를 포함 하는 데이터베이스가 있으면 ASP.NET 웹 페이지에 데이터를 표시할 수 있습니다. 표시할 테이블 행을 선택 하려면 데이터베이스에 전달 하는 명령에 해당 하는 SQL 문을 사용 합니다.

1. 왼쪽 창에서 **파일** 작업 영역을 클릭 합니다.
2. 웹 사이트의 루트에서 *Listproducts. cshtml*이라는 새 CSHTML 페이지를 만듭니다.
3. 기존 태그를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    첫 번째 코드 블록에서 이전에 만든 *SmallBakery* 파일 (데이터베이스)을 엽니다. `Database.Open` 메서드는 *.sdf* 파일이 웹 사이트의 *앱\_데이터* 폴더에 있는 것으로 가정 합니다. 실제로 *.sdf* 확장명 &#8212; 을 지정할 필요는 없습니다. 이렇게 하면 `Open` 방법이 작동 하지 않습니다.

    > [!NOTE]
    > *앱\_데이터* 폴더는 데이터 파일을 저장 하는 데 사용 되는 ASP.NET의 특수 폴더입니다. 자세한 내용은이 문서의 뒷부분에 나오는 [데이터베이스에 연결](#SB_ConnectingToADatabase) 을 참조 하세요.

    그런 다음, 다음 SQL `Select` 문을 사용 하 여 데이터베이스 쿼리 요청을 만듭니다.

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    문에서 `Product`는 쿼리할 테이블을 식별 합니다. `*` 문자는 쿼리에서 테이블의 모든 열을 반환 하도록 지정 합니다. 열을 일부만 표시 하려는 경우 열을 쉼표로 구분 하 여 나열할 수도 있습니다. `Order By` 절은 *이름* 열을 기준으로이 경우 &#8212; 데이터를 정렬 하는 방법을 나타냅니다. 즉, 각 행에 대 한 *Name* 열의 값을 기준으로 데이터를 사전순으로 정렬 합니다.

    페이지 본문에서 태그는 데이터를 표시 하는 데 사용 되는 HTML 테이블을 만듭니다. `<tbody>` 요소 내에서 `foreach` 루프를 사용 하 여 쿼리에서 반환 되는 각 데이터 행을 개별적으로 가져옵니다. 각 데이터 행에 대해 HTML 테이블 행 (`<tr>` 요소)을 만듭니다. 그런 다음 각 열에 대해 HTML 테이블 셀 (`<td>` 요소)을 만듭니다. 루프를 진행할 때마다 데이터베이스에서 사용할 수 있는 다음 행이 `row` 변수에 있습니다 (`foreach` 문에서이를 설정). 행에서 개별 열을 가져오기 위해 `row.Name` 또는 `row.Description` 또는 원하는 열 이름을 사용할 수 있습니다.
4. 브라우저에서 페이지를 실행 합니다. (파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.) 이 페이지에는 다음과 같은 목록이 표시 됩니다.

    ![[이미지]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> **SQL(구조적 쿼리 언어)**
> 
> SQL은 데이터베이스에서 데이터를 관리 하기 위한 대부분의 관계형 데이터베이스에 사용 되는 언어입니다. 여기에는 데이터를 검색 하 고 업데이트 하는 데 사용할 수 있는 명령이 포함 되어 있으며,이를 통해 데이터베이스 테이블을 만들고 수정 하 고 관리할 수 있습니다. Sql은 SQL을 사용 하 여 사용자가 원하는 것을 데이터베이스에 알려 주므로 데이터를 가져오는 방법이 나 작업을 수행 하는 방법을 파악 하기 위한 데이터베이스 작업 이라는 점을 제외 하 고, sql은 WebMatrix에서 사용 중인 프로그래밍 언어와는 다릅니다. 다음은 몇 가지 SQL 명령의 예입니다.
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> *Price* 값이 10 보다 많은 경우 *Product* 테이블의 레코드에서 *Id*, *이름*및 *가격* 열을 페치하고 *이름* 열의 값을 기준으로 결과를 사전순으로 반환 합니다. 이 명령은 조건을 충족 하는 레코드를 포함 하는 결과 집합을 반환 하거나, 일치 하는 레코드가 없는 경우 빈 집합을 반환 합니다.
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> *Product* 테이블에 새 레코드를 삽입 하 고 *Name* 열을 &quot;크 라 상&quot;로 설정 하 고 *설명* 열에 부실 즐거움&quot;를 &quot;하 고 price를 1.99으로 설정 합니다.
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> 이 명령은 만료 날짜 열이 2008 년 1 월 1 일 이전인 *Product* 테이블의 레코드를 삭제 합니다. 이 경우 *Product* 테이블에 이러한 열이 있다고 가정 합니다. 날짜는 여기에 MM/DD/YYYY 형식으로 입력 되지만 로캘에 사용 되는 형식으로 입력 해야 합니다.
> 
> `Insert Into` 및 `Delete` 명령은 결과 집합을 반환 하지 않습니다. 대신 명령의 영향을 받은 레코드 수를 나타내는 숫자를 반환 합니다.
> 
> 이러한 작업 중 일부 (예: 레코드 삽입 및 삭제)의 경우 작업을 요청 하는 프로세스에 데이터베이스에 대 한 적절 한 권한이 있어야 합니다. 따라서 프로덕션 데이터베이스의 경우 데이터베이스에 연결할 때 사용자 이름과 암호를 제공 해야 하는 경우가 많습니다.
> 
> 수십 개의 SQL 명령이 있지만 모두 이와 같은 패턴을 따릅니다. SQL 명령을 사용 하 여 데이터베이스 테이블을 만들고, 테이블의 레코드 수를 계산 하 고, 가격을 계산 하 고, 더 많은 작업을 수행할 수 있습니다.

## <a name="inserting-data-in-a-database"></a>데이터베이스에 데이터 삽입

이 섹션에서는 사용자가 *제품* 데이터베이스 테이블에 새 제품을 추가할 수 있는 페이지를 만드는 방법을 보여 줍니다. 새 제품 레코드를 삽입 한 후에는 이전 섹션에서 만든 *Listproducts. cshtml* 페이지를 사용 하 여 업데이트 된 테이블이 페이지에 표시 됩니다.

이 페이지에는 사용자가 입력 하는 데이터가 데이터베이스에 대해 유효한 지 확인 하기 위한 유효성 검사가 포함 되어 있습니다. 예를 들어 페이지의 코드를 사용 하면 모든 필수 열에 대해 값이 입력 되었는지 확인할 수 있습니다.

1. 웹 사이트에서 이름이 *Insertproducts. cshtml*인 새 CSHTML 파일을 만듭니다.
2. 기존 태그를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    페이지 본문에는 사용자가 이름, 설명 및 가격을 입력할 수 있는 세 개의 텍스트 상자를 포함 하는 HTML 폼이 포함 되어 있습니다. 사용자가 **삽입** 단추를 클릭 하면 페이지 맨 위에 있는 코드가 *SmallBakery* 데이터베이스에 대 한 연결을 엽니다. 그런 다음 `Request` 개체를 사용 하 여 사용자가 제출한 값을 가져와 로컬 변수에 할당 합니다.

    사용자가 각 필수 열에 대 한 값을 입력 했는지 확인 하려면 유효성 검사를 수행 하려는 각 `<input>` 요소를 등록 합니다.

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    `Validation` 도우미는 등록 한 각 필드에 값이 있는지 확인 합니다. 사용자가 가져오는 정보를 처리 하기 전에 일반적으로 수행 하는 `Validation.IsValid()`를 확인 하 여 모든 필드가 유효성 검사를 통과 했는지 여부를 테스트할 수 있습니다.

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    `&&` 연산자는 및를 의미 합니다 .이 테스트는 *이 형식이 양식 전송 이며 모든 필드가 유효성 검사를 통과 한 경우*에 해당 합니다.

    유효성을 검사 한 모든 열이 비어 있지 않은 경우 계속 진행 하 여 데이터를 삽입 하는 SQL 문을 만들고 다음 그림과 같이 실행 합니다.

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    삽입할 값에 대 한 매개 변수 자리 표시자 (`@0`, `@1`, `@2`)를 포함 합니다.

    > [!NOTE]
    > 보안 예방 조치로, 앞의 예제에서와 같이 매개 변수를 사용 하 여 항상 값을 SQL 문에 전달 합니다. 이렇게 하면 사용자 데이터의 유효성을 검사할 수 있을 뿐만 아니라 데이터베이스에 악성 명령을 전송 하려는 시도를 방지할 수 있습니다 (종종 SQL 삽입 공격 이라고 함).

    쿼리를 실행 하려면이 문을 사용 하 여 자리 표시자를 대체할 값을 포함 하는 변수를 전달 합니다.

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    `Insert Into` 문을 실행 한 후에는 다음 줄을 사용 하 여 제품을 나열 하는 페이지로 사용자를 보냅니다.

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    유효성 검사가 성공 하지 못한 경우 삽입을 건너뜁니다. 대신 누적 된 오류 메시지 (있는 경우)를 표시할 수 있는 도우미가 페이지에 있습니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    태그의 스타일 블록에는 `.validation-summary-errors`라는 CSS 클래스 정의가 포함 되어 있습니다. 유효성 검사 오류를 포함 하는 `<div>` 요소에 대해 기본적으로 사용 되는 CSS 클래스의 이름입니다. 이 경우 CSS 클래스는 유효성 검사 요약 오류가 빨강 및 굵게 표시 되도록 지정 하지만 원하는 서식을 표시 하는 `.validation-summary-errors` 클래스를 정의할 수 있습니다.

### <a name="testing-the-insert-page"></a>삽입 페이지 테스트

1. 브라우저에서 페이지를 봅니다. 이 페이지에는 다음 그림에 표시 된 것과 비슷한 양식이 표시 됩니다.

    ![[이미지]](5-working-with-data/_static/image5.jpg)
2. 모든 열에 대 한 값을 입력 하 고 *Price* 열을 비워 두어야 합니다.
3. **삽입**을 클릭합니다. 다음 그림과 같이 페이지에 오류 메시지가 표시 됩니다. 새 레코드가 생성 되지 않습니다.

    ![[이미지]](5-working-with-data/_static/image6.jpg)
4. 양식을 완전히 채운 다음 **삽입**을 클릭 합니다. 이번에는 *Listproducts. cshtml* 페이지가 표시 되 고 새 레코드가 표시 됩니다.

## <a name="updating-data-in-a-database"></a>데이터베이스의 데이터 업데이트

테이블에 데이터를 입력 한 후에는 업데이트 해야 할 수 있습니다. 이 절차에서는 앞에서 데이터 삽입을 위해 만든 페이지와 유사한 두 페이지를 만드는 방법을 보여 줍니다. 첫 번째 페이지에는 제품이 표시 되 고 사용자가 변경할 항목을 선택할 수 있습니다. 두 번째 페이지에서는 사용자가 실제로 편집을 수행 하 고 저장할 수 있습니다.

> [!NOTE] 
> 
> **중요** 프로덕션 웹 사이트에서는 일반적으로 데이터를 변경할 수 있는 사용자를 제한 합니다. 멤버 자격을 설정 하는 방법과 사용자에 게 사이트에서 작업을 수행할 수 있는 권한을 부여 하는 방법에 대 한 자세한 내용은 [ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격 추가](https://go.microsoft.com/fwlink/?LinkId=202904)를 참조 하세요.

1. 웹 사이트에서 이름이 *Editproducts. cshtml*인 새 CSHTML 파일을 만듭니다.
2. 파일의 기존 태그를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    이 페이지와 이전 페이지의 *Listproducts* 의 유일한 차이점은이 페이지의 HTML 테이블에 **편집** 링크를 표시 하는 추가 열이 포함 되어 있다는 것입니다. 이 링크를 클릭 하면 선택한 레코드를 편집할 수 있는 *Updateproducts. cshtml 페이지로 이동 합니다.*

    **편집** 링크를 만드는 코드를 확인 합니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    이렇게 하면 `href` 특성이 동적으로 설정 되는 HTML `<a>` 요소가 만들어집니다. `href` 특성은 사용자가 링크를 클릭할 때 표시할 페이지를 지정 합니다. 또한 현재 행의 `Id` 값을 링크에 전달 합니다. 페이지가 실행 될 때 페이지 소스에는 다음과 같은 링크가 포함 될 수 있습니다.

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    `href` 특성은 `UpdateProducts/n`으로 설정 되어 있습니다. 여기서 *n* 은 제품 번호입니다. 사용자가 이러한 링크 중 하나를 클릭 하면 결과 URL은 다음과 같이 표시 됩니다.

    `http://localhost:18816/UpdateProducts/6`

    즉, 편집할 제품 번호가 URL에 전달 됩니다.
3. 브라우저에서 페이지를 봅니다. 페이지는 다음과 같은 형식으로 데이터를 표시 합니다.

    ![[이미지]](5-working-with-data/_static/image7.jpg)

    다음으로 사용자가 실제로 데이터를 업데이트할 수 있도록 페이지를 만듭니다. 업데이트 페이지에는 사용자가 입력 한 데이터의 유효성을 검사 하는 유효성 검사가 포함 됩니다. 예를 들어 페이지의 코드를 사용 하면 모든 필수 열에 대해 값이 입력 되었는지 확인할 수 있습니다.
4. 웹 사이트에서 *Updateproducts. cshtml*라는 새 CSHTML 파일을 만듭니다.
5. 파일의 기존 태그를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    페이지 본문에는 제품이 표시 되는 HTML 폼과 사용자가 편집할 수 있는 위치가 포함 되어 있습니다. 제품을 표시 하려면 다음 SQL 문을 사용 합니다.

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    그러면 `@0` 매개 변수에 전달 된 값과 일치 하는 ID를 가진 제품이 선택 됩니다. *Id* 는 기본 키 이므로 고유 해야 하므로 하나의 제품 레코드를 이러한 방식으로 선택할 수 있습니다. 이 `Select` 문에 전달할 ID 값을 가져오려면 다음 구문을 사용 하 여 페이지에 URL의 일부로 전달 되는 값을 읽을 수 있습니다.

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    실제로 제품 레코드를 인출 하려면 하나의 레코드만 반환 하는 `QuerySingle` 메서드를 사용 합니다.

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    단일 행이 `row` 변수로 반환 됩니다. 각 열에서 데이터를 가져와 다음과 같이 로컬 변수에 할당할 수 있습니다.

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    양식의 태그에서 이러한 값은 다음과 같이 포함 된 코드를 사용 하 여 개별 텍스트 상자에 자동으로 표시 됩니다.

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    코드의 해당 부분에서 업데이트할 제품 레코드를 표시 합니다. 레코드가 표시 되 면 사용자는 개별 열을 편집할 수 있습니다.

    사용자가 **업데이트** 단추를 클릭 하 여 양식을 제출 하면 `if(IsPost)` 블록의 코드가 실행 됩니다. 그러면 `Request` 개체에서 사용자 값을 가져오고, 변수에 값을 저장 하 고, 각 열이 채워져 있는지 확인 합니다. 유효성 검사에 통과 하면 코드에서 다음과 같은 SQL Update 문을 만듭니다.

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    SQL `Update` 문에서 업데이트할 각 열을 지정 하 고 값을로 설정 합니다. 이 코드에서는 매개 변수 자리 표시자 `@0`, `@1`, `@2`등을 사용 하 여 값을 지정 합니다. 앞에서 설명한 것 처럼 보안을 위해 항상 매개 변수를 사용 하 여 SQL 문에 값을 전달 해야 합니다.

    `db.Execute` 메서드를 호출 하는 경우 SQL 문의 매개 변수에 해당 하는 순서 대로 값을 포함 하는 변수를 전달 합니다.

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    `Update` 문을 실행 한 후에는 다음 메서드를 호출 하 여 사용자를 편집 페이지로 다시 리디렉션할 수 있습니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    이는 사용자에 게 데이터베이스에 있는 데이터의 업데이트 된 목록이 표시 되 고 다른 제품을 편집할 수 있는 것을 의미 합니다.
6. 페이지를 저장합니다.
7. 업데이트 페이지가 아닌 *Editproducts. cshtml* 페이지를 실행 한 다음 **편집** 을 클릭 하 여 편집할 제품을 선택 합니다. *Updateproducts. cshtml* 페이지가 표시 되 고 선택한 레코드를 표시 합니다.

    ![[이미지]](5-working-with-data/_static/image8.jpg)
8. 변경을 수행 하 고 **업데이트**를 클릭 합니다. 제품 목록이 업데이트 된 데이터와 함께 다시 표시 됩니다.

## <a name="deleting-data-in-a-database"></a>데이터베이스의 데이터 삭제

이 섹션에서는 사용자가 *제품* 데이터베이스 테이블에서 제품을 삭제 하도록 허용 하는 방법을 보여 줍니다. 이 예제는 두 페이지로 구성 됩니다. 첫 번째 페이지에서는 사용자가 삭제할 레코드를 선택 합니다. 그런 다음 삭제할 레코드가 레코드를 삭제할 것인지 확인할 수 있는 두 번째 페이지에 표시 됩니다.

> [!NOTE] 
> 
> **중요** 프로덕션 웹 사이트에서는 일반적으로 데이터를 변경할 수 있는 사용자를 제한 합니다. 멤버 자격을 설정 하는 방법과 사용자에 게 사이트에서 작업을 수행할 수 있는 권한을 부여 하는 방법에 대 한 자세한 내용은 [ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격 추가](https://go.microsoft.com/fwlink/?LinkId=202904)를 참조 하세요.

1. 웹 사이트에서 이름이 *ListProductsForDelete*인 새 CSHTML 파일을 만듭니다.
2. 기존 태그를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    이 페이지는 이전 버전의 *Editproducts. cshtml* 페이지와 비슷합니다. 그러나 각 제품에 대 한 **편집** 링크를 표시 하는 대신 **삭제** 링크를 표시 합니다. 태그에 다음 포함 코드를 사용 하 여 **삭제** 링크를 만듭니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    그러면 사용자가 링크를 클릭할 때 다음과 같은 URL이 생성 됩니다.

    `http://<server>/DeleteProduct/4`

    URL은 *deleteproduct. cshtml* (다음에 만들) 라는 페이지를 호출 하 고 삭제할 제품의 ID (여기서 4)를 전달 합니다.
3. 파일을 저장 하지만 열린 상태로 둡니다.
4. *Deleteproduct. cshtml*라는 다른 CHTML 파일을 만듭니다. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    이 페이지는 *ListProductsForDelete* 에서 호출 되며, 사용자가 제품을 삭제 하 려 함을 확인할 수 있습니다. 삭제할 제품을 나열 하려면 다음 코드를 사용 하 여 URL에서 삭제할 제품의 ID를 가져옵니다.

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    그러면 페이지에서 사용자에 게 실제로 레코드를 삭제 하는 단추를 클릭 하도록 요청 합니다. 이는 중요 한 보안 조치입니다. 데이터 업데이트 또는 삭제와 같은 웹 사이트에서 중요 한 작업을 수행 하는 경우 이러한 작업은 항상 GET 작업이 아닌 POST 작업을 사용 하 여 수행 해야 합니다. 가져오기 작업을 사용 하 여 삭제 작업을 수행할 수 있도록 사이트를 설정 하는 경우 모든 사용자가 `http://<server>/DeleteProduct/4` 같은 URL을 전달 하 고 데이터베이스에서 원하는 모든 항목을 삭제할 수 있습니다. 확인을 추가 하 고 페이지를 코딩 하 여 게시물을 통해서만 삭제를 수행할 수 있도록 하려면 사이트에 보안 측정값을 추가 합니다.

    실제 삭제 작업은 다음 코드를 사용 하 여 수행 됩니다 .이 코드는 먼저 post 작업 이며 ID가 비어 있지 않은지 확인 합니다.

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    이 코드는 지정 된 레코드를 삭제 한 다음 사용자를 다시 목록 페이지로 리디렉션하는 SQL 문을 실행 합니다.
5. 브라우저에서 *ListProductsForDelete* 를 실행 합니다.

    ![[이미지]](5-working-with-data/_static/image9.jpg)
6. 제품 중 하나에 대 한 **삭제** 링크를 클릭 합니다. *Deleteproduct. cshtml* 페이지가 표시 되어 해당 레코드를 삭제할 것인지 확인 합니다.
7. **삭제** 단추를 클릭합니다. 제품 레코드가 삭제 되 고 업데이트 된 제품 목록으로 페이지가 새로 고쳐집니다.

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a>데이터베이스에 연결
> 
> 두 가지 방법으로 데이터베이스에 연결할 수 있습니다. 첫 번째 방법은 `Database.Open` 메서드를 사용 하 고 데이터베이스 파일의 이름을 지정 하는 것입니다 ( *.sdf* 확장명 보다 낮음).
> 
> `var db = Database.Open("SmallBakery");`
> 
> `Open` 메서드는이 인 것으로 가정 합니다. *.sdf* 파일은 웹 사이트의 *App\_Data* 폴더에 있습니다. 이 폴더는 데이터를 저장 하기 위해 특별히 설계 되었습니다. 예를 들어 웹 사이트에서 데이터를 읽고 쓸 수 있도록 하는 적절 한 권한이 있으며, 보안 조치로 WebMatrix는이 폴더의 파일에 대 한 액세스를 허용 하지 않습니다.
> 
> 두 번째 방법은 연결 문자열을 사용 하는 것입니다. 데이터베이스에 연결하는 방법에 대한 정보를 포함하는 연결 문자열입니다. 이는 파일 경로를 포함 하거나, 해당 서버에 연결할 사용자 이름 및 암호와 함께 로컬 또는 원격 서버에 SQL Server 데이터베이스의 이름을 포함할 수 있습니다. 호스팅 공급자의 사이트와 같이 중앙에서 관리 되는 버전의 SQL Server에서 데이터를 유지 하는 경우 항상 연결 문자열을 사용 하 여 데이터베이스 연결 정보를 지정 합니다.
> 
> WebMatrix에서 연결 문자열은 일반적으로 *web.config*라는 XML 파일에 저장 됩니다. 이름에서 알 수 있듯이 웹 사이트의 루트에 있는 *web.config 파일을* 사용 하 여 사이트에 필요할 수 있는 연결 문자열을 포함 하 여 사이트의 구성 정보를 저장할 수 있습니다. *Web.config 파일에* 있는 연결 문자열의 예는 다음과 같습니다.
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> 이 예에서는 연결 문자열은 로컬 *.sdf* 파일이 아닌 다른 위치에 있는 서버에서 실행 되는 SQL Server의 인스턴스에 있는 데이터베이스를 가리킵니다. `myServer` 및 `myDatabase`에 대 한 적절 한 이름을 대체 하 고 `username` 및 `password`에 대 한 SQL Server 로그인 값을 지정 해야 합니다. 사용자 이름 및 암호 값은 사용자의 서버에 로그인 하기 위해 사용자가 제공 하는 Windows 자격 증명 또는 호스팅 공급자가 제공 하는 값과 동일할 필요는 없습니다. 관리자에 게 필요한 정확한 값을 확인 합니다.
> 
> `Database.Open` 메서드는 데이터베이스 *.sdf* 파일의 이름 또는 *web.config* 파일에 저장 된 연결 문자열의 이름을 전달할 수 있으므로 유연 합니다. 다음 예에서는 이전 예제에 나와 있는 연결 문자열을 사용 하 여 데이터베이스에 연결 하는 방법을 보여 줍니다.
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> 앞서 설명한 것 처럼 `Database.Open` 메서드를 사용 하 여 데이터베이스 이름 또는 연결 문자열을 전달할 수 있으며,이를 통해 사용할 수 있습니다. 이는 웹 사이트를 배포 (게시) 할 때 매우 유용 합니다. 사이트를 개발 하 고 테스트할 때 *앱\_데이터* 폴더에 .sdf 파일을 사용할 수 있습니다 *.* 그런 다음 사이트를 프로덕션 서버로 이동할 때 *.sdf* 파일과 동일한 이름을 가진 &#8212; *web.config* 파일의 연결 문자열을 사용할 수 있지만, 코드를 변경 하지 않고도 모든 호스팅 공급자의 데이터베이스를 가리킵니다.
> 
> 마지막으로 연결 문자열을 직접 사용 하려는 경우 `Database.OpenConnectionString` 메서드를 호출 하 고 *web.config* 파일의 이름 뿐 아니라 실제 연결 문자열을 전달할 수 있습니다. 이는 페이지가 실행 될 때까지 연결 문자열 (또는 *.sdf* 파일 이름 등의 값)에 액세스할 수 없는 경우에 유용할 수 있습니다. 그러나 대부분의 시나리오에서는이 문서에 설명 된 대로 `Database.Open`를 사용할 수 있습니다.

## <a name="additional-resources"></a>추가 리소스

- [SQL Server Compact](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [WebMatrix에서 SQL Server 또는 MySQL 데이터베이스에 연결](https://go.microsoft.com/fwlink/?LinkId=208661)
- [ASP.NET 웹 페이지 사이트에서 사용자 입력 유효성 검사](https://go.microsoft.com/fwlink/?LinkId=253002)
