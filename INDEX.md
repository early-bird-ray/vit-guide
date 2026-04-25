# ViT (Vision Transformer) KMS — 마스터 인덱스

> 마지막 업데이트: 2026-04-24  
> 검색 팁: `Ctrl+F` 로 키워드 검색 가능. 태그(#tag)로 주제별 필터링.

---

## 빠른 탐색

| 목적 | 바로 가기 |
|------|-----------|
| ViT 원 논문 요약 | [01_papers/vit_original.md](01_papers/vit_original.md) |
| 스케일링 연구 | [01_papers/scaling_vit.md](01_papers/scaling_vit.md) |
| ViT 파생 모델 서베이 | [01_papers/vit_survey.md](01_papers/vit_survey.md) |
| HuggingFace 공식 문서 (한국어) | [02_huggingface/vit_docs_ko.md](02_huggingface/vit_docs_ko.md) |
| 모델 카드: vit-base-patch16-224 | [02_huggingface/vit_base_patch16_224.md](02_huggingface/vit_base_patch16_224.md) |
| Fine-tuning 가이드 | [02_huggingface/finetuning_guide.md](02_huggingface/finetuning_guide.md) |
| 한국어 튜토리얼 모음 | [03_tutorials/korean_resources.md](03_tutorials/korean_resources.md) |
| Google Scholar 레퍼런스 | [04_scholar/scholar_references.md](04_scholar/scholar_references.md) |
| **POC 서비스 10개** | [poc_services.md](poc_services.md) |

---

## 전체 항목 목록

### 📄 논문 (01_papers)

| ID | 제목 | 저자 | 연도 | 태그 |
|----|------|------|------|------|
| P001 | An Image is Worth 16x16 Words | Dosovitskiy et al. | 2020 | #원논문 #ViT #이미지분류 #Transformer |
| P002 | Scaling Vision Transformers | Zhai et al. | 2022 | #스케일링 #성능 #대규모모델 |
| P003 | Vision Transformer: ViT and its Derivatives | Fu | 2022 | #서베이 #파생모델 #리뷰 |

### 🤗 HuggingFace (02_huggingface)

| ID | 제목 | 유형 | 태그 |
|----|------|------|------|
| H001 | ViT 공식 문서 (한국어) | 공식문서 | #한국어 #API #모델클래스 #사용법 |
| H002 | google/vit-base-patch16-224 모델 카드 | 모델카드 | #사전학습 #ImageNet #86.6M파라미터 |
| H003 | ViT Fine-tuning 가이드 | 튜토리얼 | #파인튜닝 #전이학습 #이미지분류 |

### 📚 튜토리얼 (03_tutorials)

| ID | 제목 | 언어 | 태그 |
|----|------|------|------|
| T001 | 한국어 ViT 자료 모음 | 한국어 | #한국어 #블로그 #입문 #구조설명 |

### 🔬 Scholar (04_scholar)

| ID | 제목 | 태그 |
|----|------|------|
| S001 | Google Scholar 인용 및 레퍼런스 | #인용 #BibTeX #APA |

---

## 키워드 → 파일 매핑

| 키워드 | 관련 파일 |
|--------|-----------|
| 패치, patch embedding | P001, H001, H002 |
| self-attention | P001, P003, H003 |
| ImageNet | P001, P002, H002 |
| 파인튜닝, fine-tuning | H001, H002, H003 |
| 스케일링, 대규모 | P001, P002 |
| ViTForImageClassification | H001, H002, H003 |
| CIFAR-10 | H001, H003 |
| DeiT, BEiT, MAE, DINO | H001 |
| BibTeX, 인용 | S001 |
| 한국어 | H001, T001 |
| 86.6M 파라미터 | H002 |
| CNN 비교 | P001, H003, T001 |
| 전이학습, transfer learning | H002, H003 |

---

## 추천 학습 순서

```
1. P001 (원 논문 요약) → ViT 핵심 개념 파악
2. H001 (HuggingFace 한국어 문서) → 구조 및 API 이해
3. H002 (모델 카드) → 바로 실행 가능한 코드
4. H003 (Fine-tuning 가이드) → 내 데이터에 적용
5. P002 (스케일링 연구) → 심화 이해
6. P003 (서베이) → 파생 모델 전체 조감
```
