---
category: general
date: 2026-03-26
description: เรียนรู้วิธีทำ OCR ด้วย Python และจดจำข้อความจากไฟล์รูปภาพ คู่มือนี้แสดงวิธีดึงข้อความจากไฟล์
  PNG และแปลงรูปภาพเป็นข้อความอย่างรวดเร็ว.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: th
og_description: วิธีทำ OCR ด้วย Python? ทำตามคู่มือนี้เพื่อจดจำข้อความจากภาพ, ดึงข้อความจาก
  PNG, และแปลงภาพเป็นข้อความด้วยลิขสิทธิ์ทดลอง.
og_title: วิธีทำ OCR ใน Python – บทเรียนครบถ้วน
tags:
- OCR
- Python
- Image Processing
title: วิธีทำ OCR ด้วย Python – คู่มือขั้นตอนเต็มรูปแบบ
url: /th/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ใน Python – คู่มือขั้นตอนเต็ม  

เคยสงสัย **วิธีทำ OCR** บนรูปภาพที่คุณถ่ายด้วยโทรศัพท์ของคุณหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาทั่วโลกต้องการวิธีที่เชื่อถือได้ในการจดจำข้อความจากไฟล์รูปภาพโดยไม่ต้องต่อสู้กับไลบรารีเนทีฟที่ซับซ้อน  

ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างเชิงปฏิบัติที่แสดง **วิธีทำ OCR**, **recognize text from image**, และ **extract text from PNG** ด้วยตัวห่อหุ้ม Python ที่เบา ๆ เพียงไม่กี่บรรทัดของโค้ด คุณจะสามารถ **convert image to text** ได้อย่างง่ายดาย และไม่ต้องกังวลเรื่องลิขสิทธิ์เพราะเราจะใช้โหมดทดลองที่มีมาให้แล้ว  

## สิ่งที่คุณจะได้เรียนรู้  

* วิธีตั้งค่าไลเซนส์ทดลองสำหรับเครื่อง OCR (ไม่ต้องระบุเส้นทางไฟล์)  
* ลำดับการเรียกใช้ที่แม่นยำเพื่อ **recognize text from image**  
* วิธี **extract text from PNG** และจัดการกับปัญหาทั่วไปเช่นฟอนต์ที่หายไป  
* เคล็ดลับในการขยายโซลูชันเมื่อย้ายจากไลเซนส์ทดลองไปสู่ไลเซนส์การผลิต  

**Prerequisites** – คุณต้องมี Python 3.8+ และแพ็กเกจ `ocr` (ติดตั้งได้ด้วย `pip install ocr`). ไม่ต้องใช้เครื่องมือภายนอกอื่นใด  

---  

