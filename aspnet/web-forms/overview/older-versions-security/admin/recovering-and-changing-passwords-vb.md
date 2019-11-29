---
uid: web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-vb
title: 암호 복구 및 변경 (VB) | Microsoft Docs
author: rick-anderson
description: ASP.NET에는 암호 복구 및 변경을 지원 하기 위한 두 개의 웹 컨트롤이 포함 되어 있습니다. PasswordRecovery 제어를 통해 방문자는 분실 한 pa를 복구할 수 있습니다.
ms.author: riande
ms.date: 04/01/2008
ms.assetid: f9adcb5d-6d70-4885-a3bf-ed95efb4da1a
msc.legacyurl: /web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ed1df9455af94a86ce59ecc06c55846a4880596
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618982"
---
# <a name="recovering-and-changing-passwords-vb"></a>암호 복구 및 변경(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.13.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial13_ChangingPasswords_vb.pdf)

> ASP.NET에는 암호 복구 및 변경을 지원 하기 위한 두 개의 웹 컨트롤이 포함 되어 있습니다. PasswordRecovery 컨트롤을 사용 하면 방문자가 분실 한 암호를 복구할 수 있습니다. ChangePassword 컨트롤을 사용 하면 사용자가 암호를 업데이트할 수 있습니다. 이 자습서 시리즈 전체에서 확인 한 다른 로그인 관련 웹 컨트롤과 마찬가지로 PasswordRecovery 및 ChangePassword 컨트롤은 백그라운드에서 사용자의 암호를 다시 설정 하거나 수정 하기 위해 멤버 자격 프레임 워크와 함께 작동 합니다.

## <a name="introduction"></a>소개

내 은행, 유틸리티 회사, 전화 회사, 전자 메일 계정 및 개인 설정 웹 포털에 대 한 웹 사이트 사이에는 대부분의 사용자와 마찬가지로 기억할 수 있는 수십 개의 다른 암호가 있습니다. 이러한 일을 기억 하는 많은 자격 증명을 사용 하는 경우 사용자가 암호를 잊은 것은 드문 일이 아닙니다. 이를 고려 하 여 사용자 계정을 제공 하는 웹 사이트에서 사용자가 암호를 복구할 수 있는 방법을 포함 해야 합니다. 이 프로세스는 일반적으로 새 암호를 생성 하 고 파일의 사용자 전자 메일 주소로 전자 메일을 보냅니다. 사용자가 새 암호를 받은 후에는 대부분의 사용자가 사이트로 돌아와서 임의로 생성 된 암호를 기억 하기 쉬운 것으로 변경 합니다.

ASP.NET에는 암호 복구 및 변경을 지원 하기 위한 두 개의 웹 컨트롤이 포함 되어 있습니다. PasswordRecovery 컨트롤을 사용 하면 방문자가 분실 한 암호를 복구할 수 있습니다. ChangePassword 컨트롤을 사용 하면 사용자가 암호를 업데이트할 수 있습니다. 이 자습서 시리즈 전체에서 확인 한 다른 로그인 관련 웹 컨트롤과 마찬가지로 PasswordRecovery 및 ChangePassword 컨트롤은 백그라운드에서 사용자의 암호를 다시 설정 하거나 수정 하기 위해 멤버 자격 프레임 워크와 함께 작동 합니다.

이 자습서에서는 이러한 두 가지 컨트롤을 사용 하는 방법을 살펴봅니다. 또한 `MembershipUser` 클래스의 `ChangePassword` 및 `ResetPassword` 메서드를 통해 프로그래밍 방식으로 사용자의 암호를 변경 하 고 다시 설정 하는 방법을 알아봅니다.

## <a name="step-1-helping-users-recover-lost-passwords"></a>1 단계: 사용자가 분실 한 암호를 복구 하도록 지원

사용자 계정을 지 원하는 모든 웹 사이트는 잊어버린 암호를 복구 하기 위한 몇 가지 메커니즘을 사용자에 게 제공 해야 합니다. 좋은 소식은 ASP.NET에서 이러한 기능을 구현 하는 것이 PasswordRecovery 웹 컨트롤 덕분입니다. PasswordRecovery 컨트롤은 사용자에 게 사용자 이름을 요청 하는 인터페이스를 렌더링 하 고 필요한 경우 보안 질문에 대 한 답변을 표시 합니다. 그런 다음 사용자에 게 암호를 전자 메일로 보냅니다.

> [!NOTE]
> 전자 메일 메시지는 네트워크를 통해 일반 텍스트로 전송 되기 때문에 전자 메일을 통해 사용자의 암호를 전송 하는 것과 관련 된 보안 위험이 있습니다.

PasswordRecovery 컨트롤은 다음 세 가지 보기로 구성 됩니다.

- **사용자 이름** -방문자에 게 사용자 이름을 입력 하 라는 메시지를 표시 합니다. 초기 뷰입니다.
- **질문**-사용자의 사용자 이름 및 보안 질문을 텍스트로 표시 하 고 사용자가 보안 질문에 대 한 대답을 입력 하는 텍스트 상자와 함께 표시 합니다.
- **성공**-사용자에 게 암호가 전자 메일로 전송 되었음을 알리는 메시지를 표시 합니다.

