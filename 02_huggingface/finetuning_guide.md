# H003: ViT Fine-tuning 가이드

> ID: H003 | 태그: #파인튜닝 #전이학습 #이미지분류 #멀티레이블 #CNN비교 #inductive_bias

## 출처

- HuggingFace Computer Vision Course Unit 3
- URL: https://huggingface.co/learn/computer-vision-course/unit3/vision-transformers/vision-transformers-for-image-classification

---

## CNN vs ViT 비교

### 핵심 차이: Inductive Bias

| 귀납 편향 | CNN | ViT |
|----------|-----|-----|
| Translation Equivariance | ✅ (어디서나 객체 인식) | ❌ |
| Locality | ✅ (주변 픽셀 위주) | ❌ |
| 확장성 | 제한적 | ✅ 뛰어남 |
| 소규모 데이터 | 유리 | 불리 |
| 대규모 데이터 | 한계 있음 | CNN 능가 |

> **결론**: 데이터가 일정 임계치 이하면 CNN이 유리. 대규모 데이터 + 사전학습 모델 활용 시 ViT가 강력.

---

## Transfer Learning 전략

### 전략 1: Feature Extraction (빠름)
- 사전학습된 가중치 **동결(freeze)**
- 마지막 분류 레이어만 학습
- 데이터가 적거나 사전학습 도메인과 유사할 때 유효

### 전략 2: Fine-tuning (높은 정확도)
- 전체 모델 가중치를 **낮은 학습률**로 업데이트
- 도메인 차이가 클 때 유효
- GPU 메모리 더 필요

> 대부분의 경우 Transfer Learning(전략 1)만으로도 충분.

---

## Multi-class 분류 구현

```python
from transformers import ViTForImageClassification, ViTImageProcessor
import torch
from torch.optim import AdamW

# 모델 로드 (num_labels 조정)
model = ViTForImageClassification.from_pretrained(
    "google/vit-base-patch16-224-in21k",
    num_labels=10,           # 분류할 클래스 수
    ignore_mismatched_sizes=True
)
processor = ViTImageProcessor.from_pretrained("google/vit-base-patch16-224-in21k")

# 입력 전처리
inputs = processor(images=image, return_tensors="pt")

# 학습
optimizer = AdamW(model.parameters(), lr=2e-5)
outputs = model(**inputs, labels=labels)
loss = outputs.loss
loss.backward()
optimizer.step()
```

---

## Multi-label 분류 구현

```python
from transformers import ViTForImageClassification
import torch.nn as nn

model = ViTForImageClassification.from_pretrained(
    "google/vit-base-patch16-224-in21k",
    num_labels=num_labels,
    problem_type="multi_label_classification",
    ignore_mismatched_sizes=True
)

# BCEWithLogitsLoss 자동 사용 (problem_type 설정 시)
outputs = model(**inputs, labels=float_labels)
```

---

## HuggingFace Trainer 사용 예시

```python
from transformers import TrainingArguments, Trainer

training_args = TrainingArguments(
    output_dir="./vit-finetuned",
    num_train_epochs=5,
    per_device_train_batch_size=32,
    per_device_eval_batch_size=32,
    evaluation_strategy="epoch",
    save_strategy="epoch",
    load_best_model_at_end=True,
    learning_rate=2e-5,
    remove_unused_columns=False,
)

trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=train_dataset,
    eval_dataset=eval_dataset,
    compute_metrics=compute_metrics,
)

trainer.train()
```

---

## 추천 추가 자료

| 자료 | URL |
|------|-----|
| ViT fine-tuning 블로그 | https://huggingface.co/blog/fine-tune-vit |
| Swin Transformer 논문 | https://huggingface.co/papers/2103.14030 |
| ViT 학습 방법 연구 (데이터·증강·정규화) | https://huggingface.co/papers/2106.10270 |
| NielsRogge 튜토리얼 모음 | https://github.com/NielsRogge/Transformers-Tutorials/tree/master/VisionTransformer |

---

## 관련 파일

- 모델 카드 → [vit_base_patch16_224.md](vit_base_patch16_224.md)
- API 문서 → [vit_docs_ko.md](vit_docs_ko.md)
- CNN vs ViT 이론 → [../01_papers/vit_survey.md](../01_papers/vit_survey.md)
