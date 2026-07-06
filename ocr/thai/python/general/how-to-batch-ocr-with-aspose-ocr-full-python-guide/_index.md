---
category: general
date: 2026-05-03
description: วิธีทำ OCR รูปภาพเป็นชุดโดยใช้ Aspose OCR และการตรวจสอบการสะกดด้วย AI
  เรียนรู้วิธีดึงข้อความจากรูปภาพ ใช้การตรวจสอบการสะกด แหล่งทรัพยากร AI ฟรี และแก้ไขข้อผิดพลาดของ
  OCR
draft: false
keywords:
- how to batch ocr
- extract text from images
- free ai resources
- apply spell check
- correct ocr errors
language: th
og_description: วิธีทำ OCR รูปภาพเป็นชุดโดยใช้ Aspose OCR และการตรวจสอบการสะกดด้วย
  AI. ทำตามคู่มือขั้นตอนต่อขั้นตอนเพื่อดึงข้อความจากรูปภาพ, ใช้การตรวจสอบการสะกด,
  ใช้ทรัพยากร AI ฟรีและแก้ไขข้อผิดพลาดของ OCR.
og_title: วิธีทำ OCR แบบชุดด้วย Aspose OCR – บทเรียน Python ฉบับสมบูรณ์
tags:
- OCR
- Python
- AI
- Aspose
title: วิธีทำ OCR แบบกลุ่มด้วย Aspose OCR – คู่มือ Python ฉบับเต็ม
url: /th/python/general/how-to-batch-ocr-with-aspose-ocr-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ Batch OCR ด้วย Aspose OCR – คู่มือ Python ฉบับเต็ม

เคยสงสัย **วิธีทำ batch OCR** โฟลเดอร์เต็มของไฟล์ PDF หรือรูปสแกนโดยไม่ต้องเขียนสคริปต์แยกสำหรับแต่ละไฟล์หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลาย ๆ pipeline ของโลกจริง คุณจะต้อง **ดึงข้อความจากรูปภาพ**, ทำความสะอาดข้อผิดพลาดการสะกด, และสุดท้ายปล่อยทรัพยากร AI ที่คุณได้จัดสรรไว้ บทแนะนำนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าจะทำอย่างไรด้วย Aspose OCR, post‑processor AI ที่เบา, และไม่กี่บรรทัดของ Python.

เราจะอธิบายขั้นตอนการเริ่มต้น OCR engine, เชื่อมต่อ AI spell‑checker, วนลูปผ่านไดเรกทอรีของรูปภาพ, และทำความสะอาดโมเดลหลังจากนั้น. เมื่อเสร็จคุณจะได้สคริปต์พร้อมรันที่ **แก้ไขข้อผิดพลาด OCR** อัตโนมัติและปล่อย **ทรัพยากร AI ฟรี** เพื่อให้ GPU ของคุณทำงานได้อย่างราบรื่น.

## สิ่งที่คุณต้องการ

- Python 3.9+ (โค้ดใช้ type‑hints แต่ทำงานได้กับเวอร์ชัน 3.x ก่อนหน้า)
- `asposeocr` package (`pip install asposeocr`) – ให้บริการ OCR engine.
- เข้าถึงโมเดล Hugging Face `bartowski/Qwen2.5-3B-Instruct-GGUF` (ดาวน์โหลดโดยอัตโนมัติ).
- GPU ที่มี VRAM อย่างน้อยหลาย GB (สคริปต์ตั้งค่า `gpu_layers = 30`, คุณสามารถลดได้หากต้องการ).

ไม่มีบริการภายนอก, ไม่มี API ที่ต้องชำระเงิน – ทุกอย่างทำงานบนเครื่องท้องถิ่น.

---

## ขั้นตอนที่ 1: ตั้งค่า OCR Engine – **วิธีทำ Batch OCR** อย่างมีประสิทธิภาพ

