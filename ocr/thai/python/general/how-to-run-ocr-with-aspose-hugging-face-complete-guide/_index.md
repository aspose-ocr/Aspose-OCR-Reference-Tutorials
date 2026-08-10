---
category: general
date: 2026-04-29
description: เรียนรู้วิธีทำ OCR บนสแกนของคุณ ใช้โมเดล Hugging Face อัตโนมัติ และจดจำข้อความจากสแกนด้วย
  Aspose OCR ในไม่กี่นาที.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: th
og_description: วิธีทำ OCR บนสแกนด้วย Aspose OCR ดาวน์โหลดโมเดลจาก Hugging Face อัตโนมัติ
  และได้ข้อความที่สะอาดพร้อมเครื่องหมายวรรคตอน
og_title: วิธีใช้งาน OCR ด้วย Aspose & Hugging Face – คู่มือฉบับสมบูรณ์
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: วิธีใช้งาน OCR ด้วย Aspose & Hugging Face – คู่มือฉบับสมบูรณ์
url: /th/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีรัน OCR ด้วย Aspose & Hugging Face – คู่มือเต็ม

เคยสงสัย **วิธีรัน OCR** บนกองเอกสารที่สแกนโดยไม่ต้องใช้เวลาหลายชั่วโมงปรับตั้งค่าหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการ นักพัฒนาต้องการ **จดจำข้อความจากการสแกน** อย่างรวดเร็ว แต่กลับเจอปัญหาในการดาวน์โหลดโมเดลและการประมวลผลต่อเนื่อง  

ข่าวดี: บทแนะนำนี้จะแสดงวิธีแก้ปัญหาที่พร้อมใช้งานซึ่ง **ใช้โมเดล Hugging Face**, ดึงโมเดลโดยอัตโนมัติ และเพิ่มเครื่องหมายวรรคตอนเพื่อให้ผลลัพธ์อ่านเหมือนคนเขียน สุดท้ายคุณจะได้สคริปต์ที่ประมวลผลรูปภาพทุกไฟล์ในโฟลเดอร์และสร้างไฟล์ `.txt` ที่สะอาดข้างๆ การสแกนแต่ละไฟล์

## สิ่งที่คุณต้องการ

- Python 3.8+ (โค้ดใช้ f‑strings ดังนั้นเวอร์ชันเก่าจะไม่ทำงาน)
- `aspose-ocr` package (ติดตั้งโดยใช้ `pip install aspose-ocr`)
- การเข้าถึงอินเทอร์เน็ตสำหรับการดาวน์โหลดโมเดลครั้งแรก  
- โฟลเดอร์ของภาพสแกน (`.png`, `.jpg`, หรือ `.tif`)

เท่านี้—ไม่มีไบนารีเพิ่มเติม ไม่มีการจัดการโมเดลด้วยตนเอง มาเริ่มกันเลย

