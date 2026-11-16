# สิ่งที่ได้เรียนรู้และลงมือทำวันนี้

## 1. เริ่มต้นใช้งาน Google Cloud
- เข้าสู่ Google Cloud Console
- ทดลองสร้าง Project ใหม่ชื่อ my-cloud-lab
- พบปัญหา Permission resourcemanager.projects.create
- เปลี่ยนมาใช้ Project เดิมชื่อ My First Project ซึ่งอยู่ภายใต้องค์กร yru.ac.th
Project ID: data-rush-482707-i9

## 2. ทดลองใช้งาน Google Cloud Shell
- เปิด Cloud Shell ผ่าน Google Cloud Console
- กด Authorize เพื่ออนุญาตให้ Cloud Shell ใช้ข้อมูลรับรองของบัญชีเรียก Cloud API
- ทดลองคำสั่ง Linux
- ตรวจสอบ Project ID และ Docker
ได้เรียนรู้ว่าการใช้ Linux Terminal บน Cloud สามารถทำผ่าน Browser ได้โดยไม่จำเป็นต้องติดตั้ง Linux ในเครื่อง Windows

## 3. ทดลองรัน Docker Container บน Cloud

ทดลองใช้คำสั่ง:

docker run --rm hello-world

ผลลัพธ์แสดง Hello from Docker! ยืนยันว่า Docker สามารถดาวน์โหลด Image และสร้าง Container ได้สำเร็จ

หลังจากนั้นทดลองใช้ nginx:alpine และเปิด Web Server ผ่าน Port 8080

## 4. ตรวจสอบ Docker เดิมบน Windows

พบ Docker Containers เดิมทั้งหมด 3 ตัว:
Container	Image	Port เดิม
my-custom-nginx	nginx:alpine	8081
my-nginx	nginx:alpine	8080
keen_mestorf	hello-world	—

ตรวจสอบ Bind Mount และพบว่า my-custom-nginx ใช้ไฟล์เว็บไซต์จาก D:\docker-web เชื่อมเข้ากับ /usr/share/nginx/html ในแบบ Read-only

## 5. ย้ายเว็บไซต์จาก Windows ไปยัง Google Cloud
- พบไฟล์ index.html ขนาด 1,182 bytes
- อัปโหลดไฟล์จาก Windows เข้า Cloud Shell
- พบปัญหาในครั้งแรกเพราะไฟล์ยังไม่อยู่ในตำแหน่งที่ต้องการ
- ตรวจสอบและแก้ไขตำแหน่งไฟล์
- นำไฟล์เข้าโฟลเดอร์ ~/docker-web
- ใช้ Docker รัน Nginx เพื่อแสดงเว็บไซต์เดิมผ่าน Port 8081

## 6. เปิดเว็บไซต์ผ่าน Google Cloud Web Preview

ทดลองเปิดเว็บไซต์ด้วย Web Preview และสามารถแสดงหน้าเว็บเดิมจาก Windows ได้สำเร็จ โดยไม่ต้องสร้างเว็บไซต์ใหม่

# คำสั่งที่ได้ฝึกใช้งาน

## คำสั่งเเละหน้าที่

whoami	       ตรวจสอบชื่อผู้ใช้ Linux

pwd	แสดงตำแหน่งโฟลเดอร์

ls -la	ดูรายการไฟล์และสิทธิ์

gcloud config get-value project	ตรวจสอบ Google Cloud Project

docker ps -a	ดู Containers ทั้งหมด

docker inspect	ตรวจสอบการตั้งค่า Container

docker run	สร้างและรัน Container

curl	ทดสอบ HTTP Web Server

mkdir -p	สร้างโฟลเดอร์

mv	ย้ายไฟล์