ก่อนที่เราจะประมวลผลภาพจำนวนพัน เราต้องการ OCR engine ที่มั่นคง Aspose OCR ให้เราสามารถเลือกภาษาและโหมดการจดจำในคำสั่งเดียว.

```python
# Step 1: Initialize the OCR engine for English plain‑text output
def init_ocr() -> aocr.OcrEngine:
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English          # English language pack
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Returns raw string, no layout
    return ocr_engine
```

**ทำไมเรื่องนี้สำคัญ:** การตั้งค่า `recognize_mode` เป็น `Plain` ทำให้ผลลัพธ์มีน้ำหนักเบา ซึ่งเหมาะเมื่อคุณวางแผนจะทำการตรวจสอบการสะกดต่อไป หากคุณต้องการข้อมูลการจัดหน้า คุณจะสลับเป็น `Layout` แต่จะเพิ่มภาระที่คุณอาจไม่ต้องการในงาน batch.

> **เคล็ดลับ:** หากคุณกำลังจัดการกับการสแกนหลายภาษา คุณสามารถส่งรายการเช่น `ocr_engine.language = [aocr.Language.English, aocr.Language.Spanish]`.

---

## ขั้นตอนที่ 2: เริ่มต้น AI Post‑Processor – **ใช้การตรวจสอบการสะกด** กับผลลัพธ์ OCR

Aspose AI มาพร้อมกับ post‑processor ในตัวที่สามารถรันโมเดลใดก็ได้ที่คุณต้องการ ที่นี่เราดึงโมเดล Qwen 2.5 ที่ถูกควอนไทซ์จาก Hugging Face และเชื่อมต่อฟังก์ชันตรวจสอบการสะกด.

```python
# Step 2: Configure and start the AI post‑processor
def init_ai() -> aocr.ai.AsposeAI:
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 30          # Adjust based on your GPU memory
    ai_processor = AsposeAI()
    ai_processor.initialize(model_cfg)

    # Attach the built‑in spell‑check post‑processor
    ai_processor.set_post_processor(ai_processor.postprocessor_spell_check, {})
    return ai_processor
```

**ทำไมเรื่องนี้สำคัญ:** โมเดลถูกควอนไทซ์ (`q4_k_m`) ซึ่งลดการใช้หน่วยความจำอย่างมากในขณะที่ยังให้ความเข้าใจภาษาในระดับที่ดี โดยการเรียก `set_post_processor` เราบอก Aspose AI ให้รันขั้นตอน **apply spell check** โดยอัตโนมัติบนสตริงใด ๆ ที่เราป้อนเข้าไป.

> **ระวัง:** หาก GPU ของคุณไม่สามารถจัดการ 30 ชั้นได้ ให้ลดจำนวนลงเป็น 15 หรือแม้แต่ 5 – สคริปต์ยังทำงานได้ แต่จะช้าลงเล็กน้อย.

---

## ขั้นตอนที่ 3: รัน OCR และ **แก้ไขข้อผิดพลาด OCR** บนรูปภาพเดียว

ตอนนี้ OCR engine และ AI spell‑checker พร้อมแล้ว เราจะรวมเข้าด้วยกัน ฟังก์ชันนี้โหลดรูปภาพ, ดึงข้อความดิบ, แล้วรัน AI post‑processor เพื่อทำความสะอาด.

```python
# Step 3: OCR an image and run the spell‑check post‑processor
def ocr_and_correct(image_path: str,
                    ocr_engine: aocr.OcrEngine,
                    ai_processor: aocr.ai.AsposeAI) -> str:
    image = aocr.Image.load(image_path)               # Load any supported format
    raw_text = ocr_engine.recognize(image)           # Plain string from OCR
    corrected_text = ai_processor.run_postprocessor(raw_text)
    return corrected_text
```

**ทำไมเรื่องนี้สำคัญ:** การส่งสตริง OCR ดิบตรงเข้าสู่โมเดล AI ทำให้เราได้ขั้นตอน **correct OCR errors** โดยไม่ต้องเขียน regex หรือพจนานุกรมกำหนดเอง โมเดลเข้าใจบริบท จึงสามารถแก้ “recieve” → “receive” และข้อผิดพลาดที่ละเอียดอ่อนยิ่งขึ้น.

