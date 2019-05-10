---
uid: mvc/overview/older-versions-1/models-data/index
title: 모델 (데이터) | Microsoft Docs
author: rick-anderson
description: 이 자습서 시리즈에서는 Microsoft Entity Framework를 사용 하 여 ASP.NET MVC를 사용 하는 방법을 알아봅니다. 이 자습서의이 코스를 통해 웹 응용 프로그램을 작성 하는 중...
ms.author: riande
ms.date: 09/28/2011
ms.assetid: 9086d8a8-7952-4a7e-82a7-724d48178555
msc.legacyurl: /mvc/overview/older-versions-1/models-data
msc.type: chapter
ms.openlocfilehash: e4e4cce840d46ceceeb3ea77db91ad99d73ef483
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117583"
---
# <a name="models-data"></a><span data-ttu-id="1bacd-104">모델(데이터)</span><span class="sxs-lookup"><span data-stu-id="1bacd-104">Models (Data)</span></span>

> <span data-ttu-id="1bacd-105">이 자습서 시리즈에서는 Microsoft Entity Framework를 사용 하 여 ASP.NET MVC를 사용 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1bacd-105">In this tutorial series, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="1bacd-106">이 자습서의이 코스를 통해 선택, 삽입, 업데이트 및 Entity Framework를 사용 하 여 데이터베이스 데이터를 삭제 하는 방법을 보여 주는 웹 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bacd-106">Over the course of this tutorial, you build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>

- [<span data-ttu-id="1bacd-107">Entity Framework를 사용하여 모델 클래스 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="1bacd-107">Creating Model Classes with the Entity Framework (C#)</span></span>](creating-model-classes-with-the-entity-framework-cs.md)
- [<span data-ttu-id="1bacd-108">LINQ to SQL을 사용하여 모델 클래스 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="1bacd-108">Creating Model Classes with LINQ to SQL (C#)</span></span>](creating-model-classes-with-linq-to-sql-cs.md)
- [<span data-ttu-id="1bacd-109">데이터베이스 데이터의 테이블 표시(C#)</span><span class="sxs-lookup"><span data-stu-id="1bacd-109">Displaying a Table of Database Data (C#)</span></span>](displaying-a-table-of-database-data-cs.md)
- [<span data-ttu-id="1bacd-110">간단한 유효성 검사 수행(C#)</span><span class="sxs-lookup"><span data-stu-id="1bacd-110">Performing Simple Validation (C#)</span></span>](performing-simple-validation-cs.md)
- [<span data-ttu-id="1bacd-111">IDataErrorInfo 인터페이스를 사용한 유효성 검사(C#)</span><span class="sxs-lookup"><span data-stu-id="1bacd-111">Validating with the IDataErrorInfo Interface (C#)</span></span>](validating-with-the-idataerrorinfo-interface-cs.md)
- [<span data-ttu-id="1bacd-112">서비스 레이어를 사용한 유효성 검사(C#)</span><span class="sxs-lookup"><span data-stu-id="1bacd-112">Validating with a Service Layer (C#)</span></span>](validating-with-a-service-layer-cs.md)
- [<span data-ttu-id="1bacd-113">데이터 주석 유효성 검사기를 사용한 유효성 검사(C#)</span><span class="sxs-lookup"><span data-stu-id="1bacd-113">Validation with the Data Annotation Validators (C#)</span></span>](validation-with-the-data-annotation-validators-cs.md)
- [<span data-ttu-id="1bacd-114">Entity Framework를 사용하여 모델 클래스 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="1bacd-114">Creating Model Classes with the Entity Framework (VB)</span></span>](creating-model-classes-with-the-entity-framework-vb.md)
- [<span data-ttu-id="1bacd-115">LINQ to SQL을 사용하여 모델 클래스 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="1bacd-115">Creating Model Classes with LINQ to SQL (VB)</span></span>](creating-model-classes-with-linq-to-sql-vb.md)
- [<span data-ttu-id="1bacd-116">데이터베이스 데이터의 테이블 표시(VB)</span><span class="sxs-lookup"><span data-stu-id="1bacd-116">Displaying a Table of Database Data (VB)</span></span>](displaying-a-table-of-database-data-vb.md)
- [<span data-ttu-id="1bacd-117">간단한 유효성 검사 수행(VB)</span><span class="sxs-lookup"><span data-stu-id="1bacd-117">Performing Simple Validation (VB)</span></span>](performing-simple-validation-vb.md)
- [<span data-ttu-id="1bacd-118">IDataErrorInfo 인터페이스를 사용한 유효성 검사(VB)</span><span class="sxs-lookup"><span data-stu-id="1bacd-118">Validating with the IDataErrorInfo Interface (VB)</span></span>](validating-with-the-idataerrorinfo-interface-vb.md)
- [<span data-ttu-id="1bacd-119">서비스 레이어를 사용한 유효성 검사(VB)</span><span class="sxs-lookup"><span data-stu-id="1bacd-119">Validating with a Service Layer (VB)</span></span>](validating-with-a-service-layer-vb.md)
- [<span data-ttu-id="1bacd-120">데이터 주석 유효성 검사기를 사용한 유효성 검사(VB)</span><span class="sxs-lookup"><span data-stu-id="1bacd-120">Validation with the Data Annotation Validators (VB)</span></span>](validation-with-the-data-annotation-validators-vb.md)
