---
title: "🛠️ 전처리 툴킷 소개"
layout: post
toc: true
toc_label: "Toolkit Menu"
header:
  image: /assets/images/header/image-edit.jpg
author_profile: true
read_time: true
comments: true
share: true
categories: 
    - Note
    - MachineLearning
tags: 
    - augmentation
    - OpenCV
excerpt: "스크롤바로 조작 가능한 전처리 툴킷: Padding, 정규화, 블러 등 다양한 기법을 실습하며 이미지 품질을 향상시켜 보세요."
---

## 🧭 기능 소개

- 현장 이미지 품질을 확인하고 개선할 수 있다.

- 다양한 전처리 기법을 적용할 수 있다.

- **슬라이더와 버튼**으로 파라미터를 조정할 수 있다.

---

## 📚 기능 요약 (목차)

| 분류              | 전처리 종류                         |
|-------------------|--------------------------------------|
| 🎯 정규화 계열     | Normalize, Standardize               |
| 📏 크기/형태 정리 | Resize, Crop, Padding                |
| 🔁 증강 (Augmentation) | Flip, Rotate, Brightness, Noise     |
| 🌈 채널/색 변경     | Grayscale, RGB to HSV               |
| 🌀 형태 강조       | Histogram Equalization, CLAHE        |
| 🔉 노이즈 제거     | Gaussian Blur, Median Blur           |
| 🎯 영역 조정       | ROI Crop, Masking                    |
| 🌐 공간 도메인 처리| Edge Detection, Dilation             |

---

## 🎨 주요 기능 코드 예시

### ✅ 1. Padding

```python
def apply_padding(padding_type):
    if padding_type == 'Zero Padding':
        padded = cv2.copyMakeBorder(img_gray, 50, 50, 50, 50, cv2.BORDER_CONSTANT, value=[0, 0, 0])
    elif padding_type == 'Edge Padding':
        padded = cv2.copyMakeBorder(img_gray, 50, 50, 50, 50, cv2.BORDER_REPLICATE)
    # ...
    plt.imshow(padded, cmap='gray')
    plt.title(padding_type)
    plt.axis('off')
    plt.show()
```
라디오 버튼으로 패딩 타입을 선택할 수 있다.  
타입: Zero Padding, Edge Padding, Reflect Padding, Constant Padding
![Padding 예시](/assets/images/2025/preprocessing/preprocessing-padding.png)



### ✅ 2. 선형 연산 (밝기 배율 조절)

```python
def update_brightness(factor):
    img_modified = np.clip(img_gray_crop * factor, 0, 255).astype('uint8')
    plt.imshow(img_modified, cmap='gray')
    plt.title(f'Intensity x {factor:.2f}')
    plt.axis('off')
    plt.show()
```
🔘 스크롤바로 밝기 조절이 가능하다 (0.1 ~ 2.0)
![Brightness 조절 예시](/assets/images/2025/preprocessing/preprocessing-brightness.png)

✅ 3. Gaussian Blur

```python
def apply_blur(method, ksize):
    if method == 'Gaussian Blur':
        blurred = cv2.GaussianBlur(img_gray, (ksize, ksize), 0)
    plt.imshow(blurred, cmap='gray')
    plt.title(f'{method} (kernel={ksize})')
    plt.axis('off')
    plt.show()
```
🎚️ 커널 크기 슬라이더로 블러 강도 조정이 가능하다

![Gaussian Blur 예시](/assets/images/2025/preprocessing/preprocessing-gaussianblur.png)

✅ 4. Normalize

```python
img_gray_copy = img_gray.astype(np.float32) / 255.0
img_normalized = (img_gray_copy - np.min(img_gray_copy)) / (np.max(img_gray_copy) - np.min(img_gray_copy))
plt.imshow(img_normalized, cmap='gray')
plt.title("Normalized Image")
plt.axis('off')
plt.show()
```
📊 픽셀값을 0~1 범위로 조정한다 딥러닝 전처리에서 학습 안정화를 위해 사용된다

![Normalize 예시](/assets/images/2025/preprocessing/preprocessing-normalization.png)

🔧 주요 특징

✅ Colab 환경에서 실행되어 현장 PC 사양에 관계없이 이미지 편집이 가능

✅ Google Drive와 연동되어 대용량 이미지 데이터도 쉽게 활용 가능

✅ 압축파일을 직접 읽어와 업로드 시간과 용량 제한 문제를 최소화

---

📌 *코드 링크*

🔗 [Colab Full 코드](https://colab.research.google.com/drive/1wopaJsdKlRnV8OD1bxb3jMNMCOMk5Sh-?usp=sharing)

해당 노트북에서는 다양한 전처리 기법을 직접 적용해 보고,  
**슬라이더나 버튼 위젯을 통해 파라미터를 조절하며 시각적으로 결과를 확인**할 수 있습니다.
