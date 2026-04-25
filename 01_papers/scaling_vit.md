# P002: Scaling Vision Transformers

> ID: P002 | 태그: #스케일링 #성능 #대규모모델 #2B파라미터 #ImageNet90% #CVPR2022

## 기본 정보

| 항목 | 내용 |
|------|------|
| 제목 | Scaling Vision Transformers |
| 저자 | Xiaohua Zhai, Alexander Kolesnikov, Neil Houlsby, Lucas Beyer |
| 소속 | Google Research |
| 발표 | CVPR 2022 |
| 공식 페이지 | https://research.google/pubs/scaling-vision-transformers/ |

---

## 핵심 아이디어

> **ViT 모델과 데이터 규모를 키울수록 정확도가 예측 가능하게 향상된다. 20억 파라미터 모델로 ImageNet 90.45% 달성.**

---

## 주요 발견

### 스케일링 법칙
- 에러율, 데이터량, 계산량 사이의 관계를 정량화
- NLP의 스케일링 법칙을 비전 영역으로 확장
- 모델 크기와 데이터 크기를 함께 늘릴 때 최고 효율

### 성능 기록

| 조건 | 정확도 |
|------|--------|
| ImageNet top-1 (2B 파라미터 모델) | **90.45%** |
| Few-shot (10 shots per class) ImageNet | **84.86%** |

---

## 아키텍처 개선

- 메모리 요구량 감소를 위한 아키텍처 최적화
- 헤드 수, 레이어 깊이, hidden size 간 균형 탐색
- Head-free classifier 도입으로 효율 향상

---

## 실용적 시사점

1. 작은 모델로 시작해서 필요시 스케일업하는 전략이 효과적
2. 데이터 증강보다 더 많은 데이터가 대규모 모델에서 더 중요
3. Few-shot 성능이 뛰어나 레이블 적은 환경에 유리

---

## BibTeX

```bibtex
@inproceedings{zhai2022scaling,
  title={Scaling Vision Transformers},
  author={Zhai, Xiaohua and Kolesnikov, Alexander and Houlsby, Neil and Beyer, Lucas},
  booktitle={CVPR},
  year={2022},
  url={https://research.google/pubs/scaling-vision-transformers/}
}
```

---

## 관련 파일

- 원 논문 → [vit_original.md](vit_original.md) (P001)
- HuggingFace 대규모 모델 → [../02_huggingface/vit_docs_ko.md](../02_huggingface/vit_docs_ko.md)
