# Upscayl สำหรับ Google Colab

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/gunnsmart/upscaly-colab-version-/blob/arena%2F01a0fb33-upscaly-colab-version/upscayl_colab.ipynb)

Notebook นี้เปิด **Web UI จริงของ Upscayl Studio ด้วย Gradio** บน Google Colab โดยเรียก backend ทางการ `upscayl-ncnn` และดาวน์โหลดโมเดล `.param` / `.bin` จาก repository ของ Upscayl ตามที่เลือก ไม่ได้ bundle ไบนารีหรือไฟล์โมเดลขนาดใหญ่ไว้ใน repository นี้

> GitHub/ตัวแสดงไฟล์จะแสดง source ของ Notebook แต่ไม่รันโค้ดให้ ต้องเปิดใน Colab และเลือก **Runtime → Run all** จึงจะได้หน้า Web UI และลิงก์เข้าใช้งาน

## เริ่มใช้งาน

1. คลิก **Open in Colab** แล้วเลือก **Runtime → Change runtime type → GPU**
2. หากต้องการเก็บไฟล์บน Google Drive ให้ตั้ง `USE_GOOGLE_DRIVE = True` ในเซลล์ workspace
3. เลือก **Runtime → Run all** และรอให้ backend ตรวจ Vulkan และ Gradio เปิดหน้า Studio
4. เปิดลิงก์ชั่วคราวที่แสดงใน output; ใช้ username/password ที่ Notebook สร้างให้
5. ในหน้า Studio อัปโหลดหลายภาพ เลือกโมเดล, scale, format, tile และ TTA แล้วกด **เริ่ม Upscale**
6. ดูภาพเปรียบเทียบและดาวน์โหลดผลลัพธ์เป็น ZIP; ไฟล์เต็มอยู่ใน `output`

### โมเดลที่เลือกได้

- `upscayl-standard-4x` — ใช้งานทั่วไป (ค่าเริ่มต้น)
- `upscayl-lite-4x` — โมเดลขนาดเล็ก ประมวลผลเร็ว
- `high-fidelity-4x` — เน้นคงรายละเอียด
- `remacri-4x` — โมเดล Remacri
- `ultramix-balanced-4x` — สมดุลระหว่างรายละเอียดและความคม
- `ultrasharp-4x` — เน้นความคม
- `digital-art-4x` — เหมาะกับงานวาดและ digital art

โมเดลจะถูกดาวน์โหลดเฉพาะตัวที่เลือก ส่วนภาพในโฟลเดอร์ `input` สามารถรวมเข้าประมวลผลได้ด้วย checkbox ในหน้า Studio

## ความเป็นส่วนตัวและข้อจำกัด

- Web UI ใช้ลิงก์แชร์ Gradio แบบชั่วคราวและป้องกันด้วยรหัสผ่านที่สร้างใหม่ในแต่ละ runtime; อย่าแชร์ URL พร้อมรหัสผ่าน และหยุด Colab runtime เมื่อเลิกใช้งาน
- รูปถูกประมวลผลบน Colab runtime แต่การเปิดหน้า UI ผ่าน share link จะส่งทราฟฟิกผ่านบริการ Gradio; หลีกเลี่ยงภาพที่มีข้อมูลอ่อนไหว
- Colab บาง runtime มี CUDA แต่ไม่มี NVIDIA Vulkan ICD ที่ backend ต้องใช้ ในกรณีนั้นหน้า UI ยังเปิดได้ แต่การประมวลผลจะแจ้งสาเหตุและไม่ทำงาน
- หากภาพใหญ่แล้วหน่วยความจำ GPU ไม่พอ ให้เลือก Tile size `64` หรือ `32`; `Auto` ให้ backend เลือกขนาด tile
- แนะนำ PNG เมื่อต้องการรักษาความโปร่งใส

## Upstream และลิขสิทธิ์

- Upscayl application: <https://github.com/upscayl/upscayl>
- Upscayl NCNN backend: <https://github.com/upscayl/upscayl-ncnn>
- Notebook pin CLI release `20251207-174704` (ตรวจ SHA-256 ก่อนแตกไฟล์) และ pin โมเดลไว้ที่ commit `a00d55fee90e0f9435d5eaa86e76700df8199af8` เพื่อให้ผลการติดตั้งทำซ้ำได้
- Backend ระบุสัญญาอนุญาต AGPL-3.0; ไบนารีและโมเดลที่ Notebook ดาวน์โหลดคงประกาศ/เงื่อนไขของ upstream ไว้
