---
category: general
date: 2026-06-06
description: วิธีทำ OCR PDF และสร้างไฟล์ PDF ที่ค้นหาได้จากรูปภาพโดยใช้ Python เรียนรู้การเพิ่มข้อความที่ค้นหาได้และแปลงรูปภาพเป็น
  PDF/A ภายในไม่กี่นาที
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: th
og_description: วิธีทำ OCR PDF ทีละขั้นตอน เรียนรู้การเพิ่มข้อความที่ค้นหาได้และแปลงภาพเป็น
  PDF/A ด้วยสคริปต์ Python อย่างง่าย
og_title: วิธีทำ OCR PDF – คู่มือเร็วเพื่อสร้าง PDF ที่ค้นหาได้
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: วิธีทำ OCR PDF ด้วย Python – สร้าง PDF ที่ค้นหาได้จากรูปภาพ
url: /th/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR PDF – แปลงภาพสแกนเป็น PDF ที่ค้นหาได้

เคยสงสัยไหมว่า **วิธีทำ OCR PDF** เมื่อคุณมีเพียงภาพสแกนของใบแจ้งหนี้หรือใบเสร็จ? คุณไม่ได้เป็นคนเดียวที่เป็นเช่นนั้น ในหลายสำนักงาน เอกสารที่เข้ามามักเป็นไฟล์ PNG หรือ JPEG แบน และขั้นตอนต่อไป—การทำให้เนื้อหานั้นสามารถค้นหาได้—ดูเหมือนเป็นกล่องดำ  

ข่าวดีคือ? ด้วยเพียงไม่กี่บรรทัดของ Python คุณสามารถ **สร้าง PDF ที่ค้นหาได้** , **เพิ่มข้อความที่ค้นหาได้**, และแม้กระทั่ง **แปลงภาพเป็น PDF/A** เพื่อการเก็บรักษาระยะยาว ในบทแนะนำนี้เราจะเดินผ่านแต่ละขั้นตอน อธิบายเหตุผลที่สำคัญ และให้สคริปต์พร้อมใช้งานที่คุณสามารถใส่ลงในโครงการใดก็ได้

> **เคล็ดลับ:** วิธีเดียวกันนี้ใช้ได้กับการสแกนหลายหน้า; เพียงวนลูปไฟล์และเอนจินจะทำงานหนักให้เอง.

---

## สิ่งที่คุณต้องเตรียม

ก่อนที่เราจะดำเนินการต่อ โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้บนเครื่องของคุณ:

| ความต้องการ | เหตุผลที่สำคัญ |
|-------------|----------------|
| Python 3.9 หรือใหม่กว่า | ไวยากรณ์สมัยใหม่และการสนับสนุนไลบรารีที่ดีกว่า |
| `pdfium`‑based OCR engine (e.g., `pdfocr` or a commercial SDK) | จัดการการจดจำภาพและการสร้าง PDF/A |
| ไฟล์รูปภาพ (PNG, JPEG, TIFF) ที่คุณต้องการแปลงเป็น PDF ที่ค้นหาได้ | แหล่งที่มาของข้อความ |
| สิทธิ์การเขียนในโฟลเดอร์ผลลัพธ์ | เพื่อให้สคริปต์บันทึก PDF ใหม่ได้ |

หากคุณยังไม่ได้ติดตั้ง OCR SDK ให้รัน:

```bash
pip install pdfocr   # replace with your vendor's package name
```

แค่นั้น—ไม่มีการพึ่งพาระบบที่ซับซ้อน เพียงแค่ `pip install`.

---

## วิธีทำ OCR PDF – ภาพรวม

ในระดับสูง กระบวนการประกอบด้วยสามการกระทำง่าย ๆ:

1. **Recognize** ข้อความภายในภาพพร้อมคงกราฟิกเดิมไว้.  
2. **Export** ผลลัพธ์ OCR พร้อมภาพต้นฉบับเป็น **searchable PDF/A** (รูปแบบ PDF ที่เหมาะกับการเก็บรักษาระยะยาว).  
3. **Validate** ว่าไฟล์ที่ได้มีข้อความที่เลือกได้และค้นหาได้ซ้อนอยู่เหนือรูปภาพต้นฉบับ.

ด้านล่างคุณจะเห็นแต่ละขั้นตอนในโค้ด พร้อมคำอธิบาย *ทำไม* ของคำสั่งต่าง ๆ

---

## ขั้นตอนที่ 1: จดจำข้อความจากภาพ

