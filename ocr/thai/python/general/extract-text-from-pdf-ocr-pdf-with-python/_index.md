---
category: general
date: 2026-04-29
description: ดึงข้อความจาก PDF ด้วย Aspose OCR ใน Python. เรียนรู้การประมวลผล OCR
  PDF แบบชุด, แปลงข้อความจาก PDF ที่สแกน, และจัดการหน้าที่มีความมั่นใจต่ำ.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: th
og_description: ดึงข้อความจาก PDF ด้วย Aspose OCR ใน Python คู่มือนี้แสดงการประมวลผล
  OCR PDF แบบชุด การแปลงข้อความจาก PDF ที่สแกน และการจัดการผลลัพธ์ที่มีความมั่นใจต่ำ.
og_title: ดึงข้อความจาก PDF – OCR PDF ด้วย Python
tags:
- OCR
- Python
- PDF processing
title: ดึงข้อความจาก PDF – OCR PDF ด้วย Python
url: /th/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจาก PDF – OCR PDF ด้วย Python

เคยต้อง **ดึงข้อความจาก PDF** แต่ไฟล์เป็นแค่ภาพสแกนหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องแปลง PDF ให้เป็นข้อมูลที่ค้นหาได้ ข่าวดีคือ? ด้วย Aspose OCR for Python คุณสามารถแปลงข้อความจาก PDF สแกนได้ในไม่กี่บรรทัด และยังสามารถทำ **การประมวลผล OCR PDF แบบแบตช์** เมื่อคุณมีหลายสิบไฟล์ต้องจัดการ

ในบทเรียนนี้เราจะเดินผ่านขั้นตอนทั้งหมด: ตั้งค่าห้องสมุด, รัน OCR บน PDF เดียว, ขยายเป็นแบตช์, และจัดการกับหน้าที่ความเชื่อมั่นต่ำเพื่อให้คุณทราบเมื่อจำเป็นต้องตรวจสอบด้วยตนเอง เมื่อจบคุณจะได้สคริปต์พร้อมรันที่ดึงข้อความจาก PDF สแกนใด ๆ และคุณจะเข้าใจเหตุผลของแต่ละขั้นตอน

## สิ่งที่คุณต้องมี

ก่อนที่เราจะเริ่มลงมือ ตรวจสอบให้แน่ใจว่าคุณมี:

- Python 3.8 หรือใหม่กว่า (โค้ดใช้ f‑strings ดังนั้น 3.6+ ทำงานได้ แต่แนะนำ 3.8+)
- ใบอนุญาต Aspose OCR for Python หรือคีย์ทดลองฟรี (คุณสามารถรับได้จากเว็บไซต์ Aspose)
- โฟลเดอร์ที่มี PDF สแกนหนึ่งไฟล์หรือหลายไฟล์ที่ต้องการประมวลผล
- พื้นที่ดิสก์เพียงพอสำหรับไฟล์รายงาน *.txt* ที่สร้างขึ้น

เท่านี้—ไม่มีการพึ่งพาไลบรารีภายนอกหนัก ๆ, ไม่มีการทำงานกับ OpenCV. เอนจิน OCR ของ Aspose จะทำงานหนักให้คุณ

## ตั้งค่าสภาพแวดล้อม

แรกสุด ให้ติดตั้งแพ็กเกจ Aspose OCR จาก PyPI:

```bash
pip install aspose-ocr
```

หากคุณมีไฟล์ใบอนุญาต (`Aspose.OCR.lic`) ให้วางไว้ที่รากของโปรเจกต์และเปิดใช้งานดังนี้:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **เคล็ดลับ:** อย่าวางไฟล์ใบอนุญาตไว้ในระบบควบคุมเวอร์ชัน; เพิ่มไฟล์นี้ใน `.gitignore` เพื่อหลีกเลี่ยงการเปิดเผยโดยบังเอิญ

## ทำ OCR บน PDF เดียว

ตอนนี้มาดึงข้อความจาก PDF สแกนไฟล์เดียว ขั้นตอนหลักคือ:

1. สร้างอินสแตนซ์ `OcrEngine`
2. ชี้ไปที่ไฟล์ PDF
3. ดึง `OcrResult` สำหรับแต่ละหน้า
4. เขียนผลลัพธ์เป็นข้อความธรรมดาไปยังดิสก์
5. ปิดการทำงานของเอนจินเพื่อปล่อยทรัพยากรเนทีฟ

นี่คือสคริปต์เต็มที่สามารถรันได้:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**สิ่งที่คุณจะเห็น:** สำหรับแต่ละหน้า สคริปต์จะแสดงข้อความเช่น `Page 1: confidence 97.45%`. หากหน้าหนึ่งมีความเชื่อมั่นต่ำกว่า 80 % จะมีคำเตือนปรากฏ เพื่อบอกว่าการ OCR อาจพลาดอักขระบางตัว

### ทำไมวิธีนี้ถึงได้ผล

