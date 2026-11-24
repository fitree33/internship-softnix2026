# สิ่งที่ได้ดำเนินการทีละขั้นตอน
## 1. เข้าสู่ Google Cloud Console
   - เปิดหน้า Google Cloud Console
   - เข้าสู่ระบบด้วยบัญชี Google
   - พบข้อความแจ้งเตือนให้เปิดการยืนยันตัวตนสองขั้นตอน (MFA/2SV)
   - ศึกษาความสำคัญของ MFA สำหรับการรักษาความปลอดภัยบัญชี Cloud
   เข้าสู่ระบบสำเร็จ
   ยังไม่ได้ยืนยันว่าเปิด MFA สำเร็จแล้ว
## 2. ตรวจสอบ Google Cloud Project
   
   ตรวจสอบโปรเจกต์ที่เคยใช้ทดลอง Docker และ Linux บน Cloud Shell
   รายการ	ข้อมูล
   Project name	My First Project
   Project ID	data-rush-482707-i9
   Organization	yru.ac.th
   
   เลือกใช้โปรเจกต์เดิมแทนการสร้างใหม่ เพื่อทดลอง Deploy Web Server
## 3. ตรวจสอบค่าใช้จ่ายใน Google Cloud Billing
   - เข้าเมนู Billing → Overview
   - ตรวจสอบประเภทบัญชีที่แสดงว่าเป็น Free trial account
   - ตรวจสอบค่าใช้จ่ายระหว่างวันที่ 1–24 พฤศจิกายน 2569
   - พบยอดค่าใช้จ่ายที่แสดงเป็น ฿0.00
   ได้เรียนรู้ว่า Cloud Billing ใช้ตรวจสอบและจัดการค่าใช้จ่ายจากการใช้บริการ Cloud
   ตรวจสอบสำเร็จ
##4. ตรวจสอบบัญชี Billing ที่เชื่อมกับ Project
   - เข้าเมนู Manage billing accounts
   - เลือก Organization yru.ac.th
   - ตรวจสอบหน้า Your billing accounts
   - พบข้อความ No rows to display
   - เปลี่ยนไปที่แท็บ Your projects เพื่อตรวจสอบการเชื่อมต่อ Billing
   ผลการตรวจสอบ:
   Project ID	Billing
   data-rush-482707-i9	My Billing Account
   ardent-kite-482707-g7	Billing disabled
   
   ได้เรียนรู้ว่าการเชื่อมต่อ Billing Account กับ Project ไม่ได้ยืนยันว่าบัญชีนั้นพร้อมใช้งานทุกบริการเสมอไป
## 5. เข้าสู่บริการ Google Cloud Run
   - กลับมาที่ Google Cloud Console
   - เปิดบริการ Cloud Run
   - ศึกษาหน้า Overview
   - พบตัวเลือก Deploy container, Connect repository และการสร้าง Function
   - เลือกศึกษาแนวทาง Deploy จาก Container Image
   Cloud Run เป็นบริการสำหรับรันแอปพลิเคชันหรือ Container โดย Google จัดการโครงสร้างพื้นฐานให้
   เข้าสู่ Cloud Run สำเร็จ
## 6. เข้าสู่หน้าสร้าง Cloud Run Service
   - กด Deploy container
   - เข้าสู่หน้า Create service
   - ศึกษาการ Deploy จาก Container Image
   - พบตัวเลือก Test with a sample container
   - เตรียมแนวทางตั้งชื่อ Service ว่า nuclei-security-lab
   ศึกษาการตั้งค่าที่จำเป็น เช่น Region, Authentication, Public Access และการจำกัดจำนวน Instance
   
   ยังไม่ได้สร้าง Service จริง
## 7. พบปัญหา Cloud Run Admin API
   
   ระบบแสดงข้อความ:
   Cloud Run Admin API has not been used
   in project before or it is disabled.
   
   
   ทำให้ไม่สามารถโหลดรายการ Region สำหรับ Deploy ได้
   
   ศึกษาว่า Google Cloud ใช้ API เพื่อให้บริการต่าง ๆ สามารถทำงานร่วมกับโปรเจกต์ และการเปิด API ต้องมีสิทธิ์ที่เหมาะสม
   ยังไม่ได้ยืนยันว่าเปิด API สำเร็จ
## 8. พบปัญหาการเปิดใช้งาน Billing
   
   เมื่อพยายามเข้าสู่กระบวนการสร้าง Service ระบบแสดงข้อความ:
   Enable billing to keep using Cloud Run
   
   
   จึงกลับไปตรวจสอบ Billing อีกครั้ง และพบว่าการผูกบัญชี Billing กับ Project ยังไม่เพียงพอสำหรับการ Deploy ในสถานะปัจจุบัน

  # ตัดสินใจหยุดการ Deploy ชั่วคราว

เนื่องจากพบเงื่อนไขการชำระเงินและยังต้องตรวจสอบสิทธิ์การใช้โปรเจกต์ของมหาวิทยาลัย จึงหยุดการดำเนินการไว้ก่อน
- ยังไม่ได้ชำระเงิน ฿1,500
- ยังไม่ได้เปิด Web Server สาธารณะ
- ยังไม่ได้สร้าง Cloud Run Service
- ยังไม่ได้ใช้ Nuclei สแกนเป้าหมายบน Cloud
