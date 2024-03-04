---
title: 'PYNQ Z2 Project with Xilinx Vivado (1)'
layout: post
date: 2024-03-04 11:11:19Z
created: 2024-03-04 11:11:19Z
categories: Zynq
tags:
  - [ FPGA, SoC ]
use_math: true
latitude: 37.56653500
longitude: 126.97796920
altitude: 0.0000
---

ref : [Tutorial: Creating a hardware design for PYNQ](https://discuss.pynq.io/t/tutorial-creating-a-hardware-design-for-pynq/145)

# Intorduction
- 혹시나 PYNQ Z2 보드를 구매한 뒤 Vivado 를 사용하여 프로젝트를 수행하고자 하는 사람들을 위해 남겨놓는 문서이다.
- 시작에 앞서 필요한 파일들은 링크를 걸어두었으므로 참고하길 바란다.

# Index
- Vivado Installation
- Install PYNQ Z2 vivado board files to folder which Vivado installed
- Create New Project with installed board file

# Vivado Installation

Vivado를 설치하는 방법은 [Vivado Homepage](https://www.xilinx.com/support/download.html)에서 다운로드 이후 Installation setup 만 수행하면 되므로 *생략*

# Install PYNQ Z2 vivado board files to folder which Vivado installed

우선 Vivado에서 사용할 수 있도록 PYNQ Z2 보드의 HW 정보를 담은 [board file](https://dpoauwgwqsy2x.cloudfront.net/Download/pynq-z2.zip)을 PYNQ official site에서 다운로드 한다.


![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/b92b5bf3-dd9e-4b11-9b8a-e0a23a617f2c)

이후 압축을 해제하여 Vivado 설치 폴더에 해당 파일을 넣는다.

이 때 해당하는 경로는 Vivado 의 Version에 따라 다르다.

2023.1 의 경우에는  

`
C:\Xilinx\Vivado\2023.1\data\xhub\boards\XilinxBoardStore\boards\Xilinx
`

이전의 경우에는

`
C:\Xilinx\Vivado\2021.2\data\boards\board_files
`

이 때 board_files 폴더가 존재하지 않으면 만들어서 넣으면 된다.

ref_site: [PYNQ-Z2 (Zynq) board not listed as a target board on Vivado 2019.2 free web version](https://support.xilinx.com/s/question/0D52E00006hpMCUSA2/pynqz2-zynq-board-not-listed-as-a-target-board-on-vivado-20192-free-web-version?language=en_US)

# Create New Project with installed board file

![image](https://github.com/J1wanSeo/j1wanseo.github.io/assets/106726102/d80c6199-08e7-4bea-a1e5-0a48a59f802b)

Vivado 를 실행시키고, New Project > RTL Project 를 선택하고 Next 를 누르면 Default Part를 고르는 창이 나타난다.

이 때, 좌측 탭에서 Boards를 고르고 Search 에 pynq 를 검색하면 pynq-z2가 나타나며 이를 선택하면 된다.