# H002: google/vit-base-patch16-224 모델 카드

> ID: H002 | 태그: #사전학습 #ImageNet #86.6M파라미터 #Apache2.0 #바로사용가능

## 모델 정보

| 항목 | 내용 |
|------|------|
| 모델 ID | `google/vit-base-patch16-224` |
| HuggingFace URL | https://huggingface.co/google/vit-base-patch16-224 |
| 파라미터 수 | **86.6M** |
| 라이센스 | Apache 2.0 |
| 텐서 타입 | F32 |
| 월간 다운로드 | ~4,645,706회 |

---

## 학습 데이터

| 단계 | 데이터셋 | 규모 |
|------|----------|------|
| 사전학습 | ImageNet-21k | 1,400만 이미지 / 21,843 클래스 |
| 미세조정 | ImageNet 2012 (ILSVRC) | 128만 이미지 / 1,000 클래스 |

---

## 아키텍처 요약

```
입력 이미지 (224×224)
  → 16×16 패치 분할 → 196개 패치
  → 선형 임베딩
  → [CLS] 토큰 추가
  → 절대 위치 임베딩 추가
  → Transformer Encoder 12층
  → [CLS] 출력 → 분류 헤드 (1,000클래스)
```

---

## 학습 세부 정보

| 항목 | 내용 |
|------|------|
| 하드웨어 | TPUv3 8코어 |
| 배치 크기 | 4,096 |
| 학습률 워밍업 | 10,000 스텝 |
| Gradient Clipping | global norm 1 (ImageNet 미세조정) |
| 입력 해상도 | 224×224 |
| 정규화 | Mean (0.5, 0.5, 0.5) / Std (0.5, 0.5, 0.5) |

---

## 바로 실행 코드

```python
from transformers import ViTImageProcessor, ViTForImageClassification
from PIL import Image
import requests

# 이미지 로드
url = 'http://images.cocodataset.org/val2017/000000039769.jpg'
image = Image.open(requests.get(url, stream=True).raw)

# 모델 & 프로세서 로드
processor = ViTImageProcessor.from_pretrained('google/vit-base-patch16-224')
model = ViTForImageClassification.from_pretrained('google/vit-base-patch16-224')

# 추론
inputs = processor(images=image, return_tensors="pt")
outputs = model(**inputs)
logits = outputs.logits

predicted_class_idx = logits.argmax(-1).item()
print("예측 클래스:", model.config.id2label[predicted_class_idx])
```

---

## 성능

- 원 논문 Table 2, 5 참조
- 최고 성능은 384×384 해상도로 미세조정 시 달성
- 기본 체크포인트는 224×224 기준

---

## 관련 체크포인트

| 모델명 | 패치 | 해상도 | 특징 |
|--------|------|--------|------|
| `google/vit-base-patch16-224` | 16×16 | 224 | 기본 |
| `google/vit-base-patch32-224` | 32×32 | 224 | 빠름, 정확도↓ |
| `google/vit-large-patch16-224` | 16×16 | 224 | 큰 모델 |
| `google/vit-base-patch16-224-in21k` | 16×16 | 224 | ImageNet-21k만 학습 (미세조정용) |

---

## 관련 파일

- API 문서 → [vit_docs_ko.md](vit_docs_ko.md)
- Fine-tuning → [finetuning_guide.md](finetuning_guide.md)
- 원 논문 → [../01_papers/vit_original.md](../01_papers/vit_original.md)
