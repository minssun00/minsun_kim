# 연구 세션 요약 — 2026-05-30

---

## 1. 연구 프로젝트 개요

**제목:** DBTL 기반 Sucrose Synthase 엔지니어링을 통한 Reb D 생산 시스템 구축

### 핵심 반응 체계

```
[Donor regeneration] GmSUS 역반응
  Sucrose + UDP  →  UDP-Glucose + Fructose

[Product formation] UGTSL 반응
  Reb A + UDP-Glucose  →  Reb D + UDP

[UDP 재생 사이클]
  UDP가 두 반응 사이에서 순환 재사용됨
```

### 논문 스토리
- **Core problem:** UGTSL-mediated Reb A → Reb D 전환 효율은 UDP-glucose 공급 능력에 좌우됨. SuSy의 낮은 reverse performance와 비효율적 sucrose utilization이 bottleneck.
- **Solution:** DBTL-guided SuSy engineering → donor regeneration efficiency 향상 → practical Reb D bioconversion system 구축
- **확장성:** SuSy-UGTSL 시스템은 하위 GT만 교체하면 다양한 UDP-glucose 의존적 당전이 반응에 적용 가능한 modular platform

---

## 2. 논문 투고 정보

| 항목 | 내용 |
|------|------|
| **투고 목표** | 2026년 7월 |
| **Target journal** | **Bioresource Technology** *(2026-05-30 변경)* |
| **프레이밍 방향** | food sweetener보다 **bioconversion 효율, 효소 시스템 엔지니어링, 공정 최적화** 강조 |

> **변경 이유:** Bioresource Technology는 바이오프로세스/효소 엔지니어링 논문에 강하며 IF도 높음. 결론부와 abstract에서 공정 적용 가능성(scalability, cost-effective sucrose 활용)을 부각 필요.

---

## 3. β-Arbutin 생산용 UGT 합성 계획

### 3-1. 효소 정보

| 항목 | 내용 |
|------|------|
| **효소명** | Arbutin Synthase (AS) |
| **Accession** | AJ310148.1 |
| **출처** | *Rauvolfia serpentina* (Arend et al., 2001) |
| **반응** | Hydroquinone + UDP-glucose → β-Arbutin + UDP |
| **EC** | 2.4.1.218 |
| **CDS 위치** | mRNA 27–1439 (1,413 bp) |
| **단백질 크기** | 470 aa + TGA (stop) |

### 3-2. 합성 전략

- **기질:** Hydroquinone 외부 공급 + GmSUS가 UDP-glucose 공급 → **AS만 단독 발현**
- **발현 호스트:** *S. cerevisiae* CEN.PK2-1C (chassis yeast)
- **발현 방식:** signal peptide 없이 세포질 발현
- **합성 업체:** Twist Bioscience

> **MNX1 불필요:** Yang et al. 2024에서는 HQ 산화 방지를 위해 MNX1-AS 융합단백질(GGGS linker) 사용 → titer 19.7% 향상. 본 연구에서는 HQ 외부 공급이므로 MNX1 생략 가능. HQ 독성/산화 문제 발생 시 참고.

### 3-3. 참고 논문

| 논문 | 저널 | AS titer | 접근 |
|------|------|----------|------|
| Yang et al. 2024 | *Microbial Cell Factories* | 128.6 g/L (*K. phaffii*) | **Open access** ✅ |
| Zhang et al. 2026 | *Food Bioscience* | 70.87 g/L (*K. phaffii*) | papers 폴더 저장 (`1-s2.0-S2212429226006322-main.pdf`) |

- Yang et al. 2024: UbiC + MNX1 + AS 조합, GAP 프로모터, fed-batch 128.6 g/L
- 두 논문 모두 동일한 AS (AJ310148.1) 사용

---

## 4. AS CDS 서열 — Twist 합성용

**출처:** NCBI AJ310148.1, CDS 위치 27–1439
**길이:** 1,413 bp (stop codon TGA 포함)

