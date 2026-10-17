---
category: general
date: 2026-06-28
description: เตรียมภาพสำหรับ OCR ด้วยการหมุนอัตโนมัติ, การทำไบนารีและการลดสัญญาณรบกวนใน
  Python. รับผลลัพธ์ JSON ที่มีโครงสร้างโดยใช้เครื่องมือ OCR.
draft: false
keywords:
- preprocess image for OCR
- auto rotate image OCR
- OCR engine Python
- OCR structured JSON output
- image binarization for OCR
- denoise OCR image
language: th
og_description: เตรียมภาพสำหรับ OCR ด้วยการหมุนอัตโนมัติ, การทำไบนารีและการลดสัญญาณรบกวนใน
  Python. เรียนรู้วิธีสกัด JSON ที่มีโครงสร้างโดยใช้เครื่องมือ OCR.
og_title: การเตรียมภาพสำหรับ OCR – คู่มือ Python ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
    text: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
  - name: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
    text: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
  - name: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
    text: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
  - name: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
    text: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
  - name: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
    text: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: การเตรียมภาพสำหรับ OCR – คู่มือ Python ฉบับสมบูรณ์
url: /th/python/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocess Image for OCR – คู่มือ Python ฉบับสมบูรณ์

Ever wondered how to **preprocess image for OCR** so the engine actually reads what you see? You’re not alone—most developers hit the same wall when their scanned documents come out garbled. The good news? A few well‑placed steps—auto‑rotate, binarization, and denoising—can turn a messy photo into clean, machine‑readable text.

เคยสงสัยไหมว่า **preprocess image for OCR** อย่างไรให้เครื่องอ่านได้ตามที่คุณเห็น? คุณไม่ได้เป็นคนเดียว—นักพัฒนาส่วนใหญ่เจอปัญหาเดียวกันเมื่อเอกสารสแกนออกมาดูเป็นอักขระผสมกัน ข่าวดีคือ? ขั้นตอนไม่กี่ขั้นตอนที่วางอย่างเหมาะ—auto‑rotate, binarization, และ denoising—สามารถเปลี่ยนรูปภาพที่รกเป็นข้อความที่เครื่องอ่านได้อย่างสะอาด

In this tutorial we’ll walk through a **Python** workflow that not only cleans the image but also hands you back a nicely structured JSON file. By the end you’ll know how to auto‑rotate an image for OCR, apply image binarization for OCR, and even denoise OCR image data before feeding it to an **OCR engine Python** instance.

ในบทแนะนำนี้ เราจะพาไปผ่าน workflow **Python** ที่ไม่เพียงทำความสะอาดภาพเท่านั้น แต่ยังส่งคืนไฟล์ JSON ที่จัดโครงสร้างอย่างดีให้คุณ เมื่อจบคุณจะรู้วิธี auto‑rotate ภาพสำหรับ OCR, ใช้ image binarization สำหรับ OCR, และแม้กระทั่ง denoise ข้อมูลภาพ OCR ก่อนส่งให้กับ **OCR engine Python** instance.

## สิ่งที่คุณต้องมี

- Python 3.9+ (เวอร์ชันล่าสุดใดก็ได้ที่ทำงานได้)
- `Pillow` สำหรับการจัดการภาพ (`pip install pillow`)
- `ocrutil` – ไลบรารียูทิลิตี้สมมติที่ห่อหุ้ม OCR engine (ติดตั้งโดยใช้ `pip install ocrutil`)
- ภาพตัวอย่างที่เอียง (`skewed.jpg`) ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงได้

That’s it—no heavyweight frameworks, no GPU magic. Just plain‑vanilla Python and a couple of handy libraries.

เท่านี้—ไม่มีเฟรมเวิร์กหนักๆ, ไม่มีการใช้ GPU แต่อย่างใด เพียงแค่ Python ธรรมดาและไลบรารีที่สะดวกสองสามตัว

## ขั้นตอนที่ 1: โหลดภาพของคุณ – เตรียมพร้อมสำหรับ OCR

First thing’s first: we need an image object that the rest of the pipeline can chew on.

