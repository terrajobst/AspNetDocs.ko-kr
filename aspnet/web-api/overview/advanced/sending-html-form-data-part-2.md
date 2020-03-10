---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'ASP.NET Web API에서 HTML 양식 데이터 보내기: 파일 업로드 및 Multipart MIME-ASP.NET 4.x'
author: MikeWasson
description: 이 자습서에서는 web API에 파일을 업로드 하는 방법을 보여 줍니다. 또한 다중 파트 MIME 데이터를 처리 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449213"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a>ASP.NET Web API에서 HTML 양식 데이터 보내기: 파일 업로드 및 다중 파트 MIME

[Mike Wasson](https://github.com/MikeWasson)

## <a name="part-2-file-upload-and-multipart-mime"></a>2 부: 파일 업로드 및 다중 파트 MIME

이 자습서에서는 web API에 파일을 업로드 하는 방법을 보여 줍니다. 또한 다중 파트 MIME 데이터를 처리 하는 방법을 설명 합니다.

> [!NOTE]
> [완료 된 프로젝트를 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)합니다.

다음은 파일을 업로드 하는 HTML 형식의 예입니다.

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

이 폼에는 텍스트 입력 컨트롤과 파일 입력 컨트롤이 포함 되어 있습니다. 양식에 파일 입력 컨트롤이 포함 되어 있는 경우 **enctype** 특성은 항상 다중 파트/폼 데이터&quot;&quot;해야 하며,이는 양식이 다중 파트 MIME 메시지로 전송 됨을 지정 합니다.

다중 파트 MIME 메시지의 형식은 예제 요청을 살펴보면 이해 하기 쉽습니다.

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

이 메시지는 각 폼 컨트롤에 대해 하나씩 두 *부분*으로 나뉩니다. 부분 경계는 대시로 시작 하는 선으로 표시 됩니다.

> [!NOTE]
> 부분 경계는 임의의 구성 요소 (&quot;41184676334&quot;)를 포함 하 여 경계 문자열이 메시지 파트 내에 실수로 표시 되지 않도록 합니다.

각 메시지 파트에는 하나 이상의 헤더와 파트 내용이 포함 되어 있습니다.

- 콘텐츠 처리 헤더에는 컨트롤 이름이 포함 됩니다. 파일의 경우 파일 이름도 포함 됩니다.
- Content-type 헤더는 파트의 데이터를 설명 합니다. 이 헤더를 생략 하면 기본값은 text/일반입니다.

이전 예제에서 사용자는 content 형식이 image/jpeg; 인 GrandCanyon 라는 파일을 업로드 했습니다. 텍스트 입력 값은 여름 휴가&quot;&quot;되었습니다.

## <a name="file-upload"></a>파일 업로드

이제 다중 파트 MIME 메시지에서 파일을 읽는 Web API 컨트롤러를 살펴보겠습니다. 그러면 컨트롤러에서 파일을 비동기적으로 읽습니다. Web API는 [작업 기반 프로그래밍 모델](https://msdn.microsoft.com/library/dd460693.aspx)을 사용 하 여 비동기 작업을 지원 합니다. 먼저 **async** 및 **wait** 키워드를 지 원하는 .NET Framework 4.5를 대상으로 하는 경우 코드는 다음과 같습니다.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

컨트롤러 작업은 매개 변수를 사용 하지 않습니다. 미디어 형식 포맷터를 호출 하지 않고 작업 내에서 요청 본문을 처리 하기 때문입니다.

**Ismultipartcontent** 메서드는 요청에 다중 파트 MIME 메시지가 포함 되어 있는지 여부를 확인 합니다. 그렇지 않으면 컨트롤러는 HTTP 상태 코드 415 (지원 되지 않는 미디어 형식)을 반환 합니다.

**Multipartformdatastreamprovider** 클래스는 업로드 된 파일에 대 한 파일 스트림을 할당 하는 도우미 개체입니다. 다중 파트 MIME 메시지를 읽으려면 **ReadAsMultipartAsync** 메서드를 호출 합니다. 이 메서드는 모든 메시지 파트를 추출 하 여 **Multipartformdatastreamprovider**에서 제공 하는 스트림에 씁니다.

메서드가 완료 되 면 **Multipartfiledata** 개체의 컬렉션인 **filedata** 속성에서 파일에 대 한 정보를 가져올 수 있습니다.

- **Multipartfiledata. FileName** 은 파일을 저장 한 서버의 로컬 파일 이름입니다.
- **Multipartfiledata. 헤더** 는 파트 헤더 (요청 헤더*아님* )를 포함 합니다. 이를 사용 하 여 콘텐츠\_처리 및 콘텐츠 형식 헤더에 액세스할 수 있습니다.

이름에서 알 수 있듯이 **ReadAsMultipartAsync** 는 비동기 메서드입니다. 메서드가 완료 된 후 작업을 수행 하려면 [연속 작업](https://msdn.microsoft.com/library/ee372288.aspx) (.net 4.0) 또는 **wait** 키워드 (.net 4.5)를 사용 합니다.

이전 코드의 .NET Framework 4.0 버전은 다음과 같습니다.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a>양식 컨트롤 데이터 읽기

앞에서 살펴본 HTML 폼에는 텍스트 입력 컨트롤이 있습니다.

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

**Multipartformdatastreamprovider**의 **formdata** 속성에서 컨트롤의 값을 가져올 수 있습니다.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

**Formdata** 는 폼 컨트롤에 대 한 이름/값 쌍을 포함 하는 **NameValueCollection** 입니다. 컬렉션에 중복 키가 포함 될 수 있습니다. 다음 형식을 고려 합니다.

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

요청 본문은 다음과 같습니다.

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

이 경우 **Formdata** 컬렉션에는 다음과 같은 키/값 쌍이 포함 됩니다.

- 트립: 왕복
- 옵션: 비 중지
- 옵션: 날짜
- 좌석: 창