PasswordRecovery 제어에서 수행 되는 보기 및 작업은 다음 멤버 자격 구성 설정에 따라 달라 집니다.

- `RequiresQuestionAndAnswer`
- `EnablePasswordRetrieval`
- `EnablePasswordReset`

멤버 프레임 프레임 워크의 `RequiresQuestionAndAnswer` 설정은 사용자가 계정에 등록할 때 보안 질문 및 대답을 지정 해야 하는지 여부를 나타냅니다. <a id="_msoanchor_1"> </a> [*사용자 계정 만들기*](../membership/creating-user-accounts-vb.md) 자습서에서 설명한 대로 `RequiresQuestionAndAnswer` True (기본값) 이면 CreateUserWizard의 인터페이스에 새 사용자의 보안 질문 및 답변에 대 한 TextBox 컨트롤이 포함 됩니다. `RequiresQuestionAndAnswer` False 이면 이러한 정보가 수집 되지 않습니다. 마찬가지로 `RequiresQuestionAndAnswer` True 이면 사용자가 사용자 이름을 입력 한 후 PasswordRecovery 컨트롤에서 질문 보기를 표시 합니다. 사용자가 올바른 보안 대답을 입력 하는 경우에만 암호가 복구 됩니다. 그러나 `RequiresQuestionAndAnswer` False 이면 PasswordRecovery 컨트롤이 사용자 이름 보기에서 성공 뷰로 바로 이동 합니다.

사용자가 사용자 이름 또는 사용자의 사용자 이름 및 보안 대답을 제공한 후 `RequiresQuestionAndAnswer` True 이면 PasswordRecovery에서 사용자의 암호를 전자 메일로 보냅니다. `EnablePasswordRetrieval` 옵션이 True로 설정 된 경우 사용자는 현재 암호를 이메일로 전송 합니다. False로 설정 되 고 `EnablePasswordReset` True로 설정 된 경우 PasswordRecovery 컨트롤은 사용자에 대 한 새로운 무작위 암호를 생성 하 고이 새 암호를 전자 메일로 보냅니다. `EnablePasswordRetrieval`와 `EnablePasswordReset` 모두 False 인 경우 PasswordRecovery 컨트롤에서 예외를 throw 합니다.

> [!NOTE]
> `SqlMembershipProvider`은 사용자의 암호를 Clear, 해시 됨 (기본값) 또는 암호화의 세 가지 형식 중 하나로 저장 합니다. 사용 되는 저장소 메커니즘은 멤버 자격 구성 설정에 따라 달라 집니다. 데모 응용 프로그램은 해시 된 암호 형식을 사용 합니다. 해시 된 암호 형식을 사용할 때 시스템은 데이터베이스에 저장 된 해시 된 버전에서 사용자의 실제 암호를 확인할 수 없기 때문에 `EnablePasswordRetrieval` 옵션을 False로 설정 해야 합니다.

그림 1에서는 PasswordRecovery의 인터페이스 및 동작이 멤버 자격 구성에 의해 영향을 받는 방식을 보여 줍니다.

[RequiresQuestionAndAnswer, EnablePasswordRetrieval 및 Enablepasswordretrieval ![PasswordRecovery 컨트롤의 모양과 동작에 영향을 줍니다.](recovering-and-changing-passwords-vb/_static/image2.png)](recovering-and-changing-passwords-vb/_static/image1.png)

**그림 1**: `RequiresQuestionAndAnswer`, `EnablePasswordRetrieval`및 `EnablePasswordReset` passwordrecovery 컨트롤의 모양과 동작에 영향을 줍니다 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image3.png)).

> [!NOTE]
> <a id="_msoanchor_2"> </a> [*SQL Server에서 멤버 자격 스키마 만들기*](../membership/creating-the-membership-schema-in-sql-server-vb.md) 자습서에서는 `RequiresQuestionAndAnswer`를 true로 설정 하 여 멤버 자격 공급자를 구성 하 고 `EnablePasswordRetrieval`를 False로 설정 하 고 `EnablePasswordReset`을 true로 설정 합니다.

### <a name="using-the-passwordrecovery-control"></a>PasswordRecovery 제어 사용

ASP.NET 페이지에서 PasswordRecovery 컨트롤을 사용 하는 방법을 살펴보겠습니다. `RecoverPassword.aspx`를 열고 PasswordRecovery 컨트롤을 도구 상자에서 디자이너로 끌어 놓습니다. 해당 `ID` `RecoverPwd`로 설정 합니다. Login 및 CreateUserWizard 웹 컨트롤과 마찬가지로 PasswordRecovery 컨트롤의 뷰는 레이블, 텍스트 상자, 단추 및 유효성 검사 컨트롤을 포함 하는 풍부한 복합 인터페이스를 렌더링 합니다. 컨트롤의 스타일 속성을 통해 또는 뷰를 템플릿으로 변환 하 여 보기의 모양을 사용자 지정할 수 있습니다. 관심이 있는 독자를 위한 연습으로 남겨 둡니다.

