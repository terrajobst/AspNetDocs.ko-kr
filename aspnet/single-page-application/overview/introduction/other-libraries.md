---
uid: single-page-application/overview/introduction/other-libraries
title: Knockout 이외의 라이브러리를 알고 있으신가요? | Microsoft Docs
author: madskristensen
description: Knockout 이외의 라이브러리를 알고 있으신가요?
ms.author: riande
ms.date: 02/05/2013
ms.assetid: a8367c6d-ef94-4dff-a010-5eff9e6eea96
msc.legacyurl: /single-page-application/overview/introduction/other-libraries
msc.type: authoredcontent
ms.openlocfilehash: 64a4ad1fb411f7291a5cba634afdf4d2fdb16d55
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467195"
---
# <a name="know-a-library-other-than-knockout"></a>Knockout 이외의 라이브러리를 알고 있으신가요?

[Mads Kristensen](https://github.com/madskristensen)

[SPA (단일 페이지 응용 프로그램) 템플릿은](knockoutjs-template.md) 단일 페이지 응용 프로그램 작성을 시작 하는 좋은 방법입니다. 템플릿은 [KnockoutJS](http://knockoutjs.com/) 를 사용 하 여 응용 프로그램 데이터를 DOM 요소에 바인딩합니다.

하지만 녹아웃은 리치 클라이언트 응용 프로그램을 만들기 위한 유일한 JavaScript 라이브러리가 아닙니다. 다른 라이브러리는 다른 방법으로 비슷한 문제를 해결 합니다. 한 라이브러리에서 다른 라이브러리를 선호 하는 경우 여러 커뮤니티에서 만든 템플릿을 다운로드할 수 있습니다. 이러한 각 템플릿은 서로 다른 클라이언트 JavaScript 라이브러리 조합을 사용 합니다.

커뮤니티에서 만든 템플릿을 설치 하려면 아래 나열 된 템플릿 페이지 중 하나를 방문 하 여 다운로드 단추를 클릭 합니다. 템플릿은 VSIX 파일로 제공 됩니다.

## <a name="backbonejs"></a>BackboneJS

[DEFAULT.JS SPA 템플릿](../templates/backbonejs-template.md). 이 템플릿은 ASP.NET MVC에서 [백본](http://backbonejs.org/) 응용 프로그램을 개발 하기 위한 초기 구조를 제공 합니다. 기본적으로 기본 전자 메일 템플릿과 함께 사용자 등록, 로그인, 암호 재설정 및 사용자 확인 등 기본적인 사용자 로그인 기능을 제공 합니다.

## <a name="breezejs"></a>BreezeJS

[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa) 는 JavaScript 클라이언트에서 리치 데이터를 관리 하기 위한 오픈 소스 라이브러리입니다. 간단히 쿼리, 캐싱, 변경 내용 추적, 유효성 검사 등을 처리 합니다. 다음과 같은 두 가지 템플릿 기능을 간편 하 게 합니다.

- [간편/녹아웃](../templates/breezeknockout-template.md) 템플릿은 녹아웃 SPA 템플릿을 확장 하 여 데이터 바인딩을 위한 간편한 데이터 관리 및 KnockoutJS을 통해 단일 페이지 응용 프로그램을 쉽게 빌드할 수 있는 방법을 보여 줍니다.
- [간편](../templates/breezeangular-template.md) 하 고도를 사용 하는 템플릿은 녹아웃 SPA 템플릿을 간편 하 게 확장 하지만 데이터 바인딩, 종속성 주입 및 화면 관리를 위해 [AngularJS](http://angularjs.org) 라이브러리를 사용 합니다.

또한 [Hot 수건 SPA 템플릿에서](../templates/hottowel-template.md) 는 BreezeJS를 사용 합니다.

## <a name="emberjs"></a>EmberJS

[EMBERJS SPA 템플릿](../templates/emberjs-template.md). 이 템플릿은 다양 한 클라이언트 응용 프로그램을 빌드하기 위한 광범위 한 문제를 해결 하는 강력한 MVC JavaScript 라이브러리인 [ember.js](http://emberjs.com/)를 사용 합니다.

Ember.js SPA 템플릿은 EmberJS 및 Handlebars 템플릿을 사용 하 여 녹아웃 SPA 템플릿 다시 구현입니다.

## <a name="hot-towel"></a>핫 수건

[핫 수건 SPA 템플릿](../templates/hottowel-template.md). 이 템플릿은 간편, 녹아웃, RequireJS 및 Twitter 부트스트랩을 비롯 한 여러 JavaScript 라이브러리를 가져옵니다.

여기에 나열 된 다른 템플릿과 비교할 때 Hot 수건 템플릿은 사용자 고유의 응용 프로그램을 빌드할 수 있는 더 완전 한 응용 프로그램을 제공 합니다. 이러한 개념을 이해 하는 데 도움이 되는 추가 개념은 무엇 인가요? SPA를 빌드하려고 하지만 시작할 위치를 결정할 수 없는 경우 핫 수건를 사용 하 고, SPA와 여기에 빌드하는 데 필요한 모든 도구를 제공 합니다.

## <a name="feature-table"></a>기능 테이블

각 SPA 템플릿에서 제공 하는 기능은 다음과 같습니다.

|                        | ASP.NET SPA | 백본으로 | 간편/각도 | 간편/KO-KR |  Ember.js   | 핫 수건 |
|------------------------|-------------|----------|----------------|-----------|----------|-----------|
|      ToDo 샘플       |  &#10003;   |          |    &#10003;    | &#10003;  | &#10003; |           |
|     템플릿 서식      |             | &#10003; |                |           |          | &#10003;  |
| 탐색 및 기록 |             | &#10003; |    &#10003;    |           | &#10003; | &#10003;  |
|        라이브러리       |             |          |                |           |          |           |
|        Angular         |             |          |    &#10003;    |           |          |           |
|    &#8195;백본으로     |             | &#10003; |                |           |          |           |
|         손쉽게         |             |          |    &#10003;    | &#10003;  |          | &#10003;  |
|        durandal        |             |          |                |           |          | &#10003;  |
|         Ember.js          |             |          |                |           | &#10003; |           |
|        Knockout        |  &#10003;   |          |                | &#10003;  |          | &#10003;  |
