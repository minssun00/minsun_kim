# 연구 프로젝트: DBTL 기반 Sucrose Synthase 엔지니어링을 통한 Reb D 생산 시스템 구축

## 연구 개요

Sucrose synthase (GmSUS, *Glycine max*)를 DBTL 전략으로 엔지니어링하여 UDP-glucose donor regeneration 효율을 높이고, UGTSL과 커플링하여 고부가가치 steviol glycoside인 Reb D를 생산하는 in vitro bioconversion 시스템 구축.

## 핵심 반응 체계

```
[Donor regeneration] GmSUS 역반응
  Sucrose + UDP  →  UDP-Glucose + Fructose

[Product formation] UGTSL 반응
  Reb A + UDP-Glucose  →  Reb D + UDP

[UDP 재생 사이클]
  UDP가 두 반응 사이에서 순환 재사용됨
```

## 논문 스토리 구조

**Core problem:** UGTSL-mediated Reb A → Reb D 전환 효율은 UDP-glucose 공급 능력에 좌우됨. SuSy는 sucrose로부터 UDP-glucose를 in situ 재생할 수 있지만, 낮은 reverse performance와 비효율적 sucrose utilization이 bottleneck.

**Solution:** DBTL-guided SuSy engineering → donor regeneration efficiency 향상 → practical Reb D bioconversion system 구축

**확장성:** SuSy-UGTSL 시스템은 하위 GT만 교체하면 다양한 UDP-glucose 의존적 당전이 반응에 적용 가능한 modular platform

## 시스템 구성

### In vitro (논문 메인)
- **GmSUS:** His-tag 정제 효소
- **UGTSL:** Reb A → Reb D 핵심 glycosyltransferase
- **Activity assay:** UDPGH coupling assay
  - Sucrose + UDP → UDP-Glucose + Fructose
  - UDP-Glucose + NAD⁺ →[UDPGH]→ UDP-Gluconate + NADH (340nm 측정)
  - 조건: 50 mM HEPES (pH 7.5), 10 mM MgCl₂, NAD⁺, UDPGH 10 µL (1 g/L)
  - UDPGH assay 작동 확인 ✅

### Chassis yeast (SuSy 변이체 스크리닝 용도)
- *S. cerevisiae* CEN.PK2-1C 기반
- Sucrose invertase 유전자 전체 deletion → sucrose 배지 생장 억제 확인 ✅
- Fructose를 에너지원으로 사용 → SuSy reverse activity 기반 in vivo 스크리닝
- **※ Reb D in vivo 생산 목적 아님** (Reb A 분자량 ~967 Da, 세포막 투과 불가)

### 미래 방향 (이번 논문 범위 외)
- β-Arbutin in vivo 생산: hydroquinone (소분자, 막 투과 용이) → AS → β-Arbutin
  - *S. cerevisiae*에서 β-arbutin 생산 사례 없음 → 차별점
  - EU의 hydroquinone 화장품 금지로 생물학적 arbutin 생산 수요 급증
  - β-arbutin 글로벌 시장 ~10.95억 달러 (2024), CAGR 6.05%

#### β-Arbutin 합성 핵심 효소
- **AS (Arbutin Synthase)**
  - Accession: **AJ310148.1**
  - 출처: *Rauvolfia serpentina* (Arend et al., 2001)
  - 반응: Hydroquinone + UDP-glucose → β-Arbutin + UDP (EC 2.4.1.218)
  - 참고: Zhang et al. 2026 (*Food Bioscience*), Yang et al. 2024 (*Microbial Cell Factories*)에서 사용
- **합성 전략:** Hydroquinone 외부 공급 + GmSUS가 UDP-glucose 공급 → AS만 발현하면 됨
- **합성 시 고려사항:** *S. cerevisiae* 코돈 최적화, signal peptide 없이 세포질 발현
- **참고:** Yang et al. 2024에서 MNX1-AS 융합단백질(GGGS linker)로 HQ 산화 방지 → titer 19.7% 향상. 민선씨 연구에서는 HQ 외부 공급이므로 MNX1 불필요하나, HQ 독성/산화 문제 발생 시 참고 가능
- **참고문헌:**
  - Yang et al. 2024, *Microbial Cell Factories* (AS 동일, 128.6 g/L in K. phaffii)
  - Zhang et al. 2026, *Food Bioscience* (AS 동일, 70.87 g/L in K. phaffii)