![ตัวอย่างการทำ OCR](https://example.com/ocr-demo.png "วิธีทำ OCR ใน Python – แสดงข้อความที่จดจำได้")  

*ข้อความแทนรูปภาพ: วิธีทำ OCR ใน Python – ตัวอย่างผลลัพธ์*  

## ขั้นตอนที่ 1 – เปิดใช้งานไลเซนส์ทดลอง (ไม่ต้องระบุเส้นทางไฟล์)  

ก่อนที่เอนจินจะอ่านอะไรได้ มันต้องการไลเซนส์ที่ถูกต้อง โหมดทดลองเหมาะสำหรับการทดลองและโครงการขนาดเล็ก  

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*ทำไมเรื่องนี้ถึงสำคัญ:* วัตถุไลเซนส์บอกไลบรารี OCR ว่าคุณกำลังทำงานใน sandbox หากข้ามขั้นตอนนี้ เอนจินจะโยน `LicenseError` ทันทีที่คุณเรียก `recognize()`  

**Pro tip:** เมื่อคุณอัปเกรดเป็นไลเซนส์แบบชำระเงิน ให้แทนที่สองบรรทัดข้างบนด้วย `ocr.License("path/to/your/license.key").apply()`  

## ขั้นตอนที่ 2 – สร้างอินสแตนซ์ของ OCR Engine  

เมื่อไลเซนส์ทดลองทำงานแล้ว เราจะสร้างอินสแตนซ์ของเอนจินหลัก คิดว่าเป็น “สมอง” ที่จะมองรูปภาพและตัดสินว่าตัวอักษรอยู่ที่ไหน  

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*ทำไมเรื่องนี้ถึงสำคัญ:* `OcrEngine` เก็บการตั้งค่าเช่น language packs และ DPI settings คุณสามารถปรับเปลี่ยนได้ภายหลัง แต่ค่าเริ่มต้นทำงานได้ดีกับ PNG ที่เป็นภาษาอังกฤษเท่านั้น  

## ขั้นตอนที่ 3 – โหลดไฟล์ PNG ที่ต้องการประมวลผล  

นี่คือจุดที่เราจะ **recognize text from image** เมธอด `ocr.Imaging.Image.load()` รองรับ PNG, JPEG, BMP และรูปแบบอื่น ๆ อีกหลายชนิด  

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*กรณีขอบ:* หาก PNG ของคุณใช้พาเลตต์แบบ indexed (พบบ่อยในสกรีนช็อต) ตัวโหลดจะทำการแปลงเป็นบัฟเฟอร์ RGB 24‑bit โดยอัตโนมัติ การแปลงนี้อาจทำให้ประสิทธิภาพลดลงเล็กน้อย แต่รับประกันผลลัพธ์ OCR ที่แม่นยำ  

## ขั้นตอนที่ 4 – รัน OCR และดึงข้อความ  

สุดท้าย เราขอให้เอนจินทำงานแล้วดึงผลลัพธ์เป็นข้อความธรรมดา  

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**ผลลัพธ์ที่คาดหวัง** (ตัวอย่างสำหรับภาพง่าย ๆ ที่มีข้อความ “Hello World”):  

```
Hello World
```

หากภาพมีหลายบรรทัด ผลลัพธ์จะคงการขึ้นบรรทัดใหม่ ทำให้ง่ายต่อการส่งต่อไปยังกระบวนการต่อท้ายเช่นตัวแยก CSV หรือ pipeline NLP  

## ตัวเลือก: ปรับจูนเพื่อความแม่นยำที่ดียิ่งขึ้น  

* **Language packs:** `ocr_engine.set_language("eng")` (ค่าเริ่มต้น) หรือ `"fra"` สำหรับภาษาฝรั่งเศส  
* **DPI scaling:** `ocr_engine.set_dpi(300)` สามารถปรับปรุงผลลัพธ์บนสแกนความละเอียดต่ำ  
* **Pre‑processing:** การใช้ binary threshold (`ocr.Imaging.Image.threshold()`) ก่อน `set_image` มักให้ข้อความที่สะอาดขึ้นบนพื้นหลังที่มีนอยส์  

การปรับแต่งเหล่านี้มีประโยชน์เมื่อคุณย้ายจากการสาธิตเร็ว ๆ ไปสู่ **ocr tutorial python** ระดับการผลิตที่ต้องประมวลผลหลายร้อยไฟล์ต่อวัน  

## สคริปต์เต็ม – พร้อมคัดลอกและวาง  

ด้านล่างเป็นสคริปต์ที่ทำงานได้ครบถ้วนรวมทุกขั้นตอนที่กล่าวมา บันทึกเป็น `run_ocr.py` แล้วแทนที่ `YOUR_DIRECTORY/sample1.png` ด้วยเส้นทางของ PNG ของคุณเอง  

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

เรียกใช้งานจากบรรทัดคำสั่ง:  

```bash
python run_ocr.py
```

คุณควรเห็นข้อความที่สกัดออกมาปรากฏบนคอนโซล หากได้สตริงว่างเปล่า ให้ตรวจสอบว่าภาพมีข้อความที่คมชัดและมีคอนทราสต์สูง และไลเซนส์ทดลองได้ถูกนำไปใช้โดยไม่มีข้อผิดพลาด  

## คำถามทั่วไปและข้อควรระวัง  

* **“ทำงานกับ JPEG ได้ไหม?”** – ทำได้แน่นอน เมธอด `load()` ตรวจจับรูปแบบอัตโนมัติ คุณจึงสามารถสลับ PNG เป็น JPEG ได้โดยไม่ต้องแก้โค้ด  
* **“ถ้าภาพถูกหมุน?”** – เอนจินสามารถตรวจจับทิศทางอัตโนมัติได้ แต่เพื่อผลลัพธ์ที่ดีที่สุด คุณอาจหมุนภาพล่วงหน้าด้วย `input_image.rotate(90)` ก่อน `set_image`  
* **“สามารถประมวลผลหลายภาพในลูปได้ไหม?”** – ได้เลย เพียงย้ายการโหลดและการเรียก `recognize()` เข้าไปใน `for` loop; อินสแตนซ์ `ocr_engine` เดียวสามารถใช้ซ้ำได้ ซึ่งช่วยลดค่าโอเวอร์เฮดเล็กน้อย  

## ขั้นตอนต่อไป – จากการสาธิตสู่การผลิต  

ตอนนี้คุณรู้ **วิธีทำ OCR** แล้ว ลองสำรวจหัวข้อต่อไปนี้:  

* **Batch processing** – ผสานสคริปต์นี้กับ `os.listdir()` เพื่อ **extract text from PNG** เป็นจำนวนมากในครั้งเดียว  
* **Integrate with PDF** – ใช้ `pdf2image` แปลงหน้า PDF เป็น PNG แล้วส่งต่อไปยัง pipeline เดียวกัน  
* **Post‑processing** – ใช้ regex หรือ fuzzy matching เพื่อลบความผิดพลาดทั่วไปของ OCR (เช่น “0” กับ “O”)  

ทั้งหมดนี้ต่อยอดจากแนวคิดหลักของ **convert image to text** และทำให้เวิร์กโฟลว์ OCR ของคุณมีประโยชน์มากยิ่งขึ้น  

---  

### สรุปย่อ  

เราได้ครอบคลุมทุกอย่างที่คุณต้องรู้เพื่อ **วิธีทำ OCR** ใน Python: เปิดใช้งานไลเซนส์ทดลอง, สร้างเอนจิน, โหลด PNG, รันการจดจำ, และพิมพ์ผลลัพธ์ ด้วยเพียงไม่กี่บรรทัดคุณก็สามารถ **recognize text from image**, **extract text from PNG**, และ **convert image to text** สำหรับแอปพลิเคชันต่อไปได้  

ลองใช้งาน ปรับ DPI หรือการตั้งค่าภาษา แล้วปล่อยให้เอนจินทำงานหนักให้คุณเอง โชคดีในการเขียนโค้ด!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}