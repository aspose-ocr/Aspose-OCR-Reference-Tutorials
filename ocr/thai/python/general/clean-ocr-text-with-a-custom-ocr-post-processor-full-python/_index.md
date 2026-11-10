---
category: general
date: 2026-06-22
description: เรียนรู้วิธีทำความสะอาดข้อความ OCR ด้วยตัวประมวลผลหลัง OCR ใน Python
  โค้ดแบบขั้นตอนต่อขั้นตอน คำอธิบาย และเคล็ดลับเพื่อให้ได้ผลลัพธ์ JSON ที่มีโครงสร้างเชื่อถือได้
draft: false
keywords:
- clean OCR text
- OCR post processor
- Python OCR workflow
- structured JSON OCR
- OCR confidence averaging
language: th
og_description: ทำความสะอาดข้อความ OCR ทันทีโดยเพิ่มตัวประมวลผลหลัง OCR คู่มือนี้แสดงการทำงานของ
  Python อย่างครบถ้วน เหตุผลที่ทำงานได้และวิธีปรับใช้
og_title: ทำความสะอาดข้อความ OCR ด้วยตัวประมวลผลหลัง OCR แบบกำหนดเอง – บทเรียน Python
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to clean OCR text using an OCR post processor in Python.
    Step‑by‑step code, explanations, and tips for reliable structured JSON output.
  headline: Clean OCR Text with a Custom OCR Post Processor – Full Python Guide
  type: TechArticle
tags:
- OCR
- Python
- post‑processing
title: ทำความสะอาดข้อความ OCR ด้วยตัวประมวลผลหลัง OCR แบบกำหนดเอง – คู่มือ Python
  ฉบับเต็ม
url: /th/python/general/clean-ocr-text-with-a-custom-ocr-post-processor-full-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำความสะอาดข้อความ OCR ด้วยตัวประมวลผลหลัง OCR แบบกำหนดเอง – คู่มือ Python ฉบับเต็ม

เคยต้องการ **clean OCR text** แต่ผลลัพธ์ดิบกลับมีปัญหาเรื่องการขึ้นบรรทัดใหม่, ช่องว่างเกิน, และอักขระที่ความเชื่อมั่นต่ำหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลาย ๆ pipeline ของโลกจริง เครื่อง OCR จะให้คุณเป็นข้อความก้อนเดียวพร้อมคะแนนความเชื่อมั่น, แล้วคุณต้องหาวิธีแปลงให้เป็นประโยชน์  

ข่าวดีคือ? **OCR post processor** ขนาดเล็กสามารถทำให้ผลลัพธ์เรียบร้อยขึ้น, คำนวณค่า confidence เฉลี่ย, และแม้กระทั่งบรรจุทุกอย่างเป็นสตริง JSON ที่เรียบร้อย—โดยไม่ต้องแก้ไขเอนจินหลักเลย ในบทแนะนำนี้เราจะสร้าง post‑processor นั้น, ลงทะเบียนกับ AI/OCR engine ทั่วไป, และอธิบายโค้ดทุกบรรทัดเพื่อให้คุณสามารถนำไปใช้ในโปรเจคของคุณได้ทันที

---

## สิ่งที่บทแนะนำนี้ครอบคลุม

- วิธีสร้าง **clean OCR text** post‑processor ที่ทำให้ช่องว่างเป็นมาตรฐานและลบการขึ้นบรรทัดใหม่  
- ทำไมการคำนวณ **average confidence** ถึงมีคุณค่าสำหรับการตรวจสอบต่อไป  
- การลงทะเบียน processor กับ OCR engine (รูปแบบ `ai.set_post_processor`)  
- การแสดง JSON โครงสร้างที่ได้และการแก้ไขปัญหา edge case ที่พบบ่อย  

ไม่ต้องใช้ไลบรารีภายนอกนอกจาก Python standard library, ดังนั้นคุณสามารถทำตามได้บนระบบใดก็ได้ที่รัน Python 3.8+

## ข้อกำหนดเบื้องต้น

