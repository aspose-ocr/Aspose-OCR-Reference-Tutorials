---
category: general
date: 2026-03-18
description: แก้ไขข้อผิดพลาด OCR ใน Python อย่างรวดเร็ว เรียนรู้วิธีทำความสะอาด OCR,
  วิธีทำความสะอาดข้อความ OCR, แทนที่เลขศูนย์ด้วยตัวอักษร O, และประยุกต์การประมวลผลหลัง
  OCR ด้วย Python
draft: false
keywords:
- fix OCR errors
- how to clean OCR
- clean OCR text python
- replace zero with O
- python OCR post processing
language: th
og_description: แก้ไขข้อผิดพลาด OCR ใน Python อย่างรวดเร็ว เรียนรู้วิธีทำความสะอาด
  OCR, แทนที่ศูนย์ด้วย O, และใช้การประมวลผลหลัง OCR ด้วย Python ในบทเรียนเดียว
og_title: แก้ไขข้อผิดพลาด OCR ใน Python – คู่มือทำความสะอาดข้อความ OCR
tags:
- OCR
- Python
- Text Cleaning
title: แก้ไขข้อผิดพลาด OCR ใน Python – คู่มือทำความสะอาดข้อความ OCR
url: /th/python/general/fix-ocr-errors-in-python-clean-ocr-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แก้ไขข้อผิดพลาด OCR ใน Python – คู่มือทำความสะอาดข้อความ OCR

เคยจ้องมองใบแจ้งหนี้สแกนแล้วคิดว่า, *“ฉันจะแก้ไขข้อผิดพลาด OCR อย่างไรก่อนจะใส่ลงในฐานข้อมูล?”* คุณไม่ได้เป็นคนเดียว ในโลกของการอัตโนมัติเอกสาร ตัวอักษรที่อ่านผิดเพียงหนึ่งตัวอาจทำให้ทั้ง pipeline พังได้ ดังนั้นการเรียนรู้ **วิธีทำความสะอาด OCR** output จึงเป็นสิ่งสำคัญ.  

ในบทแนะนำนี้คุณจะได้เห็นวิธีการเชิงปฏิบัติแบบ end‑to‑end เพื่อ **แก้ไขข้อผิดพลาด OCR** โดยใช้ post‑processor เล็ก ๆ ที่แทนที่ตัวเลข “0” ด้วยตัวอักษร “O”—ข้อผิดพลาดทั่วไปในรหัสสินค้า เมื่อเสร็จสิ้นคุณจะสามารถนำโซลูชันนี้ไปใส่ใน workflow OCR ของ Python ใดก็ได้และได้ข้อความที่สะอาดและเชื่อถือได้มากขึ้น.

> **สิ่งที่คุณจะได้รับ:** สคริปต์ Python ที่สมบูรณ์และสามารถรันได้, คำอธิบายว่าทำไมแต่ละบรรทัดจึงสำคัญ, เคล็ดลับในการขยายตรรกะ, และการตรวจสอบความสมเหตุสมผลอย่างรวดเร็วของผลลัพธ์ที่คาดหวัง.

## ข้อกำหนดเบื้องต้น — สิ่งที่คุณต้องมีก่อนเริ่ม

- Python 3.8 หรือใหม่กว่า (syntax ทำงานบนทุกเวอร์ชันล่าสุด)  
- ไลบรารี OCR เบื้องต้น (เช่น Tesseract ผ่าน `pytesseract`) ที่คืนค่าเป็นสตริงดิบ  
- ความคุ้นเคยพื้นฐานกับฟังก์ชันและอ็อบเจกต์ใน Python  

หากคุณมีขั้นตอน OCR ที่ให้ผลลัพธ์เป็นสตริงอยู่แล้ว คุณก็พร้อมใช้งาน—ไม่ต้องติดตั้งเพิ่มเติมสำหรับส่วน post‑processing.

## ขั้นตอนที่ 1: ตั้งค่า Wrapper แบบ AI‑like ขั้นต่ำ (ทำไมเราต้องการมัน)

ในหลายโครงการเครื่อง OCR จะอยู่ภายในคลาส “AI” ขนาดใหญ่ที่จัดการ preprocessing, inference, และ post‑processing เพื่อให้ตัวอย่างเป็นอิสระ เราจะสร้างคลาส `AIProcessor` เล็ก ๆ ที่เลียนแบบรูปแบบนี้ ทำให้สามารถนำโค้ดไปใส่ใน code‑base ที่มีอยู่ได้โดยไม่ต้องเขียนใหม่.

```python
# ai_wrapper.py
class AIProcessor:
    """
    Simple wrapper that stores a post‑processing callable.
    In real projects this could be a full‑fledged model class.
    """
    def __init__(self):
        self._post_processor = None

    def set_post_processor(self, func):
        """Register a function that will clean OCR output."""
        if not callable(func):
            raise TypeError("Post‑processor must be callable")
        self._post_processor = func

    def run_postprocessor(self, text):
        """Apply the registered post‑processor to raw OCR text."""
        if self._post_processor is None:
            raise RuntimeError("No post‑processor has been set")
        return self._post_processor(text)
```

