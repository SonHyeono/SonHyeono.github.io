---
title: "AI 행원을 위한 음성인식"
layout: post
date: 2022-04-16 18:49:00 +0900
category: KB-IT-Academy
---

음성인식 API(Web Speech API)는 크게 [SpeechSynthesis](https://developer.mozilla.org/en-US/docs/Web/API/SpeechSynthesis) (Text-to-Speech)와 [SpeechRecognition](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition) (Asynchronous Speech Recognition) 두 가지로 나뉩니다.

- SpeechSynthesis는 텍스트를 음성으로 변환하는 API
- SpeechRecognition은 음성을 텍스트로 변환하는 API

SpeechRecognition은 크롬에서만 지원

- 크롬에서 음성인식 API는 서버 엔진을 통해서 제공되기 때문에 오프라인에서는 지원되지 않습니다.
