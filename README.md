# Dietitian101 - Clinical Reference Library

> **คลังความรู้และศูนย์รวมแนวทางเวชปฏิบัติด้านโภชนบำบัดทางการแพทย์ (Medical Nutrition Therapy: MNT) สำหรับนักกำหนดอาหารและบุคลากรทางการแพทย์**  
> รองรับระบบจัดการเนื้อหาผ่าน **Pages CMS** และการเขียนโค้ด/Markdown ใน **VS Code**

---

## 📋 สารบัญ
1. [ภาพรวมของระบบและสถาปัตยกรรม](#1-ภาพรวมของระบบและสถาปัตยกรรม)
2. [โครงสร้างไฟล์โปรเจกต์ (Project Structure)](#2-โครงสร้างไฟล์โปรเจกต์)
3. [การเชื่อมต่อกับ Pages CMS (.pages.yml)](#3-การเชื่อมต่อกับ-pages-cms)
4. [โครงสร้าง 9 หัวข้อหลักในแต่ละโรค (Clinical Sections)](#4-โครงสร้าง-9-หัวข้อหลักในแต่ละโรค)
5. [ศูนย์รวมแนวทางเวชปฏิบัติ (Clinical Guidelines Center)](#5-ศูนย์รวมแนวทางเวชปฏิบัติ)
6. [ฟีเจอร์เด่นบนหน้าเว็บไซต์](#6-ฟีเจอร์เด่นบนหน้าเว็บไซต์)
7. [ขั้นตอนการรันและพัฒนาใน VS Code](#7-ขั้นตอนการรันและพัฒนาใน-vs-code)

---

## 1. ภาพรวมของระบบและสถาปัตยกรรม

เว็บไซต์นี้ได้รับการออกแบบตามแนวทาง **Clinical Reference Library** ที่เน้นความเรียบง่าย สะอาดตา อ่านง่าย (High Legibility) สไตล์ Medical SaaS (อ้างอิงตาม UI ในห้องตรวจและเคาน์เตอร์โภชนาการ)

- **Frontend:** Vanilla HTML5, Modern CSS3 (CSS Variables, Flexbox, CSS Grid), Modular JavaScript (ES6)
- **CMS Backend:** [Pages CMS](https://pagescms.org) — Git-based Headless CMS ฟรี ไม่มีค่าใช้จ่าย ซิงค์กับ GitHub Repository โดยตรง
- **Data Persistence:** Markdown files พร้อม YAML Frontmatter ใน `content/` + Client-side `localStorage` สำหรับบุ๊กมาร์ก ประวัติการอ่าน และการเลือกสาขาที่สนใจ

---

## 2. โครงสร้างไฟล์โปรเจกต์

```
d:\website\Dietitian101/
├── .pages.yml                          # ไฟล์คอนฟิกของ Pages CMS (นิยามฟิลด์ทั้งหมด)
├── index.html                          # หน้าแรก: Clinical Reference Library (ค้นหา & การ์ดโรค)
├── disease.html                        # หน้าแสดงเนื้อหาโรค (9 หัวข้อ + TOC + Reading Progress)
├── guidelines.html                     # ศูนย์รวมแนวทางเวชปฏิบัติ (Clinical Guidelines)
├── library.html                        # หน้า My Library (Bookmarks, History, Favorites)
├── assets/
│   ├── css/
│   │   └── style.css                   # สไตล์หลักทั้งหมด, ดีไซน์การ์ดพาสเทล, Dark Mode
│   ├── js/
│   │   ├── data.js                     # ข้อมูลโรค 9 หัวข้อ และข้อมูล Guidelines
│   │   ├── app.js                      # Smart Search, Auto Suggest, Bookmarks, Dark Mode, Modals
│   │   └── disease.js                  # Reader Logic, ScrollSpy สารบัญ, Reading Progress
│   └── images/                         # โฟลเดอร์เก็บรูปภาพ/สื่อประกอบ
├── content/
│   ├── diseases/                       # ไฟล์ Markdown แต่ละโรค (แก้ไขผ่าน Pages CMS ได้)
│   │   ├── ckd.md
│   │   ├── type-2-diabetes.md
│   │   ├── malnutrition-refeeding.md
│   │   ├── enteral-feeding.md
│   │   ├── cirrhosis.md
│   │   └── heart-failure.md
│   └── guidelines/                     # ไฟล์ Markdown แนวทางเวชปฏิบัติ
│       ├── kdigo-2024-ckd.md
│       ├── ada-standards-2024.md
│       ├── aspen-refeeding-2020.md
│       ├── espen-icu-2023.md
│       └── tda-thai-renal-2023.md
└── README.md
```

---

## 3. การเชื่อมต่อกับ Pages CMS

**Pages CMS** เป็นระบบจัดการเนื้อหาแบบ Git-based ที่ทำงานผ่านเว็บเบราว์เซอร์ โดยอ่าน schema จากไฟล์ `.pages.yml`:

### วิธีการนำขึ้นใช้งานจริงร่วมกับ Pages CMS:
1. นำโฟลเดอร์ `Dietitian101` อัปโหลดขึ้น **GitHub Repository** (แบบ Public หรือ Private ก็ได้)
2. เข้าเว็บไซต์ [https://pagescms.org](https://pagescms.org)
3. เข้าสู่ระบบด้วยบัญชี GitHub แล้วเลือก Repository ของโปรเจกต์นี้
4. Pages CMS จะสแกนไฟล์ `.pages.yml` อัตโนมัติ และสร้างหน้าแผงควบคุม (Dashboard) สำหรับ:
   - เพิ่ม/แก้ไขโรคใน **Disease Database** พร้อมช่องกรอกทั้ง 9 หัวข้อ
   - เพิ่ม/แก้ไขเอกสารใน **Clinical Practice Guidelines**
5. เมื่อกด Save หรือ Publish ใน Pages CMS ข้อมูลจะถูก Commit กลับเข้าสู่ GitHub อัตโนมัติทันที

---

## 4. โครงสร้าง 9 หัวข้อหลักในแต่ละโรค

ตามมาตรฐานกระบวนการให้การดูแลทางโภชนาการ (Nutrition Care Process: NCP) ทั้ง 9 หัวข้อถูกกำหนดไว้ใน `.pages.yml` ดังนี้:

1. **Overview & Pathophysiology** (ภาพรวมและพยาธิสรีรวิทยา) — นิยาม การแบ่งระยะ (Staging) และกลไกของโรค
2. **Nutrition Assessment** (การประเมินภาวะโภชนาการ) — หลัก ABCD (Anthropometric, Biochemical, Clinical, Dietary)
3. **Nutrition Diagnosis** (การวินิจฉัยทางโภชนาการ) — รูปแบบ PES Statement (Problem, Etiology, Signs/Symptoms)
4. **Nutrition Requirements** (ความต้องการสารอาหาร) — ตารางคำนวณพลังงาน (Energy kcal/kg), โปรตีน (Protein g/kg), เกลือแร่ และของเหลว
5. **Medical Nutrition Therapy (MNT)** (โภชนบำบัดทางการแพทย์) — เป้าหมายและกลยุทธ์การปรับเปลี่ยนสารอาหาร
6. **Food & Dietary Management** (การจัดการอาหารและอาหารแลกเปลี่ยน) — รายการอาหารที่ควรเลือก/ควรจำกัด และแบบจำลองจานอาหาร
7. **Nutrition Monitoring & Evaluation** (การติดตามและประเมินผล) — ตัวชี้วัดผลลัพธ์และระยะเวลาการนัดติดตาม
8. **Clinical Practice Guidelines** (แนวทางเวชปฏิบัติที่เกี่ยวข้อง) — สรุปคำแนะนำจากสมาคมชั้นนำ
9. **References & Further Reading** (เอกสารอ้างอิงและแหล่งค้นคว้า) — รายการเอกสารทางวิชาการและ DOI

---

## 5. ศูนย์รวมแนวทางเวชปฏิบัติ (Clinical Guidelines Center)

หน้า `guidelines.html` รวมไกด์ไลน์ทางคลินิก สามารถ:
- กรองตามองค์กรผู้จัดทำ: **KDIGO**, **ADA**, **ASPEN**, **ESPEN**, **TDA (สมาคมนักกำหนดอาหารฯ)**
- ค้นหาด้วยชื่อไกด์ไลน์หรือปี พ.ศ. / ค.ศ.
- มีปุ่มเชื่อมโยงกลับไปยังคู่มือโรคที่เกี่ยวข้องโดยตรง
- มีลิงก์เปิดอ่านเอกสารวิชาการต้นฉบับ (Official Journal Link)

---

## 6. ฟีเจอร์เด่นบนหน้าเว็บไซต์

| ฟีเจอร์ | รายละเอียดการทำงาน |
| :--- | :--- |
| **Smart Search** | ค้นหาแบบ Real-time ด้วยชื่อโรค (ไทย/อังกฤษ), ชื่อย่อ (CKD, DM, RFS, TPN), รหัส ICD-10 หรือคำสำคัญ |
| **Auto Suggestion** | แนะนำคำค้นทันทีขณะพิมพ์ พร้อมกดคีย์ลัด `/` หรือ `Ctrl + K` เพื่อโฟกัสช่องค้นหา |
| **Table of Contents (TOC)** | สารบัญ 9 หัวข้อด้านข้างพร้อม ScrollSpy ไฮไลท์หัวข้อตามตำแหน่งการเลื่อนหน้าจริง |
| **Reading Progress** | แถบแสดงความก้าวหน้าในการอ่านด้านบนสุด พร้อมการคำนวณเวลาอ่านโดยประมาณ (Read Time) |
| **Bookmark & My Library** | บันทึกบทความและ Guideline ที่สนใจลงใน My Library ผ่าน `localStorage` |
| **Reading History** | บันทึกประวัติการเปิดอ่านบทความตามลำดับเวลาโดยอัตโนมัติ |
| **Recently Viewed** | แสดงการ์ดเข้าถึงด่วนสำหรับเอกสารที่เปิดอ่านล่าสุด |
| **My Favorite Topics** | ผู้ใช้สามารถเลือกติ๊กสาขาที่สนใจ (เช่น โรคไต, เบาหวาน, ผู้ป่วยวิกฤต) เพื่อเน้นแสดงบนหน้าแรก |
| **Responsive & Dark Mode** | รองรับมือถือ แท็บเล็ต คอมพิวเตอร์ พร้อมปุ่มสลับ Dark/Light Mode ที่จดจำสถานะ |
| **Feedback & Contact Modal** | ป๊อปอัปสำหรับเสนอแนะเนื้อหาใหม่ และปุ่มแจ้งปัญหาการใช้งาน |
| **Back to Top** | ปุ่มลอยเลื่อนกลับด้านบนแบบนุ่มนวล |

---

## 7. ขั้นตอนการรันและพัฒนาใน VS Code

1. เปิดโฟลเดอร์ `d:\website\Dietitian101` ใน **VS Code**
2. ติดตั้ง Extension แนะนำ:
   - **Live Server** (โดย Ritwick Dey)
3. คลิกขวาที่ไฟล์ `index.html` แล้วเลือก **"Open with Live Server"**
4. เว็บไซต์จะเปิดขึ้นบนเบราว์เซอร์ที่ `http://127.0.0.1:5500/index.html` ทันที!