**ทำไมเรื่องนี้สำคัญ:** การแยก post‑processor ออกจากเครื่อง OCR สอดคล้องกับหลักการ single‑responsibility และทำให้คุณสามารถสลับตรรกะการทำความสะอาดได้โดยไม่ต้องแก้ไขโค้ด OCR.

## ขั้นตอนที่ 2: เขียนฟังก์ชันที่ **แก้ไขข้อผิดพลาด OCR**

ตอนนี้เราจะสร้างหัวใจของบทแนะนำ: ฟังก์ชันที่ **แก้ไขข้อผิดพลาด OCR** โดยสลับตัวเลข “0” กับตัวอักษร “O”. รูปแบบนี้ครอบคลุมรหัสสินค้า, หมายเลขซีเรียล, และตัวระบุอัลฟานูเมอริกใด ๆ ที่เครื่อง OCR มักสับสนระหว่างสองอักษรนี้.

```python
# post_processors.py
def correct_ocr_errors(text: str) -> str:
    """
    Replace common OCR mis‑reads.
    Example: change digit "0" to letter "O" in product codes.
    """
    # You could add more rules here, e.g.:
    # text = text.replace('1', 'I')
    # text = text.replace('5', 'S')
    return text.replace("0", "O")
```

**ทำไมเราถึงแทนที่ 0 ด้วย O:** ในหลายฟอนต์ศูนย์และตัว O ตัวพิมพ์ใหญ่ดูเหมือนกัน ทำให้ OCR มักคาดเดาผิด การแก้ไขตั้งแต่ต้นทำให้การตรวจสอบ downstream (เช่น regex) ทำงานตามที่คาดหวัง.

## ขั้นตอนที่ 3: เชื่อม Post‑Processor เข้ากับอินสแตนซ์ AI

เมื่อ wrapper และฟังก์ชันทำความสะอาดพร้อม เราจะเชื่อมต่อพวกมันเข้าด้วยกัน ซึ่งเป็นการจำลองวิธีที่คุณจะลงทะเบียน custom post‑processor ใน pipeline การผลิต.

```python
# main.py
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Create the AI‑like object
ai = AIProcessor()

# Register our OCR‑fixing function
ai.set_post_processor(correct_ocr_errors)
```

หากคุณต้องการ **วิธีทำความสะอาด OCR** output สำหรับภาษาอื่นหรือรูปแบบข้อมูลอื่น เพียงเขียนฟังก์ชันใหม่และเรียก `set_post_processor` อีกครั้ง—ไม่ต้องแก้ไขส่วนอื่นของ pipeline.

## ขั้นตอนที่ 4: ป้อนข้อความ OCR ดิบและรับผลลัพธ์ที่ทำความสะอาดแล้ว

ให้เราจำลองสตริง OCR ดิบที่มี “0” ที่น่ากลัวในรหัสสินค้า ในสถานการณ์จริงคุณจะเปลี่ยน placeholder ด้วย `pytesseract.image_to_string(image)` หรือการเรียกคล้ายกัน.

```python
# Simulated OCR output (replace with your own OCR call)
raw_text = "Product code: 10A0B"

# Run the post‑processor to obtain cleaned text
cleaned_text = ai.run_postprocessor(raw_text)

print("Before cleaning :", raw_text)
print("After cleaning  :", cleaned_text)
```

**ผลลัพธ์ที่คาดหวัง**

```
Before cleaning : Product code: 10A0B
After cleaning  : Product code: 1OAOB
```

สังเกตว่าเลขศูนย์ได้เปลี่ยนเป็นตัว O ตัวพิมพ์ใหญ่ ทำให้สตริงตรงกับรูปแบบที่คาดหวังสำหรับระบบสินค้าคงคลังส่วนใหญ่.

## ขั้นตอนที่ 5: ขยายตรรกะ – ความแปรผันในโลกจริง

| ความผิดพลาดทั่วไป | ตัวอย่าง OCR | การแก้ไขที่ต้องการ | วิธีเพิ่ม |
|----------------|------------|-------------|------------|
| “1” อ่านเป็น “I” | `I23` | `123` | `text = text.replace('I', '1')` |
| “5” อ่านเป็น “S” | `S9` | `59` | `text = text.replace('S', '5')` |
| ช่องว่างเกิน | `  ABC  ` | `ABC` | `text = text.strip()` |
| ความสับสนระหว่างตัวพิมพ์ใหญ่‑เล็ก | `oRder` | `Order` | `text = text.title()` |

คุณสามารถขยาย `correct_ocr_errors` ด้วยกฎเหล่านี้ได้ เพียงให้การแปลงแต่ละอย่างเป็น **idempotent** (การรันสองครั้งไม่ควรเปลี่ยนผลลัพธ์) เพื่อหลีกเลี่ยงการทำให้ข้อมูลเสียโดยบังเอิญ.

