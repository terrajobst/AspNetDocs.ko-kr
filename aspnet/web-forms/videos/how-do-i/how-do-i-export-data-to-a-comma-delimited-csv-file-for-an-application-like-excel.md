---
uid: web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
title: '[방법:] Excel과 같은 응용 프로그램의 CSV (쉼표로 구분 된 파일) 파일로 데이터 내보내기 | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서 Chris Pel는 데이터베이스 또는 다른 원본에서 데이터를 가져와서 응용 프로그램에서 사용할 수 있는 쉼표로 구분 된 파일로 내보내는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/22/2009
ms.assetid: c9df86ad-aec2-43d5-bb8a-413ebb666673
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
msc.type: video
ms.openlocfilehash: f27873eee345fe5347023b154de2b3833c9b6138
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458069"
---
# <a name="how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel"></a><span data-ttu-id="d0a6b-103">[방법:] Excel과 같은 응용 프로그램의 CSV (쉼표로 구분 된 파일) 파일로 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="d0a6b-103">[How Do I:] Export Data to a Comma Delimited (CSV) File for an Application Like Excel</span></span>

<span data-ttu-id="d0a6b-104">사람- [Chris pel](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="d0a6b-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="d0a6b-105">이 비디오에서 Chris Pel는 데이터베이스나 다른 원본에서 데이터를 가져와서 Excel과 같은 응용 프로그램에서 사용할 수 있는 쉼표로 구분 된 파일로 내보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d0a6b-105">In this video Chris Pels shows how to take data from a database or other source and export it to a comma delimited file that can be used in an application like Excel.</span></span> <span data-ttu-id="d0a6b-106">먼저 데이터 집합을 DataTable 개체로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0a6b-106">First, a set of data is created as a DataTable object.</span></span> <span data-ttu-id="d0a6b-107">그런 다음 현재 웹 페이지 요청에 대 한 응답이 지워지고 헤더 및 콘텐츠 형식이 csv 파일로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0a6b-107">Next, the Response for the current web page request is cleared and the header and content type are configured to be a csv file.</span></span> <span data-ttu-id="d0a6b-108">그런 다음 먼저 csv 파일에 대 한 열 헤더와 데이터 값을 차례로 작성 하 여 실제 데이터를 응답 스트림에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0a6b-108">Then the actual data is added to the response stream by first writing the column headers for the csv file followed by the data values.</span></span> <span data-ttu-id="d0a6b-109">이 방법은 사용자가 데이터를 내보내야 할 때 Excel과 같은 프로그램에서 로컬로 조작할 수 있는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0a6b-109">This approach can be useful when users require an export of data so it can be manipulated locally in a program like Excel.</span></span>

[<span data-ttu-id="d0a6b-110">&#9654;비디오 보기 (19 분)</span><span class="sxs-lookup"><span data-stu-id="d0a6b-110">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel)
