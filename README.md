#beta DPO
E0oom/Llama-3.2-1B-betadpo

##Dynamic β Calibration at Batch-Level
학습의 불안정성을 완화하기 위해,각 batch 마다 동적으로 β를 계산한다.해당 방법은 data의 질에 따라 조정되며, 
high-quality,low-gap의 경우, β는 감소시켜 확실한 업데이트를 유도한다.
반대로 low-quality,high-gap의 경우 β를 증가시켜 신중한 업데이트를 촉진하고 노이즈에 대한 과적합을 방지한다.

##β-Guided Data Filtering
해당 방법은 data filtering approach 방법으로, 빈번하
게나타나는 이상값[outliers]를 제거한다.
즉,가장 신뢰할 수 있고 대표적인 샘플에 우선 순위를 지정하여 β 추정의 충실도를 유지한다. 
결과적으로 학습을 불안정하게 할 수 있는 이상값[outliers]의 영항을 줄여배치 수준 β 교정의 정밀도와 견고성을 향상시킨다.

여기서 배치의 크기를 키울 수 없는 자원의 한계로, 모멘텀 기반으로 평균과 분산을 잡아 이상치를 필터링한다.(학습에선 RTX3090을 사용하여, 배치 크기 2를 사용)

<img width="769" alt="image" src="https://github.com/user-attachments/assets/88ce8f77-613e-4a7f-8f18-30192f310c71" />
<img width="769" alt="image" src="https://github.com/user-attachments/assets/88ce8f77-613e-4a7f-8f18-30192f310c71" />
