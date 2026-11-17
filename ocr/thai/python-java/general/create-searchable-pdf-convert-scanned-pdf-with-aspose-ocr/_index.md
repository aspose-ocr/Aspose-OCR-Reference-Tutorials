---
category: general
date: 2026-03-18
description: สร้าง PDF ที่ค้นหาได้จากไฟล์สแกนของคุณโดยใช้ Aspose OCR. เรียนรู้วิธีแปลง
  PDF สแกน, ดึงข้อความจาก PDF, และจดจำข้อความใน PDF อย่างรวดเร็ว.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: th
og_description: สร้าง PDF ที่ค้นหาได้ทันที ตามคำแนะนำนี้เพื่อแปลง PDF สแกน, ดึงข้อความจาก
  PDF, และจดจำข้อความ PDF ด้วย Aspose OCR.
og_title: สร้าง PDF ที่ค้นหาได้ – ขั้นตอนโดยละเอียดด้วย Aspose OCR
tags:
- OCR
- PDF
- Aspose
- Python
title: สร้าง PDF ที่ค้นหาได้ – แปลง PDF สแกนด้วย Aspose OCR
url: /th/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้ – คู่มือขั้นตอนโดยละเอียด  

เคยต้อง **create searchable PDF** จากกองหน้าเอกสารสแกนหลายหน้าแต่ไม่รู้จะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาส่วนใหญ่มักเจออุปสรรคนี้เมื่อต้องรับไฟล์สแกนครั้งแรกบนเซิร์ฟเวอร์  

ข่าวดีคือด้วย Aspose OCR คุณสามารถ **convert scanned pdf** ได้ด้วยไม่กี่บรรทัดโค้ด, **extract text from pdf** เพื่อการตรวจสอบ, และแม้กระทั่ง **recognize text pdf** แบบเรียลไทม์ ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด ตั้งแต่การติดตั้งไลบรารีจนถึงการบันทึกเอกสารที่ค้นหาได้อย่างเต็มที่ พร้อมเคล็ดลับเล็กน้อยสำหรับการจัดการกรณี **convert image pdf** ที่ซับซ้อน

## สิ่งที่คุณจะได้เรียนรู้  

เมื่ออ่านจบบทนี้คุณจะสามารถ:

* โหลด PDF สแกน (หรือ PDF ที่มีเฉพาะภาพ) เข้า Aspose OCR  
* ระบุหน้าที่ต้องการประมวลผล – มีประโยชน์เมื่อต้องการเพียงบางส่วนของเอกสาร  
* ฝังผลลัพธ์ OCR กลับเข้าไฟล์ต้นฉบับเพื่อให้ได้ **searchable PDF** ที่แท้จริง  
* ตรวจสอบการทำงานโดยพิมพ์จำนวนหน้าและ, หากต้องการ, แสดงข้อความที่สกัดออกมา  

ไม่มีบริการภายนอก, ไม่มีเวทมนตร์ลับ—เพียง Python ธรรมดาและ API ของ Aspose

## ข้อกำหนดเบื้องต้น  

* Python 3.8 หรือใหม่กว่า  
* แพคเกจ `aspose-ocr` – ติดตั้งด้วย `pip install aspose-ocr`  
* ไฟล์ PDF สแกน (หรือ PDF ที่มีเฉพาะภาพ)  
* ความคุ้นเคยพื้นฐานกับการเขียนสคริปต์ Python  

ถ้าคุณมีทั้งหมดนี้แล้ว, ไปต่อกันเลย

<img src="searchable-pdf-workflow.png" alt="Create searchable PDF workflow">  

*(ภาพแสดงกระบวนการ OCR – ไม่จำเป็นต่อโค้ดแต่ช่วยให้ผู้เรียนที่ชอบภาพเข้าใจได้ง่ายขึ้น)*

## ขั้นตอนที่ 1 – เริ่มต้น OcrEngine  

สิ่งแรกที่ต้องทำคือสร้างอินสแตนซ์ของ `OcrEngine` คิดว่าเป็นสมองที่จะอ่านพิกเซลทุกจุดและแปลงเป็นอักขระ Unicode

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**ทำไมจึงสำคัญ:** หากไม่มี engine คุณไม่สามารถตั้งค่าตัวเลือกหรือเรียกใช้การจดจำได้ การสร้างมันตั้งแต่ต้นยังให้จุดที่คุณสามารถต่อพจนานุกรมกำหนดเองในภายหลังได้อีกด้วย

## ขั้นตอนที่ 2 – โหลด PDF แหล่งที่มาของคุณ  

Aspose OCR สามารถอ่าน PDF ได้โดยตรง ซึ่งหมายความว่าคุณไม่ต้องแปลงแต่ละหน้าเป็นรูปภาพเอง เพียงชี้ engine ไปที่ไฟล์

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*เคล็ดลับ:* หาก PDF มีขนาดใหญ่, พิจารณาโหลดจากสตรีมเพื่อหลีกเลี่ยงการล็อกไฟล์บนดิสก์

## ขั้นตอนที่ 3 – ตั้งค่าตัวเลือกการจดจำ PDF  

