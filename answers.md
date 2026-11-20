# Lab L1 · answers.md

ชื่อ-สกุล: นูรอารีฟี สาอิ
รหัสนักศึกษา: 67117648
ลิงก์ repo: https://github.com/nur-arifee01/lab01_profile

## Q1 · เครื่องมือ
ตอนรัน `flutter doctor` ไม่มีปัญหาอะไรครับ ขึ้นติ๊กถูกครบหมด (`No issues found!`) โดยเช็กหลัก ๆ 2 บรรทัดคือ `Flutter (Channel stable, 3.50.0)` ที่บอกว่ามี Flutter SDK พร้อมใช้แล้ว กับ `Android toolchain` ที่บอกว่าติดตั้ง Android SDK และกดรับ license เรียบร้อยแล้ว ส่วนตอนรัน `flutter emulators` ยังไม่มีตัวจำลองอยู่ เลยไปเปิดจัดการ Emulator ใน Android Studio แทนครับ

## Q2 · Reload
ตอนที่กด Likes ไป 3 แล้ว:
- กด `r` (Hot Reload) ค่า Likes ยังเป็น 3 เหมือนเดิมครับ แต่หน้าตา UI ที่แก้จะเปลี่ยนตาม เพราะ Hot Reload แค่อัปเดตโค้ดใหม่แล้ววาดหน้าจอซ้ำโดยยังเก็บค่า State เดิมไว้
- กด `R` (Hot Restart) ค่า Likes จะรีเซ็ตกลับเป็น 0 ครับ เพราะมันเริ่มรันแอปใหม่ตั้งแต่ `main()` ทำให้ค่า State เดิมหายไปหมดแล้วเริ่มนับ `_likes = 0` ใหม่

## Q3 · โค้ดและ Git
ที่ `_likes++` ต้องอยู่ใน `setState` เพราะถ้าบวกเลขเฉย ๆ ค่าในตัวแปรเปลี่ยนก็จริง แต่หน้าจอจะไม่เปลี่ยนตาม การใส่ `setState` คือการบอก Flutter ให้วาดหน้าจอ (`build()`) ใหม่ด้วยค่าล่าสุดครับ

ตัวอย่าง commit ที่เลือกคือ `"Add like counter with setState"` (`598bb0e`) เป็นรอบที่เปลี่ยน `HomePage` จาก `StatelessWidget` เป็น `StatefulWidget` เพิ่มตัวแปร `_likes` กับฟังก์ชัน `_like()` ที่เรียก `setState` แล้วก็ใส่ข้อความ `Likes: $_likes` กับปุ่ม `Like` เพิ่มเข้ามาครับ

## ตารางทดสอบ

| ประเภท | input หรือการกระทำ | ผลที่คาดหวัง | ผลจริง |
|---|---|---|---|
| Normal | เปิดแอป | title มีรหัส ไอคอน ชื่อ “Likes: 0” | ขึ้นครบทั้ง AppBar “Lab L1 · 67117648”, ไอคอนคน, ชื่อ-รหัส, “Likes: 0” และปุ่ม Like |
| Normal | กด Like หนึ่งครั้ง | “Likes: 1” | ขึ้น “Likes: 1” |
| Boundary | กด Like เร็ว ๆ 20 ครั้ง | “Likes: 20” ไม่มี error | นับได้ “Likes: 20” ปกติ ไม่มี error |
| Boundary | หมุนจอเป็นแนวนอน | ยังอยู่กลางจอ ไม่ overflow | ยังอยู่กลางจอ ไม่ล้นจอ |
| Reload | กด 3 ครั้ง แล้ว r แล้ว R | หลัง r ได้ 3 · หลัง R ได้ 0 | หลัง r ยังได้ 3 · หลัง R กลับเป็น 0 |
| Failure | ปิด emulator แล้ว `flutter run` | “No supported devices connected.” | ขึ้นเตือนว่าไม่พบอุปกรณ์ Android ที่เชื่อมต่อ |

## การใช้ AI
ใช้ AI (Gemini / Antigravity) ช่วยเช็กขั้นตอนตามใบงาน ช่วยดูโค้ด `lib/main.dart` กับคำสั่ง Git และช่วยเกลาคำตอบใน `answers.md` ครับ ส่วนการรันทดสอบแอป แคปภาพ และทำความเข้าใจโค้ดทำเองทั้งหมดครับ
