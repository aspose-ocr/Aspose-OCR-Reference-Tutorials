---
category: general
date: 2026-05-03
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR และการตรวจสอบการสะกดด้วย AI เรียนรู้วิธีทำ
  OCR กับภาพ โหลดภาพสำหรับ OCR แยกข้อความจากใบแจ้งหนี้และปล่อยทรัพยากร GPU
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: th
og_description: สกัดข้อความจากภาพด้วย Aspose OCR และการตรวจสอบการสะกดด้วย AI คู่มือแบบขั้นตอนต่อขั้นตอนที่ครอบคลุมวิธี
  OCR ภาพ, โหลดภาพสำหรับ OCR, และการปล่อยทรัพยากร GPU.
og_title: ดึงข้อความจากภาพ – คู่มือ OCR และตรวจสอบการสะกดอย่างครบถ้วน
tags:
- OCR
- Aspose
- AI
- Python
title: ดึงข้อความจากภาพ – OCR ด้วย Aspose AI Spell‑Check
url: /th/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากรูปภาพ – คู่มือ OCR & การตรวจสอบการสะกดแบบครบถ้วน

เคยต้องการ **สกัดข้อความจากรูปภาพ** แต่ไม่แน่ใจว่าห้องสมุดใดจะให้ความเร็วและความแม่นยำพร้อมกัน? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง—เช่นการประมวลผลใบแจ้งหนี้, การแปลงใบเสร็จเป็นดิจิทัล, หรือการสแกนสัญญา—การได้ข้อความที่สะอาดและค้นหาได้จากภาพเป็นอุปสรรคแรก.

ข่าวดีคือ Aspose OCR ที่จับคู่กับโมเดล Aspose AI ที่มีน้ำหนักเบาสามารถทำงานนี้ได้ในไม่กี่บรรทัดของ Python ในบทแนะนำนี้เราจะอธิบาย **วิธี OCR รูปภาพ**, โหลดภาพอย่างถูกต้อง, รัน post‑processor ตรวจสอบการสะกดในตัว, และสุดท้าย **ปล่อยทรัพยากร GPU** เพื่อให้แอปของคุณเป็นมิตรกับหน่วยความจำ.

เมื่อจบคู่มือนี้คุณจะสามารถ **จดจำข้อความจากใบแจ้งหนี้** ในรูปภาพ, แก้ไขข้อผิดพลาด OCR ที่พบบ่อยโดยอัตโนมัติ, และทำให้ GPU ของคุณสะอาดสำหรับชุดต่อไป.

---

## สิ่งที่คุณต้องการ

- Python 3.9 หรือใหม่กว่า (โค้ดใช้ type hints แต่ทำงานได้กับเวอร์ชัน 3.x ก่อนหน้า)
- แพ็กเกจ `aspose-ocr` และ `aspose-ai` (ติดตั้งโดยใช้ `pip install aspose-ocr aspose-ai`)
- GPU ที่รองรับ CUDA เป็นตัวเลือก; สคริปต์จะใช้ CPU หากไม่พบ GPU
- ภาพตัวอย่าง เช่น `sample_invoice.png` ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้

ไม่มีเฟรมเวิร์ก ML ขนาดใหญ่, ไม่มีการดาวน์โหลดโมเดลขนาดมหาศาล—เพียงโมเดล Q4‑K‑M ที่คอมพิวท์แล้วขนาดเล็กที่พอดีกับ GPU ส่วนใหญ่.

## ขั้นตอนที่ 1: เริ่มต้น OCR Engine – สกัดข้อความจากรูปภาพ

สิ่งแรกที่คุณทำคือสร้างอินสแตนซ์ `OcrEngine` และบอกว่าคุณคาดหวังภาษาอะไร ที่นี่เราเลือก English และขอผลลัพธ์เป็น plain‑text ซึ่งเหมาะสำหรับการประมวลผลต่อไป.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**ทำไมจึงสำคัญ:** การตั้งค่าภาษา จำกัดชุดอักขระ ทำให้ความแม่นยำดีขึ้น โหมด plain‑text จะลบข้อมูลการจัดรูปแบบที่คุณมักไม่ต้องการเมื่อเพียงต้องการสกัดข้อความจากรูปภาพ.

## ขั้นตอนที่ 2: โหลดภาพสำหรับ OCR – วิธี OCR รูปภาพ

ตอนนี้เราจะส่งภาพจริงให้กับ engine ตัวช่วย `Image.load` เข้าใจรูปแบบทั่วไป (PNG, JPEG, TIFF) และจัดการความแปลกประหลาดของ file‑IO ให้คุณ.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**เคล็ดลับ:** หากภาพต้นทางของคุณมีขนาดใหญ่ ควรปรับขนาดก่อนส่งให้ engine; มิติที่เล็กลงสามารถลดการใช้หน่วยความจำ GPU โดยไม่ทำให้คุณภาพการจดจำลดลง.

## ขั้นตอนที่ 3: กำหนดค่า Aspose AI Model – จดจำข้อความจากใบแจ้งหนี้

Aspose AI มาพร้อมกับโมเดล GGUF ขนาดเล็กที่คุณสามารถดาวน์โหลดอัตโนมัติ ตัวอย่างใช้รีโพซิทอรี `Qwen2.5‑3B‑Instruct‑GGUF` ที่คอมพิวท์เป็น `q4_k_m` เรายังบอก runtime ให้จัดสรร 20 ชั้นบน GPU เพื่อสมดุลความเร็วและการใช้ VRAM.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**เบื้องหลัง:** โมเดลคอมพิวท์มีขนาดประมาณ 1.5 GB บนดิสก์ เป็นส่วนเล็กของโมเดลความแม่นยำเต็มรูปแบบ แต่ยังคงจับความละเอียดทางภาษาที่เพียงพอเพื่อระบุการสะกดผิดทั่วไปของ OCR.

