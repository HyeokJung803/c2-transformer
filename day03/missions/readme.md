## mission 1
<img width="690" height="330" alt="image" src="https://github.com/user-attachments/assets/e1f88ca6-5b43-4879-a6d8-3f4e6b43f976" />
## ✍️ 제출 — 두 가지를 적는다

> ① 층별 모양은 일정한형태로 전부 같았다.
> ② 변화가 큰 구간은 12층 였고, 완만한 구간은 2~8층 였다.

> ⚠️ **값은 사람마다 다르다.** 문장이 다르니 당연하다. 옆 사람과 숫자가 달라도 틀린 게 아니다.
> 봐야 할 것은 **곡선의 모양**이다.

## mission 2
<img width="990" height="370" alt="image" src="https://github.com/user-attachments/assets/3922ff19-7ab1-4203-a74f-f164d37e3ef4" />
> 잔차 없이 쌓으면 약 5 층부터 신호(또는 기울기)가 사실상 0이 되어 학습이 불가능해진다.

## mission 3
<img width="689" height="350" alt="image" src="https://github.com/user-attachments/assets/d6d8ec22-7d6b-4110-a806-2c398a7e51b5" />
> 논문·BERT 는 post-LN 이고 GPT-2 이후는 pre-LN 이다.
> 깊게 쌓았을 때 논문·BERT 쪽은 값의 크기가 그대로였고, GPT-2 쪽은 계속 커졌다.


# Transformer Study

Transformer의 핵심 구성 요소와 인코더 블록의 동작 원리를 실습하며, BERT와 GPT 계열 모델의 구조적 차이를 학습했습니다.

## 학습한 개념

### Self-Attention
문장 속 모든 단어가 서로를 참고하여 중요한 정보를 선택하는 구조입니다. 이를 통해 단어의 순서뿐 아니라 문맥과 단어 간의 관계까지 학습할 수 있습니다.

### Hidden State
각 Transformer Layer를 통과하면서 만들어지는 문장 표현입니다. Layer가 깊어질수록 이전 Layer의 정보를 바탕으로 더 풍부한 의미를 담게 됩니다.

### Positional Encoding
Transformer는 문장의 순서를 알 수 없기 때문에 위치 정보를 함께 입력합니다. 사인(Sin)과 코사인(Cos) 함수를 이용해 각 위치마다 고유한 값을 부여하여 단어의 순서를 구분합니다.

### Feed Forward Network (FFN)
Self-Attention으로 모인 정보를 각 단어별로 한 번 더 가공하는 신경망입니다. 차원을 크게 확장한 뒤 다시 원래 크기로 줄이며 표현력을 높입니다.

### Residual Connection
입력을 다음 Layer로 직접 전달하는 연결 방식입니다. 정보가 중간에 사라지는 것을 줄여 깊은 모델에서도 안정적으로 학습할 수 있도록 도와줍니다.

### Gradient Vanishing
Layer가 깊어질수록 학습에 필요한 Gradient가 점점 작아져 앞부분이 잘 학습되지 않는 현상입니다. Residual Connection은 이러한 문제를 완화합니다.

### Layer Normalization
각 Layer의 출력 값을 일정한 범위로 정규화하여 학습이 불안정해지는 것을 방지합니다. 이를 통해 깊은 모델에서도 안정적으로 학습할 수 있습니다.

### Transformer Encoder Block
Transformer의 기본 단위로, **Self-Attention → Residual Connection → Layer Normalization → Feed Forward Network → Residual Connection → Layer Normalization** 순서로 구성됩니다. 이러한 블록을 여러 개 쌓아 하나의 Transformer 모델을 만듭니다.

### Post-LayerNorm (Post-LN)
Residual Connection 이후에 Layer Normalization을 수행하는 방식입니다. BERT에서 사용하는 구조로, 각 Layer의 출력 크기를 일정하게 유지하는 특징이 있습니다.

### Pre-LayerNorm (Pre-LN)
Layer Normalization을 먼저 수행한 뒤 Self-Attention과 Feed Forward를 적용하는 방식입니다. GPT-2 이후 Transformer에서 많이 사용되며, 매우 깊은 모델에서도 안정적으로 학습할 수 있습니다.

### Transformer 구조의 발전
Transformer는 Self-Attention을 기반으로 시작하여 Residual Connection과 Layer Normalization이 추가되었고, 이후 LayerNorm의 위치를 개선한 Pre-LN 구조가 도입되면서 더욱 깊고 안정적인 모델로 발전했습니다.
