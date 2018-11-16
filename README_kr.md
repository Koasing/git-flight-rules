# Git을 위한 비행 규칙

🌍
*[English](README.md) ∙ [Español](README_es.md)  ∙  [Русский](README_ru.md) ∙ [简体中文](README_zh-CN.md)∙ [한국어](README_kr.md)  ∙ [Tiếng Việt](README_vi.md)*

#### "비행 규칙"이 뭐에요?

[우주비행사를 위한 가이드](https://www.jsc.nasa.gov/news/columbia/fr_generic.pdf) (여기선 Git을 쓰는 개발자를 위한 가이드) 입니다. 무언가가 잘못 되었을 때 어떻게 해야 하는지를 담고 있지요.

>  *Flight Rules* 는 어떤 문제 X가 발생한 이유와 그 단계의 매뉴얼에서 어렵사리 얻은 지식이에요. 기본적으로 각 시나리오의 매우 자세하고 구체적인 운영 절차랍니다. [...]

> NASA는 수성(Mercury) 시대 때 지상팀에서 처음으로 "lessons learned" 이란 것을 모았는데 수천개의 문제의 상황들, 부서진 해치 손잡이로 인한 엔진 고장부터 컴퓨터 문제 그리고 그 해답까지, 1960년대 초부터 우리의 실수들, 재앙들, 해결책 등이  목록화 돼있어요. 

— Chris Hadfield, *인생을 위한 우주비행사의 가이드*.

#### 이 문서의 규칙

표기를 명확하게 하기 위해, 이 문서의 모든 예제는 현재 브랜치를 표시하고 스테이지에 변경이 있는지를 나타내도록 수정된 bash 프롬프트를 써요. 브랜치는 괄호 안에 명시되고, 브랜치 다음의 `*`는 스테이지에 변경점이 있음을 나타내요.  

모든 명령어는 적어도 git 버전 2.13.0 에서는 작동할 거에요. [git 웹사이트](https://www.git-scm.com/)에 방문해서 로컬 git 버전을 최신으로 업데이트 하세요.

[![Join the chat at https://gitter.im/k88hudson/git-flight-rules](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/k88hudson/git-flight-rules?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

  - [저장소](#%EC%A0%80%EC%9E%A5%EC%86%8C)
    - [로컬 저장소를 새로 만들고 싶어](#%EB%A1%9C%EC%BB%AC-%EC%A0%80%EC%9E%A5%EC%86%8C%EB%A5%BC-%EC%83%88%EB%A1%9C-%EB%A7%8C%EB%93%A4%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [원격 저장소를 복제해 오고 싶어](#%EC%9B%90%EA%B2%A9-%EC%A0%80%EC%9E%A5%EC%86%8C%EB%A5%BC-%EB%B3%B5%EC%A0%9C%ED%95%B4-%EC%98%A4%EA%B3%A0-%EC%8B%B6%EC%96%B4)
  - [커밋 수정](#%EC%BB%A4%EB%B0%8B-%EC%88%98%EC%A0%95)
    - [내가 방금 어떤 커밋을 남겼지?](#%EB%82%B4%EA%B0%80-%EB%B0%A9%EA%B8%88-%EC%96%B4%EB%96%A4-%EC%BB%A4%EB%B0%8B%EC%9D%84-%EB%82%A8%EA%B2%BC%EC%A7%80)
    - [커밋 메세지를 잘못 썼어](#%EC%BB%A4%EB%B0%8B-%EB%A9%94%EC%84%B8%EC%A7%80%EB%A5%BC-%EC%9E%98%EB%AA%BB-%EC%8D%BC%EC%96%B4)
    - [커밋을 다른 이름과 이메일 설정으로 해 버렸어](#%EC%BB%A4%EB%B0%8B%EC%9D%84-%EB%8B%A4%EB%A5%B8-%EC%9D%B4%EB%A6%84%EA%B3%BC-%EC%9D%B4%EB%A9%94%EC%9D%BC-%EC%84%A4%EC%A0%95%EC%9C%BC%EB%A1%9C-%ED%95%B4-%EB%B2%84%EB%A0%B8%EC%96%B4)
    - [지난 커밋에서 파일 하나를 지우고 싶어](#%EC%A7%80%EB%82%9C-%EC%BB%A4%EB%B0%8B%EC%97%90%EC%84%9C-%ED%8C%8C%EC%9D%BC-%ED%95%98%EB%82%98%EB%A5%BC-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [마지막 커밋을 지우고 싶어](#%EB%A7%88%EC%A7%80%EB%A7%89-%EC%BB%A4%EB%B0%8B%EC%9D%84-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [임의의 커밋 지우기](#%EC%9E%84%EC%9D%98%EC%9D%98-%EC%BB%A4%EB%B0%8B-%EC%A7%80%EC%9A%B0%EA%B8%B0)
    - [수정된 커밋을 푸시했는데, 에러 메세지가 떠](#%EC%88%98%EC%A0%95%EB%90%9C-%EC%BB%A4%EB%B0%8B%EC%9D%84-%ED%91%B8%EC%8B%9C%ED%96%88%EB%8A%94%EB%8D%B0-%EC%97%90%EB%9F%AC-%EB%A9%94%EC%84%B8%EC%A7%80%EA%B0%80-%EB%96%A0)
    - [실수로 하드 리셋을 했는데, 작업하던걸 되살리고 싶어](#%EC%8B%A4%EC%88%98%EB%A1%9C-%ED%95%98%EB%93%9C-%EB%A6%AC%EC%85%8B%EC%9D%84-%ED%96%88%EB%8A%94%EB%8D%B0-%EC%9E%91%EC%97%85%ED%95%98%EB%8D%98%EA%B1%B8-%EB%90%98%EC%82%B4%EB%A6%AC%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [실수로 머지를 커밋하고 푸시해 버렸어](#%EC%8B%A4%EC%88%98%EB%A1%9C-%EB%A8%B8%EC%A7%80%EB%A5%BC-%EC%BB%A4%EB%B0%8B%ED%95%98%EA%B3%A0-%ED%91%B8%EC%8B%9C%ED%95%B4-%EB%B2%84%EB%A0%B8%EC%96%B4)
    - [실수로 공개되면 안 되는 자료를 담은 파일을 커밋하고 푸시했어](#%EC%8B%A4%EC%88%98%EB%A1%9C-%EA%B3%B5%EA%B0%9C%EB%90%98%EB%A9%B4-%EC%95%88-%EB%90%98%EB%8A%94-%EC%9E%90%EB%A3%8C%EB%A5%BC-%EB%8B%B4%EC%9D%80-%ED%8C%8C%EC%9D%BC%EC%9D%84-%EC%BB%A4%EB%B0%8B%ED%95%98%EA%B3%A0-%ED%91%B8%EC%8B%9C%ED%96%88%EC%96%B4)
  - [스테이지](#%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80)
    - [스테이지의 변경점을 이전 커밋에 추가하고 싶어](#%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80%EC%9D%98-%EB%B3%80%EA%B2%BD%EC%A0%90%EC%9D%84-%EC%9D%B4%EC%A0%84-%EC%BB%A4%EB%B0%8B%EC%97%90-%EC%B6%94%EA%B0%80%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [새 파일 중 전체가 아닌 일부분만 스테이지 하고 싶어.](#%EC%83%88-%ED%8C%8C%EC%9D%BC-%EC%A4%91-%EC%A0%84%EC%B2%B4%EA%B0%80-%EC%95%84%EB%8B%8C-%EC%9D%BC%EB%B6%80%EB%B6%84%EB%A7%8C-%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80-%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [하나의 파일 변경점을 두개의 다른 커밋에 남기고 싶어](#%ED%95%98%EB%82%98%EC%9D%98-%ED%8C%8C%EC%9D%BC-%EB%B3%80%EA%B2%BD%EC%A0%90%EC%9D%84-%EB%91%90%EA%B0%9C%EC%9D%98-%EB%8B%A4%EB%A5%B8-%EC%BB%A4%EB%B0%8B%EC%97%90-%EB%82%A8%EA%B8%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [아직 스테이지에 안 올라간 변경점을 스테이지에 추가하고, 스테이지에 있는 변경점은 다시 빼고 싶어](#%EC%95%84%EC%A7%81-%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80%EC%97%90-%EC%95%88-%EC%98%AC%EB%9D%BC%EA%B0%84-%EB%B3%80%EA%B2%BD%EC%A0%90%EC%9D%84-%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80%EC%97%90-%EC%B6%94%EA%B0%80%ED%95%98%EA%B3%A0-%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80%EC%97%90-%EC%9E%88%EB%8A%94-%EB%B3%80%EA%B2%BD%EC%A0%90%EC%9D%80-%EB%8B%A4%EC%8B%9C-%EB%B9%BC%EA%B3%A0-%EC%8B%B6%EC%96%B4)
  - [스테이지 전의 변경점](#%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80-%EC%A0%84%EC%9D%98-%EB%B3%80%EA%B2%BD%EC%A0%90)
    - [스테이지 전의 변경점을 새 브랜치로 옮기고 싶어](#%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80-%EC%A0%84%EC%9D%98-%EB%B3%80%EA%B2%BD%EC%A0%90%EC%9D%84-%EC%83%88-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A1%9C-%EC%98%AE%EA%B8%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [스테이지 전의 변경점을 이미 존재하는 다른 브랜치로 옮기고 싶어](#%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80-%EC%A0%84%EC%9D%98-%EB%B3%80%EA%B2%BD%EC%A0%90%EC%9D%84-%EC%9D%B4%EB%AF%B8-%EC%A1%B4%EC%9E%AC%ED%95%98%EB%8A%94-%EB%8B%A4%EB%A5%B8-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A1%9C-%EC%98%AE%EA%B8%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [내 로컬에 있는 커밋 안된 변경점을 다 무시하고 싶어 (스테이징 됐던 안됐던)](#%EB%82%B4-%EB%A1%9C%EC%BB%AC%EC%97%90-%EC%9E%88%EB%8A%94-%EC%BB%A4%EB%B0%8B-%EC%95%88%EB%90%9C-%EB%B3%80%EA%B2%BD%EC%A0%90%EC%9D%84-%EB%8B%A4-%EB%AC%B4%EC%8B%9C%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4-%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%95-%EB%90%90%EB%8D%98-%EC%95%88%EB%90%90%EB%8D%98)
    - [스테이지 안된 특정 변경 사항을 지우고 싶어](#%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80-%EC%95%88%EB%90%9C-%ED%8A%B9%EC%A0%95-%EB%B3%80%EA%B2%BD-%EC%82%AC%ED%95%AD%EC%9D%84-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [스테이지 안된 특정 파일을 지우고 싶어](#%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80-%EC%95%88%EB%90%9C-%ED%8A%B9%EC%A0%95-%ED%8C%8C%EC%9D%BC%EC%9D%84-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [로컬에 있는 스테이지 안된 변경점만 지우고 싶어](#%EB%A1%9C%EC%BB%AC%EC%97%90-%EC%9E%88%EB%8A%94-%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80-%EC%95%88%EB%90%9C-%EB%B3%80%EA%B2%BD%EC%A0%90%EB%A7%8C-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [추적되지 않는 파일들 다 지우고 싶어](#%EC%B6%94%EC%A0%81%EB%90%98%EC%A7%80-%EC%95%8A%EB%8A%94-%ED%8C%8C%EC%9D%BC%EB%93%A4-%EB%8B%A4-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [스테이지된 파일 중 일부를 빼 버리고 싶어](#%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%A7%80%EB%90%9C-%ED%8C%8C%EC%9D%BC-%EC%A4%91-%EC%9D%BC%EB%B6%80%EB%A5%BC-%EB%B9%BC-%EB%B2%84%EB%A6%AC%EA%B3%A0-%EC%8B%B6%EC%96%B4)
  - [브랜치](#%EB%B8%8C%EB%9E%9C%EC%B9%98)
    - [모든 브랜치 리스트를 보고 싶어](#%EB%AA%A8%EB%93%A0-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%A6%AC%EC%8A%A4%ED%8A%B8%EB%A5%BC-%EB%B3%B4%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [커밋에서 브랜치 만들기](#%EC%BB%A4%EB%B0%8B%EC%97%90%EC%84%9C-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%A7%8C%EB%93%A4%EA%B8%B0)
    - [다른 브랜치에서 풀을 받아와버렸어](#%EB%8B%A4%EB%A5%B8-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%97%90%EC%84%9C-%ED%92%80%EC%9D%84-%EB%B0%9B%EC%95%84%EC%99%80%EB%B2%84%EB%A0%B8%EC%96%B4)
    - [로컬의 커밋을 지워서 서버에 있는 내 브랜치와 맞추고 싶어](#%EB%A1%9C%EC%BB%AC%EC%9D%98-%EC%BB%A4%EB%B0%8B%EC%9D%84-%EC%A7%80%EC%9B%8C%EC%84%9C-%EC%84%9C%EB%B2%84%EC%97%90-%EC%9E%88%EB%8A%94-%EB%82%B4-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%99%80-%EB%A7%9E%EC%B6%94%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [새 브랜치 대신에 마스터에 커밋을 해버렸어](#%EC%83%88-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%8C%80%EC%8B%A0%EC%97%90-%EB%A7%88%EC%8A%A4%ED%84%B0%EC%97%90-%EC%BB%A4%EB%B0%8B%EC%9D%84-%ED%95%B4%EB%B2%84%EB%A0%B8%EC%96%B4)
    - [다른 레퍼런스 같은 곳에서 모든 파일을 유지하고 싶어](#%EB%8B%A4%EB%A5%B8-%EB%A0%88%ED%8D%BC%EB%9F%B0%EC%8A%A4-%EA%B0%99%EC%9D%80-%EA%B3%B3%EC%97%90%EC%84%9C-%EB%AA%A8%EB%93%A0-%ED%8C%8C%EC%9D%BC%EC%9D%84-%EC%9C%A0%EC%A7%80%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [한 브랜치에 다른 브랜치에 남겼어야 하는 커밋을 여러개 남겼어](#%ED%95%9C-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%97%90-%EB%8B%A4%EB%A5%B8-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%97%90-%EB%82%A8%EA%B2%BC%EC%96%B4%EC%95%BC-%ED%95%98%EB%8A%94-%EC%BB%A4%EB%B0%8B%EC%9D%84-%EC%97%AC%EB%9F%AC%EA%B0%9C-%EB%82%A8%EA%B2%BC%EC%96%B4)
    - [업스트림에선 지워진 로컬 브랜치를 지우고 싶어](#%EC%97%85%EC%8A%A4%ED%8A%B8%EB%A6%BC%EC%97%90%EC%84%A0-%EC%A7%80%EC%9B%8C%EC%A7%84-%EB%A1%9C%EC%BB%AC-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A5%BC-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [실수로 브랜치를 지워버렸어](#%EC%8B%A4%EC%88%98%EB%A1%9C-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A5%BC-%EC%A7%80%EC%9B%8C%EB%B2%84%EB%A0%B8%EC%96%B4)
    - [브랜치를 지우고 싶어](#%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A5%BC-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [여러개의 브랜치를 지우고 싶어](#%EC%97%AC%EB%9F%AC%EA%B0%9C%EC%9D%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A5%BC-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [브랜치 이름을 바꾸고 싶어](#%EB%B8%8C%EB%9E%9C%EC%B9%98-%EC%9D%B4%EB%A6%84%EC%9D%84-%EB%B0%94%EA%BE%B8%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [다른 사람이 작업중인 원격 브랜치로 체크아웃 하고 싶어](#%EB%8B%A4%EB%A5%B8-%EC%82%AC%EB%9E%8C%EC%9D%B4-%EC%9E%91%EC%97%85%EC%A4%91%EC%9D%B8-%EC%9B%90%EA%B2%A9-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A1%9C-%EC%B2%B4%ED%81%AC%EC%95%84%EC%9B%83-%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [현재 로컬 브랜치로 새로운 원격 브랜치를 만들고 싶어](#%ED%98%84%EC%9E%AC-%EB%A1%9C%EC%BB%AC-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A1%9C-%EC%83%88%EB%A1%9C%EC%9A%B4-%EC%9B%90%EA%B2%A9-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A5%BC-%EB%A7%8C%EB%93%A4%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [원격 브랜치를 로컬 브랜치의 업스트림으로 설정하고 싶어](#%EC%9B%90%EA%B2%A9-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A5%BC-%EB%A1%9C%EC%BB%AC-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%9D%98-%EC%97%85%EC%8A%A4%ED%8A%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%84%A4%EC%A0%95%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [HEAD를 기본 원격 브랜치로 트래킹하도록 설정하고 싶어](#head%EB%A5%BC-%EA%B8%B0%EB%B3%B8-%EC%9B%90%EA%B2%A9-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A1%9C-%ED%8A%B8%EB%9E%98%ED%82%B9%ED%95%98%EB%8F%84%EB%A1%9D-%EC%84%A4%EC%A0%95%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [잘못된 브랜치에서 변경사항을 만들었어](#%EC%9E%98%EB%AA%BB%EB%90%9C-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%97%90%EC%84%9C-%EB%B3%80%EA%B2%BD%EC%82%AC%ED%95%AD%EC%9D%84-%EB%A7%8C%EB%93%A4%EC%97%88%EC%96%B4)
  - [리베이스와 병합](#%EB%A6%AC%EB%B2%A0%EC%9D%B4%EC%8A%A4%EC%99%80-%EB%B3%91%ED%95%A9)
    - [리베이스/병합한 걸 되돌리고 싶어](#%EB%A6%AC%EB%B2%A0%EC%9D%B4%EC%8A%A4%EB%B3%91%ED%95%A9%ED%95%9C-%EA%B1%B8-%EB%90%98%EB%8F%8C%EB%A6%AC%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [리베이스를 했는데, 강제 푸시하고 싶진 않아](#%EB%A6%AC%EB%B2%A0%EC%9D%B4%EC%8A%A4%EB%A5%BC-%ED%96%88%EB%8A%94%EB%8D%B0-%EA%B0%95%EC%A0%9C-%ED%91%B8%EC%8B%9C%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%A7%84-%EC%95%8A%EC%95%84)
    - [커밋 여러개를 하나로 합쳐야 해](#%EC%BB%A4%EB%B0%8B-%EC%97%AC%EB%9F%AC%EA%B0%9C%EB%A5%BC-%ED%95%98%EB%82%98%EB%A1%9C-%ED%95%A9%EC%B3%90%EC%95%BC-%ED%95%B4)
      - [안전한 병합 전략](#%EC%95%88%EC%A0%84%ED%95%9C-%EB%B3%91%ED%95%A9-%EC%A0%84%EB%9E%B5)
      - [브랜치를 커밋 하나로 머지해야해](#%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%A5%BC-%EC%BB%A4%EB%B0%8B-%ED%95%98%EB%82%98%EB%A1%9C-%EB%A8%B8%EC%A7%80%ED%95%B4%EC%95%BC%ED%95%B4)
      - [푸시 되지 않은 커밋만 합치고 싶어](#%ED%91%B8%EC%8B%9C-%EB%90%98%EC%A7%80-%EC%95%8A%EC%9D%80-%EC%BB%A4%EB%B0%8B%EB%A7%8C-%ED%95%A9%EC%B9%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
      - [병합을 중단해야해](#%EB%B3%91%ED%95%A9%EC%9D%84-%EC%A4%91%EB%8B%A8%ED%95%B4%EC%95%BC%ED%95%B4)
    - [브랜치의 부모 커밋을 바꿔야 해](#%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%9D%98-%EB%B6%80%EB%AA%A8-%EC%BB%A4%EB%B0%8B%EC%9D%84-%EB%B0%94%EA%BF%94%EC%95%BC-%ED%95%B4)
    - [브랜치내 모든 커밋이 머지됐는지 확인해](#%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%82%B4-%EB%AA%A8%EB%93%A0-%EC%BB%A4%EB%B0%8B%EC%9D%B4-%EB%A8%B8%EC%A7%80%EB%90%90%EB%8A%94%EC%A7%80-%ED%99%95%EC%9D%B8%ED%95%B4)
    - [대화형 리베이스로 발생가능한 이슈](#%EB%8C%80%ED%99%94%ED%98%95-%EB%A6%AC%EB%B2%A0%EC%9D%B4%EC%8A%A4%EB%A1%9C-%EB%B0%9C%EC%83%9D%EA%B0%80%EB%8A%A5%ED%95%9C-%EC%9D%B4%EC%8A%88)
      - [리베이스 편집 화면에서 'noop'](#%EB%A6%AC%EB%B2%A0%EC%9D%B4%EC%8A%A4-%ED%8E%B8%EC%A7%91-%ED%99%94%EB%A9%B4%EC%97%90%EC%84%9C-noop)
      - [충돌이 있어](#%EC%B6%A9%EB%8F%8C%EC%9D%B4-%EC%9E%88%EC%96%B4)
  - [스태시](#%EC%8A%A4%ED%83%9C%EC%8B%9C)
    - [모든 변경점을 스태시에 보관하기](#%EB%AA%A8%EB%93%A0-%EB%B3%80%EA%B2%BD%EC%A0%90%EC%9D%84-%EC%8A%A4%ED%83%9C%EC%8B%9C%EC%97%90-%EB%B3%B4%EA%B4%80%ED%95%98%EA%B8%B0)
    - [특정 파일들만 스태시에 보관하기](#%ED%8A%B9%EC%A0%95-%ED%8C%8C%EC%9D%BC%EB%93%A4%EB%A7%8C-%EC%8A%A4%ED%83%9C%EC%8B%9C%EC%97%90-%EB%B3%B4%EA%B4%80%ED%95%98%EA%B8%B0)
    - [메세지와 함께 보관하기](#%EB%A9%94%EC%84%B8%EC%A7%80%EC%99%80-%ED%95%A8%EA%BB%98-%EB%B3%B4%EA%B4%80%ED%95%98%EA%B8%B0)
    - [목록에서 특정 스태시를 가져와서 적용하기](#%EB%AA%A9%EB%A1%9D%EC%97%90%EC%84%9C-%ED%8A%B9%EC%A0%95-%EC%8A%A4%ED%83%9C%EC%8B%9C%EB%A5%BC-%EA%B0%80%EC%A0%B8%EC%99%80%EC%84%9C-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)
  - [찾아보기](#%EC%B0%BE%EC%95%84%EB%B3%B4%EA%B8%B0)
    - [모든 커밋에서 문자열을 찾고 싶어](#%EB%AA%A8%EB%93%A0-%EC%BB%A4%EB%B0%8B%EC%97%90%EC%84%9C-%EB%AC%B8%EC%9E%90%EC%97%B4%EC%9D%84-%EC%B0%BE%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [작성자나 커미터를 찾고 싶어](#%EC%9E%91%EC%84%B1%EC%9E%90%EB%82%98-%EC%BB%A4%EB%AF%B8%ED%84%B0%EB%A5%BC-%EC%B0%BE%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [특정 파일이 포함된 커밋을 목록화 하고 싶어](#%ED%8A%B9%EC%A0%95-%ED%8C%8C%EC%9D%BC%EC%9D%B4-%ED%8F%AC%ED%95%A8%EB%90%9C-%EC%BB%A4%EB%B0%8B%EC%9D%84-%EB%AA%A9%EB%A1%9D%ED%99%94-%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [커밋을 참조하는 태그를 찾고 싶어](#%EC%BB%A4%EB%B0%8B%EC%9D%84-%EC%B0%B8%EC%A1%B0%ED%95%98%EB%8A%94-%ED%83%9C%EA%B7%B8%EB%A5%BC-%EC%B0%BE%EA%B3%A0-%EC%8B%B6%EC%96%B4)
  - [서브모듈](#%EC%84%9C%EB%B8%8C%EB%AA%A8%EB%93%88)
    - [모든 서브모듈을 클론하기](#%EB%AA%A8%EB%93%A0-%EC%84%9C%EB%B8%8C%EB%AA%A8%EB%93%88%EC%9D%84-%ED%81%B4%EB%A1%A0%ED%95%98%EA%B8%B0)
    - [서브모듈 지우기](#%EC%84%9C%EB%B8%8C%EB%AA%A8%EB%93%88-%EC%A7%80%EC%9A%B0%EA%B8%B0)
  - [기타 항목들](#%EA%B8%B0%ED%83%80-%ED%95%AD%EB%AA%A9%EB%93%A4)
    - [지운 파일 복구하기](#%EC%A7%80%EC%9A%B4-%ED%8C%8C%EC%9D%BC-%EB%B3%B5%EA%B5%AC%ED%95%98%EA%B8%B0)
    - [태그 지우기](#%ED%83%9C%EA%B7%B8-%EC%A7%80%EC%9A%B0%EA%B8%B0)
    - [지워진 태그 복구하기](#%EC%A7%80%EC%9B%8C%EC%A7%84-%ED%83%9C%EA%B7%B8-%EB%B3%B5%EA%B5%AC%ED%95%98%EA%B8%B0)
    - [지워진 패치](#%EC%A7%80%EC%9B%8C%EC%A7%84-%ED%8C%A8%EC%B9%98)
    - [Zip파일로 저장소 내보내기](#zip%ED%8C%8C%EC%9D%BC%EB%A1%9C-%EC%A0%80%EC%9E%A5%EC%86%8C-%EB%82%B4%EB%B3%B4%EB%82%B4%EA%B8%B0)
    - [같은 이름의 브랜치와 태그를 푸시하기](#%EA%B0%99%EC%9D%80-%EC%9D%B4%EB%A6%84%EC%9D%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%99%80-%ED%83%9C%EA%B7%B8%EB%A5%BC-%ED%91%B8%EC%8B%9C%ED%95%98%EA%B8%B0)
  - [파일 추적하기](#%ED%8C%8C%EC%9D%BC-%EC%B6%94%EC%A0%81%ED%95%98%EA%B8%B0)
    - [파일 내용엔 변경이 없이 파일 이름을 앞글자만 대문자로 바꾸고 싶어](#%ED%8C%8C%EC%9D%BC-%EB%82%B4%EC%9A%A9%EC%97%94-%EB%B3%80%EA%B2%BD%EC%9D%B4-%EC%97%86%EC%9D%B4-%ED%8C%8C%EC%9D%BC-%EC%9D%B4%EB%A6%84%EC%9D%84-%EC%95%9E%EA%B8%80%EC%9E%90%EB%A7%8C-%EB%8C%80%EB%AC%B8%EC%9E%90%EB%A1%9C-%EB%B0%94%EA%BE%B8%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [Git 풀 받을때 로컬 파일을 덮어씌우고 싶어](#git-%ED%92%80-%EB%B0%9B%EC%9D%84%EB%95%8C-%EB%A1%9C%EC%BB%AC-%ED%8C%8C%EC%9D%BC%EC%9D%84-%EB%8D%AE%EC%96%B4%EC%94%8C%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [파일을 로컬에는 보관하고 Git에서 지우고 싶어](#%ED%8C%8C%EC%9D%BC%EC%9D%84-%EB%A1%9C%EC%BB%AC%EC%97%90%EB%8A%94-%EB%B3%B4%EA%B4%80%ED%95%98%EA%B3%A0-git%EC%97%90%EC%84%9C-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [특정한 리비전으로 파일을 복구하고 싶어](#%ED%8A%B9%EC%A0%95%ED%95%9C-%EB%A6%AC%EB%B9%84%EC%A0%84%EC%9C%BC%EB%A1%9C-%ED%8C%8C%EC%9D%BC%EC%9D%84-%EB%B3%B5%EA%B5%AC%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [커밋이나 브랜치 사이에서 특정 파일의 변경 이력이 필요해](#%EC%BB%A4%EB%B0%8B%EC%9D%B4%EB%82%98-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EC%82%AC%EC%9D%B4%EC%97%90%EC%84%9C-%ED%8A%B9%EC%A0%95-%ED%8C%8C%EC%9D%BC%EC%9D%98-%EB%B3%80%EA%B2%BD-%EC%9D%B4%EB%A0%A5%EC%9D%B4-%ED%95%84%EC%9A%94%ED%95%B4)
    - [특정 파일의 변경점을 Git이 무시하도록 하고 싶어](#%ED%8A%B9%EC%A0%95-%ED%8C%8C%EC%9D%BC%EC%9D%98-%EB%B3%80%EA%B2%BD%EC%A0%90%EC%9D%84-git%EC%9D%B4-%EB%AC%B4%EC%8B%9C%ED%95%98%EB%8F%84%EB%A1%9D-%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
  - [설정](#%EC%84%A4%EC%A0%95)
    - [Git 명령어 몇 개를 앨리어스 등록하고 싶어](#git-%EB%AA%85%EB%A0%B9%EC%96%B4-%EB%AA%87-%EA%B0%9C%EB%A5%BC-%EC%95%A8%EB%A6%AC%EC%96%B4%EC%8A%A4-%EB%93%B1%EB%A1%9D%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [저장소에 빈 디렉토리를 추가하고 싶어](#%EC%A0%80%EC%9E%A5%EC%86%8C%EC%97%90-%EB%B9%88-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EB%A5%BC-%EC%B6%94%EA%B0%80%ED%95%98%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [저장소 유저명과 비밀번호를 캐시해두고 싶어](#%EC%A0%80%EC%9E%A5%EC%86%8C-%EC%9C%A0%EC%A0%80%EB%AA%85%EA%B3%BC-%EB%B9%84%EB%B0%80%EB%B2%88%ED%98%B8%EB%A5%BC-%EC%BA%90%EC%8B%9C%ED%95%B4%EB%91%90%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [Git이 권한과 파일모드 변경을 무시하게 만들고 싶어](#git%EC%9D%B4-%EA%B6%8C%ED%95%9C%EA%B3%BC-%ED%8C%8C%EC%9D%BC%EB%AA%A8%EB%93%9C-%EB%B3%80%EA%B2%BD%EC%9D%84-%EB%AC%B4%EC%8B%9C%ED%95%98%EA%B2%8C-%EB%A7%8C%EB%93%A4%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [글로벌 유저를 설정해두고 싶어](#%EA%B8%80%EB%A1%9C%EB%B2%8C-%EC%9C%A0%EC%A0%80%EB%A5%BC-%EC%84%A4%EC%A0%95%ED%95%B4%EB%91%90%EA%B3%A0-%EC%8B%B6%EC%96%B4)
    - [Git에 명령줄 색상을 넣고 싶어](#git%EC%97%90-%EB%AA%85%EB%A0%B9%EC%A4%84-%EC%83%89%EC%83%81%EC%9D%84-%EB%84%A3%EA%B3%A0-%EC%8B%B6%EC%96%B4)
  - [뭘 잘못했는지 모르겠어](#%EB%AD%98-%EC%9E%98%EB%AA%BB%ED%96%88%EB%8A%94%EC%A7%80-%EB%AA%A8%EB%A5%B4%EA%B2%A0%EC%96%B4)
- [다른 리소스](#%EB%8B%A4%EB%A5%B8-%EB%A6%AC%EC%86%8C%EC%8A%A4)
  - [도서](#%EB%8F%84%EC%84%9C)
  - [튜토리얼](#%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC)
  - [스크립트와 도구](#%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%99%80-%EB%8F%84%EA%B5%AC)
  - [GUI 클라이언트](#gui-%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 저장소

### 로컬 저장소를 새로 만들고 싶어

이미 존재하는 디렉토리를 Git 저장소로 초기화 하려면:

```sh
(my-folder) $ git init
```

### 원격 저장소를 복제해 오고 싶어

원격 저장소를 복제(복사)하려면, 저장소 url을 복사해서 다음 명령을 실행하세요.

```sh
$ git clone [url]
```

이렇게 하면 원격 저장소의 이름과 같은 폴더를 새로 만들고 그 안에 원격 저장소를 저장할 거에요. 복제해 올 원격 서버와 연결되어 있는지 확인하세요. (대부분의 경우 인터넷에 연결되어 있는지 확인하라는 뜻이에요.)

원격 저장소의 이름과 다른 폴더로 복제하고 싶다면 다음 명령어를 실행하세요.

```sh
$ git clone [url] name-of-new-folder
```

## 커밋 수정

<a name="diff-last"></a>
### 내가 방금 어떤 커밋을 남겼지?

조금 전에 별 생각없이 `git commit -a` 명령으로 변경점을 커밋했는데, 뭘 커밋했는지 까물까물 하다고 해 봅시다. 현재 HEAD에서 가장 최근의 커밋 내용을 보려면 이렇게 해 보세요.

```sh
(master)$ git show
```

또는 

```sh
$ git log -n1 -p
```

만약 특정 커밋에 들어있는 특정 파일을 보고 싶다면, 이렇게 할 수도 있어요. (`<commitID>`는 관심을 갖고 있는 그 커밋이에요.)

```sh
$ git show <commitid>:filename
```

### 커밋 메세지를 잘못 썼어

만약 커밋 메시지를 잘못 썼지만 아직 푸시하지는 않았다면, 다음 명령어로 변경점은 그대로 두고 커밋 메시지만 고칠 수 있어요.

```sh
$ git commit --amend --only
```
이 명령어를 사용하면 기본 텍스트 편집기가 열리고 커밋 메시지를 고칠 수 있어요. 다른 방법으로, 한 큐에 처리할 수도 있지요.

```sh
$ git commit --amend --only -m 'xxxxxxx'
```

이미 푸시했다면, 커밋을 고친 뒤 강제 푸시를 할 수 있기는 한데, 별로 추천하진 않아요.

<a name="commit-wrong-author"></a>
### 커밋을 다른 이름과 이메일 설정으로 해 버렸어

하나의 커밋이라면 이렇게 수정해요.

```sh
$ git commit --amend --no-edit --author "New Authorname <authoremail@mydomain.com>"
```

다른 방법으로는, `git config --global author.(name|email)` 명령으로 저자 설정을 정확하게 다시 한 다음  

```sh
$ git commit --amend --reset-author --no-edit
```

만약 전체 이력 변경이 필요하다면, `git filter-branch`의 설명 페이지를 봐요.

### 지난 커밋에서 파일 하나를 지우고 싶어

지난 커밋에서 파일 변경내역을 지우려면, 이렇게 해봐요:

```sh
$ git checkout HEAD^ myfile
$ git add myfile
$ git commit --amend --no-edit
```

그 파일이 새롭게 커밋으로 추가됐고 그 파일을 (단지 Git에서) 지우고 싶은 경우엔,

```sh
$ git rm --cached myfile
$ git commit --amend --no-edit
```

특히나 이 방법은, 작업중인 패치가 있는데 불필요한 파일을 커밋 해서, 강제 푸시로 원격 저장소의 패치를 업데이트 해야 할 때 특히 유용해요. `--no-edit` 옵션은 기존 커밋 메세지를 유지하는데 사용하구요.

<a name="delete-pushed-commit"></a>
### 마지막 커밋을 지우고 싶어

푸시된 커밋을 지우고 싶다면 이걸 따라하면 되는데, 커밋 이력을 되돌릴 수 없는 방법으로 엎어버리며, 또 저장소에서 이미 풀을 받아간 다른 사람의 커밋 이력도 엉망으로 만들 거에요. 간단히 말하자면, 잘 모르겠으면 절대 하지 마세요.

```sh
$ git reset HEAD^ --hard
$ git push --force-with-lease [remote] [branch]
```

아직 푸시 안했으면, 리셋으로 마지막 커밋 전 상태로 돌아가요. (변경점은 스테이지에 두고서)

```
(my-branch*)$ git reset --soft HEAD@{1}
```

이 방법은 푸시를 안 했을 때만 동작해요. 이미 푸시를 했으면, 오롯이 안전한 방법은 `git revert SHAofBadCommit` 한가지 뿐이에요. 
이 방법은 모든 지난 커밋에서 바뀐 점을 거꾸로 되돌리는 새 커밋을 만들 거에요. 또는, 만약 푸시한 브랜치가 리베이스에 안전하다면 (즉 다른 개발자가 거기에서 풀 받지 않는다면), `git push --force-with-lease` 명령어를 쓸 수도 있어요. 
더 알고 싶다면, [이 섹션](#deleteremove-last-pushed-commit)을 참고해주세요.

<a name="delete-any-commit"></a>
### 임의의 커밋 지우기

위 섹션의 경고가 똑같이 적용돼요. 가능하면 이 방법은 절대 쓰지 마세요.

```sh
$ git rebase --onto SHA1_OF_BAD_COMMIT^ SHA1_OF_BAD_COMMIT
$ git push --force-with-lease [remote] [branch]
```

아니면 [대화형 리베이스](#interactive-rebase)를 쓰고, 지우고 싶은 커밋에 해당하는 줄을 지워도 돼요.

<a name="#force-push"></a>
### 수정된 커밋을 푸시했는데, 에러 메세지가 떠

```sh
To https://github.com/yourusername/repo.git
! [rejected]        mybranch -> mybranch (non-fast-forward)
error: failed to push some refs to 'https://github.com/tanay1337/webmaker.org.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

수정된 커밋은, 리베이스(아래를 보세요) 처럼 **기존 커밋을 새걸로 바꾼다는 점**을 항상 생각하세요. 따라서 수정되기 전의 커밋을 이미 원격 저장소로 푸시했다면, 변경된 내용은 강제로 푸시(`--force-with-lease`)해야 해요. 이 작업을 할 때에는 *항상* 브랜치 이름을 정확하게 입력했는지 확인하세요!

```sh
(my-branch)$ git push origin mybranch --force-with-lease
```

일반적으로 **강제 푸시를 쓰지 마세요**. 수정된 커밋을 강제로 푸시하면, 문제의 그 브랜치에서 무언가 작업을 하는 다른 개발자의 소스 이력이나, 그 브랜치에서 따낸 새끼 브랜치에서 충돌을 낼 수도 있어요. 따라서 그냥 새 커밋을 만들어서 푸시하는게 최선이에요. 같은 브랜치에서 다른 사람이 이미 어떤 작업을 했는데, 당신이 올리려는 푸시가 그 다른 사람의 변경점을 덮어쓰는 경우에도 `--force-with-lease` 는 계속 실패할 거에요.

만약 다른 사람이 같은 브랜치에서 작업하지 않는다고 *확신하거나*, 브랜치 선두를 *다른 조건 안 따지고* 바꾸고 싶다면, `--force` (`-f`) 옵션을 쓸 수 있어요. 근데 가능한 하지 마세요.

<a href="undo-git-reset-hard"></a>
### 실수로 하드 리셋을 했는데, 작업하던걸 되살리고 싶어

실수로 `git reset --hard`를 했다고 해도, git은 며칠간은 로그를 보존하고 있으니까, 보통은 그 커밋을 되살릴 수 있어요.

참고: 이건 커밋을 남겼거나 스태시에 저장하는 등, 작업 이력을 백업했을 때에만 유효해요. `git reset --hard` 은 커밋되지 않은 수정사항을 _다 지울 거에요_, 그러니 조심해서 써야해요. (쓰기에는 `git reset --keep` 이 조금 더 안전해요.)

```sh
(master)$ git reflog
```

지난 커밋과 리셋을 위한 커밋을 볼 수 있을 거에요. 돌아가고 싶은 커밋의 SHA 해시를 골라서, 다시 리셋해요:   

```sh
(master)$ git reset --hard SHA1234
```

이제 다시 작업을 시작할 수 있을 거에요.

<a href="undo-a-commit-merge"></a>
### 실수로 머지를 커밋하고 푸시해 버렸어

만약 실수로 병합할 준비가 덜 된 피쳐 브랜치를 메인 개발 브랜치에 병합했어도 되돌릴 순 있어요.
하지만 문제는 있어요: 머지 커밋은 한개 이상의 부모(보통은 두 개)를 가지게 돼요.
 
다음 명령어를 사용하세요

```sh
(feature-branch)$ git revert -m 1 <commit>
```

여기서 -m 1 옵션은 부모 번호 1(머지가 만들어진 브랜치)을 되돌릴 상위 항목으로 선택하라는 뜻이에요.

참고: 부모 번호는 커밋 식별자가 아니에요. 단지, 머지된 커밋은 `Merge: 8e2ce2d 86ac2e7` 이라는 라인을 가지고 있어요. 부모 번호는 이 라인에서 선택하려는 부모의 인덱스에요. 1부터 시작하는 인덱스니까, 첫번째 식별자는 1, 다음은 2 이렇게 이어져요.

<a href="undo-sensitive-commit-push"></a>
### 실수로 공개되면 안 되는 자료를 담은 파일을 커밋하고 푸시했어

만약 공개되면 안 되는 민감한 데이터(비밀번호나 배포용 키 같은거)를 포함한 파일을 푸시했다면, 이전 커밋을 수정하세요. 여하튼 파일이 이미 푸시되었다면, 그 파일 안에 저장되어 있던 데이터는 이미 노출된 것이라고 간주하세요. 다음 절차를 따르면 민감한 데이터를 공개 저장소나 로컬 사본에서는 지울 수 있지만, 다른 사람이 이미 풀 해서 가져간 사본에서는 **삭제할 수 없어요**. 비밀번호를 커밋했다면, **당장 바꾸세요**. 배포용 키를 커밋했다면 **당장 다시 생성하세요**. 민감한 정보를 포함하는 원래 커밋은 아무나 풀로 가져갈 수 있기 때문에, 커밋을 수정하는 것은 땜빵 조치일 뿐이에요.

파일을 수정해서 민감한 데이터를 삭제했다면, 다음을 실행하세요
```sh
(feature-branch)$ git add edited_file
(feature-branch)$ git commit --amend --no-edit
(feature-branch)$ git push --force-with-lease origin [branch]
```

파일을 통째로 지우고 싶다면(물론 로컬에서는 남겨두고), 다음을 실행하세요
```sh
(feature-branch)$ git rm --cached sensitive_file
echo sensitive_file >> .gitignore
(feature-branch)$ git add .gitignore
(feature-branch)$ git commit --amend --no-edit
(feature-branch)$ git push --force-with-lease origin [branch]
```
다른 방법으로는 민감한 데이터를 로컬 환경 변수에 저장할 수도 있어요.

파일을 통째로 지우고 싶다면(로컬에서도), 다음을 실행하세요
```sh
(feature-branch)$ git rm sensitive_file
(feature-branch)$ git commit --amend --no-edit
(feature-branch)$ git push --force-with-lease origin [branch]
```

작업 도중에 다른 커밋을 만들고서야 민감한 데이터가 있다는 것을 깨달았다면 (즉, 민감한 데이터가 몇 개의 커밋 이전에 커밋되었다면), 리베이스를 해야돼요.

## 스테이지

<a href="#i-need-to-add-staged-changes-to-the-previous-commit"></a>
### 스테이지의 변경점을 이전 커밋에 추가하고 싶어

```sh
(my-branch*)$ git commit --amend
```

커밋 메시지를 변경할 필요가 없다면, git에 커밋 메시지를 재활용 하도록 명령하세요.

```sh
(my-branch*)$ git commit --amend -C HEAD
```

<a name="commit-partial-new-file"></a>
### 새 파일 중 전체가 아닌 일부분만 스테이지 하고 싶어.

파일의 일부분만 스테이지 하려면, 보통은 이렇게 해요:

```sh
$ git add --patch filename.x
```

축약된 옵션인 `-p`를 써도 돼요. 이 방식은 대화형 모드를 열텐데요. `s` 옵션을 쓰면 커밋을 나눌 수 있어요. 하지만 새 파일이라면 그런 옵션이 없을거에요. 새 파일을 추가하려면 이렇게 하세요:

```sh
$ git add -N filename.x
```

그 다음, `e` 옵션을 써서 수동으로 추가할 라인을 정할 수 있어요. `git diff --cached`나 `git diff --staged`를 쓰면 로컬에 저장된 부분과 스테이지에 있는 라인들을 비교해서 보여줄 거에요.

<a href="stage-in-two-commits"></a>
### 하나의 파일 변경점을 두개의 다른 커밋에 남기고 싶어

`git add`는 전체 파일들을 커밋에 추가해요. `git add -p`는 추가하려는 변경점을 대화형으로 고를 수 있어요.

<a href="unstaging-edits-and-staging-the-unstaged"></a>
### 아직 스테이지에 안 올라간 변경점을 스테이지에 추가하고, 스테이지에 있는 변경점은 다시 빼고 싶어

이건 좀 꼼수인데요, 제가 발견한 방법은 일단 스테이지 전인 파일들을 스태시에 보관하세요. 그 다음, 리셋해요. 다음, 스태시에 보관한 변경점을 불러오고 스테이지에 추가하세요.

```sh
$ git stash -k
$ git reset --hard
$ git stash pop
$ git add -A
```

## 스테이지 전의 변경점

<a href="move-unstaged-edits-to-new-branch"></a>
### 스테이지 전의 변경점을 새 브랜치로 옮기고 싶어

```sh
$ git checkout -b my-branch
```

<a href="move-unstaged-edits-to-old-branch"></a>
### 스테이지 전의 변경점을 이미 존재하는 다른 브랜치로 옮기고 싶어

```sh
$ git stash
$ git checkout my-branch
$ git stash pop
```

<a href="i-want-to-discard-my-local-uncommitted-changes"></a>
### 내 로컬에 있는 커밋 안된 변경점을 다 무시하고 싶어 (스테이징 됐던 안됐던)

만약 모든 스테이징 됐거나 안 된 변경점을 버리고 싶다면 이렇게 해요:

```sh
(my-branch)$ git reset --hard
# or
(master)$ git checkout -f
```

다음 방법은 `git add`로 스테이징된 모든 파일을 스테이지에서 빼버릴 거에요.

```sh
$ git reset
```

다음 방법은 커밋되지 않은 모든 로컬 변경사항을 되돌릴 거에요. (저장소 최상단 루트에서 실행해야 돼요.)

```sh
$ git checkout .
```

또 커밋되지 않은 변경점들 중 특정 파일이나 디렉토리만 되돌릴 수 있어요.

```sh
$ git checkout [some_dir|file.txt]
```

모든 커밋되지 않은 변경점을 되돌리는 다른 방법도 있어요 (타이핑 칠게 많지만 어떤 하위 디렉토리에서도 돼요):

```sh
$ git reset --hard HEAD
```

이 방법은 추적하지 않은 파일들을 모두 지워요, 그래서 Git에서 추적하는 파일들만 남아요:

```sh
$ git clean -fd
```

`-x` 옵션을 주면 무시된 파일들까지 다 지워요.

### 스테이지 안된 특정 변경 사항을 지우고 싶어

작업 사본에서 전체가 아닌 일부 변경 사항만 제거하고 싶은 때에요.

원치않는 변경점은 체크아웃하고, 제대로 된 변경 사항은 유지하세요.

```sh
$ git checkout -p
# 날리고 싶은 변경 사항에 y를 적으세요 
```

또다른 전략은 `stash`을 같이 쓰는거에요. 챙겨야 하는 변경점을 스테이시 하고, 작업 중인 영역을 리셋하고, 다시 올바른 변경점으로 재적용해요.   

```sh
$ git stash -p
# 저장하고 싶은 사항들을 다 선택하세요
$ git reset --hard
$ git stash pop
```

대안으로, 원치않는 변경점을 스테이시해서 그걸 날리는 방법도 있어요.

```sh
$ git stash -p
# 저장하고 싶지 앟은 사항들을 다 선택하세요
$ git stash drop
```

### 스테이지 안된 특정 파일을 지우고 싶어

작업 영역에서 특정 파일을 지우고 싶을 때.

```sh
$ git checkout myFile
```

대안으로, 작업영역 내 여러 파일들을 지우고 싶을때 모두 나열해서 적어요.

```sh
$ git checkout myFirstFile mySecondFile
```

### 로컬에 있는 스테이지 안된 변경점만 지우고 싶어

모든 스테이징 안된 커밋 전인 변경점을 지우고 싶을 때

```sh
$ git checkout .
```

<a href="i-want-to-discard-all-my-untracked-files"></a>
### 추적되지 않는 파일들 다 지우고 싶어

추적되지 않는 파일들 다 지우고 싶을 땐 

```sh
$ git clean -f
```

<a href="I-want-to-unstage-specific-staged-file"></a>
### 스테이지된 파일 중 일부를 빼 버리고 싶어

때때로 지금까지 커밋된 적이 없는 파일이 실수로 스테이지 되는 경우가 있습니다. 이걸 스테이지에서 빼려면

```sh
$ git reset -- <filename>
```

결과적으로 이 파일은 스테이지에서 빠지고, 추적되지 않는 것처럼 보일 거에요.

## 브랜치

### 모든 브랜치 리스트를 보고 싶어 

로컬 브랜치 다 보기

```sh
$ git branch
```

원격 브랜치 다 보기  

```sh
$ git branch -r
```

로컬과 원격 브랜치 모두 보기

```sh
$ git branch -a
```

<a name="create-branch-from-commit"></a>
### 커밋에서 브랜치 만들기

```sh
$ git checkout -b <branch> <SHA1_OF_COMMIT>
```

<a name="pull-wrong-branch"></a>
### 다른 브랜치에서 풀을 받아와버렸어

이건 잘못된 풀을 받기전 HEAD가 어딜 가르키고 있었는지 볼 수 있는 `git reflog`를 써볼 수 있는 기회에요.

```sh
(master)$ git reflog
ab7555f HEAD@{0}: pull origin wrong-branch: Fast-forward
c5bc55a HEAD@{1}: checkout: checkout message goes here
```

간단히 원하는 커밋으로 브랜치를 되돌릴 수 있어요: 

```sh
$ git reset --hard c5bc55a
```

끝!

<a href="discard-local-commits"></a>
### 로컬의 커밋을 지워서 서버에 있는 내 브랜치와 맞추고 싶어

서버에 변경점을 푸시 안했는지부터 확인해요.

`git status` 가 오리진보다 몇개의 커밋들이 앞서 있는지 보여줄거에요: 

```sh
(my-branch)$ git status
# On branch my-branch
# Your branch is ahead of 'origin/my-branch' by 2 commits.
#   (use "git push" to publish your local commits)
#
```

리셋해서 오리진의 상태와 맞추는 (원격 저장소와 같은 내용물을 갖도록 하는) 방법 중 하나는 이렇게 하면 됩니다:

```sh
(master)$ git reset --hard origin/my-branch
```

<a name="commit-wrong-branch"></a>
### 새 브랜치 대신에 마스터에 커밋을 해버렸어

마스터에 있으면서 새 브랜치를 만들어요:

```sh
(master)$ git branch my-branch
```

마스터 브랜치를 기존 커밋으로 리셋해요:


```sh
(master)$ git reset --hard HEAD^
```

`HEAD^`는 `HEAD^1`의 축약인데요. `HEAD^`의 첫번째 부모를 의미하고, 비슷한 `HEAD^2`는 두번째 부모를 의미해요. (머지는 두 부모를 가질 수 있죠) 

알아두세요 `HEAD^2`는 `HEAD~2`과 같은게 아니에요. (더 자세한 정보는 [이 링크](http://www.paulboxley.com/blog/2011/06/git-caret-and-tilde)를 참고해요 )

다른 방법으로, `HEAD^`를 쓰고 싶지 않다면, 마스터 브랜치로 옮길 커밋 해시를 알아둬요 (`git log`가 재주를 부릴 거에요) 그리고 그 해쉬로 리셋을 해요. `git push`가 원격 저장소에 변경점이 반영되었는지 확인해 줄 겁니다.

예를 들자면, 그 마스터의 커밋의 해쉬가 `a13b85e`라면:

```sh
(master)$ git reset --hard a13b85e
HEAD is now at a13b85e
```

새 브랜치로 체크아웃 해서 계속 작업을 해요:

```sh
(master)$ git checkout my-branch
```

<a name="keep-whole-file"></a>
### 다른 레퍼런스 같은 곳에서 모든 파일을 유지하고 싶어 

스파이크(아래 알아두기 참고) 작업을 하고 있고, 변경점이 수백 개는 나왔다고 가정해보죠. 모든게 제대로 굴러가요. 이제 새 브랜치를 하나 따서 작업을 저장해 두기로 해요.

```sh
(solution)$ git add -A && git commit -m "Adding all changes from this spike into one big commit."
```

스파이크 커밋을 브랜치(아마 기능 브랜치일 수도 있고, `develop` 일 수도 있겠죠)로 옮겨 넣는다고 하면, 모든 파일을 유지하고 싶을 거에요. 큰 커밋을 작게 나누고 싶을거에요.

현재 가지고 있는건:

  * `solution` 브랜치. 스파이크 솔루션을 보관하고 있고, `develop` 브랜치보다 하나 앞선 상태.
  * `develop` 브랜치. 변경점을 추가하려는 곳.

스파이크 솔루션의 내용을 브랜치로 가져오는 것으로 해결할 수 있어요:

```sh
(develop)$ git checkout solution -- file1.txt
```

이렇게 하면 저 파일의 내용을 `solution` 브랜치에서 현재 작업중인 `develop` 브랜치로 가져올 수 있어요.

```sh
# On branch develop
# Your branch is up-to-date with 'origin/develop'.
# Changes to be committed:
#  (use "git reset HEAD <file>..." to unstage)
#
#        modified:   file1.txt
```

그 다음, 평소처럼 커밋해요.

알아두기 : 스파이크 솔루션은 문제를 분석고 해결하려고 만드는 것이에요. 이 솔루션은 문제를 예측하기 위해 사용하고, 관련된 모두가 문제를 확실히 인지하고 나면 스파이크 솔루션은 폐기돼요. ~ [위키피디아](https://en.wikipedia.org/wiki/Extreme_programming_practices).   

<a name="cherry-pick"></a>
### 한 브랜치에 다른 브랜치에 남겼어야 하는 커밋을 여러개 남겼어

마스터 브랜치에 있다고 가정하고 `git log` 해보면 커밋 두개 볼 수 있을거에요:

```sh
(master)$ git log

commit e3851e817c451cc36f2e6f3049db528415e3c114
Author: Alex Lee <alexlee@example.com>
Date:   Tue Jul 22 15:39:27 2014 -0400

    Bug #21 - Added CSRF protection

commit 5ea51731d150f7ddc4a365437931cd8be3bf3131
Author: Alex Lee <alexlee@example.com>
Date:   Tue Jul 22 15:39:12 2014 -0400

    Bug #14 - Fixed spacing on title

commit a13b85e984171c6e2a1729bb061994525f626d14
Author: Aki Rose <akirose@example.com>
Date:   Tue Jul 21 01:12:48 2014 -0400

    First commit
```

각 버그커밋의 해쉬를 가져와요. (21번은 `e3851e8`, 14번은 `5ea5173`)

우선, 마스터 브랜치의 정확한 커밋 (`a13b85e`)으로 리셋해요:

```sh
(master)$ git reset --hard a13b85e
HEAD is now at a13b85e
```

그리고, 21번 버그 작업을 위한 새로운 브랜치를 만들수 있어요:

```sh
(master)$ git checkout -b 21
(21)$
```

그리고 21번 버그 커밋을 *체리픽* 해서 브랜치 최상단에 올려요. 체리픽은 오롯이 그 커밋의 변경점을 지금 헤드에 막바로 적용한다는 뜻이에요.

```sh
(21)$ git cherry-pick e3851e8
```

이 지점에서 충돌이 있을 수도 있어요. 어떻게 충돌을 해결할지 [대화형 리베이스 섹션](#interactive-rebase) 안에 있는 [**충돌이 있어**](#merge-conflict) 부분을 참고하세요.  

자 이제 14번 버그 작업을 위해 마스터로 가서 새 브랜치를 만들어요.

```sh
(21)$ git checkout master
(master)$ git checkout -b 14
(14)$
```

그리고 마지막으로, 14번 버그작업을 위한 커밋을 체리픽해요. 

```sh
(14)$ git cherry-pick 5ea5173
```

<a name="delete-stale-local-branches"></a>
### 업스트림에선 지워진 로컬 브랜치를 지우고 싶어

깃헙에서 풀 리퀘스트를 병합하면, 포크로 가져온 병합 브랜치를 지울지 선택할 수 있어요. 해당 브랜치에 계속 작업할 계획이 없다면, 로컬 사본에서 병합된 브랜치를 삭제해 주어야 작업 사본이 오래된 브랜치로 엉망이 되지 않아 깔끔해요.

```sh
$ git fetch -p upstream
```

여기서, `upstream`은 페치로 가져오려는 원격 저장소에요.

<a name='restore-a-deleted-branch'></a>
### 실수로 브랜치를 지워버렸어

주기적으로 원격 저장소에 푸시한다면, 거의 대부분의 경우 별 문제 없을 거에요. 하지만 여전히 브랜치를 날려먹을 가능성은 있어요. 새 브랜치를 만들고 파일을 하나 만들었다고 해보죠:

```sh
(master)$ git checkout -b my-branch
(my-branch)$ git branch
(my-branch)$ touch foo.txt
(my-branch)$ ls
README.md foo.txt
```

추가하고 커밋해요.

```sh
(my-branch)$ git add .
(my-branch)$ git commit -m 'foo.txt added'
(my-branch)$ foo.txt added
 1 files changed, 1 insertions(+)
 create mode 100644 foo.txt
(my-branch)$ git log

commit 4e3cd85a670ced7cc17a2b5d8d3d809ac88d5012
Author: siemiatj <siemiatj@example.com>
Date:   Wed Jul 30 00:34:10 2014 +0200

    foo.txt added

commit 69204cdf0acbab201619d95ad8295928e7f411d5
Author: Kate Hudson <katehudson@example.com>
Date:   Tue Jul 29 13:14:46 2014 -0400

    Fixes #6: Force pushing after amending commits
```

이제 다시 마스터로 돌아가 '실수로' 브랜치를 지워보죠.

```sh
(my-branch)$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
(master)$ git branch -D my-branch
Deleted branch my-branch (was 4e3cd85).
(master)$ echo oh noes, deleted my branch!
oh noes, deleted my branch!
```

여기에서 업그레이드된 로그 도구인 'reflog'에 익숙해져야 해요. reflog는 저장소에서 발생한 모든 작업의 이력을 보관해요.

```
(master)$ git reflog
69204cd HEAD@{0}: checkout: moving from my-branch to master
4e3cd85 HEAD@{1}: commit: foo.txt added
69204cd HEAD@{2}: checkout: moving from master to my-branch
```

보시다시피 지워진 브랜치의 커밋 해쉬도 볼 수 있어요. 지웠던 브랜치를 살릴 수 있는 지 한번 해보죠.

```sh
(master)$ git checkout -b my-branch-help
Switched to a new branch 'my-branch-help'
(my-branch-help)$ git reset --hard 4e3cd85
HEAD is now at 4e3cd85 foo.txt added
(my-branch-help)$ ls
README.md foo.txt
```

짜잔! 지워진 파일들을 되돌려 놨어요. `git reflog`는 리베이스가 끔찍하게 잘못 됐을때 아주 유용해요.

### 브랜치를 지우고 싶어

원격 브랜치를 삭제하려면:

```sh
(master)$ git push origin --delete my-branch
```

이렇게도:

```sh
(master)$ git push origin :my-branch
```

로컬 브랜치를 삭제하려면:

```sh
(master)$ git branch -d my-branch
```

현재 브랜치나 업스트림에 머지되지 않은 로컬 브랜치를 지우려면:

```sh
(master)$ git branch -D my-branch
```

### 여러개의 브랜치를 지우고 싶어

`fix/`로 시작하는 모든 브랜치들을 지우고 싶다면:

```sh
(master)$ git branch | grep 'fix/' | xargs git branch -d
```

### 브랜치 이름을 바꾸고 싶어

현재 (로컬) 브랜치 이름을 바꾸려면:

```sh
(master)$ git branch -m new-name
```

다른 (로컬) 브랜치 이름을 바꾸려면

```sh
(master)$ git branch -m old-name new-name
```

<a name="i-want-to-checkout-to-a-remote-branch-that-someone-else-is-working-on"></a>
### 다른 사람이 작업중인 원격 브랜치로 체크아웃 하고 싶어

우선, 원격 저장소에서 모든 브랜치를 페치 받아요: 

```sh
(master)$ git fetch --all
```

원격 저장소의 `daves`로 체크아웃 하고 싶다고 하면.

```sh
(master)$ git checkout --track origin/daves
Branch daves set up to track remote branch daves from origin.
Switched to a new branch 'daves'
```

(`--track` 은 `git checkout -b [branch] [remotename]/[branch]` 의 축약이에요)

`daves` 브랜치의 로컬 카피를 줄거에요. 그리고 푸시된 업데이트들도 원격 브랜치로 표시돼요.

### 현재 로컬 브랜치로 새로운 원격 브랜치를 만들고 싶어

```sh
$ git push <remote> HEAD
```

또한 원격 브랜치를 현재 브랜치를 위한 업스트림으로 설정하고 싶다면, 대신 아래 방법을 써봐요:

```sh
$ git push -u <remote> HEAD
```

`push.default` 설정을 `upstream` 모드나 `simple` 모드 (Git 2.0에서 기본값)로 해 두면, 아래 커맨드는 현재 브랜치를 이전에 `-u` 옵션으로 등록한 원격 브랜치로 푸시할 거에요:

```sh
$ git push
```

`git push`의 다른 모드의 동작은 [`push.default` 문서](https://git-scm.com/docs/git-config#git-config-pushdefault)에 설명돼 있어요.

### 원격 브랜치를 로컬 브랜치의 업스트림으로 설정하고 싶어

원격 브랜치를 현재 쓰고 있는 로컬 브랜치의 업스트림으로 설정할 수 있어요:

```sh
$ git branch --set-upstream-to [remotename]/[branch]
# 아니면 짧게:
$ git branch -u [remotename]/[branch]
```

다른 로컬 브랜치에 업스트림 원격 브랜치를 설정하려면:

```sh
$ git branch -u [remotename]/[branch] [local-branch]
```

<a name="i-want-to-set-my-HEAD-to-track-the-default-remote-branch"></a>
### HEAD를 기본 원격 브랜치로 트래킹하도록 설정하고 싶어

원격 브랜치를 확인해보는 것으로, HEAD가 트래킹 중인 원격 브랜치를 볼 수 있어요. 몇몇 경우에는, 원하던 브랜치가 아닐거에요.

```sh
$ git branch -r
  origin/HEAD -> origin/gh-pages
  origin/master
```

`origin/HEAD`를 `origin/master`를 트래킹하는 것으로 변경하려면, 이 커맨드로 실행할 수 있어요:

```sh
$ git remote set-head origin --auto
origin/HEAD set to master
```

### 잘못된 브랜치에서 변경사항을 만들었어

아직 커밋하지는 않았는데 잘못된 브랜치에서 작업하는 것을 깨달았어요. 변경점을 스태시에 보관하고, 올바른 브랜치로 이동해서 다시 적용하세요.

```sh
(wrong_branch)$ git stash
(wrong_branch)$ git checkout <correct_branch>
(correct_branch)$ git stash apply
```

## 리베이스와 병합

<a name="undo-rebase"></a>
### 리베이스/병합한 걸 되돌리고 싶어

현재 브랜치를 잘못된 브랜치로 병합 또는 리베이스 했거나, 리베이스/병합 과정을 제대로 이해하지 못했거나 제대로 끝내지 못했을 거에요. Git은 위험한 작업을 하기 전에 원래의 HEAD 포인트를 ORIG_HEAD라 불리는 변수에 보관해요. 그러니 리베이스/병합 전 상태로 브랜치를 복원하는건 간단해요.

```sh
(my-branch)$ git reset --hard ORIG_HEAD
```

<a name="force-push-rebase"></a>
### 리베이스를 했는데, 강제 푸시하고 싶진 않아

아쉽게도 그런 변경점을 원격 브랜치에 반영하려면 강제 푸시밖에 방법이 없어요. 커밋 이력을 변경했기 때문이죠. 강제 푸시를 하지 않는 이상 원격 브랜치는 변경사항을 받아들이지 않을 거에요. 리베이스 작업흐름 보다는 병합 작업흐름을 이용하는 주된 이유입니다. 큰 팀에선 강제 푸시하는 개발자 새끼때문에 모두가 혼파망을 겪을 수 있어요. 그러니까 리베이스는 조심해서 사용해야 해요.
리베이스를 조금 더 안전하게 쓰려면, 당신이 만든 변경사항을 원격 브랜치에 적용하는 방법 대신, 이렇게 해 보세요.

```sh
(master)$ git checkout my-branch
(my-branch)$ git rebase -i master
(my-branch)$ git checkout master
(master)$ git merge --ff-only my-branch
```

더 확인이 필요하다면, [이 스택오버플로우의 쓰레드](https://stackoverflow.com/questions/11058312/how-can-i-use-git-rebase-without-requiring-a-forced-push)를 참고해요.


<a name="interactive-rebase"></a>
### 커밋 여러개를 하나로 합쳐야 해

`master`에 풀 리퀘스트가 될 브랜치에서 작업하고 있다고 가정해봐요. 가장 간단한 경우로, 원하는게 *모든* 커밋을 하나의 커밋으로 합치고 커밋의 타임스탬프를 버려도 된다면, 그냥 리셋하고 다시 커밋하면 돼요. 마스터 브랜치가 최신이고 모든 변경점이 커밋된 것만 확인한 다음:

```sh
(my-branch)$ git reset --soft master
(my-branch)$ git commit -am "New awesome feature"
```

좀더 세세하게 조정하고 싶고, 시간기록까지 보관하고 싶다면, 대화형 리베이스가 필요할거에요.

```sh
(my-branch)$ git rebase -i master
```

만약 다른 브랜치에서 작업한게 아니라면, `HEAD`와 상대적인 차이를 가지고 리베이스 해야해요. 예로 마지막 2개의 커밋을 쓰가버리고 싶다면 `HEAD~2`를 기준으로 리베이스 하세요. 마지막 3개를 쓰까버리려면  `HEAD~3`을 기준으로 하는 식입니다.

```sh
(master)$ git rebase -i HEAD~2
```

대화형 리베이스를 실행하면 텍스트 에디터로 이런 것들을 볼 수 있을거에요.

```vim
pick a9c8a1d Some refactoring
pick 01b2fd8 New awesome feature
pick b729ad5 fixup
pick e3851e8 another fix

# Rebase 8074d12..b729ad5 onto 8074d12
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

`#`으로 시작하는 줄은 주석이라 리베이스에 영향을 주지 않아요. 

다음으로 `pick` 부분을 다른 명령어로 바꾸거나, 해당하는 라인을 지워서 커밋을 지울 수도 있어요.

예를 들자면 **오래된 (첫번째) 커밋만 두고 두번째 오래된 커밋과 나머지를 다 합치고 싶을때**, 첫번째와 두번째 커밋 제외한 나머지 커맨드들을 `f`로 바꿔야 할거에요:  

```vim
pick a9c8a1d Some refactoring
pick 01b2fd8 New awesome feature
f b729ad5 fixup
f e3851e8 another fix
```

이 커밋들을 합치고 **커밋 이름을 바꾸고 싶다면**, 추가로 적어줘야 해요 두번째 커밋 다음에 `r`를 추가하거나 간단히 `f` 대신 `s`를 추가해주면 될거에요:

```vim
pick a9c8a1d Some refactoring
pick 01b2fd8 New awesome feature
s b729ad5 fixup
s e3851e8 another fix
```

그런 다음에 한번 더 뜨는 텍스트 에디터로 커밋 이름을 바꿀 수 있어요.

```vim
Newer, awesomer features

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# rebase in progress; onto 8074d12
# You are currently editing a commit while rebasing branch 'master' on '8074d12'.
#
# Changes to be committed:
#   modified:   README.md
#
```

전부 다 성공하면, 이런 메세지를 볼거에요:

```sh
(master)$ Successfully rebased and updated refs/heads/master.
```

#### 안전한 병합 전략
`--no-commit`는 병합을 수행하지만, 병합이 실패한 것 마냥 자동 커밋을 하지 않으므로, 커밋하기 전에 병합 결과를 확인하고 추가로 조정할 수 있게 해 줘요. `no-ff` 는 기능 브랜치가 있었다는 증거를 남기고, 프로젝트 이력을 일관되게 유지해 줘요.

```sh
(master)$ git merge --no-ff --no-commit my-branch
```

#### 브랜치를 커밋 하나로 머지해야해 

```sh
(master)$ git merge --squash my-branch
```

<a name="rebase-unpushed-commits"></a>
#### 푸시 되지 않은 커밋만 합치고 싶어

때때로 작업 도중인 커밋을 하나로 합쳐서 업스트림으로 푸시하고 싶을거에요. 이미 업스트림으로 푸시한 커밋을 실수로 하나로 병합하고 싶지는 않을 거에요. 누군가 그 커밋을 반영한 다른 작업을 했을지도 모르니까요.

```sh
(master)$ git rebase -i @{u}
```

이 명령은 아직 푸시하지 않은 커밋만 목록에 넣어서 대화형 리베이스를 실행해요. 그러니 목록 내의 커밋을 재정렬/수정/합치기 해도 안전해요. 

#### 병합을 중단해야해

때때로 병합은 어떤 파일에 문제를 일으킬 수도 있어요, 이 경우 옵션 `abort`으로 현재 충돌 해결 프로세스를 중단하고 병합하기 전 상태로 다시 구성할 수 있어요.

```sh
(my-branch)$ git merge --abort
```

이 명령은 Git 버전 >= 1.7.4 버전부터 쓸 수 있어요.

### 브랜치의 부모 커밋을 바꿔야 해

마스터 브랜치, 마스터에서 따온 기능-1 브랜치, 그리고 기능-1 브랜치에서 따온 기능-2 브랜치가 있다고 해 봅시다. 기능-1 브랜치에 새 커밋을 만들었어요. 그럼 기능-2 브랜치의 부모 커밋은 더 이상 정확하지 않아요 (기능-1 브랜치의 head에서 따 왔으니까, 기능-1 브랜치의 head를 가리키고 있어야 하잖아요.) 이 상황은 `git rebase --onto` 로 해결할 수 있어요.

```sh
(feature-2)$ git rebase --onto feature-1 <the first commit in your feature-2 branch that you don't want to bring along> feature-2
```

이 방법은 아직 병합되지는 않은 다른 기능을 기반으로 한 기능을 만들었는데, 기능-1 브랜치의 버그픽스가 기능-2 브랜치에도 반영되어야 하는 좀 꼬인 상황에 유용해요.

### 브랜치내 모든 커밋이 머지됐는지 확인해

브랜치 내 모든 커밋이 다른 브랜치로 머지됐는지 확인하려면, 그 브랜치들 HEAD (또는 특정 커밋)를 비교해야해요:

```sh
(master)$ git log --graph --left-right --cherry-pick --oneline HEAD...feature/120-on-scroll
```

이 명령은 어디에는 있고 다른덴 없는 커밋이 있나를 알려줄거에요 그리고 브랜치들 사이에 공유되지 않은게 목록을 보여줄 거구요. 다른 옵션은 이렇게:

```sh
(master)$ git log master ^feature/120-on-scroll --no-merges
```

### 대화형 리베이스로 발생가능한 이슈

<a name="noop"></a>
#### 리베이스 편집 화면에서 'noop'

이런 걸 본다면:

```
noop
```

동일한 커밋에 있거나 현재 브랜치보다 앞서 있는 브랜치에 대해 리베이스를 시도한다는 의미에요. 이렇게 해볼 수 있어요:

* 마스터 브랜치가 있어야 할 곳에 있나 확인
* 대신해서 `HEAD~2` 또는 더 기존 항목을 리베이스

<a name="merge-conflict"></a>

#### 충돌이 있어

리베이스를 똑바로 끝내지 못했다면, 충돌을 해결해야 할거에요.

어떤 파일이 충돌났는지 `git status`를 먼저 실행해봐요: 

```sh
(my-branch)$ git status
On branch my-branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

  both modified:   README.md
```

이 예시에선, `README.md` 가 충돌났네요. 파일을 열어서 아래와 같은 부분을 찾아봐요:

```vim
   <<<<<<< HEAD
   some code
   =========
   some code
   >>>>>>> new-commit
```

새로운 커밋으로 추가된 코드(예시에선, 중간 선부터 `new-commit` 까지의)와 `HEAD` 사이에서 차이점을 해결해야 할거에요.

어느 한쪽 브랜치의 코드를 남기고 싶다면, `--ours` 또는 `--theirs`를 쓰면 돼요:

```sh
(master*)$ git checkout --ours README.md
```

- *병합* 할 때, `--ours`를 쓰면 로컬 브랜치의 변경점을 유지하고, `--theirs` 는 다른 브랜치의 변경점를 유지해요.
- *리베이스* 할 땐, `--theirs`가 로컬 브랜치의 변경점을 유지하고 `--ours`는 다른 브랜치의 변경점을 유지해요. 이런 차이에 관한 설명은 Git 정식 문서 중 [이 문서](https://git-scm.com/docs/git-rebase#git-rebase---merge)를 보세요. 

만약 병합이 매우 복잡하면, 시각적으로 차이점을 보여주는 편집기를 쓸 수도 있어요:

```sh
(master*)$ git mergetool -t opendiff
```

코드의 충돌을 해결하고 테스트까지 문제없이 통과했다면, 바뀐 파일 내용을 `git add` 해주고, `git rebase --continue`로 리베이스를 계속 하세요.

```sh
(my-branch)$ git add README.md
(my-branch)$ git rebase --continue
```

모든 충돌을 해결한 내용이 커밋 전과 동일한 트리 구조를 가진다면, 대신에 `git rebase --skip`를 해야 해요.

어느 때건 전체 리베이스를 중단하고 원래 상태의 브랜치로 돌아가고 싶다면, 이렇게 할 수 있어요:  

```sh
(my-branch)$ git rebase --abort
```

<a name="stashing"></a>
## 스태시

### 모든 변경점을 스태시에 보관하기

작업중인 디렉토리에서의 변경한 내용 전부를 스태시에 보관하려면

```sh
$ git stash
```

추적되지 않는 파일까지도 포함하려면, `-u` 옵션을 쓰세요.

```sh
$ git stash -u
```

### 특정 파일들만 스태시에 보관하기

작업 디렉토리에서 한 파일만 스태시에 보관하려면

```sh
$ git stash push working-directory-path/filename.ext
```

작업 디렉토리에서 여러 파일을 스태시에 보관하려면

```sh
$ git stash push working-directory-path/filename1.ext working-directory-path/filename2.ext
```

<a name="stash-msg"></a>
### 메세지와 함께 보관하기

```sh
$ git stash save <message>
```

<a name="stash-apply-specific"></a>
### 목록에서 특정 스태시를 가져와서 적용하기 

우선 스태시 목록과 메시지를 확인하세요.

```sh
$ git stash list
```

그런 다음 리스트에서 특정 스태시를 적용하세요

```sh
$ git stash apply "stash@{n}"
```

여기에서, 'n' 은 스택 안에서 스태시의 위치를 나타내요. 가장 위에 있는 스태시가 0 이에요.


## 찾아보기

### 모든 커밋에서 문자열을 찾고 싶어

특정한 문자열이 포함된 어떤 커밋을 찾으려면, 이런 구조로 쓸 수 있어요:

```sh
$ git log -S "string to find"
```

일반적인 파라미터들은:

* `--source` 각 커밋에 도달한 명령어에 지정된 참조 이름을 보여주는걸 의미해요.

* `--all` 는 모든 브랜치에서 시작하는걸 의미해요.

* `--reverse` 반대의 순서로 출력해요, 변경점의 첫번째 커밋이 보일꺼란 거죠.

<a name="i-want-to-find-by-author-committer"></a>
### 작성자나 커미터를 찾고 싶어

작성자나 커미터의 모든 커밋을 찾으려면 이렇게 쓸 수 있어요:

```sh
$ git log --author=<name or email>
$ git log --committer=<name or email>
```

작성자와 커미터가 같지 않다는 것만 염두해두세요.
`--author`는 코드를 실제로 코드를 작성한 사람이고
반면에 `--committer`는 실제 작성자를 대신해 커밋을 한 사람이에요.

### 특정 파일이 포함된 커밋을 목록화 하고 싶어

특정 파일이 든 모든 커밋을 찾으려면 이렇게 해요:

```sh
$ git log -- <path to file>
```

보통은 정확한 경로를 쓸테지만 와일드 카드로 경로나 파일명을 쓸수도 있어요:

```sh
$ git log -- **/*.js
```

와일드 카드를 쓸 때, 커밋된 파일의 목록을 볼 수 있는 `--name-status`로 확인하는게 유용할거에요: 

```sh
$ git log --name-status -- **/*.js
```

### 커밋을 참조하는 태그를 찾고 싶어

특정 커밋이 포함된 모든 태그를 찾으려면:

```sh
$ git tag --contains <commitid>
```

## 서브모듈

<a name="clone-submodules"></a>

### 모든 서브모듈을 클론하기

```sh
$ git clone --recursive git://github.com/foo/bar.git
```

벌써 클론했다면:

```sh
$ git submodule update --init --recursive
```

<a name="delete-submodule"></a>
### 서브모듈 지우기

서브모듈을 만드는건 아주 간단하지만 지우는건 그렇진 않아요. 필요한 명령어는:

```sh
$ git submodule deinit submodulename
$ git rm submodulename
$ git rm --cached submodulename
$ rm -rf .git/modules/submodulename
```

## 기타 항목들

### 지운 파일 복구하기

우선 그 파일이 마지막으로 있었던 커밋을 찾고:

```sh
$ git rev-list -n 1 HEAD -- filename
```

그런 다음 그 파일을 체크아웃해요 

```
git checkout deletingcommitid^ -- filename
```

### 태그 지우기

```sh
$ git tag -d <tag_name>
$ git push <remote> :refs/tags/<tag_name>
```

<a name="recover-tag"></a>
### 지워진 태그 복구하기

이미 지운 태그를 복구하고 싶다면, 이런 단계를 따라해 볼 수 있어요: 우선, 연결할 수 없는 태그를 찾고:

```sh
$ git fsck --unreachable | grep tag
```

태그의 해쉬를 메모해두세요.
그런 다음 [`git update-ref`](https://git-scm.com/docs/git-update-ref)을 써서 지워진 태그를 복구해요:

```sh
$ git update-ref refs/tags/<tag_name> <hash>
```

이제 태그가 복구돼있을거에요.

### 지워진 패치

만약 깃헙에서 누군가가 풀리퀘스트를 보냈는데 이후 그 사람의 포크를 지워버렸다면, 그 저장소를 복제할 수도 없고 `git am`도 쓸 수 없어요. [.diff, .patch](https://github.com/blog/967-github-secrets) 주소가 날아가 버리니까요. 하지만 PR 자체는 [깃헙의 특별한 참조](https://gist.github.com/piscisaureus/3342247)을 이용해서 확인할 수 있어요. PR#1의 내용을 pr_1이란 새 브랜치로 페치 받으려면:

```sh
$ git fetch origin refs/pull/1/head:pr_1
From github.com:foo/bar
 * [new ref]         refs/pull/1/head -> pr_1
```

### Zip파일로 저장소 내보내기

```sh
$ git archive --format zip --output /full/path/to/zipfile.zip master
```
### 같은 이름의 브랜치와 태그를 푸시하기

로컬 브랜치와 같은 이름의 태그가 원격 저장소에 존재한다면, 일반적인 `$ git push <remote> <branch>` 명령어로 푸시할 때 다음과 같은 오류를 볼 거에요.

```sh
$ git push origin <branch>
error: dst refspec same matches more than one.
error: failed to push some refs to '<git server>'
```

헤드 참조를 푸시한다고 명시하면 해결할 수 있어요

```sh
$ git push origin refs/heads/<branch-name>
```

로컬 태그를 같은 이름의 브랜치가 존재하는 원격 저장소로 푸시하는 경우에도 비슷한 명령어를 쓸 수 있어요.

```sh
$ git push origin refs/tags/<tag-name>
```

## 파일 추적하기

<a href="i-want-to-change-a-file-names-capitalization-without-changing-the-contents-of-the-file"></a>
### 파일 내용엔 변경이 없이 파일 이름을 앞글자만 대문자로 바꾸고 싶어

```sh
(master)$ git mv --force myfile MyFile
```

### Git 풀 받을때 로컬 파일을 덮어씌우고 싶어

```sh
(master)$ git fetch --all
(master)$ git reset --hard origin/master
```

<a href="remove-from-git"></a>
### 파일을 로컬에는 보관하고 Git에서 지우고 싶어

```sh
(master)$ git rm --cached log.txt
```

### 특정한 리비전으로 파일을 복구하고 싶어

복구하고 싶은 해시가 c5f567 이라고 가정하면:

```sh
(master)$ git checkout c5f567 -- file1/to/restore file2/to/restore
```

c5f567 한 단계전으로 복구하고 싶다면, c5f567~1로 적어줘요:

```sh
(master)$ git checkout c5f567~1 -- file1/to/restore file2/to/restore
```

### 커밋이나 브랜치 사이에서 특정 파일의 변경 이력이 필요해

마지막 커밋과 c5f567으로 부터의 차이를 비교하고 싶다고 가정하면:


```sh
$ git diff HEAD:path_to_file/file c5f567:path_to_file/file
```

브랜치도 같은 방법으로:

```sh
$ git diff master:path_to_file/file staging:path_to_file/file
```

### 특정 파일의 변경점을 Git이 무시하도록 하고 싶어

커밋되면 안 되는 민감한 정보를 로컬에서만 저장하는 설정 템플릿이나 다른 파일에 쓰면 유용합니다.

```sh
$ git update-index --assume-unchanged file-to-ignore
```

다만 이 방법은 그 파일을 소스 제어에서 제거하지 *않는다는* 점을 명심하세요 - 단지 로컬에서 무시될 뿐입니다. 이를 취소하고 Git이 다시 변경사항을 확인하게 하려면, 다음 명령어로 무시 플래그를 비우게 하세요.

```sh
$ git update-index --no-assume-unchanged file-to-stop-ignoring
```

## 설정

### Git 명령어 몇 개를 앨리어스 등록하고 싶어

맥OS나 리눅스에는, Git 설정 파일이 ```~/.gitconfig``` 에 있어요. 내가 단축용으로 쓰는 (그리고 오타로 자주 치는) 앨리어스를 예시 삼아 ```[alias]``` 섹션에 추가해 봤어요.

```vim
[alias]
    a = add
    amend = commit --amend
    c = commit
    ca = commit --amend
    ci = commit -a
    co = checkout
    d = diff
    dc = diff --changed
    ds = diff --staged
    f = fetch
    loll = log --graph --decorate --pretty=oneline --abbrev-commit
    m = merge
    one = log --pretty=oneline
    outstanding = rebase -i @{u}
    s = status
    unpushed = log @{u}
    wc = whatchanged
    wip = rebase -i @{u}
    zap = fetch -p
```

### 저장소에 빈 디렉토리를 추가하고 싶어

못해요! Git은 빈 디렉터리를 지원하지 않거든요. 근데 꼼수가 있어요. 디렉토리에에 .gitignore 파일을 아래 내용으로 만들어요:  

```
 # Ignore everything in this directory
 *
 # Except this file
 !.gitignore
```

다른 일반적인 규칙은 그 폴더 안에 .gitkeep이라는 이름의 빈 파일을 만드는 거에요.

```sh
$ mkdir mydir
$ touch mydir/.gitkeep
```

.keep이란 이름으로도 쓸 수 있는데요, 두번째 라인이 ```touch mydir/.keep```가 되어야겠죠.

### 저장소 유저명과 비밀번호를 캐시해두고 싶어

인증이 필요한 저장소를 가지고 있을 텐데요.
이런 경우 유저명과 비밀번호를 캐시할 수 있을테니 매번 푸시/풀 할 때마다 입력할 필욘 없어요.
크리덴셜 헬퍼가 해줄거에요.

```sh
$ git config --global credential.helper cache
# Set git to use the credential memory cache
```

```sh
$ git config --global credential.helper 'cache --timeout=3600'
# Set the cache to timeout after 1 hour (setting is in seconds)
```

### Git이 권한과 파일모드 변경을 무시하게 만들고 싶어   

```sh
$ git config core.fileMode false
```

이 것을 로그인된 유저의 기본 행위로 설정으로 해두려면, 이렇게 써요: 

```sh
$ git config --global core.fileMode false
```

### 글로벌 유저를 설정해두고 싶어

모든 로컬 저장소에서 사용되는 유저 정보를 설정하려면, 그리고 버전 이력을 리뷰할때 알아보기 쉬운 이름으로 설정하려면: 

```sh
$ git config --global user.name “[firstname lastname]”
```

각 이력 생산자에게 연관해서 이메일 설정을 해주려면:

```sh
git config --global user.email “[valid-email]”
```

### Git에 명령줄 색상을 넣고 싶어

손 쉬운 리뷰를 위한 Git 명령줄 자동 색상을 설정 하려면:

```sh
$ git config --global color.ui auto
```

## 뭘 잘못했는지 모르겠어

음, 망했군요. 뭔가를 `reset` 했거나, 잘못된 브랜치에 병합했거나, 강제 푸시를 했는데 커밋을 못 찾고 있는 모양이군요. 알다시피, 어떤 시점에선, 모든게 괜찮았고, 그 시점으로 돌아가고 싶겠죠.

이게 바로 `git reflog`의 존재이유에요.  `reflog` 는 브랜치 끝에 가해지는 변경점을 모두 보관해요. 그 브랜치 끝이 브랜치 이름이나 태그에 의해 참조되지 않더라도 말이죠. 기본적으로, HEAD가 변경될 때마다 reflog에 새로운 항목이 추가돼요. 아쉽게도 이 기능은 로컬 저장소에서만 동작하고, 오직 움직임만을 트래킹해요 (예를 들자면, 어디에도 기록되지 않았던 파일의 변경사항은 추적되지 않아요)

```sh
(master)$ git reflog
0a2e358 HEAD@{0}: reset: moving to HEAD~2
0254ea7 HEAD@{1}: checkout: moving from 2.2 to master
c10f740 HEAD@{2}: checkout: moving from master to 2.2
```

위의 reflog는 마스터에서 2.2 브랜치로 체크아웃하고 되돌린 것을 보여주네요. 그 뒤에, 더 오래된 커밋으로 하드리셋을 했어요. 가장 최근의 활동은 가장 위에 표시되고, `HEAD@{0}` 라벨로 표시돼요.

잘못해서 뒤로 옮겨간 것이라면, reflog는 당신이 실수로 2커밋을 날려버리기 전에 마스터가 가리키고 있던 (0254ea7) 커밋을 보관하고 있을 거에요.

```sh
$ git reset --hard 0254ea7
```

`git reset`을 쓰는 것으로 이제 마스터를 이전 커밋으로 되돌릴 수 있어요. 이력이 실수로 변경됐을 때의 안전그물을 제공할 거에요.  

([여기](https://www.atlassian.com/git/tutorials/rewriting-history/git-reflog)에서 복제해와 수정했어요).


# 다른 리소스

## 도서

* [Learn Enough Git to Be Dangerous](https://www.learnenough.com/git-tutorial) - A book by Michael Hartl covering Git from basics
* [Pro Git](https://git-scm.com/book/en/v2) - Scott Chacon and Ben Straub's excellent book about Git
* [Git Internals](https://github.com/pluralsight/git-internals-pdf) - Scott Chacon's other excellent book about Git

## 튜토리얼

* [19 Git Tips For Everyday Use](https://www.alexkras.com/19-git-tips-for-everyday-use) - A list of useful Git one liners
* [Atlassian's Git tutorial](https://www.atlassian.com/git/tutorials) Get Git right with tutorials from beginner to advanced.
* [Learn Git branching](https://learngitbranching.js.org/) An interactive web based branching/merging/rebasing tutorial
* [Getting solid at Git rebase vs. merge](https://medium.com/@porteneuve/getting-solid-at-git-rebase-vs-merge-4fa1a48c53aa)
* [Git Commands and Best Practices Cheat Sheet](https://zeroturnaround.com/rebellabs/git-commands-and-best-practices-cheat-sheet) - A Git cheat sheet in a blog post with more explanations
* [Git from the inside out](https://codewords.recurse.com/issues/two/git-from-the-inside-out) - A tutorial that dives into Git's internals
* [git-workflow](https://github.com/asmeurer/git-workflow) - [Aaron Meurer](https://github.com/asmeurer)'s howto on using Git to contribute to open source repositories
* [GitHub as a workflow](https://hugogiraudel.com/2015/08/13/github-as-a-workflow/) - An interesting take on using GitHub as a workflow, particularly with empty PRs
* [Githug](https://github.com/Gazler/githug) - A game to learn more common Git workflows

## 스크립트와 도구

* [firstaidgit.io](http://firstaidgit.io/) A searchable selection of the most frequently asked Git questions
* [git-extra-commands](https://github.com/unixorn/git-extra-commands) - a collection of useful extra Git scripts
* [git-extras](https://github.com/tj/git-extras) - GIT utilities -- repo summary, repl, changelog population, author commit percentages and more
* [git-fire](https://github.com/qw3rtman/git-fire) - git-fire is a Git plugin that helps in the event of an emergency by adding all current files, committing, and pushing to a new branch (to prevent merge conflicts).
* [git-tips](https://github.com/git-tips/tips) - Small Git tips
* [git-town](https://github.com/Originate/git-town) - Generic, high-level Git workflow support! http://www.git-town.com

## GUI 클라이언트
* [GitKraken](https://www.gitkraken.com/) - The downright luxurious Git client,for Windows, Mac & Linux
* [git-cola](https://git-cola.github.io/) - another Git client for Windows and OS X
* [GitUp](https://github.com/git-up/GitUp) - A newish GUI that has some very opinionated ways of dealing with Git's complications
* [gitx-dev](https://rowanj.github.io/gitx/) - another graphical Git client for OS X
* [Sourcetree](https://www.sourcetreeapp.com/) - Simplicity meets power in a beautiful and free Git GUI. For Windows and Mac.
* [Tower](https://www.git-tower.com/) - graphical Git client for OS X (paid)
* [tig](https://jonas.github.io/tig/) - terminal text-mode interface for Git
* [Magit](https://magit.vc/) - Interface to Git implemented as an Emacs package.
* [GitExtensions](https://github.com/gitextensions/gitextensions) - a shell extension, a Visual Studio 2010-2015 plugin and a standalone Git repository tool.
* [Fork](https://git-fork.com/) - a fast and friendly Git client for Mac (beta)
* [gmaster](https://gmaster.io/) - a Git client for Windows that has 3-way merge, analyze refactors, semantic diff and merge (beta)
* [gitk](https://git-scm.com/docs/gitk) - a Git client for linux to allow simple view of repo state.
* [SublimeMerge](https://www.sublimemerge.com/) - Blazing fast, extensible client that provides 3-way merges, powerful search and syntax highlighting, in active development.
