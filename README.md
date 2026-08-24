# Term Deposit Subscription Prediction

**Machine Learning Classification | Python · Decision Tree · Random Forest · Scikit-learn**

โปรเจกต์พัฒนาโมเดล Machine Learning เพื่อทำนายว่าลูกค้าธนาคารมีแนวโน้มสมัครเงินฝากประจำ (Term Deposit) หรือไม่ โดยใช้ข้อมูลจาก Bank Marketing Dataset และเปรียบเทียบผลระหว่าง Decision Tree กับ Random Forest

## Project Overview

ข้อมูลที่ใช้มีจำนวน **4,521 records** และประกอบด้วยข้อมูลเกี่ยวกับลูกค้าและการติดต่อทางการตลาด เช่น อายุ อาชีพ สถานภาพสมรส ยอดเงินคงเหลือ ระยะเวลาการสนทนา และผลจากการติดต่อครั้งก่อน

ก่อนสร้างโมเดล มีการตรวจสอบข้อมูล แปลงตัวแปรหมวดหมู่ให้อยู่ในรูปแบบที่โมเดลสามารถใช้งานได้ และแบ่งข้อมูลออกเป็น Training และ Test Set

เนื่องจาก Target Class มีสัดส่วนไม่เท่ากัน โดยกลุ่มที่สมัคร Term Deposit มีจำนวนน้อยกว่ากลุ่มที่ไม่สมัคร จึงใช้ `class_weight="balanced"` และพิจารณา Recall ร่วมกับ Accuracy, Precision และ F1-Score ในการเลือกโมเดล

## Objective

- สร้าง Classification Model สำหรับทำนายการสมัคร Term Deposit
- เปรียบเทียบประสิทธิภาพของ Decision Tree และ Random Forest
- ประเมินผลภายใต้ปัญหา Class Imbalance
- วิเคราะห์ Feature Importance เพื่อดูว่าตัวแปรใดมีบทบาทต่อการทำนาย

## Dataset

ข้อมูลก่อนแปลงประกอบด้วย **4,521 records และ 17 columns**

Target Variable คือ `y`

- `0` — ไม่สมัคร Term Deposit
- `1` — สมัคร Term Deposit

จำนวนข้อมูลในแต่ละ Class คือ

- **Class 0:** 4,000 records
- **Class 1:** 521 records

หลังจากแปลงตัวแปรหมวดหมู่ด้วย Encoding ข้อมูลสำหรับสร้างโมเดลมีทั้งหมด **42 features**

## Data Preparation

ขั้นตอนการเตรียมข้อมูลประกอบด้วย

- ตรวจสอบโครงสร้างและชนิดข้อมูล
- ตรวจสอบ Missing Values
- สำรวจข้อมูลด้วย Descriptive Statistics
- แปลง Target Variable ให้อยู่ในรูปแบบตัวเลข
- แปลง Categorical Variables ด้วย One-Hot Encoding
- แยก Features และ Target
- แบ่งข้อมูลเป็น Training และ Test Set
- ทำ Feature Scaling ด้วย StandardScaler

ใช้ `train_test_split()` โดยกำหนด

- **Test Size:** 30%
- **Random State:** 0
- **Stratify:** Target Variable

หลังแบ่งข้อมูลได้

- **Training Set:** 3,164 records
- **Test Set:** 1,357 records

การใช้ Stratified Split ช่วยรักษาสัดส่วนของ Target Class ใน Training และ Test Set ให้ใกล้เคียงกับข้อมูลเดิม

## Models

### Decision Tree

สร้าง Decision Tree Classifier โดยกำหนด

- **Criterion:** Gini
- **Max Depth:** 8
- **Class Weight:** Balanced
- **Random State:** 0

โมเดลถูก Train ด้วยข้อมูลที่ผ่าน StandardScaler แล้ว

### Random Forest

สร้าง Random Forest Classifier สำหรับเปรียบเทียบกับ Decision Tree โดยกำหนด

- **Number of Trees:** 15
- **Max Depth:** None
- **Min Samples Split:** 2
- **Class Weight:** Balanced
- **Random State:** 0

## Model Evaluation

ใช้ตัวชี้วัดในการประเมินโมเดล ได้แก่

- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix

### Model Comparison

| Model | Accuracy | Precision | Recall | F1-Score |
|---|---:|---:|---:|---:|
| Decision Tree | 78.48% | 31.62% | **75.00%** | **44.49%** |
| Random Forest | **88.80%** | **53.70%** | 18.59% | 27.62% |