---

## ขั้นตอนที่ 4: **ดึงข้อความจากรูปภาพ** เป็นจำนวนมาก – ลูป Batch ที่แท้จริง

นี่คือจุดที่ความมหัศจรรย์ของ **วิธีทำ batch OCR** ปรากฏ เราจะวนลูปผ่านไดเรกทอรี, ข้ามไฟล์ที่ไม่รองรับ, และเขียนผลลัพธ์ที่แก้ไขแล้วแต่ละไฟล์เป็นไฟล์ `.txt`.

```python
# Step 4: Process an entire folder of images
if __name__ == "__main__":
    # Initialize once – reuse for every file
    ocr_engine = init_ocr()
    ai_processor = init_ai()

    input_dir = "YOUR_DIRECTORY/input_images"
    output_dir = "YOUR_DIRECTORY/output_text"
    os.makedirs(output_dir, exist_ok=True)

    for file_name in os.listdir(input_dir):
        # Only handle common image extensions
        if not file_name.lower().endswith(('.png', '.jpg', '.jpeg', '.tif', '.tiff')):
            continue

        image_path = os.path.join(input_dir, file_name)
        corrected = ocr_and_correct(image_path, ocr_engine, ai_processor)

        txt_path = os.path.join(output_dir,
                                os.path.splitext(file_name)[0] + ".txt")
        with open(txt_path, "w", encoding="utf-8") as txt_file:
            txt_file.write(corrected)

        print(f"Processed {file_name}")

    # Step 5: Release **free AI resources** after the batch finishes
    ai_processor.free_resources()
```

### ผลลัพธ์ที่คาดหวัง

สำหรับรูปภาพที่มีประโยค *“The quick brown fox jumps over the lazzy dog.”* คุณจะเห็นไฟล์ข้อความที่มี:

```
The quick brown fox jumps over the lazy dog.
```

สังเกตว่า “z” คู่ถูกแก้ไขโดยอัตโนมัติ – นั่นคือ AI spell‑check ทำงาน.

**ทำไมเรื่องนี้สำคัญ:** ด้วยการสร้างวัตถุ OCR และ AI **ครั้งเดียว** แล้วใช้ซ้ำ เราจะหลีกเลี่ยงภาระการโหลดโมเดลสำหรับแต่ละไฟล์ นี่เป็นวิธีที่มีประสิทธิภาพที่สุดในการ **ทำ batch OCR** ในระดับใหญ่.

---

## ขั้นตอนที่ 5: ทำความสะอาด – **ปล่อยทรัพยากร AI** อย่างถูกต้อง

เมื่อเสร็จสิ้น การเรียก `free_resources()` จะปล่อยหน่วยความจำ GPU, บริบท CUDA, และไฟล์ชั่วคราวใด ๆ ที่โมเดลสร้างขึ้น.

```python
# Step 5: Explicitly free GPU and model memory
ai_processor.free_resources()
```

การข้ามขั้นตอนนี้อาจทำให้มีการจัดสรร GPU ค้างอยู่ ซึ่งอาจทำให้กระบวนการ Python ถัดไปล่มหรือใช้ VRAM มากเกินไป คิดว่าเป็นส่วน “ปิดไฟ” ของงาน batch.

---

## ข้อผิดพลาดทั่วไป & เคล็ดลับเพิ่มเติม

