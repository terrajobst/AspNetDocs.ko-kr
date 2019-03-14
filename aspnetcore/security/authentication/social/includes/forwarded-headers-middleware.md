---
ms.openlocfilehash: d7ef9b11af8ee11e4ec84404f8cdeb0b89384a3c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57130452"
---
## <a name="forward-request-information-with-a-proxy-or-load-balancer"></a><span data-ttu-id="156c2-101">앞으로 프록시를 사용 하 여 정보를 요청 하거나 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="156c2-101">Forward request information with a proxy or load balancer</span></span>

<span data-ttu-id="156c2-102">앱 프록시 서버 또는 부하 분산 장치 뒤에 배포 하는 경우 원래 요청 정보 중 일부를 앱 요청 헤더에 전달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="156c2-102">If the app is deployed behind a proxy server or load balancer, some of the original request information might be forwarded to the app in request headers.</span></span> <span data-ttu-id="156c2-103">이 정보에는 일반적으로 보안 요청 체계가 포함 됩니다 (`https`), 호스트 및 클라이언트 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="156c2-103">This information usually includes the secure request scheme (`https`), host, and client IP address.</span></span> <span data-ttu-id="156c2-104">앱 검색 하 고 원래 요청 정보를 사용 하 여 이러한 요청 헤더를 자동으로 읽습니다 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="156c2-104">Apps don't automatically read these request headers to discover and use the original request information.</span></span>

<span data-ttu-id="156c2-105">스키마 외부 공급자를 사용 하 여 인증 흐름에 영향을 주는 링크 생성에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="156c2-105">The scheme is used in link generation that affects the authentication flow with external providers.</span></span> <span data-ttu-id="156c2-106">보안 체계 손실 (`https`) 안전 하지 않은 잘못 된 리디렉션 Url을 생성 하는 앱에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="156c2-106">Losing the secure scheme (`https`) results in the app generating incorrect insecure redirect URLs.</span></span>

<span data-ttu-id="156c2-107">전달 된 헤더 미들웨어를 사용 하 여 원래 요청 정보를 요청 처리에 대 한 앱을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="156c2-107">Use Forwarded Headers Middleware to make the original request information available to the app for request processing.</span></span>

<span data-ttu-id="156c2-108">자세한 내용은 <xref:host-and-deploy/proxy-load-balancer>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="156c2-108">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>
