# Upscayl สำหรับ Google Colab

โปรเจกต์นี้เพิ่ม Notebook สำหรับใช้งาน **Upscayl บน Google Colab** โดยเรียก backend ทางการ `upscayl-ncnn` และดาวน์โหลดโมเดล `.param` / `.bin` จาก repository ของ Upscayl ตามโมเดลที่เลือก ไม่ได้ bundle ไบนารีหรือไฟล์โมเดลขนาดใหญ่ไว้ใน repository นี้

> Notebook ใช้ Upscayl NCNN/Vulkan backend จริง ไม่ใช่การจำลองผลด้วย PyTorch ดังนั้นต้องใช้ Colab runtime ที่มี NVIDIA GPU และเปิดใช้งาน Vulkan ได้

## เริ่มใช้งาน

1. เปิด [`upscayl_colab.ipynb`](upscayl_colab.ipynb) ใน Google Colab
2. เลือก **Runtime → Change runtime type → GPU** แล้วเริ่ม runtime ใหม่หากเพิ่งเปลี่ยน
3. รันเซลล์ตามลำดับ Notebook จะติดตั้ง/ตรวจสอบ Vulkan, ดาวน์โหลด Upscayl CLI และโมเดลที่เลือก
4. ตั้งค่าโมเดล, ขนาดภาพ และ output format ในเซลล์ **ตั้งค่าการ Upscale**
5. อัปโหลดรูปในเซลล์ **อัปโหลดรูป** หรือเปิด `USE_GOOGLE_DRIVE = True` เพื่ออ่าน/บันทึกไฟล์บน Google Drive (ถ้าวางรูปใน `input` ไว้แล้ว ให้ตั้ง `UPLOAD_FILES = False`)
6. รันเซลล์ประมวลผล แล้วดาวน์โหลดผลลัพธ์เป็น ZIP หรือหยิบไฟล์จากโฟลเดอร์ `output`

### โมเดลที่เลือกได้

- `upscayl-standard-4x` — ใช้งานทั่วไป (ค่าเริ่มต้น)
- `upscayl-lite-4x` — โมเดลขนาดเล็ก ประมวลผลเร็ว
- `high-fidelity-4x` — เน้นคงรายละเอียด
- `remacri-4x` — โมเดล Remacri
- `ultramix-balanced-4x` — สมดุลระหว่างรายละเอียดและความคม
- `ultrasharp-4x` — เน้นความคม
- `digital-art-4x` — เหมาะกับงานวาดและ digital art

โมเดลถูกดาวน์โหลดเฉพาะตัวที่เลือก และผลลัพธ์จะอยู่ในโฟลเดอร์ `output` ของ workspace

## ข้อควรทราบ / แก้ปัญหา

- Notebook จะตรวจสอบว่า Vulkan มองเห็น NVIDIA GPU ก่อนเริ่ม หาก Colab runtime ไม่มี NVIDIA Vulkan ICD หรือไม่แสดง GPU ที่ใช้ได้ การประมวลผลจะหยุดพร้อมข้อความวินิจฉัย — Colab บาง runtime อาจไม่รองรับ Vulkan แม้จะมี CUDA
- หากประมวลผลภาพใหญ่แล้วหน่วยความจำ GPU ไม่พอ ให้ลด `TILE_SIZE` เป็น `64` หรือ `32`; ค่า `0` คือให้ backend เลือกขนาด tile อัตโนมัติ
- แนะนำ PNG เมื่อต้องการรักษาความโปร่งใส
- ไฟล์ภาพจะถูกประมวลผลภายใน Colab runtime; Notebook ดาวน์โหลดไบนารีและโมเดลจาก GitHub ทางการของ Upscayl

## Upstream และลิขสิทธิ์

- Upscayl application: <https://github.com/upscayl/upscayl>
- Upscayl NCNN backend: <https://github.com/upscayl/upscayl-ncnn>
- Notebook pin CLI release `20251207-174704` (ตรวจ SHA-256 ก่อนแตกไฟล์) และ pin โมเดลไว้ที่ commit `a00d55fee90e0f9435d5eaa86e76700df8199af8` เพื่อให้ผลการติดตั้งทำซ้ำได้
- Backend ระบุสัญญาอนุญาต AGPL-3.0; ไบนารีและโมเดลที่ Notebook ดาวน์โหลดคงประกาศ/เงื่อนไขของ upstream ไว้
