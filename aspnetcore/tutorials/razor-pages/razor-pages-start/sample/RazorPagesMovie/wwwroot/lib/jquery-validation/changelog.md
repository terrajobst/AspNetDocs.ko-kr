---
ms.openlocfilehash: 170d5ec71b0789bc1efb43fbdd4e24eab36a8cc4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037370"
---
<a name="--"></a>--
==================

## <a name="core"></a>코어
  * 사용하지 않는 removeAttrs 메서드 제거
  * URL 메서드에 대한 regex 바꾸기
  * $.ajax의 잘못된 url 매개 변수를 제거하고 $.extend로 덮어쓰기
  * 중첩된 취소 제출 단추를 올바르게 처리
  * 들여쓰기 수정
  * attributeRules 및 dataRules를 리팩터링하여 normalizer 공유
  * 숫자 입력을 위해 값을 숫자로 변환하는 dataRules 메서드
  * 프로토콜 상대 URL을 허용하도록 URL 메서드 업데이트
  * 더 이상 사용되지 않는 $.format 자리 표시자 제거
  * jQuery 1.7+ on/off 사용, destroy 메서드 추가
  * IE8 호환성으로 인해 .indexOf가 $.inArray로 변경됨
  * Opera Mini에 대해 NaN 값 특성을 정의되지 않음으로 캐스팅
  * 필수 메서드 내의 값 자르기 중지
  * :disabled 선택기를 사용하여 비활성화된 요소 일치
  * 일부 키보드 키를 제외하여 필드의 유효성 검사 방지
  * 전체 DOM에서 라디오/확인란 요소 검색 안 함
  * 잘못된 규칙 메서드에 대해 더 나은 오류 throw
  * 숫자 유효성 검사 오류를 수정함
  * whatwg 사양에 대한 참조 수정
  * 사용자 지정 입력 집합의 유효성을 검사할 때 잘못된 요소에 포커스 지정
  * 사용자 지정 강조 표시 메서드를 사용할 때 요소 스타일 재설정
  * 오류 ID의 달러 기호 이스케이프
  * “비활성화된 필드뿐만 아니라 읽기 전용 필드도 무시합니다.” 되돌리기
  * Luhn 알고리즘에 대한 주석의 링크 업데이트

## <a name="additionals"></a>추가 사항
  * dateITA를 업데이트하여 표준 시간대 문제 해결
  * 확장 메서드를 메서드 기간으로만 수정
  * 기간 일치만 검색하도록 accept 메서드 수정
  * 1자리 숫자 시간을 허용하도록 time 메서드 업데이트
  * notEqualTo 메서드에 대한 잘못된 테스트 삭제
  * notEqualTo 메서드 추가
  * `$`를 통해 올바른 jQuery 참조 사용
  * iban 메서드에서 불필요한 regex 확인 제거
  * 브라질 CPF 번호

## <a name="localization"></a>지역화
  * messages_tr.js 업데이트
  * messages_sr_lat.js 업데이트
  * 페루 스페인어(ES PE) 추가
  * 조지아어(ქართული, ge) 추가
  * 카탈로니아어 번역에서 오타가 수정됨
  * 핀란드어(fi) 번역 개선
  * 아르메니아어(hy_AM) 로케일 추가
  * currency 메서드로 이탈리아어(it) 번역 확장
  * bn_BD 로케일 추가
  * zh 로케일 업데이트
  * 이탈리아어 메시지 끝에서 Full Stop 제거

<a name="1131--2014-10-14"></a>1.13.1 / 2014-10-14
==================

## <a name="core"></a>코어
  * autoCreateRanges에 대한 값으로 0 허용
  * 모든 validationTargetFor 요소에 무시 설정 적용
  * min/max/rangelength 메서드에서 값을 자르지 않음
  * errorsFor에서 선택기로 사용하기 전에 ID/이름 이스케이프
  * focusCleanup 옵션의 명시적 기본값
  * describedby 선택기의 잘못된 regexp 수정
  * 비활성화된 필드뿐만 아니라 읽기 전용 필드 무시
  * ID 이스케이프를 개선하고, 이스케이프된 ID를 describedby에 저장
  * submitHandler의 반환 값을 사용하여 폼 제출 허용 또는 금지

## <a name="additionals"></a>추가 사항
  * postalcodeBR 메서드 추가
  * 매개 변수가 문자열인 경우 패턴 메서드 수정


<a name="1130--2014-07-01"></a>1.13.0 / 2014-07-01
==================

## <a name="all"></a>모두
* 플러그 인 UMD 래퍼 추가

## <a name="core"></a>코어
* 오류가 아닌 aria-describedby 및 숨겨진 빈 오류 유지
* dateISO RegExp 개선
* click-event를 위임하는 라디오/확인란을 추가함
* non-label 요소에 aria-describedby 사용
* 라디오/확인란에 focusin, focusout 및 keyup도 등록
* rangelength 특성 값에 대한 정규화 수정
* type="number" 필드를 처리하도록 elementValue 메서드 업데이트
* IE8(?)을 지원하기 위해 문자열에 배열 표기법 대신 charAt 사용

## <a name="localization"></a>지역화
* rangelength 메서드의 슬로바키아어 변역 수정
* 핀란드어 메서드 추가
* GL 번호 유효성 검사 메시지를 수정함
* ES 번호 메서드 유효성 검사 메시지를 수정함
* galician(GL)을 추가함
* 최소 및 최대 메서드에 대한 프랑스어 메시지를 수정함

## <a name="additionals"></a>추가 사항
* statesUS 메서드 추가
* dateITA 메서드를 수정하여 DST 버그 처리
* 이란어 날짜 메서드 추가
* postalCodeCA 메서드 추가
* postalcodeIT 메서드 추가

<a name="1120--2014-04-01"></a>1.12.0 / 2014-04-01
==================