- **`OcrEngine`** เป็นประตูสู่ไลบรารี Aspose OCR เนทีฟ; มันจัดการทุกอย่างตั้งแต่การเตรียมภาพล่วงหน้าไปจนถึงการจดจำอักขระ
- **`extract_from_pdf`** จะทำการแรสเตอร์แต่ละหน้าของ PDF โดยอัตโนมัติ ไม่ต้องแปลง PDF เป็นภาพด้วยตนเอง
- **คะแนนความเชื่อมั่น** ช่วยให้คุณทำการตรวจสอบคุณภาพอัตโนมัติ—สำคัญมากเมื่อคุณประมวลผลเอกสารทางกฎหมายหรือการแพทย์ที่ต้องการความแม่นยำสูง

## การประมวลผล OCR PDF แบบแบตช์ด้วย Python

โครงการในโลกจริงส่วนใหญ่ต้องจัดการไฟล์มากกว่าหนึ่งไฟล์ ให้ขยายสคริปต์ไฟล์เดียวเป็น **pipeline การประมวลผล OCR PDF แบบแบตช์** ที่เดินผ่านไดเรกทอรี, ประมวลผลแต่ละ PDF, และเก็บผลลัพธ์ในโฟลเดอร์ย่อยที่สอดคล้องกัน

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### วิธีที่ช่วยได้

- **ความสามารถขยาย:** ฟังก์ชันเดินผ่านโฟลเดอร์ครั้งเดียว สร้างโฟลเดอร์ย่อยสำหรับผลลัพธ์ของแต่ละ PDF ทำให้จัดการได้เป็นระเบียบเมื่อมีเอกสารหลายสิบไฟล์
- **การนำกลับมาใช้ใหม่:** `ocr_pdf_file` สามารถเรียกจากสคริปต์อื่น (เช่น เว็บเซอร์วิส) เนื่องจากเป็นฟังก์ชันบริสุทธิ์
- **การจัดการข้อผิดพลาด:** สคริปต์จะแสดงข้อความเป็นมิตรหากโฟลเดอร์อินพุตว่างเปล่า ช่วยหลีกเลี่ยงการล้มเหลวแบบเงียบ

## แปลงข้อความจาก PDF สแกน – จัดการกรณีขอบ

แม้โค้ดข้างต้นจะทำงานได้กับ PDF ส่วนใหญ่ คุณอาจเจอกรณีพิเศษบางอย่าง:

| สถานการณ์ | สาเหตุ | วิธีแก้ |
|-----------|--------|----------|
| **PDF ที่เข้ารหัส** | PDF มีการป้องกันด้วยรหัสผ่าน | ส่งรหัสผ่านไปยัง `extract_from_pdf(pdf_path, password="yourPwd")` |
| **เอกสารหลายภาษา** | Aspose OCR ตั้งค่าเริ่มต้นเป็นภาษาอังกฤษ | ตั้งค่า `ocr_engine.language = "spa"` สำหรับภาษาสเปน หรือระบุรายการภาษาสำหรับหลายภาษา |
| **PDF ขนาดใหญ่มาก (>500 หน้า)** | การใช้หน่วยความจำพุ่งสูงเพราะโหลดทุกหน้าเข้าสู่ RAM | ประมวลผล PDF เป็นชิ้นส่วนโดยใช้ `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` แล้ววนลูป |
| **คุณภาพสแกนแย่** | DPI ต่ำหรือมีสัญญาณรบกวนมากทำให้ความเชื่อมั่นลดลง | ทำการพรี‑โปรเซสภาพด้วย `engine.image_preprocessing = True` หรือเพิ่ม DPI ผ่าน `engine.dpi = 300` |

> **ระวัง:** การเปิดใช้งานการพรี‑โปรเซสภาพอาจทำให้เวลา CPU เพิ่มขึ้นอย่างเห็นได้ชัด หากคุณรันแบตช์ทุกคืน ควรจัดสรรเวลาให้เพียงพอหรือใช้ worker แยกออกมา

## ตรวจสอบผลลัพธ์

หลังสคริปต์ทำงานเสร็จ คุณจะพบโครงสร้างโฟลเดอร์เช่น:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

เปิดไฟล์ `.txt` ใดก็ได้; คุณควรเห็นข้อความที่เป็น UTF‑8 สะอาดตรงกับเนื้อหาที่สแกนไว้เดิม หากพบอักขระแปลก ๆ ให้ตรวจสอบการตั้งค่าภาษาใน PDF และตรวจสอบว่ามีการติดตั้งแพ็คฟอนต์ที่ถูกต้องบนเครื่อง

## ทำความสะอาดทรัพยากร

Aspose OCR พึ่งพา DLL เนทีฟ ดังนั้นจึงจำเป็นต้องเรียก `engine.dispose()` หลังจากใช้งานเสร็จ การลืมขั้นตอนนี้อาจทำให้เกิดการรั่วของหน่วยความจำ โดยเฉพาะในงานแบตช์ที่รันเป็นเวลานาน

```python
# Always the last line of your script
engine.dispose()
```

## ตัวอย่างครบวงจรจากต้นจนจบ

รวมทุกอย่างเข้าด้วยกัน นี่คือตัวอย่างสำหรับไฟล์เดียว

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}