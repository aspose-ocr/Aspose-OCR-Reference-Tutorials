---
category: general
date: 2026-04-26
description: วิธีทำหลังการประมวลผลผลลัพธ์ OCR และดึงข้อความพร้อมพิกัด เรียนรู้วิธีแก้ปัญหาแบบขั้นตอนโดยใช้ผลลัพธ์เชิงโครงสร้างและการแก้ไขด้วย
  AI.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: th
og_description: วิธีการประมวลผลผลลัพธ์ OCR หลังการสแกนและสกัดข้อความพร้อมพิกัด ปฏิบัติตามบทเรียนเชิงลึกนี้เพื่อกระบวนการทำงานที่เชื่อถือได้
og_title: วิธีการประมวลผลต่อ OCR – คู่มือครบถ้วน
tags:
- OCR
- Python
- AI
- Text Extraction
title: วิธีการประมวลผลต่อ OCR – ดึงข้อความพร้อมพิกัดด้วย Python
url: /th/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการประมวลผลต่อ OCR – ดึงข้อความพร้อมพิกัดใน Python

เคยต้องการ **how to post‑process OCR** ผลลัพธ์หรือไม่ เพราะผลลัพธ์ดิบเต็มไปด้วยเสียงรบกวนหรือจัดตำแหน่งไม่ตรง? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง—การสแกนใบแจ้งหนี้, การแปลงใบเสร็จเป็นดิจิทัล, หรือแม้กระทั่งการเสริมประสบการณ์ AR—เครื่อง OCR จะให้คำศัพท์ดิบแก่คุณ แต่คุณยังต้องทำความสะอาดและติดตามตำแหน่งของแต่ละคำบนหน้า นั่นคือจุดที่โหมดผลลัพธ์แบบโครงสร้างร่วมกับตัวประมวลผลหลังที่ขับเคลื่อนด้วย AI จะโดดเด่น

ในบทแนะนำนี้ เราจะพาไปผ่าน pipeline Python ที่สมบูรณ์และสามารถรันได้ ซึ่ง **extracts text with coordinates** จากภาพ, รันขั้นตอนการแก้ไขด้วย AI, และพิมพ์แต่ละคำพร้อมตำแหน่ง (x, y) ของมัน ไม่มีการนำเข้าโค้ดที่ขาดหาย ไม่มีทางลัดแบบ “ดูเอกสาร” ที่คลุมเครือ—เพียงโซลูชันที่เป็นอิสระที่คุณสามารถนำไปใช้ในโปรเจกต์ของคุณได้ทันที

> **เคล็ดลับ:** หากคุณใช้ไลบรารี OCR ที่แตกต่างกัน ให้มองหาโหมด “structured” หรือ “layout”; แนวคิดยังคงเหมือนเดิม.

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มลงลึก ตรวจสอบให้แน่ใจว่าคุณมี:

| ความต้องการ | เหตุผลที่สำคัญ |
|-------------|----------------|
| Python 3.9+ | ไวยากรณ์สมัยใหม่และ type hints |
| `ocr` library that supports `OutputMode.STRUCTURED` (e.g., a fictional `myocr`) | จำเป็นสำหรับข้อมูล bounding‑box |
| An AI post‑processing module (could be OpenAI, HuggingFace, or a custom model) | ปรับปรุงความแม่นยำหลัง OCR |
| An image file (`input.png`) in your working directory | แหล่งที่เราจะอ่าน |

หากส่วนใดส่วนหนึ่งฟังดูแปลกใหม่ เพียงติดตั้งแพคเกจจำลองด้วย `pip install myocr ai‑postproc`. โค้ดด้านล่างยังรวม stub สำรองเพื่อให้คุณทดสอบการทำงานโดยไม่ต้องใช้ไลบรารีจริง

## ขั้นตอนที่ 1: เปิดใช้งานโหมด Structured Output สำหรับ OCR Engine  

สิ่งแรกที่เราทำคือบอกให้ OCR engine ให้ข้อมูลมากกว่าข้อความธรรมดา Structured output จะคืนค่าคำแต่ละคำพร้อมกับ bounding box และคะแนนความมั่นใจ ซึ่งเป็นสิ่งจำเป็นสำหรับ **extract text with coordinates** ในภายหลัง.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*ทำไมสิ่งนี้ถึงสำคัญ:* หากไม่ได้เปิดโหมด structured คุณจะได้เพียงสตริงยาว ๆ และจะสูญเสียข้อมูลเชิงพื้นที่ที่จำเป็นสำหรับการวางข้อความบนภาพหรือการวิเคราะห์ layout ต่อไป

## ขั้นตอนที่ 2: จดจำภาพและจับคำ, กล่อง, และความมั่นใจ  

ตอนนี้เราจะส่งภาพเข้า engine ผลลัพธ์เป็นอ็อบเจกต์ที่มีรายการของอ็อบเจกต์คำแต่ละตัว ซึ่งแต่ละอ็อบเจกต์จะเปิดเผย `text`, `x`, `y`, `width`, `height`, และ `confidence`.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*กรณีขอบ:* หากภาพว่างหรืออ่านไม่ออก `structured_result.words` จะเป็นรายการว่าง ควรตรวจสอบและจัดการอย่างราบรื่น

## ขั้นตอนที่ 3: รัน AI‑Based Post‑Processing พร้อมรักษาตำแหน่ง  

