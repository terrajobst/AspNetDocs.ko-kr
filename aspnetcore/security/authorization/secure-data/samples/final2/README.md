---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049110"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a><span data-ttu-id="5c275-101">보안 사용자 데이터 샘플을 빌드/실행 방법</span><span class="sxs-lookup"><span data-stu-id="5c275-101">How to build/run Secure user data sample</span></span>

* <span data-ttu-id="5c275-102">암호 관리자 도구를 사용 하 여 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c275-102">Set password with the Secret Manager tool:</span></span>

  `dotnet user-secrets set SeedUserPW <pw>`

* <span data-ttu-id="5c275-103">데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c275-103">Update the database:</span></span>

    `dotnet ef database update`

* <span data-ttu-id="5c275-104">프로젝트에서 HTTPS를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="5c275-104">Enable HTTPS in the project</span></span>
