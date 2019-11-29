---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에 대 한 더 복잡 한 데이터 모델 만들기 (4/10) | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9c19ec47ad98a319ddee17db014c4b15e3734778
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595356"
---
# <a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a>ASP.NET MVC 응용 프로그램에 대 한 더 복잡 한 데이터 모델 만들기 (4/10)

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. [이 챕터의](building-the-ef5-mvc4-chapter-downloads.md) 시작 또는 시작 프로젝트 다운로드에서 자습서 시리즈를 시작 하 고 여기에서 시작할 수 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완료 된 챕터를 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 하 여 문제를 재현해 보세요. 일반적으로 코드를 완성 된 코드와 비교 하 여 문제에 대 한 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 방법에 대 한 자세한 내용은 [오류 및 해결](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) 방법을 참조 하세요.

이전 자습서에서는 세 가지 엔터티로 구성 된 간단한 데이터 모델을 사용 했습니다. 이 자습서에서는 더 많은 엔터티 및 관계를 추가 하 고 서식 지정, 유효성 검사 및 데이터베이스 매핑 규칙을 지정 하 여 데이터 모델을 사용자 지정 합니다. 데이터 모델을 사용자 지정 하는 두 가지 방법, 즉 엔터티 클래스에 특성을 추가 하 고 데이터베이스 컨텍스트 클래스에 코드를 추가 하 여이를 확인할 수 있습니다.

완료되면 엔터티 클래스는 다음 그림에 표시된 완성된 데이터 모델을 구성하게 됩니다.

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a>특성을 사용하여 데이터 모델 사용자 지정

이 섹션에서는 서식 지정, 유효성 검사 및 데이터베이스 매핑 규칙을 지정하는 특성을 사용하여 데이터 모델을 사용자 지정하는 방법을 배웁니다. 다음 섹션의 일부에서는 이미 만든 클래스에 특성을 추가 하 고 모델의 나머지 엔터티 형식에 대해 새 클래스를 만들어 전체 `School` 데이터 모델을 만듭니다.

### <a name="the-datatype-attribute"></a>DataType 특성

학생 등록 날짜의 경우, 이 필드에서 필요한 것은 날짜이지만 현재 모든 웹 페이지는 날짜와 함께 시간을 표시합니다. 데이터 주석 특성을 사용하면 데이터를 표시하는 모든 보기에서 표시 형식을 해결하는 하나의 코드 변경을 만들 수 있습니다. 수행 방법의 예제를 보려면 특성을 `Student` 클래스의 `EnrollmentDate` 속성에 추가합니다.

