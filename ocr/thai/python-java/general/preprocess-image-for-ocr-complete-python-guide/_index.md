---
category: general
date: 2026-06-28
description: ทำการเตรียมภาพสำหรับ OCR ด้วย Python เพื่อเพิ่มความแม่นยำ เรียนรู้กระบวนการเตรียมภาพอย่างเต็มรูปแบบ
  ปรับปรุงผลลัพธ์ของ OCR และสกัดข้อความจากภาพที่เป็นภาษาซิริลิก
draft: false
keywords:
- preprocess image for OCR
- how to improve OCR accuracy
- python OCR with preprocessing
- image preprocessing pipeline python
- extract text from Cyrillic image
language: th
og_description: ทำการเตรียมภาพสำหรับ OCR ด้วย Python และเรียนรู้วิธีเพิ่มความแม่นยำของ
  OCR คู่มือนี้จะพาคุณผ่านกระบวนการเตรียมภาพอย่างครบถ้วนและการสกัดข้อความจากภาพที่เป็นอักษรซีริลลิก
og_title: การประมวลผลล่วงหน้าภาพสำหรับ OCR – บทเรียน Python ฉบับเต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the code works on 3.10+ as well). - Basic familiarity
      with Python packages and virtual environments. - An OCR library that provides
      `OcrEngine`, `Language`, and `ImagePreprocessor` classes (e.g., a wrapper around
      Tesseract or a commercial SDK). - A sample Cyrillic image (`cyri'
  - name: Why These Three Steps?
    text: 1. **Deskew** – OCR engines assume left‑to‑right (or top‑to‑bottom) alignment.
      A few degrees of rotation can drop accuracy by 30 % or more. 2. **Binarize**
      – Converting to a binary image reduces the data the OCR engine must analyze,
      sharpening character edges. 3. **Denoise** – Small specks or compre
  - name: How This Improves OCR Accuracy
    text: '- By feeding a **clean, deskewed, binarized** image, the engine can focus
      on character shapes rather than fighting noise. - Specifying `Language.Cyrillic`
      activates the correct character set and language model, which is a key factor
      in **how to improve OCR accuracy** for non‑Latin scripts.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: การเตรียมภาพสำหรับ OCR – คู่มือ Python ฉบับสมบูรณ์
url: /th/python-java/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การเตรียมภาพสำหรับ OCR – คู่มือ Python ฉบับสมบูรณ์

เคยสงสัยไหมว่าการ **preprocess image for OCR** อย่างไรจึงทำให้ข้อความออกมาชัดเจนเหมือนคริสตัล? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเมื่อเครื่อง OCR แสดงผลอักขระที่บิดเบือน โดยเฉพาะกับสแกน Cyrillic ที่เอียงหรือมีเสียงรบกวน ข่าวดีคือ pipeline การเตรียมภาพที่ออกแบบดีสามารถเพิ่มอัตราการจดจำได้อย่างมาก

ในบทเรียนนี้เราจะดำดิ่งสู่โซลูชัน **Python OCR with preprocessing** ที่จัดการกับการแก้เอียง (deskewing), การทำเป็นสีทึบ (binarization) และการลดสัญญาณรบกวน (denoising) จากนั้นจะแสดงวิธี **extract text from Cyrillic image** ไฟล์ต่าง ๆ เมื่อจบคุณจะมีสคริปต์ที่นำกลับมาใช้ใหม่ได้ เข้าใจ **how to improve OCR accuracy** และพร้อมปรับ pipeline ให้เข้ากับภาษา หรือแหล่งภาพใดก็ได้

## สิ่งที่คุณจะได้เรียนรู้

- เหตุผลเบื้องหลังแต่ละขั้นตอนการเตรียมภาพและทำไมจึงสำคัญต่อ OCR
- วิธีประกอบ **image preprocessing pipeline python** ที่สามารถนำกลับมาใช้ใหม่ในหลายโครงการ
- ตัวอย่างครบถ้วนที่สามารถรันได้ซึ่งสร้าง OCR engine, เตรียมภาพ Cyrillic, และพิมพ์ข้อความที่จดจำได้
- เคล็ดลับการจัดการกับกรณีขอบเช่นการเอียงมาก, คอนทราสต์ต่ำ, หรือเอกสารหลายภาษา
- ไอเดียขั้นต่อไป เช่น การประมวลผลเป็นชุด, แพ็คภาษาที่กำหนดเอง, และการรวมกับบริการ OCR บนคลาวด์

### ข้อกำหนดเบื้องต้น

- Python 3.8 หรือใหม่กว่า (โค้ดทำงานบน 3.10+ ด้วย)
- ความคุ้นเคยพื้นฐานกับแพ็กเกจ Python และ virtual environments
- ไลบรารี OCR ที่มีคลาส `OcrEngine`, `Language`, และ `ImagePreprocessor` (เช่น wrapper ของ Tesseract หรือ SDK เชิงพาณิชย์)  
- ตัวอย่างภาพ Cyrillic (`cyrillic_skewed.jpg`) ที่วางไว้ในโฟลเดอร์ที่คุณควบคุม

> **Pro tip:** หากคุณยังไม่มี wrapper OCR ที่พร้อมใช้ ให้ลองดูแพ็กเกจโอเพ่นซอร์ส `pytesseract` แล้วจับคู่กับ `opencv-python` แนวคิดในคู่มือนี้สามารถนำไปใช้ได้โดยตรง

---

## ขั้นตอนที่ 1: ติดตั้งและนำเข้าแพ็กเกจที่จำเป็น

ก่อนอื่นให้จัดการกับ dependencies ก่อน เราจะใช้ `ocr_lib` สมมติที่รวม engine และ utilities สำหรับการเตรียมภาพ หากคุณใช้ `pytesseract` + OpenCV ให้เปลี่ยน import ตามนั้น

```python
# Install the (fictional) OCR library – replace with your actual package manager command
# pip install ocr-lib

from ocr_lib import OcrEngine, Language, ImagePreprocessor
import os
```

> **Why this matters:** การนำเข้าคลาสที่ถูกต้องทำให้เรามีการแยกส่วนที่ชัดเจนระหว่าง OCR engine (การจดจำ) กับ image pre‑processor (การปรับปรุง) การผสมกันอาจทำให้โค้ดพันกันและแก้บั๊กยาก

---

## ขั้นตอนที่ 2: สร้าง **Preprocess Image for OCR** Pipeline

ตอนนี้เราจะสร้างหัวใจของบทเรียน: pipeline ที่ทำการแก้เอียง, ทำเป็นสีทึบ, และลดสัญญาณรบกวนแต่ละการแปลงมุ่งเป้าไปที่จุดอ่อนเฉพาะของ OCR engine

```python
# Step 2: Initialise the pre‑processing chain
preprocessor = ImagePreprocessor()

# Deskew – correct rotation so text lines are horizontal
preprocessor = preprocessor.deskew()

# Binarize – convert to pure black‑and‑white using a threshold (180 works well for most scans)
preprocessor = preprocessor.binarize(threshold=180)

# Remove noise – apply a mild median filter (strength=2) to smooth speckles
preprocessor = preprocessor.removeNoise(strength=2)
```

### ทำไมต้องใช้สามขั้นตอนนี้?

1. **Deskew** – OCR engine สมมติว่าข้อความจัดเรียงจากซ้ายไปขวา (หรือจากบนลงล่าง) การหมุนเพียงไม่กี่องศาอาจทำให้ความแม่นยำลดลง 30 % หรือมากกว่า
2. **Binarize** – การแปลงเป็นภาพสีทึบลดข้อมูลที่ OCR engine ต้องวิเคราะห์ ทำให้ขอบอักขระคมชัดขึ้น
3. **Denoise** – จุดรบกวนหรือ artefacts จากการบีบอัดอาจถูกตีความเป็นเครื่องหมายวรรคตอนหรือ diacritic โดยเฉพาะใน Cyrillic ที่หลายตัวอักษรมีรูปร่างคล้ายกัน

> **Edge case note:** หากภาพต้นทางของคุณสะอาดอยู่แล้ว คุณสามารถข้าม `removeNoise` หรือปรับค่าพารามิเตอร์ `strength` ให้ต่ำลง การลดสัญญาณรบกวนอย่างเกินไปอาจลบรายละเอียดสำคัญเช่นจุด diacritic

---

## ขั้นตอนที่ 3: โหลดภาพและใช้ Pipeline

เมื่อ pipeline พร้อม เราจะส่งพาธไฟล์เข้าไป เมธอด `apply` จะคืนอ็อบเจกต์ภาพที่ผ่านการประมวลผลซึ่ง OCR engine สามารถรับได้โดยตรง

```python
# Path to the original Cyrillic image (adjust as needed)
image_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")

# Run the preprocessing pipeline
processed_image = preprocessor.apply(image_path)
```

หากต้องการพรีวิวผลลัพธ์ คุณสามารถบันทึกลงดิสก์ได้:

```python
# Optional: save the preprocessed image for visual verification
processed_image.save("preprocessed_cyrillic.jpg")
print("Preprocessed image saved – check the file to confirm deskewing and binarization.")
```

> **Why preview?** การเห็นภาพที่แปลงแล้วช่วยให้คุณปรับค่า threshold ได้อย่างละเอียด บางครั้ง threshold ที่ 180 อาจแรงเกินไป; ลดลงเป็น 150 อาจช่วยรักษาเส้นที่อ่อนแอไว้ได้

---

## ขั้นตอนที่ 4: ตั้งค่า OCR Engine และจดจำข้อความ

ต่อไปเราจะเปลี่ยนไปที่ส่วน OCR จริง เราจะตั้งค่า engine ให้ใช้ Cyrillic language pack ซึ่งจำเป็นสำหรับ **extract text from Cyrillic image** ไฟล์

```python
# Initialise the OCR engine
engine = OcrEngine()

# Tell the engine we’re working with Cyrillic text
engine.setLanguage(Language.Cyrillic)

# Perform recognition on the preprocessed image
ocr_result = engine.recognizeImage(processed_image)

# Extract plain text from the OCR result object
recognized_text = ocr_result.getText()
print("=== Recognized Text ===")
print(recognized_text)
```

### How This Improves OCR Accuracy

- ด้วยการป้อนภาพ **clean, deskewed, binarized** engine สามารถมุ่งเน้นที่รูปร่างของอักขระแทนการต่อสู้กับสัญญาณรบกวน
- การระบุ `Language.Cyrillic` เปิดใช้งานชุดอักขระและโมเดลภาษาที่ถูกต้อง ซึ่งเป็นปัจจัยสำคัญใน **how to improve OCR accuracy** สำหรับสคริปต์ที่ไม่ใช่ละติน

---

## ขั้นตอนที่ 5: ห่อทุกอย่างเป็นฟังก์ชันที่นำกลับมาใช้ใหม่ (ทางเลือก)

หากคุณวางแผนจะประมวลผลหลายไฟล์ การห่อโลจิกไว้ในฟังก์ชันทำให้โค้ดสะอาดและบำรุงรักษาง่ายขึ้น

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Preprocess an image and extract Cyrillic text using the OCR engine.

    Parameters
    ----------
    image_path : str
        Full path to the source image.

    Returns
    -------
    str
        Recognized Cyrillic text.
    """
    # Build the preprocessing pipeline (could be cached for performance)
    preprocessor = (ImagePreprocessor()
                    .deskew()
                    .binarize(threshold=180)
                    .removeNoise(strength=2))

    processed = preprocessor.apply(image_path)

    engine = OcrEngine()
    engine.setLanguage(Language.Cyrillic)

    result = engine.recognizeImage(processed)
    return result.getText()


# Example usage
if __name__ == "__main__":
    sample_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")
    text = extract_cyrillic_text(sample_path)
    print("Extracted Cyrillic text:")
    print(text)
```

> **Why a function?** ฟังก์ชันแยกโลจิกการเตรียมภาพออก ทำให้เปลี่ยนภาษาอื่นหรือปรับพารามิเตอร์ได้โดยไม่ต้องเขียนสคริปต์ใหม่ทั้งหมด

---

## Common Pitfalls and How to Tackle Them

| ปัญหา | อาการ | วิธีแก้ |
|-------|----------|-----|
| **Extreme skew (>15°)** | ข้อความดูบิดเบือนหรือหายไป | เพิ่มความทนทานของ `deskew()` หรือทำการหมุนล่วงหน้าด้วย `getRotationMatrix2D` ของ OpenCV |
| **Low contrast** | การทำสีทึบทำให้ทุกอย่างเป็นสีขาว | ลดค่า `threshold` หรือทำขั้นตอนการขยายคอนทราสต์ก่อน `binarize()` |
| **Small font size** | ตัวอักษรรวมกันหลังทำสีทึบ | ใช้ภาพต้นฉบับความละเอียดสูงขึ้น หรือใช้ Gaussian blur เบา ๆ ก่อน threshold |
| **Multiple languages** | ตัวอักษร Cyrillic ไม่อ่านออก | ตั้งค่า `engine.setLanguage([Language.Cyrillic, Language.English])` หากไลบรารีรองรับโหมดหลายภาษา |
| **Unsupported image format** | `apply()` เกิดข้อผิดพลาด | แปลงภาพเป็น PNG หรือ JPEG ก่อนด้วย Pillow (`Image.open().convert('RGB')`) |

---

## Extending the **Image Preprocessing Pipeline Python** Approach

1. **Batch Processing** – วนลูปผ่านไดเรกทอรีของภาพและบันทึกผลลัพธ์แต่ละไฟล์ในไฟล์ CSV
2. **Parallel Execution** – ใช้ `concurrent.futures.ThreadPoolExecutor` เพื่อเร่งความเร็วงานขนาดใหญ่
3. **Custom Filters** – เพิ่มการดำเนินการ morphological (`erode`, `dilate`) สำหรับแบบฟอร์มพิมพ์
4. **Cloud OCR Integration** – แทนที่ `OcrEngine` ด้วยไคลเอนต์ API (Google Vision, Azure Computer Vision) ขณะยังคงใช้ขั้นตอนการเตรียมภาพเดียวกัน

```python
# Example of batch processing with ThreadPoolExecutor
from concurrent.futures import ThreadPoolExecutor, as_completed

def batch_extract(folder: str):
    files = [os.path.join(folder, f) for f in os.listdir(folder) if f.lower().endswith('.jpg')]
    results = {}

    with ThreadPoolExecutor(max_workers=4) as executor:
        future_to_file = {executor.submit(extract_cyrillic_text, f): f for f in files}
        for future in as_completed(future_to_file):
            file_path = future_to_file[future]
            try:
                results[file_path] = future.result()
            except Exception as exc:
                results[file_path] = f"Error: {exc}"
    return results
```

---

## Visual Summary

![preprocess image for OCR example](/images/ocr_preprocess_example.png "แผนภาพแสดง pipeline การเตรียมภาพสำหรับ OCR: deskew → binarize → denoise → OCR engine")

*แผนภาพนี้แสดงแต่ละขั้นตอนของ workflow **preprocess image for OCR** ตั้งแต่สแกนดิบจนถึงผลลัพธ์ข้อความขั้นสุดท้าย*

---

## Conclusion

เราได้เดินผ่านโซลูชัน **preprocess image for OCR** อย่างครบถ้วนใน Python ตั้งแต่การติดตั้งแพ็กเกจที่จำเป็น ไปจนถึงการสร้าง **image preprocessing pipeline python** ที่แข็งแรงและสุดท้าย **extract text from Cyrillic image** ไฟล์ต่าง ๆ ด้วยการทำ deskew, binarize, และ denoise ก่อนส่งภาพให้ OCR engine คุณจะเห็นการเพิ่มขึ้นอย่างชัดเจนของ **how to improve OCR accuracy** โดยเฉพาะสำหรับสคริปต์ Cyrillic ที่ท้าทาย

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองสลับโมเดลภาษาเป็น Arabic, ทดลอง adaptive thresholding, หรือเชื่อม pipeline กับ Flask API เพื่อประมวลผลเอกสารแบบเรียลไทม์ ไม่ว่าคุณจะทำอะไร ฐานความรู้นี้จะทำให้คุณแปลงสแกนที่รกเป็นข้อความที่สะอาดและค้นหาได้ง่าย

Happy coding, and may your OCR results be ever crystal‑clear!

## สิ่งที่คุณควรเรียนต่อ

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบต่าง ๆ ในโปรเจกต์ของคุณ

- [สกัดข้อความจากภาพด้วย Aspose OCR – คู่มือขั้นตอนโดยละเอียด](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [คำนวณมุมเอียงสำหรับการเตรียมภาพ OCR](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [วิธีตั้งค่า Threshold Value ในการจดจำภาพ OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}