- OCR engine ที่ทำงานได้และเปิดเผยอ็อบเจ็กต์ `ocr_result` ที่มี `text`, `confidence` (รายการของ float), และ `bounding_boxes`  
- ความคุ้นเคยพื้นฐานกับฟังก์ชัน Python และการจัดการ JSON  
- ตัวเลือก: สภาพแวดล้อมเสมือน (virtual environment) เพื่อจัดการ dependencies ให้เป็นระเบียบ  

หากคุณไม่แน่ใจว่า engine ของคุณรองรับ custom post‑processor หรือไม่, ตรวจสอบเอกสารของมันสำหรับเมธอด `set_post_processor`—ส่วนใหญ่ของ AI‑powered OCR SDK สมัยใหม่รองรับ

## ขั้นตอนที่ 1: กำหนด OCR Post Processor ที่ **Clean OCR Text**

แรกเริ่ม เราจะเขียนฟังก์ชันที่รับผลลัพธ์ OCR ดิบ, ทำความสะอาดข้อความ, คำนวณเมตริกความเชื่อมั่น, และคืนสตริง JSON. สังเกตว่าการดำเนินการแต่ละขั้นตอนมีคอมเมนต์อธิบายอย่างตั้งใจ; คอมเมนต์เหล่านี้คือ “เหตุผล” ที่ผู้ช่วย AI ชอบอ้างอิง

```python
import json

def create_structured_json(ocr_result, **kwargs):
    """
    Turn an OCR result into a clean, structured JSON payload.

    Parameters
    ----------
    ocr_result : object
        Must expose .text (raw string), .confidence (list of floats),
        and .bounding_boxes (list of box coordinates).

    Returns
    -------
    str
        JSON string with cleaned text, average confidence, and bounding boxes.
    """
    # 1️⃣ Clean the raw text: replace newlines with spaces and trim excess whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # 2️⃣ Compute the average confidence – useful for quality gating.
    # Guard against division by zero if the engine returns an empty list.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0  # fallback when confidence data is missing

    # 3️⃣ Preserve the original bounding boxes for downstream layout analysis.
    boxes = ocr_result.bounding_boxes

    # 4️⃣ Assemble the dictionary and dump it as a JSON string.
    data = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }

    # ensure_ascii=False keeps Unicode characters intact (think accented letters, emojis, etc.)
    return json.dumps(data, ensure_ascii=False)
```

**ทำไมวิธีนี้ถึงได้ผล:**  
- `replace("\n", " ")` แปลงผลลัพธ์ OCR หลายบรรทัดให้เป็นสตริงเดียวที่สามารถค้นหาได้—ตรงกับความหมายของ “clean OCR text” ใน pipeline ส่วนใหญ่  
- การลบช่องว่างที่ต้นและท้ายช่วยหลีกเลี่ยง token ว่างเปล่าที่อาจทำให้ tokenizer พังในภายหลัง  
- การคำนวณ average confidence ให้เมตริกคุณภาพเดียว; คุณสามารถปฏิเสธผลลัพธ์ที่ต่ำกว่าค่าเกณฑ์ (เช่น 0.85) ก่อนบันทึกลงฐานข้อมูล  
- การไม่แก้ไข bounding boxes ทำให้คุณยังคงสามารถแสดงเลย์เอาต์เดิมได้ หากต้องการไฮไลท์พื้นที่ที่ confidence ต่ำ  

## ขั้นตอนที่ 2: ลงทะเบียน **OCR Post Processor** แบบกำหนดเองกับ Engine ของคุณ

ส่วนใหญ่ของ AI‑powered OCR SDK จะเปิดเผยเมธอดเพื่อเชื่อมต่อ callback ของ post‑processing. ด้านล่างเราจะสมมติว่าอ็อบเจ็กต์ชื่อ `ai` (engine) มี `set_post_processor`. หากไลบรารีของคุณใช้ชื่ออื่น, ให้แทนที่ตามนั้น

```python
# Register the post‑processor; the second argument can hold custom settings.
ai.set_post_processor(create_structured_json, custom_settings={})
```

