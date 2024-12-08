# 이미지 캡션 생성 프로그램

이 프로그램은 BLIP(Bootstrapping Language-Image Pre-training) 모델을 사용하여 이미지에 대한 설명문(캡션)을 자동으로 생성하는 Python 스크립트입니다.

## 주요 기능

- 입력된 이미지에 대한 자연어 설명문 생성
- 이미지와 생성된 캡션의 시각화
- GPU 가속 지원 (CUDA 사용 가능 시)

## 필요 라이브러리

```python
- cv2 (OpenCV)
- torch (PyTorch)
- PIL (Python Imaging Library)
- transformers
- matplotlib
```

## 코드 구조

### 1. 라이브러리 임포트 및 초기 설정
```python
import cv2
import torch
from PIL import Image
from transformers import BlipProcessor, BlipForConditionalGeneration
import matplotlib.pyplot as plt
import os
```

### 2. BLIP 모델 초기화
- Salesforce에서 제공하는 'blip-image-captioning-base' 모델 사용
- GPU 사용 가능 시 CUDA 활용, 그렇지 않을 경우 CPU 사용
- 초기화 과정에서 발생하는 오류 처리 포함

### 3. 캡션 생성 함수 (generate_caption)

주요 처리 단계:
1. 이미지 파일 존재 여부 확인
2. OpenCV를 사용한 이미지 로드
3. BGR에서 RGB 색상 형식으로 변환
4. PIL Image 형식으로 변환
5. BLIP 모델을 통한 캡션 생성
6. matplotlib을 사용한 결과 시각화

오류 처리:
- 파일 존재 여부 검증
- 이미지 로드 실패 처리
- 캡션 생성 과정의 예외 처리
- 시각화 과정의 예외 처리

## 사용 방법

1. 이미지 파일을 준비합니다.
2. 아래와 같이 함수를 호출합니다:
```python
image_path = "./images/image.jpg"  # 이미지 경로 설정
caption = generate_caption(image_path)
print(f"\n생성된 캡션: {caption}")
```

## 주의사항

1. CUDA 지원 GPU가 없는 경우 CPU에서 실행되며, 처리 속도가 느릴 수 있습니다.
2. 이미지 파일은 일반적인 이미지 형식(jpg, png 등)을 지원합니다.
3. 생성되는 캡션은 영어로 출력됩니다.

## 오류 처리

프로그램은 다음과 같은 상황에서 적절한 오류 메시지를 반환합니다:
- 이미지 파일이 존재하지 않는 경우
- 이미지 파일을 읽을 수 없는 경우
- 모델 초기화 중 오류가 발생한 경우
- 캡션 생성 중 오류가 발생한 경우
- 결과 시각화 중 오류가 발생한 경우

## 출력 예시

프로그램 실행 시:
1. 모델 로딩 상태와 사용 중인 디바이스 정보 출력
2. 이미지와 생성된 캡션이 포함된 이미지 표시
3. 생성된 캡션 텍스트 출력