import csv
import random
import os

# Configuration
NUM_CLASSES = 3
STUDENTS_PER_CLASS = 20
OUTPUT_FILE = 'student_scores.csv'

# Korean Name Components
surnames = ['김', '이', '박', '최', '정', '강', '조', '윤', '장', '임', '한', '오', '서', '신', '권', '황', '안', '송', '전', '홍']
first_names = ['민준', '서준', '도윤', '예준', '시우', '하준', '지호', '주원', '지우', '이안', 
               '서연', '서현', '지우', '서윤', '하은', '민서', '지유', '윤서', '채원', '지민',
               '준우', '현우', '다은', '수아', '나연', '예은', '지현', '지원', '혜진', '동현']

def generate_name():
    return random.choice(surnames) + random.choice(first_names)

def generate_data():
    data = []
    headers = ['분반', '번호', '이름', '문항1(20점)', '문항2(20점)', '문항3(20점)', '문항4(20점)', '문항5(20점)', '총점']
    
    for class_num in range(1, NUM_CLASSES + 1):
        for student_num in range(1, STUDENTS_PER_CLASS + 1):
            scores = []
            for _ in range(5):
                # Generate a score between 10 and 20, weighted towards higher scores for realism
                score = random.randint(10, 20)
                scores.append(score)
            
            total_score = sum(scores)
            name = generate_name()
            
            row = [
                f"{class_num}반",
                student_num,
                name,
                scores[0],
                scores[1],
                scores[2],
                scores[3],
                scores[4],
                total_score
            ]
            data.append(row)
            
    return headers, data

def save_to_csv(headers, data):
    with open(OUTPUT_FILE, 'w', newline='', encoding='utf-8-sig') as f:
        writer = csv.writer(f)
        writer.writerow(headers)
        writer.writerows(data)
    print(f"Successfully generated {len(data)} student records to {os.path.abspath(OUTPUT_FILE)}")

if __name__ == "__main__":
    headers, data = generate_data()
    save_to_csv(headers, data)
