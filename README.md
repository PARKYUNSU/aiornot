<img width="500" alt="dds" src="https://github.com/PARKYUNSU/aiornot/assets/125172299/9c2aeb27-6709-4220-8039-f72299afbe27">


## AI 생성 이미지 판별

(AI-generated image detection)

---

## 프로젝트 개요

---

최근 AI로 생성한 프로필 사진을 주민등록증 사진으로 사용할 수 있는지 논란이 되었다. 앞으로도 AI 이미지 생성 서비스는 늘어날 전망이다. 증명사진으로 본인 여부를 확인하는 공공 · 민간 분야에 서는 이에 대비할 시스템이 필요하다. 딥러닝 분류 모델을 기반으로 증명사진의 AI 생성 여부를 판별하는 서비스를 제공하고자 한다.

## 프로젝트 목표

---

1. Hugging face 에서 대용량 AI, 실제 사진을 이용(https://huggingface.co/spaces/competitions/aiornot) - 대회 마감으로 차단
2. CNN (**Convolutional Neural Networks**)을 활용하여 분류 모델 구축
3.  Stable Diffusion / StarGAN 으로 생성된 AI 증명사진 데이터 셋을 이용하여 판별 서비스 기획

## 프로젝트 수행 절차

---

1. Hugging face에서 대용량 AI, 실제 데이터 셋을 받아서 진행합니다.
2. 훈련데이터 13,032 이미지 검증데이터 5,586 이미지로 나누기
3. CNN(**Convolutional Neural Network**)을 활용하여 Convolutional Layers를 직접 구축
4. 최적의 파라미터를 찾아서 이미지를 입력으로 받아들이고, 이미지에서 중요한 특징을 추출
5. 테스트 데이터 43,443 이미지 테스트 및 결과 확인
6. 학습된 모델을 Stable Diffusion / StarGAN 으로 생성된 AI 증명사진 데이터 셋에 적용
7. 가상환경 서버를 만들어 사용자가 웹페이지 및 API를 이용하여 사용하게끔 서비스 기획

---

### 데이터

| 데이터        | 이미지 수     | Class 0 비율 | Class 1 비율 |
|---------------|-----------|-------------|-------------|
| 훈련 데이터   |   13,032  |44.5%|55.5%|
| 검증 데이터   |    5,586  |44.5%|55.5%|
| 테스트 데이터 |   43,443  |44.5%|55.5%|

### Model Summary

| Layer (type)                  | Output Shape      | Param #    |
|-------------------------------|-------------------|------------|
| conv2d                        | (None, 256, 256, 32) | 896      |
| conv2d_1                      | (None, 256, 256, 32) | 9,216    |
| batch_normalization           | (None, 256, 256, 32) | 128      |
| activation                    | (None, 256, 256, 32) | 0        |
| max_pooling2d                 | (None, 128, 128, 32) | 0        |
| dropout                       | (None, 128, 128, 32) | 0        |
| conv2d_2                      | (None, 128, 128, 64) | 18,432   |
| batch_normalization_1         | (None, 128, 128, 64) | 256      |
| activation_1                  | (None, 128, 128, 64) | 0        |
| conv2d_3                      | (None, 128, 128, 64) | 36,864   |
| batch_normalization_2         | (None, 128, 128, 64) | 256      |
| activation_2                  | (None, 128, 128, 64) | 0        |
| max_pooling2d_1               | (None, 64, 64, 64)   | 0        |
| dropout_1                     | (None, 64, 64, 64)   | 0        |
| conv2d_4                      | (None, 64, 64, 128)  | 73,728   |
| batch_normalization_3         | (None, 64, 64, 128)  | 512      |
| activation_3                  | (None, 64, 64, 128)  | 0        |
| conv2d_5                      | (None, 64, 64, 128)  | 147,456  |
| batch_normalization_4         | (None, 64, 64, 128)  | 512      |
| activation_4                  | (None, 64, 64, 128)  | 0        |
| max_pooling2d_2               | (None, 32, 32, 128)  | 0        |
| dropout_2                     | (None, 32, 32, 128)  | 0        |
| flatten                       | (None, 131072)       | 0        |
| dense                         | (None, 256)          | 33,554,432|
| batch_normalization_5         | (None, 256)          | 1,024    |
| activation_5                  | (None, 256)          | 0        |
| dropout_3                     | (None, 256)          | 0        |
| reshape                       | (None, 1, 256)       | 0        |
| conv1d                        | (None, 1, 512)       | 655,872  |
| max_pooling1d                 | (None, 1, 512)       | 0        |
| conv1d_1                      | (None, 1, 512)       | 1,311,232|
| max_pooling1d_1               | (None, 1, 512)       | 0        |
| conv1d_2                      | (None, 1, 1024)      | 1,573,888|
| flatten_1                     | (None, 1024)         | 0        |
| dense_1                       | (None, 1)            | 1,025    |


## 모델 결과



---
