---
category: general
date: 2026-06-28
description: วิธีทำ OCR แบบกลุ่มใน Python—ดึงข้อความจากภาพและแปลงหน้าสแกนเป็นข้อความโดยใช้การประมวลผล
  OCR แบบกลุ่ม
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: th
og_description: เรียนรู้วิธีทำ OCR เป็นชุดใน Python ดึงข้อความจากรูปภาพ และแปลงหน้าสแกนเป็นข้อความด้วยการประมวลผล
  OCR แบบชุดที่มีประสิทธิภาพ
og_title: วิธีทำ OCR แบบแบตช์ใน Python – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: วิธีทำ OCR แบบชุดใน Python – คู่มือครบวงจรสำหรับการดึงข้อความจากภาพ
url: /th/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR ใน Python – คู่มือครบถ้วนสำหรับการดึงข้อความจากรูปภาพ

หากคุณกำลังสงสัย **วิธีทำ batch OCR ใน Python** คุณมาถูกที่แล้ว บทแนะนำนี้จะแสดงวิธีที่รวดเร็วในการ **ดึงข้อความจากรูปภาพ** และ **แปลงหน้าสแกนเป็นข้อความ** ด้วยการใช้อินสแตนซ์ของ OCR engine เพียงหนึ่งตัว ไม่ต้องคัดลอก‑วางไฟล์ทีละไฟล์อีกต่อไป—ให้โค้ดทำงานหนักแทน

เราจะเดินผ่านทุกอย่างที่คุณต้องการ: การติดตั้งไลบรารี, การโหลดโฟลเดอร์สแกนทั้งหมด, การรันการประมวลผล batch OCR, และการจัดการผลลัพธ์อย่างราบรื่น เมื่อเสร็จคุณจะมีสคริปต์ที่นำชุด PNG หรือ JPEG ไปแปลงเป็นไฟล์ข้อความที่ค้นหาได้ในไม่กี่วินาที

## สิ่งที่คุณต้องเตรียม

* Python 3.9+ ที่ติดตั้งแล้ว (โค้ดทำงานบน 3.8 ได้เช่นกัน แต่ 3.9+ จะให้คุณสมบัติ typing ที่ใหม่ที่สุด).
* ไลบรารี OCR สมัยใหม่—ที่นี่เราใช้ **Aspose.OCR for Python via .NET** ซึ่งเปิดเผยคลาส `OcrEngine` ตามที่แสดงในโค้ดตัวอย่างเดิม.  
  ```bash
  pip install aspose-ocr
  ```
* โฟลเดอร์ที่มีหน้าสแกน (`page1.png`, `page2.png`, …). สิ่งใดที่ Pillow เปิดได้ก็ทำงานได้, ดังนั้น PDF, TIFF หรือ BMP ก็ใช้ได้เช่นกัน.
* ความอยากรู้อยากเห็นเล็กน้อย—หากคุณยังไม่เคยทำอัตโนมัติ image‑to‑text มาก่อน คุณกำลังจะเห็นว่าทำไม batch OCR ถึงเป็นการเปลี่ยนเกม.

> **เคล็ดลับ:** หากคุณต้องการใช้ไลบรารี pure‑Python ให้เปลี่ยน `OcrEngine` เป็น `pytesseract.image_to_string`. โลจิกโดยรอบยังคงเหมือนเดิม.

## วิธีทำ Batch OCR ใน Python – คู่มือขั้นตอนโดยละเอียด

ด้านล่างเป็นสคริปต์ที่สมบูรณ์และสามารถรันได้ ทุกบรรทัดมีคอมเมนต์เพื่อให้คุณเห็น *ทำไม* แต่ละส่วนจึงสำคัญ ไม่ใช่แค่ *ทำอะไร*  

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### ผลลัพธ์ที่คาดหวัง

การรันสคริปต์กับโฟลเดอร์ที่มีสแกน PNG จำนวนสามไฟล์จะให้ผลลัพธ์ประมาณนี้:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

ตัวอย่างแสดง 200 ตัวอักษรแรกของแต่ละหน้า, และข้อความเต็มจะอยู่ในไดเรกทอรี `ocr_output`.

## ดึงข้อความจากรูปภาพโดยใช้ Engine เพียงหนึ่งตัว

ทำไมเราถึงสร้าง **หนึ่ง** `OcrEngine` แล้วนำกลับมาใช้ใหม่? การสร้างอินสแตนซ์ของ engine มีค่าใช้จ่ายสูงเพราะต้องโหลดแพ็คภาษาและ DLL เนทีฟ การแชร์อินสแตนซ์เดียวกันทั่ว batch จะทำให้คุณ:

