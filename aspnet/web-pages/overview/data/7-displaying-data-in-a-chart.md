---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: ASP.NET 웹 페이지 (Razor)를 사용 하 여 차트에 데이터 표시 | Microsoft Docs
author: microsoft
description: 이 장에서는 차트에 데이터를 표시 하는 방법을 설명 합니다. 이전 장에서는 데이터를 수동으로 표시 하는 방법에 대해 알아보았습니다. 이 장에서 설명 하는 내용 ...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: 6dad67d4e3d38d57a761c567d937d714a3184ea9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509135"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>ASP.NET 웹 페이지를 사용 하 여 차트에 데이터 표시 (Razor)

[Microsoft](https://github.com/microsoft) 에서

> 이 문서에서는 `Chart` 도우미를 사용 하 여 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 차트를 사용 하 여 데이터를 표시 하는 방법을 설명 합니다.
> 
> **학습 내용**:
> 
> - 차트에 데이터를 표시 하는 방법
> - 기본 제공 테마를 사용 하 여 차트 스타일을 만드는 방법
> - 차트를 저장 하는 방법 및 성능 향상을 위해 차트를 캐시 하는 방법
> 
> 다음은이 문서에 도입 된 ASP.NET 프로그래밍 기능입니다.
> 
> - `Chart` 도우미입니다.
> 
> > [!NOTE]
> > 이 문서의 정보는 ASP.NET 웹 페이지 1.0 및 웹 페이지 2에 적용 됩니다.

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>차트 도우미

데이터를 그래픽 형식으로 표시 하려는 경우 `Chart` 도우미를 사용할 수 있습니다. `Chart` 도우미는 다양 한 차트 종류의 데이터를 표시 하는 이미지를 렌더링할 수 있습니다. 서식 지정 및 레이블 지정을 위한 다양 한 옵션을 지원 합니다. `Chart` 도우미는 Microsoft Excel 이나 기타 도구 &#8212; 영역 차트, 가로 막대형 차트, 세로 막대형 차트, 꺾은선형 차트 및 원형 차트와 같은 보다 특수 한 차트와 주식형 차트를 비롯 하 여 익숙한 차트의 모든 유형을 비롯 하 여 30 개 이상의 차트를 렌더링할 수 있습니다.

| **영역 차트** ![설명: 영역 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image1.jpg) | **가로 막대형 차트** ![설명: 가로 막대형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **세로 막대형 차트** ![설명: 세로 막대형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image3.jpg) | **꺾은선형 차트** ![설명: 꺾은선형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **원형 차트** ![설명: 원형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image5.jpg) | **주식형 차트** ![설명: 주식형 차트 종류의 그림](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>차트 요소

차트에는 데이터와 범례, 축, 계열 등과 같은 추가 요소가 표시 됩니다. 다음 그림에서는 `Chart` 도우미를 사용할 때 사용자 지정할 수 있는 다양 한 차트 요소를 보여 줍니다. 이 문서에서는 이러한 요소 중 일부 (모두 아님)를 설정 하는 방법을 보여 줍니다.

![설명: 차트 요소를 보여 주는 그림](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>데이터에서 차트 만들기

차트에 표시 되는 데이터는 배열, 데이터베이스에서 반환 된 결과 또는 XML 파일에 있는 데이터에서 볼 수 있습니다.

### <a name="using-an-array"></a>배열 사용

[Razor 구문을 사용한 ASP.NET 웹 페이지 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=202890)에서 설명한 것 처럼 배열을 사용 하면 유사한 항목의 컬렉션을 단일 변수에 저장할 수 있습니다. 배열을 사용 하 여 차트에 포함 하려는 데이터를 포함할 수 있습니다.

이 절차에서는 기본 차트 종류를 사용 하 여 배열의 데이터에서 차트를 만드는 방법을 보여 줍니다. 또한 페이지 내에서 차트를 표시 하는 방법을 보여 줍니다.

1. *ChartArrayBasic*라는 새 파일을 만듭니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    이 코드는 먼저 새 차트를 만들고 너비와 높이를 설정 합니다. `AddTitle` 메서드를 사용 하 여 차트 제목을 지정 합니다. 데이터를 추가 하려면 `AddSeries` 메서드를 사용 합니다. 이 예제에서는 `AddSeries` 메서드의 `name`, `xValue`및 `yValues` 매개 변수를 사용 합니다. `name` 매개 변수는 차트 범례에 표시 됩니다. `xValue` 매개 변수는 차트의 가로 축을 따라 표시 되는 데이터 배열을 포함 합니다. `yValues` 매개 변수는 차트의 세로 요소를 그리는 데 사용 되는 데이터 배열을 포함 합니다.

    `Write` 메서드는 실제로 차트를 렌더링 합니다. 이 경우 차트 종류를 지정 하지 않았기 때문에 `Chart` 도우미가 세로 막대형 차트인 기본 차트를 렌더링 합니다.
3. 브라우저에서 페이지를 실행 합니다. 브라우저에 차트가 표시 됩니다. 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>차트 데이터에 데이터베이스 쿼리 사용

차트에 표시할 정보가 데이터베이스에 있는 경우 데이터베이스 쿼리를 실행 한 다음 결과의 데이터를 사용 하 여 차트를 만들 수 있습니다. 이 절차에서는 [ASP.NET 웹 페이지 사이트의 데이터베이스 작업 소개](https://go.microsoft.com/fwlink/?LinkId=202893)문서에서 만든 데이터베이스의 데이터를 읽고 표시 하는 방법을 보여 줍니다.

1. 폴더가 아직 없는 경우 *응용 프로그램\_데이터* 폴더를 웹 사이트의 루트에 추가 합니다.
2. *앱\_Data* 폴더에 [ASP.NET 웹 페이지 사이트의 데이터베이스 작업 소개](https://go.microsoft.com/fwlink/?LinkId=202893)에 설명 된 *SmallBakery* 라는 데이터베이스 파일을 추가 합니다.
3. *ChartDataQuery*라는 새 파일을 만듭니다.
4. 기존 콘텐츠를 다음으로 바꿉니다.   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    이 코드는 먼저 SmallBakery 데이터베이스를 열고 `db`라는 변수에 할당 합니다. 이 변수는 데이터베이스에서 읽고 쓰는 데 사용할 수 있는 `Database` 개체를 나타냅니다. 그런 다음,이 코드는 SQL 쿼리를 실행 하 여 각 제품의 이름과 가격을 가져옵니다. 이 코드는 차트의 `DataBindTable` 메서드를 호출 하 여 새 차트를 만들고 데이터베이스 쿼리를 전달 합니다. 이 메서드는 두 개의 매개 변수를 사용 합니다. `dataSource` 매개 변수는 쿼리의 데이터를 위한 것이 고 `xField` 매개 변수를 사용 하면 차트의 x 축에 사용 되는 데이터 열을 설정할 수 있습니다.

    `DataBindTable` 메서드를 사용 하는 대신 `Chart` 도우미의 `AddSeries` 메서드를 사용할 수 있습니다. `AddSeries` 메서드를 사용 하 여 `xValue` 및 `yValues` 매개 변수를 설정할 수 있습니다. 예를 들어 다음과 같이 `DataBindTable` 메서드를 사용 하는 대신

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    다음과 같이 `AddSeries` 메서드를 사용할 수 있습니다.

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    둘 다 동일한 결과를 렌더링 합니다. `AddSeries` 방법은 차트 종류와 데이터를 더 명시적으로 지정할 수 있기 때문에 더 유연 하지만, 추가 유연성이 필요 하지 않으면 `DataBindTable` 메서드를 사용 하는 것이 더 쉽습니다.
5. 브라우저에서 페이지를 실행 합니다. 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>XML 데이터 사용

차트의 세 번째 옵션은 XML 파일을 차트의 데이터로 사용 하는 것입니다. 이를 위해서는 xml 파일에 XML 구조를 설명 하는 스키마 파일 ( *.xsd* 파일)도 있어야 합니다. 이 절차에서는 XML 파일에서 데이터를 읽는 방법을 보여 줍니다.

1. *App\_data* 폴더에서 *data .XML*이라는 새 XML 파일을 만듭니다.
2. 기존 XML을 가상 회사의 직원에 대 한 XML 데이터 인 다음으로 바꿉니다. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. *App\_data* 폴더에서 *data .XSD*라는 새 XML 파일을 만듭니다. 이 경우 확장명은 *.xsd*입니다.
4. 기존 XML을 다음으로 바꿉니다. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. 웹 사이트의 루트에서 *Chartdataxml. cshtml*라는 새 파일을 만듭니다.
6. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    코드는 먼저 `DataSet` 개체를 만듭니다. 이 개체는 XML 파일에서 읽은 데이터를 관리 하 고 스키마 파일의 정보에 따라 구성 하는 데 사용 됩니다. 코드의 맨 위에는 `using SystemData`문이 포함 되어 있습니다. `DataSet` 개체를 사용 하려면이 작업이 필요 합니다. 자세한 내용은이 문서의 뒷부분에 나오는 [&quot; 문과 정규화 된 이름을 사용 하&quot;](#SB_UsingStatements) 를 참조 하세요.)

    그런 다음 코드는 데이터 집합을 기반으로 `DataView` 개체를 만듭니다. 데이터 뷰에서는 차트가 바인딩할 &#8212; 수 있는 개체 (읽기 및 그리기)를 제공 합니다. `xValue` 및 `yValues` 매개 변수가 `DataView` 개체로 설정 된 경우를 제외 하 고 앞에서 설명한 것 처럼 `AddSeries` 메서드를 사용 하 여 차트를 데이터에 바인딩합니다.

    또한이 예제에서는 특정 차트 종류를 지정 하는 방법을 보여 줍니다. `AddSeries` 메서드에서 데이터를 추가 하면 `chartType` 매개 변수도 원형 차트를 표시 하도록 설정 됩니다.
7. 브라우저에서 페이지를 실행 합니다. 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"Using" 문 및 정규화 된 이름
> 
> Razor 구문로 ASP.NET 웹 페이지 하는 .NET Framework는 수많은 구성 요소 (클래스)로 구성 됩니다. 이러한 모든 클래스를 관리할 수 있도록 하는 것은 라이브러리와 유사 하 게 *네임 스페이스로*구성 됩니다. 예를 들어 `System.Web` 네임 스페이스는 브라우저/서버 통신을 지 원하는 클래스를 포함 하 고, `System.Xml` 네임 스페이스는 XML 파일을 만들고 읽는 데 사용 되는 클래스를 포함 하며, `System.Data` 네임 스페이스는 데이터를 사용할 수 있도록 하는 클래스를 포함 합니다.
> 
> .NET Framework에서 지정 된 클래스에 액세스 하기 위해 코드는 클래스 이름 뿐만 아니라 클래스가 있는 네임 스페이스를 알고 있어야 합니다. 예를 들어 `Chart` 도우미를 사용 하기 위해 코드는 네임 스페이스 (`System.Web.Helpers`)를 클래스 이름 (`Chart`)과 결합 하는 `System.Web.Helpers.Chart` 클래스를 찾아야 합니다. 이는 .NET Framework의 vastness 내에서 완전 하 고 명확한 &#8212; 위치를 클래스의 정규화 된 이름 이라고 합니다. 코드에서이는 다음과 같습니다.
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> 그러나 클래스 또는 도우미를 참조할 때마다 이러한 긴 정규화 된 이름을 사용 해야 하는 것은 어렵고 오류가 발생 하기 쉽습니다. 따라서 클래스 이름을 더 쉽게 사용할 수 있도록 관심 있는 네임 스페이스를 *가져올* 수 있습니다 .이는 일반적으로 .NET Framework의 많은 네임 스페이스 중 일부에 불과합니다. 네임 스페이스를 가져온 경우`System.Web.Helpers.Chart`(정규화 된 이름) 대신 클래스 이름 (`Chart`)만 사용할 수 있습니다. 코드가 실행 되 고 클래스 이름이 발견 되 면 가져온 네임 스페이스를 검색 하 여 해당 클래스를 찾을 수 있습니다.
> 
> Razor 구문에서 ASP.NET 웹 페이지를 사용 하 여 웹 페이지를 만드는 경우 일반적으로 `WebPage` 클래스, 다양 한 도우미 등을 포함 하 여 매번 동일한 클래스 집합을 사용 합니다. 웹 사이트를 만들 때마다 관련 네임 스페이스를 가져오는 작업을 저장 하기 위해 ASP.NET가 구성 되어 모든 웹 사이트의 코어 네임 스페이스 집합을 자동으로 가져옵니다. 따라서 네임 스페이스를 처리 하거나 지금까지 가져올 필요가 없습니다. 작업 한 모든 클래스는 이미 가져온 네임 스페이스에 있습니다.
> 
> 그러나 경우에 따라 자동으로 가져온 네임 스페이스에 없는 클래스로 작업 해야 합니다. 이 경우 해당 클래스의 정규화 된 이름을 사용 하거나 클래스를 포함 하는 네임 스페이스를 수동으로 가져올 수 있습니다. 네임 스페이스를 가져오려면 문서 앞의 예제에서 살펴본 것 처럼 `using` 문 (Visual Basic에서`import`)을 사용 합니다.
> 
> 예를 들어 `DataSet` 클래스는 `System.Data` 네임 스페이스에 있습니다. `System.Data` 네임 스페이스는 Razor 페이지에 자동으로 ASP.NET 수 없습니다. 따라서 정규화 된 이름을 사용 하 여 `DataSet` 클래스로 작업 하려면 다음과 같은 코드를 사용할 수 있습니다.
> 
> `var dataSet = new System.Data.DataSet();`
> 
> `DataSet` 클래스를 반복 해 서 사용 해야 하는 경우 다음과 같은 네임 스페이스를 가져온 다음 코드에서 클래스 이름만 사용할 수 있습니다.
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> 참조할 다른 .NET Framework 네임 스페이스에 대 한 `using` 문을 추가할 수 있습니다. 그러나이 작업을 수행 하는 대부분의 클래스는 ASP.NET 및 *.* a s t 페이지에서 사용 하기 위해 자동으로 가져오는 네임 스페이스에 있기 때문에이 작업을 수행 하지 않아도 *됩니다.*

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>웹 페이지 내에 차트 표시

지금까지 살펴본 예제에서는 차트를 만든 다음 차트가 브라우저에 그래픽으로 직접 렌더링 됩니다. 그러나 대부분의 경우에는 브라우저에서 뿐만 아니라 차트를 페이지의 일부로 표시 하려고 합니다. 이렇게 하려면 2 단계 프로세스가 필요 합니다. 첫 번째 단계는 이미 살펴본 대로 차트를 생성 하는 페이지를 만드는 것입니다.

두 번째 단계는 결과 이미지를 다른 페이지에 표시 하는 것입니다. 이미지를 표시 하려면 이미지를 표시 하는 것과 같은 방식으로 HTML `<img>` 요소를 사용 합니다. 그러나 *.jpg* 또는 *.png* 파일을 참조 하는 대신 `<img>` 요소는 차트를 만드는 `Chart` 도우미를 포함 하는 *cshtml* 파일을 참조 합니다. 표시 페이지가 실행 되 면 `<img>` 요소는 `Chart` 도우미의 출력을 가져오고 차트를 렌더링 합니다.

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. *Showchart. cshtml*라는 파일을 만듭니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    이 코드에서는 `<img>` 요소를 사용 하 여 이전에 *ChartArrayBasic* 파일에서 만든 차트를 표시 합니다.
3. 브라우저에서 웹 페이지를 실행 합니다. *Showchart. cshtml* 파일은 *ChartArrayBasic* 파일에 포함 된 코드에 따라 차트 이미지를 표시 합니다.

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>차트 스타일 지정

`Chart` 도우미는 차트의 모양을 사용자 지정할 수 있는 많은 옵션을 지원 합니다. 색, 글꼴, 테두리 등을 설정할 수 있습니다. 차트의 모양을 사용자 지정 하는 쉬운 방법은 *테마*를 사용 하는 것입니다. 테마는 글꼴, 색, 레이블, 색상표, 테두리 및 효과를 사용하여 렌더링하는 방법을 지정하는 정보의 모음입니다. 차트의 스타일이 차트의 종류를 나타내지 않습니다.

다음 표에서는 기본 제공 테마를 나열 합니다.

| 테마 | Description |
| --- | --- |
| `Vanilla` | 흰색 배경에 빨간색 열을 표시 합니다. |
| `Blue` | 파랑 그라데이션 배경에 파란색 열을 표시 합니다. |
| `Green` | 녹색 그라데이션 배경에 파란색 열을 표시 합니다. |
| `Yellow` | 노란색 그라데이션 배경에 주황색 열을 표시 합니다. |
| `Vanilla3D` | 흰색 배경에 3 차원 빨간색 열을 표시 합니다. |

새 차트를 만들 때 사용할 테마를 지정할 수 있습니다.

1. *ChartStyleGreen*라는 새 파일을 만듭니다.
2. 페이지의 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    이 코드는 데이터에 데이터베이스를 사용 하지만 `Chart` 개체를 만들 때 `theme` 매개 변수를 추가 하는 이전 예제와 동일 합니다. 다음은 변경 된 코드를 보여 줍니다.

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. 브라우저에서 페이지를 실행 합니다. 이전과 동일한 데이터를 볼 수 있지만 차트가 더 세련 된 형태입니다. 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>차트 저장

이 문서에서 살펴본 대로 `Chart` 도우미를 사용 하는 경우 도우미는 호출 될 때마다 처음부터 새로 차트를 다시 만듭니다. 필요한 경우 차트의 코드도 데이터베이스를 다시 쿼리하거나 XML 파일을 다시 읽어서 데이터를 가져옵니다. 쿼리 하는 데이터베이스가 크거나 XML 파일에 많은 데이터가 포함 되어 있는 경우와 같이이 작업을 수행 하는 것이 복잡할 수 있습니다. 차트가 많은 데이터를 포함 하지 않는 경우에도 이미지를 동적으로 만드는 프로세스에서 서버 리소스를 차지 하 고 많은 사람들이 차트를 표시 하는 페이지를 요청 하는 경우 웹 사이트의 성능에 영향을 줄 수 있습니다.

차트를 만들 때 발생 하는 성능에 미치는 영향을 줄이기 위해 처음 필요할 때 차트를 만든 다음 저장할 수 있습니다. 차트가 다시 생성 되지 않고 다시 생성 되 면 저장 된 버전을 가져와 렌더링할 수 있습니다.

다음과 같은 방법으로 차트를 저장할 수 있습니다.

- 서버에 있는 컴퓨터 메모리에 차트를 캐시 합니다.
- 차트를 이미지 파일로 저장 합니다.
- 차트를 XML 파일로 저장 합니다. 이 옵션을 사용 하면 차트를 저장 하기 전에 수정할 수 있습니다.

### <a name="caching-a-chart"></a>차트 캐싱

차트를 만든 후에는이를 캐시할 수 있습니다. 차트를 캐시 하면 다시 표시 해야 하는 경우 다시 만들 필요가 없습니다. 캐시에 차트를 저장 하는 경우 해당 차트에 고유 해야 하는 키를 제공 합니다.

서버에 메모리가 부족 하면 캐시에 저장 된 차트가 제거 될 수 있습니다. 또한 어떤 이유로 든 응용 프로그램이 다시 시작 되 면 캐시가 지워집니다. 따라서 캐시 된 차트를 사용 하 여 작업 하는 표준 방법은 항상 캐시에서 사용할 수 있는지 여부를 확인 하 고, 그렇지 않은 경우에는 항상 먼저 확인 하 고, 그렇지 않으면 다시 만듭니다.

1. 웹 사이트의 루트에서 *Showcachedchart. cshtml*라는 파일을 만듭니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    `<img>` 태그는 *ChartSaveToCache* 파일을 가리키고 페이지에 키를 쿼리 문자열로 전달 하는 `src` 특성을 포함 합니다. 키에는 myChartKey&quot;&quot;값이 포함 됩니다. *ChartSaveToCache* 파일에는 차트를 만드는 `Chart` 도우미가 포함 되어 있습니다. 잠시 후이 페이지를 만듭니다.

    페이지 끝에는 *Clearcache. cshtml*라는 페이지에 대 한 링크가 있습니다. 이 페이지에 곧 만들 수도 있습니다. *Clearcache가 필요 합니다.* 이 예제에서는 테스트 캐싱 으로만 cshtml를 사용 합니다 .이 예제에서는 캐시 된 차트를 사용할 때 일반적으로 포함 하는 링크나 페이지가 아닙니다.
3. 웹 사이트의 루트에서 *ChartSaveToCache*라는 새 파일을 만듭니다.
4. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    코드는 먼저 쿼리 문자열의 키 값으로 전달 된 항목이 있는지 여부를 확인 합니다. 이 경우 코드는 `GetFromCache` 메서드를 호출 하 고 키를 전달 하 여 캐시에서 차트를 읽으려고 시도 합니다. 해당 키 아래의 캐시에 아무 것도 없는 것으로 표시 되 면 (차트가 처음 요청 될 때 발생 함) 코드에서 평소와 같이 차트를 만듭니다. 차트가 완성 되 면 코드는 `SaveToCache`를 호출 하 여 캐시에 저장 합니다. 이 메서드에는 키가 필요 합니다 (나중에 차트를 요청할 수 있도록 하 고, 차트를 캐시에 저장 해야 하는 시간). 차트를 캐시 하는 정확한 시간은 표시 되는 데이터가 변경 될 수 있는 빈도에 따라 달라 집니다. 또한 `SaveToCache` 메서드는 `slidingExpiration` 매개 변수가 필요 &#8212; 합니다 .이 매개 변수가 true로 설정 된 경우에는 차트에 액세스할 때마다 시간 제한 카운터가 다시 설정 됩니다. 이 경우에는 사용자가 차트에 마지막으로 액세스 한 후에 차트의 캐시 항목이 2 분 후 만료 됩니다. 슬라이딩 만료의 대안은 절대 만료입니다. 즉, 캐시 항목에 액세스 하는 빈도에 관계 없이 캐시 항목은 캐시에 저장 된 후 정확히 2 분이 만료 됩니다.

    마지막으로,이 코드는 `WriteFromCache` 메서드를 사용 하 여 캐시에서 차트를 인출 하 고 렌더링 합니다. 이 메서드는 캐시에서 차트를 가져오며 캐시에서 차트를 생성 하 여 캐시에 저장 해야 하는지 여부에 관계 없이 캐시에서 차트를 가져오기 때문에 캐시를 확인 하는 `if` 블록 외부에 있습니다.

    예제에서 `AddTitle` 메서드는 타임 스탬프를 포함 합니다. (현재 날짜 및 시간 &#8212; `DateTime.Now` &#8212; 제목에 추가 합니다.)
5. *Clearcache. cshtml* 이라는 새 페이지를 만들고 해당 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    이 페이지에서는 `WebCache` 도우미를 사용 하 여 *ChartSaveToCache*에 캐시 된 차트를 제거 합니다. 앞에서 설명한 대로 일반적으로 다음과 같은 페이지가 필요 하지 않습니다. 캐싱을 보다 쉽게 테스트할 수 있도록 여기에서 만듭니다.
6. 브라우저에서 *Showcachedchart. cshtml* 웹 페이지를 실행 합니다. 이 페이지에는 *ChartSaveToCache* 파일에 포함 된 코드를 기반으로 하는 차트 이미지가 표시 됩니다. 차트 제목에 타임 스탬프를 기록 합니다. 

    ![설명: 차트 제목의 타임 스탬프를 포함 하는 기본 차트의 그림](7-displaying-data-in-a-chart/_static/image13.jpg)
7. 브라우저를 닫습니다.
8. *Showcachedchart. cshtml* 를 다시 실행 합니다. 타임 스탬프는 이전과 동일 합니다 .이는 차트가 다시 생성 되지 않았지만 캐시에서 읽 었는 지를 나타냅니다.
9. *Showcachedchart. cshtml*에서 **캐시 지우기** 링크를 클릭 합니다. 이렇게 하면 캐시가 지워진 것으로 보고 하는 *Clearcache. cshtml*로 이동 합니다.
10. **Showcachedchart로 돌아가기** 링크를 클릭 하거나 *Showcachedchart.* WebMatrix에서 cshtml를 다시 실행 합니다. 캐시가 제거 되었으므로 이번 타임 스탬프가 변경 된 것을 확인할 수 있습니다. 따라서 코드는 차트를 다시 생성 하 고 캐시에 다시 배치 해야 했습니다.

### <a name="saving-a-chart-as-an-image-file"></a>차트를 이미지 파일로 저장

서버에 이미지 파일 (예: *.jpg* 파일)로 차트를 저장할 수도 있습니다. 그런 다음 이미지 파일을 이미지와 같은 방식으로 사용할 수 있습니다. 파일은 임시 캐시에 저장 되는 것이 아니라 저장 된다는 장점이 있습니다. 새 차트 이미지를 서로 다른 시간 (예: 매시간)으로 저장 한 다음 시간에 따라 발생 하는 변경 내용에 대 한 영구 기록을 유지할 수 있습니다. 웹 응용 프로그램에 이미지 파일을 저장할 서버의 폴더에 파일을 저장할 수 있는 권한이 있는지 확인 해야 합니다.

1. 웹 사이트의 루트에서 이미 존재 하지 않는 경우 *\_ChartFiles* 라는 폴더를 만듭니다.
2. 웹 사이트의 루트에서 *Chartsave. cshtml*라는 새 파일을 만듭니다.
3. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    코드는 먼저 `File.Exists` 메서드를 호출 하 여 *.jpg* 파일이 있는지 여부를 확인 합니다. 파일이 없는 경우 코드는 배열에서 새 `Chart`를 만듭니다. 이번에는 코드가 `Save` 메서드를 호출 하 고 `path` 매개 변수를 전달 하 여 차트를 저장할 위치의 파일 경로와 파일 이름을 지정 합니다. 페이지 본문에서 `<img>` 요소는 경로를 사용 하 여 표시할 *.jpg* 파일을 가리킵니다.
4. *Chartsave. cshtml* 파일을 실행 합니다.
5. WebMatrix로 돌아갑니다. *Chart01* 라는 이미지 파일은 *\_chartfiles* 폴더에 저장 되어 있습니다.

### <a name="saving-a-chart-as-an-xml-file"></a>차트를 XML 파일로 저장

마지막으로 차트를 서버에 XML 파일로 저장할 수 있습니다. 차트를 캐시 하거나 파일에 차트를 저장 하는 것 보다이 방법을 사용 하면 원하는 경우 차트를 표시 하기 전에 XML을 수정할 수 있다는 이점이 있습니다. 응용 프로그램에 이미지 파일을 저장 하려는 서버의 폴더에 대 한 읽기/쓰기 권한이 있어야 합니다.

1. 웹 사이트의 루트에서 *Chartsavexml. cshtml*라는 새 파일을 만듭니다.
2. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    이 코드는 XML 파일을 사용 하는 경우를 제외 하 고는 캐시에 차트를 저장 하는 데 앞서 살펴본 코드와 비슷합니다. 코드는 먼저 `File.Exists` 메서드를 호출 하 여 XML 파일이 있는지 여부를 확인 합니다. 파일이 존재 하는 경우 코드는 새 `Chart` 개체를 만들고 파일 이름을 `themePath` 매개 변수로 전달 합니다. 그러면 XML 파일의 모든 항목을 기반으로 차트가 만들어집니다. XML 파일이 아직 없는 경우 코드는 normal과 같은 차트를 만든 다음 `SaveXml`를 호출 하 여 저장 합니다. 앞에서 살펴본 것 처럼 `Write` 메서드를 사용 하 여 차트를 렌더링 합니다.

    캐싱을 보여 주는 페이지와 마찬가지로이 코드에는 차트 제목에 타임 스탬프가 포함 됩니다.
3. *Chartdisplayxmlchart. cshtml* 이라는 새 페이지를 만들고 다음 태그를 추가 합니다. 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. *Chartdisplayxmlchart. cshtml* 페이지를 실행 합니다. 차트가 표시 됩니다. 차트 제목의 타임 스탬프를 기록해 둡니다.
5. 브라우저를 닫습니다.
6. WebMatrix에서 *\_ChartFiles* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **새로 고침**을 클릭 한 다음 폴더를 엽니다. 이 폴더의 *Xmlchart .xml* 파일은 `Chart` 도우미에 의해 만들어졌습니다. 

    ![설명: 차트 도우미가 만든 XMLChart .xml 파일을 보여 주는 _ChartFiles 폴더입니다.](7-displaying-data-in-a-chart/_static/image14.jpg)
7. *Chartdisplayxmlchart. cshtml* 페이지를 다시 실행 합니다. 페이지를 처음 실행 했을 때와 동일한 타임 스탬프가 차트에 표시 됩니다. 이전에 저장 한 XML에서 차트가 생성 되기 때문입니다.
8. WebMatrix에서 *\_ChartFiles* 폴더를 열고 *xmlchart .xml* 파일을 삭제 합니다.
9. *차트를 한* 번 더 실행 합니다. 이번에는 `Chart` 도우미가 XML 파일을 다시 만들어야 했기 때문에 타임 스탬프가 업데이트 됩니다. 원하는 경우 *\_ChartFiles* 폴더를 확인 하 고 XML 파일이 다시 표시 되는지 확인 합니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [ASP.NET 웹 페이지 사이트의 데이터베이스 작업 소개](https://go.microsoft.com/fwlink/?LinkId=202893)
- [ASP.NET 웹 페이지 사이트에서 캐싱을 사용 하 여 성능 향상](https://go.microsoft.com/fwlink/?LinkId=202903)
- [차트 클래스](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99)) (MSDN의 ASP.NET 웹 페이지 API 참조)
