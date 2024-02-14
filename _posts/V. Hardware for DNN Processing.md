1.  MAC (multiply and accumulate) Operation을 얼마나 최적화 하여 수행하는지가 중요
    1.  병렬 구조로 구성되기 쉬우며 얼마나 효과적으로 병렬 구조를 가지는 지가 중요하다.
        1.  temporal architecture
            1.  vector (SMD) & parallel thread (SIMT)
                1.  ALU 전체를 중앙에서 제어하는 방식으로 사용한다.
                2.  memory에서 데이터를 받아 처리하는 역할을 수행하며 서로 통신하는 것은 아님
                
        2.  spatial architecture
            1.  ALU가 자체적인 control을 가질 수 있으며 필요에 따라 memory(scratch pad/register)도 가지고 있음
            2.  이러한 ALU 를 PE라고 부른다.
            3.  *ASIC이나 FPGA*에서 주로 사용하는 디자인 모델
                1.  중복되는 data를 reuse 하는 정도를 늘려서 연산량을 ↓
        3.  Accelerate Kernel compuatition @ CPU/GPU
            1.  kernel이 layer MAC 연산을 할 때 효과적으로 연산하기 위해서 방법을 제공하는 것
                1.  FC의 경우 결과물이 1x1xM (fmap의 개수) 로 출력된다
                2.  CONV의 경우 Matrix Mult수행 시 Toeplitz Matrix를 통해 1x1xK 의 꼴로 출력될 수 있도록 함
                3.  FFT를 활용하면 연산량이 확연하게 감소
                    1.  O(N<sup>2</sup> N<sup>2</sup>) → O(N<sup>2</sup>log<sub>2</sub>N)
                    2.  하지만 연산 량은 줄지만 계수나 기타 부호가 길어지기 때문에 메모리 소요량이 높다. (Capacity and BW)
                        1.  해결 방안으로 filter를 미리 FFT 해놓고 들어오는 입력만 dyanmic 하게 변환하여 사용하는 방식
        4.  Energy -Efficient Dataflow for Accelerators
            
            1.  MAC 연산 시 4번의 memory access가 필요하다 (3 read, 1 write)
            2.  이 때마다 DRAM(off-chip memory)를 사용하면 전력/시간 낭비가 크다
            3.  memory hierachy를 구성하여 필요에 따라 저장하는 공간을 다르게 구성하여 문제 해결
            4.  이 때 DRAM과 같이 외부에 존재하는 data를 칩 내부로 가져와서 연산하는 것에 사용
            5.  reuse를 최대한 효과적으로 많이 하는 것이 유리하다  
                ![9faa0a5cd08f63eedf8249c9bd7e1d1b.png](../../_resources/9faa0a5cd08f63eedf8249c9bd7e1d1b.png)
				
# *참고사항
- fmap은 CONV에서 입/출력 되는 data가 저장된 곳을 뜻함  
                ![809c750d703d0571a9445ba2cafed5a1.png](../../_resources/809c750d703d0571a9445ba2cafed5a1.png)
            
            > 결국 특징 추출은 CONV이 하고 뒤에서 FC Layer가 추론하는 것 아닌가?  
            > 그렇다면 FC Layer에서 quantization 하고 CONV에서 quant 하는 것은 weight 값 뿐인 것.
			
- psum :partial sum
	- 이전 단까지의 연산 결과를 저장해 놓는 방식을 채택
	- 