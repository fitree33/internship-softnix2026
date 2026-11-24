# ลองใช้คำสั่ง Docker Linux
## 1. เปิด Linux ผ่าน Docker
เปิด Docker Desktop แล้วเข้า PowerShell พิมพ์:
docker run -it --name linux-lab ubuntu bash

## 2. คำสั่งพื้นฐาน (Basic Commands)
คำสั่ง	หน้าที่
- pwd	ดูว่าปัจจุบันอยู่โฟลเดอร์ไหน
- ls	แสดงไฟล์และโฟลเดอร์
- ls -l	แสดงรายละเอียดไฟล์
- ls -la	แสดงไฟล์ทั้งหมดรวมไฟล์ซ่อน
- cd folder	เข้าโฟลเดอร์
- cd ..	ย้อนกลับหนึ่งระดับ
- cd ~	กลับไป Home Directory
- clear	ล้างหน้าจอ Terminal
- history	ดูประวัติคำสั่ง
- man ls	เปิดคู่มือคำสั่ง ls
- whoami	ดูชื่อผู้ใช้ปัจจุบัน

## 3. จัดการไฟล์และโฟลเดอร์ (File Management)
คำสั่ง	หน้าที่
- mkdir test	สร้างโฟลเดอร์ test
- mkdir -p a/b	สร้างโฟลเดอร์ซ้อนกัน
- touch file.txt	สร้างไฟล์เปล่า
- cat file.txt	อ่านเนื้อหาไฟล์
- less file.txt	อ่านไฟล์ทีละหน้า
- cp a.txt b.txt	คัดลอกไฟล์
- mv a.txt b.txt	ย้ายหรือเปลี่ยนชื่อไฟล์
- rm file.txt	ลบไฟล์
- rmdir test	ลบโฟลเดอร์ที่ว่าง
- find /home -name "*.txt"	ค้นหาไฟล์ .txt
- grep "error" file.txt	ค้นหาคำว่า error ภายในไฟล์
- head -n 10 file.txt	แสดง 10 บรรทัดแรก
- tail -n 10 file.txt	แสดง 10 บรรทัดสุดท้าย

4. ตรวจสอบข้อมูลระบบ (System Information)
คำสั่ง	หน้าที่
- uname -a	แสดงรายละเอียด Kernel
- uname -r	แสดงเวอร์ชัน Kernel
- cat /etc/os-release	ดูชื่อและเวอร์ชัน Linux
- hostname	ดูชื่อเครื่อง
- uptime	ดูระยะเวลาที่เครื่องเปิดอยู่
- date	ดูวันที่และเวลา
- free -h	ดูการใช้ RAM
- df -h	ดูพื้นที่ Disk
- du -sh /var/log	ดูขนาดโฟลเดอร์ Log
- lsblk	แสดงอุปกรณ์จัดเก็บข้อมูล
- lscpu	แสดงข้อมูล CPU