แม้ OCR engine ที่ดีที่สุดก็อาจทำผิดพลาด—เช่น “O” กับ “0” หรือการขาด diacritics โมเดล AI ที่ฝึกบนข้อความเฉพาะโดเมนสามารถแก้ไขข้อผิดพลาดเหล่านี้ได้ อย่างสำคัญ เราจะรักษาพิกัดเดิมไว้เพื่อให้ layout เชิงพื้นที่คงที่

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*ทำไมเราถึงรักษาพิกัด:* งานต่อไปหลายอย่าง (เช่น การสร้าง PDF, การติดป้าย AR) พึ่งพาการวางตำแหน่งที่แม่นยำ AI จะทำการแก้ไขเฉพาะฟิลด์ `text` เท่านั้น ไม่กระทบ `x`, `y`, `width`, `height`

## ขั้นตอนที่ 4: วนลูปผ่านคำที่แก้ไขและแสดงข้อความพร้อมพิกัด  

สุดท้าย เราจะวนลูปผ่านคำที่แก้ไขและพิมพ์แต่ละคำพร้อมมุมบน‑ซ้าย `(x, y)` ของมัน ซึ่งสอดคล้องกับเป้าหมาย **extract text with coordinates**.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

แต่ละบรรทัดจะแสดงคำที่แก้ไขและตำแหน่งที่แน่นอนบนภาพต้นฉบับ

## ตัวอย่างการทำงานเต็มรูปแบบ  

ด้านล่างเป็นสคริปต์เดียวที่เชื่อมทุกขั้นตอนเข้าด้วยกัน คุณสามารถคัดลอก‑วาง ปรับคำสั่ง import ให้ตรงกับไลบรารีของคุณ และรันได้โดยตรง

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**การรันสคริปต์**

```bash
python ocr_postprocess_demo.py
```

หากคุณติดตั้งไลบรารีจริงสคริปต์จะประมวลผล `input.png` ของคุณ มิฉะนั้น การทำงานแบบ stub จะทำให้คุณเห็นกระบวนการและผลลัพธ์ที่คาดหวังโดยไม่มีการพึ่งพาไลบรารีภายนอก

## คำถามที่พบบ่อย (FAQ)

| คำถาม | คำตอบ |
|----------|--------|
| *ทำงานกับ Tesseract ได้หรือไม่?* | Tesseract เองไม่ได้เปิดโหมด structured โดยตรง แต่ wrapper อย่าง `pytesseract.image_to_data` จะคืนค่า bounding boxes ที่คุณสามารถส่งต่อไปยัง AI post‑processor เดียวกันได้. |
| *ถ้าต้องการมุมล่าง‑ขวาแทนมุมบน‑ซ้ายจะทำอย่างไร?* | แต่ละวัตถุคำยังให้ค่า `width` และ `height` ด้วย คำนวณ `x2 = x + width` และ `y2 = y + height` เพื่อให้ได้มุมตรงข้าม. |
| *ฉันสามารถประมวลผลหลายภาพเป็นชุดได้หรือไม่?* | ได้เลย. ห่อขั้นตอนทั้งหมดในลูป `for image_path in Path("folder").glob("*.png"):` แล้วเก็บผลลัพธ์ต่อไฟล์. |
| *ฉันจะเลือกโมเดล AI สำหรับการแก้ไขอย่างไร?* | สำหรับข้อความทั่วไป โมเดล GPT‑2 ขนาดเล็กที่ฝึกต่อบนข้อผิดพลาดของ OCR จะทำงานได้ สำหรับข้อมูลเฉพาะโดเมน (เช่น ใบสั่งยา) ให้ฝึกโมเดล sequence‑to‑sequence บนข้อมูลคู่ noisy‑clean. |
| *คะแนนความมั่นใจมีประโยชน์หลังการแก้ไขด้วย AI หรือไม่?* | คุณยังสามารถเก็บคะแนนความมั่นใจเดิมไว้เพื่อการดีบักได้ แต่ AI อาจให้คะแนนความมั่นใจของมันเองหากโมเดลรองรับ. |

## กรณีขอบและแนวทางปฏิบัติที่ดีที่สุด  

1. **ภาพที่ว่างหรือเสียหาย** – ตรวจสอบเสมอว่า `structured_result.words` ไม่เป็นรายการว่างก่อนดำเนินการต่อ.  
2. **สคริปต์ที่ไม่ใช่ละติน** – ตรวจสอบว่า OCR engine ของคุณตั้งค่าตามภาษาที่ต้องการ; AI post‑processor ต้องได้รับการฝึกบนสคริปต์เดียวกัน.  
3. **ประสิทธิภาพ** – การแก้ไขด้วย AI อาจมีค่าใช้จ่ายสูง. แคชผลลัพธ์หากคุณจะใช้ภาพเดียวกันซ้ำ, หรือรันขั้นตอน AI แบบอะซิงโครนัส.  
4. **ระบบพิกัด** – ไลบรารี OCR อาจใช้จุดเริ่มต้นที่ต่างกัน (บน‑ซ้าย vs. ล่าง‑ซ้าย). ปรับให้เหมาะสมเมื่อวางทับบน PDF หรือ canvas.  

## สรุป  

คุณมีสูตรครบวงจรสำหรับ **how to post‑process OCR** และ **extract text with coordinates** อย่างมั่นคงแล้ว ด้วยการเปิดใช้งาน structured output, ส่งผลลัพธ์ผ่านชั้นการแก้ไขด้วย AI, และรักษา bounding box ดั้งเดิม คุณสามารถเปลี่ยนสแกน OCR ที่มีเสียงรบกวนให้เป็นข้อความที่สะอาดและรับรู้เชิงพื้นที่ พร้อมใช้งานในงานต่อไปเช่น การสร้าง PDF, การอัตโนมัติการป้อนข้อมูล, หรือการวางข้อความเสริมในความเป็นจริงเสมือน

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองเปลี่ยน stub AI เป็นการเรียก OpenAI `gpt‑4o‑mini`, หรือรวม pipeline นี้เข้ากับ FastAPI

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}