---
uid: web-pages/overview/data/working-with-files
title: ASP.NET 웹 페이지 (Razor) 사이트에서 파일 작업 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 파일을 읽고, 쓰고, 추가 하 고, 삭제 하 고, 업로드 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: eee916e4-ba4c-439a-a24e-68df7d45a569
msc.legacyurl: /web-pages/overview/data/working-with-files
msc.type: authoredcontent
ms.openlocfilehash: 684c47a8a8480dc040e5144144577c94c35d39e5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521885"
---
# <a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 파일 작업

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor (ASP.NET 웹 페이지) 사이트에서 파일을 읽고, 쓰고, 추가 하 고, 삭제 하 고, 업로드 하는 방법을 설명 합니다.
> 
> > [!NOTE]
> > 이미지를 업로드 하 고 조작 하려면 (예: 대칭 이동 또는 크기 조정) [ASP.NET 웹 페이지 사이트에서 이미지 작업](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images)을 참조 하세요.
> 
> 
> **학습 내용:** 
> 
> - 텍스트 파일을 만들고이 파일에 데이터를 쓰는 방법
> - 기존 파일에 데이터를 추가 하는 방법
> - 파일을 읽고 파일에서 표시 하는 방법입니다.
> - 웹 사이트에서 파일을 삭제 하는 방법
> - 사용자가 한 파일 또는 여러 파일을 업로드할 수 있도록 하는 방법입니다.
> 
> 다음은이 문서에 도입 된 ASP.NET 프로그래밍 기능입니다.
> 
> - 파일을 관리 하는 방법을 제공 하는 `File` 개체입니다.
> - `FileUpload` 도우미입니다.
> - 경로와 파일 이름을 조작할 수 있는 메서드를 제공 하는 `Path` 개체입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 2
>   
> 
> 이 자습서는 WebMatrix 3 에서도 작동 합니다.

<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a>텍스트 파일을 만들고 여기에 데이터 쓰기

웹 사이트에서 데이터베이스를 사용 하는 것 외에도 파일을 사용할 수 있습니다. 예를 들어 텍스트 파일을 사이트에 대 한 데이터를 저장 하는 간단한 방법으로 사용할 수 있습니다. 데이터를 저장 하는 데 사용 되는 텍스트 파일을 *플랫 파일이*라고도 합니다. 텍스트 파일은 *.txt*, *.xml*또는 *.csv* (쉼표로 구분 된 값)와 같은 다양 한 형식일 수 있습니다.

텍스트 파일에 데이터를 저장 하려는 경우 `File.WriteAllText` 메서드를 사용 하 여 만들 파일과 해당 파일에 쓸 데이터를 지정할 수 있습니다. 이 절차에서는 3 개의 `input` 요소 (이름, 성 및 전자 메일 주소)와 **제출** 단추를 포함 하는 간단한 양식이 포함 된 페이지를 만듭니다. 사용자가 양식을 제출할 때 텍스트 파일에 사용자의 입력을 저장 합니다.