ก่อนอื่นเราขอให้เอนจิน OCR อ่านพิกเซลและคืนอ็อบเจกต์ผลลัพธ์ที่เก็บทั้งภาพดิบและข้อความที่สกัดออกมา คิดว่าเป็นการที่เอนจิน “อ่าน” ใบแจ้งหนี้ให้คุณ

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### ทำไมเรื่องนี้ถึงสำคัญ

- **Preserving graphics** หมายถึงการคงเลย์เอาต์แบบภาพ (ตาราง, โลโก้, ตราประทับ) ให้เหมือนกับที่สแกนจับได้อย่างแม่นยำ.  
- อ็อบเจกต์ `result` มักจะมีเลเยอร์ข้อความที่ซ่อนอยู่ซึ่งเราจะฝังลงใน PDF ในขั้นต่อไป.  
- การใช้ `recognize_image` แทน `recognize_pdf` ช่วยหลีกเลี่ยงขั้นตอนแปลงเพิ่มเติม ทำให้การประมวลผลสำหรับภาพหน้าเดียวเร็วขึ้น.

#### ความแปรผันทั่วไป

- หากคุณมี **multi‑page TIFF** ให้ส่งพาธไฟล์โดยตรง; เอนจินส่วนใหญ่จะถือแต่ละหน้าเป็นภาพแยกกัน.  
- สำหรับ PDF ที่มีภาพอยู่แล้ว คุณสามารถเรียก `engine.recognize_pdf("file.pdf")` และข้ามขั้นตอนนี้ได้เลย.

---

## ขั้นตอนที่ 2: ส่งออกผลลัพธ์ OCR เป็น PDF/A ที่ค้นหาได้

ตอนนี้เรานำ `result` จากขั้นตอน 1 ไปบอกเอนจินให้เขียนไฟล์ใหม่ ธงสำคัญที่นี่คือ *PDF/A*—เวอร์ชันมาตรฐาน ISO ของ PDF ที่ออกแบบมาสำหรับการเก็บรักษาระยะยาว

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### ทำไมเรื่องนี้ถึงสำคัญ

- **Searchable PDF**: ไฟล์ผลลัพธ์มีเลเยอร์ข้อความที่ซ่อนอยู่และสามารถเลือกได้ คุณจึงสามารถกด Ctrl + F ค้นหาในเอกสารได้ทันที.  
- **PDF/A compliance**: องค์กรบางแห่ง (กฎหมาย, การเงิน) ต้องการ PDF/A เพื่อเป็นหลักฐานตรวจสอบ; ขั้นตอนนี้ทำให้เป็นไปตามกฎโดยอัตโนมัติ.  
- วิธีนี้ยัง **adds searchable text** โดยไม่ทำให้ภาพแบนลง จึงรักษาความคมชัดของกราฟิกได้อย่างสมบูรณ์.

#### Edge case: Need a regular PDF instead?

หากคุณไม่ต้องการ PDF/A ให้เปลี่ยน `save_as_pdfa` เป็น `save_as_pdf` ส่วนที่เหลือของเวิร์กโฟลว์ยังคงเหมือนเดิม.

---

## ขั้นตอนที่ 3: ตรวจสอบ PDF ที่ค้นหาได้

การตรวจสอบอย่างรวดเร็วจะช่วยป้องกันบั๊กที่ซ่อนอยู่ในภายหลัง เปิดไฟล์ที่สร้างขึ้นในโปรแกรมอ่าน PDF ใดก็ได้ ลองเลือกคำหนึ่งคำและใช้ฟังก์ชันค้นหา

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณรันสคริปต์ คอนโซลจะแสดง:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

เมื่อเปิดไฟล์ คุณควรเห็นภาพใบแจ้งหนี้ต้นฉบับพร้อมเลเยอร์ข้อความที่บางและมองไม่เห็น การไฮไลท์คำใดก็จะพบว่ามันเลือกได้—**นั่นคือข้อความที่ค้นหาได้** ที่คุณเพิ่งเพิ่มเข้าไป.

---

## การเพิ่มข้อความที่ค้นหาได้ให้กับ PDF ที่มีอยู่ (โบนัส)

บางครั้งคุณอาจมี PDF อยู่แล้วแต่ต้อง **add searchable text** ให้กับมัน เอนจินเดียวกันสามารถซ้อนผลลัพธ์ OCR ลงบน PDF ที่มีอยู่ได้:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

ที่นี่ `apply_to` จะผสานเลเยอร์ที่ซ่อนอยู่กับหน้าต้นฉบับ ทำให้คุณ **create searchable PDF** ได้โดยไม่ต้องสแกนใหม่.

---

## ข้อผิดพลาดทั่วไปและเคล็ดลับ

