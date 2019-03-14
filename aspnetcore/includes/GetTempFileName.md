---
ms.openlocfilehash: 2cd201e16cd491d0f468e8ef141b522f1694a257
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57165866"
---
**경고**: 다음 코드에서는 `GetTempFileName`을 throw 하는 `IOException` 이전 임시 파일을 삭제 하지 않고 65535 개 이상의 파일이 생성 되는 경우. 실제 앱은 임시 파일을 삭제하거나 `GetTempPath` 및 `GetRandomFileName`을 사용하여 임시 파일 이름을 만듭니다. 65535개의 파일 제한은 서버마다 있으므로 서버의 다른 앱은 65535개의 파일을 모두 사용할 수 있습니다. 