| Issue | What to Look For | Fix |
|-------|------------------|-----|
| **ข้อผิดพลาด Out‑of‑memory** | GPU หมดหลังจากประมวลผลหลายสิบภาพ | ลด `gpu_layers` หรือสลับเป็น CPU (`model_cfg.gpu_layers = 0`). |
| **Missing language pack** | OCR คืนค่าเป็นสตริงว่าง | ตรวจสอบว่าเวอร์ชัน `asposeocr` มีข้อมูลภาษาอังกฤษ; ติดตั้งใหม่หากจำเป็น. |
| **ไฟล์ที่ไม่ใช่รูปภาพ** | สคริปต์ล่มเมื่อเจอไฟล์ `.pdf` ที่หลงเหลือ | เงื่อนไข `if not file_name.lower().endswith(...)` จะข้ามไฟล์เหล่านั้นอยู่แล้ว. |
| **Spell‑check ไม่ทำงาน** | ผลลัพธ์เหมือนกับ OCR ดิบ | ตรวจสอบว่าได้เรียก `ai_processor.set_post_processor` ก่อนลูป. |
| **ความเร็ว batch ช้า** | ใช้เวลา >5 วินาทีต่อภาพ | เปิดใช้งาน `model_cfg.allow_auto_download = "false"` หลังการรันครั้งแรก เพื่อไม่ให้โมเดลดาวน์โหลดซ้ำทุกครั้ง. |

**เคล็ดลับ:** หากคุณต้องการ **ดึงข้อความจากรูปภาพ** ในภาษาที่ไม่ใช่ภาษาอังกฤษ เพียงเปลี่ยน `ocr_engine.language` เป็น enum ที่เหมาะสม (เช่น `aocr.Language.French`). AI post‑processor เดียวกันจะยังคงทำการตรวจสอบการสะกด, แต่คุณอาจต้องการโมเดลเฉพาะภาษาสำหรับผลลัพธ์ที่ดีที่สุด.

---

## สรุป & ขั้นตอนต่อไป

เราได้ครอบคลุม pipeline ทั้งหมดสำหรับ **วิธีทำ batch OCR**:

1. **Initialize** OCR engine แบบ plain‑text สำหรับภาษาอังกฤษ.  
2. **Configure** โมเดล AI ตรวจสอบการสะกดและผูกเป็น post‑processor.  
3. **Run** OCR บนแต่ละภาพและให้ AI **correct OCR errors** โดยอัตโนมัติ.  
4. **Loop** ผ่านไดเรกทอรีเพื่อ **ดึงข้อความจากรูปภาพ** จำนวนมาก.  
5. **Free AI resources** เมื่องานเสร็จสิ้น.

จากนี้คุณสามารถ:

- ส่งข้อความที่แก้ไขแล้วเข้าสู่ pipeline NLP ต่อไป (การวิเคราะห์ความรู้สึก, การสกัดเอนทิตี้, ฯลฯ).
- เปลี่ยน post‑processor ตรวจสอบการสะกดเป็นสรุปแบบกำหนดเองโดยเรียก `ai_processor.set_post_processor(your_custom_func, {})`.
- ทำให้ลูปโฟลเดอร์ทำงานแบบขนานด้วย `concurrent.futures.ThreadPoolExecutor` หาก GPU ของคุณรองรับหลายสตรีม.

---

## ความคิดสุดท้าย

การทำ Batch OCR ไม่จำเป็นต้องเป็นภาระหนัก ด้วยการใช้ Aspose OCR ร่วมกับโมเดล AI ที่เบา คุณจะได้ **โซลูชันครบวงจร** ที่ **ดึงข้อความจากรูปภาพ**, **ใช้การตรวจสอบการสะกด**, **แก้ไขข้อผิดพลาด OCR**, และ **ปล่อยทรัพยากร AI** อย่างสะอาด ให้สคริปต์ทำงานบนโฟลเดอร์ทดสอบ, ปรับจำนวนชั้น GPU ให้ตรงกับฮาร์ดแวร์ของคุณ, แล้วคุณจะมี pipeline พร้อมใช้งานในไม่กี่นาที.

มีคำถามเกี่ยวกับการปรับโมเดล, การจัดการ PDF, หรือการรวมเข้ากับบริการเว็บ? แสดงความคิดเห็นด้านล่างหรือทักมาผมบน GitHub. โค้ดดิ้งอย่างสนุกสนาน, และขอให้ OCR ของคุณแม่นยำเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}