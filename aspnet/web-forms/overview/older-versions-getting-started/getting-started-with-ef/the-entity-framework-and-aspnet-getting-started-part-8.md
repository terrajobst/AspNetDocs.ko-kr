---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-8 부 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 응용 프로그램 샘플은 ...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473507"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a>Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-8 부

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md) 를 참조 하십시오.

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a>Dynamic Data 기능을 사용 하 여 데이터 서식 지정 및 유효성 검사

이전 자습서에서 저장 프로시저를 구현 했습니다. 이 자습서에서는 Dynamic Data 기능을 통해 다음과 같은 이점을 제공 하는 방법을 보여 줍니다.

- 필드는 데이터 형식에 따라 자동으로 표시 되도록 서식이 지정 됩니다.
- 필드는 데이터 형식에 따라 자동으로 유효성이 검사 됩니다.
- 데이터 모델에 메타 데이터를 추가 하 여 서식 지정 및 유효성 검사 동작을 사용자 지정할 수 있습니다. 이 작업을 수행 하는 경우 한 곳에 서식 및 유효성 검사 규칙을 추가할 수 있으며, Dynamic Data 컨트롤을 사용 하 여 필드에 액세스 하는 모든 곳에서 자동으로 적용 됩니다.

이 기능이 어떻게 작동 하는지 확인 하려면 기존 *학생* 페이지의 필드를 표시 하 고 편집 하는 데 사용 하는 컨트롤을 변경 하 고 `Student` 엔터티 형식의 이름 및 날짜 필드에 서식 및 유효성 검사 메타 데이터를 추가 합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a>DynamicField 및 DynamicControl 컨트롤 사용

*학생용 .aspx* 페이지를 열고 `StudentsGridView` 컨트롤에서 **이름** 및 **등록 날짜** `TemplateField` 요소를 다음 태그로 바꿉니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

이 태그는 학생 이름 템플릿 필드에서 `TextBox` 및 `Label` 컨트롤 대신 `DynamicControl` 컨트롤을 사용 하 고 등록 날짜에 `DynamicField` 컨트롤을 사용 합니다. 서식 문자열을 지정 하지 않았습니다.

`StudentsGridView` 컨트롤 뒤에 `ValidationSummary` 컨트롤을 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

`SearchGridView` 컨트롤에서 `EditItemTemplate` 요소를 생략 하는 것을 제외 하 고 `StudentsGridView` 컨트롤과 같이 **이름** 및 **등록 날짜** 열의 태그를 바꿉니다. 이제 `SearchGridView` 컨트롤의 `Columns` 요소에 다음 태그가 포함 됩니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

*Students.aspx.cs* 를 열고 다음 `using` 문을 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

페이지의 `Init` 이벤트에 대 한 처리기를 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

이 코드는 Dynamic Data에서 `Student` 엔터티의 필드에 대해 이러한 데이터 바인딩된 컨트롤에 서식 지정 및 유효성 검사를 제공 하도록 지정 합니다. 페이지를 실행할 때 다음 예제와 같은 오류 메시지가 표시 되 면 일반적으로 `Page_Init`에서 `EnableDynamicData` 메서드를 호출 하는 것을 잊은 것입니다.

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

페이지를 실행 합니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)

**등록 날짜** 열에는 속성 형식이 `DateTime`되기 때문에 날짜와 함께 시간이 표시 됩니다. 나중에이 문제를 해결 합니다.

지금은 Dynamic Data에서 기본 데이터 유효성 검사를 자동으로 제공 합니다. 예를 들어 **편집**을 클릭 하 고 날짜 필드의 선택을 취소 한 다음 **업데이트**를 클릭 하면 값이 데이터 모델에서 null을 허용 하지 않기 때문에 Dynamic Data에서 자동으로 필수 필드로 설정 됩니다. 이 페이지는 필드 뒤에 별표를 표시 하 고 `ValidationSummary` 컨트롤에 오류 메시지를 표시 합니다.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)

별표 위에 마우스 포인터를 놓으면 오류 메시지를 볼 수도 있으므로 `ValidationSummary` 컨트롤을 생략할 수 있습니다.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)

또한 Dynamic Data **등록 날짜** 필드에 입력 한 데이터가 유효한 날짜 인지 확인 합니다.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)

여기에서 볼 수 있듯이 일반적인 오류 메시지입니다. 다음 섹션에서는 유효성 검사 및 서식 지정 규칙 뿐만 아니라 메시지를 사용자 지정 하는 방법을 알아봅니다.

