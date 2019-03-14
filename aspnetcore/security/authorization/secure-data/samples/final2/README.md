---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049110"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a>보안 사용자 데이터 샘플을 빌드/실행 방법

* 암호 관리자 도구를 사용 하 여 암호를 설정 합니다.

  `dotnet user-secrets set SeedUserPW <pw>`

* 데이터베이스를 업데이트 합니다.

    `dotnet ef database update`

* 프로젝트에서 HTTPS를 사용 하도록 설정
