---
category: general
date: 2026-03-28
description: วิธีทำ OCR บน ROI ด้วย Python – เรียนรู้วิธีตั้งค่าตัวเลือกการเตรียมข้อมูลล่วงหน้าเพื่อการสกัดข้อความที่แม่นยำจากพื้นที่ภาพเฉพาะ
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: th
og_description: วิธีทำ OCR บน ROI ด้วย Python – คู่มือนี้แสดงวิธีตั้งค่าการเตรียมข้อมูลล่วงหน้าเพื่อการสกัดข้อความที่เชื่อถือได้จากพื้นที่ภาพที่กำหนด.
og_title: วิธีทำ OCR บน ROI ด้วย Python – วิธีตั้งค่าการเตรียมข้อมูล
tags:
- OCR
- Python
- Aspose
title: วิธีทำ OCR บน ROI ใน Python – วิธีตั้งค่าการเตรียมข้อมูลล่วงหน้า
url: /th/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ROI ด้วย Python – วิธีตั้งค่าการเตรียมข้อมูลล่วงหน้า

เคยสงสัย **วิธีทำ OCR ROI** ในภาพใบแจ้งหนี้ที่มีเสียงรบกวนโดยไม่ต้องโหลดทั้งหน้าเข้าหน่วยความจำหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการจริง ๆ เราแค่ต้องการฟิลด์บางส่วนเท่านั้น—ชื่อผู้ลูกค้า, ที่อยู่, ยอดรวม—ดังนั้นการสแกนทั้งเอกสารจึงเป็นการทำงานเกินความจำเป็น  

ข่าวดีคือ? ด้วย Aspose OCR คุณสามารถบอกให้เอนจินรู้ **ว่าต้องมองที่ไหน** และแม้กระทั่งบอกให้ทำความสะอาดภาพก่อน ในบทแนะนำนี้เราจะอธิบาย **วิธีตั้งค่าการเตรียมข้อมูลล่วงหน้า** กำหนด Regions of Interest (ROIs) และดึงข้อความที่สะอาดออกมาในไม่กี่บรรทัดของ Python  

เมื่ออ่านจบคุณจะได้สคริปต์ที่พร้อมรันเพื่อดึงบล็อกเฉพาะจากใบแจ้งหนี้, ใบเสร็จ, หรือแบบฟอร์มใด ๆ ไม่ต้องใช้เครื่องมือเพิ่มเติม เพียงแค่ Aspose OCR และตรรกะ Python เล็กน้อย

---

## สิ่งที่คุณต้องเตรียม

- **Python 3.8+** (โค้ดทำงานได้กับเวอร์ชันล่าสุด)  
- **Aspose OCR for Python via .NET** – ติดตั้งด้วย `pip install aspose-ocr`  
- ตัวอย่างภาพ (เช่น `invoice.png`) ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้  
- ความคุ้นเคยพื้นฐานกับฟังก์ชัน Python และไวยากรณ์เชิงวัตถุ  

ถ้าคุณมีทั้งหมดนี้แล้ว เยี่ยม—มาดำเนินการต่อที่โค้ดกันเลย

---

![How to OCR ROI diagram](ocr-roi.png "How to OCR ROI example")

*Alt text: แผนภาพวิธีทำ OCR ROI แสดงกล่อง ROI บนภาพใบแจ้งหนี้*

---

## ขั้นตอนที่ 1 – เริ่มต้น OCR Engine (How to OCR ROI)

ก่อนที่เราจะบอกเอนจิน *ว่าต้องมองที่ไหน* เราต้องสร้างอินสแตนซ์ของ OCR processor ก่อน วัตถุนี้เก็บการตั้งค่าทั้งหมดและทำการจดจำ

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*เหตุผลที่สำคัญ*: คลาส `OcrEngine` ทำหน้าที่แยกส่วนงานหนัก (การตรวจจับฟอนต์, การวิเคราะห์เลย์เอาต์ ฯลฯ) การสร้างเอนจินเพียงครั้งเดียวช่วยหลีกเลี่ยงการรีอินิชเชียลไลซ์ทรัพยากรหนักสำหรับแต่ละภาพ ทำให้ประสิทธิภาพเร็วขึ้น

