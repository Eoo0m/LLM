<img width="818" height="277" alt="image" src="https://github.com/user-attachments/assets/0e453edc-ec26-43ac-9c2e-70c6d7d11b79" />

# β-DPO


β-DPO (Wu et al., 2024)를 참조하여 정적 β 값의 한계를 극복하였습니다.
논문에서 제가 구현한 부분을 요약하면 다음과 같습니다.

1. Dynamic β Calibration at Batch-Level
학습의 불안정성을 완화하기 위해,
각 batch 마다 동적으로 β를 계산한다.해당 방법은 data의 질에 따라 조정되며, high-quality,low-gap의 경우, β는 감소시켜 확실한 업데이트를 유도한다.
반대로 low- quality,high-gap의 경우 β를 증가시켜 신중한 업데이트를 촉진하고 노이즈에 대한 과적합을 방지한다.


3. β-Guided Data Filtering
해당 방법은 data filtering approach 방법으로, 빈번하게 나타나는 이상값[outliers]를 제거한다.
즉,가장 신뢰할 수 있고 대표적인 샘플에 우선 순위를 지정하여 β 추정의 충실도를 유지한다.
결과적으로 학습을 불안정하게 할 수 있는 이상값[outliers]의 영항을 줄여배치 수준 β 교정의 정밀도와 견고성을 향상시킨다.


<pre> self.M0 = self.momentum * self.M0 + (1 - self.momentum) * Mi 
self.var = self.momentum * self.var + (1 - self.momentum) * (delta ** 2) 
sigma = self.var ** 0.5 </pre>

배치의 한계로 기존 통계 기법을 적용하기 어려운 문제가 발생했습니다.

이에 평균을 moving average로 표준편차를 momentum 기반으로하여 control chart를 구성한 후 이상치를 잡아내는 방식으로 구현하였습니다.

<img width="777" height="306" alt="image" src="https://github.com/user-attachments/assets/9445ef82-03ea-4002-b8f6-10655649cab3" />