## <a name="adding-metadata-to-the-data-model"></a>데이터 모델에 메타 데이터 추가

일반적으로 Dynamic Data에서 제공 하는 기능을 사용자 지정 하려고 합니다. 예를 들어 데이터가 표시 되는 방법 및 오류 메시지의 내용을 변경할 수 있습니다. 일반적으로 데이터 형식에 따라 자동으로 제공 되는 Dynamic Data 보다 많은 기능을 제공 하도록 데이터 유효성 검사 규칙을 사용자 지정 합니다. 이렇게 하려면 엔터티 형식에 해당 하는 partial 클래스를 만듭니다.

**솔루션 탐색기**에서 **ContosoUniversity** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **참조 추가**를 선택한 다음 `System.ComponentModel.DataAnnotations`에 대 한 참조를 추가 합니다.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)

*DAL* 폴더에서 새 클래스 파일을 만들고 이름을 *Student.cs*로 바꾼 후 해당 파일의 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

이 코드는 `Student` 엔터티에 대 한 partial 클래스를 만듭니다. 이 partial 클래스에 적용 되는 `MetadataType` 특성은 메타 데이터를 지정 하는 데 사용 하는 클래스를 식별 합니다. 메타 데이터 클래스는 어떤 이름도 가질 수 있지만, 엔터티 이름 및 "메타 데이터"를 사용 하는 것이 일반적인 방법입니다.

메타 데이터 클래스의 속성에 적용 되는 특성은 형식 지정, 유효성 검사, 규칙 및 오류 메시지를 지정 합니다. 여기에 표시 된 특성에는 다음과 같은 결과가 표시 됩니다.

- `EnrollmentDate`는 시간 없이 날짜로 표시 됩니다.
- 두 이름 필드의 길이는 모두 25 자이 하 여야 하 고 사용자 지정 오류 메시지가 제공 됩니다.
- 두 이름 필드가 모두 필요 하며 사용자 지정 오류 메시지가 제공 됩니다.

*학습자* 페이지를 다시 실행 하면 날짜가 시간 없이 표시 되는 것을 볼 수 있습니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)

행을 편집 하 고 이름 필드의 값을 지웁니다. 필드 오류를 나타내는 별표는 **업데이트**를 클릭 하기 전에 필드를 벗어나면 바로 표시 됩니다. **업데이트**를 클릭 하면 지정한 오류 메시지 텍스트가 페이지에 표시 됩니다.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)

25 자 보다 긴 이름을 입력 하 고 **업데이트**를 클릭 하면 지정한 오류 메시지 텍스트가 페이지에 표시 됩니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)

이제 데이터 모델 메타 데이터에서 이러한 형식 지정 및 유효성 검사 규칙을 설정 했으므로 `DynamicControl` 또는 `DynamicField` 컨트롤을 사용 하는 경우 이러한 필드를 표시 하거나 변경할 수 있도록 허용 하는 모든 페이지에 규칙이 자동으로 적용 됩니다. 이렇게 하면 프로그래밍 및 테스트를 더 쉽게 수행할 수 있도록 작성 해야 하는 중복 코드의 양이 줄어들고,이로 인해 응용 프로그램 전체에서 데이터 형식 지정 및 유효성 검사가 일관 되 게 유지 됩니다.

## <a name="more-information"></a>추가 정보

이 자습서에서는 Entity Framework 시작에 대 한이 일련의 자습서를 마칩니다. Entity Framework를 사용 하는 방법을 배우는 데 도움이 되는 자세한 내용은 [다음 Entity Framework 자습서 시리즈의 첫 번째 자습서](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) 를 계속 진행 하거나 다음 사이트를 방문 하세요.

- [Entity Framework FAQ](http://www.ef-faq.org/introduction.html)
- [Entity Framework 팀 블로그](https://blogs.msdn.com/b/adonet/)
- [MSDN Library의 Entity Framework](https://msdn.microsoft.com/library/bb399572.aspx)
- [MSDN 데이터 개발자 센터의 Entity Framework](https://msdn.microsoft.com/data/ef.aspx)
- [MSDN Library의 EntityDataSource 웹 서버 컨트롤 개요](https://msdn.microsoft.com/library/cc488502.aspx)
- [MSDN Library의 EntityDataSource control API 참조](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [MSDN의 Entity Framework 포럼](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [Julie Lerman의 블로그](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-7.md)