사용자가이 페이지를 방문 하면 사용자의 사용자 이름을 입력 하 고 제출 단추를 클릭 합니다. 멤버 자격 구성 설정에서 `RequiresQuestionAndAnswer` 속성을 True로 설정 했으므로 PasswordRecovery 컨트롤이 질문 뷰를 표시 합니다. 사용자가 올바른 보안 대답을 입력 하 고 제출을 클릭 하면 PasswordRecovery 컨트롤은 사용자의 암호를 임의로 생성 된 암호를 업데이트 하 고이 암호를 파일의 전자 메일 주소로 전자 메일로 보냅니다. 코드를 한 줄도 작성 하지 않아도이 모든 것이 가능 합니다.

이 페이지를 테스트 하기 전에 다음을 수행 하는 것이 가장 일반적입니다. `Web.config`에서 메일 배달 설정을 지정 해야 합니다. PasswordRecovery 컨트롤은 전자 메일을 보내기 위한 이러한 설정에 의존 합니다.

메일 배달 구성은 [`<system.net>` 요소의](https://msdn.microsoft.com/library/6484zdc1.aspx) [`<mailSettings>` 요소](https://msdn.microsoft.com/library/w355a94k.aspx)를 통해 지정 됩니다. [`<smtp>` 요소](https://msdn.microsoft.com/library/ms164240.aspx) 를 사용 하 여 배달 방법과 기본 보낸 사람 주소를 지정 합니다. 다음 태그는 포트 25에서 `smtp.example.com` 라는 네트워크 SMTP 서버를 사용 하 고 사용자 이름 및 암호의 사용자 이름/암호 자격 증명을 사용 하도록 메일 설정을 구성 합니다.

> [!NOTE]
> `<system.net>`은 루트 `<configuration>` 요소의 자식 요소와 `<system.web>`의 형제입니다. 따라서 `<system.web>` 요소 내에 `<system.net>` 요소를 배치 하지 마십시오. 대신 같은 수준에 배치 합니다.

[!code-xml[Main](recovering-and-changing-passwords-vb/samples/sample1.xml)]

네트워크에서 SMTP 서버를 사용 하는 것 외에도 전자 메일 메시지를 보낼 픽업 디렉터리를 지정할 수 있습니다.

SMTP 설정을 구성한 후 브라우저를 통해 `RecoverPassword.aspx` 페이지를 방문 합니다. 먼저 사용자 저장소에 존재 하지 않는 사용자 이름을 입력 해 보세요. 그림 2에 나와 있는 것 처럼 PasswordRecovery 컨트롤은 사용자 정보에 액세스할 수 없음을 나타내는 메시지를 표시 합니다. 메시지의 텍스트는 컨트롤의 [`UserNameFailureText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.usernamefailuretext.aspx)을 통해 사용자 지정할 수 있습니다.

[![잘못 된 사용자 이름을 입력 하면 오류 메시지가 표시 됩니다.](recovering-and-changing-passwords-vb/_static/image5.png)](recovering-and-changing-passwords-vb/_static/image4.png)

**그림 2**: 잘못 된 사용자 이름을 입력 하는 경우 오류 메시지가 표시 됨 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image6.png))

이제 사용자 이름을 입력 합니다. 사용자가 액세스할 수 있는 전자 메일 주소를 사용 하 여 시스템의 계정에 대 한 사용자 이름 및 보안 대답을 사용 합니다. 사용자 이름을 입력 하 고 제출을 클릭 하면 PasswordRecovery 컨트롤이 해당 질문 보기를 표시 합니다. 사용자 이름 보기와 마찬가지로, 잘못 된 대답을 입력 하면 PasswordRecovery 컨트롤에서 오류 메시지를 표시 합니다 (그림 3 참조). [`QuestionFailureText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.questionfailuretext.aspx) 을 사용 하 여이 오류 메시지를 사용자 지정할 수 있습니다.

[사용자가 잘못 된 보안 대답을 입력 하는 경우 오류 메시지가 표시 ![](recovering-and-changing-passwords-vb/_static/image8.png)](recovering-and-changing-passwords-vb/_static/image7.png)

**그림 3**: 사용자가 잘못 된 보안 대답을 입력 하는 경우 오류 메시지가 표시 됨 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image9.png))

마지막으로 올바른 보안 대답을 입력 하 고 제출을 클릭 합니다. 내부적으로 PasswordRecovery 컨트롤은 임의의 암호를 생성 하 여 사용자 계정에 할당 하 고 사용자에 게 새 암호를 알려 주는 전자 메일을 보낸 다음 (그림 4 참조) 성공 뷰를 표시 합니다.

[사용자가 새 암호를 사용 하 여 전자 메일을 보내는 ![](recovering-and-changing-passwords-vb/_static/image11.png)](recovering-and-changing-passwords-vb/_static/image10.png)

**그림 4**: 사용자에 게 새 암호를 포함 하는 전자 메일을 보냈습니다 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image12.png)).

### <a name="customizing-the-email"></a>전자 메일 사용자 지정

PasswordRecovery 컨트롤에서 보낸 기본 전자 메일은 더 이상 표시 되지 않습니다 (그림 4 참조). 이 메시지는 `<smtp>` 요소의 `from` 특성에 지정 된 계정에서 주체 암호와 일반 텍스트 본문과 함께 전송 됩니다.

