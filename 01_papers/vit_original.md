# P001: An Image is Worth 16x16 Words

> ID: P001 | 태그: #원논문 #ViT #이미지분류 #Transformer #패치 #self-attention

## 기본 정보

| 항목 | 내용 |
|------|------|
| 제목 | An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale |
| 저자 | Alexey Dosovitskiy, Lucas Beyer, Alexander Kolesnikov, Dirk Weissenborn, Xiaohua Zhai, Thomas Unterthiner, Mostafa Dehghani, Matthias Minderer, Georg Heigold, Sylvain Gelly, Jakob Uszkoreit, Neil Houlsby |
| 소속 | Google Research, Brain Team |
| 발표 | ICLR 2021 |
| arXiv | https://arxiv.org/abs/2010.11929 |
| 최초 제출 | 2020-10-22 (v1), 2021-06-03 (v2) |

---

## 핵심 아이디어 (한 줄 요약)

> **이미지를 16×16 패치로 잘라 토큰처럼 Transformer에 넣으면 CNN 없이도 이미지 분류를 잘 할 수 있다.**

---

## Abstract (요약)

Transformer 아키텍처는 NLP에서 표준이 됐지만, 컴퓨터 비전에서는 제한적으로 사용됐다.  
이 논문은 CNN 의존 없이 순수 Transformer를 이미지에 직접 적용하는 방법을 제시한다.  
- 이미지를 패치 시퀀스로 분할 → Transformer 입력
- 대규모 데이터 사전학습 후 ImageNet, CIFAR-100, VTAB 등에서 SOTA 달성
- 기존 CNN 대비 훈련 계산 자원 절감

---

## 구조 설명

```
이미지 (예: 224×224)
   ↓ 16×16 패치로 분할 → 196개 패치
   ↓ Linear Embedding (패치 → 토큰 벡터)
   ↓ [CLS] 토큰 앞에 추가
   ↓ Positional Embedding 추가
   ↓ Transformer Encoder (Multi-Head Self-Attention + MLP)
   ↓ [CLS] 토큰의 출력 → 분류 헤드
   ↓ 예측 클래스
```

---

## 핵심 기술 포인트

| 포인트 | 설명 |
|--------|------|
| 이미지 패치화 | 224×224 이미지 → 16×16 패치 196개 |
| 패치 임베딩 | 각 패치를 선형 변환해 D차원 벡터로 |
| [CLS] 토큰 | BERT와 동일하게 분류용 특수 토큰 prepend |
| 위치 임베딩 | 1D absolute position embedding 사용 |
| Self-Attention | 모든 패치 간 전역 관계 학습 |
| 대규모 사전학습 | JFT-300M, ImageNet-21k에서 사전학습 시 CNN 능가 |

---

## 성능 (주요 벤치마크)

| 모델 | ImageNet Top-1 | 데이터 |
|------|----------------|--------|
| ViT-B/16 | 81.8% | JFT-300M pre-train |
| ViT-L/16 | 85.2% | JFT-300M pre-train |
| ViT-H/14 | 88.5% | JFT-300M pre-train |

---

## 모델 변형

| 모델명 | Layers | Hidden Size | MLP Size | Heads | Params |
|--------|--------|-------------|----------|-------|--------|
| ViT-B/16 | 12 | 768 | 3072 | 12 | 86M |
| ViT-L/16 | 24 | 1024 | 4096 | 16 | 307M |
| ViT-H/14 | 32 | 1280 | 5120 | 16 | 632M |

---

## 장단점

**장점**
- 대규모 데이터에서 CNN 능가
- 모델·데이터 스케일링 시 성능 향상 뚜렷
- 전역 self-attention으로 장거리 의존성 학습

**단점**
- 소규모 데이터에서 CNN 대비 열세 (inductive bias 부재)
- 대용량 데이터 필요
- 계산량이 패치 수에 O(n²) 비례

---

## 공개 코드 & 모델

- GitHub: https://github.com/google-research/vision_transformer
- HuggingFace: `google/vit-base-patch16-224`

---

## BibTeX

```bibtex
@article{dosovitskiy2020image,
  title={An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale},
  author={Dosovitskiy, Alexey and Beyer, Lucas and Kolesnikov, Alexander and
          Weissenborn, Dirk and Zhai, Xiaohua and Unterthiner, Thomas and
          Dehghani, Mostafa and Minderer, Matthias and Heigold, Georg and
          Gelly, Sylvain and Uszkoreit, Jakob and Houlsby, Neil},
  journal={ICLR 2021},
  year={2021},
  url={https://arxiv.org/abs/2010.11929}
}
```

---

## 관련 파일

- 파생 모델 서베이 → [vit_survey.md](vit_survey.md) (P003)
- 스케일링 연구 → [scaling_vit.md](scaling_vit.md) (P002)
- HuggingFace 사용법 → [../02_huggingface/vit_docs_ko.md](../02_huggingface/vit_docs_ko.md)
