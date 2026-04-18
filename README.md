# Term Deposit Subscription Prediction (ML)
> **Predicting Banking Customer Behavior using Decision Tree Classifier and Feature Engineering**

โปรเจกต์พัฒนาแบบจำลองการเรียนรู้ของเครื่อง (Machine Learning) เพื่อพยากรณ์โอกาสที่ลูกค้าธนาคารจะตัดสินใจสมัครบริการเงินฝากประจำ (Term Deposit) โดยวิเคราะห์จากฐานข้อมูลการตลาดของธนาคาร เพื่อเพิ่มประสิทธิภาพในการคัดกรองกลุ่มเป้าหมาย

## 📌 บทสรุปโครงการ (Project Overview)
* **วัตถุประสงค์ (Objective):** เพื่อสร้างแบบจำลองจำแนกประเภท (Classification Model) ที่สามารถระบุปัจจัยสำคัญและทำนายพฤติกรรมการตัดสินใจสมัครบริการของลูกค้าได้อย่างแม่นยำ
* **ปัญหา (Problem):** การติดต่อลูกค้าแบบเหมาสวม (Mass Marketing) สิ้นเปลืองทรัพยากรและเวลา การทราบล่วงหน้าว่าลูกค้าคนใดมีแนวโน้มจะสมัคร จะช่วยให้ทีมขายโฟกัสได้ถูกจุดและเพิ่ม Conversion Rate
* **ข้อมูล (Data):** ชุดข้อมูล Bank Marketing (Campaign Data) ที่ประกอบด้วยข้อมูลประชากร พฤติกรรมการติดต่อในอดีต และปัจจัยด้านเศรษฐกิจ

## 🛠️ เทคนิคและเครื่องมือ (Tech Stack)
* **Language:** Python 3
* **Libraries:** `Pandas`, `NumPy`, `Scikit-learn`, `Matplotlib`, `Seaborn`
* **Machine Learning Model:** **Decision Tree Classifier**
* **Techniques:**
    * **Data Cleaning & Preprocessing:** จัดการค่าที่ขาดหายและแปลงตัวแปรหมวดหมู่ (Label Encoding)
    * **Feature Engineering:** คัดเลือกและเตรียมตัวแปรที่มีอิทธิพลต่อผลลัพธ์
    * **Model Visualization:** การแสดงผลลำดับการตัดสินใจของต้นไม้ (Tree Plot)

## 📊 ขั้นตอนการดำเนินงาน (Methodology)
1. **Exploratory Data Analysis (EDA):** สำรวจความสัมพันธ์ระหว่างปัจจัยต่างๆ เช่น อายุ อาชีพ และระยะเวลาการสนทนา กับผลการสมัครบริการ
2. **Data Split:** แบ่งข้อมูลเป็นชุด Training และ Testing เพื่อประเมินประสิทธิภาพความแม่นยำของแบบจำลอง
3. **Model Training:** ฝึกสอนแบบจำลอง Decision Tree เพื่อสร้างกฎในการจำแนกลูกค้า (Decision Rules)
4. **Feature Importance Analysis:** วิเคราะห์หาตัวแปรที่มีอิทธิพลสูงสุดต่อแบบจำลอง

## 🚀 ผลการศึกษาและ Insights (Results & Insights)
* **Key Discovery:** พบว่า **"ระยะเวลาที่ใช้ในการสนทนา" (Duration)** เป็นปัจจัยที่มีผลต่อการตัดสินใจสมัครมากที่สุด (Importance Score สูงถึง 0.53)
* **Business Insight:** ลูกค้าที่ใช้เวลาฟังข้อมูลและซักถามเป็นเวลานาน มีแนวโน้มที่จะตอบรับบริการสูงกว่าปกติ ซึ่งสะท้อนถึงคุณภาพของการโน้มน้าวใจในกระบวนการขาย
* **Performance:** แบบจำลองสามารถจำแนกกลุ่มลูกค้าที่มีแนวโน้มสมัครออกจากกลุ่มที่ไม่สมัครได้อย่างเป็นระบบ ช่วยลดภาระงานของฝ่ายการตลาดในการติดต่อลูกค้าที่ไม่ใช่กลุ่มเป้าหมาย

---
**Developed by:** Ampika Pratumtong  
**Contact:** Ampika.pratumtong47@gmail.com