```
ATGGAGCATACACCTCACATTGCTATGGTGCCCACTCCGGGAATGGGTCAT
CTGATCCCCCTCGTTGAGTTCGCTAAACGACTCGTCCTCCGTCACAACTTT
GGCGTCACTTTTATTATCCCAACCGATGGACCTCTCCCTAAAGCACAGAAGA
GTTTTCTTGATGCTCTTCCCGCCGGCGTAAACTATGTTCTTCTTCCCCCGGT
AAGCTTCGACGACTTACCCGCTGATGTTAGGATAGAGACCCGTATTTGTCTC
ACCATCACTCGCTCTCTCCCGTTTGTTCGGGATGCCGTTAAGACTCTACTCG
CCACCACCAAGTTAGCTGCTCTAGTGGTGGATCTTTTCGGCACCGATGCATT
TGATGTTGCAATTGAGTTCAAGGTCTCCCCTTATATCTTCTATCCTACGACG
GCCATGTGCCTGTCTCTTTTCTTTCACTTGCCTAAGCTTGATCAAATGGTGT
CCTGCGAATATAGAGACGTCCCAGAACCATTGCAGATTCCAGGATGCATACC
CATTCACGGGAAGGATTTTCTTGACCCAGCTCAGGATCGCAAAAATGATGCC
TACAAATGCCTCCTTCACCAGGCCAAGAGATACCGGTTAGCTGAGGGTATCA
TGGTCAACACCTTCAACGACTTGGAGCCAGGACCCTTAAAAGCTTTGCAGGA
GGAAGACCAGGGTAAGCCACCCGTTTATCCGATCGGACCACTCATCAGAGCG
GATTCAAGCAGCAAGGTCGACGACTGTGAATGTTTGAAATGGCTAGATGACC
AGCCACGTGGGTCGGTTCTGTTTATTTCTTTCGGAAGCGGTGGGGCAGTCTC
CCATAATCAGTTCATTGAGCTAGCTTTGGGATTAGAGATGAGCGAGCAAAGA
TTCTTGTGGGTTGTCCGAAGCCCAAATGATAAAATTGCGAATGCAACGTATT
TCAGCATTCAAAATCAGAATGATGCTCTTGCATATCTGCCAGAAGGATTCTTG
GAGAGAACCAAGGGGCGTTGTCTTTTGGTCCCGTCTTGGGCGCCGCAGACTG
AAATTCTTAGCCATGGTTCCACGGGTGGATTTCTAACCCACTGCGGGTGGAAC
TCTATTCTTGAGAGTGTAGTTAATGGGGTGCCGCTAATTGCTTGGCCTCTTT
ATGCAGAGCAAAAGATGAACGCCGTAATGTTGACGGAGGGTCTTAAAGTGGC
CCTGAGGCCAAAAGCCGGTGAAAATGGCTTGATAGGCCGAGTCGAGATCGCC
AATGCCGTTAAGGGCTTAATGGAGGGAGAGGAAGGAAAGAAGTTCCGCAGCA
CAATGAAAGACCTAAAAGATGCGGCATCGAGGGCGCTAAGTGA
```

### 4-1. Twist 주문 전 체크리스트

- [ ] **S. cerevisiae 코돈 최적화** — 필수 (식물 유래 서열, 효모 발현 비최적화)
  - Twist 주문 시 Codon Optimization 옵션에서 *S. cerevisiae* 선택
  - 또는 [JCat](http://www.jcat.de) / IDT CodonOpt 사전 최적화 후 제출
- [ ] 발현 벡터에 맞는 **제한효소 사이트** 또는 **Gibson assembly overlap** 추가
- [ ] 발현 벡터 확정 (pYES2, pESC, 또는 기타)
- [ ] 프로모터 / 터미네이터 선택

---

## 5. 현재 실험 진행 상황 (2026-05-30 기준)

### 완료
- [x] Chassis yeast 구축 및 검증 (sucrose 배지 생장 억제 확인)
- [x] DBTL 라이브러리 제작 완료
- [x] UDPGH assay 작동 확인

### 진행 중
- [x] S11E, R456K (#3) — E. coli transformation 완료, colony 확인 예정
- [x] S11E, R456K, R59S (#4) — E. coli transformation 완료, colony 확인 예정
- [ ] 나머지 8종 (WT, S11E, #5~#10) — 미착수
- [ ] 확보된 3종 yeast transformation 진행 중
- [ ] Figure 1용 yeast culture 진행 중

### 대기 중
- [ ] His-tag 변이체 발현 및 활성 비교 (Fig 3)
- [ ] Coupled system Reb D 생산 비교 (Fig 4)

### 기술적 이슈 해결
**Synterm 문제 → N-term His-tag으로 우회**
- GmSUS C-말단 Synterm (TA-rich, 시퀀싱 저해, 제거 시 발현량 저하)
- 해결책: C-term His-tag 포기 → N-term His-tag 전환 (Inverse PCR + self-ligation)
- 2026-05-30 E. coli transformation 완료 → colony 확인 예정

---

## 6. Figure 구성 계획

| Figure | 내용 | 상태 |
|--------|------|------|
| Fig 1 | UDP-glucose 농도 vs Reb D 생산량 | Yeast culture 진행 중 |
| Fig 2 | DBTL workflow + chassis yeast 구축 + variant screening | 진행 중 |
| Fig 3 | UDPGH assay scheme + selected variants 활성 비교 + kinetics | UDPGH assay 확인 ✅ |
| Fig 4 | Coupled system Reb D 생산량 비교 (WT vs engineered SuSy) | 대기 중 |
| Fig 5 | 조건 최적화 (sucrose 농도, SuSy:UGTSL ratio 등) | 대기 중 |

---

## 7. SuSy 변이체 후보군

**기반 변이:** S11E, R456K, R59S

| 추가 변이 | 출처 | 비고 |
|-----------|------|------|
| Y224N | DBTL (고빈도) | CTD-GT-B hinge 유연성 |
| L294F | DBTL (고빈도) | catalytic loop 지지 |
| N128A | DBTL (고빈도) / ML 예측 | CTD-EPBD 경계 |
| Y97F | DBTL (고빈도) | N-말단 조절 신호 감쇠 |
| A49T | DBTL (고빈도) | 표면 안정성 보조 |
| L62Q | ML 예측 | CTD 국소 유연성 |
| L76Q | ML 예측 | — |

**ML 모델:** ESM-C embedding + XGBoost, 정확도 0.96 (positive/negative 각 ~12,000 sequence)
