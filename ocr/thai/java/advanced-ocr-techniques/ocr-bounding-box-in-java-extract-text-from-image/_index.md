---
category: general
date: 2026-06-16
description: บทเรียน OCR bounding box ใน Java แสดงวิธีการดึงข้อความจากภาพ, อ่านข้อความจากภาพ,
  และรับคะแนนความเชื่อมั่นของ OCR สำหรับไฟล์ JPG.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: th
og_description: กล่องขอบเขต OCR ใน Java ช่วยให้คุณจดจำข้อความจากไฟล์ JPG ดึงข้อความจากภาพ
  และดูคะแนนความเชื่อมั่นของ OCR — ทั้งหมดในตัวอย่างโค้ดง่าย ๆ.
og_title: กล่องขอบเขต OCR ใน Java – ดึงข้อความจากภาพ
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: กล่องขอบ OCR ใน Java – ดึงข้อความจากภาพ
url: /th/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box ใน Java – ดึงข้อความจากภาพ

เคยสงสัยไหมว่าเราจะรับ **ocr bounding box** สำหรับแต่ละชิ้นของข้อความในภาพ Java ได้อย่างไร? ในบทแนะนำนี้เราจะสาธิตวิธี **extract text from image** files, **read text from image**, และแม้กระทั่งดู **ocr confidence score** ขณะ **recognize text from jpg** files คำตอบสั้น ๆ คือ? เพียงไม่กี่บรรทัดของโค้ดโดยใช้ไลบรารี OCR สมัยใหม่ พร้อมคำอธิบายสั้น ๆ ว่าทำไมแต่ละการเรียกจึงสำคัญ

ด้านล่างคุณจะพบตัวอย่างที่พร้อมรันครบถ้วน, การอธิบายแบบขั้นตอน‑ต่อ‑ขั้นตอน, และเคล็ดลับปฏิบัติที่คุณสามารถคัดลอกไปใช้ในโปรเจกต์ของคุณได้โดยตรง เมื่อเสร็จแล้วคุณจะสามารถแสดงผลออกมาแบบนี้ได้:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## สิ่งที่คุณต้องเตรียม

