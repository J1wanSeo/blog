---
layout: post
title: parameterized cell 수정 불가능 에러
date: 2023-11-07 15:30:31+09
created: 2023-11-07 15:23:56Z
latitude: 37.24108640
longitude: 127.17755370
altitude: 0.0000
categories: Cadence
---

![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/236126d0-91dc-4ea7-988c-8a87e00d4dfa)

이미 주어진 nand2, nand3를 연결해서 사용하려고 하니 해당 에러가 나타났음

이런 에러가 발생하는 경우:
- layout 에서 i를 눌러서 불러와서 사용하였음
	- 이렇게 하면 pcell이 잠긴 상태로 불러와져서 수정이 불가능하다.
- 해결방법
	- library manager에서 해당 layout에 들어간 이후에 원하는 것을 c 눌러서 복사하고, 내가 사용하려고 하는 layout 에 붙여넣기 해야함

![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/273ac576-4f49-49b3-b489-c1b19c4dda67)

- 우리가 수정하려는 것이 잠긴 경우에 해결하는 방법
> Library Manager
> File &rarr; open shell window
> clsAdminTool
> are .
> ale .


![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/66222014-7465-44c1-b4da-a332f1d17563)