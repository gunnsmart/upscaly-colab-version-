# Upscayl สำหรับ Google Colab

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/gunnsmart/upscaly-colab-version-/blob/arena%2F01a0fb33-upscaly-colab-version/upscayl_colab.ipynb)

โปรเจกต์นี้เพิ่ม Notebook สำหรับใช้งาน **Upscayl บน Google Colab** โดยเรียก backend ทางการ `upscayl-ncnn` และดาวน์โหลดโมเดล `.param` / `.bin` จาก repository ของ Upscayl ตามโมเดลที่เลือก ไม่ได้ bundle ไบนารีหรือไฟล์โมเดลขนาดใหญ่ไว้ใน repository นี้

> Notebook ใช้ Upscayl NCNN/Vulkan backend จริง ไม่ใช่การจำลองผลด้วย PyTorch ดังนั้นต้องใช้ Colab runtime ที่มี NVIDIA GPU และเปิดใช้งาน Vulkan ได้

## เริ่มใช้งาน

> UI เป็น widget ที่แสดงเมื่อ Notebook ทำงานใน Google Colab เท่านั้น — GitHub/ตัวแสดงไฟล์จะแสดง source ของ Notebook แต่ไม่รัน cell ให้

1. เปิด [`upscayl_colab.ipynb`](upscayl_colab.ipynb) ใน Google Colab
2. เลือก **Runtime → Change runtime type → GPU** แล้วเริ่ม runtime ใหม่หากเพิ่งเปลี่ยน
3. รันเซลล์ตามลำดับ แผง **Upscayl Studio** จะแสดงก่อน แล้ว Notebook จะติดตั้ง/ตรวจสอบ Vulkan และดาวน์โหลด Upscayl CLI
4. ใช้แผง UI เพื่ออัปโหลดหลายภาพ เลือกโมเดล, scale, format และ tile แล้วกด **เริ่ม Upscale**
5. ถ้าต้องการเก็บไฟล์บน Google Drive ให้ตั้ง `USE_GOOGLE_DRIVE = True` ก่อนรันเซลล์ workspace; ใน UI สามารถติ๊กให้รวมภาพจากโฟลเดอร์ `input` ได้
6. ดูตัวอย่างก่อน–หลังและกด **ดาวน์โหลด ZIP**; ผลเต็มจะอยู่ในโฟลเดอร์ `output`

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

- UI จะแสดงได้แม้ backend setup ไม่ผ่าน แต่ปุ่มประมวลผลจะรายงานสาเหตุ หาก Colab runtime ไม่มี NVIDIA Vulkan ICD จะยัง upscale ไม่ได้ — Colab บาง runtime อาจไม่รองรับ Vulkan แม้จะมี CUDA
- หากประมวลผลภาพใหญ่แล้วหน่วยความจำ GPU ไม่พอ ให้เลือก Tile size `64` หรือ `32` ใน UI; ค่า `Auto` ให้ backend เลือกขนาด tile อัตโนมัติ
- แนะนำ PNG เมื่อต้องการรักษาความโปร่งใส
- ไฟล์ภาพจะถูกประมวลผลภายใน Colab runtime; Notebook ดาวน์โหลดไบนารีและโมเดลจาก GitHub ทางการของ Upscayl

## Upstream และลิขสิทธิ์

- Upscayl application: <https://github.com/upscayl/upscayl>
- Upscayl NCNN backend: <https://github.com/upscayl/upscayl-ncnn>
- Notebook pin CLI release `20251207-174704` (ตรวจ SHA-256 ก่อนแตกไฟล์) และ pin โมเดลไว้ที่ commit `a00d55fee90e0f9435d5eaa86e76700df8199af8` เพื่อให้ผลการติดตั้งทำซ้ำได้
- Backend ระบุสัญญาอนุญาต AGPL-3.0; ไบนารีและโมเดลที่ Notebook ดาวน์โหลดคงประกาศ/เงื่อนไขของ upstream ไว้