*Models\Student.cs*에서 `System.ComponentModel.DataAnnotations` 네임 스페이스에 대 한 `using` 문을 추가 하 고 다음 예제와 같이 `EnrollmentDate` 속성에 `DataType` 및 `DisplayFormat` 특성을 추가 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성은 데이터베이스 내장 형식 보다 구체적인 데이터 형식을 지정 하는 데 사용 됩니다. 이 경우에는 날짜 및 시간이 아닌 날짜만 추적하고자 합니다. [DataType 열거형](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 은 *날짜, 시간, PhoneNumber, 통화, EmailAddress* 등과 같은 다양 한 데이터 형식을 제공 합니다. `DataType` 특성을 통해 응용 프로그램에서 자동으로 형식별 기능을 제공하도록 설정할 수도 있습니다. 예를 들어 [EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)에 대 한 `mailto:` 링크를 만들 수 있으며, [HTML5](http://html5.org/)를 지 원하는 브라우저에서 [데이터 형식](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 에 날짜 선택기를 제공할 수 있습니다. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성은 html 5 브라우저에서 이해할 수 있는 html 5 [데이터](http://ejohn.org/blog/html-5-data-attributes/) ( *데이터 대시로*발음) 특성을 내보냅니다. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성은 유효성 검사를 제공 하지 않습니다.

`DataType.Date`는 표시되는 날짜의 서식을 지정하지 않습니다. 기본적으로 데이터 필드는 서버의 [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)를 기준으로 기본 형식에 따라 표시 됩니다.

`DisplayFormat` 특성은 날짜 형식을 명시적으로 지정하는 데 사용됩니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

`ApplyFormatInEditMode` 설정은 값이 편집을 위해 텍스트 상자에 표시 될 때 지정 된 서식 지정도 적용 되도록 지정 합니다. (예를 들어 통화 값의 경우 텍스트 상자에 통화 기호를 편집 하는 것을 원하지 않을 수 있습니다.

[Displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성은 단독으로 사용할 수 있지만 일반적으로 [데이터 형식](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성을 사용 하는 것이 좋습니다. `DataType` 특성은 화면에 렌더링 하는 방법과 반대로 데이터의 *의미 체계* 를 전달 하 고 `DisplayFormat`에서 얻을 수 없는 다음과 같은 이점을 제공 합니다.

- 브라우저는 HTML5 기능을 사용 하도록 설정할 수 있습니다 (예: 달력 컨트롤, 로캘에 적합 한 통화 기호, 전자 메일 링크 등 표시).
- 기본적으로 브라우저는 사용자의 [로캘에](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)따라 올바른 형식을 사용 하 여 데이터를 렌더링 합니다.
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성을 사용 하면 MVC가 데이터를 렌더링할 올바른 필드 템플릿을 선택할 수 있습니다. 단독으로 사용 하는 경우 [displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 은 문자열 템플릿을 사용 합니다. 자세한 내용은 Brad Wilson의 [ASP.NET MVC 2 템플릿](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)을 참조 하세요. (MVC 2 용으로 작성 된 경우에도이 문서는 현재 버전의 ASP.NET MVC에 적용 됩니다.)

`DataType` 특성을 날짜 필드와 함께 사용 하는 경우 Chrome 브라우저에서 필드가 올바르게 렌더링 되도록 하기 위해 `DisplayFormat` 특성도 지정 해야 합니다. 자세한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)를 참조 하세요.

학생 인덱스 페이지를 다시 실행 하 고 등록 날짜에 대 한 시간이 더 이상 표시 되지 않는지 확인 합니다. `Student` 모델을 사용 하는 모든 보기의 경우에도 마찬가지입니다.

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>StringLengthAttribute

특성을 사용 하 여 데이터 유효성 검사 규칙 및 메시지를 지정할 수도 있습니다. 사용자가 이름을 50자 이하로 입력하였는지를 확인한다고 가정합니다. 이 제한을 추가 하려면 다음 예제와 같이 `LastName`에 [Stringlength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성을 추가 하 고 속성을 `FirstMidName` 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

[Stringlength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성은 사용자가 이름에 공백을 입력 하는 것을 방지 하지 않습니다. [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 특성을 사용 하 여 입력에 제한을 적용할 수 있습니다. 예를 들어 다음 코드는 첫 번째 문자가 대문자 여야 하 고 나머지 문자는 영문자 여야 합니다.

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) 특성은 [stringlength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성과 비슷한 기능을 제공 하지만 클라이언트 쪽 유효성 검사는 제공 하지 않습니다.

응용 프로그램을 실행 하 고 **학생** 탭을 클릭 합니다. 다음 오류가 발생 합니다.

*' Schoolcontext.cs ' 컨텍스트를 지 원하는 모델이 데이터베이스를 만든 이후 변경 되었습니다. Code First 마이그레이션를 사용 하 여 데이터베이스를 업데이트 하는 것이 좋습니다 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*

데이터베이스 모델이 변경 되어 데이터베이스 스키마를 변경 해야 하 고 Entity Framework 검색 되었습니다. UI를 사용 하 여 데이터베이스에 추가한 데이터를 잃지 않고 마이그레이션을 사용 하 여 스키마를 업데이트 합니다. `Seed` 메서드에서 만든 데이터를 변경한 경우 `Seed` 메서드에서 사용 하는 [Addorupdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) 방법 때문에 원래 상태로 다시 변경 됩니다. ([Addorupdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) 는 데이터베이스 용어에서의 "upsert" 작업과 동일 합니다.)

PMC(패키지 관리자 콘솔)에서 다음 명령을 입력합니다.

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

`add-migration MaxLengthOnNames` 명령은 *&lt;timeStamp&gt;\_MaxLengthOnNames.cs*이라는 파일을 만듭니다. 이 파일에는 현재 데이터 모델과 일치 하도록 데이터베이스를 업데이트 하는 코드가 포함 되어 있습니다. 마이그레이션 파일 이름 앞에 나오는 타임 스탬프는 Entity Framework에서 마이그레이션을 순서를 정렬 하는 데 사용 됩니다. 여러 마이그레이션을 만든 후, 데이터베이스를 삭제 하는 경우 또는 마이그레이션을 사용 하 여 프로젝트를 배포 하는 경우 모든 마이그레이션이 생성 된 순서 대로 적용 됩니다.

**만들기** 페이지를 실행 하 고 50 자 보다 긴 이름을 입력 합니다. 50 자를 초과 하면 클라이언트 쪽 유효성 검사는 즉시 오류 메시지를 표시 합니다.

![클라이언트 쪽 val 오류](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a>열 특성

또한 특성을 사용하여 클래스 및 속성을 데이터베이스에 매핑하는 방법을 제어할 수 있습니다. 필드에 중간 이름이 포함될 수 있으므로 첫 번째 이름 필드에 이름 `FirstMidName`을 사용한 경우를 가정합니다. 하지만 데이터베이스에 임시 쿼리를 작성하는 사용자는 해당 이름이 익숙하기 때문에 데이터베이스 열 이름을 `FirstName`으로 하려고 합니다. 이 매핑을 수행하기 위해 `Column` 특성을 사용할 수 있습니다.

`Column` 특성은 데이터베이스를 만드는 시기를 지정하고 `FirstMidName` 속성에 매핑하는 `Student` 테이블의 열 이름은 `FirstName`이 됩니다. 즉, 코드가 `Student.FirstMidName`을 참조하는 경우 데이터는 `Student` 테이블의 `FirstName` 열에서 가져오거나 업데이트됩니다. 열 이름을 지정 하지 않으면 속성 이름과 이름이 동일 하 게 지정 됩니다.

다음 강조 표시 된 코드에 표시 된 것과 같이 [system.componentmodel](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) 에 대 한 using 문과 열 이름 특성을 `FirstMidName` 속성에 추가 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

[열 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) 을 추가 하면 schoolcontext.cs를 지 원하는 모델이 변경 되므로 데이터베이스와 일치 하지 않습니다. PMC에 다음 명령을 입력 하 여 다른 마이그레이션을 만듭니다.

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

**서버 탐색기** (Express for Web을 사용 하는 경우**데이터베이스 탐색기** )에서 *학생* 테이블을 두 번 클릭 합니다.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

다음 그림에서는 처음 두 마이그레이션을 적용 하기 전의 원래 열 이름을 보여 줍니다. `FirstMidName`에서 `FirstName`로 바꾸는 열 이름 외에도 두 개의 name 열이 `MAX` 길이에서 50 자로 변경 되었습니다.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

이 자습서의 뒷부분에서 볼 수 있듯이 [흐름 API](https://msdn.microsoft.com/data/jj591617)를 사용 하 여 데이터베이스 매핑 변경을 수행할 수도 있습니다.

> [!NOTE]
> 이러한 모든 엔터티 클래스 만들기를 완료 하기 전에 컴파일하려고 하면 컴파일러 오류가 발생할 수 있습니다.

## <a name="create-the-instructor-entity"></a>강사 엔터티 만들기

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

*Models\Instructor.cs*을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

`Student` 및 `Instructor` 엔터티의 여러 속성은 동일합니다. 이 시리즈의 뒷부분에 나오는 [상속 구현](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) 자습서에서는이 중복성을 제거 하기 위해 상속을 사용 하 여 리팩터링 합니다.

### <a name="the-required-and-display-attributes"></a>필수 및 표시 특성

`LastName` 속성의 특성은 필수 필드 임을 지정 하 고, 입력란의 캡션은 "Last Name" (공백이 없는 "LastName")이 되 고 값이 50 자 보다 길면 안 됩니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

[Stringlength 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 은 데이터베이스의 최대 길이를 설정 하 고 ASP.NET MVC에 대 한 클라이언트 쪽 및 서버 쪽 유효성 검사를 제공 합니다. 이 특성의 최소 문자열 길이를 지정할 수도 있지만, 최소값은 데이터베이스 스키마에 영향을 주지 않습니다. DateTime, int, double 및 float와 같은 값 형식에는 [필수 특성이](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 필요 하지 않습니다. 값 형식에 null 값을 할당할 수 없으므로 기본적으로 필요 합니다. [필수 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 을 제거 하 고 `StringLength` 특성에 대 한 최소 길이 매개 변수로 바꿀 수 있습니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

여러 특성을 한 줄에 배치 하 여 다음과 같이 강사 클래스를 작성할 수도 있습니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a>FullName 계산 속성

`FullName`은 다른 두 개의 속성을 연결하여 생성되는 값을 반환하는 계산된 속성입니다. 따라서 `get` 접근자만 있으며 데이터베이스에 `FullName` 열이 생성 되지 않습니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>강좌 및 OfficeAssignment 탐색 속성

`Courses` 및 `OfficeAssignment` 속성은 탐색 속성입니다. 앞서 설명한 것 처럼 일반적으로는 [지연 로드](https://msdn.microsoft.com/magazine/hh205756.aspx)라는 Entity Framework 기능을 활용할 수 있도록 [가상](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) 으로 정의 됩니다. 또한 탐색 속성이 여러 엔터티를 포함할 수 있는 경우 해당 형식은 [ICollection&lt;t&gt;](https://msdn.microsoft.com/library/92t2ye13.aspx) 인터페이스를 구현 해야 합니다. 예를 들어, `IEnumerable<T>`는 [추가](https://msdn.microsoft.com/library/63ywd54z.aspx)를 구현 하지 않으므로 [IList&lt;t&gt;](https://msdn.microsoft.com/library/5y536ey6.aspx) 한정 하지만 [IEnumerable&lt;t&gt;](https://msdn.microsoft.com/library/9eekhta0.aspx) 는 그렇지 않습니다.

강사는 다양 한 과정을 학습할 수 있으므로 `Courses` `Course` 엔터티 컬렉션으로 정의 됩니다. 비즈니스 규칙 상태 강사는 최대 하나의 사무실만 가질 수 있으므로 `OfficeAssignment` 단일 `OfficeAssignment` 엔터티로 정의 됩니다 (office가 할당 되지 않은 경우 `null` 될 수 있음).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a>OfficeAssignment 엔터티 만들기

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

다음 코드를 사용 하 여 *Models\OfficeAssignment.cs* 를 만듭니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

변경 내용을 저장 하 고 컴파일러가 catch 할 수 있는 복사 및 붙여넣기 오류가 없는지 확인 하는 프로젝트를 빌드합니다.

### <a name="the-key-attribute"></a>키 특성

`Instructor`와 `OfficeAssignment` 엔터티 간에는 일 대 일 또는 일 관계가 있습니다. 사무실 할당은 할당 된 강사와 관련 하 여 존재 하므로 기본 키는 `Instructor` 엔터티에 대 한 외래 키 이기도 합니다. 그러나 Entity Framework는 이름이 `ID` 또는 *classname* `ID` 명명 규칙을 따르지 않으므로이 엔터티의 기본 키로 `InstructorID`를 자동으로 인식할 수 없습니다. 따라서 `Key` 특성은 키로 식별하는 데 사용됩니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

엔터티에 자체 기본 키가 있지만 속성 이름을 `classnameID` 또는 `ID`와 다르게 지정 하려는 경우에도 `Key` 특성을 사용할 수 있습니다. 기본적으로 EF는 식별 관계에 대 한 열 이기 때문에 키를 데이터베이스에서 생성 되지 않은 것으로 처리 합니다.

### <a name="the-foreignkey-attribute"></a>ForeignKey 특성

일 대 일 또는 일 대 일 관계 또는 두 엔터티 사이에 일 대 일 관계가 있는 경우 (예: `OfficeAssignment`와 `Instructor`) EF는 관계의 끝이 주 서버이 고 end가 종속 되는 작업을 수행할 수 없습니다. 일 대 일 관계에는 다른 클래스에 대 한 각 클래스의 참조 탐색 속성이 있습니다. [ForeignKey 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) 을 종속 클래스에 적용 하 여 관계를 설정할 수 있습니다. [ForeignKey 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)을 생략 하면 마이그레이션을 만들려고 할 때 다음과 같은 오류가 발생 합니다.

' ContosoUniversity ' 및 ' ContosoUniversity ' 형식 간의 연결에 대 한 주 끝을 확인할 수 없습니다. 이 연결의 주 끝은 relationship 흐름 API 또는 데이터 주석을 사용 하 여 명시적으로 구성 해야 합니다.

자습서의 뒷부분에서는 흐름 API를 사용 하 여이 관계를 구성 하는 방법을 보여 줍니다.

### <a name="the-instructor-navigation-property"></a>강사 탐색 속성

`Instructor` 엔터티에는 null을 허용 하는 `OfficeAssignment` 탐색 속성이 있으며 (강사에 게 office 할당이 없을 수 있음), `OfficeAssignment` 엔터티에는 null을 허용 하지 않는 `Instructor` 탐색 속성이 있습니다. (`InstructorID`은 (는) 비 null을 허용 하지 않고 office 할당을 사용할 수 없기 때문입니다. `Instructor` 엔터티에 관련 `OfficeAssignment` 엔터티가 있는 경우 각 엔터티는 해당 탐색 속성의 다른 엔터티에 대 한 참조를 가집니다.

강사 탐색 속성에 `[Required]` 특성을 배치 하 여 관련 강사가 있어야 하지만, InstructorID 외래 키 (이 테이블에 대 한 키 이기도 함)가 null을 허용 하지 않도록 지정할 필요는 없습니다.

## <a name="modify-the-course-entity"></a>강좌 엔터티 수정

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

*Models\Course.cs*에서 이전에 추가한 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

과정 엔터티에는 관련 `Department` 엔터티를 가리키는 외래 키 속성 `DepartmentID` 있으며 `Department` 탐색 속성이 있습니다. Entity Framework는 관련된 엔터티에 대한 탐색 속성이 있는 경우 사용자가 외래 키 속성을 데이터 모델에 추가하지 않아도 됩니다. EF는 필요할 때마다 데이터베이스에 외래 키를 자동으로 만듭니다. 하지만 데이터 모델에 외래 키가 있으면 더 간단하고 더 효율적으로 업데이트를 수행할 수 있습니다. 예를 들어 편집할 강의 엔터티를 인출 하는 경우 `Department` 엔터티를 로드 하지 않는 경우에는 null이 됩니다. 따라서 강좌 엔터티를 업데이트할 때 먼저 `Department` 엔터티를 인출 해야 합니다. 외래 키 속성 `DepartmentID` 데이터 모델에 포함 된 경우 업데이트 하기 전에 `Department` 엔터티를 페치할 필요가 없습니다.

### <a name="the-databasegenerated-attribute"></a>DatabaseGenerated 특성

`CourseID` 속성에 [None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) 매개 변수가 있는 [databasegenerated 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) 은 데이터베이스에 의해 생성 되는 것이 아니라 사용자가 기본 키 값을 제공 하도록 지정 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

기본적으로 Entity Framework는 데이터베이스에서 기본 키 값이 생성 된 것으로 가정 합니다. 이는 대부분의 시나리오에서 사용자가 원하는 것입니다. 그러나 `Course` 엔터티의 경우 한 부서의 1000 시리즈, 다른 부서에 대 한 2000 시리즈 등의 사용자 지정 강좌 번호를 사용 합니다.

### <a name="foreign-key-and-navigation-properties"></a>외래 키 및 탐색 속성

`Course` 엔터티의 외래 키 속성 및 탐색 속성은 다음과 같은 관계를 반영 합니다.

- 강좌는 한 부서에 할당되므로, 위에서 언급한 이유로 `DepartmentID` 외래 키와 `Department` 탐색 속성이 있습니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- 강좌에는 등록된 학생이 여러 명 있을 수 있으므로 `Enrollments` 탐색 속성은 컬렉션입니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- 여러 강사가 한 강좌를 수업할 수 있으므로 `Instructors` 탐색 속성은 컬렉션입니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a>부서 엔터티 만들기

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

다음 코드를 사용 하 여 *Models\Department.cs* 를 만듭니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>열 특성

이전에는 [열 특성](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) 을 사용 하 여 열 이름 매핑을 변경 했습니다. `Department` 엔터티에 대 한 코드에서 `Column` 특성은 SQL 데이터 형식 매핑을 변경 하는 데 사용 됩니다 .이 열은 데이터베이스에서 SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx) 형식을 사용 하 여 정의 됩니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

열 매핑은 일반적으로 필요 하지 않습니다. Entity Framework은 일반적으로 속성에 대해 정의 하는 CLR 형식을 기반으로 적절 한 SQL Server 데이터 형식을 선택 하기 때문입니다. CLR `decimal` 형식은 SQL Server `decimal` 유형에 매핑됩니다. 그러나이 경우 열은 통화 금액을 보유 하 고 있으며 [money](https://msdn.microsoft.com/library/ms179882.aspx) 데이터 형식이 더 적합 합니다.

### <a name="foreign-key-and-navigation-properties"></a>외래 키 및 탐색 속성

외래 키 및 탐색 속성은 다음과 같은 관계를 반영합니다.

- 부서는 관리자가 있을 수도 있고 없을 수도 있으며, 관리자는 항상 강사입니다. 따라서 `InstructorID` 속성은 `Instructor` 엔터티에 대 한 외래 키로 포함 되 고, `int` 형식 지정 후에 물음표를 추가 하 여 속성을 nullable로 표시 합니다. 탐색 속성의 이름은 `Administrator` 이지만 `Instructor` 엔터티는 포함 됩니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- 부서에 많은 강좌가 있을 수 있으므로 `Courses` 탐색 속성이 있습니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > 규칙에 따라 Entity Framework는 null 비허용 외래 키 및 다대다 관계에 대한 하위 삭제를 사용하도록 허용합니다. 이로 인해 순환 하위 삭제 규칙이 생성 될 수 있으며,이로 인해 이니셜라이저 코드가 실행 될 때 예외가 발생 합니다. 예를 들어 `Department.InstructorID` 속성을 null 허용으로 정의 하지 않은 경우 이니셜라이저가 실행 될 때 다음과 같은 예외 메시지가 표시 됩니다. "참조 관계로 인해 순환 참조가 허용 되지 않습니다." 비즈니스 규칙에서 속성을 null을 허용 하지 않는 것으로 `InstructorID` 해야 하는 경우 다음 흐름 API를 사용 하 여 관계에서 하위 삭제를 사용 하지 않도록 설정 해야 합니다. 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modifying-the-student-entity"></a>학생 엔터티 수정

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

*Models\Student.cs*에서 이전에 추가한 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a>등록 엔터티

 *Models\Enrollment.cs*에서 이전에 추가한 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a>외래 키 및 탐색 속성

외래 키 속성 및 탐색 속성은 다음 관계를 반영합니다.

- 등록 레코드는 단일 강좌에 해당하므로 `CourseID` 외래 키 속성 및 `Course` 탐색 속성이 있습니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- 등록 레코드는 단일 학생에 해당하므로 `StudentID` 외래 키 속성 및 `Student` 탐색 속성이 있습니다. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a>다대다 관계

`Student`와 `Course` 엔터티 사이에는 다 대 다 관계가 있으며, `Enrollment` 엔터티 함수는 데이터베이스의 *페이로드가 있는* 다대다 조인 테이블로 사용 됩니다. 즉, `Enrollment` 테이블은 조인 된 테이블에 대 한 외래 키 외에 추가 데이터 (이 경우에는 기본 키와 `Grade` 속성)를 포함 합니다.

다음 그림은 이러한 관계 모양을 엔터티 다이어그램으로 보여 줍니다. (이 다이어그램은 [Entity Framework 파워 도구](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d)를 사용 하 여 생성 되었습니다. 다이어그램을 만드는 것은 자습서의 일부가 아니므로 그림으로 사용 됩니다.)

![Student-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

각 관계선의 한쪽 끝에는 1이 있고 다른 하나에는 별표 (\*)가 있으며이는 일 대 다 관계를 나타냅니다.

`Enrollment` 테이블에 등급 정보가 포함 되지 않은 경우 `CourseID` 및 `StudentID`라는 두 개의 외래 키만 포함 해야 합니다. 이 경우에는 데이터베이스에서 페이로드 (또는 *순수 조인 테이블*)가 *없는* 다대다 조인 테이블에 해당 하므로 모델 클래스를 만들 필요가 없습니다. `Instructor` 및 `Course` 엔터티에는 이러한 종류의 다대다 관계가 있으며, 볼 수 있듯이 두 엔터티 사이에 엔터티 클래스가 없습니다.

![Instructor-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

그러나 다음 데이터베이스 다이어그램에 표시 된 것 처럼 데이터베이스에 조인 테이블이 필요 합니다.

![Instructor-Course_many-to-many_relationship_tables](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

Entity Framework는 `CourseInstructor` 테이블을 자동으로 만들고 `Instructor.Courses`를 읽고 업데이트 하 고 탐색 속성을 `Course.Instructors` 하 여 간접적으로 읽고 업데이트 합니다.

## <a name="entity-diagram-showing-relationships"></a>관계를 보여 주는 엔터티 다이어그램

다음 그림에는 Entity Framework 파워 도구가 완벽한 School 모델을 만드는 다이어그램이 나와 있습니다.

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

다 대 다 관계 선 (\*\*) 및 일 대 다 관계 줄 (1 ~ \*) 외에도 여기에서 `Instructor`와 `OfficeAssignment` 엔터티 사이에 일 대 일 또는 일 관계 줄 (1 ~ 0 ..1)을 표시 하 고, 강사와 부서 엔터티 사이에 0 또는 일대다 관계 줄 (0 ..1 ~ \*)을 지정할 수 있습니다.

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a>데이터베이스 컨텍스트에 코드를 추가 하 여 데이터 모델 사용자 지정

다음으로 `SchoolContext` 클래스에 새 엔터티를 추가 하 고 [흐름 API](https://msdn.microsoft.com/data/jj591617) 호출을 사용 하 여 일부 매핑을 사용자 지정 합니다. API는 일련의 메서드 호출을 단일 문으로 살펴볼 하는 경우가 종종 있기 때문에 "흐름"입니다.

이 자습서에서는 특성을 사용 하 여 수행할 수 없는 데이터베이스 매핑에 대해서만 흐름 API를 사용 합니다. 그러나 대부분의 서식 지정, 유효성 검사 및 매핑 규칙을 지정하는 데 흐름 API를 사용할 수 있습니다. `MinimumLength`와 같은 일부 특성은 흐름 API를 통해 적용할 수 없습니다. 앞에서 설명한 것 처럼 `MinimumLength` 스키마를 변경 하지 않고 클라이언트 및 서버 쪽 유효성 검사 규칙만 적용 합니다.

일부 개발자는 흐름 API를 단독으로 사용하는 것을 선호하므로 자신의 엔터티 클래스를 “정리”할 수 있습니다. 원하는 경우 특성과 흐름 API를 섞을 수 있으며, 흐름 API를 사용해야만 수행할 수 있는 몇 가지 사용자 지정이 있습니다. 하지만 일반적으로 이러한 두 가지 방법 중 하나를 선택하여 가능한 한 일관되게 사용하는 것이 좋습니다.

데이터 모델에 새 엔터티를 추가 하 고 특성을 사용 하 여 수행 하지 않은 데이터베이스 매핑을 수행 하려면 *DAL\SchoolContext.cs* 의 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

[Onmodelcreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) 메서드의 새 문은 다 대 다 조인 테이블을 구성 합니다.

- `Instructor`와 `Course` 엔터티 간의 다 대 다 관계의 경우 코드에서 조인 테이블의 테이블 및 열 이름을 지정 합니다. 이 코드를 사용 하지 않고 다 대 다 관계를 구성할 수 Code First 하지만 호출 하지 않는 경우에는 `InstructorID` 열의 `InstructorInstructorID`와 같은 기본 이름을 가져옵니다.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

다음 코드는 특성 대신 흐름 API를 사용 하 여 `Instructor`와 `OfficeAssignment` 엔터티 간의 관계를 지정 하는 방법의 예를 제공 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

백그라운드에서 수행 하는 "흐름 API" 문에 대 한 자세한 내용은 [흐름 API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) 블로그 게시물을 참조 하세요.

## <a name="seed-the-database-with-test-data"></a>테스트 데이터로 데이터베이스 시드

만든 새 엔터티에 대 한 시드 데이터를 제공 하기 위해 *migrations\ configuration.cs* 파일의 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

첫 번째 자습서에서 살펴본 것 처럼 대부분의이 코드는 새 엔터티 개체를 업데이트 하거나 만들며 테스트에 필요한 속성에 샘플 데이터를 로드 합니다. 그러나 `Instructor` 엔터티와 다 대 다 관계가 있는 `Course` 엔터티가 처리 되는 방식을 확인 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

`Course` 개체를 만들 때 코드 `Instructors = new List<Instructor>()`를 사용 하 여 `Instructors` 탐색 속성을 빈 컬렉션으로 초기화 합니다. 이렇게 하면 `Instructors.Add` 메서드를 사용 하 여이 `Course` 관련 된 `Instructor` 엔터티를 추가할 수 있습니다. 빈 목록을 만들지 않은 경우에는 `Instructors` 속성이 null이 고 `Add` 메서드가 없기 때문에 이러한 관계를 추가할 수 없습니다. 생성자에 목록 초기화를 추가할 수도 있습니다.

## <a name="add-a-migration-and-update-the-database"></a>마이그레이션을 추가 하 고 데이터베이스를 업데이트 합니다.

PMC에서 `add-migration` 명령을 입력 합니다.

`PM> add-Migration Chap4`

이 시점에서 데이터베이스를 업데이트 하려고 하면 다음과 같은 오류가 발생 합니다.

*ALTER TABLE 문이 FOREIGN KEY 제약 조건 "FK\_dbo와 충돌 했습니다. 과정\_dbo. 부서\_DepartmentID ". 데이터베이스 "ContosoUniversity", 테이블 "dbo .에서 충돌이 발생 했습니다. 부서 ", 열 ' DepartmentID '.*

&lt;*타임 스탬프&gt;\_Chap4.cs* 파일을 편집 하 고 다음 코드를 변경 합니다. SQL 문을 추가 하 고 `AddColumn` 문을 수정 합니다.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

새 항목을 추가할 때 기존 `AddColumn` 줄을 주석으로 처리 하거나 삭제 해야 합니다. 그렇지 않으면 `update-database` 명령을 입력할 때 오류가 발생 합니다.

기존 데이터를 사용 하 여 마이그레이션을 실행 하는 경우에는 데이터베이스에 스텁 데이터를 삽입 하 여 foreign key 제약 조건을 충족 해야 합니다 .이 작업을 수행 하는 것이 좋습니다. 생성 된 코드는 `Course` 테이블에 null을 허용 하지 않는 `DepartmentID` 외래 키를 추가 합니다. 코드가 실행 될 때 `Course` 테이블에 이미 행이 있는 경우 SQL Server에서 null이 될 수 없는 열에 넣을 값을 알 수 없기 때문에 `AddColumn` 작업이 실패 합니다. 따라서 코드를 변경 하 여 새 열에 기본값을 지정 하 고 "Temp" 라는 스텁 부서를 만들어 기본 학과 역할을 수행 했습니다. 따라서이 코드를 실행할 때 기존 `Course` 행이 있으면 모두 "Temp" 부서와 관련 됩니다.

`Seed` 메서드를 실행 하면 `Department` 테이블에 행이 삽입 되 고 기존 `Course` 행이 새 `Department` 행과 관련 됩니다. UI에 강좌를 추가 하지 않은 경우에는 더 이상 "Temp" 부서 또는 `Course.DepartmentID` 열에 기본값이 필요 하지 않습니다. 다른 사람이 응용 프로그램을 사용 하 여 과정을 추가 하는 경우에도 `Seed` 메서드 코드를 업데이트 하 여 열에서 기본값을 제거 하 고 "Temp" 부서를 삭제 하기 전에 `Course` 모든 행 (`Seed` 메서드의 이전 실행에서 삽입 한 행만)이 유효한 `DepartmentID` 값을 갖도록 할 수 있습니다.

&lt;*타임 스탬프&gt;\_Chap4.cs* 파일 편집을 마친 후에는 PMC에 `update-database` 명령을 입력 하 여 마이그레이션을 실행 합니다.

> [!NOTE]
> 데이터를 마이그레이션하고 스키마를 변경 하는 경우 다른 오류가 발생할 수 있습니다. 해결할 수 없는 마이그레이션 오류가 발생 하면 *web.config 파일에서* 연결 문자열을 변경 하거나 데이터베이스를 삭제할 수 있습니다. 가장 간단한 방법은 *web.config 파일에서* 데이터베이스 이름을 바꾸는 것입니다. 예를 들어 다음과 같이 데이터베이스 이름을 CU\_test로 변경 합니다.
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
> 새 데이터베이스를 사용 하면 마이그레이션할 데이터가 없으며 `update-database` 명령이 오류 없이 완료 될 가능성이 훨씬 높습니다. 데이터베이스를 삭제 하는 방법에 대 한 지침은 [Visual Studio 2012에서 데이터베이스](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)를 삭제 하는 방법을 참조 하세요.

이전 처럼 **서버 탐색기** 에서 데이터베이스를 열고 **테이블** 노드를 확장 하 여 모든 테이블이 생성 되었는지 확인 합니다. (이전에 **서버 탐색기** 열린 상태 이면 **새로 고침** 단추를 클릭 합니다.)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

`CourseInstructor` 테이블에 대 한 모델 클래스를 만들지 않았습니다. 앞에서 설명한 것 처럼 `Instructor`와 `Course` 엔터티 간의 다 대 다 관계에 대 한 조인 테이블입니다.

`CourseInstructor` 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시** 를 선택 하 여 `Course.Instructors` 탐색 속성에 추가한 `Instructor` 엔터티의 결과로 데이터가 있는지 확인 합니다.

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a>요약

이제 더 복잡한 데이터 모델 및 해당 데이터베이스가 만들어졌습니다. 다음 자습서에서는 관련 된 데이터에 액세스 하는 다양 한 방법에 대해 자세히 설명 합니다.

[ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