```python
def correct_ocr_errors(text: str) -> str:
    text = text.replace("0", "O")
    text = text.replace("I", "1")
    text = text.replace("S", "5")
    return text.strip()
```

**เคล็ดลับ:** หากคุณมีแคตาล็อกของรหัสที่ถูกต้องอยู่แล้ว ให้พิจารณาตรวจสอบสตริงที่ทำความสะอาดแล้วกับ regex หรือ lookup table ขั้นตอนเพิ่มเติมนี้จะจับข้อผิดพลาด OCR ที่เหลืออยู่ที่การสลับอักขระอย่างง่ายอาจพลาด.

## ขั้นตอนที่ 6: ผสานกับเครื่อง OCR จริง (ทางเลือก)

ด้านล่างเป็นภาพตัวอย่างอย่างรวดเร็วว่าคุณจะเชื่อม post‑processor เข้ากับกระบวนการ OCR จริงโดยใช้ `pytesseract` อย่างไร ส่วนนี้เป็นทางเลือกแต่แสดง pipeline แบบ end‑to‑end.

```python
import pytesseract
from PIL import Image
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Initialize AI wrapper and register the cleaner
ai = AIProcessor()
ai.set_post_processor(correct_ocr_errors)

# Load an image containing a product label
image = Image.open("sample_label.png")

# Perform OCR (this returns raw text)
raw_ocr = pytesseract.image_to_string(image)

# Clean the OCR output
cleaned = ai.run_postprocessor(raw_ocr)

print("Raw OCR   :", raw_ocr)
print("Cleaned   :", cleaned)
```

> **หมายเหตุ:** `pytesseract` ต้องการให้ Tesseract OCR ถูกติดตั้งบนระบบของคุณ ส่วนโค้ดข้างต้นทำงานบน Windows, macOS, และ Linux ตราบใดที่ไฟล์ไบนารีอยู่ใน PATH ของคุณ.

## ขั้นตอนที่ 7: ตรวจสอบผลลัพธ์โดยโปรแกรม

เมื่อคุณทำอัตโนมัติเป็นชุดใหญ่ การตรวจสอบว่าขั้นตอนการทำความสะอาดทำงานตามที่คาดหวังเป็นเรื่องสะดวก การทดสอบหน่วยอย่างรวดเร็วสามารถประหยัดเวลาการดีบักได้หลายชั่วโมงในภายหลัง.

```python
def test_correct_ocr_errors():
    assert correct_ocr_errors("0O0") == "OOO"
    assert correct_ocr_errors(" 10A0B ") == "1OAOB"
    print("All tests passed!")

test_correct_ocr_errors()
```

การรันเทสต์นี้ยืนยันว่าฟังก์ชัน **แก้ไขข้อผิดพลาด OCR** อย่างสม่ำเสมอ แม้เมื่อมีช่องว่างเพิ่มเติมแอบเข้ามา.

## ภาพประกอบ

ด้านล่างเป็นภาพสเก็ตช์ของ pipeline (คีย์เวิร์ดหลักปรากฏในข้อความ alt สำหรับ SEO).

![แผนภาพไหลของการแก้ไขข้อผิดพลาด OCR – แสดง OCR ดิบที่ป้อนเข้าสู่ post‑processor ที่แทนที่ศูนย์ด้วย O]()

## สรุป – สิ่งที่เราบรรลุ

เราได้เดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ซึ่งแสดง **วิธีทำความสะอาด OCR** output ใน Python โดยเฉพาะวิธี **แทนที่ศูนย์ด้วย O** และ **แก้ไขข้อผิดพลาด OCR** ด้วย post‑processor โมดูลาร์ การแยกตรรกะการทำความสะอาดออกจากเครื่อง OCR ทำให้คุณได้ความยืดหยุ่น, ความสามารถในการทดสอบ, และตำแหน่งที่ชัดเจนในการเพิ่มกฎในอนาคต เช่น *วิธีทำความสะอาด OCR* สำหรับการสับสนของอักขระอื่น ๆ  

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองเพิ่มตัวตรวจสอบ regex สำหรับรหัสสินค้า, ทดลองการจับคู่แบบ fuzzy สำหรับข้อความที่มีเสียงรบกวน, หรือสำรวจไลบรารีเต็มรูปแบบอย่าง `ocrmypdf` ที่มี post‑processing hooks อยู่แล้ว รูปแบบที่เราอธิบายสามารถขยายได้ดี ไม่ว่าคุณจะจัดการกับใบแจ้งหนี้ไม่กี่ฉบับหรือเอกสารสแกนเป็นล้านฉบับ  

---

*ขอให้เขียนโค้ดอย่างสนุกสนาน และขอให้ pipeline OCR ของคุณปราศจากข้อผิดพลาด!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}