---

## ขั้นตอนที่ 2 – โหลดภาพต้นฉบับของคุณ (How to OCR ROI)

Aspose Storage ทำให้การโหลดภาพเป็นเรื่องง่าย เพียงชี้ไปที่พาธไฟล์ คุณก็จะได้อ็อบเจ็กต์ `Image` พร้อมประมวลผล

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*เคล็ดลับ*: หากคุณทำงานกับสตรีม (เช่น ภาพที่อัปโหลดผ่านเว็บ API) คุณสามารถส่งอ็อบเจ็กต์ `BytesIO` ไปยัง `Image.load` แทนพาธไฟล์ได้

---

## ขั้นตอนที่ 3 – กำหนด Regions of Interest (ROIs)

ตอนนี้เราตอบคำถามหลัก **วิธีทำ OCR ROI**: บอกเอนจินว่าตรงสี่เหลี่ยมใดบรรจุข้อมูลที่เราต้องการ แต่ละ ROI ถูกกำหนดด้วยมุมบน‑ซ้าย (`x`, `y`) และขนาด (`width`, `height`)

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*ทำไมต้องใช้ ROI?*  
- **ความเร็ว** – เอนจินข้ามส่วนที่ไม่เกี่ยวข้องของภาพ  
- **ความแม่นยำ** – เน้นพื้นที่เล็ก ๆ ทำให้สัญญาณรบกวนจากส่วนอื่นไม่ทำให้ตัวจดจำสับสน  
- **ความยืดหยุ่น** – สามารถเพิ่ม ROI ได้ตามต้องการ; เอนจินจะคืนรายการผลลัพธ์ตามลำดับเดียวกัน

---

## ขั้นตอนที่ 4 – วิธีตั้งค่าการเตรียมข้อมูลล่วงหน้าเพื่อความแม่นยำของ OCR

ภาพที่สแกนหรือถ่ายจากโทรศัพท์มักมีการเอียง, คอนทราสต์ต่ำ, หรือแสงไม่สม่ำเสมอ Aspose OCR มีอ็อบเจ็กต์ `PreprocessingOptions` ที่ให้คุณเปิดใช้งานการแก้ไขทั่วไปก่อนการจดจำ

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*วิธีที่ช่วย*:  
- **Deskew** ลบการเอียงที่ทำให้รูปร่างอักขระไม่ชัดเจน  
- **Binarize** ลดสัญญาณรบกวนสี ให้ OCR ทำงานบนภาพไบนารีที่สะอาด  
- **Contrast** เพิ่มความคมของเส้นที่จาง ซึ่งมีประโยชน์มากสำหรับใบเสร็จที่ซีดจาง  

คุณสามารถทดลองเปิด/ปิดฟลักเหล่านี้และดูผลลัพธ์ การทำเช่นนี้คือวิธี **ตั้งค่าการเตรียมข้อมูลล่วงหน้า** อย่างมีประสิทธิภาพ

---

## ขั้นตอนที่ 5 – ทำ OCR เฉพาะใน ROI ที่กำหนดไว้

เมื่อมีเอนจิน, ภาพ, ROI, และการเตรียมข้อมูลพร้อมแล้ว ถึงเวลาเรียก `recognize` วิธีนี้จะคืนอ็อบเจ็กต์ `OcrResult` ที่มีคอลเลกชัน `regions`—แต่ละรายการตรงกับลำดับ ROI ที่เราส่งเข้าไป

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*เบื้องหลัง*: เอนจินจะครอปแต่ละ ROI, ใช้ขั้นตอนการเตรียมข้อมูล, แล้วรันโมเดลจดจำบนส่วนที่ทำความสะอาดแล้ว เพราะเราส่งรายการเข้าไป ผลลัพธ์จึงรักษาลำดับเดิม ทำให้การประมวลผลต่อไปง่ายขึ้น

---

## ขั้นตอนที่ 6 – อ่านและใช้ข้อความที่สกัดออกมา (How to OCR ROI)

สุดท้าย ให้วนลูปผ่านรายการ `regions` และพิมพ์—หรือบันทึก—สตริงที่จดจำได้ อ็อบเจ็กต์ `Region` มีคุณสมบัติ `text` ที่เก็บผลลัพธ์ในรูป Unicode

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

