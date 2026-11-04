---
category: general
date: 2026-03-18
description: บทเรียน OCR พื้นฐานด้วย Python แสดงวิธีแปลงไฟล์ TIFF เป็นข้อความ, โหลด
  OCR ของภาพ, ตั้งค่าชั้น GPU, และแก้ไขศูนย์นำหน้าโดยใช้ Aspose AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: th
og_description: บทเรียน OCR พื้นฐานด้วย Python จะพาคุณผ่านการแปลงไฟล์ TIFF เป็นข้อความที่สะอาด
  การโหลดรูปภาพ การตั้งค่าเลเยอร์ GPU และการแก้ไขศูนย์นำหน้า
og_title: OCR พื้นฐานด้วย Python – แปลง TIFF เป็นข้อความ
tags:
- OCR
- Python
- AI
- Aspose
title: OCR พื้นฐานด้วย Python – แปลงไฟล์ TIFF เป็นข้อความ
url: /th/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – แปลง TIFF เป็นข้อความด้วย AI Post‑Processing

กำลังมองหาวิธีทำ **basic ocr python** บนเอกสารสแกนของคุณหรือไม่? ในคู่มือนี้เราจะอธิบายขั้นตอนการแปลงไฟล์ TIFF ให้เป็นข้อความที่สะอาดและค้นหาได้โดยใช้ Aspose OCR และ AI post‑processor  

หากคุณเคยประสบปัญหาในการ **convert TIFF to text** เพราะผลลัพธ์ดิบเต็มไปด้วยการพิมพ์ผิดหรือสัญลักษณ์แปลก ๆ คุณไม่ได้เป็นคนเดียว เราจะสาธิตวิธี **load image OCR** ปรับเอนจินให้ **set GPU layers** และแม้กระทั่ง **fix leading zeroes** ที่มักพบในหมายเลขใบแจ้งหนี้

## What You’ll Learn

- วิธี initialise Aspose OCR engine สำหรับเอกสารพิมพ์  
- ขั้นตอนที่แน่นอนในการ **load image OCR** จากไฟล์ TIFF และรับข้อความดิบ  
- การกำหนดค่า AI model, ดาวน์โหลดอัตโนมัติ, และ **set GPU layers** เพื่อเร่งความเร็วการ inference  
- การเพิ่ม spell‑check ในตัวพร้อมฟังก์ชันกำหนดเองที่ **fixes leading zeroes**  
- การทำความสะอาดผลลัพธ์ OCR และการปล่อยทรัพยากรอย่างถูกต้อง  

เมื่อจบบทเรียนนี้คุณจะมีสคริปต์ Python เพียงไฟล์เดียวที่สามารถแปลง TIFF ใด ๆ ให้เป็นข้อความที่เรียบร้อยและค้นหาได้—ไม่ต้องคัดลอก‑วางด้วยมือ

### Prerequisites

- Python 3.8+ ติดตั้งบนเครื่องของคุณ  
- แพคเกจ `aspose-ocr` (`pip install aspose-ocr`)  
- ตัวเลือก: GPU ที่มี VRAM อย่างน้อย 4 GB หากต้องการ **set GPU layers**; หากไม่มีโค้ดจะสลับไปใช้ CPU โดยอัตโนมัติ  

---

## basic ocr python – load image and recognize text

สิ่งแรกที่เราต้องทำคือ **load image OCR** เพื่อให้เอนจินอ่านพิกเซล Aspose’s `OcrEngine` รองรับหลายรูปแบบ แต่ที่นี่เรามุ่งเน้นที่ TIFF เพราะเป็นรูปแบบที่พบบ่อยที่สุดสำหรับใบแจ้งหนี้สแกน

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** หากคุณทำงานกับ multi‑page TIFFs, Aspose จะประมวลผลแต่ละหน้าโดยอัตโนมัติ ดังนั้นไม่จำเป็นต้องเขียนลูปเพิ่ม

เมื่อโหลดภาพแล้ว ให้รันการจดจำขั้นพื้นฐาน

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

คุณจะเห็นผลลัพธ์ประมาณนี้:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

สังเกต *ศูนย์* ก่อนตัวอักษรหรือไม่? นั่นคือ artefact ของ OCR ที่เราจะทำความสะอาดในภายหลัง

![ขั้นตอนการทำ basic ocr python](/images/ocr-workflow.png "basic ocr python workflow diagram")

---

## Step 2: Convert TIFF to text – prepare the AI post‑processor

Raw OCR มีประโยชน์ แต่หลาย pipeline ในการผลิตต้องการเวอร์ชันที่เรียบหรู Aspose มี wrapper `AsposeAI` ที่สามารถดาวน์โหลดโมเดลจาก Hugging Face, รันบน GPU, และทำ spell‑check อัตโนมัติ

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Why `set GPU layers` matters

