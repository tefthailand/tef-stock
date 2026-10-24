# TEF Stock — Production Release Checklist

ใช้หลังจาก PR ที่เกี่ยวข้องผ่านการ review แล้วเท่านั้น

## ก่อน Merge

- [ ] PR เปลี่ยนเฉพาะไฟล์/ขอบเขตที่ระบุในคำอธิบาย
- [ ] ไม่มีข้อมูลสต็อกจริงหรือ credential อยู่ใน diff
- [ ] ทดสอบ workflow บนเว็บทดสอบตาม `docs/staging-workflow-test-matrix.md`
- [ ] ตรวจ Admin / TEF Staff / Gmail แยกกัน
- [ ] ตรวจไทย–English
- [ ] ตรวจจอ 320 px, 375 px และ desktop
- [ ] ตรวจ Print Preview และโลโก้หัวกระดาษ
- [ ] CI/checks ผ่าน และมี approving review

## การขึ้น Production

1. Merge PR ทีละชุดตามลำดับความเสี่ยง:
   1. correctness/data display
   2. Home/role/language/responsive
   3. movement photo preview
   4. test documentation
   5. print/release documentation
2. รอ GitHub Pages deploy จาก `main` สำเร็จ
3. เปิด URL ใหม่หรือ hard refresh เพื่อล้าง cache
4. ทดสอบแบบ read-only บน Production:
   - เปิด Home
   - ตรวจเมนูตามสิทธิ์
   - ตรวจรูปตัวอย่าง
   - ตรวจภาษา
   - เปิด Print Preview โดยไม่ส่ง/บันทึกเอกสาร
5. ห้ามกด Submit, Approve, Issue, Count Save หรือ Undo บน Production ระหว่าง smoke test

## เงื่อนไขหยุดและย้อนกลับ

หยุด rollout และแจ้งผู้ดูแลทันทีเมื่อพบ:

- รูปไม่ตรงรหัสหรือชื่อ
- ผู้ใช้เห็นเมนูของบทบาทอื่น
- API error หรือหน้าใดหน้าแสดงผลไม่ครบ
- ข้อมูลจำนวน/ยอดคงเหลือเปลี่ยนโดยไม่ได้ตั้งใจ
- Print Preview ขาดโลโก้ หัวกระดาษ หรือตาราง

หากจำเป็นต้องย้อนกลับ ให้ revert เฉพาะ merge commit ของ PR ที่เป็นต้นเหตุ โดยตรวจ diff และขออนุมัติก่อนทุกครั้ง

## หลัง Deploy

- [ ] บันทึก commit และ PR ที่ขึ้นจริง
- [ ] บันทึกเวลาที่ deploy เสร็จ
- [ ] บันทึกผล smoke test
- [ ] แจ้งผู้ใช้งานว่าระบบพร้อมหรือมีข้อจำกัดใด
- [ ] เฝ้าดู error/latency หลังเปิดใช้งานช่วงแรก
