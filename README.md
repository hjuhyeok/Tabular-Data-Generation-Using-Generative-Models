# **📌 InfoGAN + CTGAN: Tabular data 생성 모델**

## **1. 소개**
이 프로젝트는 **InfoGAN과 CTGAN을 결합**하여 **테이블 데이터(Tabular Data)**를 효과적으로 생성하는 모델입니다.  
범주형(Categorical) 데이터와 연속형(Continuous) 데이터를 모두 고려하며, 보다 **구조화된 데이터 생성을 가능하게 합니다.**

### **주요 문제점**
- **범주형과 연속형 데이터**를 동시에 다루는 어려움
- 데이터 분포를 **유지하면서 생성된 데이터 품질 확보**
- 의미 있는 **잠재 변수(latent structure) 학습 필요**

---

## **2. 배경 지식**
### **InfoGAN (Information Maximizing GAN)**
- 기존 GAN에서 **구조적인 잠재 변수 \( c \)를 학습**할 수 있도록 확장된 모델
- **데이터의 주요 특징(feature)을 학습**하여 **더 의미 있는 샘플 생성 가능**
- 특정 속성을 조절하여 **조건부 데이터 생성** 가능

### **CTGAN (Conditional Tabular GAN)**
- **테이블 데이터 전용 생성 모델**
- 핵심 기술:
  1. **Mode-specific Normalization** → 연속형 데이터 정규화 개선
  2. **Conditional Vectors** → 특정 범주 데이터 학습 가능

---

## **3. InfoGAN + CTGAN 결합 모델**
이 모델은 **InfoGAN의 잠재 변수 학습 기능**과 **CTGAN의 조건부 샘플링 기능**을 결합하여 **더 나은 데이터 생성을 목표**로 합니다.

### **구조 (Architecture)**
![모델 아키텍처](https://github.com/hjuhyeok/Tabular-Data-Generation-Using-Generative-Models/blob/main/%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90.png)

- **Generator \( G(z, c) \)**:
  - **잠재 변수 \( c \)**를 활용하여 데이터 생성
  - **CTGAN의 Mode-specific Normalization 기법**을 적용하여 데이터 분포 유지
  
- **Discriminator \( D(x) \)**:
  - **실제 데이터와 가짜 데이터를 판별**
  - **InfoGAN의 Q-network 포함** → 잠재 변수 \( c \) 예측 기능 추가

### **훈련 과정 (Training Process)**
1. **잠재 노이즈 \( z \) 및 구조적 코드 \( c \)를 기반으로 데이터 생성**
2. **판별자(Discriminator) 학습** → 진짜/가짜 데이터 구별
3. **Q-network 학습** → 생성된 데이터에서 \( c \)를 복원하도록 학습
4. **Gradient Penalty (WGAN-GP) 적용** → 모델 학습 안정성 증가

---

## **4. 실험 결과**
- **사용 데이터셋**: 범주형 + 연속형 데이터를 포함한 테이블 데이터셋
- **평가 결과**:
  - 기존 CTGAN보다 **범주형 데이터 분포를 더 균형 있게 유지**
  - InfoGAN 도입으로 **데이터의 의미 있는 특징을 학습 가능**
  - **조건부 샘플링 적용**으로 특정 카테고리 데이터 생성 가능

---

## **5. 결론**
- **InfoGAN과 CTGAN을 결합하여 더 구조화된 테이블 데이터 생성 가능**
- **잠재 변수를 활용하여 의미 있는 데이터 표현 학습**

---
## **6. 참고문헌**
- **InfoGAN 논문: https://arxiv.org/abs/1606.03657**
- **CTGAN 논문: https://arxiv.org/abs/1907.00503**



