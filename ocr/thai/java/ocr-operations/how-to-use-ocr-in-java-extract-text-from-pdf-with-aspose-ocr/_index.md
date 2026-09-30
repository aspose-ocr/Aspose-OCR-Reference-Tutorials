---
category: general
date: 2026-02-17
description: วิธีใช้ OCR ใน Java เพื่อดึงข้อความจาก PDF, แปลง PDF เป็นภาพ, และทำ OCR
  บนไฟล์ PDF ที่สแกนโดยใช้ Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: th
og_description: วิธีใช้ OCR ใน Java เพื่อดึงข้อความจากไฟล์ PDF เรียนรู้การแปลง PDF
  เป็นภาพและการจดจำ PDF ที่สแกนด้วย Aspose.OCR.
og_title: วิธีใช้ OCR ใน Java – คู่มือครบถ้วน
tags:
- OCR
- Java
- Aspose
title: วิธีใช้ OCR ใน Java – ดึงข้อความจาก PDF ด้วย Aspose.OCR
url: /th/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน Java – ดึงข้อความจาก PDF ด้วย Aspose.OCR

เคยสงสัย **วิธีใช้ OCR** เพื่อแปลง PDF ที่สแกนเป็นข้อความที่ค้นหาได้หรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนาส่วนใหญ่มักเจอปัญหาเมื่อ PDF มาถึงในรูปแบบของภาพหลายๆ หน้า และเครื่องมือดึงข้อความทั่วไปก็ให้ผลลัพธ์เป็นศูนย์ ข่าวดีคือ ด้วยเพียงไม่กี่บรรทัดของ Java และ Aspose.OCR คุณสามารถ **ดึงข้อความจาก PDF**, **แปลง PDF เป็นภาพ**, และ **จดจำ PDF ที่สแกน** ได้ในขั้นตอนเดียวที่ง่ายดาย

ในบทแนะนำนี้เราจะพาคุณผ่านทุกอย่างที่ต้องรู้—from การรับลิขสิทธิ์ของไลบรารีจนถึงการพิมพ์ผลลัพธ์สุดท้าย เมื่อจบคุณจะมีโปรแกรมที่พร้อมรันเพื่อดึงข้อความธรรมดาออกจากรายงาน, ใบแจ้งหนี้ หรืออีบุ๊คที่สแกนใดๆ ไม่ต้องพึ่งบริการภายนอก ไม่ต้องใช้เวทมนตร์—เพียงโค้ด Java ที่คุณควบคุมเอง

## สิ่งที่คุณต้องมี

- **Java Development Kit (JDK) 8+** – เวอร์ชันล่าสุดใดก็ได้
- **Aspose.OCR for Java** JAR (ดาวน์โหลดจากเว็บไซต์ของ Aspose)  
- **ไฟล์ลิขสิทธิ์ Aspose.OCR ที่ถูกต้อง** (`Aspose.OCR.lic`) เวอร์ชันทดลองฟรีก็ใช้ได้ แต่ลิขสิทธิ์เต็มจะให้ความแม่นยำสูงสุด
- **PDF ที่สแกนตัวอย่าง** (เช่น `scanned-report.pdf`)  
- IDE หรือโปรแกรมแก้ไขข้อความธรรมดาพร้อมเทอร์มินัล

แค่นั้นเอง ไม่ต้องใช้ Maven, Gradle หรือ dependency เพิ่มเติม—แค่ใส่ Aspose.OCR JAR ลงใน classpath

![ตัวอย่างการใช้ OCR](image-placeholder.png "ตัวอย่างการใช้ OCR")

## ขั้นตอนที่ 1 – โหลดลิขสิทธิ์ Aspose.OCR (ทำไมต้องทำ)

ก่อนที่เอนจินจะทำงานเต็มประสิทธิภาพ คุณต้องบอกตำแหน่งไฟล์ลิขสิทธิ์ให้มันรู้ หากข้ามขั้นตอนนี้ ไลบรารีจะอยู่ในโหมดทดลอง ซึ่งจะใส่ลายน้ำบนผลลัพธ์และอาจจำกัดความแม่นยำ

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**ทำไมถึงได้ผล:** คลาส `License` จะอ่านไฟล์ `.lic` แล้วลงทะเบียนแบบทั่วโลก หลังจากตั้งค่าแล้ว ทุก `OcrEngine` ที่คุณสร้างจะใช้ฟีเจอร์ที่ได้รับลิขสิทธิ์โดยอัตโนมัติ

## ขั้นตอนที่ 2 – สร้าง OCR Engine (เอนจินที่ทำงานเบื้องหลัง)

อินสแตนซ์ `OcrEngine` คือหัวใจหลักที่สแกนภาพและแปลงเป็นข้อความ คิดว่าเป็นสมองที่ตีความรูปแบบพิกเซล

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**เคล็ดลับ:** คุณสามารถปรับภาษา, ค่า confidence threshold, หรือแม้กระทั่งเปิดการเร่งความเร็วด้วย GPU ผ่านคุณสมบัติของเอนจิน สำหรับ PDF ภาษาอังกฤษส่วนใหญ่ค่าเริ่มต้นก็เพียงพอ

## ขั้นตอนที่ 3 – เตรียมข้อมูลเข้า: เพิ่ม PDF ของคุณ (แปลง PDF เป็นภาพภายใน)