* **ประหยัดหน่วยความจำ** – มีชุดทรัพยากรเพียงชุดเดียวที่อยู่ใน RAM.
* **เพิ่มความเร็ว** – engine ยังคงอยู่ในสถานะพร้อมทำงาน, หลีกเลี่ยงการเริ่มต้นซ้ำหลายครั้ง.
* **รักษาความสอดคล้อง** – การตั้งค่าการจดจำเดียวกันจะใช้กับทุกหน้า, ซึ่งสำคัญเมื่อคุณต้องการ **ดึงข้อความจากรูปภาพ** ที่มีรูปแบบเดียวกัน.

หากคุณต้องการปรับการจดจำ (เช่น เปิดการตรวจสอบการสะกดหรือเปลี่ยนภาษา) ให้ทำก่อน *ก่อน* เรียก `recognize_batch`. หน้าอื่น ๆ ที่ตามมาจะสืบทอดการตั้งค่าเหล่านั้นโดยอัตโนมัติ.

## แปลงหน้าสแกนเป็นข้อความอย่างมีประสิทธิภาพ

หัวใจของปัญหา—**แปลงหน้าสแกนเป็นข้อความ**—ได้รับการแก้ไขโดย `engine.recognize_batch(images)`. ภายใต้การทำงานไลบรารีจะประมวลผลแต่ละรูปภาพใน pool ของเธรดพื้นหลัง, ทำให้คุณได้การสเกลแบบเกือบเชิงเส้นบนเครื่องหลายคอร์ สิ่งที่ควรจำไว้บ้าง:

* **คุณภาพของภาพสำคัญ** – 300 dpi หรือสูงกว่าให้ผลลัพธ์ดีที่สุด หากสแกนของคุณความละเอียดต่ำ ให้พิจารณา up‑sampling ด้วย Pillow ก่อนส่งให้ engine.
* **สี vs. เฉดสีเทา** – OCR engine มักทำงานเร็วกว่าในโหมด 8‑bit grayscale. คุณสามารถเพิ่มขั้นตอนการเตรียมล่วงหน้า:  
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **การสนับสนุนภาษา** – Aspose.OCR รองรับกว่า 40 ภาษา ตั้ง `engine.language = "eng"` หรือ `"fra"` ก่อนเรียก batch หากคุณไม่ได้ทำงานกับภาษาอังกฤษ.

## แนวทางปฏิบัติที่ดีที่สุดสำหรับการประมวลผล Batch OCR

แม้โค้ดข้างต้นจะสั้นแล้ว, การใช้งาน batch OCR ระดับ production มักต้องการการป้องกันเพิ่มเติม:

| ข้อกังวล | แนวทางแนะนำ |
|----------|----------------------|
| **ชุดข้อมูลขนาดใหญ่ ( > 500 ไฟล์ )** | แบ่งเป็นส่วนย่อยของ 100–200 รูปภาพเพื่อให้การใช้หน่วยความจำน้อยลง. |
| **ไฟล์เสียหายหรือไม่รองรับ** | `load_images` helper จะจับข้อยกเว้นและบันทึกคำเตือนแล้ว; คุณยังสามารถเขียน fallback เพื่อข้ามหรือย้ายไฟล์ที่เสียได้. |
| **การตรวจสอบความคืบหน้า** | ห่อ `recognize_batch` ในลูปที่ให้ผลลัพธ์หลังจากแต่ละรูปภาพ หากไลบรารีมี callback ต่อภาพ. |
| **การประมวลผลหลัง** | ทำการตรวจสอบการสะกดหรือทำความสะอาดด้วย regex บนสตริงที่ได้เพื่อปรับปรุงการค้นหาในขั้นต่อไป. |
| **การทำงานแบบขนาน** | หากคุณมีการตั้งค่าหลายโหนด, แจกจ่ายโฟลเดอร์ไปยัง worker ต่าง ๆ แล้วรวมผลลัพธ์ `.txt` สุดท้าย. |

## คำถามที่พบบ่อย

**Q: สามารถใช้กับ PDF โดยตรงได้หรือไม่?**  
A: แน่นอน. แปลงแต่ละหน้าของ PDF เป็นภาพก่อน (เช่น ใช้ `pdf2image`) แล้วส่งรายการที่ได้ให้ `recognize_batch`. ส่วนที่เหลือของ pipeline จะไม่เปลี่ยนแปลง

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณเอง.

- [ดึงข้อความจากรูปภาพด้วย Aspose OCR – คู่มือขั้นตอนโดยละเอียด](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [ดึงข้อความจากรูปภาพโดยใช้การทำ OCR บนโฟลเดอร์](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [วิธีดึงข้อความจากไฟล์ ZIP โดยใช้ Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}