พารามิเตอร์ `gpu_layers` บอกโมเดล GGUF ว่าจะเก็บจำนวน layer ของ transformer ไว้บน GPU กี่ชั้น มากกว่าหนึ่ง layer = inference เร็วขึ้นแต่ใช้ VRAM มากขึ้น หากคุณใช้แล็ปท็อปที่สเปคต่ำ ให้ลดค่าเป็น `10` หรือไม่ระบุเลยเพื่อใช้ CPU

---

## Step 3: Apply spellcheck and **fix leading zeroes**

Aspose AI มาพร้อม spell‑checker ในตัวที่จับการพิมพ์ผิดภาษาอังกฤษส่วนใหญ่ อย่างไรก็ตาม การแก้ไขเฉพาะโดเมน—เช่นเปลี่ยน `0` นำหน้าเป็น `O` สำหรับรหัสใบแจ้งหนี้—ต้องใช้ post‑processor กำหนดเอง

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Why this works:** Regular expression ค้นหาขอบคำ (`\b`), ศูนย์, แล้วตามด้วยอักษรใหญ่สามตัวอย่างตรง จากนั้นแทนที่ศูนย์ด้วยตัวอักษร “O”. คุณสามารถขยาย pattern เพื่อจัดการกับกรณีอื่น ๆ (เช่น `0[0-9]{2}` สำหรับตัวเลขที่อ่านผิด)

---

## Step 4: Clean the OCR result with the AI post‑processor

ตอนนี้เราจะรวมทุกอย่าง: สตริงดิบจาก **basic ocr python**, spell‑check, และการแก้ศูนย์นำหน้า เมธอด `run_postprocessor` จะคืนค่าข้อความที่ทำความสะอาดแล้วพร้อมใช้ในระบบต่อไป

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

ผลลัพธ์ทั่วไปหลัง post‑processor:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

คุณจะเห็นว่าศูนย์นำหน้าถูกเปลี่ยนเป็น `O` และการพิมพ์ผิดทั่วไปได้รับการแก้ไข ข้อความนี้พร้อมสำหรับการทำ indexing ใน search engine หรือส่งต่อไปยัง pipeline การสกัดข้อมูล

---

## Step 5: Release AI resources – keep your GPU happy

หากคุณรันงาน OCR หลายงานในบริการที่ทำงานต่อเนื่อง ควรปล่อยหน่วยความจำ GPU ของโมเดลเมื่อเสร็จสิ้น

```python
ocr_ai.free_resources()
```

การข้ามขั้นตอนนี้อาจทำให้เกิดข้อผิดพลาด “out‑of‑memory” ในการเรียกครั้งต่อไป โดยเฉพาะเมื่อ **set GPU layers** เป็นค่าที่สูง

---

## Optional Variations & Edge Cases

| Situation | What to change |
|-----------|----------------|
| **Handwritten documents** | ใช้ `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` แทน `PRINTED` |
| **No GPU available** | ตั้ง `gpu_layers=0` หรือไม่ระบุอาร์กิวเมนต์; โมเดลจะรันบน CPU (ช้ากว่าแต่ปลอดภัย) |
| **Different language** | เปลี่ยน Hugging Face repo ID ไปเป็นโมเดลเฉพาะภาษา เช่น `microsoft/Florence-2-base` |
| **Batch processing** | ห่อขั้นตอนในลูป `for file in glob("*.tif"):` แล้วเก็บผลลัพธ์ใน list หรือ CSV |
| **More complex zero patterns** | ขยาย `invoice_fix` ด้วย regex เพิ่มเติม เช่น `r"\b0+([A-Z]{2,})\b"` สำหรับศูนย์นำหน้าหลายตัว |

---

## Conclusion

เราจบ pipeline **basic ocr python** ที่โหลด TIFF, ดึงข้อความดิบ, แล้วทำความสะอาดด้วย AI model พร้อม **set GPU layers** เพื่อประสิทธิภาพ การทำ post‑processor กำหนดเองแสดงให้เห็นวิธี **fix leading zeroes**, รายละเอียดเล็ก ๆ ที่มักทำให้การวิเคราะห์ต่อไปล้มเหลว

ลองทดลองเพิ่มเติม: ใช้ quantization อื่น (`float16` เพื่อความแม่นยำสูงขึ้น), เปลี่ยน spell‑check เป็นพจนานุกรมเฉพาะโดเมน, หรือเชื่อมต่อหลายฟังก์ชันแก้ไขกำหนดเอง รูปแบบยังคงเหมือนเดิม—load, recognize, configure AI, post‑process, และ clean up

**Next steps** ที่คุณอาจสนใจ:

- ผสานผลลัพธ์ที่ทำความสะอาดกับฐานข้อมูลหรือ Elasticsearch index  
- ใช้แนวทางเดียวกันเพื่อ **convert TIFF to text** สำหรับ PDF หลายภาษา  
- เพิ่ม UI ด้วย Flask หรือ FastAPI เพื่อให้ผู้ใช้ที่ไม่เชี่ยวชาญสามารถอัปโหลดไฟล์และรับข้อความที่ทำความสะอาดได้ทันที  

Happy coding, and may your OCR results always be crisp and zero‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}