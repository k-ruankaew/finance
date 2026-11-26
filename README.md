# ระบบเอกสารบัญชี

เว็บแอปหน้าเดียวสำหรับเอกสารบัญชีของบริษัท: ใบขอซื้อ/ขอจ้าง (PR), ใบขอเบิกค่าใช้จ่าย, ใบเบิกเงินทดรองจ่าย (FM-AC-03),
ใบเบิกค่าเดินทาง, ใบรับรองแทนใบเสร็จ (FM-AC-02), ใบแจ้งเปิดโครงการ และใบแจ้งเปลี่ยนแปลง/ปิดโครงการ

## ไฟล์
| ไฟล์ | หน้าที่ |
|---|---|
| `index.html` | ตัวระบบทั้งหมด (HTML/CSS/JS ไฟล์เดียว) |
| `xltemplates.js` | แม่แบบ Excel ของบริษัท (base64) ใช้ตอนดาวน์โหลดแบบฟอร์ม .xlsx |
| `templates/*.xlsx` | แม่แบบ Excel ต้นฉบับ (สร้าง `xltemplates.js` ใหม่จากไฟล์เหล่านี้ได้) |

## การเก็บข้อมูล
- เมื่อเปิดเป็น Artifact บน claude.ai: ใช้ฐานข้อมูลกลางของ Artifact (`claude.use("db")`), ตัวตนผู้ใช้ (`user`) และการดาวน์โหลด (`downloads`)
- เมื่อเปิดนอก claude.ai (เช่น GitHub Pages หรือเปิดไฟล์ตรง ๆ): ทำงานใน **โหมดออฟไลน์** ข้อมูลเก็บใน localStorage ของเบราว์เซอร์นั้นเท่านั้น ไม่แชร์ข้ามคน และปุ่มดาวน์โหลดใช้ไม่ได้

## สร้าง xltemplates.js ใหม่หลังแก้แม่แบบ
```bash
python3 -c "import base64,json;n=['pr.xlsx','exp.xlsx','adv.xlsx','pj.xlsx'];open('xltemplates.js','w').write('window.XLTPL='+json.dumps({x:base64.b64encode(open('templates/'+x,'rb').read()).decode() for x in n})+';\n')"
```
