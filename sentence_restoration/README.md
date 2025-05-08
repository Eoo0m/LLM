
## 난독화된 한글 리뷰 복원 AI

https://colab.research.google.com/drive/11XIJrvN6FBNS1Ez0JDo1NuOFfN68N3V8?usp=sharing

<img width="725" alt="Screenshot 2025-05-08 at 5 48 08 PM" src="https://github.com/user-attachments/assets/d2337f62-a818-47a7-8507-8b1acdfb942b" />






### 난독화된 한글 리뷰를 원래의 명확한 내용의 리뷰로 복원

'별 한 게토 았깝땀. 왜 싸람듯릭 펼 1캐를 쥰눈징 컥꺾폰 싸람믐롯섞 맒록 섧멍핥쟈'  -> '별 한 개도 아깝다. 왜 사람들이 별 1개를 주는지 겪어본 사람으로서 말로 설명하자'

1. 초기 시도
T5모델을 통해 학습 중 토큰화를 잘 못하는 것을 발견
text = '별 한 게토 았깝땀. 왜 싸람듯릭 펼 1캐를 쥰눈징 컥꺾폰 싸람믐롯섞 맒록 섧멍핥쟈'
input_ids = [3, 2, 3, 2, 3, 2, 3, 2, 5, 3, 2, 3, 2, 3, 2, 209, 2, 3, 2, 3, 2, 3, 2, 3, 2, 3, 2, 1]
tokens = ['▁', '<unk>', '▁', '<unk>', ... , '▁', '<unk>', '▁', '<unk>', '</s>']

2. 난독화된 단어들은 바이트 단위로 쪼개는 byT5 사용하기로 결심.
   
input_ids = [238, 182, 135, 35, 240, ... ,39, 162, 139, 1]
tokens = ['ë', '³', '\x84', ' ', 'í', '\x95', ... ,'\x8d', 'í', '\x95', '¥', 'ì', '\x9f', '\x88', '</s>']

3.
<img width="335" alt="image" src="https://github.com/user-attachments/assets/8e667322-c59c-4433-9b7e-62aee2a83a0b" />

weight_decay, lr등을 조절하며 실험. 
emperical한 수치로 결정

learning_rate=0.00025,
per_device_train_batch_size=2,
per_device_eval_batch_size=4,
num_train_epochs=7,
weight_decay=0.01