สิ่งแรกที่ต้องทำคือ: เราต้องการอ็อบเจกต์ภาพที่ pipeline ส่วนอื่นสามารถประมวลผลต่อได้.

```python
from PIL import Image
import ocrutil

# Load the image you want to process
img_path = "YOUR_DIRECTORY/skewed.jpg"
img = Image.open(img_path)          # Pillow gives us a convenient Image object
print(f"Loaded image size: {img.size}")
```

*ทำไมเรื่องนี้ถึงสำคัญ:* การโหลดภาพด้วย Pillow ทำให้เรารักษาข้อมูลพิกเซลดั้งเดิมทั้งหมดไว้ ซึ่งเป็นสิ่งสำคัญเมื่อเรานำไปทำ binarization ต่อไป การข้ามขั้นตอนนี้หรือใช้ตัวโหลดคุณภาพต่ำอาจทำให้ความแม่นยำของ OCR เสียหายได้

## ขั้นตอนที่ 2: Auto‑rotate ภาพสำหรับ OCR (auto rotate image OCR)

A photo taken with a phone is often tilted or even upside‑down. The `ocrutil.auto_rotate` helper detects the text baseline and rotates the image accordingly.

ภาพที่ถ่ายด้วยโทรศัพท์มักจะเอียงหรือแม้กระทั่งกลับหัว ตัวช่วย `ocrutil.auto_rotate` จะตรวจจับ baseline ของข้อความและหมุนภาพให้ตรงตามนั้น

```python
# Automatically correct 90°/180° rotation
img = ocrutil.auto_rotate(img)
print("Auto‑rotation applied.")
```

*เคล็ดลับ:* หากคุณทราบว่าเอกสารของคุณมักอยู่ในตำแหน่งตั้งตรงเสมอ คุณสามารถข้ามขั้นตอนนี้ได้ แต่ในสถานการณ์จริง “auto rotate image OCR” จะช่วยคุณประหยัดการทำความสะอาดด้วยมือมาก

## ขั้นตอนที่ 3: Preprocess Image for OCR – Binarization + Denoising

Now we get to the heart of the matter: **preprocess image for OCR**. The two most effective tricks are:

ตอนนี้เรามาถึงหัวใจของเรื่อง: **preprocess image for OCR**. สองเทคนิคที่มีประสิทธิภาพที่สุดคือ:

1. **Binarization** – การแปลงภาพเป็นสีขาว‑ดำบริสุทธิ์ ซึ่งทำให้ขอบอักขระคมชัดขึ้น
2. **Denoising** – การกำจัดจุดรบกวนที่ OCR engine อาจสับสนเป็น glyphs

```python
# Apply preprocessing: binarization + denoising
img = ocrutil.preprocess(img)   # Under the hood: thresholding + median filter
print("Preprocessing completed.")
```

If you peek at the image after this step (e.g., `img.show()`), you’ll notice a stark contrast with the background—exactly what a good OCR engine craves.

หากคุณดูภาพหลังจากขั้นตอนนี้ (เช่น `img.show()`), คุณจะสังเกตเห็นความคอนทราสต์ที่ชัดเจนกับพื้นหลัง—สิ่งที่ OCR engine ที่ดีต้องการอย่างยิ่ง

## ขั้นตอนที่ 4: ตั้งค่า OCR Engine (OCR engine Python)

With a clean image in hand, we instantiate the OCR engine. The `ocrutil.OcrEngine` class wraps a popular open‑source OCR backend (think Tesseract) while exposing a friendly Python API.

เมื่อมีภาพที่สะอาดแล้ว เราจะสร้างอินสแตนซ์ของ OCR engine. คลาส `ocrutil.OcrEngine` ห่อหุ้ม backend OCR โอเพ่นซอร์สที่เป็นที่นิยม (เช่น Tesseract) พร้อมเปิดเผย API ของ Python ที่เป็นมิตร

```python
# Create and configure the OCR engine
engine = ocrutil.OcrEngine()
engine.set_image(img)           # Feed the preprocessed image
print("Engine ready for recognition.")
```

