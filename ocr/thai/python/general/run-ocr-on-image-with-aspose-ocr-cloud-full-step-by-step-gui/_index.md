---
category: general
date: 2026-03-28
description: เรียนรู้วิธีการทำ OCR บนภาพ ดาวน์โหลดโมเดล Hugging Face อัตโนมัติ ทำความสะอาดข้อความ
  OCR และกำหนดค่าโมเดล LLM ใน Python ด้วย Aspose OCR Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: th
og_description: ทำการ OCR บนภาพและทำความสะอาดผลลัพธ์โดยใช้โมเดล Hugging Face ที่ดาวน์โหลดอัตโนมัติ
  คู่มือนี้แสดงวิธีตั้งค่าโมเดล LLM ใน Python.
og_title: ทำ OCR บนรูปภาพ – คู่มือ Aspose OCR Cloud อย่างครบถ้วน
tags:
- OCR
- Python
- LLM
- HuggingFace
title: เรียกใช้ OCR บนภาพด้วย Aspose OCR Cloud – คู่มือขั้นตอนเต็ม
url: /th/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เรียกใช้ OCR บนภาพ – คู่มือเต็มของ Aspose OCR Cloud

เคยต้องการเรียกใช้ OCR บนไฟล์รูปภาพแต่ผลลัพธ์ดิบดูเหมือนเป็นการสับสนกันหรือไม่? ตามประสบการณ์ของผม จุดเจ็บปวดที่ใหญ่ที่สุดไม่ได้อยู่ที่การรับรู้เอง—แต่เป็นการทำความสะอาด. โชคดีที่ Aspose OCR Cloud ให้คุณแนบ LLM post‑processor ที่สามารถ *ทำความสะอาดข้อความ OCR* โดยอัตโนมัติ. ในบทเรียนนี้เราจะพาคุณผ่านทุกอย่างที่คุณต้องการ: ตั้งแต่ **การดาวน์โหลดโมเดลจาก Hugging Face** ไปจนถึงการกำหนดค่า LLM, การรัน OCR engine, และสุดท้ายการขัดเกลาผลลัพธ์.

โดยตอนจบของคู่มือนี้คุณจะมีสคริปต์พร้อม‑รันที่:

1. ดึงโมเดล Qwen 2.5 ขนาดกะทัดรัดจาก Hugging Face (ดาวน์โหลดอัตโนมัติให้คุณ).  
2. กำหนดค่าโมเดลให้รันบางส่วนของเครือข่ายบน GPU และส่วนที่เหลือบน CPU.  
3. ทำงาน OCR engine บนรูปภาพบันทึกมือ.  
4. ใช้ LLM ทำความสะอาดข้อความที่ได้รับการจดจำ, ให้ผลลัพธ์ที่อ่านได้โดยมนุษย์.

> **Prerequisites** – Python 3.8+, แพ็กเกจ `asposeocrcloud`, GPU ที่มี VRAM อย่างน้อย 4 GB (ไม่บังคับแต่แนะนำ), และการเชื่อมต่ออินเทอร์เน็ตสำหรับการดาวน์โหลดโมเดลครั้งแรก.

---

## สิ่งที่คุณต้องการ

- **Aspose OCR Cloud SDK** – ติดตั้งด้วย `pip install asposeocrcloud`.  
- **ภาพตัวอย่าง** – เช่น `handwritten_note.jpg` ที่วางไว้ในโฟลเดอร์โลคัล.  
- **การสนับสนุน GPU** – หากคุณมี GPU ที่เปิดใช้งาน CUDA, สคริปต์จะย้าย 30 ชั้นไปยัง GPU; หากไม่มีจะกลับไปใช้ CPU โดยอัตโนมัติ.  
- **สิทธิ์การเขียน** – สคริปต์จะแคชโมเดลใน `YOUR_DIRECTORY`; ตรวจสอบให้แน่ใจว่าโฟลเดอร์นั้นมีอยู่.

---

## Step 1 – Configure the LLM Model (download Hugging Face model)

สิ่งแรกที่เราทำคือบอก Aspose AI ว่าจะดึงโมเดลจากที่ไหน. คลาส `AsposeAIModelConfig` จัดการการดาวน์โหลดอัตโนมัติ, การควอนไทซ์, และการจัดสรรชั้นบน GPU.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Why this matters** – การควอนไทซ์เป็น `int8` ช่วยลดการใช้หน่วยความจำอย่างมหาศาล (≈ 4 GB เทียบกับ 12 GB). การแยกโมเดลระหว่าง GPU และ CPU ทำให้คุณสามารถรัน LLM ขนาด 3 พันล้านพารามิเตอร์แม้บน RTX 3060 ที่ค่อนข้างธรรมดา. หากคุณไม่มี GPU, ตั้งค่า `gpu_layers=0` แล้ว SDK จะทำงานทั้งหมดบน CPU.

> **Tip:** การรันครั้งแรกจะดาวน์โหลดประมาณ ~ 1.5 GB, ดังนั้นให้เวลาสักครู่และเชื่อมต่อที่เสถียร.

---

## Step 2 – Initialise the AI Engine with the Model Configuration

ตอนนี้เราจะสปินอัพ Aspose AI engine และป้อนการกำหนดค่าที่เราสร้างขึ้นมาให้มัน.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**What’s happening under the hood?** SDK ตรวจสอบ `directory_model_path` เพื่อหาโมเดลที่มีอยู่แล้ว. หากพบเวอร์ชันที่ตรงกันจะโหลดทันที; หากไม่พบจะดาวน์โหลดไฟล์ GGUF จาก Hugging Face, แยกแพ็คและเตรียม pipeline สำหรับการ inference.

