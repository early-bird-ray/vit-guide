# P003: Vision Transformer — ViT and its Derivatives

> ID: P003 | 태그: #서베이 #파생모델 #리뷰 #DeiT #Swin #MAE #BEiT

## 기본 정보

| 항목 | 내용 |
|------|------|
| 제목 | Vision Transformer: Vit and its Derivatives |
| 저자 | Zujun Fu |
| 제출 | 2022-05-12 (v1), 2022-05-24 (v2) |
| arXiv | https://arxiv.org/abs/2205.11239 |
| DOI | https://doi.org/10.48550/arXiv.2205.11239 |
| 분야 | cs.CV (Computer Vision and Pattern Recognition) |

---

## 개요

ViT 이후 등장한 파생 모델들과 크로스 도메인 응용을 정리한 리뷰 논문.  
NLP의 self-attention을 비전으로 가져온 패치 임베딩 방식을 기반으로,  
ImageNet, COCO, ADE20k 등 주요 벤치마크에서의 성능을 비교 분석.

---

## 주요 파생 모델 정리

| 모델 | 핵심 아이디어 | 개발사 |
|------|-------------|--------|
| **DeiT** | 데이터 효율적 ViT (지식 증류) | Facebook AI |
| **BEiT** | BERT 방식 마스크 이미지 모델링 | Microsoft Research |
| **MAE** | 75% 패치 마스킹 후 픽셀 재구성 | Facebook AI |
| **DINO** | Self-supervised ViT 학습 | Facebook AI |
| **Swin Transformer** | 계층적 ViT, shifted window attention | Microsoft |
| **CvT** | Conv 연산 통합 ViT | Microsoft |

---

## ViT vs CNN 비교 요약

| 기준 | CNN | ViT |
|------|-----|-----|
| 귀납 편향 | 강함 (locality, translation equivariance) | 약함 |
| 소규모 데이터 | 유리 | 불리 |
| 대규모 데이터 | 한계 있음 | 능가 |
| 확장성 | 제한적 | 뛰어남 |
| 전역 관계 학습 | 어려움 | 용이 |

---

## BibTeX

```bibtex
@article{fu2022vit,
  title={Vision Transformer: Vit and its Derivatives},
  author={Fu, Zujun},
  journal={arXiv preprint arXiv:2205.11239},
  year={2022},
  url={https://arxiv.org/abs/2205.11239}
}
```

---

## 관련 파일

- 원 논문 → [vit_original.md](vit_original.md) (P001)
- HuggingFace DeiT/BEiT 등 → [../02_huggingface/vit_docs_ko.md](../02_huggingface/vit_docs_ko.md)
