# 소량 데이터 기반 아몬드 이미지 분류에서 전이학습과 학습 기법 적용의 실험적 탐색

본 프로젝트는 소량의 학습 데이터 환경에서 아몬드 품종 이미지 분류 모델이 전이학습을 통해 어느 정도의 성능을 달성할 수 있는지를 실험적으로 탐색한 개인 연구입니다. 다양한 pretrained 모델과 학습 기법(Augmentation, Cross-Validation K-Fold 등)을 비교하여, 데이터 효율성과 일반화 성능의 trade-off를 분석하고자 하였습니다.

---

## 🧪 프로젝트 개요

- **목표**: 최소한의 데이터로도 높은 정확도를 달성할 수 있는 분류 모델 설계  
- **주제**: 아몬드 4종 품종 분류  

- **전이학습 기반 학습 전략**:
  - Fine-tuning
  - Data Augmentation
  - Cross Validation (K-Fold)

- **실험 구성 요소**:
  - 다양한 pretrained 모델 비교 (ResNet, DenseNet, ConvNext 등)
  - 데이터 비율 축소 실험 (최소 16장)
  - 학습 기법 조합에 따른 성능 및 일반화 평가

---

## 📂 데이터셋

- 총 이미지 수: 1,556장  
- 클래스: 4개 품종  
- 해상도: 198x284 ~ 647x1076  
- 전처리: 224x224 Resize, 정규화  
- 출처: [Kaggle - Almond Varieties Dataset](https://www.kaggle.com/datasets/mahyeks/almond-varieties/data)

---

## 🔧 실험 구성

### 🔹 초기 실험
소량의 학습 데이터로도 높은 성능을 달성할 수 있는지를 확인하기 위해,  
train set 비율을 점차 줄여가며 pretrained 모델의 fine-tuning 효과와 성능 저하 시점을 관찰하였다.

- 사용 모델:
  - ResNet50
  - EfficientNet-B0
  - MobileNetV3
  - ShuffleNetV2
- 비교 내용:
  - Fine-tuning vs Pretrained (Baseline) 성능 비교
  - 데이터셋 비율별 정확도 변화 분석

### 🔹 후기 실험
전이학습 기반의 성능 향상을 극대화하기 위해, 다양한 학습 기법을 적용하여  
학습 데이터 수 대비 정확도와 일반화 성능을 최적화할 수 있는 조합을 탐색하였다.

- 사용 모델:
  - ResNet50
  - ResNet152
  - VGG16
  - DenseNet201
  - SeResNext101
  - ConvNext_Base
- 적용 기법:
  - Fine-tuning
  - Augmentation + Fine-tuning
  - K-Fold + Fine-tuning (Best Fold & Ensemble)
  - Augmentation + K-Fold + Fine-tuning

---

## 📊 주요 결과

최소한의 학습 데이터만으로도 전이학습 기반 모델들이 높은 정확도를 유지할 수 있음을 실험적으로 확인하였고,  
ConvNext_Base 모델의 Augmentation 적용 실험에서 가장 높은 정확도(97.39%)를 기록하였다.

| 모델          | 학습 기법               | Accuracy |
|---------------|--------------------------|----------|
| ConvNext_Base | Augmentation             | **97.39%** |
| ConvNext_Base | K-Fold Ensemble          | 96.27%   |
| DenseNet201   | K-Fold Ensemble          | 95.56%   |
| ResNet50      | K-Fold Ensemble          | 95.82%   |

🔍 **핵심 요약**
- Pretrained 모델 단독 사용 대비, fine-tuning은 모든 실험에서 성능 향상에 크게 기여
- Augmentation과 K-Fold는 각각 다른 방식으로 성능 및 일반화 향상에 효과적
- 두 기법을 동시에 적용할 경우 학습 수렴이 불안정해지는 현상이 관찰됨

---

## 🔍 주요 인사이트

- 학습 데이터가 극도로 제한된 상황(16장 학습, 8장 검증)에서도 fine-tuning만으로 90% 이상의 정확도 달성 가능함을 확인함
- Augmentation은 정확도 향상에 효과적이나, Confusion Matrix 기준으로는 K-Fold가 더 균형 잡힌 일반화 성능을 보임
- Augmentation과 K-Fold를 동시에 적용한 실험에서는 모든 fold에서 학습 수렴이 불안정하게 나타나며,  
  두 기법의 상호작용 구조에 대한 추가 분석이 필요한 것으로 판단됨

---

## 📚 참고 문헌

1. Saedi, M., Farokhi, E., Ebrahimi, M. A., & Mahmoudi, M. R. (2024).  
   *An intelligent system based on image processing techniques and deep learning models for classification of almond kernel varieties*.  
   European Food Research and Technology. [https://doi.org/10.1007/s00217-024-04562-4](https://doi.org/10.1007/s00217-024-04562-4)