* ARIA 테스트([3d5658e](https://github.com/jzaefferer/jquery-validation/commit/3d5658e9e4825fab27198c256beed86f0bd12577)) 추가
* es-AR 지역화 메시지를 추가합니다. ([7b30beb](https://github.com/jzaefferer/jquery-validation/commit/7b30beb8ebd218c38a55d26a63d529e16035c7a2))
* 누락된 점을 'es' 및 'es_AR' 메시지에 추가합니다. ([a2a653c](https://github.com/jzaefferer/jquery-validation/commit/a2a653cb68926ca034b4b09d742d275db934d040))
* 인도네시아(ID) 지역화가 추가됨([1d348bd](https://github.com/jzaefferer/jquery-validation/commit/1d348bdcb65807c71da8d0bfc13a97663631cd3a))
* NIF, NIE 및 CIF 스페인어 문서 번호 유효성 검사가 추가됨([#830](https://github.com/jzaefferer/jquery-validation/issues/830), [317c20f](https://github.com/jzaefferer/jquery-validation/commit/317c20fa9bb772770bb9b70d46c7081d7cfc6545))
* 현재 폼을 원격 ajax 요청의 컨텍스트에 추가함([0a18ae6](https://github.com/jzaefferer/jquery-validation/commit/0a18ae65b9b6d877e3d15650a5c2617a9d2b11d5))
* 추가: 후행 공백 자르기 IBAN 메서드 업데이트 ([#970](https://github.com/jzaefferer/jquery-validation/issues/970)하십시오 [347b04a](https://github.com/jzaefferer/jquery-validation/commit/347b04a7d4e798227405246a5de3fc57451d52e1))
* BIC 메서드: RegEx를 개선 {1} 항상 중복 됩니다. gh-744를 마감합니다([5cad6b4](https://github.com/jzaefferer/jquery-validation/commit/5cad6b493575e8a9a82470d17e0900c881130873)).
* Bower: 패키지 등록에 Bower.json 추가 ([e86ccb0](https://github.com/jzaefferer/jquery-validation/commit/e86ccb06e301613172d472cf15dd4011ff71b398))
* jQuery.noConflict과의 호환성을 위해 'jQuery'에 대한 달러 참조를 변경합니다. gh-754를 마감합니다([2049afe](https://github.com/jzaefferer/jquery-validation/commit/2049afe46c1be7b3b89b1d9f0690f5bebf4fbf68)).
* Core: 오류 목록 항목에 "메서드" 필드 추가 ([89a15c7](https://github.com/jzaefferer/jquery-validation/commit/89a15c7a4b17fa2caaf4ff817f09b04c094c3884))
* Core: Data-msg 특성을 통해 일반 메시지에 대 한 지원이 추가 되었습니다 ([5bebaa5](https://github.com/jzaefferer/jquery-validation/commit/5bebaa5c55c73f457c0e0181ec4e3b0c409e2a9d))
* Core: 특성 값이 0을 허용 (예: min = '0') ([#854](https://github.com/jzaefferer/jquery-validation/issues/854)하십시오 [9dc0d1d](https://github.com/jzaefferer/jquery-validation/commit/9dc0d1dd946b2c6178991fb16df0223c76162579))
* Core: 사용 안 함 $.format 사용 되지 않음 ([#755](https://github.com/jzaefferer/jquery-validation/issues/755)하십시오 [bf3b350](https://github.com/jzaefferer/jquery-validation/commit/bf3b3509140ea8ab5d83d3ec58fd9f1d7822efc5))
* Core: 다중 오류 클래스에 대 한 지원 수정 ([c1f0baf](https://github.com/jzaefferer/jquery-validation/commit/c1f0baf36c21ca175bbc05fb9345e5b44b094821))
* Core: 요소에서 이벤트 무시 무시 ([#700](https://github.com/jzaefferer/jquery-validation/issues/700)하십시오 [a864211](https://github.com/jzaefferer/jquery-validation/commit/a86421131ea69786ee9e0d23a68a54a7658ccdbf))
* Core: ElementValue 메서드 개선 ([6c041ed](https://github.com/jzaefferer/jquery-validation/commit/6c041edd21af1425d12d06cdd1e6e32a78263e82))
* Core: Make element() handle ignored elements properly. ([3f464a8](https://github.com/jzaefferer/jquery-validation/commit/3f464a8da49dbb0e4881ada04165668e4a63cecb))
* Core: W3C HTML5 사양 스타일으로 구문 분석 하는 dataRules 스위치 ([460fd22](https://github.com/jzaefferer/jquery-validation/commit/460fd22b6c84a74c825ce1fa860c0a9da20b56bb))
* Core: 선택 사항에 success 트리거 이지만 다른 성공적인 유효성 검사기 ([#851](https://github.com/jzaefferer/jquery-validation/issues/851)하십시오 [f93e1de](https://github.com/jzaefferer/jquery-validation/commit/f93e1deb48ec8b3a8a54e946a37db2de42d3aa2a))
* Core: 대신 일반 요소를 사용 하 여 래핑 해제 요소를 다시 ([03cd4c9](https://github.com/jzaefferer/jquery-validation/commit/03cd4c93069674db5415a0bf174a5870da47e5d2))
* Core: 원격 유효성 검사가 마지막에 실행되는지 확인([#711](https://github.com/jzaefferer/jquery-validation/issues/711), [ad91b6f](https://github.com/jzaefferer/jquery-validation/commit/ad91b6f388b7fdfb03b74e78554cbab9fd8fca6f))
* 데모: 여러 부분 데모에서 올바른 옵션을 사용 합니다. ([#1025](https://github.com/jzaefferer/jquery-validation/issues/1025), [070edc7](https://github.com/jzaefferer/jquery-validation/commit/070edc7be4de564cb74cfa9ee4e3f40b6b70b76f))
* 추가 메서드에서 $/jQuery 사용법을 수정합니다. #839 수정([#839](https://github.com/jzaefferer/jquery-validation/issues/839), [59bc899](https://github.com/jzaefferer/jquery-validation/commit/59bc899e4586255a4251903712e813c21d25b3e1))
* 중국어 번역 개선([1a0bfe3](https://github.com/jzaefferer/jquery-validation/commit/1a0bfe32b16f8912ddb57388882aa880fab04ffe))
* 초기 ARIA-Required 구현([bf3cfb2](https://github.com/jzaefferer/jquery-validation/commit/bf3cfb234ede2891d3f7e19df02894797dd7ba5e))
* 지역화: 확장에 대한 수락 값을 변경합니다. #771을 수정하고 gh-793을 마감합니다. ([#771](https://github.com/jzaefferer/jquery-validation/issues/771), [12edec6](https://github.com/jzaefferer/jquery-validation/commit/12edec66eb30dc7e86756222d455d49b34016f65))
* 메시지: 아이슬란드어 지역화 추가 ([dc88575](https://github.com/jzaefferer/jquery-validation/commit/dc885753c8872044b0eaa1713cecd94c19d4c73d))
* 메시지: 누락 된 점을 'bg', 'fr' 및 'sr' 메시지를 추가 합니다. ([adbc636](https://github.com/jzaefferer/jquery-validation/commit/adbc6361c377bf6b74c35df9782479b1115fbad7))
* 메시지: Messages_sr_lat.js 만들기 ([f2f9007](https://github.com/jzaefferer/jquery-validation/commit/f2f90076518014d98495c2a9afb9a35d45d184e6))
* 메시지: Messages_tj.js ([de830b3](https://github.com/jzaefferer/jquery-validation/commit/de830b3fd8689a7384656c17565ee92c2878d8a5))
* 메시지: Sr_lat 번역 수정, 누락 된 공간 추가 ([880ba1c](https://github.com/jzaefferer/jquery-validation/commit/880ba1ca545903a41d8c5332fc4038a7e9a580bd))
* 메시지: Messages_sr.js 업데이트, 누락 된 공간 수정 ([10313f4](https://github.com/jzaefferer/jquery-validation/commit/10313f418c18ea75f385248468c2d3600f136cfb))
* 메서드: 통화에 대 한 추가 메서드 추가 ([1a981b4](https://github.com/jzaefferer/jquery-validation/commit/1a981b440346620964c87ebdd0fa03246348390e))
* 메서드: StripHTML의 문장 부호 제거에 따옴표를 추가 ([aa0d624](https://github.com/jzaefferer/jquery-validation/commit/aa0d6241c3ea04663edc1e45ed6e6134630bdd2f))
* 메서드: DateITA 메서드 수정, 일광 절약 시간 오류 방지 ([279b932](https://github.com/jzaefferer/jquery-validation/commit/279b932c1267b7238e6652880b7846ba3bbd2084))
* 메서드: 지역화 된 칠레 어 문화권 (ES-CL)에 대 한 메서드 ([cf36b93](https://github.com/jzaefferer/jquery-validation/commit/cf36b933499e435196d951401221d533a4811810))
* 메서드: HTML5 regex를 사용 하 여, email2 메서드 제거 하도록 메일 업데이트 ([#828](https://github.com/jzaefferer/jquery-validation/issues/828)하십시오 [dd162ae](https://github.com/jzaefferer/jquery-validation/commit/dd162ae360639f73edd2dcf7a256710b2f5a4e64))
* 패턴 메서드: HTML5 구현 기호가 포함 하지 않으므로, 구분 기호를 제거 합니다. ([37992c1](https://github.com/jzaefferer/jquery-validation/commit/37992c1c9e2e0be8b315ccccc2acb74863439d3e))
* 길이 검사를 포함하도록 신용 카드 유효성 검사기 제한 gh-772를 마감합니다([f5f47c5](https://github.com/jzaefferer/jquery-validation/commit/f5f47c5c661da5b0c0c6d59d169e82230928a804)).
* messages_ko.js를 업데이트하고 gh-715를 마감합니다([5da3085](https://github.com/jzaefferer/jquery-validation/commit/5da3085ff02e0e6ecc955a8bfc3bb9a8d220581b)).
* messages_pt_BR.js를 업데이트합니다. gh-782를 마감합니다([4bf813b](https://github.com/jzaefferer/jquery-validation/commit/4bf813b751ce34fac3c04eaa2e80f75da3461124)).
* 새 접두사를 승인하도록 phonesUK 및 mobileUK를 업데이트합니다. gh-750을 마감합니다([d447b41](https://github.com/jzaefferer/jquery-validation/commit/d447b41b830dee984be21d8281ec7b87a852001d)).
* 9자리 우편 번호를 확인합니다. gh-726을 마감합니다([165005d](https://github.com/jzaefferer/jquery-validation/commit/165005d4b5780e22d13d13189d107940c622a76f)).
* phoneUS: N11 제외 사항을 추가 합니다. gh-861을 마감합니다([519bbc6](https://github.com/jzaefferer/jquery-validation/commit/519bbc656bcb26e8aae5166d7b2e000014e0d12a)).
* resetForm은 aria-invalid 값을 지워야 합니다([4f8a631](https://github.com/jzaefferer/jquery-validation/commit/4f8a631cbe84f496ec66260ada52db2aa0bb3733)).
* valid(): 모든 요소를 확인 합니다. #791 수정 - valid()는 첫 번째(유효하지 않은) 요소만 유효성을 검사합니다([#791](https://github.com/jzaefferer/jquery-validation/issues/791), [6f26803](https://github.com/jzaefferer/jquery-validation/commit/6f268031afaf4e155424ee74dd11f6c47fbb8553)).

<a name="1111--2013-03-22"></a>1.11.1 / 2013-03-22
==================

  * 또한 범위 메서드의 매개 변수를 숫자로 변환하는 방식으로 되돌립니다. gh-702를 마감합니다.
  * PHP의 사용 대부분을 mockjax 처리기로 바꿉니다. 일부 데모를 정리하고 최신 masked-input 플러그 인으로 업데이트합니다. captcha 데모를 PHP에 유지합니다. #662를 수정합니다.
  * milk 데모에서 인라인 코드 강조 표시를 제거합니다. 소스 보기는 정상적으로 작동합니다.
  * jQuery 생성자로 전달하기 전에 템플릿 콘텐츠에서 공백을 잘라 내어 dynamic-totals 데모를 수정합니다.
  * 최소/최대 유효성 검사를 수정합니다. gh-666을 마감합니다. #648을 수정합니다.
  * 규칙으로 제공되며 규칙을 통해 업데이트된 후에 예외를 발생하는 '메시지'를 수정했습니다. gh-670을 마감하고 #624를 수정합니다.
  * 한국어(ko) 지역화를 추가합니다. gh-671을 마감합니다.
  * 잘못된 우편 번호를 더 많이 필터링하도록 영국 우편 번호 메서드를 개선했습니다. # 682를 마감합니다.
  * messages_sv.js를 업데이트합니다. # 683을 마감합니다.
  * 프로젝트 웹 사이트에 대한 grunt 링크를 변경합니다. # 684를 마감합니다.
  * 다른 모든 메서드가 필드에 적용된 후 원격 메서드를 목록 아래로 이동하여 마지막으로 실행합니다. #679를 수정합니다.
  * plugin.json 설명을 업데이트합니다. 'validate' 단어를 포함해야 합니다.
  * 철자 오류를 수정합니다.
  * 자체 경로를 사용하도록 jQuery 로더를 수정합니다. 중첩된 데모를 수정합니다.
  * 노드 모듈 'phantomjs'를 통해 설치할 경우 PhantomJS 1.8을 사용하도록 grunt-contrib-qunit을 업데이트합니다.
  * valid()가 0 또는 1이 아닌 부울을 반환하도록 합니다. #109 수정 - valid()는 부울 값을 반환하지 않습니다.

<a name="1110--2013-02-04"></a>1.11.0 / 2013-02-04
==================

  * `min`, `max` 및 `range` 규칙의 개수로 지우기를 제거합니다. #455를 수정합니다. gh-528을 마감합니다.
  * 기존 레이블 업데이트 - #430을 수정하고 gh-436을 마감합니다.
  * 그룹 보간을 방지하도록 $.validator.format을 수정합니다. IE8/9 이상에서는 -bash를 일치하는 항목으로 바꿉니다. #614를 수정합니다.
  * MIME 형식 regex를 수정합니다.
  * 플러그 인 매니페스트 및 업데이트 헤더를 MIT 라이선스에만 추가하고, 불필요한 이중 라이선스(예: jQuery)를 삭제합니다.
  * 히브리어 메시지: 제거 된 점을 수정 gh-568 문장 끝
  * require_from_group 유효성 검사를 위한 프랑스어 번역 gh-573을 수정합니다.
  * 그룹이 배열 또는 문자열이 되도록 허용합니다. #479를 수정합니다.
  * 여러 MIME 형식을 갖는 공백을 제거했습니다.
  * 일부 날짜 유효성 검사, JS 구문 오류를 수정합니다.
  * 메타데이터 플러그 인에 대한 지원을 제거하고 data-rule- 및 data-msg-(907467e8에 추가됨) 속성으로 바꿉니다.
  * sftp가 유효한 url-pattern으로서 추가되었습니다.
  * Malay(my) 지역화를 추가합니다.
  * localization/messages_hu.js를 업데이트합니다.
  * focusin/focusout polyfill을 제거합니다. #542 수정 - jquery.validate를 포함하면 IE9의 focusin 및 focusout 이벤트를 방해합니다.
  * 지역화: 핀란드어 번역에서 오타가 수정된 됨
  * 유효한 상태에서 유효하지 않은 상태가 될 때 잘못됨 아이콘을 표시하도록 RTM 데모를 수정합니다.
  * 입력이 너무 빠르게 수행될 경우 ajax 호출이 진행되지 못하게 하는 원격 함수의 초기 반환이 수정되었습니다. 원격 유효성 검사가 항상 최신 값의 유효성을 검사하는지 확인합니다.
  * #244에 대한 수정을 실행 취소합니다. #521 수정 - 텍스트가 필드에 입력되는 즉시 메일 유효성 검사가 실행됩니다.

<a name="1100--2012-09-07"></a>1.10.0 / 2012-09-07
===================

  * 커뮤니티 피드백을 기준으로 nowhitespace, phoneUS, phoneUK 및 mobileUK의 프랑스어 문자열을 수정했습니다.
  * 표준 ISO_3166-1(http://en.wikipedia.org/wiki/ISO_3166-1))에 따라 language_REGION의 파일 이름을 바꿉니다. 대만어의 경우 언어는 중국어(zh)이고 지역은 대만(TW)입니다.
  * RegEx 패턴(특히 영국 전화 번호)을 최적화합니다.
  * 각 파일에 대해 언어 이름을 추가하고, 에스토니아어, 조지아어, 우크라이나어 및 중국어(http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes))에 대한 표준 ISO 639에 따라 언어 코드 이름을 바꿉니다.
  * 크로아티아어(HR) 지역화를 추가했습니다.
  * 기존 프랑스어 번역이 편집되고 추가 메서드에 대한 프랑스어 번역이 추가되었습니다.
  * 데이터 특성에서 사용자 지정 오류 메시지를 지정하기 위한 변경 내용이 병합되었습니다.
  * 새 번호에 대한 영국 휴대폰 번호 regex가 업데이트되었습니다. #154를 수정합니다.
  * 테스트에 성공한 호출에 요소를 추가합니다. #60을 수정합니다.
  * 시간 추가 메서드에 대한 regex를 수정했습니다. #131을 수정합니다.
  * 이제 resetForm은 양식 요소에서 이전 previousValue를 지웁니다. #312를 수정합니다.
  * elementValue를 사용하도록 require_from_group 및 changed require_from_group에 확인란 테스트를 추가했습니다. #359를 수정합니다.
  * jQuery 1.5.2+에서 dataFilter 응답 문제가 수정되었습니다. #405를 수정합니다.
  * jQuery 모바일 데모가 추가되었습니다. #249를 수정합니다.
  * 정확성을 위해 findByName의 최적화를 복원합니다. #82 수정 - IE7의 $.validator.prototype.findByName 중단
  * 미국 우편 번호 지원 및 테스트를 추가했습니다. #90을 수정합니다.
  * keyup에서 lastElement를 lastActive로 변경하고, 탭 또는 빈 요소에 대한 유효성 검사를 건너뜁니다. #244를 수정합니다.
  * stripHtml에서 숫자 제거가 제거되었습니다. #2를 수정합니다.
  * 유효하지 않음/유효함 원격 유효성 검사에서 유효하지 않음 개수를 수정했습니다. #286을 수정합니다.
  * file_input에 대한 링크를 데모 인덱스에 추가합니다.
  * 이전 accept 메서드를 확장 additional-method로 이동하고, 표준 브라우저 MIME 형식 필터링을 처리하도록 새 accept 메서드를 추가했습니다. #287을 수정하고 #369를 대체합니다.
  * onfocusout이 false로 설정된 경우 blur 이벤트를 사용하지 않도록 설정합니다. 테스트를 추가했습니다.
  * 라디오 단추 및 확인란에 대한 값 문제를 수정했습니다. #363을 수정합니다.
  * rangeWords에 대한 테스트를 추가하고 메서드의 regex 및 범위를 수정했습니다. #308을 수정합니다.
  * TinyMCE 데모를 수정하고 데모 페이지에 링크를 추가했습니다. #382를 수정합니다.
  * min/max에 대한 지역화 메시지를 변경했습니다. #273을 수정합니다.
  * 기본 빈 형식 특성의 문제를 수정하기 위해 텍스트 입력 형식에 대한 의사 선택기를 추가했습니다. 테스트 및 일부 테스트 태그를 추가했습니다. #217을 수정합니다.
  * dynamic-totals 데모에 대한 대리자 버그를 수정했습니다. #51을 수정합니다.
  * 영숫자 유효성 검사기의 잘못된 메시지를 수정합니다.
  * 필수 특성에서 올바르지 않은 false 검사를 제거했습니다.
  * 비 html5 브라우저의 필수 특성 수정 사항입니다. #301을 수정합니다.
  * “require_from_group” 및 “skip_or_fill_minimum” 메서드를 추가했습니다.
  * 스웨덴어에 대해 올바른 iso 코드를 사용합니다.
  * HTML5 doctype을 사용하도록 데모 HTML 파일을 업데이트했습니다.
  * 선행 0이 없는 10진수에 대한 regex 문제를 수정했습니다. 새 메서드 테스트를 추가했습니다. #41을 수정합니다.
  * 문자열 값만 정규화하는(다중 선택의 배열 값은 그대로 유지) elementValue 메서드를 도입합니다. #116을 수정합니다.
  * 동적으로 추가된 제출 단추를 지원하고 테스트 사례를 업데이트했습니다. validateDelegate를 사용합니다. PR #9의 코드입니다.
  * 테스트 설비에서 잘못된 큰따옴표를 수정합니다.
  * 상한을 제외하지 않고 포함하도록 maxWords 메서드를 수정합니다. #284를 수정합니다.
  * 독일어 범위 유효성 검사기 메시지에서 문법 오류를 수정했습니다. #315를 수정합니다.
  * errorClass 옵션의 여러 클래스 이름 처리를 수정했습니다. Max Lynch가 테스트했습니다. #280을 수정합니다.
  * jQuery.format 사용법을 수정합니다. $.validator.format이어야 합니다. #329를 수정합니다.
  * '모든' 영국 전화 번호 + UK 우편 번호에 대한 메서드
  * 패턴 메서드: 문자열 매개 변수를 RegExp 변환 합니다. 문제 #223을 수정합니다.
  * 독일어 지역화 파일의 문법 오류
  * 메시지의 에스토니아어 지역화를 추가했습니다.
  * themerollered 데모의 도구 설명 처리를 개선했습니다.
  * qSA 충족을 위해 형식 특성 없이 입력 필드에 type="text"를 추가합니다.
  * 도구 팁을 사용하여 오류를 오버레이로 표시하도록 themerollered 데모를 업데이트합니다.
  * 최신 jQuery UI(및 최신 jQuery 버전)를 사용하도록 themerollered 데모를 업데이트합니다. 페이지 로드 속도를 높이도록 코드를 이동합니다.
  * 일본어로 잘못 작성된 최소 오류 메시지를 수정했습니다.
  * 양식 플러그 인을 최신 버전으로 업데이트합니다. ajaxSubmit 데모를 강화합니다.
  * 지역화된 메서드로 전환하고 남은 classRuleSettings의 dateDE 및 numberDE 메서드를 삭제합니다.
  * 제출 이벤트를 submitHandler 콜백으로 전달
  * #219 수정 - dependency-callback 또는 dependency-expression을 사용하여 요소에 대한 valid()를 수정합니다.
  * 현재 릴리스만 압축되도록 dist dir을 제거하여 빌드를 개선합니다.

<a name="190"></a>1.9.0
---
* 바스크어(EU) 지역화를 추가했습니다.
* 슬로베니아어(SL) 지역화를 추가했습니다.
* 문제 #127 수정 - 핀란드어 번역에 ; 대신 :가 있습니다.
* 러시아어 지역화를 수정했습니다. 구문 문제가 최소화되었습니다.
* HTML5 입력 형식에 대한 지원을 추가했습니다. #97을 수정합니다.
* 양식에서 novalidate 특성을 설정하고 형식 특성을 읽어 HTML5 지원 기능을 개선했습니다.
* showLabel()을 수정하여 오류 요소에서 모든 클래스를 제거했습니다. settings.validClass만 제거합니다. #151을 수정합니다.
* 임의의 정규식을 기준으로 유효성을 검사하기 위해 additional-methods에 'pattern'을 추가했습니다.
* 끝에서 점을 허용하지 않도록(RFC에서 유효하지만 여기서는 원치 않음) email 메서드를 개선했습니다. #143을 수정합니다.
* 스웨덴어 및 노르웨이어 번역을 수정했으며 min/max 메시지가 전환되었습니다. #181을 수정합니다.
* #184 수정 - resetForm:은 lastElement를 설정 해제해야 합니다.
* #71 수정 - 기존 time 메서드를 개선하고 12시간 am/pm 시간 형식에 대한 time12h 메서드를 추가합니다.
* #177 수정 - 단일 라디오 또는 확인란 입력의 유효성 검사를 수정합니다.
* #189 수정 - 이제 :hidden 요소가 기본적으로 무시됩니다.
* #194 수정 - 특성이 실패하면 필요합니다. jQuery가 1.6이 이상이면 .attr 대신 .prop을 사용합니다.
* #47, #39, #32 수정 - 신용 카드 번호에 대시뿐만 아니라 공백이 포함되도록 허용했습니다(공백은 일반적으로 사용자가 입력함).

<a name="181"></a>1.8.1
---
* 태국어(TH) 지역화를 추가했습니다. #85를 수정합니다.
* 베트남어(VI) 지역화를 추가했습니다. Ngoc에 감사드립니다.
* 문제 #78을 수정했습니다. 오류/유효 스타일이 유효성 검사가 필요한 동일한 그룹의 모든 라디오 단추에 적용됩니다.
* form.elements는 jQuery 1.6에서는 더 이상 지원되지 않으므로 사용하지 마세요. 결함이 많습니다(IE6-8: form.elements === form).

<a name="180"></a>1.8.0
---
* NL 지역화를 개선했습니다(http://plugins.jquery.com/node/14120)).
* 조지아어(GE) 지역화를 추가했습니다. Avtandil Kikabidze에게 감사드립니다.
* 세르비아어(SR) 지역화를 추가했습니다. Aleksandar Milovac에게 감사드립니다.
* ipv4 및 ipv6를 추가 메서드에 추가했습니다. Natal Ngétal에게 감사드립니다.
* 일본어(JA) 지역화를 추가했습니다. Bryan Meyerovich에게 감사드립니다.
* 카탈로니아어(CA) 지역화를 추가했습니다. Xavier de Pedro에게 감사드립니다.
* for-in 루프 내에서 누락된 var 문을 수정했습니다.
* 잘못된 형식의 메시지에 문제가 발생한 경우 원격 유효성 검사에 대한 수정 사항입니다(https://github.com/jzaefferer/jquery-validation/issues/11)).
* 이전 버전과의 호환성을 유지하면서 jQuery 1.5.1과의 호환성을 유지하기 위한 버그 수정 사항입니다.

<a name="17"></a>1.7
---
* 리투아니아어(LT) 지역화를 추가했습니다.
* 그리스어(EL) 지역화를 추가했습니다(http://plugins.jquery.com/node/12319)).
* 라트비아어(LV) 지역화를 추가했습니다(http://plugins.jquery.com/node/12349)).
* 히브리어(HE) 지역화를 추가했습니다(http://plugins.jquery.com/node/12039)).
* 스페인어(ES) 지역화를 수정했습니다(http://plugins.jquery.com/node/12696)).
* jQuery UI themerolled 데모를 추가했습니다.
* cmxform.js를 제거했습니다.
* 4개의 누락된 세미콜론을 수정했습니다(http://plugins.jquery.com/node/12639)).
* additional-methods.js의 phone-method 이름을 phoneUS로 바꾸었습니다.
* phoneUK 및 mobileUK 메서드를 additional-methods.js에 추가했습니다(http://plugins.jquery.com/node/12359)).
* 단일 요소에서 rules-method를 사용할 때 여러 양식이 수정되지 않도록 옵션을 자세히 확장합니다(http://plugins.jquery.com/node/12411)).
* 이전 버전과의 호환성을 유지하면서 jQuery 1.4.2와의 호환성을 유지하기 위한 버그 수정 사항입니다.

<a name="16"></a>1.6
---
* 아랍어(AR), 포르투갈어(PTPT), 페르시아어(FA), 핀란드어(FI) 및 불가리아어(BR) 지역화를 추가했습니다.
* 스웨덴어(SE) 지역화를 업데이트했습니다(일부 누락된 html iso 문자).
* 메시지 인수에 대해 빈 문자열 및 정의되지 않은 문자를 제대로 처리하도록 $.validator.addMethod를 수정했습니다.
* 2개의 잘못된 전역 변수를 수정했습니다.
* 개수를 세기 전에 html을 삭제하도록 min/max/rangeWords(additional-methods.js)를 개선했습니다. 서식 있는 텍스트 편집기에서 단어를 계산할 때 좋습니다.
* DE, NL 및 PT에 대한 지역화된 메서드를 추가했습니다. dateDE 및 numberDE 메서드를 제거합니다(대신 date 및 number 메서드와 함께 messages_de.js 및 methods_de.js 사용).
* 원격 양식 제출 동기화를 수정했습니다. Matas Petrikas에게 감사드립니다.
* 대화형 선택 유효성 검사를 개선했습니다. 이제 클릭할 때도 유효성 검사가 수행됩니다(옵션 또는 선택을 통해 브라우저 간 불일치 확인). Safari에서는 작동하지 않으며 선택 요소에 대해 click 이벤트가 트리거되지 않습니다. http://plugins.jquery.com/node/11520을 수정합니다.
* 최신 양식 플러그 인(2.36)을 업데이트하고 http://plugins.jquery.com/node/11487을 수정했습니다.
* 대상이 변경될 때 equalTo 대상의 blur 이벤트에 바인딩하여 유효성 검사를 다시 수행합니다. http://plugins.jquery.com/node/11450을 수정합니다.
* 선택 유효성 검사가 단순화되었으며 jQuery의 val() 메서드로 위임되어 선택 값을 가져옵니다. http://plugins.jquery.com/node/11239를 수정해야 합니다.
* 숫자에 대한 기본 메시지를 수정했습니다(http://plugins.jquery.com/node/9853)).
* 캐시된 원격 메시지에 발생한 문제를 해결했습니다(http://plugins.jquery.com/node/11029 및 http://plugins.jquery.com/node/9351)).
* additional-methods.js의 누락된 세미콜론을 수정했습니다(http://plugins.jquery.com/node/9233)).
* 메시지의 대체 매개 변수 자동 검색을 추가했으며 형식 함수를 제공할 필요가 없어졌습니다(http://plugins.jquery.com/node/11195)).
* Sizzle로 인한 :filled/:blank 문제를 수정했습니다(http://plugins.jquery.com/node/11144)).
* additional-methods.js에 정수 메서드를 추가했습니다(http://plugins.jquery.com/node/9612)).
* for-attribute에 이스케이프로 처리해야만 선택기 내에서 유효해지는 문자가 포함되는 errorsFor 메서드를 수정했습니다(http://plugins.jquery.com/node/9611)).

<a name="155"></a>1.5.5
---
* http://plugins.jquery.com/node/8659에 대한 수정
* messages_cs.js의 후행 쉼표를 수정했습니다.

<a name="154"></a>1.5.4
---
* 원격 메서드 버그를 수정했습니다(http://plugins.jquery.com/node/8658)).

<a name="153"></a>1.5.3
---
* wrapper-option과 관련된 버그를 수정했습니다. wrapper-option과 일치하는 모든 ancestor-elements가 선택됩니다(http://plugins.jquery.com/node/7624)).
* 최신 jQuery UI Accordion을 사용하도록 다중 파트 데모를 업데이트했습니다.
* additionalMethods.js에 dateNL 및 time 메서드를 추가했습니다.
* 중국어 번체(대만, tw) 및 카자흐스탄어(KK) 지역화를 추가했습니다.
* jQuery.format(이전 String.format)을 jQuery.validator.format으로 이동했습니다. jQuery.format을 더 이상 사용되지 않으며 1.6에서 제거됩니다(자세한 내용은 http://code.google.com/p/jquery-utils/issues/detail?id=15 참조).
* messages_pl.js 및 messages_ptbr.js를 정리했습니다(1.4에서 제거된 max/min/rangeValue에 대한 정의된 메시지는 계속 유지됨).
* 여러 요소의 valid-plugin-method에서 결함 있는 부울 논리를 수정했습니다. 이제 모든 요소가 boolean-true 결과에 대해 유효해야 합니다(http://plugins.jquery.com/node/8481)).
* $..Validator.addmethod 개선: 정의 되지 않은 세 번째 메시지-인수를 기존 메시지 (덮어쓰지 않습니다. http://plugins.jquery.com/node/8443)
* SubmitHandler 옵션 개선: 이벤트 제출 단추 캡처되고는 제출 단추 클릭 submitHandler를 호출 하기 전에 폼에 삽입 되며 그 이후에; 제거를 사용 하면 제출 단추 그대로 (유지 http://plugins.jquery.com/node/7183#comment-3585)
* 옵션 validClass와 기본값 "valid"(유효성 검사 후 해당 클래스를 모든 유효한 요소에 추가)를 추가했습니다(http://dev.jquery.com/ticket/2205)).
* additionalMethods.js에 creditcardtypes 메서드를 추가했습니다. 테스트가 포함됩니다(http://dev.jquery.com/ticket/3635)를 통해).
* 서버 쪽 메시지가 유효한 경우 문자열 또는 true로 허용하고, 유효하지 않은 경우 클라이언트 쪽 정의 메시지를 사용하여 false로 나타내도록 원격 메서드를 개선했습니다(http://dev.jquery.com/ticket/3807)).
* 또한 Drupal 스타일의 쉼표로 구분된 값 목록도 수락하도록 accept 메서드를 개선했습니다(http://plugins.jquery.com/node/8580)).

<a name="152"></a>1.5.2
---
* maxWords, minWords 및 rangeWords에 대한 additional-methods.js의 메시지를 $.format에 대한 호출을 포함하도록 수정했습니다.
* 메서드에 전달된 값을 jQuery의 val()과 동일하게 캐리지 리턴(~)을 제외하도록 수정했습니다.
* 슬로바키아어(sk) 지역화를 추가했습니다.
* jQuery UI 탭과 통합하기 위한 데모를 추가했습니다.
* 탭 데모에 selects-grouping 예제를 추가했습니다(두 번째 탭, 생년월일 필드 참조).

<a name="151"></a>1.5.1
---
* invalid-form 이벤트를 바인딩하는 대신 invalidHandler 옵션을 사용하도록 marketo 데모를 업데이트했습니다.
* TinyMCE 통합 예제를 추가했습니다.
* 우크라이나어(ua) 지역화를 추가했습니다.
* 잘린 값에 작동하도록 길이 유효성 검사를 수정했습니다(유효성 검사 이전에 일반 잘라내기가 제거되는 1.5 버전에서 재발).
* 1.2.6 및 1.3과의 호환성을 위한 다양한 소규모 수정 사항

<a name="15"></a>1.5
---
* 기본 데모가 개선되어 암호 변경 후 암호 확인 필드의 유효성이 검사됩니다.
* 자르지 않은 입력 값을 유효성 검사 메서드의 첫 번째 매개 변수로 전달하도록 기본 유효성 검사를 수정했습니다. 그에 따라 변경되어야 하며 잘라내기에 의존하는 기존 사용자 지정 메서드가 위반됩니다.
* 노르웨이어(no), 이탈리아어(it), 헝가리어(ro) 및 루마니아어(ro) 지역화가 추가되었습니다.
* # 3195: 스웨덴어 지역화의 2 가지 결함
* # 3503 수정된: 메시지 속성을 수락 하도록 규칙을 확장 합니다: 지정 하는 데 규칙을 통해 요소에 사용자 지정 메시지 추가 ("add", {메시지: {필요: "Required! " } });
* # 3356 수정된: 메타 옵션을 사용할 때 # 2908에서 재발
* # 3370: Google 툴바의;를 사용 하 여 문제를 방지할 수 있습니다를 title 특성에서 메시지 읽기를 건너뛰도록 설정 추가 ignoreTitle 옵션 기본값은 호환성을 위해 false
* # 3516 수정된: 원격 유효성 검사 관련 된 경우에 트리거 invalid-form 이벤트
* invalidHandler 옵션을 바인딩할 바로 가기로 추가했습니다("invalid-form", function() {}).
* ajaxSubmit-integration-demo에서 표시기를 로드할 때 나타나는 Safari 문제를 수정했습니다(본문에 먼저 추가된 후 숨김).
* 신용 카드 유효성 검사를 위한 테스트를 추가하고 기본 메시지를 개선했습니다.
* 원격 유효성 검사를 개선하여 매개 변수로 $.ajax를 통과하기 위한 옵션을 수락합니다($.ajax가 지원하는 모든 항목과 URL 속성을 포함하는 URL 문자열 또는 옵션).

<a name="14"></a>1.4
---
* #2931 수정: 문서 순서에서 요소가 유효한지 검사하고 type=image inputs를 무시합니다.
* $ 및 jQuery 변수 사용 방식을 수정했으므로 이제 모든 noConflict 사용 변형 방식과도 완벽하게 호환됩니다.
* #2908을 구현하여 메타데이터 ala class="{required:true,messages:{required:'required field'}}"를 통해 사용자 지정 메시지를 사용 가능으로 설정하고 demo/custom-messages-metadata-demo.html을 추가했습니다.
* 더 이상 사용되지 않는 메서드, minValue (min), maxValue (max), rangeValue (rangevalue), minLength (minlength), maxLength (maxlength), rangeLength (rangelength)를 제거했습니다.
* #2215 재발 문제 해결된: 것은 아닙니다 현재 요소에 대해서만 unhighlight 호출
* #2989를 구현하여 이미지 단추가 유효성 검사를 취소할 수 있도록 합니다.
* IE가 maxlength=0에 대해 유효성 검사를 잘못 수행하는 문제를 수정했습니다.
* 체코어(cs) 지역화를 추가했습니다.
* validator.resetForm()에서 validator.submitted를 재설정하여 필요한 경우 전체 재설정을 사용하도록 합니다.
* #3035를 수정하여 규칙을 읽을 때 모든 오류 특성(0, 정의되지 않음, 빈 문자열)을 건너뛰고, maxlength 해결 방법의 일부를 제거했습니다(0의 경우).
* 네덜란드어(nl) 지역화를 추가했습니다(#3201).

<a name="13"></a>1.3
---
* invalid-form 이벤트를 수정하여 이제 양식이 유효하지 않을 때만 트리거됩니다.
* 스페인어(es), 러시아어(ru), 포르투갈 브라질어(ptbr), 터키어(tr) 및 폴란드어(pl) 지역화를 추가했습니다.
* 여러 특성의 추가 및 제거를 용이하게 진행하기 위해 removeAttrs 플러그 인을 추가했습니다.
* groups: { arbitraryGroupName: "fieldName1 fieldName2[, fieldNameN" }을 통해 여러 요소에 대해 단일 메시지를 표시할 수 있는 groups 옵션을 추가했습니다.
* rules("add", "method1[, methodN]"/{method1:param[, method_n:param]}) 및 rules("remove"[, "method1[, method_n]")을 통해 (정적) 규칙을 추가 및 제거할 수 있게 rules()가 개선되었습니다.
* rules-option이 개선되어, 메서드의 공백으로 구분된 문자열 목록이 수락됩니다. 예: {birthdate: "required date"}
* 인라인 규칙을 사용 하 여 확인란 그룹 유효성 검사를 수정 합니다. 규칙은 첫 번째 요소에 지정 된,으로 그룹은 이제 유효성이 제대로 검사 클릭
* #2473을 수정하여 boolean-false의 명시적 매개 변수가 있는 모든 규칙을 무시합니다. 예를 들어 required:false는 required를 지정하지 않는 것과 같습니다(지금까지는 required:true로 처리됨).
* 고정된 됩니다 # 2473의 수정 된 패치를 사용 하 여: 다른 규칙이 더 이상; 평가 중지 하지 않는 종속성-불일치를 반환 하는 메서드 성공 선택적 필드에 적용 되지 않습니다 하지만
* 잘린 값을 사용하지 않도록 URL 및 메일 유효성 검사를 수정했습니다.
* 숫자 및 대시만 수락하도록 신용 카드 유효성 검사를 수정했습니다(“asdf”는 유효한 신용 카드 번호가 아님).
* 취소 단추에 대해 단추 및 입력 요소를 둘 다 허용합니다(class="cancel"을 통해).
* # 2215: 및 메시지를 더 이상 visual 의도 하지 않은 요소 및 UI sideeffects 없이 양식의 유효성을 검사 하려면 추출 된 validator.checkForm을 확인 하는 동안 숨기기의 일부로 unhighlight를 호출 하도록 고정된 메시지 표시
* AIR과의 호환성을 위해 함수를 사용하여 사용자 지정 선택기(:blank, :filled, :unchecked)를 다시 작성했습니다.

<a name="121"></a>1.2.1
-----

* 유효성 검사 플러그 인과 대리자 플러그 인을 번들로 묶었습니다. 항상 필요합니다.
* 적절한 동기화를 위해 ajaxQueue 플러그 인의 부분을 포함하도록 원격 유효성 검사를 개선했습니다(추가 플러그 인이 필요하지 않음).
* 0보다 작은 pendingRequest를 방지하기 위해 stopRequest를 수정했습니다.
* jQuery.validator.autoCreateRanges 속성을 추가했습니다(기본값 false). 이를 통해 min/max를 range로, minlength/maxlength를 rangelength로 변환할 수 있습니다. 이 경우 기본적으로 1.2에서 범위를 자동으로 생성하여 발생하는 문제를 수정합니다.
* 필드가 비어 있는 경우(즉, 성공을 트리거하지 않음) 어떤 항목도 강조 표시하지 않도록 optional-methods를 수정했습니다.
* 강조 표시해야 할 항목이 없는 경우에도 do-nothing-callback을 강제로 실행하는 대신 highlight/unhighlight 옵션에 대해 false/null을 허용합니다.
* 요소를 선택하지 않은 validate() 호출을 수정하여 오류를 throw하지 않고 정의되지 않음을 반환하도록 했습니다.
* 데모를 개선하여 메타데이터를 규칙 지정을 위한 클래스/특성으로 바꾸었습니다.
* 원격 유효성 검사에 사용자 지정 메시지가 사용되지 않는 오류를 수정했습니다.
* 도메인 레이블 및 최상위 레이블을 요구하도록 메일 및 URL 유효성 검사를 수정했습니다.
* TLD(실제로 도메인 레이블 요구)를 요구하도록 URL 및 메일 유효성 검사를 수정했습니다. 1.2 버전(TLD은 선택 사항)은 추가 사항에 url2 및 email2로 이동되었습니다.
* IE6/7에서 dynamic-totals 데모를 수정했으며 템플릿을 개선했습니다. 이제 텍스트 영역을 사용하여 다중 행 템플릿 및 문자열 보간을 저장합니다.
* 암호 필드를 선택 항목으로 지정하는 “메일 암호” 링크가 있는 로그인 양식 예제를 추가했습니다.
* 두 필드에 대한 단일 메시지 예제를 사용해서 dynamic-totals 데모를 개선했습니다.

<a name="12"></a>1.2
---

* AJAX-captcha 유효성 검사 예제를 추가했습니다(http://psyrens.com/captcha/) 기반).
* remember-the-milk-demo를 추가했습니다(허용해 주신 RTM 팀에 감사합니다.).
* marketo-demo를 추가했습니다(Glen Lipka에 감사드립니다.).
* ajax-validation에 대한 지원을 추가했습니다. “remote” 메서드를 참조하세요. 서버 쪽은 유효한 요소에 대해 JSON, true를 반환하고 유효하지 않은 요소에 대해 false 또는 문자열을 반환합니다. 문자열은 메시지로 사용됩니다.
* 기본적으로 요소에 대해 errorClass를 설정/해제하고 사용자 지정 강조 표시를 허용하도록 highlight/unhighlight 옵션을 추가했습니다.
* 유효성 검사기 API를 사용하지 않고도 양식 및 필드를 프로그래밍 방식으로 쉽게 검사하기 위한 valid() 플러그 인 메서드를 추가했습니다.
* 요소에 대한 규칙을 읽고 쓰기 위한 rules() 플러그 인 메서드를 추가했습니다(현재 읽기 전용).
* Scott Gonzalez의 참여 덕분에 이메일 메서드에 대한 regex가 바뀌었습니다. http://projects.scottsplayground.com/email_address_validation/을 참조하세요.
* 위임에만 의존하도록 이벤트 아키텍처를 재구성했으며 성능 및 개발자를 위한 사용 편의성을 둘 다 개선했습니다(jquery.delegate.js 필요).
* 모든 메서드에 대한 대화형 예제를 포함하여 인라인에서 http://docs.jquery.com/Plugins/Validation으로 설명서를 이동했습니다.
* validator.refresh()를 제거했습니다. 이제 유효성 검사가 완전히 동적으로 진행됩니다.
* minValue를 min으로, maxValue를 max로, rangeValue를 range로 이름을 바꾸었으며 이전 이름은 더 이상 사용되지 않습니다(1.3에서 제거됨).
* minLength를 minlength로, maxLength를 maxlength로, rangeLength를 rangelength로 이름을 바꾸었으며 이전 이름은 더 이상 사용되지 않습니다(1.3에서 제거됨).
* min + max를 range로, minlength + maxlength를 rangelength로 병합하는 기능을 추가했습니다.
* 동적 규칙 매개 변수에 대한 지원을 추가하여 함수를 매개 변수로 지정할 수 있습니다. 예를 들어 minlength의 경우 요소 유효성을 검사할 때 호출됩니다.
* null 및 빈 문자열을 아무것도 표시하지 않는 메시지로 지정할 수 있습니다(marketo 데모 참조).
* 규칙 재구성: 이제 조합이 지원 규칙 옵션, 메타 데이터, 클래스 (신규) 및 특성 (신규) rules() 대 한 자세한 내용은 참조 하세요.

<a name="112"></a>1.1.2
---

* Scott Gonzalez의 참여 덕분에 URL 메서드에 대한 regex가 바뀌었습니다. http://projects.scottsplayground.com/iri/을 참조하세요.
* 유니코드 문자를 더 잘 처리하도록 email 메서드를 개선했습니다.
* 양식 제출 시만이 아니라 모든 요소가 유효한 경우 숨겨지도록 오류 컨테이너를 수정했습니다.
* String.format을 jQuery.format으로 수정했습니다(jQuery 네임스페이스로 이동).
* 대문자 및 소문자 확장자를 모두 허용하도록 accept 메서드를 수정했습니다.
* 지정된 양식에 대해 하나의 유효성 검사기 인스턴스만 생성하고 항상 해당 인스턴스 1개만 반환하도록 validate() 플러그 인 메서드를 수정했습니다(이벤트를 여러 번 바인딩할 필요가 없음).
* debug-mode 콘솔 로그를 “error”에서 “warn” 수준으로 변경했습니다.

<a name="111"></a>1.1.1
-----

* jQuery 1.1.4 이후에 IE에서 오류 레이블을 생성하지 못하도록 잘못된 XHTML을 수정했습니다.
* 고정 및 향상 된 String.format: 전역 검색 및 바꾸기로 배열 인수 보다 효율적으로 처리
* 양식 요소 대신 상태를 저장하기 위해 validator-object를 사용하도록 cancel-button 처리를 수정했습니다.
* “complex” 이름(예: 대괄호를 포함하는 이름(“list[]”))을 처리하도록 이름 선택기를 수정했습니다.
* 유효성 검증에서 제외할 단추 및 비활성화된 요소를 추가했습니다.
* 새 요소에 처리기를 추가할 수 있도록 새로 고칠 요소 이벤트 처리기를 이동했습니다.
* 긴 최상위 수준 도메인(예: “.travel”)을 허용하도록 메일 유효성 검사를 수정했습니다.
* showErrors()를 valid()에서 form()으로 이동했습니다.
* validator.size() 추가: 현재 오류 수를 반환합니다.
* 해당 메서드에 보다 쉽게 액세스하기 위해 유효성 검사기를 범위로 지정하여 submitHandler를 호출합니다. 예를 들어 errorsFor(Element)를 사용하여 오류 레이블을 찾습니다.
* jQuery 1.1.x 및 1.2.x와 호환됩니다.

<a name="11"></a>1.1
---

* blur, keyup 및 click에 대한 유효성 검사를 추가했습니다(확인란 및 라디오 단추). event-option을 바꿉니다.
* resetForm을 수정했습니다.
* custom-methods-demo를 수정했습니다.

<a name="10"></a>1.0
---

* 구분 기호를 포함하는 올바른 10진수를 확인하도록 number 및 numberDE 메서드를 개선했습니다.
* 규칙이 있는 요소만 확인됩니다(그렇지 않으면 success-option이 모든 요소에 적용됨).
* 신용 카드 번호 메서드를 추가했습니다(Brian Klug의 도움을 받음).
* ignore-option을 추가했습니다. 예를 들면 ignore: "[@type=hidden]"과 같습니다. 이 식을 사용하여 유효성을 검사할 요소를 제외합니다. 기본값: 없음(제출 및 재설정 단추는 항상 무시됨)
* 유연한 String.format 도우미를 제공하여 Functions-as-messages를 개선했습니다.
* Functions를 메시지로 승인하고 runtime-custom-messages를 제공합니다.
* successList의 규칙이 없는 요소의 제외를 수정했습니다.
* custom-method-demo를 수정하고, 경고를 오류 수를 표시하는 메시지로 바꾸었습니다.
* submitHandler를 사용할 때 form-submit-prevention을 수정했습니다.
* 요소 ID가 입력에 오류 레이블을 연결하는 데 여전히 사용되지만(있는 경우) 요소 ID에 대한 종속성을 완전히 제거했습니다. 이를 위해 내부 errorList에 대한 id:message 쌍을 갖는 개체 대신 {name, message, element}를 갖는 배열을 사용했습니다.
* 단순 규칙을 단순 문자열로 지정하기 위한 지원을 추가했습니다. 예를 들어 “required”는 {required: true}와 같습니다.
* 추가 기능: 잘못 된 필드의 부모 요소에 쉽게 레이블/필드 컨테이너 또는 필드에 대 한 레이블 스타일 errorClass를 추가 합니다.
* 기능 추가: focusCleanup - 사용되도록 설정된 경우 유효하지 않은 요소에서 errorClass를 제거하고 요소에 포커스가 놓일 때마다 오류 메시지를 모두 숨깁니다.
* 필드 유효성이 성공적으로 검사되었음을 표시하는 성공 옵션을 추가했습니다.
* Opera select-issue를 수정했습니다(attribute-collision 방지).
* IE에서 숨겨진 요소에 포커스를 둘 때 발생하는 문제를 수정했습니다.
* 클래스 “cancel”이 있는 제출 단추에 대한 유효성 검사를 건너뛰는 기능을 추가했습니다.
* title 특성에 대해 플러그 인 옵션 메시지를 지정하여 Google 툴바의 잠재적 문제를 수정했습니다.
* submitHandler는 실제 제출 이벤트가 처리되었을 때만 호출되며, validator.form()은 유효하지 않은 양식에 대해서만 false를 반환합니다.
* 이제 유효하지 않은 요소에는 제출 시 또는 validator.focusInvalid()를 통해서만 포커스가 놓이므로 focus-on-blur의 모든 문제가 방지됩니다.
* IE6 오류 컨테이너 레이아웃 문제를 해결했습니다.
* errorElement 옵션을 통해 오류 요소를 사용자 지정합니다.
* 폼에서 새 입력을 찾기 위해 validator.refresh()를 추가했습니다.
* 승인 유효성 검사 메서드를 추가했습니다. 파일 확장자를 확인합니다.
* 두 개의 사용자 지정 식, 즉 빈 값이 있는 요소를 선택하기 위한 “:blank”와 하나의 값이 있는 요소를 선택하기 위한 “:filled”를 추가하여 종속성 기능을 개선했습니다. 두 경우 모두 공백은 제외됩니다.
* 유효성 검사기에 resetForm() 메서드를 추가 합니다. (사용 가능한 경우 양식 플러그 인 사용) 각 양식 요소를 잘못 된 요소에는 클래스를 제거 하 고, 모든 오류 메시지를 숨깁니다.
* validator.showErrors()에 대한 문서를 수정했습니다.
* text() 대신 항상 html()을 사용하도록 오류 레이블 생성을 수정하여 임의 HTML이 메시지로 전달될 수 있도록 했습니다.
* 지정된 오류 클래스를 사용하도록 오류 레이블 생성을 수정했습니다.
* 추가 된 종속성 기능: 메서드 인수로 문자열 (jQuery 식) 및 함수를 모두 허용 해야 합니다.
* 오류 메시지 표시의 사용자 지정 개선: 일반 메시지를 사용 하 고 추가 컨테이너; 표시/숨기기 (하는 동안 기본 처리기를 위임할 수 있는 고유한 메커니즘을 사용 하 여 메시지 표시를 완전히 대체 (기본 below-element) 하는 대신 생성 된 레이블의 배치를 사용자 지정
* IE(오류 컨테이너) 및 Opera(메타데이터)의 2가지 주요 버그를 수정했습니다.
* 비어 있는 필드를 유효한 필드로 수락하도록 유효성 검사 메서드를 수정했습니다(예외: 'required' 및 'equalTo' 메서드).
* 이름이 “min”에서 “minLength”로, “max”에서 “maxLength”로, “length”에서 “rangeLength”로 바뀌었습니다.
* “minValue”, “maxValue” 및 “rangeValue”를 추가했습니다.
* 다양한 이벤트를 지원하기 위해 API를 간소화했습니다. 기본값인 제출을 사용하지 않도록 설정할 수 있습니다. 이벤트가 지정되면 각 요소(전체 폼 대신)에 적용됩니다. 이제 keyup-validation과 submit-validation을 결합하기가 상당히 쉬워졌습니다.
* 플러그 인 설정을 통해 메시지를 정의할 때 one-message-per-rule에 대한 지원을 추가했습니다.
* 일부 부모 요소에서 메타데이터를 래핑하기 위한 지원을 추가했습니다. 메타데이터가 다른 플러그 인에도 사용될 때 유용합니다.
* 리팩터링된 테스트 및 데모: 파일을 작은 데모는 개선
* 향상 된 설명서: 메서드에 대 한 더 많은 예제를 자세히 참조 몇 가지 기본 사항을 설명 하는 텍스트