**เคล็ดลับ:** ส่งค่าการตั้งค่าผ่าน `custom_settings` หากคุณต้องการสลับพฤติกรรม (เช่น เปิด/ปิดการลบ newline). วิธีนี้ทำให้ processor ใช้ซ้ำได้ในหลายโปรเจค

## ขั้นตอนที่ 3: รัน OCR Engine – ผลลัพธ์ตอนนี้เป็นสตริง JSON

เมื่อเชื่อมต่อ post‑processor แล้ว, การเรียก `engine.recognize()` (หรือเมธอดที่ SDK ของคุณใช้) จะเรียก `create_structured_json` โดยอัตโนมัติ. Engine จะคืนอ็อบเจ็กต์ที่มีแอตทริบิวต์ `.text` ที่มี payload JSON อยู่แล้ว

```python
# The engine runs OCR, then our post‑processor formats the output.
structured_result = engine.recognize()
```

> **หมายเหตุ:** SDK บางตัวอาจคืนสตริงธรรมดาแทนอ็อบเจ็กต์ที่มีแอตทริบิวต์ `.text`. ปรับขั้นตอนต่อไปให้เหมาะสม

## ขั้นตอนที่ 4: แสดง (หรือบันทึก) ผลลัพธ์ JSON โครงสร้าง

สุดท้าย เราจะพิมพ์ JSON ไปที่คอนโซล. ในสภาพแวดล้อมการผลิตคุณอาจเขียนลงไฟล์, คิวข้อความ, หรือฐานข้อมูล

```python
# Show the clean OCR text and additional metadata.
print("Structured JSON:", structured_result.text)
```

**ผลลัพธ์คอนโซลที่คาดหวัง** (จัดรูปแบบเพื่อความอ่านง่าย):

```json
{
  "clean_text": "The quick brown fox jumps over the lazy dog.",
  "average_confidence": 0.9375,
  "boxes": [
    [0, 0, 120, 30],
    [0, 35, 115, 30],
    ...
  ]
}
```

หากคุณเห็นอักขระ newline เกินหรือ confidence เป็น `0.0`, ตรวจสอบว่า OCR engine ของคุณได้เติมค่า `ocr_result.confidence` จริงหรือไม่. เงื่อนไขป้องกันใน post‑processor จะป้องกัน `ZeroDivisionError`, แต่คุณยังต้องการทราบว่าข้อมูล confidence หายไปทำไม

## การจัดการ Edge Cases ที่พบบ่อย

| สถานการณ์ | สิ่งที่ควรระวัง | วิธีแก้เร็ว |
|-----------|-------------------|-----------|
| **ผล OCR ว่าง** | `ocr_result.text` คือ `""` และรายการ `confidence` ว่าง | Processor จะคืนค่า `clean_text` ว่างและ `average_confidence` = 0.0 อยู่แล้ว. คุณสามารถเพิ่มเงื่อนไข early‑return หากต้องการข้ามการสร้าง JSON ทั้งหมด |
| **อักขระที่ไม่ใช่ ASCII** | Unicode จะถูก escape (`\u00e9`) | ใช้ `ensure_ascii=False` (มีในโค้ดแล้ว) เพื่อให้ตัวอักษรเช่น “é” อ่านได้ |
| **เอกสารที่ยาวมาก** | ขนาด JSON อาจเกินขีดจำกัดของ API | พิจารณา stream ผลลัพธ์หรือเขียนลงไฟล์แทนการคืนสตริงเดียว |
| **Bounding boxes หาย** | บาง OCR engine ไม่ได้ให้ข้อมูล layout | ตั้งค่า `boxes` เป็น `None` หรือรายการว่าง; ผู้ใช้ต่อไปควรจัดการกับการไม่มีข้อมูลอย่างราบรื่น |

## เคล็ดลับระดับมืออาชีพ & แนวทางปฏิบัติที่ดีที่สุด

