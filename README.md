# 교육리더십 파이썬 코딩 예제 모음

방금 작성했던 5가지 교육리더십 및 행정 관련 파이썬 코드들입니다.

## 1. 리더십 스타일 자가 진단 (edu_1_leadership_style.py)
변혁적 리더십(Transformational)과 거래적 리더십(Transactional) 문항을 통해 자신의 리더십 성향을 진단합니다.

```python
# edu_1_leadership_style.py
# 리더십 유형 진단: 변혁적 리더십 vs 거래적 리더십
# 각 항목에 대해 1~5점 점수를 입력받아 주된 리더십 스타일을 판별합니다.

print("=== 리더십 스타일 자가 진단 (1: 전혀 아님 ~ 5: 매우 그렇다) ===")

# 변혁적 리더십 (Transformational) 관련 문항
t1 = int(input("1. 나는 구성원에게 비전을 제시하고 영감을 준다: "))
t2 = int(input("2. 나는 구성원의 개인적 성장을 돕는다: "))
trans_score = t1 + t2

# 거래적 리더십 (Transactional) 관련 문항
c1 = int(input("3. 나는 성과에 대한 보상을 명확히 한다: "))
c2 = int(input("4. 나는 규칙 위반 시 즉각 시정한다: "))
transac_score = c1 + c2

print("-" * 30)
print(f"변혁적 리더십 점수: {trans_score}점")
print(f"거래적 리더십 점수: {transac_score}점")
print("-" * 30)

if trans_score > transac_score:
    print("당신은 '변혁적 리더십' 성향이 강합니다.")
    print("구성원의 동기부여와 변화를 이끄는 데 강점이 있습니다.")
elif transac_score > trans_score:
    print("당신은 '거래적 리더십' 성향이 강합니다.")
    print("조직의 안정적 운영과 성과 보상에 강점이 있습니다.")
else:
    print("두 가지 리더십 성향이 균형을 이루고 있습니다.")
```

---

## 2. 동기부여 점수 계산기 (edu_2_motivation_calc.py)
브룸(Vroom)의 기대이론(Expectancy Theory) 공식 `(M = E x I x V)`을 활용하여 교사의 동기부여 수준을 수치화합니다.

```python
# edu_2_motivation_calc.py
# 브룸(Vroom)의 기대이론(Expectancy Theory) 계산기
# 동기(Motivation) = 기대감(E) x 수단성(I) x 유의성(V)

print("=== 교사 동기부여 계산기 (Vroom의 기대이론) ===")

# 기대감 (Expectancy): 노력이 성과로 이어질 확률 (0.0 ~ 1.0)
expectancy = float(input("기대감 (노력하면 성과를 낼 수 있는가? 0.0~1.0): "))

# 수단성 (Instrumentality): 성과가 보상으로 이어질 확률 (0.0 ~ 1.0)
instrumentality = float(input("수단성 (성과를 내면 보상을 받는가? 0.0~1.0): "))

# 유의성 (Valence): 보상에 대한 개인적 가치 (-10 ~ +10)
valence = int(input("유의성 (그 보상이 나에게 얼마나 가치 있는가? -10~10): "))

# 동기 점수 계산
motivation = expectancy * instrumentality * valence

print(f"\n계산된 동기부여 점수: {motivation:.2f}점")

if motivation > 5:
    print("분석: 동기부여 수준이 매우 높습니다!")
elif motivation > 0:
    print("분석: 긍정적인 동기가 부여되어 있습니다.")
elif motivation == 0:
    print("분석: 동기가 전혀 없습니다. (어느 한 요인이 0임)")
else:
    print("분석: 역효과(부정적 동기)가 발생할 수 있습니다.")
```

---

## 3. 의사결정 대안 평가 (edu_3_decision_matrix.py)
합리적 의사결정 모형에 따라 비용과 영향력에 가중치를 두어 학교 개선 사업의 우선순위를 결정합니다.

