---
layout: post
title: DRC errors
updated: 2023-12-05 13:47:49Z
date: 2023-11-09 02:33:21Z
latitude: 37.24108640
longitude: 127.17755370
altitude: 0.0000
categories: Cadence
---

- off-grid error
    - layout에서 e 눌러서 X/Y Snap spacing 을 너무 작게 하면 발생
    - ![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/ada5c227-b042-4630-93c3-47134156e279)

        - 0.005로 설정시 발생하였음
        - ![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/08f28d8b-a8d7-462e-9733-e728e90ab0dc)
        - 상기 설정이 이미 설계된 nand2의 설정값
- poly contact 과 metal via는 같은 곳에 만들면 안된다,
    - 따로 떨어뜨려서 제작해야함
    - ![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/ce9c1e9c-c5a3-4134-8179-b85a569ee48c)
- contact-via 만들기
    - ![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/cfb499ce-5eac-43c4-bfff-8df67837d160)
    - 위에서 Mode의 2번째인 Stack을 활용하면 한번에 여러층의 via 를 만들 수 있다.  
        ![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/03b5b2b7-3a7b-4a5e-a3a9-c91444f4949c)
> contact or via에서 metal 의 minimum area를 늘리라고 DRC 에러가 발생하는 경우 row 나 col 을 늘려서 via/contact 의 사이즈를 키워주면 된다.

![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/817c94c7-2114-46ed-9604-d9c6e10f5ebd)
- 상기 error 발생 시 ntap or ptap ( VDD VSS )의 row 나 col을 늘려주어 사이즈를 키우면 된다.