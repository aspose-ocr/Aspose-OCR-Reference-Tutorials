---
category: general
date: 2026-03-26
description: แปลงภาพเป็นข้อความด้วย Aspose OCR และทำความสะอาดข้อความ OCR ด้วย Python
  เรียนรู้วิธีดึงข้อความจากภาพและประมวลผลต่อในสคริปต์เดียว.
draft: false
keywords:
- convert image to text
- how to extract image text
- clean ocr text python
- Aspose OCR Python
- AI spell‑checker Python
- post‑process OCR output
language: th
og_description: แปลงรูปภาพเป็นข้อความอย่างรวดเร็ว คู่มือนี้แสดงวิธีดึงข้อความจากรูปภาพและทำความสะอาดข้อความ
  OCR แบบสไตล์ Python ด้วย Aspose OCR และตัวตรวจสอบการสะกดด้วย AI.
og_title: แปลงรูปภาพเป็นข้อความด้วย Python – บทเรียนครบถ้วน
tags:
- OCR
- Python
- Aspose
- AI
title: แปลงรูปภาพเป็นข้อความด้วย Python – คู่มือเต็มขั้นตอน
url: /th/python/general/convert-image-to-text-with-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลงรูปภาพเป็นข้อความ – คำแนะนำ Python ฉบับสมบูรณ์

เคยต้อง **convert image to text** แล้วได้ผลลัพธ์ที่ยุ่งยากหรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา OCR ให้ผลลัพธ์เต็มไปด้วยการสะกดผิด สัญลักษณ์แปลก ๆ หรือการตัดบรรทัดที่ไม่ถูกต้อง ข่าวดีคือ ด้วยไม่กี่บรรทัดของ Python และ Aspose OCR คุณสามารถดึงข้อความที่ตรงจากรูปภาพใด ๆ **และ** ทำความสะอาดโดยอัตโนมัติได้

ในคู่มือนี้เราจะสาธิต **วิธีดึงข้อความจากรูปภาพ**, แล้วใช้ AI‑powered spell‑checker เพื่อให้ได้เนื้อหาที่อ่านง่ายและดูเป็นมืออาชีพ เมื่อเสร็จแล้วคุณจะมีสคริปต์เดียวที่รับไฟล์ PNG แล้วสร้างไฟล์ `.txt` ที่สะอาด—ไม่ต้องคัดลอก‑วางด้วยมือ  

> **สิ่งที่คุณจะได้เรียนรู้**  
> * ติดตั้งและตั้งค่า Aspose OCR  
> * แยกข้อความจากไฟล์รูปภาพ  
> * เริ่มต้นโมเดล Aspose AI สำหรับการตรวจสอบการสะกด  
> * ใช้ post‑processor เพื่อทำความสะอาดผลลัพธ์ OCR  
> * บันทึกผลลัพธ์ขั้นสุดท้ายและปล่อยทรัพยากร  

ทั้งหมดนี้ทำงานในสไตล์ **clean OCR text python**—หมายความว่าโค้ดพร้อมนำไปใช้ในโปรเจกต์ใดก็ได้โดยไม่ต้องมี wrapper เพิ่มเติม

---

## ความต้องการเบื้องต้น

ก่อนที่เราจะเริ่ม, โปรดตรวจสอบว่าคุณมี:

| ความต้องการ | เหตุผลที่สำคัญ |
|-------------|----------------|
| Python 3.9 หรือใหม่กว่า | ไวยากรณ์สมัยใหม่ & type hints |
| `asposeocr` package (`pip install asposeocr`) | Core OCR engine |
| การเข้าถึงอินเทอร์เน็ต (ครั้งแรก) | Model auto‑download from Hugging Face |
| ภาพ PNG/JPEG ที่ต้องการอ่าน | Input source |

ไม่จำเป็นต้องมี GPU, แต่หากมี AI model จะใช้โดยอัตโนมัติเพื่อเร่งการตรวจสอบการสะกด

---

## ขั้นตอนที่ 1: แปลงรูปภาพเป็นข้อความด้วย Aspose OCR

สิ่งแรกที่เราต้องการคือ OCR engine ที่เชื่อถือได้ Aspose OCR เป็นไลบรารีเชิงพาณิชย์ แต่มี tier ฟรีที่อุดมใจสำหรับการพัฒนา ด้านล่างเราจะเริ่มต้น engine, ตั้งภาษาเป็น English, และเปิดการแก้ไขการเอียงอัตโนมัติ (auto‑skew) เพื่อจัดการกับสแกนที่เอียง

```python
import asposeocr as ocr

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English   # English language pack
ocr_engine.auto_skew = True                  # Auto‑deskew images
```

