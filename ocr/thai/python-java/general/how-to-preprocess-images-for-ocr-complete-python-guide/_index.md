---
category: general
date: 2026-06-06
description: วิธีการเตรียมภาพล่วงหน้าสำหรับ OCR ด้วย Python เรียนรู้การทำไบนาไรซ์ภาพด้วย
  Otsu วิธีการแก้เอียงเอกสารสแกน และเพิ่มความแม่นยำของ OCR สำหรับข้อความภาษาเยอรมัน
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: th
og_description: วิธีการเตรียมภาพล่วงหน้าสำหรับ OCR ด้วย Python บทเรียนนี้แสดงการทำให้ภาพเป็นสีขาว‑ดำด้วยวิธี
  Otsu, วิธีการแก้ไขการเอียงของเอกสารสแกน, และวิธีการปรับปรุงความแม่นยำของ OCR สำหรับภาพภาษาเยอรมัน.
og_title: วิธีเตรียมภาพสำหรับ OCR – คู่มือ Python ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: วิธีเตรียมภาพสำหรับ OCR – คู่มือ Python ฉบับเต็ม
url: /th/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการเตรียมภาพสำหรับ OCR – คู่มือ Python ฉบับสมบูรณ์

เคยสงสัย **วิธีการเตรียมภาพสำหรับ OCR** ว่าจะทำให้ข้อความออกมาชัดเจนเหมือนคริสตัลหรือไม่? คุณไม่ได้เป็นคนเดียว เอกสารสแกน—โดยเฉพาะหน้าภาษาเยอรมันที่มีสัญญาณรบกวน—อาจเป็นฝันร้ายสำหรับเครื่อง OCR ใด ๆ ข่าวดีคือ? ขั้นตอนการเตรียมภาพอัจฉริยะไม่กี่ขั้นตอนสามารถเปลี่ยนสแกนที่เบลอและมีจุดรบกวนให้เป็นภาพที่สะอาดและอ่านได้โดยเครื่อง

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่างเชิงปฏิบัติที่แสดง **วิธีการเตรียมภาพสำหรับ OCR** ด้วย Python คุณจะได้เรียนรู้ **การทำให้ภาพเป็นสีขาวดำด้วย Otsu**, **วิธีการแก้ไขการเอียงของเอกสารสแกน**, และโดยรวม **วิธีการปรับปรุงความแม่นยำของ OCR** เมื่อคุณต้อง **ดึงข้อความจากไฟล์ภาพภาษาเยอรมัน** ไม่มีเนื้อหาเกินความจำเป็น เพียงสคริปต์ทำงานที่คุณสามารถคัดลอก‑วางได้ทันที

## สิ่งที่คุณต้องเตรียม

- **Python 3.9+** (any recent version works)
- ไลบรารี OCR ที่เปิดเผยคลาส `OcrEngine` – สำหรับการสาธิตเราจะสมมติว่าใช้แพคเกจ `ocr` ทั่วไป ติดตั้งด้วย `pip install ocr-lib`.
- สแกนภาษาเยอรมันที่มีสัญญาณรบกวน (`noisy_german_scan.tif`) ที่คุณต้องการทดสอบ
- ความเข้าใจพื้นฐานเกี่ยวกับฟังก์ชัน Python (ถ้าคุณเคยเขียน `def` มาก่อนก็พร้อม)

> **Pro tip:** หากคุณใช้ SDK OCR ตัวอื่น (เช่น Tesseract ผ่าน `pytesseract`) แนวคิดยังคงเหมือนเดิม—เพียงปรับชื่อเมธอดให้ตรง

## ภาพรวมของวิธีแก้ปัญหา

1. **Create an OCR engine instance.**  
2. **Set the recognition language to German.**  
3. **Build a custom preprocessing pipeline** that includes deskewing, denoising, binarization (Otsu), and contrast stretching.  
4. **Attach the pipeline to the engine** so every image passes through it automatically.  
5. **Run the OCR** on a noisy German scan.  
6. **Print the extracted text** to verify the result.

ด้านล่างเราจะอธิบายแต่ละขั้นตอน แสดง **ทำไม** จึงสำคัญ และแสดงโค้ดที่คุณต้องใช้อย่างแม่นยำ

![ตัวอย่างการเตรียมภาพสำหรับ OCR](image.png "ตัวอย่างการเตรียมภาพสำหรับ OCR")

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ของ OCR Engine

First things first—without an engine, nothing happens. The `OcrEngine` object is the entry point that coordinates all later processing.

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Why this matters:* การเริ่มต้น engine จะตั้งค่าทรัพยากรภายใน (เช่นโมเดลภาษา) และให้คุณมีพื้นฐานที่สะอาดเพื่อแนบ pipeline แบบกำหนดเองต่อไป

## ขั้นตอนที่ 2: ตั้งค่าภาษาในการรับรู้เป็นภาษาเยอรมัน

OCR accuracy is heavily language‑dependent. By telling the engine to expect German, you activate the right character set and language model.

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

If you skip this, the engine might default to English, mis‑recognizing umlauts (ä, ö, ü) and the ß character—common pitfalls when dealing with German scans.

