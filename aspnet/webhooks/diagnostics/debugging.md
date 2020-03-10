---
uid: webhooks/diagnostics/debugging
title: ASP.NET 웹 후크 디버깅 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크를 디버그 하는 방법입니다.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520601"
---
# <a name="aspnet-webhooks-debugging"></a>ASP.NET 웹 후크 디버깅  

## <a name="debugging-in-azure"></a>Azure에서 디버깅

Azure에서 실행 하는 동안 웹 응용 프로그램을 디버그 하려면 [Visual Studio를 사용 하 여 Azure App Service에서 웹 앱 문제 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)자습서를 참조 하세요.

## <a name="debugging-with-source-and-symbols"></a>소스 및 기호를 사용 하 여 디버깅

사용자 고유의 코드를 디버깅 하는 것 외에도 Microsoft ASP.NET 웹 후크에 직접 디버그할 수 있으며 실제로 모든 .NET에서 디버그할 수 있습니다. 이는 로컬에서 디버그 하는지 원격으로 디버그 하는지 여부에 관계 없이 작동 합니다. 먼저 **디버그** 로 이동 하 여 **옵션 및 설정**으로 이동 하 여 소스 및 기호를 찾도록 Visual Studio를 구성 합니다. 다음과 같이 옵션을 설정 합니다.

![옵션 및 설정](_static/SourceSymbols.png)

그런 다음 [symbolsource.org](http://symbolsource.org) 에 대 한 링크를 추가 하 여 소스 및 기호를 다운로드 합니다. 위의 메뉴에 있는 **기호** 탭으로 이동 하 여 다음을 기호 위치로 추가 합니다.

```
http://srv.symbolsource.org/pdb/Public
```

또한 캐시 디렉터리에 짧은 이름을 사용 해야 합니다. 그렇지 않으면 파일 이름이 너무 길어서 기호가 로드 되지 않을 수 있습니다. 샘플 경로는 다음과 같습니다.

```
C:\SymCache
```

설정은 다음과 유사 하 게 표시 됩니다.

![옵션 기호 파일 위치 예](_static/SymSource.png)
