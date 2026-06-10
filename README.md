# 🔥 GeoAI Classification Model in Chiang Mai: การคาดการณ์พื้นที่เผาใหม่ของพื้นที่เชียงใหม่ด้วย XGBoost

## 📖 ภาพรวมของโปรเจกต์ (Project Overview)
โปรเจกต์นี้คือการสร้าง **GeoAI Classification Model** เพื่อคาดการณ์ว่า พื้นที่บริเวณนั้นจะเกิดการเผาไหม้ซ้ำหรือไม่ โดยวิเคราะห์จากข้อมูลในอดีต ซึ่งข้อมูลถูกเก็บในทุกๆ 10 วันของแต่ละเดือน ตั้งแต่วันที่ 1 มกราคม 2026 - 30 เมษายน 2026 เป็นเวลา 4 เดือน

วัตถุประสงค์ของโปรเจคนี้ :
> *"ในอีก 10 วันถัดไป พื้นที่กริดไหนมีโอกาสเกิดไฟป่าขึ้นอีก?"*

---

## ⚙️ สถาปัตยกรรมและการทำงาน (Workflow & Methodology)

เราใช้ **XGBoost** ซึ่งเป็น Machine Learning Model ที่มีประสิทธิภาพสูงในการดึงแพทเทิร์นที่ซับซ้อนจากข้อมูลเชิงพื้นที่ โดยสามารถดูขั้นตอนการทำงานได้จาก Flowchart ด้านล่างนี้:

```mermaid
graph TD
    %% กำหนดสีของกล่อง
    classDef input fill:#f9f871,stroke:#333,stroke-width:2px;
    classDef process fill:#00c9a7,stroke:#333,stroke-width:2px,color:#fff;
    classDef model fill:#845ec2,stroke:#333,stroke-width:2px,color:#fff;
    classDef evaluate fill:#ff9671,stroke:#333,stroke-width:2px,color:#000;

    A["นำเข้าข้อมูล Burned Area <br> 10 Days Interval (4 เดือน)"]:::input --> B("เตรียมข้อมูลเชิงพื้นที่ <br> Spatial Grid & Features"):::process
    B --> C{"แบ่งชุดข้อมูล <br> Train / Test Split"}:::process
    
    C -->|"Train Data: 3 เดือน"| D["ฝึกสอนโมเดล <br> XGBoost"]:::model
    C -->|"Test Data: 1 เดือนสุดท้าย"| E["ข้อมูลจริงที่เกิดขึ้น <br> Ground Truth"]:::input
    
    D --> F("สร้างแผนที่ทำนายพื้นที่เกิดไฟ <br> Predictive Map"):::model
    
    F --> G{"เปรียบเทียบผลลัพธ์ <br> Prediction vs Reality"}
    E --> G
    
    G --> H["วัดผลความแม่นยำ <br> 4 Metrics"]:::evaluate