![how to run OCR example](https://example.com/ocr-demo.png "how to run OCR example")

## ขั้นตอนที่ 1: นำเข้า Aspose OCR Classes & ตั้งค่าสภาพแวดล้อม

เราเริ่มโดยดึงคลาสที่จำเป็นจากไลบรารี Aspose OCR การนำเข้าทั้งหมดตั้งแต่ต้นทำให้สคริปต์เป็นระเบียบและง่ายต่อการตรวจหาการพึ่งพาที่ขาดหาย

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*ทำไมเรื่องนี้สำคัญ*: `OcrEngine` ทำงานหนัก ส่วน `AsposeAI` ให้เราต่อโมเดลภาษาใหญ่เพื่อการประมวลผลต่อเนื่องที่ฉลาดขึ้น หากคุณละเว้นการนำเข้า โค้ดส่วนที่เหลือจะไม่คอมไพล์เลย—ดังนั้นอย่าลืมทำ

## ขั้นตอนที่ 2: กำหนดค่าโมเดล Hugging Face ที่รองรับ GPU  

ตอนนี้เราบอก Aspose ว่าจะดึงโมเดลจากที่ไหนและต้องใช้เลเยอร์บน GPU กี่ชั้น ธง `allow_auto_download="true"` ทำหน้าที่ **ดาวน์โหลดโมเดลโดยอัตโนมัติ** ให้คุณ

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **เคล็ดลับ**: หากคุณไม่มี GPU ให้ตั้งค่า `gpu_layers=0` โมเดลจะย้อนกลับไปใช้ CPU ซึ่งช้ากว่าแต่ยังทำงานได้

### ทำไมต้องเลือกโมเดล Hugging Face?

Hugging Face มีคอลเลกชันขนาดใหญ่ของ LLM ที่พร้อมใช้ โดยการชี้ไปที่ `Qwen/Qwen2.5-3B-Instruct-GGUF` คุณจะได้โมเดลขนาดกะทัดรัดที่ปรับตามคำสั่งซึ่งสามารถเพิ่มเครื่องหมายวรรคตอน แก้ไขการเว้นวรรค และแม้กระทั่งแก้ไขข้อผิดพลาด OCR เล็กน้อย นี่คือแก่นของการ **ใช้โมเดล hugging face** ในการปฏิบัติ

## ขั้นตอนที่ 3: เริ่มต้น AI Engine และเปิดใช้งานการประมวลผลต่อเนื่องเพื่อเพิ่มเครื่องหมายวรรคตอน  

AI engine ไม่ได้มีไว้เพียงการสนทนาที่หรูหรา—ที่นี่เราติดตั้ง *punctuation adder* เพื่อทำความสะอาดผลลัพธ์ OCR ดิบ

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*เกิดอะไรขึ้น?* การเรียก `set_post_processor` ลงทะเบียน post‑processor ในตัวที่ทำงานหลังจาก OCR engine เสร็จ มันรับสตริงดิบและแทรกเครื่องหมายจุลภาค จุด และตัวอักษรพิมพ์ใหญ่ในตำแหน่งที่ควรจะเป็น ทำให้ข้อความสุดท้ายอ่านง่ายขึ้นมาก

## ขั้นตอนที่ 4: สร้าง OCR Engine และเชื่อมต่อ AI Engine  

การเชื่อมต่อ AI engine กับ OCR engine ทำให้เราได้อ็อบเจ็กต์เดียวที่สามารถอ่านอักขระและทำให้ผลลัพธ์เรียบเนียนขึ้น

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

หากคุณข้ามขั้นตอนนี้ OCR จะยังทำงานได้ แต่คุณจะเสียการเพิ่มเครื่องหมายวรรคตอน—ทำให้ผลลัพธ์ดูเหมือนสตรีมของคำต่อเนื่อง

## ขั้นตอนที่ 5: ประมวลผลทุกภาพในโฟลเดอร์  

นี่คือหัวใจของบทแนะนำ เราวนลูปผ่านแต่ละภาพ รัน OCR ใช้ post‑processor แล้วเขียนข้อความที่ทำความสะอาดแล้วลงไฟล์ `.txt` ข้างๆ

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### สิ่งที่คาดว่าจะได้

การรันสคริปต์จะแสดงผลประมาณ:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

แต่ละบรรทัดบอกคะแนนความเชื่อมั่น (การตรวจสอบสุขภาพอย่างรวดเร็ว) และสร้างไฟล์ `invoice_001.png.txt`, `receipt_2024.tif.txt` เป็นต้น ที่มีข้อความที่มีเครื่องหมายวรรคตอนและอ่านง่ายเหมือนมนุษย์

### กรณีขอบและการปรับเปลี่ยน

- **การสแกนที่ไม่ใช่ภาษาอังกฤษ**: เปลี่ยน `hugging_face_repo_id` ไปยังโมเดลหลายภาษา (เช่น `microsoft/Multilingual-LLM-GGUF`)  
- **แบชขนาดใหญ่**: ห่อวงวนลูปด้วย `concurrent.futures.ThreadPoolExecutor` เพื่อประมวลผลแบบขนาน แต่ต้องระวังขีดจำกัดหน่วยความจำ GPU  
- **การประมวลผลต่อเนื่องแบบกำหนดเอง**: แทนที่ `"punctuation_adder"` ด้วยสคริปต์ของคุณเองหากต้องการทำความสะอาดเฉพาะโดเมน (เช่น การลบหมายเลขใบแจ้งหนี้)

## ขั้นตอนที่ 6: ทำความสะอาดทรัพยากร  

เมื่องานเสร็จ การปล่อยทรัพยากรช่วยป้องกันการรั่วไหลของหน่วยความจำ ซึ่งสำคัญอย่างยิ่งหากคุณรันนี้ในบริการที่ทำงานต่อเนื่อง

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

การละเลยขั้นตอนนี้อาจทำให้หน่วยความจำ GPU ค้างอยู่ ซึ่งจะทำให้การรันครั้งต่อไปล้มเหลว

## สรุป: วิธีรัน OCR ตั้งแต่ต้นจนจบ  

ในไม่กี่บรรทัด เราได้แสดง **วิธีรัน OCR** บนโฟลเดอร์ของการสแกน, **ใช้โมเดล Hugging Face** ที่ดาวน์โหลดตัวเองครั้งแรก, และ **จดจำข้อความจากการสแกน** พร้อมเครื่องหมายวรรคตอนที่เพิ่มโดยอัตโนมัติ สคริปต์เต็มพร้อมคัดลอก‑วาง ปรับเส้นทางของคุณ แล้วรันได้เลย

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง  

- **การประมวลผลต่อเนื่องเป็นชุด**: สำรวจ `ocr_engine.run_batch_postprocessor` เพื่อการจัดการแบบกลุ่มที่เร็วขึ้น  
- **โมเดลทางเลือก**: ลองใช้ตระกูล `openai/whisper` หากคุณต้องการ speech‑to‑text ควบคู่กับ OCR  
- **การรวมกับฐานข้อมูล**: เก็บข้อความที่สกัดออกใน SQLite หรือ Elasticsearch เพื่อทำคลังข้อมูลที่ค้นหาได้  

อย่าลังเลที่จะทดลอง—เปลี่ยนโมเดล ปรับ `gpu_layers` หรือเพิ่ม post‑processor ของคุณเอง ความยืดหยุ่นของ Aspose OCR ร่วมกับศูนย์โมเดลของ Hugging Face ทำให้เป็นพื้นฐานที่หลากหลายสำหรับโครงการดิจิไทซ์เอกสารใด ๆ  

---  

*ขอให้สนุกกับการเขียนโค้ด! หากเจออุปสรรคใด ๆ ฝากคอมเมนต์ด้านล่างหรือดูเอกสาร Aspose OCR เพื่อดูตัวเลือกการตั้งค่าที่ลึกขึ้น.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}