Random Forest มี Accuracy และ Precision สูงกว่า แต่ Recall สำหรับกลุ่มลูกค้าที่สมัครจริงอยู่ที่ประมาณ **18.59%**

Decision Tree มี Accuracy ต่ำกว่า แต่สามารถตรวจจับกลุ่มลูกค้าที่สมัครได้ดีกว่า โดยมี Recall **75%** และ F1-Score สูงกว่า Random Forest

เนื่องจากเป้าหมายของโปรเจกต์ต้องการให้โมเดลสามารถตรวจจับกลุ่มลูกค้าที่มีแนวโน้มสมัครได้ จึงเลือก Decision Tree เป็น Final Model

## Final Model

**Decision Tree Classifier**

ผลการประเมิน Final Model บน Test Set คือ

- **Accuracy:** 78.48%
- **Precision:** 31.62%
- **Recall:** 75.00%
- **F1-Score:** 44.49%

### Confusion Matrix

```text
[[948 253]
 [ 39 117]]
```

จากลูกค้าที่สมัครจริงทั้งหมด **156 ราย**

- ทำนายถูกว่าเป็นผู้สมัคร 117 ราย
- ทำนายผิดว่าไม่สมัคร 39 ราย

จึงได้ Recall เท่ากับ **75%**

## Feature Importance

จาก Decision Tree พบว่า `duration` เป็น Feature ที่มี Importance สูงที่สุด ประมาณ **0.529**

ตัวแปรที่มี Importance สูงในลำดับต้น ๆ ได้แก่

| Feature | Importance |
|---|---:|
| `duration` | 0.529 |
| `poutcome_success` | 0.081 |
| `contact_unknown` | 0.072 |
| `age` | 0.057 |
| `balance` | 0.039 |
| `day` | 0.028 |
| `pdays` | 0.026 |

## Key Insight

`duration` หรือระยะเวลาในการสนทนากับลูกค้าเป็น Feature ที่มีอิทธิพลต่อ Decision Tree สูงที่สุด

อย่างไรก็ตาม ตัวแปรนี้มีข้อจำกัดในการนำไปใช้งานจริงสำหรับการทำนายก่อนเริ่มติดต่อ เนื่องจากระยะเวลาการสนทนาจะทราบได้หลังจากการโทรหาลูกค้าเกิดขึ้นแล้ว

ดังนั้น หากต้องการนำโมเดลไปใช้เพื่อคัดเลือกลูกค้าก่อนเริ่มแคมเปญ ควรพิจารณาสร้างโมเดลอีกเวอร์ชันโดยไม่ใช้ `duration`

## Limitations

- ข้อมูลมีปัญหา Class Imbalance ระหว่างลูกค้าที่สมัครและไม่สมัคร
- Precision ของ Final Model ยังอยู่ในระดับต่ำ จึงมี False Positive ค่อนข้างมาก
- ตัวแปร `duration` มี Feature Importance สูง แต่ไม่เหมาะสำหรับใช้ทำนายก่อนการติดต่อ
- โมเดลในโปรเจกต์นี้ยังไม่ได้ทำ Hyperparameter Tuning แบบละเอียด

## Skills Demonstrated

- Data Preprocessing
- Exploratory Data Analysis
- Categorical Encoding
- Feature Scaling
- Stratified Train/Test Split
- Machine Learning Classification
- Decision Tree
- Random Forest
- Class Imbalance Analysis
- Model Evaluation
- Confusion Matrix Analysis
- Feature Importance

## Tools & Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Google Colab / Jupyter Notebook

## Project Activities

โปรเจกต์นี้ครอบคลุมตั้งแต่การเตรียมและสำรวจข้อมูล การแปลงตัวแปร การแบ่ง Training/Test Set การสร้าง Decision Tree และ Random Forest การเปรียบเทียบผลของโมเดล ไปจนถึงการวิเคราะห์ Feature Importance และข้อจำกัดของ Final Model

## Project Files

```text
term-deposit-subscription-prediction/
│
├── README.md
└── term-deposit-subscription-prediction.ipynb
```

## Project Type

**Academic Project — Machine Learning Classification**

โปรเจกต์นี้จัดทำขึ้นเพื่อประยุกต์ใช้ Machine Learning กับปัญหา Binary Classification โดยเน้นการเปรียบเทียบโมเดลภายใต้ Class Imbalance และพิจารณา Metric มากกว่า Accuracy เพียงอย่างเดียวในการเลือก Final Model

> **Note:** Repository นี้จัดทำขึ้นเพื่อการศึกษาและการนำเสนอผลงานใน Portfolio