## ขั้นตอนที่ 3: สร้าง Pipeline การเตรียมภาพแบบกำหนดเอง

This is the heart of **how to preprocess images for OCR**. We’ll chain four transformations:

| การแปลง | ทำอะไร | ทำไมถึงช่วย |
|----------|--------|--------------|
| **Deskew** | หมุนภาพกลับเป็นแนวนอน (สูงสุด 5°) | สแกนมักไม่ตรงแนวอย่างสมบูรณ์; การแก้เอียงจะลบความเอียงที่ทำให้การแยกอักขระสับสน |
| **Denoise** | ลดจุดรบกวนแบบสุ่ม (strength 0.7) | สัญญาณรบกวนสร้างขอบเท็จที่ OCR อาจตีความเป็นอักขระ |
| **Binarize (Otsu)** | แปลงเป็นสีขาว‑ดำโดยใช้วิธี Otsu | ภาพไบนารีที่สะอาดให้คอนทราสต์ชัดเจนระหว่างพื้นหน้า (ข้อความ) กับพื้นหลัง |
| **Contrast Stretch** | ขยายช่วงไดนามิก | ปรับปรุงการอ่านของเส้นที่อ่อนเฉา โดยเฉพาะในเอกสารเก่า |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### วิธีการแก้ไขการเอียงของเอกสารสแกน

The `deskew` call above is the concrete answer to **how to deskew scanned documents**. Internally it estimates the dominant text line angle via Hough transform and rotates the image back. If your documents are rotated more than 5°, bump `max_angle` up, but beware of over‑rotation artifacts.

### ทำให้ภาพเป็นสีขาวดำโดยใช้ Otsu

The `binarize(method="otsu")` line directly answers the query **binarize image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class variance, which is perfect for documents with bimodal histograms (dark text vs. light background).

## ขั้นตอนที่ 4: แนบ Pipeline ไปยัง Engine

Now we tell the OCR engine to run every incoming image through the pipeline we just built.

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Why this matters:* Without registering, the engine would process the raw scan, ignoring all the cleaning we just configured. This step ensures **how to improve OCR accuracy** by applying the same preprocessing consistently.

## ขั้นตอนที่ 5: รับรู้ข้อความจากสแกนภาษาเยอรมันที่มีสัญญาณรบกวน

Time to put everything together. We feed the engine a noisy German image and let it do the heavy lifting.

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

If you’re curious about performance, you can time the call:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## ขั้นตอนที่ 6: แสดงข้อความที่รับรู้ได้

Finally, we print the extracted string. This is the direct answer to **extract text from german image**.

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### ผลลัพธ์ที่คาดหวัง

Assuming the sample scan contains the sentence “Die schnelle braune Füchsin springt über den faulen Hund.” you should see something like:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

If the output still contains garbled characters, consider tweaking the `denoise` strength or increasing the `max_angle` for deskewing.

## ข้อผิดพลาดทั่วไปและวิธีแก้ไข

- **Missing language model:** ลืมเรียก `set_recognition_language(Language.GERMAN)` มักทำให้ไม่มีอูมลัตต์ ตรวจสอบการเรียกอีกครั้ง
- **Over‑denoising:** ความแรงมากกว่า 0.9 อาจลบเส้นบาง ๆ โดยเฉพาะในฟอนต์เก่า ควรใช้ 0.5‑0.7 สำหรับกรณีส่วนใหญ่
- **Incorrect file format:** OCR บางตัวไม่รองรับ TIFF หลายหน้า หากมีเอกสารหลายหน้าให้แยกเป็นไฟล์หน้าเดียวก่อน
- **Pipeline order:** ลำดับที่แสดง (deskew → denoise → binarize → contrast) มีเหตุผล การทำ binarize ก่อน denoise จะตรึงสัญญาณรบกวนไว้ ควร denoise ก่อนเสมอ

## การขยาย Pipeline (ต่อไปคืออะไร?)

Now that you have a solid baseline, you might want to:

- **Add a morphological opening** to clean tiny blobs (`.morph_open(kernel=3)`).
- **Integrate a language model** for post‑processing correction (`ocr_engine.apply_spellcheck()`).
- **Parallelize batch processing** for large datasets using `concurrent.futures`.

All of these are natural extensions that keep the core idea of **how to preprocess images for OCR** intact while boosting **how to improve OCR accuracy** even further.

## สรุป

We’ve just covered **how to preprocess images for OCR** from start to finish: create an engine, set German language, build a pipeline that **binarize image using Otsu**, **how to deskew scanned documents**, and finally **extract text from german image** with higher confidence. By following the six steps above you’ll see a noticeable jump in recognition quality—no more endless manual corrections.

Give the script a spin with your own scans, experiment with the parameters, and let the results speak for themselves. Got questions about a particular preprocessing tweak? Drop a comment, and we’ll dive deeper together.

Happy coding, and may your OCR be ever accurate!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [สกัดข้อความจากรูปภาพด้วย C# พร้อมเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [วิธีตั้งค่าค่าธรณีใน OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [วิธี OCR รูปภาพ – ทำ OCR บนรูปภาพใน OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}