---
title: "오디오 분류 시작"
layout: post
date: 2022-04-18 20:19:00 +0900
category: KB(Bank)-IT-Academy
---

## 보이스피싱을 분류할 수 있을까?

![image](https://user-images.githubusercontent.com/26592315/163797389-bab77d6f-db13-442f-a6e7-91626ac62aca.png)

- 미래에는 점차 AI 은행원이 기존의 행원분들을 대체
- 그에 따른 ( 기존 행원분들이 막아낼 수 있었던 ) 보이스피싱을 AI 행원들도 막아내기 위해서는 어떠한 기능이 들어가야 할까?

첫번째 방법은 목소리 구분이다. 긴장과 불안의 목소리를 구분을 해서 보이스피싱 혹은 사건사고를 방지하는 것이다.

## 데이터 수집

DCASE, AudioSet, Urban Sound, FSD, Freesound 에 다량의 데이터를
보유하고 있으면서 데이터 저작권 사용이 가능한 사이트 선정(예: FreeSound)

## 음성 분류 연습

[wget 다운로드 받는 사이트(64bit EXE 파일)](https://eternallybored.org/misc/wget/)

- cmd 창에서 `echo %PATH%` 입력 후 C:\WINDOWS\system32 가 등록되어 있는 확인 후, 위에서 다운받은 wget 파일을 system32 폴더로 복사하면 wget 명령어를 window에서도 사용가능합니다.

- [wmv 파일, 음성 분류 연습 데이터](https://www.dropbox.com/s/3dsnj5ldtf3dcx4/GeneralMidi.wav)
  - wmv 파일에는 128개 악기와 46개 타악기의 음을 50개씩 2초 간격으로 존재