- **Java 11** หรือใหม่กว่า (ไวยากรณ์ด้านล่างใช้คีย์เวิร์ด `var` เพื่อความกระชับ, แต่คุณสามารถลบออกได้หากใช้ JDK รุ่นเก่า)  
- ไลบรารี OCR ที่มี Java API – สำหรับคู่มือนี้เราจะใช้ **[Tesseract4J](https://github.com/nguyenq/tess4j)** ซึ่งเป็น wrapper เบา ๆ ของเอนจิน Tesseract ที่เป็นที่นิยม  
- ภาพ JPEG (`.jpg`) ที่มีข้อความพิมพ์ชัดเจน  
- IDE ที่คุณชื่นชอบ (IntelliJ IDEA, Eclipse, VS Code…) – ใดก็ได้

หากคุณยังไม่มีไลบรารี, เพียงเพิ่ม dependency ของ Maven นี้:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

ตอนนี้มาลงมือทำกันเลย

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR Bounding Box: การตั้งค่า Engine

สิ่งแรกที่ต้องทำคือสร้างอินสแตนซ์ของ OCR engine คิดว่าเป็นการเปิดสแกนเนอร์ที่ต่อไปจะอ่านพิกเซล

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**ทำไมจึงสำคัญ:**  
หากไม่ได้ตั้งค่า `datapath`, Tesseract จะไม่รู้ว่าพ็อกเกจภาษาอยู่ที่ไหนและจะเกิดข้อผิดพลาด “Failed loading language” ที่อ่านยาก การเรียก `setLanguage` เป็นทางเลือกถ้าคุณต้องการใช้พ็อกเกจภาษาอังกฤษเริ่มต้นเท่านั้น, แต่การระบุอย่างชัดเจนทำให้โค้ดอ่านง่ายขึ้นสำหรับผู้ที่มาดูต่อในอนาคต

## โหลดภาพที่ต้องการประมวลผล

ต่อไปให้ส่ง JPEG ที่ต้องการวิเคราะห์ให้กับ engine ไลบรารีรับ `File` หรือ `BufferedImage`; เราจะใช้ `File` เพื่อความง่าย

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**เคล็ดลับ:**  
หากภาพของคุณอยู่ใน resources (เช่น ภายใน JAR), ใช้ `getResourceAsStream` แล้วห่อด้วย `ImageIO.read` วิธีนี้ทำให้บทแนะนำทำงานได้ทั้งในเครื่องโลคัลและในแอปที่บรรจุเป็นแพคเกจ

## ทำการ OCR Recognition

ตอนนี้เราจะสั่งให้ engine อ่านรูปผลลัพธ์จะเป็นสตริงข้อความธรรมดา, แต่เรายังต้องการ **ocr confidence score** และ **ocr bounding box** สำหรับแต่ละบรรทัดด้วย

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**ทำไมเราถึงใช้ `getWords` แทน `doOCR` ธรรมดา:**  
`doOCR` ให้สตริงดิบแต่ละละทิ้งข้อมูลเชิงพื้นที่ไป การเรียก `getWords` พร้อม `RIL_WORD` (หรือ `RIL_TEXTLINE` หากต้องการกล่องระดับบรรทัด) จะคืนรายการ `Word` objects ที่แต่ละอันบรรจุข้อความ, ความเชื่อมั่น, และสี่เหลี่ยมขอบเขต นี่คือหัวใจของฟีเจอร์ **ocr bounding box**

## ทำความเข้าใจผลลัพธ์

การรันโค้ดข้างต้นกับ JPEG ที่สะอาดจะให้ผลลัพธ์คล้ายกับ:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – ตัวอักษรที่ถูกจดจำ  
- **Confidence** – ค่า floating‑point ระหว่าง 0‑1; ค่ามากหมายถึง engine มีความมั่นใจสูงกว่า  
- **Box** – สี่เหลี่ยมที่ล้อมรอบคำในพิกัดพิกเซล (x, y, width, height)

ตอนนี้คุณสามารถ **read text from image** พร้อมรู้ตำแหน่งที่แน่นอนของแต่ละส่วนบนแคนวาส – เหมาะสำหรับการไฮไลท์, ครอป, หรือส่งต่อไปยัง pipeline NLP ต่อไป

## กรณีขอบและข้อผิดพลาดทั่วไป

| Situation | What to Watch For | Fix / Work‑around |
|-----------|-------------------|-------------------|
| Image is blurry or low‑contrast | Confidence scores drop dramatically (often below 0.6). | Pre‑process with OpenCV: increase contrast, apply thresholding. |
| JPEG contains rotated text | Bounding boxes appear skewed or missing. | Use `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` to let Tesseract auto‑detect orientation. |
| Large images cause OutOfMemoryError | Java heap fills up when loading big pictures. | Downscale the image before OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| You need line‑level boxes instead of word‑level | `RIL_WORD` returns per‑word boxes. | Switch to `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Non‑English characters appear as � | Language data not loaded. | Download the appropriate `.traineddata` file and point `setDatapath` to its folder. |

การจัดการกับปัญหาเหล่านี้ตั้งแต่แรกจะช่วยคุณประหยัดเวลาการดีบักหลายชั่วโมงในภายหลัง

## ตัวอย่างทำงานเต็มรูปแบบ (ทุกขั้นตอนในไฟล์เดียว)

ด้านล่างเป็นคลาส Java ที่สามารถคัดลอก‑วางลงในโฟลเดอร์ `src/main/java` แล้วรันด้วย `mvn exec:java` ได้เลย ตัวอย่างนี้รวมทุกอย่างที่เราได้พูดถึงไว้ในที่เดียว

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## คุณควรเรียนรู้อะไรต่อไป?


บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ต่อ‑ขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}