## DBTL 전략

- **협력:** 고려대 (실험) + KRIBB 생명연 (ML / 구조 분석)
- **랜덤 mutagenesis 라이브러리:** 제작 완료 (고려대)
- **ML 모델:** ESM-C embedding (pretrained) + XGBoost, 정확도 0.96
  - Dataset: positive/negative 각 약 12,000개 sequence
- **구조 분석:** AlphaFold3 + ProteinMPNN 기반 (KRIBB, 진행 중)

## SuSy 변이체 후보군

기반 변이: **S11E, R456K, R59S**

| 추가 변이 | 출처 | 비고 |
|-----------|------|------|
| Y224N | DBTL (고빈도) | CTD-GT-B hinge 유연성 |
| L294F | DBTL (고빈도) | catalytic loop 지지 |
| N128A (=L128A) | DBTL (고빈도) / ML 예측 | CTD-EPBD 경계 |
| Y97F  | DBTL (고빈도) | N-말단 조절 신호 감쇠 |
| A49T  | DBTL (고빈도) | 표면 안정성 보조 |
| L62Q  | ML 예측 | CTD 국소 유연성 |
| L76Q  | ML 예측 | - |

## Figure 구성 계획

| Figure | 내용 | 상태 |
|--------|------|------|
| Fig 1 | UDP-glucose 농도 vs Reb D 생산량 (UGTSL 반응이 donor에 의존함을 증명) | Yeast culture 진행 중 |
| Fig 2 | DBTL workflow + chassis yeast 구축 + variant screening | 진행 중 |
| Fig 3 | UDPGH assay scheme + selected variants 활성 비교 + kinetics | UDPGH assay 확인 ✅ |
| Fig 4 | Coupled system에서 Reb D 생산량 비교 (WT vs engineered SuSy) | 대기 중 |
| Fig 5 | 조건 최적화 (sucrose 농도, SuSy:UGTSL ratio 등) + practical performance | 대기 중 |

## 현재 실험 진행 상황

- [x] Chassis yeast 구축 및 검증 (sucrose 배지 생장 억제 확인)
- [x] DBTL 라이브러리 제작 완료
- [x] UDPGH assay 작동 확인
- [ ] Plasmid 확보 진행 중 (10종 중 2종 transformation 완료, 2026-05-30)
  - 🔄 S11E, R456K (#3) — E. coli transformation 완료, colony 확인 예정
  - 🔄 S11E, R456K, R59S (#4) — E. coli transformation 완료, colony 확인 예정
  - ⏳ 나머지 8종 (WT, S11E, #5~#10) — 미착수
- [ ] 확보된 3종 yeast transformation 진행 중
- [ ] Figure 1용 yeast culture 진행 중
- [ ] His-tag 변이체 발현 및 활성 비교 (Fig 3)
- [ ] Coupled system Reb D 생산 비교 (Fig 4)

## 현재 기술적 문제 및 해결

**Synterm 문제 → N-term His-tag으로 우회 (2026-05-30)**
- GmSUS C-말단 Synterm (TA-rich, 시퀀싱 저해, 제거 시 발현량 저하)
- 해결책: C-term His-tag 포기 → **N-term His-tag**으로 전환
  - Inverse PCR로 insert 삽입 + self-ligation
  - 2026-05-30 E. coli transformation 완료 → colony 확인 예정

## 논문 일정 및 목표 저널

- **투고 목표:** 2026년 7월
- **Target journal:** Bioresource Technology
  - DBTL-guided enzyme engineering + in vitro bioconversion system → scope 적합
  - 프레이밍: food sweetener보다 **bioconversion 효율, 효소 시스템 엔지니어링, 공정 최적화** 측면 강조 필요

## 주요 논의 사항

- Reb D in vivo 불가 이유: Reb A (MW ~967 Da, 고친수성) 세포막 투과 불가
- Yeast surface display는 시간 소요로 이번 논문 범위 외, 향후 과제
- β-arbutin in vivo 생산은 다음 논문 방향으로 검토 중