사이트로 돌아가서 다음 정보를 사용 하 여 로그인 하세요.

사용자 *이름: 사용자 이름*

암호: *암호*

PasswordRecovery 컨트롤의 [`SendingMail` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.sendingmail.aspx)에 대 한 이벤트 처리기를 통해 프로그래밍 방식으로 사용자 지정 하거나 [`MailDefinition` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.maildefinition.aspx)을 통해 선언적으로이 메시지를 사용자 지정할 수 있습니다. 이러한 두 옵션을 살펴보겠습니다.

`SendingMail` 이벤트는 전자 메일 메시지를 보내기 직전에 발생 하며 전자 메일 메시지를 프로그래밍 방식으로 조정 하는 마지막 기회입니다. 이 이벤트가 발생 하면 이벤트 처리기에 [`MailMessageEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.mailmessageeventargs.aspx)형식의 개체가 전달 되 고 `Message` 속성에는 보낼 전자 메일에 대 한 참조가 포함 됩니다.

`SendingMail` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다 .이 코드는 프로그래밍 방식으로 참조 목록에 `webmaster@example.com`를 추가 합니다.

[!code-vb[Main](recovering-and-changing-passwords-vb/samples/sample2.vb)]

선언적 방법을 사용 하 여 전자 메일 메시지를 구성할 수도 있습니다. PasswordRecovery의 `MailDefinition` 속성은 [`MailDefinition`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.aspx)형식의 개체입니다. `MailDefinition` 클래스는 `From`, `CC`, `Priority`, `Subject`, `IsBodyHtml`, `BodyFileName`및 기타를 비롯 한 전자 메일 관련 속성의 호스트를 제공 합니다. 처음에는 암호를 다시 설정 하는 것과 같이 [`Subject` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.subject.aspx) 을 기본적으로 사용 되는 것 보다 더 설명적인 이름 (암호)으로 설정 합니다.

전자 메일 메시지의 본문을 사용자 지정 하려면 본문의 내용이 포함 된 별도의 전자 메일 템플릿 파일을 만들어야 합니다. 먼저 `EmailTemplates`이라는 웹 사이트에서 새 폴더를 만듭니다. 그런 다음 `PasswordRecovery.txt` 라는 폴더에 새 텍스트 파일을 추가 하 고 다음 콘텐츠를 추가 합니다.

[!code-aspx[Main](recovering-and-changing-passwords-vb/samples/sample3.aspx)]

자리 표시자 `<%UserName%>`와 `<%Password%>`를 사용 합니다. PasswordRecovery 컨트롤은 전자 메일을 보내기 전에 이러한 두 자리 표시자를 사용자의 사용자 이름 및 복구 된 암호로 자동으로 대체 합니다.

마지막으로, `MailDefinition`의 [`BodyFileName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx) 을 방금 만든 전자 메일 템플릿 (`~/EmailTemplates/PasswordRecovery.txt`)으로 가리킵니다.

이러한 변경을 수행한 후 `RecoverPassword.aspx` 페이지를 다시 방문 하 고 사용자 이름 및 보안 대답을 입력 합니다. 그림 5와 같은 전자 메일을 받게 됩니다. `webmaster@example.com`은 참조 된 것 이며 주체와 본문은 업데이트 된 것입니다.

[![제목, 본문 및 참조 목록이 업데이트 되었습니다.](recovering-and-changing-passwords-vb/_static/image14.png)](recovering-and-changing-passwords-vb/_static/image13.png)

**그림 5**: 제목, 본문 및 참조 목록이 업데이트 되었습니다 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image15.png)).

HTML 형식 전자 메일 집합 [`IsBodyHtml`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.isbodyhtml.aspx) 를 True (기본값은 False)로 보내고 html을 포함 하도록 전자 메일 템플릿을 업데이트 합니다.

`MailDefinition` 속성이 PasswordRecovery 클래스에 고유 하지 않습니다. 2 단계에서 볼 수 있듯이 ChangePassword 컨트롤은 `MailDefinition` 속성도 제공 합니다. 또한 CreateUserWizard 컨트롤에는 새 사용자에 게 환영 전자 메일 메시지를 자동으로 보내도록 구성할 수 있는 속성이 포함 되어 있습니다.

> [!NOTE]
> 현재는 왼쪽 탐색에 `RecoverPassword.aspx` 페이지에 연결 하는 링크가 없습니다. 사용자는 사이트에 성공적으로 로그온 할 수 없는 경우에만이 페이지를 방문 하는 데 관심이 있습니다. 따라서 `RecoverPassword.aspx` 페이지에 대 한 링크를 포함 하도록 `Login.aspx` 페이지를 업데이트 합니다.

### <a name="programmatically-resetting-a-users-password"></a>프로그래밍 방식으로 사용자 암호 다시 설정