> **ทำไมต้องเปิด `auto_skew`?**  
> เอกสารสแกนหลายฉบับไม่ได้อยู่แบนราบอย่างสมบูรณ์ Auto‑skew จะหมุนภาพให้พอเหมาะเพื่อเพิ่มความแม่นยำของการจดจำอักขระ, ซึ่งจะลดจำนวนคำที่อ่านผิดและต้องทำความสะอาดในภายหลัง

ต่อไปเราจะส่งไฟล์รูปภาพให้ engine:

```python
# Recognise text from the input image (replace with your own path)
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR output:")
print(ocr_result.text[:200])  # Show first 200 characters for sanity check
```

คุณสมบัติ `ocr_result.text` จะมีสตริงดิบที่ดึงมาจากรูปภาพ ในขั้นตอนนี้คุณอาจสังเกตเห็นเครื่องหมายวรรคตอนที่แปลก ๆ, การตัดบรรทัดที่ไม่เหมาะ, หรือแม้แต่คำที่สะกดผิด—ปัญหาที่เราตั้งใจจะแก้

![convert image to text workflow](image.png){alt="แผนผังกระบวนการแปลงรูปภาพเป็นข้อความ"}

---

## ขั้นตอนที่ 2: ตั้งค่า AI Spell‑Checker (Clean OCR Text Python)

การทำความสะอาดผลลัพธ์ OCR สามารถทำได้ด้วยการแทนที่ด้วย regex, แต่เพื่อให้ได้ข้อความที่อ่านง่ายจริง ๆ เราจะใช้ Aspose AI พร้อม LLM ขนาดเบาที่เชี่ยวชาญด้านการตรวจสอบการสะกด โมเดลจะถูกดึงจาก Hugging Face ครั้งแรกที่คุณรันสคริปต์, ดังนั้นคุณไม่ต้องดาวน์โหลดอะไรด้วยตนเอง

```python
from asposeocr import AsposeAI, AsposeAIModelConfig

# Model configuration – auto‑download enabled
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30                # Use GPU if available, otherwise CPU fallback
)

# Initialise the AI spell‑checker
spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")
```

**ทำไมเลือกโมเดลนี้?**  
`Qwen2.5‑3B‑Instruct‑GGUF` เป็นโมเดลขนาด 3 พันล้านพารามิเตอร์ที่ปรับแต่งสำหรับคำสั่ง, ทำงานได้อย่างสบายบน GPU ของแล็ปท็อป (หรือแม้แต่ CPU ด้วยการควอนไทซ์ int8). ความเร็วพอเหมาะสำหรับการตรวจสอบการสะกดบรรทัดต่อบรรทัดโดยไม่กินหน่วยความจำมาก

---

## ขั้นตอนที่ 3: ใช้ Spell‑Checking กับผลลัพธ์ OCR

เมื่อเรามีข้อความ OCR และโมเดล AI พร้อม, เราเพียงแค่ส่งสตริงดิบเข้าไปใน post‑processor. เมธอดจะคืนเวอร์ชันที่ทำความสะอาดแล้วซึ่งคุณสามารถเขียนลงไฟล์ได้โดยตรง

```python
# Run the spell‑checking post‑processor
corrected_text = spell_checker.run_postprocessor(ocr_result.text)

print("\nCleaned OCR output (first 200 chars):")
print(corrected_text[:200])
```

การปรับปรุงที่คุณจะเห็นทั่วไป:

* “teh” → “the”  
* “recieve” → “receive”  
* การขาดช่องว่างหลังเครื่องหมายวรรคตอน – แก้โดยอัตโนมัติ  
* การตัดบรรทัดแปลก ๆ ถูกเปลี่ยนเป็นประโยคที่สมบูรณ์  

หากต้องการควบคุมมากขึ้น, คุณสามารถส่ง prompt ที่กำหนดเองไปยัง `run_postprocessor`, แต่ preset “spell_check” ทำงานได้ดีในกรณีส่วนใหญ่

---

## ขั้นตอนที่ 4: บันทึกข้อความที่ทำความสะอาดลงไฟล์

ตอนนี้ข้อความเรียบร้อยแล้ว, เราจะบันทึกลงไฟล์ การใช้ UTF‑8 จะทำให้ตัวอักษรพิเศษ (เช่น ตัวอักษรที่มีสำเนียง) ไม่หายไป

```python
output_path = "YOUR_DIRECTORY/output_text.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\n✅ Processing complete: input_image.png → {output_path}")
```

คุณสามารถเปิดไฟล์นี้ด้วยโปรแกรมแก้ไขใดก็ได้และจะเห็นเอกสารที่มนุษย์อ่านได้พร้อมสำหรับการประมวลผลต่อไป—ไม่ว่าจะเป็นการป้อนให้โมเดลภาษา, การทำดัชนีเพื่อการค้นหา, หรือการเก็บเป็นเอกสาร