```python
# edu_3_decision_matrix.py
# 합리적 의사결정 모형: 가중치 평가표
# 여러 학교 개선 대안 중 가장 높은 점수를 받은 대안을 선택

# 평가 기준 가중치 설정 (총합 1.0)
w_cost = 0.4      # 비용 효율성
w_impact = 0.6    # 학생 영향력

def calculate_score(cost_score, impact_score):
    return (cost_score * w_cost) + (impact_score * w_impact)

# 대안 리스트 [대안명, 비용점수, 영향력점수]
options = [
    ["도서관 리모델링", 70, 90],
    ["급식실 현대화", 80, 85],
    ["스마트패드 보급", 60, 95]
]

best_option = ""
max_score = -1

print("=== 학교 개선 사업 우선순위 결정 ===")
print(f"가중치 -> 비용: {w_cost}, 영향력: {w_impact}")

for opt in options:
    name = opt[0]
    score_c = opt[1]
    score_i = opt[2]
    
    final_score = calculate_score(score_c, score_i)
    print(f"- {name}: {final_score:.1f}점")
    
    if final_score > max_score:
        max_score = final_score
        best_option = name

print("-" * 30)
print(f"최종 결정: '{best_option}' 대안이 가장 적합합니다.")
```

---

## 4. 갈등 해결 스타일 분석 (edu_4_conflict_mode.py)
토마스-킬만(Thomas-Kilmann) 모델을 기반으로 독단성과 협조성 점수에 따라 갈등 관리 유형을 4가지로 분류합니다.

```python
# edu_4_conflict_mode.py
# 토마스-킬만(Thomas-Kilmann) 갈등 관리 유형 분석
# 자신의 주장을 관철하려는 '독단성'과 상대를 배려하는 '협조성' 두 축으로 판단

def check_conflict_mode(assertiveness, cooperativeness):
    # 중앙값 기준 5점 (0~10점 척도 가정)
    if assertiveness >= 5 and cooperativeness >= 5:
        return "협력형 (Collaborating)"
    elif assertiveness >= 5 and cooperativeness < 5:
        return "경쟁형 (Competing)"
    elif assertiveness < 5 and cooperativeness >= 5:
        return "수용형 (Accommodating)"
    else:
        return "회피형 (Avoiding)"
    # 타협형은 복잡하므로 여기서는 생략하거나 정중앙으로 간주

print("=== 갈등 해결 스타일 분석 (0~10점) ===")
my_assert = int(input("독단성 (내 주장을 얼마나 강하게 내세우는가?): "))
my_coop = int(input("협조성 (상대방 의견을 얼마나 들어주는가?): "))

try:
    if my_assert == 5 and my_coop == 5:
        mode = "타협형 (Compromising)"
    else:
        mode = check_conflict_mode(my_assert, my_coop)
        
    print(f"당신의 갈등 해결 스타일은 '{mode}' 입니다.")

except Exception as e:
    print("올바른 숫자를 입력해주세요.")
```

---

## 5. 학교 예산 편성 시뮬레이션 (edu_5_budget_plan.py)
총 예산에서 고정비를 제외한 가용 자원을 계산하고, 부서별 신청액이 초과될 경우 비율대로 삭감 조정하는 예산 행정 로직입니다.

```python
# edu_5_budget_plan.py
# 단위학교 예산 편성 시뮬레이션
# 총 예산에서 필수 고정비를 제외하고 자율 운영비를 분배

total_budget = int(input("내년도 학교 총 예산(만원)을 입력하세요: "))

# 고정비 (인건비, 시설유지비 등) - 전체의 약 70% 가정
fixed_cost = int(total_budget * 0.7)
avail_budget = total_budget - fixed_cost

print(f"\n총 예산: {total_budget}만원")
print(f"고정경비(예상): {fixed_cost}만원")
print(f"가용 재원(자율 예산): {avail_budget}만원")
print("-" * 30)

# 부서별 예산 신청
depts = ["교무기획부", "교육연구부", "생활안전부", "방과후학교부"]
requests = {}
total_req = 0

print("각 부서별 예산 신청액을 입력받습니다.")
for dept in depts:
    amount = int(input(f"{dept} 신청액(만원): "))
    requests[dept] = amount
    total_req += amount

print("-" * 30)
if total_req <= avail_budget:
    print(f"모든 부서의 예산 신청이 승인되었습니다. (잔액: {avail_budget - total_req}만원)")
else:
    print(f"예산 초과입니다! (초과액: {total_req - avail_budget}만원)")
    print("일괄 삭감 비율을 적용하여 조정합니다...")
    
    ratio = avail_budget / total_req
    for dept, amt in requests.items():
        adjusted = int(amt * ratio)
        print(f"{dept}: {amt} -> {adjusted}만원 (조정됨)")
```
