# Lab L1 · answers.md

ชื่อ-สกุล: นูรอารีฟี สาอิ
รหัสนักศึกษา: 67117648
ลิงก์ repo: https://github.com/nur-arifee01/lab01_profile

## Q1 · เครื่องมือ
จากการรัน `flutter doctor` ไม่พบปัญหา (`No issues found!`) โดยได้ตรวจสอบบรรทัดสำคัญ 2 บรรทัด ได้แก่:
- `[√] Flutter (Channel stable, 3.50.0, on Microsoft Windows)` — หมายถึงติดตั้ง Flutter SDK และ Dart พร้อมใช้งานบนเครื่องเรียบร้อยแล้ว
- `[√] Android toolchain - develop for Android devices (Android SDK version 36.0.0)` — หมายถึงมี Android SDK และยอมรับ Android licenses ครบถ้วน สามารถ build แอป Android ได้

นอกจากนี้ตอนรัน `flutter emulators` พบว่ายังไม่มี Android AVD สร้างไว้ จึงตรวจสอบและจัดการผ่าน Device Manager ใน Android Studio (อ้างอิงจากเอกสารทางการ https://docs.flutter.dev/get-started)

## Q2 · Reload
เมื่อค่า Likes เป็น 3 อยู่:
- **กด `r` (Hot Reload):** ค่า Likes **ยังคงเป็น 3** เหมือนเดิม (ส่วนข้อความหรือ UI ที่แก้ไขใหม่จะอัปเดตทันที) เพราะ Hot Reload จะส่งโค้ดใหม่เข้า Dart VM และสั่งเรียก `build()` ใหม่โดย **คงค่าตัวแปรในอ็อบเจกต์ `State` (`_HomePageState`) เดิมไว้**
- **กด `R` (Hot Restart):** ค่า Likes **รีเซ็ตกลับเป็น 0** เพราะ Hot Restart จะ **ทำลาย State เดิมทั้งหมดและเริ่มต้นรันแอปใหม่ตั้งแต่ฟังก์ชัน `main()`** ทำให้ `int _likes = 0;` ถูกสร้างค่าเริ่มต้นขึ้นมาใหม่

## Q3 · โค้ดและ Git
- **ทำไม `_likes++` ต้องอยู่ใน `setState`:** หากเขียนแค่ `_likes++` ค่าตัวแปรในหน่วยความจำจะเพิ่มขึ้นจริง แต่ Flutter จะไม่ทราบว่าข้อมูลมีการเปลี่ยนแปลง จึงไม่เรียกเมธอด `build()` เพื่อวาดหน้าจอใหม่ การเรียก `setState(() => _likes++)` เป็นการบอก Flutter framework ว่า State เปลี่ยนแล้ว ให้ rebuild widget เพื่อแสดงจำนวน Likes ล่าสุดบนหน้าจอ
- **ตัวอย่าง Commit ที่เลือก:** `"Add like counter with setState"` (`598bb0e`) — เปลี่ยน `HomePage` จาก `StatelessWidget` เป็น `StatefulWidget` คู่กับ `_HomePageState`, เพิ่มตัวแปร `int _likes = 0;` และเมธอด `_like()` ที่เรียก `setState()`, ลบ `const` หน้า `Center` และเพิ่ม `Text('Likes: $_likes')` กับปุ่ม `FilledButton` (`Like`)

## ตารางทดสอบ

| ประเภท | input หรือการกระทำ | ผลที่คาดหวัง | ผลจริง |
|---|---|---|---|
| Normal | เปิดแอป | title มีรหัส ไอคอน ชื่อ “Likes: 0” | แสดง AppBar “Lab L1 · 67117648”, ไอคอนรูปคน, “นูรอารีฟี สาอิ - 67117648”, “Likes: 0” และปุ่ม Like ถูกต้อง |
| Normal | กด Like หนึ่งครั้ง | “Likes: 1” | เปลี่ยนเป็น “Likes: 1” ทันที |
| Boundary | กด Like เร็ว ๆ 20 ครั้ง | “Likes: 20” ไม่มี error | นับได้ “Likes: 20” ครบและไม่มี error |
| Boundary | หมุนจอเป็นแนวนอน | ยังอยู่กลางจอ ไม่ overflow | เนื้อหายังจัดกึ่งกลางหน้าจอและไม่เกิด overflow |
| Reload | กด 3 ครั้ง แล้ว r แล้ว R | หลัง r ได้ 3 · หลัง R ได้ 0 | หลังกด r ยังแสดง “Likes: 3” · หลังกด R รีเซ็ตเป็น “Likes: 0” |
| Failure | ปิด emulator แล้ว `flutter run` | “No supported devices connected.” | แสดงข้อความไม่พบอุปกรณ์ Android ที่เชื่อมต่อ (No supported devices connected / ให้เลือกอุปกรณ์อื่นแทน) |

## การใช้ AI
ใช้ AI (Antigravity / Gemini) ช่วยตรวจสอบขั้นตอนตามใบงาน Lab L1, ช่วยเขียนและตรวจสอบโค้ด `lib/main.dart` ตามสไลด์ Step 3–6, ช่วยรันคำสั่ง Git commit/push และช่วยร่างโครงคำตอบใน `answers.md` โดยได้รันทดสอบแอปจริง ตรวจสอบโค้ด และทำความเข้าใจการทำงานของ `StatefulWidget`, `setState`, `r` (Hot Reload) และ `R` (Hot Restart) ด้วยตนเองทั้งหมด