---

## ขั้นตอนที่ 5: ปล่อยทรัพยากร AI (การดูแลที่ดี)

Aspose AI จะเก็บน้ำหนักโมเดลไว้ในหน่วยความจำ การปล่อยทรัพยากรเมื่อเสร็จจะช่วยป้องกันการรั่วของหน่วยความจำ, โดยเฉพาะในบริการที่ทำงานต่อเนื่องเป็นเวลานาน

```python
spell_checker.free_resources()
```

เท่านี้! ทั้งกระบวนการ—from image to clean text—อยู่ในโค้ด Python ไม่เกิน 30 บรรทัด

---

## คำถามที่พบบ่อย & กรณีขอบ

### ถ้าภาพไม่ใช่ภาษาอังกฤษ?
ตั้งค่า `ocr_engine.language` ให้เป็น enum ที่เหมาะสม, เช่น `ocr.Language.French`. โมเดลตรวจสอบการสะกดเป็น language‑agnostic สำหรับการสะกดพื้นฐาน, แต่คุณอาจต้องการโมเดลหลายภาษาเพื่อผลลัพธ์ที่ดีที่สุด

### GPU ของฉันมีแค่ 20 layers—ยังใช้โมเดลได้หรือไม่?
ได้เลย. เพียงลด `gpu_layers` เป็น `20` (หรือ `0` สำหรับ CPU อย่างเดียว). ไลบรารีจะสลับไปใช้ CPU สำหรับเลเยอร์ที่เหลือโดยอัตโนมัติ

### การดาวน์โหลดโมเดลล้มเหลวเนื่องจาก proxy ของบริษัท?
ตั้งค่าตัวแปรสภาพแวดล้อม (`HTTP_PROXY`, `HTTPS_PROXY`) ก่อนรันสคริปต์. ขั้นตอนดาวน์โหลดจะเคารพการตั้งค่าเหล่านี้

### ฉันต้องการทำความสะอาดแบบ regex อย่างเร็ว ๆ ไม่ใช้ AI?
คุณสามารถข้ามขั้นตอน AI แล้วใช้การทำความสะอาดแบบง่าย:

```python
import re
clean = re.sub(r'\s+', ' ', ocr_result.text).strip()
```

แต่จำไว้ว่า regex ไม่สามารถแก้คำที่สะกดผิดจริง ๆ—AI ทำหน้าที่นั้นให้คุณ

---

## สคริปต์ทำงานเต็มรูปแบบ

ด้านล่างเป็นสคริปต์ที่พร้อมรันทั้งหมด. แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์ที่เก็บรูปภาพและที่คุณต้องการให้ไฟล์ผลลัพธ์อยู่

```python
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Initialise OCR engine
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
ocr_engine.auto_skew = True

# -------------------------------------------------
# Step 2 – Recognise text from image
# -------------------------------------------------
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR (first 200 chars):")
print(ocr_result.text[:200])

# -------------------------------------------------
# Step 3 – Configure AI spell‑checker
# -------------------------------------------------
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30
)

spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")

# -------------------------------------------------
# Step 4 – Clean the OCR output
# -------------------------------------------------
corrected_text = spell_checker.run_postprocessor(ocr_result.text)
print("\nCleaned OCR (first 200 chars):")
print(corrected_text[:200])

# -------------------------------------------------
# Step 5 – Write to file
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/output_text.txt"
with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\nProcessing complete: input_image.png → {output_path}")

# -------------------------------------------------
# Step 6 – Free AI resources
# -------------------------------------------------
spell_checker.free_resources()
```

การรันสคริปต์นี้จะสร้าง `output_text.txt` ที่มีการถอดข้อความจากรูปภาพอย่างเรียบร้อย

---

## สรุป

เราได้แสดงวิธี **convert image to text** ด้วย Aspose OCR, แล้ว **clean OCR text python**‑style ด้วย AI spell‑checker. โซลูชันนี้เป็นไฟล์ Python เดียว, ทำงานได้บน Windows, macOS, หรือ Linux

หากต้องการก้าวต่อไป, พิจารณา:

* **วิธีดึงข้อความจากรูปภาพ** ใน PDF โดยแปลงหน้าเป็นรูปภาพก่อน  
* ป้อนข้อความที่ทำความสะอาดแล้วเข้าสู่โมเดลสรุปเพื่อสร้างรายงานอัตโนมัติ  
* เก็บผลลัพธ์ในฐานข้อมูลเวกเตอร์เพื่อการค้นหาเชิงความหมาย  

ลองใช้, ปรับแต่งพารามิเตอร์ของโมเดล, แล้วให้ pipeline OCR‑to‑text กลายเป็นเครื่องมือสำคัญในกระบวนการนำเข้าข้อมูลของคุณ. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}