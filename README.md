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
### ROC (0.869)
<img width="453" alt="스크린샷 2024-05-06 오후 3 04 13" src="https://github.com/PARKYUNSU/aiornot/assets/125172299/099dc5b7-d76c-4acd-9e72-e243ae1696ac">


### Confusion Matrix

|           | Precision | Recall  | F1-Score | Support |
|-----------|-----------|---------|----------|---------|
|     0     |   0.7414  |  0.5534 |   0.6338 |  19338  |
|     1     |   0.7023  |  0.8451 |   0.7671 |  24104  |
|-----------|-----------|---------|----------|---------|
| **Accuracy** |           |         |   0.7153 |  43442  |
| **Macro Avg** |   0.7218  |  0.6993 |   0.7004 |  43442  |
|**Weighted Avg**|  0.7197  |  0.7153 |   0.7078 |  43442  |


### 실제 이미지 결과 
1로 시작하는 파일 : 실제 / 0으로 시작하는 파일 : AI

| File Name | Image | Label | Prediction |
|---|---|---|---|
| 1-4 | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/5aa74c71-8ea8-466a-ba6d-52652bafa015" width="100"> | Not AI | Not AI |
| 0-222.jpeg |<img src= "https://github.com/PARKYUNSU/aiornot/assets/125172299/bb5becba-17b3-40b8-9f66-00e286cbb353" width="100">| AI | AI |
| 0-777.jpg | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/097f04f9-88e1-4cea-a421-d52d3dc5d1f4" width="100">| AI | AI |
| 0-2.jpg | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/d1fac5c3-4f6c-459d-b507-f01f9be5cbe5" width="100">| AI | AI |
| 0-2323.jpg | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/32f43e9c-6f5d-4eb6-b34d-bf773b793a1b" width="100">| AI | AI |
| 0-7.jpeg | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/35a0220f-2d23-4bbe-947c-6c569608a759" width="100">| AI | AI |
| 0-231234.jpeg |<img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/42031c80-5f96-4b95-ba8d-e92614f4d74f" width="100">| AI | Not AI |
| 1-1.jpg | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/6e06de63-fba1-474f-ad76-735b9846930b" width="100">| Not AI | Not AI |
| 1-2.png | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/a1efc742-772c-430c-9920-e89c559645e6" width="100">| Not AI | AI |
| 1-3.jpg | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/7f34acc9-6772-465f-8d48-856f6226fdb9" width="100">| Not AI | AI |
| 0-211222.jpg | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/ba43c0a2-e0fd-4b18-84fe-6e93065c2169" width="100">| AI | AI |
| 0-23212.jpeg | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/be1c46a3-e593-4d24-815a-cffe7c4c3071" width="100"> | Not AI | Not AI |
| 0-123.jpg | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/dfb8bbed-1c8c-4171-9263-45f7f17193a6" width="100"> | AI | AI |
| 0-232.png | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/e4406288-6a56-40ac-bf06-2c203aa0b3e4" width="100">| AI | AI |
| 0-8.png | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/3105184a-9246-423b-8a4b-7934e9d615a5" width="100">| AI | Not AI |
| 0-1.jpeg | <img src="https://github.com/PARKYUNSU/aiornot/assets/125172299/1e581e3d-40e0-4724-8b12-03bfaadf9e2b" width="100"> | AI | AI |
