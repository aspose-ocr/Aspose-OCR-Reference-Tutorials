---
category: general
date: 2026-06-16
description: ดึงข้อความจากไฟล์ TIFF ด้วย Python OCR. เรียนรู้วิธีแปลง TIFF เป็นข้อความแบบขั้นตอนต่อขั้นตอน
  พร้อมจัดการเอกสารหลายหน้าได้อย่างง่ายดาย.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: th
og_description: ดึงข้อความจากไฟล์ TIFF ด้วย Python OCR. ทำตามคำแนะนำนี้เพื่อแปลง TIFF
  เป็นข้อความ, จัดการการสแกนหลายหน้า, และได้ผลลัพธ์ที่สะอาด.
og_title: ดึงข้อความจากไฟล์ TIFF – คู่มือ Python ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: สกัดข้อความจากไฟล์ TIFF – คู่มือ Python ฉบับสมบูรณ์
url: /th/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจาก TIFF – คู่มือ Python ฉบับสมบูรณ์

เคยต้องการ **ดึงข้อความจากภาพ TIFF** แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องจัดการกับเอกสารสแกนหรือเอกสารเก่า ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ Python คุณสามารถ **แปลง TIFF เป็นข้อความ** ได้อย่างรวดเร็ว แม้ไฟล์จะมีหลายสิบหน้า

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างจากโลกจริง: โหลดไฟล์ TIFF หลายหน้า, ตั้งค่าภาษา OCR เป็นภาษาฝรั่งเศส, และดึงข้อความที่ได้รับการจดจำออกจากแต่ละหน้า. เมื่อจบคุณจะมีสคริปต์พร้อมรัน, เข้าใจเหตุผลของแต่ละขั้นตอน, และรู้วิธีปรับใช้กับภาษาอื่นหรือรูปแบบภาพอื่น

## ข้อกำหนดเบื้องต้น

- ติดตั้ง Python 3.8 หรือใหม่กว่า
- แพคเกจ `ocr` (หรือไลบรารี OCR ที่เข้ากันได้ซึ่งมีคลาส `OcrEngine`). คุณสามารถติดตั้งด้วย `pip install ocr-lib`—เปลี่ยนเป็นชื่อแพคเกจจริงที่คุณใช้
- ไฟล์ TIFF หลายหน้า (เช่น `french-scans.tif`) ที่คุณต้องการประมวลผล
- ความคุ้นเคยพื้นฐานกับการเขียนสคริปต์ Python

ไม่มีการพึ่งพาที่หนักหน่วง, ไม่มีบริการภายนอก—เพียงแค่ Python ธรรมดาและเครื่องมือ OCR

---

## ขั้นตอนที่ 1: ตั้งค่า OCR Engine เพื่อ **ดึงข้อความจาก TIFF**

สิ่งแรกที่ต้องทำ—เราต้องการอินสแตนซ์ของ OCR engine และต้องบอกให้มันรู้ว่าจะใช้ภาษาอะไร. ในกรณีของเราวัสดุเป็นภาษาฝรั่งเศส, ดังนั้นเราจะตั้งค่าภาษาให้สอดคล้อง

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**ทำไมสิ่งนี้ถึงสำคัญ:**  
การตั้งค่าภาษาช่วยเพิ่มความแม่นยำอย่างมาก. ตัวอักษรภาษาฝรั่งเศสเช่น “é” หรือ “ç” จะถูกอ่านผิดเป็นสัญลักษณ์ทั่วไปหาก engine ใช้ค่าเริ่มต้นเป็นภาษาอังกฤษ. โดยการเลือกภาษาฝรั่งเศสอย่างชัดเจน เราให้แผนที่อักขระที่ถูกต้องกับ engine

> **เคล็ดลับ:** หากคุณกำลังประมวลผลเอกสารหลายภาษา, คุณสามารถเปลี่ยน `engine.language` ได้ทันทีก่อนการเรียก `recognize()` แต่ละครั้ง

---

## ขั้นตอนที่ 2: โหลดไฟล์ TIFF หลายหน้าที่คุณต้องการ **แปลง TIFF เป็นข้อความ**