## ขั้นตอนที่ 4: เริ่มต้น AsposeAI และแนบ post‑processor ตรวจสอบการสะกด

Aspose AI มี post‑processor ตรวจสอบการสะกดที่พร้อมใช้ โดยการแนบมัน ผลลัพธ์ OCR ทุกอย่างจะถูกทำความสะอาดโดยอัตโนมัติ.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**ทำไมต้องใช้ post‑processor?** เครื่องมือ OCR มักอ่าน “Invoice” เป็น “Invo1ce” หรือ “Total” เป็น “T0tal” การตรวจสอบการสะกดจะรันโมเดลภาษาน้ำหนักเบาบนสตริงดิบและแก้ไขข้อผิดพลาดเหล่านั้นโดยที่คุณไม่ต้องเขียนพจนานุกรมเอง.

## ขั้นตอนที่ 5: รัน post‑processor ตรวจสอบการสะกดบนผลลัพธ์ OCR

เมื่อทุกอย่างเชื่อมต่อแล้ว การเรียกครั้งเดียวจะให้ข้อความที่แก้ไขแล้ว เรายังพิมพ์ทั้งเวอร์ชันดั้งเดิมและเวอร์ชันที่ทำความสะอาดเพื่อให้คุณเห็นการปรับปรุง.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

ผลลัพธ์ทั่วไปสำหรับใบแจ้งหนี้อาจมีลักษณะดังนี้:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

สังเกตว่า “Invo1ce” ถูกเปลี่ยนเป็นคำที่ถูกต้อง “Invoice” นั่นคือพลังของการตรวจสอบการสะกด AI ในตัว.

## ขั้นตอนที่ 6: ปล่อยทรัพยากร GPU – ปล่อยทรัพยากร GPU อย่างปลอดภัย

หากคุณรันสคริปต์นี้ในบริการที่ทำงานต่อเนื่อง (เช่นเว็บ API ที่ประมวลผลหลายสิบใบแจ้งหนี้ต่อวินาที) คุณต้องปล่อยคอนเท็กซ์ GPU หลังจากแต่ละชุด มิฉะนั้นจะเกิดการรั่วหน่วยความจำและในที่สุดจะเจอข้อผิดพลาด “CUDA out of memory”.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**เคล็ดลับมืออาชีพ:** เรียก `free_resources()` ภายในบล็อก `finally` หรือ context manager เพื่อให้มันทำงานเสมอ แม้เกิดข้อยกเว้น.

## ตัวอย่างทำงานเต็มรูปแบบ

การรวมส่วนต่าง ๆ เข้าด้วยกันให้คุณได้สคริปต์ที่เป็นอิสระที่สามารถใส่ลงในโปรเจกต์ใดก็ได้.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

บันทึกไฟล์, ปรับเส้นทางไปยังภาพของคุณ, และรัน `python extract_text_from_image.py` คุณควรเห็นข้อความใบแจ้งหนี้ที่ทำความสะอาดแล้วแสดงบนคอนโซล.

## คำถามที่พบบ่อย (FAQ)

**Q: ทำงานบนเครื่องที่มีเฉพาะ CPU หรือไม่?**  
A: แน่นอน หากไม่พบ GPU Aspose AI จะย้อนกลับไปใช้ CPU แม้ว่าจะช้ากว่า คุณสามารถบังคับใช้ CPU ได้โดยตั้งค่า `model_cfg.gpu_layers = 0`.

**Q: ถ้าใบแจ้งหนี้ของฉันเป็นภาษาอื่นที่ไม่ใช่ English จะทำอย่างไร?**  
A: เปลี่ยน `ocr_engine.language` เป็นค่า enum ที่เหมาะสม (เช่น `aocr.Language.Spanish`). โมเดลตรวจสอบการสะกดเป็นหลายภาษา แต่คุณอาจได้ผลลัพธ์ที่ดีกว่าด้วยโมเดลเฉพาะภาษา.

**Q: ฉันสามารถประมวลผลหลายภาพในลูปได้หรือไม่?**  
A: ได้ เพียงย้ายขั้นตอนการโหลด, การจดจำ, และ post‑processing เข้าไปในลูป `for` จำไว้ว่าต้องเรียก `ocr_ai.free_resources()` หลังลูปหรือหลังแต่ละชุดหากคุณใช้ AI อินสแตนซ์เดียวกันซ้ำ.

**Q: ขนาดการดาวน์โหลดโมเดลเท่าไหร่?**  
A: ประมาณ 1.5 GB สำหรับเวอร์ชันคอมพิวท์ `q4_k_m` จะถูกแคชหลังจากรันครั้งแรก ดังนั้นการรันต่อมาจะเร็วทันใจ.

## สรุป

ในบทแนะนำนี้เราได้สาธิตวิธี **สกัดข้อความจากรูปภาพ** ด้วย Aspose OCR, กำหนดค่าโมเดล AI ขนาดเล็ก, ใช้ post‑processor ตรวจสอบการสะกด, และปล่อย **ทรัพยากร GPU** อย่างปลอดภัย กระบวนการครอบคลุมตั้งแต่การโหลดภาพจนถึงการทำความสะอาดหลังการใช้งาน ให้คุณมี pipeline ที่เชื่อถือได้สำหรับสถานการณ์ **จดจำข้อความจากใบแจ้งหนี้**  

ขั้นตอนต่อไป? ลองเปลี่ยน post‑processor ตรวจสอบการสะกดเป็นโมเดลการสกัดเอนทิตีแบบกำหนดเอง

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}