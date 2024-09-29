---
title: Linux Vivado 설치 시 에러..  generating installed device list
date: 2024-03-07 05:46:55Z
created: 2024-03-07 05:39:58Z
latitude: 37.56653500
longitude: 126.97796920
altitude: 0.0000
tags:
  - [ FPGA, Linux, Xilinx ]
use_math: true
---

Linux에서 Vivado를 설치할 때 파일 다운로드 이후 설치 이후 세번째 단계에서 generating installed device list 를 나타내며 진행되지 않는 경우 해결방법

1. 우선 Vivado installer를 실행시킨 터미널에  Ctrl + C. 를 눌러 설치를 강제 종료 시킨다.

![Screenshot 2024-03-07 at 14.41.58.jpg](_resources/Screenshot%202024-03-07%20at%2014.41.58.jpg)

2. 해당 터미널에서 라이브러리 2개를 설치한다.
> sudo apt update
sudo apt upgrade
sudo apt install libncurses5
sudo apt install libtinfo5
sudo apt install libncurses5-dev libncursesw5-dev
sudo apt install ncurses-compat-libs

3. 자신이 설치한 Vivado 경로에 맞게 해당 내용을 입력하여 installed_devices.txt를 생성한다.

나의 경우 /tools/Xilinx/ 가 기본 경로로 설정되어 해당 경로에서 설치하였음

> /tools/Xilinx/Vivado/2023.2/bin/vivado -nolog -nojournal -mode batch -source /tools/Xilinx/Vivado/2023.2/scripts/sysgen/tcl/xlpartinfo.tcl -tclargs /tools/Xilinx/Vivado/2023.2/data/parts/installed_devices.txt

4. /tools/Xilinx/Vivado/2023.2/bin/ 에 들어가서 ./vivado 명령어를 통해 실행시키면 된다.

ref: https://support.xilinx.com/s/question/0D52E00006iHjbcSAC/vivado-20211-installation-hangs-at-generating-installed-device-list?language=ja