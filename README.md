# ทฤษฎีใหม่: เกมบริหารประเทศด้วยเศรษฐกิจพอเพียง

เกม 2D จำลองสถานการณ์บริหารประเทศ สำหรับส่งงานวิชาสังคมศึกษา หัวข้อ
**"เศรษฐกิจพอเพียงกับการพัฒนาเศรษฐกิจของไทย"**

ผู้เล่นจะสวมบทบาท 4 ตัวละคร ได้แก่ **ผู้บริหารประเทศ, พ่อค้า, ชาวบ้าน และนักลงทุนต่างชาติ**
ตอบคำถามทั้งหมด **20 ข้อ** (บทบาทละ 5 ข้อ) แต่ละข้อมี 2 ตัวเลือก ซึ่งจะส่งผลต่อสถานะของประเทศ
4 ด้าน คือ **เศรษฐกิจ / สังคม / สิ่งแวดล้อม / ความพอเพียง** แสดงผลผ่านมาตรวัดวงกลม
และเมื่อจบเกมจะสรุปผลการบริหารประเทศ พร้อมปุ่มพิมพ์/บันทึกสรุปคำตอบทั้ง 20 ข้อ
เพื่อใช้ประกอบการส่งอาจารย์

ทั้งหมดเป็นไฟล์เดียว `index.html` (HTML + CSS + JavaScript ล้วน) ไม่ต้องติดตั้งอะไรเพิ่ม
เปิดไฟล์ในเบราว์เซอร์ได้ทันที และ deploy ขึ้น GitHub Pages ได้ง่าย

---

## 1) เปิดทดสอบเกมก่อน deploy

เปิดไฟล์ `index.html` ด้วยเบราว์เซอร์ได้เลย (ดับเบิลคลิก หรือใน VS Code คลิกขวา →
**Open with Live Server** ถ้าติดตั้ง extension ไว้)

---

## 2) วิธี Deploy ขึ้น GitHub Pages (ทำผ่าน VS Code)

### ขั้นตอนที่ 1: สร้าง Repository บน GitHub
1. เข้า https://github.com → กด **New repository**
2. ตั้งชื่อ เช่น `sufficiency-economy-game`
3. เลือก Public แล้วกด **Create repository** (ไม่ต้องติ๊ก README เพราะเรามีไฟล์แล้ว)

### ขั้นตอนที่ 2: เปิดโฟลเดอร์นี้ใน VS Code
1. เปิด VS Code → **File > Open Folder** → เลือกโฟลเดอร์ที่มี `index.html` และ `README.md`
2. เปิด Terminal ใน VS Code (`Ctrl + \``  หรือเมนู Terminal > New Terminal)

### ขั้นตอนที่ 3: Push ขึ้น GitHub ผ่าน Terminal
รันคำสั่งทีละบรรทัด (แก้ `YOUR-USERNAME` และชื่อ repo ให้ตรงกับของตัวเอง):

```bash
git init
git add .
git commit -m "เกมบริหารประเทศ เศรษฐกิจพอเพียง"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/sufficiency-economy-game.git

### ขั้นตอนที่ 4: เปิดใช้งาน GitHub Pages
1. เข้าไปที่ repository บนเว็บ GitHub
2. ไปที่ **Settings > Pages** (เมนูด้านซ้าย)
3. ในหัวข้อ **Build and deployment > Source** เลือก **Deploy from a branch**
4. **Branch** เลือก `main` และโฟลเดอร์เลือก `/ (root)` แล้วกด **Save**
5. รอประมาณ 1-2 นาที แล้วรีเฟรชหน้า Settings > Pages จะมีลิงก์ขึ้นมา เช่น:
   `https://YOUR-USERNAME.github.io/sufficiency-economy-game/`

เปิดลิงก์นี้จะเจอเกมของคุณที่เล่นได้จริงบนอินเทอร์เน็ต ส่งลิงก์นี้ให้อาจารย์ได้เลย

---

## 3) ถ้าจะแก้ไข/เพิ่มคำถามภายหลัง

เปิด `index.html` แล้วหาส่วน `const QUESTIONS = [ ... ]` ในแท็ก `<script>`
แต่ละคำถามมีโครงสร้าง:

```js
{ role:'government', label:'ระดับนโยบาย', text:'คำถาม...',
  choices:[
    {text:'ตัวเลือกที่ 1', delta:{economy:3, society:0, environment:-1, sufficiency:-3}},
    {text:'ตัวเลือกที่ 2', delta:{economy:1, society:2, environment:1, sufficiency:3}}
  ],
  feedback:'คำอธิบายผลกระทบที่จะแสดงหลังเลือกคำตอบ' }
```

- `role` ต้องเป็นหนึ่งใน `government / merchant / villager / investor`
- `delta` คือค่าที่จะบวก/ลบออกจากสถานะประเทศแต่ละด้าน (ช่วงที่แนะนำ -3 ถึง 3)

แก้ไขแล้วบันทึกไฟล์ จากนั้น commit และ push ขึ้น GitHub ใหม่:

```bash
git add .
git commit -m "แก้ไขคำถาม"
git push
```

GitHub Pages จะอัปเดตเว็บให้อัตโนมัติภายในไม่กี่นาที
