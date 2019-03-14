---
title: Razor 구성 요소 레이아웃
author: guardrex
description: Blazor 및 Razor 구성 요소 앱에 대 한 재사용 가능한 레이아웃 구성 요소를 만드는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/layouts
ms.openlocfilehash: 23d8f441c0b3bbde7a73717f6257013831617ec0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039040"
---
# <a name="razor-components-layouts"></a>Razor 구성 요소 레이아웃

[Rainer Stropek](https://www.timecockpit.com)

앱에는 대개 둘 이상의 페이지가 포함 됩니다. 메뉴, 저작권 메시지 및 로고와 같은 레이아웃 요소를 모든 페이지에 있어야 합니다. 이러한 레이아웃 요소의 코드의 모든 앱의 페이지에 복사 하 고 효율적인 솔루션이 아닙니다. 이러한 중복을 유지 관리 하 고 아마도 시간에 따른 일관 되지 않은 콘텐츠에 이어집니다. *레이아웃* 이 문제를 해결 합니다.

기술적으로 레이아웃에는 다른 구성 요소입니다. Razor 템플릿 또는 레이아웃을 정의 된 C# 코드 및 데이터 바인딩, 종속성 주입 및 다른 일반 기능의 구성 요소를 포함할 수 있습니다. 설정 하는 두 가지 추가적인 측면을 *구성 요소* 에 *레이아웃*:

* 레이아웃 구성 요소에서 상속 해야 `BlazorLayoutComponent`합니다. `BlazorLayoutComponent` 정의 `Body` 레이아웃 내에서 렌더링할 콘텐츠를 포함 하는 속성입니다.
* 레이아웃 구성 요소를 사용 합니다 `Body` 본문 콘텐츠에 표시 될 위치를 지정 하는 속성 Razor 구문을 사용 하 여 렌더링 `@Body`합니다. 렌더링 하는 동안 `@Body` 레이아웃의 내용으로 바뀝니다.

다음 코드 샘플에는 레이아웃 요소의 Razor 템플릿을 보여 줍니다. 사용 하 여 `BlazorLayoutComponent` 고 `@Body`:

```csharp
@inherits BlazorLayoutComponent

<header>
    <h1>ERP Master 3000</h1>
</header>

<nav>
    <a href="master-data">Master Data Management</a>
    <a href="invoicing">Invoicing</a>
    <a href="accounting">Accounting</a>
</nav>

@Body

<footer>
    &copy; by @CopyrightMessage
</footer>

@functions {
    public string CopyrightMessage { get; set; }
    ...
}
```

## <a name="use-a-layout-in-a-component"></a>구성 요소에서 레이아웃을 사용 하 여

Razor 지시문을 사용 하 여 `@layout` 구성 요소에 레이아웃을 적용 합니다. 컴파일러는 변환에이 지시문을 `LayoutAttribute`, 구성 요소 클래스에 적용 되는 합니다.

다음 코드 예제에서는 개념을 보여 줍니다. 이 구성 요소의 내용이 삽입 됩니다 합니다 *MasterLayout* 의 위치에 `@Body`:

```csharp
@layout MasterLayout

@page "/master-data"

<h2>Master Data Management</h2>
...
```

## <a name="centralized-layout-selection"></a>중앙 집중식된 레이아웃 선택

모든 폴더는 앱은 명명 된 템플릿 파일을 포함할 수도 있습니다 *_ViewImports.cshtml*합니다. 컴파일러는 동일한 폴더에서 Razor 템플릿 및 모든 하위 폴더에 재귀적으로 모든 뷰 가져오기 파일에 지정 된 지시문을 포함 합니다. 따라서를 *_ViewImports.cshtml* 포함 된 파일 `@layout MainLayout` 폴더를 사용 하는 구성 요소의 모든는 *MainLayout* 레이아웃 합니다. 반복적으로 추가할 필요가 없습니다 `@layout` 의 모든 항목에  *\*.cshtml* 파일입니다.

기본 템플릿을 사용 하는 참고 합니다 *_ViewImports.cshtml* 레이아웃을 선택 하기 위한 메커니즘입니다. 새로 만든된 앱을 포함 합니다 *_ViewImports.cshtml* 파일을 *페이지* 폴더입니다.

## <a name="nested-layouts"></a>중첩 된 레이아웃

중첩 된 레이아웃의 앱 구성 될 수 있습니다. 구성 요소에서 다른 레이아웃을 참조 하는 레이아웃을 참조할 수 있습니다. 예를 들어 중첩 레이아웃 다중 수준 메뉴 구조를 반영 하기 위해 사용할 수 있습니다.

다음 코드 샘플에는 중첩 된 레이아웃을 사용 하는 방법을 보여 줍니다. 합니다 *CustomersComponent.cshtml* 파일은 표시할 구성 요소입니다. 구성 요소는 레이아웃을 참조 하는 참고 `MasterDataLayout`합니다.

*CustomersComponent.cshtml*:

```csharp
@layout MasterDataLayout

@page "/master-data/customers"

<h1>Customer Maintenance</h1>
...
```

*MasterDataLayout.cshtml* 파일은 제공 된 `MasterDataLayout`합니다. 다른 레이아웃을 참조 하는 레이아웃 `MainLayout`, 포함할 수 있는 것입니다.

*MasterDataLayout.cshtml*:

```csharp
@layout MainLayout
@inherits BlazorLayoutComponent

<nav>
    <!-- Menu structure of master data module -->
    ...
</nav>

@Body
```

마지막으로, `MainLayout` 머리글, 바닥글 및 주 메뉴와 같은 최상위 레이아웃 요소를 포함 합니다.

*MainLayout.cshtml*:

```csharp
@inherits BlazorLayoutComponent

<header>...</header>
<nav>...</nav>

@Body
```
