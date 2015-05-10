---
layout: post
title:  Spring - Servlet Filter 와 @ModelAttribute
categories: Spring
---

이번에 내가 담당하는 사이트의 내부 보안검수를 받았는데 특정 URL에서 크로스 사이트 스크립팅(이하 XSS) 공격 위험성이 있다는 진단을 받았다. 이 프로젝트는 Spring 기반으로 작성된 프로젝트로서 XSS 방어용 Servlet Filter 를 등록해놨기 때문에 예상치 못한 진단에 문제가 되는 해당 URL에 Mapping 되는 Controller 메서드들을 살펴보았는데 하나같이 전부 @ModelAttribute를 사용하는 곳이었다.
