# H001: HuggingFace ViT 공식 문서 (한국어)

> ID: H001 | 태그: #한국어 #API #모델클래스 #사용법 #ViTConfig #SDPA

## 출처

- 공식 URL: https://huggingface.co/docs/transformers/ko/model_doc/vit
- 언어: 한국어

---

## 개요

ViT는 Dosovitskiy et al. (2020)의 논문에서 소개된 모델로,  
Transformer 인코더를 ImageNet에서 성공적으로 훈련시킨 **최초의 논문**.  
기존 CNN 구조 대비 매우 우수한 결과를 달성.

---

## 사용 팁

| 팁 | 내용 |
|----|------|
| 이미지 전처리 | `ViTImageProcessor` 로 리사이즈 + 정규화 |
| 입력 크기 | 기본 224×224 고정 (패치 크기 이름에 표시) |
| 해상도 업스케일 | 미세조정 시 더 높은 해상도 사용 가능, 위치 임베딩 2D 보간 자동 수행 |
| 성능 최적화 | `attn_implementation="sdpa"` + `float16` 로 1.33× 속도 향상 |

---

## 주요 모델 클래스

### ViTConfig
```python
from transformers import ViTConfig, ViTModel

configuration = ViTConfig()  # 기본값 = vit-base-patch16-224 설정
model = ViTModel(configuration)
```

**주요 파라미터:**

| 파라미터 | 기본값 | 설명 |
|----------|--------|------|
| `hidden_size` | 768 | hidden representation 차원 |
| `num_hidden_layers` | 12 | Transformer 레이어 수 |
| `num_attention_heads` | 12 | Attention 헤드 수 |
| `intermediate_size` | 3072 | MLP 차원 |
| `image_size` | 224 | 입력 이미지 크기 |
| `patch_size` | 16 | 패치 크기 |
| `num_channels` | 3 | 입력 채널 수 (RGB) |

---

### ViTModel (특징 추출용)
```python
from transformers import ViTModel

model = ViTModel.from_pretrained("google/vit-base-patch16-224")
# 출력: last_hidden_state, pooler_output, hidden_states, attentions
```

---

### ViTForImageClassification (분류용)
```python
from transformers import AutoImageProcessor, ViTForImageClassification
import torch
from datasets import load_dataset

dataset = load_dataset("huggingface/cats-image")
image = dataset["test"]["image"][0]

image_processor = AutoImageProcessor.from_pretrained("google/vit-base-patch16-224")
model = ViTForImageClassification.from_pretrained("google/vit-base-patch16-224")

inputs = image_processor(image, return_tensors="pt")

with torch.no_grad():
    logits = model(**inputs).logits

predicted_label = logits.argmax(-1).item()
print(model.config.id2label[predicted_label])
```

---

### ViTForMaskedImageModeling (마스크 사전학습용)
```python
from transformers import AutoImageProcessor, ViTForMaskedImageModeling
import torch

image_processor = AutoImageProcessor.from_pretrained("google/vit-base-patch16-224-in21k")
model = ViTForMaskedImageModeling.from_pretrained("google/vit-base-patch16-224-in21k")

num_patches = (model.config.image_size // model.config.patch_size) ** 2
pixel_values = image_processor(images=image, return_tensors="pt").pixel_values
bool_masked_pos = torch.randint(low=0, high=2, size=(1, num_patches)).bool()

outputs = model(pixel_values, bool_masked_pos=bool_masked_pos)
loss, reconstructed = outputs.loss, outputs.reconstruction
```

---

## SDPA 최적화 (PyTorch 2.1.1+)

```python
model = ViTForImageClassification.from_pretrained(
    "google/vit-base-patch16-224",
    attn_implementation="sdpa",
    dtype=torch.float16
)
```

**속도 비교 (A100-40GB, float32):**

| Batch size | Eager (ms) | SDPA (ms) | 속도 향상 |
|------------|-----------|-----------|----------|
| 1 | 7 | 6 | 1.17× |
| 2~8 | 8 | 6 | 1.33× |

---

## 후속 모델 (HuggingFace 지원)

| 모델 | 특징 | 체크포인트 예시 |
|------|------|----------------|
| DeiT | 데이터 효율적, 지식 증류 | `facebook/deit-base-patch16-224` |
| BEiT | BERT 방식 마스크 사전학습 | Microsoft Research |
| DINO | Self-supervised | HuggingFace Hub 검색 |
| MAE | 75% 마스킹 재구성 | Facebook AI |

---

## 학습 자료 링크

| 유형 | 제목 | URL |
|------|------|-----|
| 블로그 | ViT fine-tuning 방법 | https://huggingface.co/blog/fine-tune-vit |
| 노트북 | CIFAR-10 fine-tuning (Trainer) | GitHub NielsRogge/Transformers-Tutorials |
| 노트북 | CIFAR-10 fine-tuning (PyTorch Lightning) | GitHub NielsRogge/Transformers-Tutorials |
| 블로그 | Keras 이미지 분류 | https://www.philschmid.de/image-classification-huggingface-transformers-keras |
| 블로그 | Optimum 양자화 | https://www.philschmid.de/optimizing-vision-transformer |

---

## 관련 파일

- 원 논문 → [../01_papers/vit_original.md](../01_papers/vit_original.md)
- 모델 카드 → [vit_base_patch16_224.md](vit_base_patch16_224.md)
- Fine-tuning 가이드 → [finetuning_guide.md](finetuning_guide.md)
