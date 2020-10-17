---
title: 우분투 서버 한글화 절차
description: 구 블로그에서 가져옴
date: 2015-09-20
slug: locale_setting
image: ubuntu.png
draft: false
categories:
    - Server
---
    apt-get install language-pack-ko
    locale-gen ko_KR.UTF-8
    LANG=ko_KR.URF-8
    LANGUAGE=ko_KR:ko:en_GB:en
그후 `/etc/default/locale` 에다가

    LANG=ko_KR.UTF-8
추가해준뒤 재부팅

`locale` 커맨드로 `ko_KR.UTF-8`가 제대로 설정되었는지 확인.

14.04버전 기준이다.
Debian계열에선 전부 작동한다.