Aspose.OCR จะถือแต่ละหน้าของ PDF เป็นภาพ เมื่อคุณเรียก `addPdf` ไลบรารีจะทำการ rasterize แต่ละหน้าโดยอัตโนมัติ ซึ่งเป็นสิ่งที่คุณต้องการเพื่อ **แปลง PDF เป็นภาพ** ก่อนทำการจดจำ

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**สิ่งที่เกิดขึ้น:**  
- PDF ถูกเปิดขึ้น  
- แต่ละหน้าเรนเดอร์ที่ 300 dpi (ค่าเริ่มต้น) เพื่อรักษารายละเอียดของอักขระ  
- วัตถุ bitmap ที่เรนเดอร์จะถูกเก็บไว้ในคอลเลกชัน `OcrInput`

หากคุณต้องการภาพดิบ (เพื่อดีบักหรือทำการประมวลผลล่วงหน้า) ให้เรียก `ocrInput.getPages()` หลังจากขั้นตอนนี้

## ขั้นตอนที่ 4 – รันกระบวนการ OCR (ทำ OCR บน PDF)

ตอนนี้งานหนักเริ่มขึ้นแล้ว เมธอด `recognize` จะวนลูปผ่านทุกภาพ, รันอัลกอริทึมจดจำ, และรวมผลลัพธ์ไว้ใน `OcrResult`

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**ทำไมคุณควรสนใจ:** `OcrResult` ไม่ได้มีแค่ข้อความธรรมดาเท่านั้น แต่ยังมีคะแนนความมั่นใจ, กล่องขอบเขต, และอ้างอิงภาพต้นฉบับ สำหรับการใช้งานส่วนใหญ่คุณแค่ต้องการ `getText()` เท่านั้น

## ขั้นตอนที่ 5 – ดึงและแสดงข้อความที่สกัดออกมา

สุดท้าย ดึงสตริงข้อความธรรมดาจากผลลัพธ์และพิมพ์ออกมา คุณยังสามารถบันทึกลงไฟล์, ส่งต่อไปยังดัชนีการค้นหา, หรือป้อนเข้าสู่ pipeline NLP ต่อไปได้

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หาก `scanned-report.pdf` มีเพียงย่อหน้าง่าย ๆ คุณจะเห็นข้อความประมาณนี้:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

รูปแบบจะสะท้อนโครงสร้างต้นฉบับโดยคงการขึ้นบรรทัดใหม่ไว้เท่าที่เป็นไปได้

## การจัดการกรณีขอบทั่วไป

### 1. PDF หลายภาษา

หากเอกสารของคุณมีข้อความภาษาฝรั่งเศสหรือสเปน ให้ตั้งค่าภาษาก่อนเรียก `recognize`:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

คุณสามารถส่งอาเรย์ของภาษาเพื่อให้เอนจินทำการตรวจจับอัตโนมัติได้

### 2. สแกนความละเอียดต่ำ

เมื่อทำงานกับสแกน 150 dpi ให้เพิ่ม DPI การเรนเดอร์ภายใน:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

DPI ที่สูงขึ้นช่วยให้ตัวอักษรคมชัดขึ้น แต่จะใช้หน่วยความจำมากขึ้น

### 3. PDF ขนาดใหญ่ (การจัดการหน่วยความจำ)

สำหรับ PDF ที่มีหลายสิบหน้า ให้ประมวลผลเป็นชุด:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

วิธีนี้จะช่วยป้องกันไม่ให้ heap ของ JVM เติบโตจนเกินขนาด

## ตัวอย่างเต็มพร้อมรัน

ด้านล่างเป็นโปรแกรมสมบูรณ์—รวมการ import และการจัดการลิขสิทธิ์—เพื่อให้คุณคัดลอกและรันได้ทันที

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

รันด้วยคำสั่ง:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

คุณควรเห็นข้อความที่สกัดออกมาปรากฏบนคอนโซล

## สรุป – สิ่งที่เราได้ครอบคลุม

- **วิธีใช้ OCR** ใน Java ด้วย Aspose.OCR  
- ขั้นตอนการ **ดึงข้อความจาก PDF**  
- ภายในไลบรารีจะ **แปลง PDF เป็นภาพ** ก่อนทำการจดจำอักขระ  
- เคล็ดลับสำหรับ **ทำ OCR บน PDF** ที่มีหลายภาษา, สแกนความละเอียดต่ำ, และเอกสารขนาดใหญ่  
- ตัวอย่างโค้ดที่พร้อมรันที่คุณสามารถใส่ลงในโปรเจกต์ Java ใดก็ได้

## ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

เมื่อคุณสามารถ **จดจำ PDF ที่สแกน** ได้แล้ว ลองสำรวจไอเดียต่อไปนี้:

- **สร้าง PDF ที่ค้นหาได้** – นำข้อความ OCR กลับไปวางบน PDF ต้นฉบับเพื่อสร้างเอกสารที่ค้นหาได้  
- **บริการประมวลผลแบบแบตช์** – ห่อหุ้มโค้ดใน microservice ของ Spring Boot ที่รับ PDF ผ่าน REST  
- **เชื่อมต่อกับ Elasticsearch** – ทำดัชนีข้อความที่สกัดเพื่อการค้นหาเต็มข้อความอย่างรวดเร็วในคลังเอกสารของคุณ  
- **การประมวลผลภาพล่วงหน้า** – ใช้ OpenCV เพื่อลบการเอียงหรือสัญญาณรบกวนของหน้า ก่อนทำ OCR เพื่อความแม่นยำที่สูงขึ้น

หัวข้อเหล่านี้ต่อยอดจากแนวคิดหลักที่เราได้สำรวจไว้แล้ว อย่ากลัวที่จะทดลองและให้ OCR engine ทำงานหนักแทนคุณ

---

*ขอให้เขียนโค้ดสนุก! หากเจออุปสรรค—เช่นข้อผิดพลาดลิขสิทธิ์หรือผลลัพธ์เป็น null—แสดงความคิดเห็นด้านล่างได้เลย ฉันพร้อมช่วยดีบักเสมอ*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}