*ทำไมเราต้องทำเช่นนี้:* การส่งภาพที่ผ่านการ preprocess ให้กับอ็อบเจกต์ **OCR engine Python** รับประกันว่า engine จะทำงานกับข้อมูลคุณภาพสูงสุดที่คุณสามารถให้ได้ ซึ่งแปลตรงไปยังความแม่นยำที่สูงขึ้น

## ขั้นตอนที่ 5: การจดจำข้อความแบบ Plain‑text (Optional but Handy)

Sometimes you just need the raw text. This step is optional because the main goal of the tutorial is structured output, but it’s useful for quick sanity checks.

บางครั้งคุณอาจต้องการข้อความดิบเท่านั้น ขั้นตอนนี้เป็น optional เนื่องจากเป้าหมายหลักของบทแนะนำคือผลลัพธ์ที่มีโครงสร้าง, แต่ก็มีประโยชน์สำหรับการตรวจสอบอย่างรวดเร็ว

```python
# Get plain text (useful for debugging)
plain_text = engine.recognize()
print("Plain‑text output:\n", plain_text[:200])   # Print first 200 chars
```

You’ll see a string that looks like the original document, albeit without any layout information. If the text looks garbled, go back and tweak the preprocessing parameters.

คุณจะเห็นสตริงที่ดูเหมือนเอกสารต้นฉบับ แม้จะไม่มีข้อมูลเลย์เอาต์ใด ๆ หากข้อความดูเป็นอักขระผสมกัน ให้กลับไปปรับพารามิเตอร์ของการ preprocess

## ขั้นตอนที่ 6: ดึงข้อมูลเชิงโครงสร้างและบันทึกเป็น JSON (OCR structured JSON output)

The real power of modern OCR engines is their ability to return layout information—tables, columns, and even form fields. `engine.recognize_structured()` does exactly that, and we’ll dump the result into a tidy JSON file.

พลังที่แท้จริงของ OCR engine สมัยใหม่คือความสามารถในการคืนข้อมูลเลย์เอาต์—ตาราง, คอลัมน์, และแม้กระทั่งฟิลด์ฟอร์ม `engine.recognize_structured()` ทำเช่นนั้นอย่างแม่นยำ และเราจะบันทึกผลลัพธ์ลงในไฟล์ JSON ที่เป็นระเบียบ

```python
# Recognize structured data (tables, layout) and export to JSON
structured_result = engine.recognize_structured()
output_path = "YOUR_DIRECTORY/out.json"
ocrutil.save_result(structured_result, output_path)
print(f"Structured OCR result saved to {output_path}")
```

A snippet of the JSON might look like this:

ตัวอย่างส่วนหนึ่งของ JSON อาจมีลักษณะดังนี้:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "type": "text",
          "bbox": [12, 34, 560, 120],
          "text": "Invoice #12345"
        },
        {
          "type": "table",
          "bbox": [15, 130, 580, 400],
          "rows": [
            ["Item", "Qty", "Price"],
            ["Widget A", "2", "$19.99"]
          ]
        }
      ]
    }
  ]
}
```

*สิ่งที่คุณจะได้:* ตัวแทนข้อมูลที่เครื่องอ่านได้ซึ่งคุณสามารถส่งต่อโดยตรงไปยังฐานข้อมูล, API, หรือเครื่องมือรายงาน—ไม่ต้องคัดลอก‑วางด้วยมืออีกต่อไป

## โบนัส: การยืนยันด้วยภาพ (Image with Alt Text)

Below is a before‑and‑after snapshot of the preprocessing pipeline. Notice how the contrast spikes and the noise disappears.

ด้านล่างเป็นภาพก่อน‑และ‑หลังของ pipeline การ preprocess. สังเกตว่าคอนทราสต์เพิ่มขึ้นและสัญญาณรบกวนหายไป.

![Preprocess image for OCR – ดั้งเดิม vs ทำความสะอาด](/images/ocr_preprocess_example.png){: .align-center alt="preprocess image for OCR ตัวอย่าง"}

*หากคุณสนใจ:* แทนที่ `ocrutil.preprocess` ด้วย routine ของ OpenCV ของคุณเองและคุณยังคงปฏิบัติตามปรัชญา **preprocess image for OCR** เดียวกัน—threshold, filter, แล้วจึงส่งต่อ

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

- **Over‑binarizing:** การตั้งค่า threshold สูงเกินไปอาจลบอักขระที่จางหายไป หากคุณเห็นตัวอักษรหาย ให้ลด threshold ใน `ocrutil.preprocess`
- **Wrong DPI:** OCR engine สมมติว่ามีความละเอียดประมาณ ~300 dpi สำหรับเอกสารพิมพ์ หากภาพของคุณความละเอียดต่ำ ควรอัปสเกลก่อนทำ preprocessing
- **Skipping auto‑rotate:** แม้การเอียง 5 องศาก็อาจทำให้การตรวจจับบรรทัดผิดพลาด ขั้นตอน “auto rotate image OCR” มีต้นทุนต่ำและช่วยประหยัดเวลาการดีบักหลายชั่วโมงในภายหลัง

## การขยาย Workflow

Now that you have a solid baseline, you might want to:

เมื่อคุณมีพื้นฐานที่มั่นคงแล้ว คุณอาจต้องการ:

1. **Add language packs** (`engine.set_language('eng+spa')`) สำหรับเอกสารหลายภาษา  
2. **Integrate with Pandas** เพื่อแปลงตาราง JSON เป็น DataFrames สำหรับการวิเคราะห์  
3. **Run batch processing** โดยวนลูปผ่านโฟลเดอร์ของภาพและเพิ่มผลลัพธ์ลงในไฟล์ JSON หลัก  

All of these extensions still rely on the core idea: **preprocess image for OCR** before you ever call the engine.

ส่วนขยายทั้งหมดนี้ยังคงอิงแนวคิดหลัก: **preprocess image for OCR** ก่อนที่คุณจะเรียก engine

## สรุป

You’ve just learned how to **preprocess image for OCR** in Python—auto‑rotate, binarize, denoise, and finally hand the clean picture to an **OCR engine Python** that spits out both plain text and a rich **OCR structured JSON output**. By following these steps, you’ll dramatically improve recognition rates and get data that’s ready for downstream processing.

คุณเพิ่งเรียนรู้วิธี **preprocess image for OCR** ด้วย Python—auto‑rotate, binarize, denoise, และสุดท้ายส่งภาพที่สะอาดให้กับ **OCR engine Python** ที่จะให้ผลลัพธ์เป็นทั้งข้อความธรรมดาและ **OCR structured JSON output** ที่สมบูรณ์ การทำตามขั้นตอนเหล่านี้จะทำให้คุณเพิ่มอัตราการจดจำอย่างมากและได้ข้อมูลที่พร้อมสำหรับการประมวลผลต่อไป

Ready to level up? Try swapping the built‑in `ocrutil.preprocess` with a custom OpenCV pipeline, experiment with different binarization techniques, or feed the JSON into a reporting dashboard. The sky’s the limit, and the foundation you just built will keep you from stumbling over the same image‑quality issues again.

พร้อมจะก้าวต่อไหม? ลองเปลี่ยน `ocrutil.preprocess` ที่มาพร้อมกับระบบเป็น pipeline OpenCV ที่กำหนดเอง, ทดลองเทคนิค binarization ต่าง ๆ, หรือส่ง JSON ไปยังแดชบอร์ดรายงาน. ไม่มีขีดจำกัด, และพื้นฐานที่คุณสร้างขึ้นจะช่วยให้คุณหลีกเลี่ยงปัญหาคุณภาพภาพเดิมได้อีกต่อไป

Happy coding, and may your OCR results be ever crisp!

ขอให้เขียนโค้ดอย่างสนุกสนาน, และผลลัพธ์ OCR ของคุณเต็มไปด้วยความคมชัด!

## สิ่งที่คุณควรเรียนต่อไป?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโปรเจกต์ของคุณ

- [ดึงข้อความจากภาพด้วย Aspose OCR – คู่มือขั้นตอนโดยละเอียด](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [ดึงข้อความจากภาพ – การปรับแต่ง OCR ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)
- [วิธีตั้งค่า Threshold Value ในการจดจำภาพ OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}