นี่คือจุดที่คีย์เวิร์ดรองเริ่มทำงาน คุณสามารถบอก engine ให้ **convert scanned pdf** เฉพาะบางหน้า, ฝังข้อความที่จดจำได้, หรือแม้กระทั่งรักษาภาพต้นฉบับไว้โดยไม่เปลี่ยนแปลง

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**ทำไมจึงสำคัญ:**  
* `setEmbedRecognisedText(True)` คือกุญแจสำคัญที่ทำให้ PDF แบบแรสเตอร์กลายเป็น **searchable PDF**  
* `setPageRange` ช่วยให้คุณ **convert image pdf** อย่างเลือกสรร – มีประโยชน์สำหรับเอกสารขนาดใหญ่ที่ต้องการ OCR เพียงไม่กี่หน้า  
* การเปิดใช้งานการสกัดข้อความทำให้คุณสามารถ **extract text from pdf** ได้ในภายหลังโดยไม่ต้องเปิดตัวดูเอกสาร

## ขั้นตอนที่ 4 – ผูกตัวเลือกเข้ากับ Engine  

ตอนนี้ให้ผูกตัวเลือกเข้ากับ engine ขั้นตอนนี้มักถูกมองข้าม, แต่หากข้ามไป engine จะทำงานด้วยการตั้งค่าเริ่มต้น (ไม่มีข้อความที่ค้นหาได้)

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## ขั้นตอนที่ 5 – รัน OCR บนหน้าที่เลือก  

เมื่อทุกอย่างเชื่อมต่อเรียบร้อย การจดจำจริงเป็นเพียงการเรียกเมธอดเดียว

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

หากคุณกำลังประมวลผลเอกสารหลายเมกะไบต์, ควรห่อโค้ดนี้ใน `try/except` เพื่อจับ `OcrException` และบันทึกหน้าที่เกิดปัญหา

## ขั้นตอนที่ 6 – ตรวจสอบผลลัพธ์  

การตรวจสอบอย่างรวดเร็วคือการพิมพ์จำนวนหน้าที่ engine คิดว่าประมวลผลแล้ว คุณยังสามารถดึงข้อความดิบออกมาหากต้องการ **extract text from pdf** เพื่อการวิเคราะห์ต่อ

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**ทำไมคุณต้องสนใจ:** การเห็นจำนวนหน้ายืนยันว่า `setPageRange` ทำงาน, ส่วนข้อความที่สกัดออกมาพิสูจน์ว่า OCR ได้จดจำอักขระจริงๆ

## ขั้นตอนที่ 7 – บันทึก PDF ที่ค้นหาได้  

สุดท้าย, เขียนผลลัพธ์กลับไปยังดิสก์ ค่าคงที่ `ImageFormats.PDF` บอก Aspose ให้เก็บไฟล์เป็น PDF พร้อมข้อความที่ค้นหาได้

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

เปิดไฟล์ที่ได้ในโปรแกรมอ่าน PDF ใดก็ได้และลองค้นหาข้อความ—เรียบร้อย, คุณได้ **created searchable pdf** แล้ว!

## การจัดการกรณีทั่วไป  

### เมื่อแหล่งที่มาคือ PDF ที่มี *เฉพาะภาพ*  

หาก PDF อินพุตของคุณมีเพียงภาพ (ไม่มีเลเยอร์ข้อความ) โค้ดเดียวกันก็ทำงานได้—แค่ตรวจสอบให้ `setEmbedRecognisedText(True)` ยังคงเปิดอยู่ คุณอาจต้องเพิ่ม DPI เพื่อความแม่นยำที่ดียิ่งขึ้น:

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### การจัดการหลายภาษา  

Aspose OCR รองรับแพ็คเกจภาษา โหลดภาษาก่อนเรียก `recognize()`:

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### เอกสารขนาดใหญ่  

การประมวลผล PDF สแกน 500 หน้าอาจใช้หน่วยความจำมาก แบ่งงานเป็นส่วนย่อย:

1. วนลูปตามช่วงหน้า (`setPageRange(start, end)`)  
2. บันทึกแต่ละส่วนเป็น PDF ที่ค้นหาได้ชั่วคราว  
3. รวมส่วนต่างๆ ด้วย `PdfMerger` (คอมโพเนนต์ Aspose อีกตัว)

## ตัวอย่างทำงานเต็มรูปแบบ (รวมทุกขั้นตอน)

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

การรันสคริปต์นี้จะให้คุณได้ **searchable PDF** ที่สามารถเปิดใน Adobe Reader, Chrome หรือโปรแกรมอ่าน PDF ใดก็ได้และค้นหาคำได้ทันที

## สรุป  

ตอนนี้คุณมีโซลูชันครบวงจรจากต้นจนจบเพื่อ **create searchable PDF** ด้วย Aspose OCR ตั้งแต่การโหลดแหล่งที่มา, การตั้งค่าตัวเลือกที่ **convert scanned pdf**, การสกัดและตรวจสอบข้อความ, จนถึงการบันทึกผลลัพธ์ที่ค้นหาได้ ทุกขั้นตอนถูกครอบคลุม  

ต่อไปคุณอาจอยากสำรวจสถานการณ์ **convert image pdf** ที่แหล่งที่มาคือชุด JPEG ที่บรรจุเป็น PDF, หรือเจาะลึก OCR เฉพาะภาษาเพื่อเพิ่มความแม่นยำให้กับเอกสารหลายภาษา ไม่ว่าคุณจะทำอย่างไร รูปแบบก็ยังคงเหมือนเดิม: ตั้งค่าตัวเลือก, รัน `recognize()`, แล้วบันทึก  

ลองปรับเปลี่ยนช่วงหน้า, ปรับ DPI, หรือเชื่อมพจนานุกรมกำหนดเอง หากเจออุปสรรคใด ๆ แสดงความคิดเห็นด้านล่างหรือดูเอกสารอย่างเป็นทางการของ Aspose เพื่ออัปเดต API ล่าสุด ขอให้สนุกกับ OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}