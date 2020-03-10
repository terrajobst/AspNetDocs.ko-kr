# <a name="contribute-to-the-aspnet-documentation"></a>ASP.NET 설명서에 참가

이 문서에서는 [ASP.NET 문서 사이트](https://docs.microsoft.com/aspnet/)에서 호스팅되는 문서 및 코드 샘플에 참여하는 프로세스를 설명합니다. 오타 수정 및 새 문서 작성을 통한 참여를 환영합니다.

## <a name="how-to-make-a-simple-correction-or-suggestion"></a>간단한 수정 또는 제안을 수행하는 방법

문서는 리포지토리에 Markdown 파일로 저장됩니다. Markdown 파일의 내용에 대한 간단한 변경 작업은 브라우저 창의 오른쪽 상단 모서리에서 **편집** 링크를 선택하여 수행할 수 있습니다. (좁은 브라우저 창에서 **옵션** 모음을 확장 하 여 **편집** 링크를 표시 합니다.) 지침에 따라 끌어오기 요청 (PR)을 만듭니다. Microsoft에서 PR을 살펴보고 변경 사항을 수락하거나 제안합니다.

## <a name="how-to-make-a-more-complex-submission"></a>더 복잡한 제출을 수행하는 방법

[Git 및 GitHub.com](https://guides.github.com/activities/hello-world/)의 기본적인 내용을 이해하고 있어야 합니다.

* 기존 문서 변경 또는 새 문서 생성처럼 원하는 작업을 설명하는 [문제](https://github.com/dotnet/AspNetDocs/issues/new)를 엽니다. Microsoft에서는 새 항목 제안의 개요를 요청하는 경우가 많습니다. 많은 시간을 투자하기 전에 팀의 승인을 기다리세요.
* [Dotnet/AspNetDocs](https://github.com/dotnet/AspNetDocs/) 리포지토리를 포크 하 고 변경에 대 한 분기를 만듭니다.
* 마스터에게 변경 내용이 포함된 PR을 제출합니다.
* PR에 'cla-required' 레이블이 할당되어 있으면 [CLA(기여 사용권 계약)를 작성](https://cla.dotnetfoundation.org/)하세요.
* PR 피드백에 응답합니다.

예를 들어 이 프로세스를 통해 새 문서가 게시되는 경우 .NET Docs 리포지토리에서 [문제 &num;67](https://github.com/dotnet/docs/issues/67) 및 [끌어오기 요청 &num;798](https://github.com/dotnet/docs/pull/798)을 참조하세요. 새 문서는 [코드 문서화](https://docs.microsoft.com/dotnet/articles/csharp/codedoc)입니다.

## <a name="docs-authoring-pack-extension-in-visual-studio-code"></a>Visual Studio Code에서 Docs Authoring Pack 확장

Visual Studio Code를 사용하여 ASP.NET 문서에 참여하는 경우 [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) 확장을 설치하여 생산성을 높일 수 있습니다. 이 확장은 Markdown 린팅, 코드 맞춤법 검사 및 문서 서식 파일에 도움이 되는 다양한 도구를 제공합니다.

## <a name="markdown-syntax"></a>Markdown 구문

문서는 [GitHub-flavored Markdown(GFM)](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html)의 상위 집합인 [DocFx-flavored Markdown](https://guides.github.com/features/mastering-markdown/)으로 작성됩니다. ASP.NET 설명서에서 일반적으로 사용 되는 UI 기능에 대 한 DFM 구문 예제는 .NET Docs 리포지토리 스타일 가이드에서 [Metadata And Markdown Template](https://github.com/dotnet/docs/blob/master/styleguide/template.md) 을 참조 하세요.

## <a name="folder-structure-conventions"></a>폴더 구조 규칙

각 Markdown 파일에는 이미지 폴더와 샘플 코드 폴더가 있을 수 있습니다. 아티클이 [signalr/overview/advanced/](https://github.com/dotnet/AspNetDocs/blob/master/aspnet/signalr/overview/advanced/dependency-injection.md) [\_signalr](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/_static) 인 경우 이미지는 고정 되어 있고 샘플 응용 프로그램 프로젝트 파일은 [signalr/개요/고급/종속성-삽입/샘플](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/samples)에서 사용할 수 있습니다. *Signalr/개요/고급/종속성 주입* 파일의 이미지는 다음 Markdown에 의해 렌더링 됩니다.

```md
![description of image for alt attribute](dependency-injection/_static/image1.png)
```

모든 이미지에는 [대체 텍스트](https://wikipedia.org/wiki/Alt_attribute)가 있어야 합니다. 대체 텍스트를 지정하는 방법에 대한 조언을 보려면 [WebAIM: 대체 텍스트](https://webaim.org/techniques/alttext/)와 같은 온라인 리소스를 참조하세요.

Markdown 파일 이름 및 이미지 파일 이름에는 소문자를 사용하세요.

## <a name="internal-links"></a>내부 링크

내부 링크는 xref 링크가 있는 대상 문서의 `uid`를 사용해야 합니다(링크 텍스트는 연결된 콘텐츠의 제목으로 설정됨).

```md
<xref:uid_of_the_topic>
```

문서의 제목이 링크 텍스트에 적합하지 않은 경우(예: 문장의 단어나 구문이 링크 텍스트인 경우) 다음을 사용하여 xref 링크 및 링크 텍스트를 지정하세요.

```md
[link text](xref:uid_of_the_topic)
```

자세한 내용은 [DocFX 교차 참조](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#cross-reference)를 참조하세요.

## <a name="images-and-screenshots"></a>이미지 및 스크린샷

다음을 제외하고 문서와 함께 이미지를 포함하지 마세요.

* 기본 온보딩(초급) 자습서에서
* 명확성을 위해 이미지가 필요한 경우

이러한 제한 사항은 리포지토리의 크기를 줄입니다.

선택적 단계로, 문서에서 사용되는 이미지 및 스크린샷이 압축되었는지 확인하세요. 그러면 파일 크기 및 페이지 로드 성능이 개선됩니다. 주요 도구로는 TinyPNG([TinyPNG 웹 사이트](https://tinypng.com/) 또는 [TinyPNG API](https://tinypng.com/developers) 사용) 또는 [Image Optimizer](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ImageOptimizer) Visual Studio 확장이 있습니다.

## <a name="code-snippets"></a>코드 조각

문서에는 요점을 설명하는 코드 조각이 포함된 경우가 많습니다. DFM을 사용하여 Markdown 파일에 코드를 복사하거나 별도의 코드 파일을 참조할 수 있습니다. 코드에서 오류 가능성을 최소화하기 위해 가능하면 별도의 코드 파일을 사용하는 것이 좋습니다. 코드 파일은 앞에서 샘플 프로젝트에 대해 설명한 폴더 구조를 사용 하 여 리포지토리에 저장 됩니다.

다음 예에서는 [configuration/index.md](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#code-snippet) 파일에서 사용할 *DFM 코드 조각 구문*을 설명합니다.

전체 코드 파일을 코드 조각으로 렌더링하려면:

```md
[!code-csharp[](configuration/index/sample/Program.cs)]
```

줄 번호를 사용하여 파일의 일부를 코드 조각으로 렌더링하려면

```md
[!code-csharp[](configuration/index/sample/Program.cs?range=1-10,20,30,40-50]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=1-10,20,30,40-50]
```

C# 코드 조각의 경우 [C# 지역](https://docs.microsoft.com/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region)을 참조하세요. 가능할 때마다 줄 번호보다는 지역을 사용하세요. 코드 파일의 줄 번호는 변경되거나, Markdown의 줄 번호 참조와 비동기화될 가능성이 높습니다. C# 지역은 중첩할 수 있습니다. 외부 지역을 참조할 경우 내부 `#region` 및 `#endregion` 지시문은 코드 조각에 렌더링되지 않습니다.

"snippet_Example"이라는 C# 지역을 렌더링하려면

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example)]
```

렌더링된 코드 조각에서 선택된 줄을 강조 표시하려면(일반적으로 노란색 배경으로 렌더링됨):

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example&highlight=1-3,10,20-25)]
[!code-csharp[](configuration/index/sample/Program.cs?range=10-20&highlight=1-3]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=10-20&highlight=1-3]
[!code-javascript[](configuration/index/sample/UsingOptionsSample.csproj?range=10-20&highlight=1-3]
```

## <a name="test-changes-with-docfx"></a>DocFX로 변경 내용 테스트

로컬에서 호스팅되는 사이트 버전을 만드는 [DocFX 명령줄 도구](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool)로 변경 내용을 테스트하세요. DocFX는 docs.microsoft.com용으로 생성된 스타일 및 사이트 확장을 렌더링하지 않습니다.

DocFX 요구 사항:

* Windows에 설치된 .NET Framework
* Linux 또는 macOS용 Mono.

### <a name="windows-instructions"></a>Windows 지침

* *DocFX 릴리스*에서 [docfx.zip](https://github.com/dotnet/docfx/releases)을 다운로드하고 압축을 풉니다.
* PATH에 DocFX를 추가합니다.
* 명령 셸에서 *docfx. json* 파일이 포함 된 *aspnet* 폴더로 이동 하 고 다음 명령을 실행 합니다.

  ```console
  docfx --serve
  ```

* 브라우저에서 `http://localhost:8080/group1-dest/`로 이동합니다.

### <a name="mono-instructions"></a>Mono 지침

* Homebrew를 통해 Mono 설치:

  ```console
  brew install mono
  ```

* [최신 버전의 DocFX](https://github.com/dotnet/docfx/releases)를 다운로드합니다.
* *$HOME/bin/docfx*에 보관 파일을 추출합니다.
* bash 셸에서 **docfx**의 별칭 쌍을 만듭니다. 첫 번째 별칭은 문서를 작성하는 데 사용됩니다. 두 번째 별칭은 문서를 작성하고 서비스를 제공하는 데 사용됩니다.

  ```console
  alias docfx='mono $HOME/bin/docfx/docfx.exe'
  alias docfx-serve='mono $HOME/bin/docfx/docfx.exe --serve'
  ```

* 명령 셸에서 *docfx. json* 파일이 포함 된 *aspnet* 폴더로 이동 하 고 다음 명령을 실행 하 여 해당 별칭을 통해 문서를 빌드하고 제공 합니다.

  ```console
  docfx-serve
  ```

* 브라우저에서 `http://localhost:8080/group1-dest/`로 이동합니다.

## <a name="voice-and-tone"></a>어투 및 어조

가장 폭넓은 잠재 고객이 쉽게 이해할 수 있는 설명서를 작성하는 것이 목표입니다. 이에 따라 Microsoft는 기여자가 지켜주었으면 하는 문장체에 대한 지침을 정했습니다. 자세한 내용은 .NET 리포지토리의 [음성 및 톤 지침](https://github.com/dotnet/docs/blob/master/styleguide/voice-tone.md) 을 참조 하세요.

## <a name="microsoft-writing-style-guide"></a>Microsoft 문장체 가이드

[Microsoft 문장체 가이드](https://docs.microsoft.com/style-guide/welcome/)에서는 ASP.NET Core 설명서를 포함한 모든 형태의 기술 설명서에 대한 문장체 및 용어 지침을 제공합니다.

## <a name="redirects"></a>리디렉션

문서를 삭제하거나, 파일 이름을 변경하거나, 다른 폴더로 이동할 경우 해당 문서를 책갈피에 추가한 사람이 *404 찾을 수 없음* 오류를 받지 않도록 리디렉션을 만드세요. [마스터 리디렉션 파일](https://github.com/dotnet/AspNetDocs/blob/master/.openpublishing.redirection.json)에 리디렉션을 추가합니다.
