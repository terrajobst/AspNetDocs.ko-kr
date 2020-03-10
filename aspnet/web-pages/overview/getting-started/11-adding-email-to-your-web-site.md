---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: ASP.NET 웹 페이지 (Razor) 사이트에서 전자 메일 보내기 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 웹 사이트에서 자동화 된 전자 메일 메시지를 보내는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 23e9717329525fb5a0ed505c9dc94505d4f9dbbe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515327"
---
# <a name="sending-email-from-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 전자 메일 보내기

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 웹 사이트에서 전자 메일 메시지를 보내는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - 웹 사이트에서 전자 메일 메시지를 보내는 방법입니다.
> - 전자 메일 메시지에 파일을 첨부 하는 방법
> 
> 다음은이 문서에서 소개 하는 ASP.NET 기능입니다.
> 
> - `WebMail` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.

<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a>웹 사이트에서 전자 메일 메시지 보내기

웹 사이트에서 전자 메일을 보내야 할 수 있는 모든 종류의 이유가 있습니다. 사용자에 게 확인 메시지를 보내거나 사용자에 게 알림을 보낼 수 있습니다 (예: 새 사용자가 등록 한 경우). `WebMail` 도우미를 사용 하면 쉽게 전자 메일을 보낼 수 있습니다.

`WebMail` 도우미를 사용 하려면 SMTP 서버에 대 한 액세스 권한이 있어야 합니다. SMTP는 *간단한 메일 전송 프로토콜*을 의미 합니다. SMTP 서버는 받는 사람의 서버 &#8212; 에 메시지를 전달 하는 전자 메일 서버입니다 .이는 전자 메일의 아웃 바운드 쪽입니다. 웹 사이트에 대 한 호스팅 공급자를 사용 하는 경우 전자 메일을 설정 하 고 SMTP 서버 이름을 사용자에 게 알려줄 수 있습니다. 회사 네트워크 내에서 작업 하는 경우 관리자 또는 IT 부서에서 일반적으로 사용할 수 있는 SMTP 서버에 대 한 정보를 제공할 수 있습니다. 집에서 작업 하는 경우 일반 전자 메일 공급자를 사용 하 여 테스트할 수 있으며, 사용자는 SMTP 서버의 이름을 알려줄 수 있습니다. 일반적으로 다음이 필요 합니다.

- SMTP 서버의 이름입니다.
- 포트 번호입니다. 이것은 거의 항상 25입니다. 그러나 ISP에서 포트 587를 사용 하도록 요구할 수 있습니다. 전자 메일에 SSL (secure sockets layer)을 사용 하는 경우 다른 포트가 필요할 수 있습니다. 전자 메일 공급자에 게 문의 하세요.
- 자격 증명 (사용자 이름, 암호)

이 절차에서는 두 페이지를 만듭니다. 첫 번째 페이지에는 기술 지원 양식에 입력 한 것 처럼 사용자가 설명을 입력할 수 있는 양식이 있습니다. 첫 번째 페이지는 두 번째 페이지로 정보를 전송 합니다. 두 번째 페이지에서 코드는 사용자 정보를 추출 하 고 전자 메일 메시지를 보냅니다. 또한 문제 보고서를 받았는지 확인 하는 메시지를 표시 합니다.

