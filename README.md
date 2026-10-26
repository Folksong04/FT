# FT ♥

เว็บบันทึกรอบเดือน (ปฏิทินรายเดือน / รายปี + สรุปจำนวนวัน) โทนความรัก
ทุกคนที่ใส่รหัสผ่านถูกจะเห็นและแก้ไขข้อมูลชุดเดียวกัน ข้อมูลเก็บใน Google Sheet (แบบเดียวกับเว็บบันทึกสุขภาพคุณย่า)

- `index.html` - หน้าเว็บ (ขึ้น GitHub)
- `.nojekyll`, `manifest.json`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` - ขึ้น GitHub
- `google-apps-script.gs` - โค้ดฝั่ง Google Sheet (**ไม่ต้องขึ้น GitHub** เพราะมีรหัสผ่านอยู่)

## 1. ตั้งค่า Google Sheet (ทำครั้งเดียว)

1. สร้าง Google Sheet ใหม่ เช่นชื่อ `FT Data`
2. เมนู **ส่วนขยาย → Apps Script** → ลบโค้ดเดิม แล้ววางโค้ดทั้งหมดจาก `google-apps-script.gs` → กดบันทึก
3. กด **ทำให้ใช้งานได้ (Deploy) → การทำให้ใช้งานได้รายการใหม่ (New deployment)**
   - ประเภท: **เว็บแอป (Web app)**
   - เรียกใช้ในฐานะ (Execute as): **ฉัน (Me)**
   - ผู้ที่มีสิทธิ์เข้าถึง (Who has access): **ทุกคน (Anyone)**
   - กด Deploy → อนุญาตสิทธิ์ (Authorize) → คัดลอก **URL ของเว็บแอป** (ลงท้ายด้วย `/exec`)
4. เปิด `index.html` หาบรรทัด `const API_URL = 'PASTE_WEB_APP_URL_HERE';` แล้ววาง URL แทน

ข้อมูลจะไปอยู่ในแท็บ `Periods` ของ Sheet (คอลัมน์ วันที่มา / วันที่หาย / บันทึกเมื่อ)

> ถ้าแก้โค้ดใน Apps Script ภายหลัง ต้องกด **Deploy → Manage deployments → แก้ไข (ดินสอ) → Version: New version → Deploy**
> URL จะเหมือนเดิม ไม่ต้องแก้ `index.html`

## 2. ขึ้น GitHub Pages

1. อัปโหลดไฟล์ทั้งหมด **ยกเว้น** `google-apps-script.gs` ขึ้น repo (ถ้ามี `data.json` เก่าใน repo ให้ลบทิ้งได้)
2. **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main` / `(root)` → **Save**
3. ลิงก์เว็บคือ `https://<username>.github.io/<repo>/`

## รหัสผ่าน

- รหัสอยู่ในบรรทัด `const PIN = '...'` ของ Apps Script (ตรวจที่ฝั่ง Google ไม่ได้อยู่ในหน้าเว็บ)
  ถ้าจะเปลี่ยนรหัส แก้ที่ Apps Script แล้ว Deploy เวอร์ชันใหม่ตามด้านบน
- ใส่ครั้งเดียวต่อการเปิดแท็บ กด "🔒 ล็อก" เพื่อล็อกใหม่

## ใช้บนมือถือ

- หน้าเว็บปรับตามขนาดจอ ปัดซ้าย / ขวาบนปฏิทินเพื่อเปลี่ยนเดือน
- เพิ่มเป็นแอปบนหน้าจอหลัก
  - **iPhone (Safari):** ปุ่มแชร์ → "เพิ่มไปยังหน้าจอโฮม"
  - **Android (Chrome):** เมนู ⋮ → "เพิ่มลงในหน้าจอหลัก" / "ติดตั้งแอป"
