# 건축/인테리어 파이썬 코딩 예제 모음

방금 작성했던 5가지 건축 실무 관련 파이썬 코드들입니다.

## 1. 면적 단위 변환기 (arch_1_area_converter.py)
제곱미터($m^2$)를 평 단위로 변환하는 기초적인 프로그램입니다.

```python
# arch_1_area_converter.py
# 건축 기초: 면적 단위 변환기 (제곱미터 -> 평)

def m2_to_pyung(m2_area):
    # 1 제곱미터 = 0.3025 평
    pyung = m2_area * 0.3025
    return pyung

print("=== 면적 단위 변환기 ===")
area_input = float(input("면적을 제곱미터(m²) 단위로 입력하세요: "))

pyung_result = m2_to_pyung(area_input)

print(f"입력하신 {area_input}m²는 약 {pyung_result:.2f}평 입니다.")
```

---

## 2. 타일 소요량 계산기 (arch_2_tile_calc.py)
방 크기에 맞춰 바닥 타일이 몇 장 필요한지 계산하며, 자투리를 고려해 올림(`math.ceil`) 처리를 합니다.

```python
# arch_2_tile_calc.py
# 타일 소요량 계산기 (올림 처리 포함)
import math

print("=== 바닥 타일 계산기 ===")

# 방의 크기 입력 (cm 단위)
room_width = int(input("방의 가로 길이를 입력하세요(cm): "))
room_height = int(input("방의 세로 길이를 입력하세요(cm): "))

# 타일 한 장의 크기 (30cm x 30cm 가정)
tile_size = 30 

# 가로, 세로에 들어가는 타일 개수 계산 (여분을 위해 올림 처리)
count_w = math.ceil(room_width / tile_size)
count_h = math.ceil(room_height / tile_size)

total_tiles = count_w * count_h

print(f"가로 {count_w}장, 세로 {count_h}장이 필요합니다.")
print(f"총 필요한 타일 개수: {total_tiles}장")
# 파손 대비 여유분 10% 추가 안내
print(f"(여유분 포함 권장 구매량: {math.ceil(total_tiles * 1.1)}장)")
```

---

## 3. 원형 기둥 콘크리트 부피 (arch_3_concrete_vol.py)
원기둥의 부피 공식($\pi r^2 h$)을 이용해 필요한 레미콘 양을 계산합니다.

```python
# arch_3_concrete_vol.py
# 원형 기둥 콘크리트 부피 계산하기
import math

print("=== 원형 기둥 콘크리트 부피 계산 ===")

radius = float(input("기둥의 반지름(m)을 입력하세요: "))
height = float(input("기둥의 높이(m)를 입력하세요: "))
count = int(input("기둥의 개수를 입력하세요: "))

# 원기둥 부피 공식 = 원주율 * 반지름^2 * 높이
# math.pi를 사용하면 정확한 원주율을 쓸 수 있습니다.
volume_one = math.pi * (radius ** 2) * height
total_volume = volume_one * count

print(f"기둥 1개의 부피: {volume_one:.2f}㎥")
print(f"총 {count}개 기둥에 필요한 레미콘 부피: {total_volume:.2f}㎥")
```

---

## 4. 벽돌 소요량 산출 (arch_4_brick_count.py)
벽 전체 면적에서 창문 면적을 뺀(Net Area) 뒤 벽돌 소요량을 계산합니다.

```python
# arch_4_brick_cound.py
# 벽면 조적(벽돌 쌓기) 수량 산출 (창문 면적 제외)

print("=== 벽돌 소요량 계산 (창문 제외) ===")

# 벽 전체 크기
wall_w = float(input("벽의 가로 길이(m): "))
wall_h = float(input("벽의 세로 길이(m): "))

# 창문 크기
window_w = float(input("창문의 가로 길이(m): "))
window_h = float(input("창문의 세로 길이(m): "))

# 순수 벽돌 시공 면적 = 벽 면적 - 창문 면적
net_wall_area = (wall_w * wall_h) - (window_w * window_h)

# 1제곱미터당 벽돌 소요량 (표준 벽돌 0.5B 쌓기 기준 약 75장이라 가정)
bricks_per_m2 = 75

total_bricks = net_wall_area * bricks_per_m2

print(f"시공해야 할 실제 벽 면적: {net_wall_area:.2f}m²")
print(f"예상 소요 벽돌 수: 약 {int(total_bricks)}장")
```

---

## 5. 공사비 간편 견적 (arch_5_cost_est.py)
자재 등급(고급/중급/보급)에 따라 평당 단가를 다르게 적용하여 총공사비를 계산합니다.

```python
# arch_5_cost_est.py
# 건축 공사비 간편 견적서

def calculate_cost(area_pyung, material_grade):
    # 평당 공사비 단가 (단위: 만원)
    if material_grade == "고급":
        price_per_pyung = 800
    elif material_grade == "중급":
        price_per_pyung = 600
    else: # 보급형
        price_per_pyung = 450
        
    total_price = area_pyung * price_per_pyung
    return total_price

print("=== 간편 공사비 견적 시스템 ===")
pyung = float(input("건축 연면적(평)을 입력하세요: "))
grade = input("자재 등급을 입력하세요 (고급/중급/보급): ")

estimated_cost = calculate_cost(pyung, grade)

print("----------------------------")
print(f"면적: {pyung}평")
print(f"등급: {grade}")
print(f"예상 건축비: {estimated_cost:,.0f}만 원") # 1000단위 쉼표 표시
print("----------------------------")
```
