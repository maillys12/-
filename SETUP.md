# MONTYSTORE — วิธีตั้งค่าระบบ

## Google Sheets และ Apps Script
1. สร้าง Google Sheet ใหม่ แล้วคัดลอก ID จาก URL
2. เปิด Extensions → Apps Script และวางไฟล์ `apps-script/Code.gs`
3. ใส่ Sheet ID, API ตรวจสลิป, Token และเลขบัญชีร้านใน `CONFIG`
4. รัน `setup()` หนึ่งครั้ง เพื่อสร้าง Users, Sessions, Products, Orders และ Deposits
5. Deploy → New deployment → Web app ตั้ง Execute as: Me และ Who has access: Anyone
6. นำ Web app URL ไปแทน `API_URL` ใน `app/page.tsx`

## ความปลอดภัย
- Password เก็บแบบ SHA-256 พร้อม salt และไม่เก็บรหัสผ่านจริง
- Session token ในชีตถูก hash และมีวันหมดอายุ
- ตรวจเลขบัญชีผู้รับและเลขอ้างอิงสลิปก่อนเพิ่มเครดิต
- Script Lock ป้องกันสลิปเดียวถูกเติมพร้อมกัน
- Token ของ API ตรวจสลิปต้องอยู่ใน Apps Script เท่านั้น ห้ามใส่หน้าเว็บหรือ GitHub

ผู้ให้บริการตรวจสลิปแต่ละรายใช้ชื่อฟิลด์ต่างกัน จึงต้องปรับ `verifySlip_()` ให้ตรงเอกสารของผู้ให้บริการที่เลือกก่อนเปิดใช้งานจริง