1. 이미 존재 하지 않는 경우 *App\_Data*라는 새 폴더를 만듭니다.
2. 웹 사이트의 루트에서 *UserData. cshtml*라는 새 파일을 만듭니다.
3. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    HTML 태그는 세 개의 텍스트 상자를 사용 하 여 폼을 만듭니다. 코드에서 `IsPost` 속성을 사용 하 여 처리를 시작 하기 전에 페이지가 전송 되었는지 여부를 확인 합니다.

    첫 번째 작업은 사용자 입력을 가져와 변수에 할당 하는 것입니다. 그런 다음 코드는 개별 변수의 값을 쉼표로 구분 된 하나의 문자열로 연결 합니다. 그러면 다른 변수에 저장 됩니다. 쉼표 구분 기호는 생성 하는 큰 문자열에 쉼표를 포함 하 고 있기 때문에 따옴표 (",")에 포함 된 문자열입니다. 함께 연결 하는 데이터의 끝에 `Environment.NewLine`를 추가 합니다. 줄 바꿈 (줄 바꿈 문자)이 추가 됩니다. 이 연결을 모두 사용 하 여 만드는 작업은 다음과 같은 문자열입니다.

    [!code-css[Main](working-with-files/samples/sample2.css)]

    (끝에 보이지 않는 줄 바꿈 포함)

    그런 다음 데이터를 저장할 파일의 위치와 이름을 포함 하는 변수 (`dataFile`)를 만듭니다. 위치를 설정 하려면 특별 한 처리가 필요 합니다. 웹 사이트에서는 웹 서버에서 파일의 *C:\Folder\File.txt* 와 같은 절대 경로에 대 한 코드를 참조 하는 것은 바람직하지 않습니다. 웹 사이트를 이동 하는 경우 절대 경로가 잘못 됩니다. 또한 호스트 된 사이트의 경우 (자체 컴퓨터와 반대 됨) 일반적으로 코드를 작성할 때 올바른 경로를 알 수 없습니다.

    그러나 경우에 따라 (예: 파일을 작성 하는 경우) 전체 경로가 필요 합니다. 이 솔루션은 `Server` 개체의 `MapPath` 메서드를 사용 하는 것입니다. 그러면 웹 사이트의 전체 경로가 반환 됩니다. 웹 사이트 루트의 경로를 가져오려면 `~` 연산자 (사이트의 가상 루트를 represen)를 사용 하 여 `MapPath`합니다. ( *~/App\_Data/* 와 같이 하위 폴더 이름을 전달 하 여 해당 하위 폴더에 대 한 경로를 가져올 수도 있습니다.) 그런 다음 전체 경로를 만들기 위해 메서드가 반환 하는 항목에 대 한 추가 정보를 연결할 수 있습니다. 이 예제에서는 파일 이름을 추가 합니다. [Razor 구문을 사용 하 여 ASP.NET 웹 페이지 프로그래밍](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)에 대 한 소개에서 파일 및 폴더 경로를 사용 하는 방법에 대해 자세히 알아볼 수 있습니다.

    이 파일은 *App\_Data* 폴더에 저장 됩니다. 이 폴더는 [ASP.NET 웹 페이지 사이트의 데이터베이스 작업 소개](https://go.microsoft.com/fwlink/?LinkId=195209)에 설명 된 대로 데이터 파일을 저장 하는 데 사용 되는 ASP.NET의 특수 폴더입니다.

    `File` 개체의 `WriteAllText` 메서드는 파일에 데이터를 씁니다. 이 메서드는 두 개의 매개 변수, 즉 쓸 파일의 이름 (경로 포함) 및 쓸 실제 데이터를 사용 합니다. 첫 번째 매개 변수의 이름에는 접두사로 `@` 문자가 있습니다. 이는 축 자 문자열 리터럴을 제공 한다는 것을 ASP.NET 하 고, "/"와 같은 문자는 특별 한 방식으로 해석 되지 않아야 함을 나타냅니다. 자세한 내용은 [Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)를 참조 하세요.

    > [!NOTE]
    > 코드에서 응용 프로그램 *\_Data* 폴더에 파일을 저장 하려면 해당 폴더에 대 한 읽기/쓰기 권한이 필요 합니다. 개발 컴퓨터에는 일반적으로 문제가 되지 않습니다. 그러나 호스팅 공급자의 웹 서버에 사이트를 게시 하는 경우 해당 권한을 명시적으로 설정 해야 할 수 있습니다. 호스팅 공급자의 서버에서이 코드를 실행 하 고 오류를 수신 하는 경우 호스팅 공급자에 게 문의 하 여 이러한 권한을 설정 하는 방법을 알아보세요.

- 브라우저에서 페이지를 실행 합니다. 

    ![](working-with-files/_static/image1.jpg)
- 필드에 값을 입력 한 다음 **제출**을 클릭 합니다.
- 브라우저를 닫습니다.
- 프로젝트로 돌아가서 뷰를 새로 고칩니다.
- *Data .txt* 파일을 엽니다. 양식에서 제출한 데이터는 파일에 있습니다. 

    ![[이미지]](working-with-files/_static/image2.jpg)
- *Data .txt* 파일을 닫습니다.

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a>기존 파일에 데이터 추가

이전 예제에서는 `WriteAllText` 사용 하 여 데이터의 한 부분에만 있는 텍스트 파일을 만듭니다. 메서드를 다시 호출 하 고 동일한 파일 이름을 전달 하면 기존 파일을 완전히 덮어씁니다. 그러나 파일을 만든 후에는 파일의 끝에 새 데이터를 추가 하는 경우가 많습니다. `File` 개체의 `AppendAllText` 메서드를 사용 하 여이 작업을 수행할 수 있습니다.

1. 웹 사이트에서 *UserData* 파일의 복사본을 만들고 복사본의 이름을 *UserDataMultiple*로 지정 합니다.
2. 다음 코드 블록을 사용 하 여 여는 `<!DOCTYPE html>` 태그 앞에 코드 블록을 바꿉니다. 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    이 코드에는 이전 예제에서 변경 된 내용이 하나 있습니다. `WriteAllText`를 사용 하는 대신 `the AppendAllText` 메서드를 사용 합니다. `AppendAllText`는 파일의 끝에 데이터를 추가 하는 것을 제외 하 고 메서드는 유사 합니다. `WriteAllText`와 마찬가지로 `AppendAllText` 파일이 없는 경우 파일을 만듭니다.
3. 브라우저에서 페이지를 실행 합니다.
4. 필드에 대 한 값을 입력 한 다음 **제출**을 클릭 합니다.
5. 데이터를 더 추가 하 고 양식을 다시 제출 합니다.
6. 프로젝트로 돌아가서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새로 고침**을 클릭 합니다.
7. *Data .txt* 파일을 엽니다. 이제 방금 입력 한 새 데이터를 포함 합니다. 

    ![[이미지]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a>파일에서 데이터 읽기 및 표시

텍스트 파일에 데이터를 쓸 필요가 없는 경우에도 데이터를 한 곳에서 읽어야 할 수도 있습니다. 이렇게 하려면 `File` 개체를 다시 사용할 수 있습니다. `File` 개체를 사용 하 여 각 줄을 개별적으로 읽거나 (줄 바꿈으로 구분) 개별 항목을 구분 하는 방법에 관계 없이 읽을 수 있습니다.

이 절차에서는 이전 예제에서 만든 데이터를 읽고 표시 하는 방법을 보여 줍니다.

1. 웹 사이트의 루트에서 *Displaydata. cshtml*라는 새 파일을 만듭니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    이 메서드 호출을 사용 하 여 앞의 예제에서 만든 파일을 `userData`라는 변수로 읽어 먼저 코드를 실행 합니다.

    [!code-css[Main](working-with-files/samples/sample5.css)]

    이 작업을 수행 하는 코드는 `if` 문 내에 있습니다. 파일을 읽으려면 먼저 `File.Exists` 메서드를 사용 하 여 파일을 사용할 수 있는지 여부를 확인 하는 것이 좋습니다. 또한이 코드는 파일이 비어 있는지 여부를 확인 합니다.

    페이지 본문에는 서로 중첩 된 두 개의 `foreach` 루프가 포함 되어 있습니다. 외부 `foreach` 루프는 데이터 파일에서 한 번에 한 줄을 가져옵니다. 이 경우 줄은 파일 &#8212; 의 줄 바꿈으로 정의 됩니다. 즉, 각 데이터 항목은 별도의 줄에 있습니다. 외부 루프는 정렬 된 목록 (`<ol>` 요소) 안에 새 항목 (`<li>` 요소)을 만듭니다.

    내부 루프는 쉼표를 구분 기호로 사용 하 여 각 데이터 줄을 항목 (필드)으로 분할 합니다. 이전 예제를 기반으로 하 여 각 줄에는 이름, 성 및 &#8212; 전자 메일 주소 라는 세 개의 필드가 쉼표로 구분 되어 포함 되어 있음을 의미 합니다. 또한 내부 루프는 `<ul>` 목록을 만들고 데이터 줄의 각 필드에 대해 하나의 목록 항목을 표시 합니다.

    이 코드에서는 두 가지 데이터 형식, 배열 및 `char` 데이터 형식을 사용 하는 방법을 보여 줍니다. 배열은 `File.ReadAllLines` 메서드가 데이터를 배열로 반환 하기 때문에 필요 합니다. `char` 데이터 형식은 `Split` 메서드가 각 요소가 `char`형식인 `array`을 반환 하기 때문에 필요 합니다. 배열에 대 한 자세한 내용은 [Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects)를 참조 하세요.
3. 브라우저에서 페이지를 실행 합니다. 이전 예제에서 입력 한 데이터가 표시 됩니다. 

    ![[이미지]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> **Microsoft Excel 쉼표로 분리 된 파일의 데이터 표시**
> 
> Microsoft Excel을 사용 하 여 스프레드시트에 포함 된 데이터를 쉼표로 구분 된 파일 ( *.csv* 파일)로 저장할 수 있습니다. 이렇게 하면 파일이 Excel 형식이 아닌 일반 텍스트로 저장 됩니다. 스프레드시트의 각 행은 텍스트 파일에서 줄 바꿈으로 구분 되며, 각 데이터 항목은 쉼표로 구분 됩니다. 이전 예제에 표시 된 코드를 사용 하 여 코드에서 데이터 파일의 이름을 변경 하는 것 만으로 Excel 쉼표로 분리 된 파일을 읽을 수 있습니다.

<a id="Deleting_Files"></a>
## <a name="deleting-files"></a>파일 삭제

웹 사이트에서 파일을 삭제 하려면 `File.Delete` 방법을 사용 하면 됩니다. 이 절차에서는 사용자가 파일 이름을 알고 있는 경우 *이미지 폴더에서 이미지 (* *.jpg* 파일)를 삭제할 수 있도록 하는 방법을 보여 줍니다.

> [!NOTE] 
> 
> **중요** 프로덕션 웹 사이트에서는 일반적으로 데이터를 변경할 수 있는 사용자를 제한 합니다. 멤버 자격을 설정 하는 방법과 사용자에 게 사이트에서 작업을 수행할 수 있는 권한을 부여 하는 방법에 대 한 자세한 내용은 [ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격 추가](https://go.microsoft.com/fwlink/?LinkId=202904)를 참조 하세요.

1. 웹 사이트에서 이름이 *images*인 하위 폴더를 만듭니다.
2. 하나 이상의 *.jpg* 파일을 *images* 폴더에 복사 합니다.
3. 웹 사이트의 루트에서 *Filedelete. cshtml*라는 새 파일을 만듭니다.
4. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    이 페이지에는 사용자가 이미지 파일의 이름을 입력할 수 있는 양식이 포함 되어 있습니다. .Jpg 파일 이름 확장명을 입력 하지 않습니다 *.* 이와 같이 파일 이름을 제한 하면 사용자가 사이트에서 임의의 파일을 삭제할 수 없습니다.

    이 코드는 사용자가 입력 한 파일 이름을 읽은 다음 전체 경로를 생성 합니다. 경로를 만들기 위해 코드는 현재 웹 사이트 경로 (`Server.MapPath` 메서드에서 반환), *이미지* 폴더 이름, 사용자가 제공한 이름 및 ".jpg"를 리터럴 문자열로 사용 합니다.

    이 파일을 삭제 하기 위해 코드는 `File.Delete` 메서드를 호출 하 여 방금 만든 전체 경로를 전달 합니다. 태그의 끝에서 코드는 파일이 삭제 되었다는 확인 메시지를 표시 합니다.
5. 브라우저에서 페이지를 실행 합니다. 

    ![[이미지]](working-with-files/_static/image5.jpg)
6. 삭제할 파일의 이름을 입력 한 다음 **제출**을 클릭 합니다. 파일이 삭제 된 경우 페이지의 맨 아래에 파일 이름이 표시 됩니다.

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a>사용자가 파일 업로드 허용

사용자는 `FileUpload` 도우미를 사용 하 여 웹 사이트에 파일을 업로드할 수 있습니다. 다음 절차에서는 사용자가 단일 파일을 업로드할 수 있도록 하는 방법을 보여 줍니다.

1. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)의 설명에 따라 웹 사이트에 ASP.NET 웹 도우미 라이브러리를 추가 합니다 (이전에 추가 하지 않은 경우).
2. *App\_Data* 폴더에서 새 폴더를 만들고 이름을 *UploadedFiles*로 다시 만듭니다.
3. 루트에서 *FileUpload*라는 새 파일을 만듭니다.
4. 페이지의 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    페이지의 본문 부분은 `FileUpload` 도우미를 사용 하 여 친숙 한 업로드 상자와 단추를 만듭니다.

    ![[이미지]](working-with-files/_static/image6.jpg)

    `FileUpload` 도우미에 대해 설정한 속성은 파일에 대 한 단일 상자를 선택 하 고 제출 단추를 클릭 하 여 **업로드**를 읽도록 지정 합니다. (이 문서의 뒷부분에서 더 많은 상자를 추가 합니다.)

    사용자가 **업로드**를 클릭 하면 페이지 맨 위에 있는 코드에서 파일을 가져와 저장 합니다. 양식 필드에서 값을 가져오는 데 일반적으로 사용 하는 `Request` 개체에는 업로드 된 파일 (또는 파일)을 포함 하는 `Files` 배열도 있습니다. 배열의 &#8212; 특정 위치에서 개별 파일을 가져올 수 있습니다. 예를 들어 첫 번째 업로드 된 파일을 가져오기 위해 `Request.Files[0]`를 가져오고 두 번째 파일을 가져오고 `Request.Files[1]`를 가져올 수 있습니다. 프로그래밍에서 계산은 일반적으로 0부터 시작 합니다.

    업로드 된 파일을 페치할 때 해당 파일을 조작할 수 있도록 변수에 저장 합니다 (여기 `uploadedFile`). 업로드 된 파일의 이름을 확인 하려면 해당 `FileName` 속성을 가져옵니다. 그러나 사용자가 파일을 업로드 하면 전체 경로를 포함 하는 사용자의 원래 이름이 `FileName`에 포함 됩니다. 다음과 같이 표시 될 수 있습니다.

    *C:\Users\Public\Sample.txt*

    그러나 서버에 대 한 것이 아니라 사용자 컴퓨터의 경로 이기 때문에 모든 경로 정보를 원하지는 않습니다. 실제 파일 이름 (*샘플 .txt*)만 필요 합니다. 다음과 같이 `Path.GetFileName` 메서드를 사용 하 여 경로에서 파일만 제거할 수 있습니다.

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    `Path` 개체는 경로를 제거 하 고 경로를 결합 하는 데 사용할 수 있는 다음과 같은 여러 메서드가 있는 유틸리티입니다.

    업로드 된 파일의 이름을 지정한 후에는 업로드 된 파일을 웹 사이트에 저장 하려는 새 경로를 만들 수 있습니다. 이 경우 `Server.MapPath`, 폴더 이름 (*앱\_데이터/UploadedFiles*) 및 새로 제거 된 파일 이름을 결합 하 여 새 경로를 만듭니다. 그런 다음 업로드 된 파일의 `SaveAs` 메서드를 호출 하 여 실제로 파일을 저장할 수 있습니다.
5. 브라우저에서 페이지를 실행 합니다. 

    ![[이미지]](working-with-files/_static/image7.jpg)
6. **찾아보기** 를 클릭 한 다음 업로드할 파일을 선택 합니다. 

    ![[이미지]](working-with-files/_static/image8.jpg)

    **찾아보기** 단추 옆의 텍스트 상자에는 경로와 파일 위치가 포함 됩니다.

    ![[이미지]](working-with-files/_static/image9.jpg)
7. **업로드**를 클릭합니다.
8. 웹 사이트에서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새로 고침**을 클릭 합니다.
9. *UploadedFiles* 폴더를 엽니다. 업로드 한 파일은 폴더에 있습니다. 

    ![[이미지]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a>사용자가 여러 파일 업로드 허용

이전 예제에서는 사용자가 파일 하나를 업로드할 수 있습니다. 하지만 `FileUpload` 도우미를 사용 하 여 한 번에 두 개 이상의 파일을 업로드할 수 있습니다. 이는 한 번에 한 파일을 업로드 하는 것이 지루한 사진 업로드와 같은 시나리오에 유용 합니다. [ASP.NET 웹 페이지 사이트에서 이미지를 사용 하 여 작업 하는](https://go.microsoft.com/fwlink/?LinkId=202897)사진을 업로드 하는 방법에 대해 알아볼 수 있습니다. 이 예제에서는 동일한 기술을 사용 하 여 둘 이상의를 업로드할 수 있지만 사용자가 한 번에 2를 업로드할 수 있게 하는 방법을 보여 줍니다.

1. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).
2. *FileUploadMultiple*라는 새 페이지를 만듭니다.
3. 페이지의 기존 콘텐츠를 다음으로 바꿉니다.  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    이 예제에서는 사용자가 기본적으로 두 파일을 업로드할 수 있도록 페이지 본문의 `FileUpload` 도우미가 구성 되어 있습니다. `allowMoreFilesToBeAdded`이 `true`으로 설정 되어 있으므로 도우미가 사용자가 더 많은 업로드 상자를 추가할 수 있는 링크를 렌더링 합니다.

    ![[이미지]](working-with-files/_static/image11.jpg)

    사용자가 업로드 하는 파일을 처리 하기 위해 코드는 이전 예제 &#8212; 에서 사용한 것과 동일한 기본 기술을 사용 하 여 `Request.Files` 파일을 가져온 다음 저장 합니다. (올바른 파일 이름 및 경로를 가져오기 위해 수행 해야 하는 다양 한 작업 포함) 이 시간을 혁신 하는 것은 사용자가 여러 파일을 업로드할 수 있고 많은 것을 알 수 없기 때문입니다. `Request.Files.Count`를 찾을 수 있습니다.

    이 번호를 사용 하면 `Request.Files`를 반복 하 고 각 파일을 차례로 가져와 저장할 수 있습니다. 컬렉션을 통해 알려진 횟수를 반복 하려는 경우 다음과 같이 `for` 루프를 사용할 수 있습니다.

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    `i` 변수는 0에서 설정 하는 상한에 해당 하는 임시 카운터 일 뿐입니다. 이 경우 상한 값은 파일 수입니다. 하지만 카운터는 ASP.NET에서 계산 시나리오에 일반적으로 발생 하는 것 처럼 0에서 시작 되므로 상한 값은 실제로 파일 수보다 하나 미만입니다. 3 개의 파일을 업로드 하는 경우 수는 0에서 2 사이입니다.

    `uploadedCount` 변수는 성공적으로 업로드 되 고 저장 된 모든 파일의 합계를 가집니다. 이 코드는 예상 되는 파일을 업로드 하지 못할 수 있는 가능성을 계정으로 합니다.
4. 브라우저에서 페이지를 실행 합니다. 브라우저에 페이지와 두 개의 업로드 상자가 표시 됩니다.
5. 업로드할 파일 두 개를 선택 합니다.
6. **다른 파일 추가**를 클릭 합니다. 이 페이지에는 새 업로드 상자가 표시 됩니다. 

    ![[이미지]](working-with-files/_static/image12.jpg)
7. **업로드**를 클릭합니다.
8. 웹 사이트에서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새로 고침**을 클릭 합니다.
9. *UploadedFiles* 폴더를 열어서 성공적으로 업로드 된 파일을 확인 합니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지 사이트에서 이미지 작업](https://go.microsoft.com/fwlink/?LinkId=202897)

[CSV 파일로 내보내기](https://msdn.microsoft.com/library/ms155919.aspx)
