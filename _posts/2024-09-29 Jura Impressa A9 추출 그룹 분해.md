---
title: Jura Impressa A9 추출 그룹 분해
layout: post
date: 2024-09-29 04:02:26Z
created: 2024-09-29 02:40:00Z
categories: Jura
latitude: 37.56653500
longitude: 126.97796920
altitude: 0.0000
---

## 개요

* * *

어쩌다 보니 Jura(유라)의 커피머신 Impressa A9 를 가지게 되었다.  
문제는 해당 제품이 북미향 제품이라 120V를 지원하다는 점이었다.

나름 전공공부(?)도 할 겸 분해를 해서 120V → 230V 변환을 시켜보자고 시작하는 내용 이다.

우선 분해의 대표주자인 ifixit.com 을 참고한 결과 다행히도 분해하는 방법이 적혀있었다.

그러므로 대부분의 분해 방법은 해당 링크를 참고하면 될 듯하다.

https://ko.ifixit.com/Teardown/Jura+Impressa+A9+Teardown/62543?srsltid=AfmBOopOugPwlfDzD_JhLLqLIQdRIkTmVy-FAqLwBFIenWs_3jkDe3H9

생각보다 많은 힘을 필요로 하니.. 개인적으로 별나사가 많아 힘들었다.

손이 잘 안들어가서 결국에는 쿠팡에서 전동 드라이버용 별나사 비트를 사서 해결했다.  
https://www.coupang.com/vp/products/7970106867

분해 후 정확하게 어떤 부품이 있나 확인해 보기 위해 찾아본 결과 부품의 정보가 들어있는 pdf 가 있었다.

해당 도면을 참고한 결과 바꾸어야 되는 부품으로는

* * *

1.  ## 120V Transformer
    

![36ccfa9e585d7cd1e9292f6d7c2e9b96.png](../../_resources/36ccfa9e585d7cd1e9292f6d7c2e9b96.png)

120V 를 15.5V/1.1A or 9V/0.5A 로 바꾸어 주는 것 같다.

2.  ## Grinder Motor (DOMEL 482.3.504)
    

Transformer를 거치지 않고 120V/230V 가 직접 들어가는 것 같다.  
![b94b1c67e13e62ad7eb4cd64a684221c.png](../../_resources/b94b1c67e13e62ad7eb4cd64a684221c.png)

3.  ## Water Pump Motor (SYSKO.SAP.HP4)
    

2번과 마찬가지로 120V/230V 가 직접 들어가는 듯 하다.

![6bc80f5440ebeb49b4ce60eaa102a5ad.png](../../_resources/6bc80f5440ebeb49b4ce60eaa102a5ad.png)

4.  ## PCB
    

파워보드가 기본적으로 120V를 입력으로 받아서 사용하게 되고, 이 때문에 바꾸어 주어야 하는 것 같다(?) 는 의심이 든다. 근데 안에 존재하는 VAC가 16A250V 라고 쓰여있는 거로 봐서는 공통적으로 사용되는 부품인 것 같기도 하다.

![1492087b285ad0d5983aad5629e821a3.png](../../_resources/1492087b285ad0d5983aad5629e821a3.png)

![6695f6f140789891da8c82bcfef009c9.png](../../_resources/6695f6f140789891da8c82bcfef009c9.png)

다른 사이트에 존재하는 230V PCB 부품, 대략적인 구조와 부품이 동일 한 것을 찾아볼 수 있다.  
하지만 검증된 것은 아니다.

빨간색 박스로 칠한 것이 파나소닉의 ALZ51B12인데, 해당 파트가 파워 릴레이로 회로의 안전을 담당하며 스위칭 해주는 역할이라고 한다. 데이터 시트를 보면 250VAC 까지 가능한 거로 봐서는 호환되는 모양새 이다. 아마 해당 전압을 PCB를 통해 다른 하위 부품에 뿌려주는 방식인 것 같다.  
![6e490256736ca87a06bfe15590e568f5.png](../../_resources/6e490256736ca87a06bfe15590e568f5.png)

아쉬운 점은 해당 PCB Schematic 이 있으면 훨씬 쉬울 것 같은데 이게 없다는 점이다.

5.  ## 기타
    

![205c1e9e03d332c051c6784162910936.png](../../_resources/205c1e9e03d332c051c6784162910936.png)

Gear Motor가 12V를 사용하는것으로 보았을 때 Encoder/Gear Motor 는 바꿀 필요가 없는 것 같다.

(위 사진에서 1012 부분)

제어 방식은 내부에 존재하는 PCB 를 통해서 하는 것 같다.

* * *

## 결론

결국 나의 생각으로는 PCB 를 제외하고 3개를 바꾸면 될 것 같은데 해외 사이트에서 부품을 검색해보니 새 제품으로 하는 경우에는 이미 $200 을 넘는다. 공학도라면 이윤추구를 먼저 생각해야 되기 때문에 굳이 손해나는 일을 할 필요는 없는 것 같다. 덕분에 대략적인 제품들의 파워 구조를 알게 되었으니 지적 호기심 추구는 이미 달성한 듯 싶다.

: 중고로 하나 사는게 더 저렴해서 안바꾼다.