---
ms.openlocfilehash: 939231583679d469d01724cc1a405bd45e46d2c5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57175903"
---
```console
npm run release
```

<span data-ttu-id="6ff67-101">이 명령은 앱을 실행할 때 제공되는 클라이언트 쪽 자산을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff67-101">This command yields the client-side assets to be served when running the app.</span></span> <span data-ttu-id="6ff67-102">자산은 *wwwroot* 폴더에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ff67-102">The assets are placed in the *wwwroot* folder.</span></span>

<span data-ttu-id="6ff67-103">Webpack은 다음 작업을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff67-103">Webpack completed the following tasks:</span></span>

* <span data-ttu-id="6ff67-104">*wwwroot* 디렉터리의 콘텐츠를 제거했습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff67-104">Purged the contents of the *wwwroot* directory.</span></span>
* <span data-ttu-id="6ff67-105">TypeScript를 JavaScript로 변환했습니다(*트랜스파일*&mdash;이라는 프로세스).</span><span class="sxs-lookup"><span data-stu-id="6ff67-105">Converted the TypeScript to JavaScript&mdash;a process known as *transpilation*.</span></span>
* <span data-ttu-id="6ff67-106">파일 크기를 줄이기 위해 생성된 JavaScript를 변환했습니다(*축소*&mdash;라는 프로세스).</span><span class="sxs-lookup"><span data-stu-id="6ff67-106">Mangled the generated JavaScript to reduce file size&mdash;a process known as *minification*.</span></span>
* <span data-ttu-id="6ff67-107">*src*에서 *wwwroot* 디렉터리로 처리된 JavaScript, CSS 및 HTML 파일을 복사했습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff67-107">Copied the processed JavaScript, CSS, and HTML files from *src* to the *wwwroot* directory.</span></span>
* <span data-ttu-id="6ff67-108">다음 요소를 *wwwroot/index.html* 파일에 삽입했습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff67-108">Injected the following elements into the *wwwroot/index.html* file:</span></span>
    * <span data-ttu-id="6ff67-109">*wwwroot/main.\<hash\>.css* 파일을 참조하는 `<link>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff67-109">A `<link>` tag, referencing the *wwwroot/main.\<hash\>.css* file.</span></span> <span data-ttu-id="6ff67-110">이 태그는 `</head>` 태그를 닫기 전에 즉시 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff67-110">This tag is placed immediately before the closing `</head>` tag.</span></span>
    * <span data-ttu-id="6ff67-111">축소된 *wwwroot/main.\<hash\>.js* 파일을 참조하는 `<script>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff67-111">A `<script>` tag, referencing the minified *wwwroot/main.\<hash\>.js* file.</span></span> <span data-ttu-id="6ff67-112">이 태그는 `</body>` 태그를 닫기 전에 즉시 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff67-112">This tag is placed immediately before the closing `</body>` tag.</span></span>