| ปัญหา | วิธีหลีกเลี่ยง |
|-------|----------------|
| **Low‑resolution source images** (< 150 dpi) | ขยายภาพหรือขอสแกนความละเอียดสูงกว่า; ความแม่นยำของ OCR ลดลงอย่างมากเมื่อต่ำกว่า 150 dpi. |
| **Missing language data** | ติดตั้งแพ็คเกจภาษาที่เหมาะกับ OCR engine ของคุณ (`pip install pdfocr[eng,spa]`). |
| **Output folder not writable** | รันสคริปต์ด้วยสิทธิ์ที่เพียงพอหรือเลือกไดเรกทอรีอื่น. |
| **PDF/A validation fails** | ตรวจสอบว่าไม่ได้ฝังฟอนต์หรือ JavaScript ที่ไม่รองรับ; ส่วนใหญ่ SDK จะจัดการให้โดยอัตโนมัติเมื่อใช้ `save_as_pdfa`. |

---

## สคริปต์เต็ม – โซลูชันไฟล์เดียว

ด้านล่างเป็นสคริปต์ที่ทำงานแบบอิสระซึ่งเชื่อมทุกอย่างเข้าด้วยกัน คัดลอก‑วาง แทนที่พาธตัวแปร แล้วคุณก็พร้อม **convert image to PDF/A** ภายในไม่กี่วินาที

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**สิ่งที่สคริปต์นี้ทำ:**  
1. โหลด OCR engine.  
2. อ่านภาพที่เลือกและสกัดข้อความ.  
3. เขียน **searchable PDF/A** ที่คุณสามารถแจกจ่ายหรือเก็บรักษาได้ทันที.  

คุณสามารถห่อ `main` logic ไว้ในฟังก์ชันที่ประมวลผลโฟลเดอร์ทั้งหมด—เพียงวนลูป `os.listdir()` แล้วทำซ้ำสามขั้นตอนสำหรับแต่ละไฟล์.

---

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง

ตอนนี้คุณได้เชี่ยวชาญ **วิธีทำ OCR PDF** แล้ว ลองสำรวจแนวคิดต่อไปนี้:

- **Batch processing:** ใช้ `concurrent.futures` เพื่อ OCR ใบแจ้งหนี้หลายสิบฉบับพร้อมกัน.  
- **Metadata injection:** เพิ่มวันที่สร้างหรือหมายเลขใบแจ้งหนี้ลงในเมตาดาต้า PDF เพื่อการจัดทำดัชนีที่ง่ายขึ้น.  
- **Hybrid PDFs:** ผสานข้อความที่ค้นหาได้กับภาพต้นฉบับที่ฝังไว้เพื่อสร้าง “digital twin” ของเอกสารกระดาษ.  
- **Alternative outputs:** ส่งออกเป็น **DOCX** หรือ **HTML** หากระบบ downstream ต้องการรูปแบบที่แก้ไขได้.  

แต่ละหัวข้อนี้ต่อยอดจากแนวคิดหลักที่คุณเรียนรู้—recognize, export, verify.

---

## สรุป

โดยสรุป คุณตอนนี้รู้แล้วว่า **วิธีทำ OCR PDF** โดยการแปลงภาพง่าย ๆ ให้เป็น **searchable PDF/A** ด้วยเพียงสามบรรทัดของ Python สคริปต์จัดการงานหนัก คงกราฟิกต้นฉบับ และให้เอกสารที่เป็นมาตรฐานซึ่งคุณสามารถค้นหา, เก็บรักษา หรือแชร์ได้  

ลองใช้กับใบแจ้งหนี้, ใบเสร็จ, หรือสัญญาที่สแกนของคุณ หากเจออุปสรรคใด ๆ คอมเมนต์ด้านล่างหรือดูเอกสารอย่างเป็นทางการของ SDK—มักจะมีตัวอย่างเพิ่มเติมมากมาย. Happy coding, และสนุกกับความสามารถใหม่ที่ทำให้ภาพใด ๆ กลายเป็นข้อมูลที่ค้นหาได้ทันที!

![ตัวอย่างวิธีทำ OCR PDF แสดงภาพต้นฉบับและการซ้อนทับ PDF ที่ค้นหาได้](placeholder.png "ตัวอย่างวิธีทำ OCR PDF")

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ต่อ‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโครงการของคุณเอง

- [วิธีทำ OCR PDF ด้วย .NET และ Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [จดจำข้อความ PDF – การทำ OCR ด้วย Aspose.OCR สำหรับ Java](/ocr/english/java/ocr-operations/)
- [แปลงภาพเป็น PDF C# – บันทึกผลลัพธ์ OCR หลายหน้า](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}