หากข้อความดูเป็นอักขระผสมกัน ให้กลับไปตรวจสอบ **วิธีตั้งค่าการเตรียมข้อมูลล่วงหน้า**: อาจเพิ่ม `contrast` หรือปิด `binarize` สำหรับโลโก้สี

---

## ข้อผิดพลาดทั่วไปและเคล็ดลับระดับมืออาชีพ

| ปัญหา | สาเหตุ | วิธีแก้ (วิธีตั้งค่าการเตรียมข้อมูลล่วงหน้า) |
|-------|--------|----------------------------------------------|
| ตัวอักษรเอียงแสดงเป็นอักขระไร้ความหมาย | `deskew` ปิดหรือภาพหมุนมากเกินไป | เปิด `preprocessing_options.deskew = True` |
| ตัวเลขกลายเป็นจุดหรือรอยแปลก | คอนทราสต์ต่ำหรือการ binarize มากเกินไป | ลด `contrast` (เช่น `1.2`) หรือตั้ง `binarize = False` |
| พิกัด ROI ผิดพลาดหลายพิกเซล | DPI ต่างกันหรือสแกนเนอร์สเกล | ใช้เครื่องมือ (เช่น Paint.NET) วัดตำแหน่งพิกเซลที่แม่นยำ หรือเพิ่ม margin เล็กน้อย (`+5` พิกเซล) ให้แต่ละ ROI |
| ผลลัพธ์ว่างสำหรับบาง region | ROI อยู่นอกขอบภาพ | ตรวจสอบขนาดภาพ: `source_image.width`, `source_image.height` |

---

## การขยายโซลูชัน (How to OCR ROI in Different Scenarios)

- **Dynamic ROIs**: หากใบแจ้งหนี้ของคุณมีเลย์เอาต์แปรผัน คุณสามารถรัน OCR หน้าเต็มอย่างเร็วเพื่อค้นหาคำสำคัญ (“Customer:”, “Address:”) แล้วคำนวณ ROI แบบไดนามิกได้  
- **Batch Processing**: ห่อขั้นตอนข้างต้นเป็นฟังก์ชันและวนลูปผ่านโฟลเดอร์ของภาพ อย่าลืมใช้อินสแตนซ์ `ocr_engine` เดียวกันเพื่อประหยัดหน่วยความจำ  
- **Exporting to JSON**: แทนการพิมพ์ ให้สร้างดิกชันนารีและใช้ `json.dumps` ส่งออก; วิธีนี้ทำให้การผสานต่อ (เช่น ส่งข้อมูลเข้าสู่ระบบ ERP) ง่ายดาย

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## สรุป

คุณมีตัวอย่างที่สมบูรณ์และพร้อมรันที่แสดง **วิธีทำ OCR ROI** ด้วย Python พร้อมกับการ **ตั้งค่าการเตรียมข้อมูลล่วงหน้า** เพื่อความแม่นยำสูงสุด การจำกัดเอนจินให้ทำงานเฉพาะสี่เหลี่ยมที่ต้องการและทำความสะอาดภาพล่วงหน้า จะทำให้ได้ผลลัพธ์ที่เร็วกว่าและสะอาดกว่า—เหมาะกับการอัตโนมัติใบแจ้งหนี้, การแปลงฟอร์ม, หรือสถานการณ์ใด ๆ ที่ต้องการเพียงส่วนหนึ่งของหน้า  

พร้อมก้าวต่อไปหรือยัง? ลองปรับพิกัด ROI สำหรับประเภทเอกสารอื่น หรือทดลองเปิดฟลักการเตรียมข้อมูลเพิ่มเติม เช่น `sharpen` หรือ `noise_reduction` ความยืดหยุ่นของ Aspose OCR ทำให้คุณสามารถปรับแต่งไพป์ไลน์ให้เข้ากับคุณภาพภาพใด ๆ  

หากเจออุปสรรค ตรวจสอบคอนโซลสำหรับ region ที่ว่างและกลับไปปรับการตั้งค่าการเตรียมข้อมูล ลุยโค้ดให้สนุกและขอให้ OCR ของคุณแม่นยำเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}