ไฟล์ TIFF สามารถเก็บหลายเฟรม—คิดว่าแต่ละเฟรมเป็นหน้าแยก. ไลบรารี OCR ทำให้เรามองข้ามรายละเอียดนี้, ดังนั้นเราเพียงแค่ชี้ไปที่ไฟล์

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**คำเตือนกรณีขอบ:**  
หากเส้นทางไฟล์ผิดหรือไฟล์ TIFF เสียหาย, เมธอด `load_from_file` จะโยนข้อยกเว้น. ควรห่อไว้ในบล็อก `try/except` สำหรับโค้ดการผลิต:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## ขั้นตอนที่ 3: รัน OCR บนเอกสารทั้งหมด – แกนหลักของ **ดึงข้อความจาก TIFF**

ตอนนี้ให้ engine ทำการเวทมนต์ของมัน. การเรียก `recognize()` จะประมวลผลทุกหน้าในครั้งเดียวและคืนค่าอ็อบเจ็กต์ผลลัพธ์ที่เต็มรูปแบบ

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**อะไรกำลังเกิดขึ้นเบื้องหลัง?**  
Engine จะวนลูปแต่ละเฟรม, ทำการเตรียมข้อมูลล่วงหน้า (การจัดแนวใหม่, การทำไบนารี), รันเครือข่ายประสาทเทียม, และรวมผลลัพธ์. เนื่องจากเราเรียก `recognize()` เพียงครั้งเดียว, ไลบรารีสามารถแชร์ทรัพยากรระหว่างหน้า, ทำให้เร็วกว่าเมื่อวนลูปด้วยตนเอง

---

## ขั้นตอนที่ 4: ดึงข้อความที่จดจำได้จากผลลัพธ์ JSON – **แปลง TIFF เป็นข้อความ** หน้าโดยหน้า

อ็อบเจ็กต์ผลลัพธ์สามารถแปลงเป็น JSON. ภายใน JSON นั้นคุณจะพบอาเรย์ `pages`, แต่ละอันมีฟิลด์ `text`

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

ตอนนี้เรามีรายการ Python ที่สะอาดซึ่งแต่ละองค์ประกอบสอดคล้องกับผลลัพธ์ OCR ของแต่ละหน้า

---

## ขั้นตอนที่ 5: พิมพ์หรือบันทึกข้อความสำหรับแต่ละหน้า – ส่วนสุดท้ายของ **ดึงข้อความจาก TIFF**

ให้เราวนลูปผ่านหน้าและแสดงข้อความที่ดึงออกมา. คุณยังสามารถเขียนแต่ละหน้าเป็นไฟล์ `.txt` แยกต่างหากหากต้องการ

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### ผลลัพธ์ที่คาดหวัง (ตัวอย่าง)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

หาก OCR สำเร็จ, คุณจะเห็นบล็อกข้อความภาษาฝรั่งเศสที่สะอาดสำหรับแต่ละหน้า. หากพบอักขระผิดรูป, ตรวจสอบการตั้งค่าภาษาอีกครั้งหรือพิจารณาเพิ่มความละเอียดของภาพก่อน OCR

---

## การจัดการกับปัญหาทั่วไปเมื่อคุณ **แปลง TIFF เป็นข้อความ**

| ปัญหา | ทำไมถึงเกิด | วิธีแก้เร็ว |
|-------|--------------|-------------|
| **อาเรย์ `pages` ว่าง** | TIFF ไม่ได้โหลดอย่างถูกต้องหรือไม่มีเฟรม. | ตรวจสอบเส้นทางไฟล์และให้แน่ใจว่า TIFF ไม่ใช่ PNG หน้าหนึ่งที่ปลอมเป็น TIFF. |
| **อักขระเสีย** | ความไม่ตรงกันของภาษา หรือคุณภาพภาพต่ำ. | ตั้งค่า `engine.language` ให้ถูกต้องและทำการเตรียมภาพล่วงหน้า (เช่น เพิ่ม DPI). |
| **หน่วยความจำพุ่งสูงเมื่อใช้ TIFF ขนาดใหญ่** | การโหลดทุกหน้าพร้อมกันใช้ RAM มาก. | ประมวลผลเป็นชิ้นส่วน: โหลดเฟรมเดียว, ทำ OCR, แล้วทิ้งก่อนไปยังหน้าถัดไป. |
| **ข้อผิดพลาด Unicode เมื่อพิมพ์** | การเข้ารหัสของคอนโซลไม่รองรับอักขระมีสำเนียง. | ใช้ `print(page["text"].encode('utf-8').decode('utf-8'))` หรือกำหนดค่าคอนโซลของคุณให้เป็น UTF‑8. |

