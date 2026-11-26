## 1. ติดตั้ง Kali Linux และ Hydra ผ่าน Docker
เริ่มจากตรวจสอบ Docker Desktop และตำแหน่งจัดเก็บข้อมูล พบว่า Docker ใช้ WSL2 Backend และเก็บข้อมูลไว้บนไดรฟ์ D:
D:\DockerData\DockerDesktopWSL


จากนั้นสร้าง Kali Linux Container:
docker run -it --name hydra-kali kalilinux/kali-rolling bash


ติดตั้ง Hydra:
apt update
apt install hydra -y


ตรวจสอบการติดตั้งด้วย hydra -h
สำเร็จ — Hydra Version 9.7
## 2. สร้าง Docker Lab สำหรับทดสอบ SSH
สร้าง Network ชื่อ hydra-lab-net และ SSH Server Container เพื่อใช้เป็นเป้าหมายในการทดสอบ
Container	หน้าที่
hydra-kali	รัน Kali Linux และ Hydra
hydra-ssh-lab	ให้บริการ SSH สำหรับทดสอบ

SSH Server ใช้บัญชีทดลอง hydralab โดยเปิด Password Authentication

## 3. ทดลอง Password Guessing ด้วย Hydra
สร้างไฟล์รายการรหัสผ่าน 3 รายการ แล้วใช้ Hydra ทดสอบกับ SSH Server ภายใน Docker

คำสั่งที่ใช้:
hydra -l hydralab -P /tmp/passwords.txt -s 2222 -t 1 -f -V ssh://hydra-ssh-lab


ผลลัพธ์:
ครั้งที่	Password	ผลลัพธ์
1	123456	ไม่สำเร็จ
2	password	ไม่สำเร็จ
3	LabPass123	สำเร็จ

Hydra พบข้อมูลเข้าสู่ระบบที่ถูกต้องและหยุดทำงานตามตัวเลือก -f

ทดลองทั้งหมด 2 รอบ และประสบความสำเร็จทั้งสองรอบ
สำเร็จ — ค้นพบ Password ที่กำหนดไว้ในแล็บ
## 4. ทดลอง Nmap กับเครื่อง Windows อีกเครื่อง
ทดลองใช้ Nmap ตรวจสอบพอร์ตของเครื่องเพื่อนที่ได้รับอนุญาต ภายในเครือข่ายเดียวกัน

IP เป้าหมาย:
192.168.120.76


คำสั่ง:
nmap -sT -Pn -p 22,80,443,3389 192.168.120.76


ผลการตรวจสอบ:
Port	Service	สถานะ
22	SSH	filtered
80	HTTP	filtered
443	HTTPS	filtered
3389	RDP	filtered

พบว่าทั้ง 4 พอร์ตมีสถานะ filtered ซึ่งหมายถึง Nmap ไม่สามารถระบุได้แน่ชัดว่าพอร์ตเปิดหรือปิด เนื่องจากไม่ได้รับคำตอบเพียงพอ อาจมี Firewall กรองการเชื่อมต่ออยู่

หลังจากนั้นตัดสินใจกลับมาฝึกกับ Docker Lab ของตนเอง เพื่อควบคุมสภาพแวดล้อมได้สะดวกกว่า
สำเร็จ — ฝึกใช้ Nmap และวิเคราะห์สถานะพอร์ต
## 5. ศึกษา SSH Log Analysis
ตรวจสอบ Logs จาก SSH Server Container โดยใช้คำสั่ง:
docker exec hydra-ssh-lab tail -n 50 /config/logs/openssh/current


พบเหตุการณ์จาก Hydra ทั้งสองรอบ:
ผลการวิเคราะห์ SSH Logs
4
Login Failed

2
Login Success

2
รอบทดสอบ



ได้เรียนรู้ความหมายของ Log เช่น:
- Failed password — ยืนยันตัวตนไม่สำเร็จ
- Accepted password — ยืนยันตัวตนสำเร็จ
- preauth — เหตุการณ์ก่อนยืนยันตัวตนเสร็จสิ้น
- Connection reset by peer — ฝั่งที่เชื่อมต่อส่งคำสั่ง Reset การเชื่อมต่อ
รวมถึงเรียนรู้ว่า Log สามารถใช้ตรวจสอบการ Login ผิดซ้ำ ๆ เพื่อช่วยตรวจจับพฤติกรรมที่น่าสงสัยได้
สำเร็จ — ตรวจพบเหตุการณ์จาก Hydra ใน SSH Logs
## 6. ศึกษา Docker Networking และ Timezone
ตรวจสอบ IP ของ Kali Container:
docker exec hydra-kali hostname -i


ผลลัพธ์:
172.17.0.2 172.19.0.2


พบว่า 172.19.0.2 ตรงกับ Source IP ที่ปรากฏใน SSH Logs

จึงสามารถเชื่อมโยงเหตุการณ์การทดลองรหัสผ่านกับ Kali Container ที่เป็นต้นทางได้

นอกจากนี้ยังเรียนรู้เรื่อง Timezone:
เวลา UTC ใน Log	เวลาไทย
08:37:34	15:37:34
09:03:20	16:03:20

ทำให้เข้าใจความสำคัญของการแปลงเวลาเมื่อวิเคราะห์ Logs จากระบบต่าง ๆ
<img width="1407" height="682" alt="Screenshot 2026-11-26 162228" src="https://github.com/user-attachments/assets/0c1492d5-a0d7-4bc0-9b71-6becb9c1095a" />
<img width="1251" height="450" alt="Screenshot 2026-11-26 155515" src="https://github.com/user-attachments/assets/7e7e3414-33c2-4de3-8450-fe46f4d0d883" />
<img width="1395" height="690" alt="Screenshot 2026-11-26 153822" src="https://github.com/user-attachments/assets/f6b4a01c-cdaf-40b4-bc0a-591da12760f2" />
<img width="1152" height="701" alt="Screenshot 2026-11-26 153802" src="https://github.com/user-attachments/assets/2e0fc6e5-cc7b-44e1-aa84-8f3937738ee6" />
<img width="1912" height="762" alt="Screenshot 2026-11-26 153744" src="https://github.com/user-attachments/assets/6db025dc-7477-47e5-833f-3606efedbc2e" />
