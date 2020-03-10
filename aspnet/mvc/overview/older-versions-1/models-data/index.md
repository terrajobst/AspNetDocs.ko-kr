---
uid: mvc/overview/older-versions-1/models-data/index
title: 모델 (데이터) | Microsoft Docs
author: rick-anderson
description: 이 자습서 시리즈에서는 Microsoft Entity Framework에서 ASP.NET MVC를 사용 하는 방법에 대해 알아봅니다. 이 자습서에서는 웹 응용 프로그램을 빌드하는 과정을 안내 합니다.
ms.author: riande
ms.date: 09/28/2011
ms.assetid: 9086d8a8-7952-4a7e-82a7-724d48178555
msc.legacyurl: /mvc/overview/older-versions-1/models-data
msc.type: chapter
ms.openlocfilehash: e4e4cce840d46ceceeb3ea77db91ad99d73ef483
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469427"
---
# <a name="models-data"></a><span data-ttu-id="e2254-104">모델(데이터)</span><span class="sxs-lookup"><span data-stu-id="e2254-104">Models (Data)</span></span>

> <span data-ttu-id="e2254-105">이 자습서 시리즈에서는 Microsoft Entity Framework에서 ASP.NET MVC를 사용 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e2254-105">In this tutorial series, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="e2254-106">이 자습서에서는 Entity Framework를 사용 하 여 데이터베이스 데이터를 선택, 삽입, 업데이트 및 삭제 하는 방법을 보여 주는 웹 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2254-106">Over the course of this tutorial, you build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>

- [<span data-ttu-id="e2254-107">Entity Framework를 사용하여 모델 클래스 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="e2254-107">Creating Model Classes with the Entity Framework (C#)</span></span>](creating-model-classes-with-the-entity-framework-cs.md)
- [<span data-ttu-id="e2254-108">LINQ to SQL을 사용하여 모델 클래스 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="e2254-108">Creating Model Classes with LINQ to SQL (C#)</span></span>](creating-model-classes-with-linq-to-sql-cs.md)
- [<span data-ttu-id="e2254-109">데이터베이스 데이터의 테이블 표시(C#)</span><span class="sxs-lookup"><span data-stu-id="e2254-109">Displaying a Table of Database Data (C#)</span></span>](displaying-a-table-of-database-data-cs.md)
- [<span data-ttu-id="e2254-110">간단한 유효성 검사 수행(C#)</span><span class="sxs-lookup"><span data-stu-id="e2254-110">Performing Simple Validation (C#)</span></span>](performing-simple-validation-cs.md)
- [<span data-ttu-id="e2254-111">IDataErrorInfo 인터페이스를 사용한 유효성 검사(C#)</span><span class="sxs-lookup"><span data-stu-id="e2254-111">Validating with the IDataErrorInfo Interface (C#)</span></span>](validating-with-the-idataerrorinfo-interface-cs.md)
- [<span data-ttu-id="e2254-112">서비스 레이어를 사용한 유효성 검사(C#)</span><span class="sxs-lookup"><span data-stu-id="e2254-112">Validating with a Service Layer (C#)</span></span>](validating-with-a-service-layer-cs.md)
- [<span data-ttu-id="e2254-113">데이터 주석 유효성 검사기를 사용한 유효성 검사(C#)</span><span class="sxs-lookup"><span data-stu-id="e2254-113">Validation with the Data Annotation Validators (C#)</span></span>](validation-with-the-data-annotation-validators-cs.md)
- [<span data-ttu-id="e2254-114">Entity Framework를 사용하여 모델 클래스 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="e2254-114">Creating Model Classes with the Entity Framework (VB)</span></span>](creating-model-classes-with-the-entity-framework-vb.md)
- [<span data-ttu-id="e2254-115">LINQ to SQL을 사용하여 모델 클래스 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="e2254-115">Creating Model Classes with LINQ to SQL (VB)</span></span>](creating-model-classes-with-linq-to-sql-vb.md)
- [<span data-ttu-id="e2254-116">데이터베이스 데이터의 테이블 표시(VB)</span><span class="sxs-lookup"><span data-stu-id="e2254-116">Displaying a Table of Database Data (VB)</span></span>](displaying-a-table-of-database-data-vb.md)
- [<span data-ttu-id="e2254-117">간단한 유효성 검사 수행(VB)</span><span class="sxs-lookup"><span data-stu-id="e2254-117">Performing Simple Validation (VB)</span></span>](performing-simple-validation-vb.md)
- [<span data-ttu-id="e2254-118">IDataErrorInfo 인터페이스를 사용한 유효성 검사(VB)</span><span class="sxs-lookup"><span data-stu-id="e2254-118">Validating with the IDataErrorInfo Interface (VB)</span></span>](validating-with-the-idataerrorinfo-interface-vb.md)
- [<span data-ttu-id="e2254-119">서비스 레이어를 사용한 유효성 검사(VB)</span><span class="sxs-lookup"><span data-stu-id="e2254-119">Validating with a Service Layer (VB)</span></span>](validating-with-a-service-layer-vb.md)
- [<span data-ttu-id="e2254-120">데이터 주석 유효성 검사기를 사용한 유효성 검사(VB)</span><span class="sxs-lookup"><span data-stu-id="e2254-120">Validation with the Data Annotation Validators (VB)</span></span>](validation-with-the-data-annotation-validators-vb.md)