- **Batch processing:** หากคุณต้อง OCR หลายร้อยหน้า, ให้ใส่การเรียกการจดจำในลูปและเก็บ JSON payload แต่ละอันในรายการ. จากนั้นบันทึกรายการทั้งหมดลงไฟล์เดียวเพื่อการวิเคราะห์แบบ batch ที่ง่ายขึ้น.  
- **Confidence thresholds:** ก่อนบันทึก, ตรวจสอบ `average_confidence`. กฎโดยประมาณ: ปฏิเสธผลลัพธ์ที่ต่ำกว่า `0.80` สำหรับงานการป้อนข้อมูลที่สำคัญ.  
- **Logging instead of printing:** ในการผลิต, แทนที่ `print()` ด้วย logger ที่มีโครงสร้าง (`logging.info(...)`) เพื่อให้คุณสามารถติดตามว่าภาพใดให้ผลลัพธ์ confidence ต่ำ.  
- **Testing:** เขียน unit test ที่ส่ง mock `ocr_result` พร้อมข้อความและค่าความเชื่อมั่นที่รู้จัก, แล้วตรวจสอบว่าโครงสร้าง JSON ตรงตามคาดหวัง  

## ตัวอย่างทำงานเต็ม (รวมทุกขั้นตอน)

ด้านล่างเป็นสคริปต์เต็มที่คุณสามารถคัดลอก‑วางลงในไฟล์ชื่อ `ocr_cleanup.py`. อย่าลืมแทนที่อ็อบเจ็กต์ placeholder `engine` และ `ai` ด้วยอินสแตนซ์จริงจาก OCR SDK ของคุณ

```python
import json

# ----------------------------------------------------------------------
# Step 1: Define the post‑processor that cleans OCR text and builds JSON.
# ----------------------------------------------------------------------
def create_structured_json(ocr_result, **kwargs):
    """
    Convert raw OCR output into a clean JSON string.
    """
    # Clean the raw text: collapse newlines, trim whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # Safely compute average confidence.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0

    # Keep bounding boxes for layout work.
    boxes = ocr_result.bounding_boxes

    payload = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }
    return json.dumps(payload, ensure_ascii=False)

# ----------------------------------------------------------------------
# Step 2: Register the post‑processor with the OCR engine.
# ----------------------------------------------------------------------
# Replace `ai` with your actual engine/controller instance.
ai.set_post_processor(create_structured_json, custom_settings={})

# ----------------------------------------------------------------------
# Step 3: Run OCR – the result is automatically transformed.
# ----------------------------------------------------------------------
structured_result = engine.recognize()

# ----------------------------------------------------------------------
# Step 4: Output the structured JSON.
# ----------------------------------------------------------------------
print("Structured JSON:", structured_result.text)
```

บันทึกไฟล์, รัน `python ocr_cleanup.py`, และคุณควรเห็นสตริง JSON ที่จัดรูปแบบอย่างสวยงามซึ่งประกอบด้วย **clean OCR text**, คะแนน confidence เฉลี่ย, และ bounding boxes ดั้งเดิม.

## สรุป

ตอนนี้คุณมีวิธีที่ครบถ้วนและพร้อมใช้งานในระดับ production เพื่อ **clean OCR text** ด้วย **OCR post processor** แบบกำหนดเองใน Python. โซลูชันทำให้ช่องว่างเป็นมาตรฐาน, ป้องกันข้อมูล confidence ที่หายไป, และคืน payload JSON ที่อธิบายตัวเองซึ่งบริการต่อไปสามารถใช้ได้โดยไม่ต้องแยกวิเคราะห์เพิ่มเติม  

ต่อจากนี้คุณอาจ:

- ขยาย processor เพื่อ **กรองคำที่ confidence ต่ำ** ก่อนสร้าง `clean_text`.  
- เพิ่ม **การตรวจจับภาษา** เพื่อส่ง JSON ไปยัง pipeline ที่กำหนดตาม locale  
- รวม post‑processor นี้กับไลบรารี **spell‑checking** เพื่อเพิ่มชั้นคุณภาพเพิ่มเติม  

คุณสามารถปรับโค้ด, ทดลองค่า confidence thresholds ต่าง ๆ, หรือแบ่งปันการปรับปรุงของคุณในคอมเมนต์ได้เลย. ขอให้เขียนโค้ดสนุก!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจคของคุณ

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}