---

## การขยายสคริปต์: จาก **ดึงข้อความจาก TIFF** ไปสู่การประมวลผลแบบกลุ่ม

เมื่อคุณมีพื้นฐานที่มั่นคงแล้ว, พิจารณาขั้นตอนต่อไปนี้:

1. **การแปลงเป็นกลุ่ม** – ห่อกระบวนการทั้งหมดในฟังก์ชัน `def ocr_tiff(path):` และวนลูปผ่านไดเรกทอรีของไฟล์ TIFF
2. **ส่งออกเป็นไฟล์** – แทนการพิมพ์, เขียนข้อความของแต่ละหน้าไปยัง `page_{i}.txt` หรือรวมทั้งหมดเป็นเอกสารเดียว
3. **เครื่องมือ OCR ทางเลือก** – หากต้องการความแม่นยำสูงขึ้น, เปลี่ยน `ocr.OcrEngine()` เป็น Tesseract (`pytesseract`) หรือ Azure Cognitive Services—เพียงรักษาตรรกะ “ดึงข้อความจาก TIFF” เดิม
4. **การประมวลผลต่อ** – รันการตรวจสอบการสะกด, การตรวจจับภาษา, หรือทำความสะอาดด้วย regex เพื่อทำให้ผลลัพธ์ OCR ดิบเป็นระเบียบ

---

## สคริปต์เต็มพร้อมรัน

ด้านล่างเป็นโค้ดเต็มพร้อมคัดลอกและวาง. มีการจัดการข้อผิดพลาดพื้นฐานและบันทึกข้อความของแต่ละหน้าเป็นไฟล์แยกตามต้องการ

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

รันสคริปต์นี้, ชี้ `tiff_file` ไปที่เอกสารของคุณ, แล้วดูคอนโซลเต็มไปด้วยประโยคภาษาฝรั่งเศสที่สะอาด. หากคุณระบุ `out_folder`, คุณจะพบชุดไฟล์ `page_#.txt` พร้อมสำหรับการประมวลผลต่อไป

---

## สรุป

เราเพิ่ง **ดึงข้อความจากไฟล์ TIFF** ด้วยกระบวนการ OCR ของ Python ที่ง่ายดาย, และตอนนี้คุณรู้วิธี **แปลง TIFF เป็นข้อความ** อย่างเชื่อถือได้. ตั้งค่า engine ด้วยภาษาที่ถูกต้องจนถึงการวนลูปผ่านผลลัพธ์ JSON ของแต่ละหน้า, ทุกขั้นตอนอธิบายพร้อมเหตุผล, เพื่อให้คุณปรับใช้กับภาษาอื่น, รูปแบบภาพอื่น, หรือการทำงานเป็นกลุ่มขนาดใหญ่

ต่อไปคืออะไร? ลองเปลี่ยน backend OCR เป็น Tesseract, ทดลองกับแพ็คภาษาอื่น, หรือรวมผลลัพธ์เข้าสู่ฐานข้อมูลที่ค้นหาได้. ไม่มีขีดจำกัดเมื่อคุณสามารถแปลงภาพสแกนเป็นข้อความที่ค้นหาได้อย่างเชื่อถือ

อย่าลังเลที่จะคอมเมนต์หากเจอปัญหาหรือมีไอเดียสำหรับการปรับปรุงเพิ่มเติม. โค้ดให้สนุก!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคในคู่มือนี้. แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ

- [ดึงข้อความจากภาพด้วย Aspose OCR – คู่มือขั้นตอน](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [ดึงข้อความจากภาพโดยใช้การดำเนินการ OCR บนโฟลเดอร์](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [แปลงภาพเป็นข้อความ – ทำ OCR บนภาพจาก URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}