---
uid: web-api/overview/security/working-with-ssl-in-web-api
title: Web API에서 SSL 사용 | Microsoft Docs
author: MikeWasson
description: Ssl 클라이언트 인증서 사용을 비롯 하 여 ASP.NET Web API에서 SSL을 사용 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/22/2019
ms.assetid: 97f6164f-59cf-45c0-b820-e4aa29b45396
msc.legacyurl: /web-api/overview/security/working-with-ssl-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 31589b3713b1f1a9b98d12906bfef81f8bf5e3f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484415"
---
# <a name="working-with-ssl-in-web-api"></a>Web API의 SSL 작업

[Mike Wasson](https://github.com/MikeWasson)

일반 HTTP를 통해 몇 가지 일반적인 인증 체계가 안전 하지 않습니다. 특히, 기본 인증 및 폼 인증은 암호화되지 않은 자격 증명을 보냅니다. 보안을 유지 하려면 이러한 인증 체계에서 SSL을 사용 *해야 합니다* . 또한 SSL 클라이언트 인증서를 사용 하 여 클라이언트를 인증할 수 있습니다.

## <a name="enabling-ssl-on-the-server"></a>서버에서 SSL 사용

IIS 7 이상에서 SSL을 설정 하려면 다음을 수행 합니다.

- 인증서를 만들거나 가져옵니다. 테스트를 위해 자체 서명 된 인증서를 만들 수 있습니다.
- HTTPS 바인딩을 추가 합니다.

자세한 내용은 [IIS 7에서 SSL을 설정 하는 방법](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)을 참조 하십시오.

로컬 테스트를 위해 Visual Studio의 IIS Express에서 SSL을 사용 하도록 설정할 수 있습니다. 속성 창에서 **SSL 사용** 을 **True**로 설정 합니다. **SSL URL**의 값을 확인 합니다. HTTPS 연결을 테스트 하려면이 URL을 사용 합니다.

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a>Web API 컨트롤러에서 SSL 적용

HTTPS와 HTTP 바인딩이 모두 있는 경우 클라이언트는 여전히 HTTP를 사용 하 여 사이트에 액세스할 수 있습니다. 일부 리소스는 HTTP를 통해 사용할 수 있으며, 다른 리소스에는 SSL이 필요 합니다. 이 경우 작업 필터를 사용 하 여 보호 된 리소스에 대해 SSL을 요구 합니다. 다음 코드에서는 SSL을 확인하는 Web API 인증 필터를 보여 줍니다.

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

SSL이 필요한 모든 Web API 작업에 이 필터를 추가합니다.

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a>SSL 클라이언트 인증서

SSL은 공개 키 인프라 인증서를 사용 하 여 인증을 제공 합니다. 서버에서 클라이언트에 대해 서버를 인증 하는 인증서를 제공 해야 합니다. 클라이언트에서 서버에 인증서를 제공 하는 것은 일반적이 지 않지만 클라이언트를 인증 하는 한 가지 옵션입니다. SSL로 클라이언트 인증서를 사용 하려면 서명 된 인증서를 사용자에 게 배포 하는 방법이 필요 합니다. 많은 응용 프로그램 종류의 경우이 작업은 좋은 사용자 환경이 아니지만 일부 환경 (예: enterprise)에서 가능 합니다.

| 장점 | 단점 |
| --- | --- |
| -인증서 자격 증명은 사용자 이름/암호 보다 강력 합니다. -SSL은 인증, 메시지 무결성 및 메시지 암호화를 사용 하 여 완전 한 보안 채널을 제공 합니다. | -PKI 인증서를 얻고 관리 해야 합니다. -클라이언트 플랫폼은 SSL 클라이언트 인증서를 지원 해야 합니다. |

클라이언트 인증서를 허용 하도록 IIS를 구성 하려면 IIS 관리자를 열고 다음 단계를 수행 합니다.

1. 트리 뷰에서 사이트 노드를 클릭 합니다.
2. 중간 창에서 **SSL 설정** 기능을 두 번 클릭 합니다.
3. **클라이언트 인증서**아래에서 다음 옵션 중 하나를 선택 합니다. 

    - **수락**: IIS는 클라이언트의 인증서를 수락 하지만이를 요구 하지는 않습니다.
    - **필요**: 클라이언트 인증서가 필요 합니다. 이 옵션을 사용 하려면 "SSL 필요"도 선택 해야 합니다.

Applicationhost.config 파일에서 다음 옵션을 설정할 수도 있습니다.

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

**SslNegotiateCert** 플래그는 iis가 클라이언트의 인증서를 수락 하지만이를 요구 하지 않습니다 (iis 관리자의 "수락" 옵션과 동일). 인증서를 요구 하려면 **SslRequireCert** 플래그를 설정 합니다. 테스트를 위해 로컬 applicationhost의 IIS Express에서 이러한 옵션을 설정할 수도 있습니다. "Documents\IISExpress\config"에 있는 구성 파일입니다.

### <a name="creating-a-client-certificate-for-testing"></a>테스트용 클라이언트 인증서 만들기

테스트를 위해 [makecert.exe](/windows/desktop/SecCrypto/makecert) 를 사용 하 여 클라이언트 인증서를 만들 수 있습니다. 먼저 테스트 루트 인증 기관을 만듭니다.

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

Makecert.exe는 개인 키에 대 한 암호를 입력 하 라는 메시지를 표시 합니다.

다음으로, 다음과 같이 테스트 서버의 "신뢰할 수 있는 루트 인증 기관" 저장소에 인증서를 추가 합니다.

1. MMC를 엽니다.
2. **파일**에서 **스냅인 추가/제거**를 선택 합니다.
3. **컴퓨터 계정**을 선택 합니다.
4. **로컬 컴퓨터** 를 선택 하 고 마법사를 완료 합니다.
5. 탐색 창에서 "신뢰할 수 있는 루트 인증 기관" 노드를 확장 합니다.
6. **작업** 메뉴에서 **모든 작업**을 가리킨 다음 **가져오기** 를 클릭 하 여 인증서 가져오기 마법사를 시작 합니다.
7. 인증서 파일 (TempCA .cer)로 이동 합니다.
8. **열기**를 클릭 하 고 **다음** 을 클릭 하 여 마법사를 완료 합니다. 암호를 다시 입력 하 라는 메시지가 표시 됩니다.

이제 첫 번째 인증서로 서명 된 클라이언트 인증서를 만듭니다.

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a>Web API에서 클라이언트 인증서 사용

서버 쪽에서 요청 메시지에 대해 [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) 를 호출 하 여 클라이언트 인증서를 가져올 수 있습니다. 클라이언트 인증서가 없는 경우 메서드는 null을 반환 합니다. 그렇지 않으면 **X509Certificate2** 인스턴스를 반환 합니다. 이 개체를 사용 하 여 발급자 및 주체와 같은 인증서에서 정보를 가져옵니다. 그런 다음 인증 및/또는 권한 부여에이 정보를 사용할 수 있습니다.

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