![[이미지]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> 이 예제를 간단 하 게 유지 하기 위해 코드는 사용 하는 페이지에서 `WebMail` 도우미를 바로 초기화 합니다. 그러나 실제 웹 사이트의 경우에는 웹 사이트의 모든 파일에 대 한 `WebMail` 도우미를 초기화 하도록 전역 파일에이와 같은 초기화 코드를 배치 하는 것이 더 좋습니다. 자세한 내용은 [ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)을 참조 하세요.

1. 새 웹 사이트를 만듭니다.
2. *Emailrequest. cshtml* 이라는 새 페이지를 추가 하 고 다음 태그를 추가 합니다. 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    Form 요소의 `action` 특성이 *ProcessRequest*로 설정 되어 있는지 확인 합니다. 이는 양식이 현재 페이지로 다시 전송 되는 대신 해당 페이지로 전송 됨을 의미 합니다.
3. *ProcessRequest* 라는 새 페이지를 웹 사이트에 추가 하 고 다음 코드 및 태그를 추가 합니다.   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    코드에서 페이지에 전송 된 양식 필드의 값을 가져옵니다. 그런 다음 `WebMail` 도우미의 `Send` 메서드를 호출 하 여 전자 메일 메시지를 만들고 보냅니다. 이 경우 사용할 값은 폼에서 전송 된 값과 연결 하는 텍스트로 구성 됩니다.

    이 페이지에 대 한 코드는 `try/catch` 블록 내에 있습니다. 어떤 이유로 든 전자 메일을 보내려고 시도 하지 않는 경우 (예: 설정이 적절 하지 않은 경우) `catch` 블록의 코드가 실행 되 고 `errorMessage` 변수를 발생 한 오류로 설정 합니다. `try/catch` 블록 또는 `<text>` 태그에 대 한 자세한 내용은 [Razor 구문을 사용한 ASP.NET 웹 페이지 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors)를 참조 하세요.

    페이지 본문에서 `errorMessage` 변수가 비어 있으면 (기본값) 사용자에 게 전자 메일 메시지가 전송 되었다는 메시지가 표시 됩니다. `errorMessage` 변수를 true로 설정 하면 메시지를 보내는 데 문제가 있음을 사용자에 게 표시 합니다.

    오류 메시지를 표시 하는 페이지 부분에는 추가 테스트 인 `if(debuggingFlag)`있습니다. 전자 메일을 보내는 데 문제가 있는 경우이 변수를 true로 설정할 수 있습니다. `debuggingFlag` true 이면 전자 메일을 보내는 데 문제가 있는 경우 전자 메일 메시지를 보내려고 할 때 보고 된 ASP.NET을 보여 주는 추가 오류 메시지가 표시 됩니다. 양호 경고: ASP.NET에서 전자 메일 메시지를 보낼 수 없을 때 보고 하는 오류 메시지는 제네릭일 수 있습니다. 예를 들어 ASP.NET에서 SMTP 서버에 연결할 수 없는 경우 (예: 서버 이름에 오류가 발생 한 경우) 오류가 `Failure sending mail`됩니다.

    > [!NOTE] 
    > 
    > **중요** 예외 개체 (코드의`ex`)에서 오류 메시지가 표시 되 면 해당 메시지를 사용자에 게 정기적으로 전달 *하지* 마십시오. 예외 개체에는 종종 사용자에 게 표시 되지 않아야 하는 정보가 포함 되며 보안 취약성이 있을 수 있습니다. 이로 인해이 코드에는 오류 메시지를 표시 하는 스위치로 사용 되는 `debuggingFlag` 변수 및 기본적으로 변수가 false로 설정 된 이유가 포함 됩니다. 전자 메일을 보내는 데 문제가 발생 하 여 디버깅 해야 하는 경우에 *만* 해당 변수를 true로 설정 하 여 오류 메시지를 표시 해야 합니다. 문제를 해결 한 후에는 `debuggingFlag`을 false로 다시 설정 합니다.

    코드에서 다음과 같은 전자 메일 관련 설정을 수정 합니다.

   - `your-SMTP-host`를 액세스할 수 있는 SMTP 서버의 이름으로 설정 합니다.
   - `your-user-name-here`를 SMTP 서버 계정에 대 한 사용자 이름으로 설정 합니다.
   - `your-account-password`를 SMTP 서버 계정의 암호로 설정 합니다.
   - `your-email-address-here`를 본인의 전자 메일 주소로 설정 합니다. 메시지가 전송 되는 전자 메일 주소입니다. (일부 전자 메일 공급자는 다른 `From` 주소를 지정 하는 것을 허용 하지 않으며 사용자 이름을 `From` 주소로 사용 합니다.)

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a>전자 메일 설정 구성
     > 
     > SMTP 서버, 포트 번호 등에 대해 적절 한 설정이 있는지 확인 하는 것이 어려울 수 있습니다. 다음은 이에 대한 몇 가지 팁입니다.
     > 
     > - SMTP 서버 이름은 `smtp.provider.com` 또는 `smtp.provider.net`와 같은 경우가 많습니다. 그러나 호스팅 공급자에 사이트를 게시 하는 경우 해당 지점에서 SMTP 서버 이름이 `localhost`될 수 있습니다. 이는 게시 되 고 사이트는 공급자의 서버에서 실행 되기 때문입니다. 전자 메일 서버는 응용 프로그램의 관점에서 로컬 일 수 있습니다. 서버 이름을 변경 하면 게시 프로세스의 일부로 SMTP 서버 이름을 변경 해야 할 수 있습니다.
     > - 포트 번호는 일반적으로 25입니다. 그러나 일부 공급자는 포트 587 또는 다른 포트를 사용 해야 합니다.
     > - 올바른 자격 증명을 사용 하는지 확인 합니다. 호스팅 공급자에 사이트를 게시 한 경우 공급자가 특별히 표시 한 자격 증명을 전자 메일에 사용 합니다. 이러한 자격 증명은 게시 하는 데 사용 하는 자격 증명과 다를 수 있습니다.
     > - 자격 증명이 필요 하지 않은 경우도 있습니다. 개인 ISP를 사용 하 여 전자 메일을 보내는 경우 메일 공급자가 이미 자격 증명을 알고 있을 수 있습니다. 게시 한 후 로컬 컴퓨터에서 테스트 하는 경우와 다른 자격 증명을 사용 해야 할 수 있습니다.
     > - 전자 메일 공급자가 암호화를 사용 하는 경우 `WebMail.EnableSsl`를 `true`으로 설정 해야 합니다.
4. 브라우저에서 *Emailrequest. cshtml* 페이지를 실행 합니다. (파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.)
5. 사용자 이름과 문제 설명을 입력 한 다음 **제출** 단추를 클릭 합니다. 메시지를 확인 하 고 전자 메일 메시지를 보내는 *ProcessRequest* 페이지로 리디렉션됩니다. 

    ![[이미지]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a>전자 메일을 사용 하 여 파일 보내기

전자 메일 메시지에 첨부 된 파일을 보낼 수도 있습니다. 이 절차에서는 텍스트 파일과 두 개의 HTML 페이지를 만듭니다. 텍스트 파일을 전자 메일 첨부 파일로 사용 합니다.

1. 웹 사이트에서 새 텍스트 파일을 추가 하 고 이름을 *MyFile*로 추가 합니다.
2. 다음 텍스트를 복사 하 여 파일에 붙여 넣습니다. 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. *Sendfile. cshtml* 라는 페이지를 만들고 다음 태그를 추가 합니다. 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. *Processfile. cshtml* 라는 페이지를 만들고 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. 예제의 코드에서 다음 전자 메일 관련 설정을 수정 합니다.

    - `your-SMTP-host`를 액세스할 수 있는 SMTP 서버의 이름으로 설정 합니다.
    - `your-user-name-here`를 SMTP 서버 계정에 대 한 사용자 이름으로 설정 합니다.
    - `your-email-address-here`를 본인의 전자 메일 주소로 설정 합니다. 메시지가 전송 되는 전자 메일 주소입니다.
    - `your-account-password`를 SMTP 서버 계정의 암호로 설정 합니다.
    - `target-email-address-here`를 본인의 전자 메일 주소로 설정 합니다. 이전에는 일반적으로 다른 사람에 게 전자 메일을 보내면 테스트를 위해 자신에 게 전자 메일을 보낼 수 있습니다.
6. 브라우저에서 *Sendfile. cshtml* 페이지를 실행 합니다.
7. 이름, 제목 줄 및 첨부할 텍스트 파일의 이름을 입력 합니다 (*MyFile*).
8. `Submit` 단추를 클릭합니다. 이전과 마찬가지로 메시지를 확인 하 고 첨부 파일을 포함 하는 전자 메일 메시지를 보내는 *Processfile. cshtml* 페이지로 리디렉션됩니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [ASP.NET 웹 페이지(Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)
- [간단한 메일 전송 프로토콜](https://msdn.microsoft.com/library/aa480435.aspx)
- [ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
