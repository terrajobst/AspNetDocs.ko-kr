---
ms.openlocfilehash: 85fa9f8b18dc7dfb3e9d37703549dc5c28dc7a4a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062600"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="0c190-101">Movie 모델 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="0c190-101">Scaffold the Movie model</span></span>

* <span data-ttu-id="0c190-102">명령줄에서 다음을 실행합니다(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 프로젝트 디렉터리에서).</span><span class="sxs-lookup"><span data-stu-id="0c190-102">Run the following from the command line (in the project directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files):</span></span>

  ```console
  dotnet restore
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

<span data-ttu-id="0c190-103">오류가 표시될 경우:</span><span class="sxs-lookup"><span data-stu-id="0c190-103">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="0c190-104">앞의 오류는 잘못된 디렉터리에 있는 경우 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0c190-104">The preceeding error happens when you are in the wrong directory.</span></span> <span data-ttu-id="0c190-105">명령 셸에서 프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)를 연 다음, 이전 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0c190-105">Open a command shell to the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files), and then run the preceeding command.</span></span>

<span data-ttu-id="0c190-106">오류가 표시될 경우:</span><span class="sxs-lookup"><span data-stu-id="0c190-106">If you get the error:</span></span>
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

<span data-ttu-id="0c190-107">Visual Studio를 종료하고 명령을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0c190-107">Exit Visual Studio and run the command again.</span></span>
