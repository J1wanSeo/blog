---
title: AI Accelerator용 보드 구매기
updated: 2024-02-19 06:23:38Z
created: 2024-02-19 03:32:26Z
latitude: 37.56653500
longitude: 126.97796920
altitude: 0.0000
---

# Background

디지털 회로 설계 엔지니어가 되고싶다는 마음에 프로젝트를 하나 직접 수행해 보면 좋을 것 같다는 생각을 했다.  
그렇다면 FPGA 보드를 우선 구매해야 이를 직접 테스트할 수 있을 것 같다는 생각에 FPGA 보드 종류를 여러가지 검색해 보았다. 제품을 구매하는 기준은 아래와 같았다.

# Standards

1.  자일링스 기반이었으면 함
2.  내가 FPGA에 올리고 싶은 프로그램 = AI 이므로 성능이 어느정도 보장되었으면 좋겠음
3.  가격이 너무 비싸지 않았으면 함 .. → 중고거래로 합리적인 가격이면 괜찮음
4.  IDE에 대한 강좌가 잘 있었으면 좋겠음,
    1.  나름 보편적으로 사람들이 사용하는 기기여야 문제가 발생하였을 때 참고할만한 내용이 많을 것이라 생각함.

위와 같은 기준으로 보드를 찾아보고 있는데 나와 비슷한(?) 상황에 놓인 인터넷 게시글을 발견하였다.  
[\[질문\]2020.12.13 18:42 FPGA 설계에 대해서 질문드립니다.](https://gigglehd.com/gg/hard/8936873)

해당 글의 댓글들을 읽어보니 Zybo라는 보드가 나름 성능적 측면에서 나쁘지 않다는 것을 확인하였다. 추가적으로 웹서칭을 진행해 보니 Nexys 라는 계열의 보드도 있길래 두 보드를 한 번 비교해 보았다. 두 제품 모두 자일링스 칩셋 기반에 Digilent라는 회사에서 만드는 보드여서 해당 홈페이지 웹사이트에서 스펙을 비교해보았다.  
*우선 Zybo Z7를 구매한다면 z7-20 보드를 구매할 예정이라 해당 스펙으로 비교하였음*

![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/9aa1f9f5-bd0c-4900-bc3f-41ce69d053b6)
![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/bbf95506-4490-4f12-9a0e-53a6727be01a)

아무래도 User I/O 부분에서는 Nexys A7이 더 많은 지원항목을 보여주었다.  
중점적으로 사용하는 칩셋에서 차이가 발생하는 것을 확인할 수 있었는데, 해당 내용을 좀 더 찾아보았다.  
Nexys A7의 경우 Xillinx 의 Artix를 사용한다.  
Artix 7의 경우 [Xillinx 의 FPGA 칩셋](https://www.xilinx.com/products/silicon-devices/fpga.html) 중 하나인데, 28nm 공정을 사용한 FPGA 이다.

반면 Zybo Z7 의 경우 Zynq 7020 칩셋을 사용하며 이는 [Xillinx 의 SoC](https://www.xilinx.com/products/silicon-devices/soc.html) 중 하나이다.  
어떤 차이가 존재하는 지 궁금해서 찾아보니, Zynq의 경우 SoC 로서 ARM Cortex A9을 메인으로 사용하고, FPGA에서 사용하는 메인 함수들을 추가적으로 지원하고 있다.  
*이미지 클릭 시 해당 공식 문서로 이동*  
[![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/d3a30f63-9a94-4340-9e99-2113a85cc612)](https://www.xilinx.com/content/dam/xilinx/support/documents/product-briefs/zynq-7000-product-brief.pdf)

이러한 내용을 바탕으로 가격대가 조금 더 있지만 추후 범용성을 생각하여 Zybo Z7을 구매할 것 같다.

# PYNQ

아무래도 가격대가 있다 보니 조금 더 저렴하게 구매할 수는 없을까? 해서 알리익스프레스 에도 검색 해 보았다.  
찾다보니 zynq 칩셋을 이용한 pynq라는 것을 발견하였고 이게 무엇인가 궁금하여 인터넷에 찾아보니 [공식문서](https://github.com/Xilinx/PYNQ_Workshop/blob/master/01_PYNQ_Workshop_introduction.pdf)가 있었다.

![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/e72ab886-a349-4b6b-a6e1-94c1aecb03ed)

자일링스(Xilinx)에서 Python 을 활용하여 FPGA를 개발할 수 있도록 만든 프레임워크의 한 종류이고, 해당 보드 종류에 맞게 업로드 하면 네트워크로 Jupyter Notebook을 방문하여 사용할 수 있도록 만든 것이다.

공식 문서에서 제공하는 PYNQ Z2 보드는 하기와 같은 스펙을 가지고 있다.

![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/e8da97a2-38f0-47ca-be56-3ac6f5902dfb)

메모리는 512 MB 로 절반이고 기타 I/O도 다른 것을 확인할 수 있었다.
같은 칩셋과 사용하고 저렴하여 TUL의 PYNQ -Z2 를 구매하기로 결정

국내 사이트 들에서는 가격이 생각보다 비싸서  (40만원대) [공식 링크](https://www.tulembedded.com/FPGA/ProductsPYNQ-Z2.html)에 있는 [element14](https://kr.element14.com/tul-corporation/1m1-m000127dev/eval-board-32bit-arm-cortex-a9/dp/3605842?CMP=e-email-sys-orderack-GLB)에서 구매하기로 결정했다.
![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/5cb9671a-a251-4825-9532-4ac363830b5a)

18.5 만원대 면 훨씬 저렴하다고 생각이 들고.. 부품 오기 전 까지 열심히 공부해야겠다.
아 원화 결제라 달러결제 하고 싶다고 이야기 했는데 안된다는(...)  답변만 받았다.

![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/95ea3bc7-efca-4e0c-97f0-5a2e5378c8c0)