---

## Step 3 – Create the OCR Engine and Attach the AI Post‑Processor

OCR engine ทำหน้าที่หนักในการจดจำอักขระ. โดยการแนบ `ocr_ai.run_postprocessor` เราจะเปิดใช้งาน **clean OCR text** โดยอัตโนมัติหลังการจดจำ.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Why use a post‑processor?** OCR ดิบมักมีการขึ้นบรรทัดใหม่ในตำแหน่งที่ไม่ถูกต้อง, เครื่องหมายวรรคตอนที่ตรวจจับผิด, หรือสัญลักษณ์รบกวน. LLM สามารถเขียนใหม่ให้เป็นประโยคที่สมบูรณ์, แก้ไขการสะกด, และแม้กระทั่งสรุปคำที่หายไป—โดยสรุปคือเปลี่ยนข้อมูลดิบให้เป็นข้อความที่เรียบหรู.

---

## Step 4 – Run OCR on an Image File

เมื่อทุกอย่างเชื่อมต่อกันแล้ว, ถึงเวลาป้อนภาพให้กับ engine.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Edge case:** หากภาพมีขนาดใหญ่ (> 5 MP) คุณอาจต้องปรับขนาดก่อนเพื่อเร่งการประมวลผล. SDK รองรับอ็อบเจกต์ Pillow `Image`, ดังนั้นคุณสามารถทำพรี‑โปรเซสด้วย `PIL.Image.thumbnail()` หากต้องการ.

---

## Step 5 – Let the AI Clean Up the Recognised Text and Show Both Versions

สุดท้ายเราจะเรียกใช้ post‑processor ที่แนบไว้ก่อนหน้านี้. ขั้นตอนนี้แสดงความแตกต่างระหว่าง *ก่อน* และ *หลัง* การทำความสะอาด.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Expected Output

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

สังเกตว่า LLM ได้:

- แก้ไขการจดจำ OCR ที่พบบ่อย (`Th1s` → `This`).  
- ลบสัญลักษณ์รบกวน (`&` → `and`).  
- ปรับบรรทัดใหม่ให้เป็นประโยคที่สมบูรณ์.

---

## 🎨 Visual Overview (Run OCR on image Workflow)

![Run OCR on image workflow](run_ocr_on_image_workflow.png "Diagram showing the run OCR on image pipeline from model download to cleaned output")

แผนภาพด้านบนสรุป pipeline ทั้งหมด: **download Hugging Face model → configure LLM → initialise AI → OCR engine → AI post‑processor → clean OCR text**.

---

## Common Questions & Pro Tips

### What if I don’t have a GPU?

ตั้งค่า `gpu_layers=0` ใน `AsposeAIModelConfig`. โมเดลจะทำงานทั้งหมดบน CPU, ซึ่งช้ากว่าแต่ยังทำงานได้. คุณยังสามารถสลับไปใช้โมเดลที่เล็กลง (เช่น `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`) เพื่อให้เวลา inference อยู่ในระดับที่รับได้.

### How do I change the model later?

เพียงอัปเดต `hugging_face_repo_id` แล้วรัน `ocr_ai.initialize(model_config)` ใหม่. SDK จะตรวจจับการเปลี่ยนเวอร์ชัน, ดาวน์โหลดโมเดลใหม่, และแทนที่ไฟล์ที่แคชไว้.

### Can I customise the post‑processor prompt?

ได้. ส่งพจนานุกรมไปยัง `custom_settings` พร้อมคีย์ `prompt_template`. ตัวอย่างเช่น:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Should I store the cleaned text to a file?

แน่นอน. หลังจากทำความสะอาดแล้วคุณสามารถเขียนผลลัพธ์ลงไฟล์ `.txt` หรือ `.json` เพื่อการประมวลผลต่อไป:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Conclusion

เราได้แสดงให้คุณเห็นวิธี **run OCR on image** ด้วย Aspose OCR Cloud, ดาวน์โหลดโมเดลจาก Hugging Face อัตโนมัติ, กำหนดค่า **configure LLM model** อย่างเชี่ยวชาญ, และสุดท้าย **clean OCR text** ด้วย LLM post‑processor ที่ทรงพลัง. ทั้งหมดนี้รวมอยู่ในสคริปต์ Python เพียงไฟล์เดียวที่ง่ายต่อการรันและทำงานได้ทั้งบนเครื่องที่มี GPU และเครื่องที่มีเฉพาะ CPU.

หากคุณคุ้นเคยกับ pipeline นี้แล้ว, ลองทดลองกับ:

- **Different LLMs** – ลอง `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` เพื่อรับหน้าต่างบริบทที่กว้างขึ้น.  
- **Batch processing** – วนลูปผ่านโฟลเดอร์ของภาพและรวมผลลัพธ์ที่ทำความสะอาดเป็น CSV.  
- **Custom prompts** – ปรับแต่ง AI ให้ตรงกับโดเมนของคุณ (เอกสารกฎหมาย, บันทึกการแพทย์, ฯลฯ).

อย่าลังเลที่จะปรับค่า `gpu_layers`, เปลี่ยนโมเดล, หรือใส่ prompt ของคุณเอง. ท้องฟ้าเป็นขอบเขต, และโค้ดที่คุณมีตอนนี้คือจุดเริ่มต้น.

Happy coding, and may your OCR outputs be ever clean! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}