사용자 암호를 다시 설정할 때 PasswordRecovery 컨트롤은 `MembershipUser` 개체의 [`ResetPassword` 메서드](https://msdn.microsoft.com/library/system.web.security.membershipuser.resetpassword.aspx)를 호출 합니다. 이 메서드에는 두 개의 오버 로드가 있습니다.

- **[`ResetPassword`](https://msdn.microsoft.com/library/d94bdzz2.aspx)** -사용자의 암호를 다시 설정 합니다. `RequiresQuestionAndAnswer` False 인 경우이 오버 로드를 사용 합니다.
- **[`ResetPassword(securityAnswer)`](https://msdn.microsoft.com/library/d90zte4w.aspx)** -제공 된 *보안 대답이* 올바른 경우에만 사용자 암호를 다시 설정 합니다. `RequiresQuestionAndAnswer` True 인 경우이 오버 로드를 사용 합니다.

두 오버 로드는 임의로 새로 생성 된 새 암호를 반환 합니다.

멤버 자격 프레임 워크의 다른 메서드와 마찬가지로 `ResetPassword` 메서드는 구성 된 공급자에 위임 합니다. `SqlMembershipProvider`은 다른 필드 중에서 사용자의 사용자 이름, 새 암호 및 제공 된 암호 대답을 전달 하 여 `aspnet_Membership_ResetPassword` 저장 프로시저를 호출 합니다. 저장 프로시저는 암호 대답이 일치 하는지 확인 한 다음 사용자의 암호를 업데이트 합니다.

몇 가지 낮은 수준 구현 참고 사항:

- 잠긴 사용자는 자신의 암호를 재설정할 수 없습니다. 그러나 승인 되지 않은 사용자는이 될 수 있습니다. <a id="_msoanchor_3"> </a> [*사용자 계정 잠금 해제 및*](unlocking-and-approving-user-accounts-vb.md) 승인 자습서에서 잠긴 상태와 승인 된 상태에 대해 더 자세히 설명 합니다.
- 암호 대답이 잘못 된 경우 사용자의 실패 한 암호 대답 시도 횟수가 증가 합니다. 지정 된 기간 내에 잘못 된 보안 대답 시도가 지정 된 횟수 만큼 발생 하면 사용자가 잠깁니다.

### <a name="a-word-on-how-the-random-passwords-are-generated"></a>임의의 암호를 생성 하는 방법에 대 한 단어

그림 4 및 5의 메일 메시지에 표시 되는 임의로 생성 된 암호는 멤버 관리 클래스의 [`GeneratePassword` 메서드에서](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)생성 됩니다. 이 메서드는 두 개의 정수 입력 매개 변수 *길이* 와 *numberOfNonAlphanumericCharacters* 를 수락 하 고 최소 *numberOfNonAlphanumericCharacters* 수가 영숫자가 아닌 문자 이상으로 *길이가* 긴 문자열을 반환 합니다. 멤버 자격 클래스 또는 로그인 관련 웹 컨트롤 내에서이 메서드를 호출 하는 경우 이러한 두 매개 변수의 값은 각각 7 및 1로 설정 된 멤버 자격 구성의 `MinRequiredPasswordLength` 및 `MinRequiredNonalphanumericCharacters` 속성에 따라 결정 됩니다.

`GeneratePassword` 메서드는 암호화 된 난수 생성기를 사용 하 여 임의 문자를 선택 하는 데 아무런 바이어스가 없는지 확인 합니다. 또한 `GeneratePassword` `Public`되므로 임의의 문자열이 나 암호를 생성 해야 하는 경우 ASP.NET 응용 프로그램에서 직접 사용할 수 있습니다.

> [!NOTE]
> `SqlMembershipProvider` 클래스는 항상 14 자 이상으로 임의의 암호를 생성 하므로 `MinRequiredPasswordLength` 14 보다 작은 경우 해당 값은 무시 됩니다.

## <a name="step-2-changing-passwords"></a>2 단계: 암호 변경

임의로 생성 된 암호는 기억을 어렵습니다. 그림 4: `WWGUZv(f2yM:Bd`에 표시 된 암호를 고려 합니다. 메모리에 커밋을 시도 합니다. 사용자가이 정렬의 임의로 생성 된 암호를 보낸 후에는 암호를 기억 하기 쉬운 항목으로 변경할 수 있습니다.

ChangePassword 컨트롤을 사용 하 여 사용자가 암호를 변경 하는 인터페이스를 만듭니다. PasswordRecovery 컨트롤과 매우 유사 하 게 ChangePassword 컨트롤은 암호 변경 및 성공의 두 뷰로 구성 됩니다. 암호 변경 보기는 사용자에 게 이전 암호와 새 암호를 묻는 메시지를 표시 합니다. 올바른 이전 암호와 최소 길이 및 영숫자가 아닌 문자 요구 사항을 충족 하는 새 암호를 제공 하면 ChangePassword 컨트롤은 사용자의 암호를 업데이트 하 고 성공 보기를 표시 합니다.

> [!NOTE]
> ChangePassword 컨트롤은 `MembershipUser` 개체의 [`ChangePassword` 메서드](https://msdn.microsoft.com/library/system.web.security.membershipuser.changepassword.aspx)를 호출 하 여 사용자의 암호를 수정 합니다. ChangePassword 메서드는 두 개의 `String` 입력 매개 변수인 *oldpassword* 및 *newPassword*를 수락 하 고, 제공 된 *oldpassword* 가 올바르면 사용자 계정을 *newPassword*로 업데이트 합니다.

`ChangePassword.aspx` 페이지를 열고 페이지에 ChangePassword 컨트롤을 추가 하 여 `ChangePwd`이름을 지정 합니다. 이 시점에서 디자인 뷰에는 암호 변경 보기가 표시 됩니다 (그림 6 참조). PasswordRecovery 컨트롤과 마찬가지로 컨트롤의 스마트 태그를 통해 뷰 간을 전환할 수 있습니다. 또한 이러한 보기의 모양은 다양 한 스타일 속성을 통해 사용자 지정 하거나 템플릿으로 변환 하 여 사용자 지정할 수 있습니다.

[페이지에 ChangePassword 컨트롤을 추가 ![](recovering-and-changing-passwords-vb/_static/image17.png)](recovering-and-changing-passwords-vb/_static/image16.png)

**그림 6**: 페이지에 ChangePassword 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image18.png))

ChangePassword 컨트롤은 현재 로그인 한 사용자의 암호 *또는* 지정 된 다른 사용자의 암호를 업데이트할 수 있습니다. 그림 6에 표시 된 것 처럼 기본 암호 변경 보기는 이전 암호와 새 암호에 대해 각각 하나씩, 세 개의 TextBox 컨트롤을 렌더링 합니다. 이 기본 인터페이스는 현재 로그온 한 사용자의 암호를 업데이트 하는 데 사용 됩니다.

ChangePassword 컨트롤을 사용 하 여 다른 사용자의 암호를 업데이트 하려면 컨트롤의 [`DisplayUserName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.changepassword.displayusername.aspx) 을 True로 설정 합니다. 이렇게 하면 네 번째 텍스트 상자가 페이지에 추가 되어 암호를 변경할 사용자의 사용자 이름을 묻는 메시지가 표시 됩니다.

로그인 할 필요 없이 로그 아웃 된 사용자가 암호를 변경 하도록 하려면 `DisplayUserName`를 True로 설정 하는 것이 유용 합니다. 개인적으로, 사용자가 자신의 암호를 변경 하도록 허용 하기 전에 사용자에 게 로그인을 요구 하는 것이 잘못 된 것으로 생각 합니다. 따라서 `DisplayUserName`을 False (기본값)로 설정 된 상태로 둡니다. 그러나이 결정을 내릴 때 익명 사용자가이 페이지에 도달 하는 것을 기본적으로 제한 하 게 됩니다. 익명 사용자가 `ChangePassword.aspx`를 방문 하지 못하도록 사이트의 URL 권한 부여 규칙을 업데이트 합니다. URL 권한 부여 규칙 구문에서 메모리를 새로 고쳐야 하는 경우에는 <a id="_msoanchor_4"> </a> [*사용자 기반 권한 부여*](../membership/user-based-authorization-vb.md) 자습서를 다시 참조 하세요.

> [!NOTE]
> `DisplayUserName` 속성은 관리자가 다른 사용자의 암호를 변경할 수 있도록 하는 데 유용 하다는 것을 볼 수 있습니다. 그러나 `DisplayUserName`가 True로 설정 된 경우에도 올바른 이전 암호를 알고 입력 해야 합니다. 3 단계에서 관리자가 사용자 암호를 변경할 수 있도록 하는 기술에 대해 설명 합니다.

브라우저를 통해 `ChangePassword.aspx` 페이지를 방문 하 여 암호를 변경 합니다. 멤버 자격 구성에 지정 된 암호 길이 및 영숫자가 아닌 문자 요구 사항을 충족 하지 못하는 새 암호를 입력 하는 경우 오류 메시지가 표시 됩니다 (그림 7 참조).

[페이지에 ChangePassword 컨트롤을 추가 ![](recovering-and-changing-passwords-vb/_static/image20.png)](recovering-and-changing-passwords-vb/_static/image19.png)

**그림 7**: 페이지에 ChangePassword 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image21.png))

올바른 기존 암호와 새 암호를 입력 하면 로그온 한 사용자의 암호가 변경 되 고 성공 뷰가 표시 됩니다.

### <a name="sending-a-confirmation-email"></a>확인 전자 메일 보내기

기본적으로 ChangePassword 컨트롤은 암호가 방금 업데이트 된 사용자에 게 전자 메일 메시지를 보내지 않습니다. 전자 메일을 보내려면 컨트롤의 `MailDefinition` 속성을 구성 하기만 하면 됩니다. 사용자가 새 암호를 포함 하는 HTML 형식 전자 메일을 보내도록 ChangePassword 컨트롤을 구성 하겠습니다.

`ChangePassword.htm`이라는 `EmailTemplates` 폴더에 새 파일을 만들어 시작 합니다. 다음 태그를 추가 합니다.

[!code-html[Main](recovering-and-changing-passwords-vb/samples/sample4.html)]

그런 다음 ChangePassword 컨트롤의 `MailDefinition` 속성 `BodyFileName`, `IsBodyHtml`및 `Subject` 속성을 ~/EmailTemplates/ChangePassword.htm, True로 설정 하 고 암호를 각각 변경 합니다.

이러한 변경을 수행한 후에는 페이지를 다시 방문 하 여 암호를 다시 변경 합니다. 이번에는 ChangePassword 컨트롤이 사용자 지정 된 HTML 형식 전자 메일을 파일의 사용자 전자 메일 주소로 보냅니다 (그림 8 참조).

[사용자에 게 암호가 변경 되었음을 알리는 전자 메일 메시지를 ![합니다.](recovering-and-changing-passwords-vb/_static/image23.png)](recovering-and-changing-passwords-vb/_static/image22.png)

**그림 8**: 사용자에 게 암호가 변경 되었음을 알리는 전자 메일 메시지 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image24.png))

## <a name="step-3-allowing-administrators-to-change-users-passwords"></a>3 단계: 관리자가 사용자의 암호를 변경할 수 있도록 허용

사용자 계정을 지 원하는 응용 프로그램의 일반적인 기능은 관리자가 다른 사용자의 암호를 변경할 수 있는 기능입니다. 시스템에 사용자가 자신의 암호를 변경할 수 있는 기능이 없기 때문에이 기능이 필요한 경우도 있습니다. 이 경우 사용자가 잊어버린 암호를 복구 하는 유일한 방법은 관리자가 새 암호를 할당 하는 것입니다. 그러나 PasswordRecovery 및 ChangePassword 컨트롤을 사용 하면 관리자가 사용자의 암호를 변경 하는 작업을 수행할 수 있으므로 사용자가 자신의 암호를 변경 하지 않아도 됩니다.

그러나 클라이언트가 관리자에 게 다른 사용자의 암호를 변경할 수 있는 insists? 아쉽게도이 기능을 추가 하는 것은 약간의 작업 일 수 있습니다. 사용자 암호를 변경 하려면 `MembershipUser` 개체의 `ChangePassword` 메서드에 이전 암호와 새 암호를 제공 해야 하지만, 관리자가 사용자의 암호를 알고 있어야 수정할 수 있습니다.

한 가지 해결 방법은 먼저 사용자의 암호를 다시 설정한 후 다음과 같은 코드를 사용 하 여 새 암호로 변경 하는 것입니다.

[!code-vb[Main](recovering-and-changing-passwords-vb/samples/sample5.vb)]

이 코드는 관리자가 변경 하려는 암호의 사용자 인 사용자 *이름*에 대 한 정보를 검색 하는 것으로 시작 합니다. 그런 다음 `ResetPassword` 메서드를 호출 하 여 사용자에 게 새 임의 암호를 할당 합니다. 임의로 생성 된이 암호는 메서드에 의해 반환 되 고 `resetPwd`변수에 저장 됩니다. 이제 사용자의 암호를 알고 있으므로 `ChangePassword`에 대 한 호출을 통해 변경할 수 있습니다.

문제는 `RequiresQuestionAndAnswer` False 인 멤버 자격 시스템 구성이 설정 된 경우에만이 코드가 작동 한다는 것입니다. 응용 프로그램에서와 같이 `RequiresQuestionAndAnswer` True 이면 `ResetPassword` 메서드에 보안 대답을 전달 해야 합니다. 그렇지 않으면 예외가 throw 됩니다.

보안 질문 및 대답을 요구 하도록 멤버 자격 프레임 워크를 구성 하 고 클라이언트에서 관리자에 게 사용자 암호를 변경할 수 insists 하는 경우 세 가지 옵션이 있습니다.

- 비행기에서 손을 발생 시키고, 이것이 수행할 수 없는 유일한 일 임을 클라이언트에 알립니다.
- `RequiresQuestionAndAnswer`을 False로 설정 합니다. 이로 인해 응용 프로그램의 보안이 떨어집니다. 부정한 사용자가 다른 사용자의 전자 메일 수신함에 대 한 액세스 권한을 획득 했다고 가정 합니다. 손상 된 사용자가 자신의 책상을 떠난 후에 워크스테이션을 잠그지 않았거나 공용 터미널에서 전자 메일에 액세스 하 여 로그 아웃 하지 않았을 수 있습니다. 두 경우 모두 부정한 사용자는 `RecoverPassword.aspx` 페이지를 방문 하 여 사용자의 사용자 이름을 입력할 수 있습니다. 그러면 시스템이 보안 대답을 묻지 않고 복구 된 암호를 전자 메일로 보냅니다.
- 멤버 프레임 프레임 워크에서 만든 추상화 계층을 우회 하 고 SQL Server 데이터베이스로 직접 작업 합니다. 멤버 자격 스키마에는 사용자 암호를 설정 하 고 해당 작업을 수행 하기 위해 보안 대답 또는 이전 암호를 요구 하지 않는 `aspnet_Membership_SetPassword` 라는 저장 프로시저가 포함 되어 있습니다.

이러한 옵션은 특히 매력적인 것은 아니지만 개발자의 생명은 경우에 따라 다를 수 있습니다.

`Membership` 및 `MembershipUser` 클래스를 우회 하 고 `SecurityTutorials` 데이터베이스에 대해 직접 작동 하는 코드를 작성 하는 세 번째 방법을 앞에서 구현 했습니다.

> [!NOTE]
> 데이터베이스를 직접 사용 하 여 멤버 자격 프레임 워크에서 제공 하는 캡슐화는 부서 합니다. 이 의사 결정은 `SqlMembershipProvider`에 연결 하 여 코드를 이식할 수 없게 만듭니다. 또한이 코드는 멤버 자격 스키마가 변경 되는 경우 ASP.NET의 이후 버전에서 예상 대로 작동 하지 않을 수 있습니다. 이 방법은 해결 방법 이며, 대부분의 대안과 마찬가지로 모범 사례에 대 한 예가 아닙니다.

코드에는 몇 가지 끌지 비트가 있으며 매우 긴 경우 따라서이 자습서를 심층적으로 조사 하는 것이 좋습니다. 더 자세히 알아보려면이 자습서에 대 한 코드를 다운로드 하 고 `~/Administration/ManageUsers.aspx` 페이지를 방문 하세요. <a id="_msoanchor_5"> </a> [이전 자습서](building-an-interface-to-select-one-user-account-from-many-vb.md)에서 만든이 페이지에는 각 사용자가 나열 됩니다. `UserInformation.aspx` 페이지에 대 한 링크를 포함 하도록 GridView를 업데이트 하 고, querystring을 통해 선택한 사용자의 사용자 이름을 전달 합니다. `UserInformation.aspx` 페이지에는 선택한 사용자에 대 한 정보와 암호를 변경 하는 텍스트 상자가 표시 됩니다 (그림 9 참조).

새 암호를 입력 하 고 두 번째 텍스트 상자에서 확인 한 후 사용자 업데이트 단추를 클릭 하면 다시 게시 ensues 및 `aspnet_Membership_SetPassword` 저장 프로시저가 호출 되어 사용자의 암호가 업데이트 됩니다. 이 기능에 관심이 있는 독자 들이 코드에 보다 친숙 하 게 하 고, 암호를 변경한 사용자에 게 전자 메일을 보내는 것을 포함 하도록 기능을 확장 하는 것이 좋습니다.

[관리자가 사용자의 암호를 변경할 수 ![](recovering-and-changing-passwords-vb/_static/image26.png)](recovering-and-changing-passwords-vb/_static/image25.png)

**그림 9**: 관리자가 사용자의 암호를 변경할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image27.png)).

> [!NOTE]
> `UserInformation.aspx` 페이지는 현재 멤버 프레임 워크가 암호화 되지 않은 형식으로 암호를 저장 하도록 구성 된 경우에만 작동 합니다. 이 기능을 추가 하기 위해 초대 했지만 새 암호를 암호화 하는 코드는 없습니다. 필요한 코드를 추가 하는 방법은 디컴파일러와 같은 코드를 사용 하 [여 .NET Framework](http://www.aisto.com/roeder/dotnet/) 의 메서드에 대 한 소스 코드를 검사 하는 것입니다. `SqlMembershipProvider` 클래스의 `ChangePassword` 메서드를 검사 하 여 시작 합니다. 암호의 해시를 만들기 위한 코드를 작성 하는 데 사용 하는 기술입니다.

## <a name="summary"></a>요약

ASP.NET는 사용자가 암호를 관리 하는 데 도움이 되는 두 가지 컨트롤을 제공 합니다. PasswordRecovery 컨트롤은 암호를 잊어버린 사용자에 게 유용 합니다. 멤버 프레임 워크의 구성에 따라 사용자는 기존 암호나 임의로 생성 된 새 암호를 전자 메일로 전송 합니다. ChangePassword 컨트롤을 사용 하면 사용자가 암호를 업데이트할 수 있습니다.

Login 및 CreateUserWizard 컨트롤과 마찬가지로 PasswordRecovery 및 ChangePassword 컨트롤은 몇 가지 선언적 태그나 코드 줄을 작성 하지 않고도 풍부한 사용자 인터페이스를 렌더링 합니다. 기본 사용자 인터페이스가 사용자의 요구를 충족 하지 않는 경우 다양 한 스타일 속성을 통해 사용자 지정할 수 있습니다. 또는 훨씬 더 세부적인 제어를 위해 컨트롤의 인터페이스를 템플릿으로 변환할 수 있습니다. 내부적으로 이러한 컨트롤은 멤버 자격 API를 사용 하 여 `MembershipUser` 개체의 `ResetPassword` 및 `ChangePassword` 메서드를 호출 합니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ChangePassword 컨트롤 퀵 스타트](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/changepassword.aspx)
- [PasswordRecovery 제어 퀵 스타트](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/passwordrecovery.aspx)
- [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`System.Net.Mail` Faq](http://www.systemnetmail.com/)

### <a name="about-the-author"></a>작성자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 선임 검토자는 Michael Emmings 및 Suchi Banerjee를 포함 합니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 에 줄을 놓습니다.

> [!div class="step-by-step"]
> [이전](building-an-interface-to-select-one-user-account-from-many-vb.md)
> [다음](unlocking-and-approving-user-accounts-vb.md)
