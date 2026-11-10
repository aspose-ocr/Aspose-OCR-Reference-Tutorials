---
category: general
date: 2026-03-26
description: สร้าง PDF ที่ค้นหาได้โดยใช้ Aspose.OCR Java – เรียนรู้การโหลดภาพ OCR,
  ตั้งค่าภาษาเริ่มต้น, ดึงข้อความจากภาพและบันทึกเป็น PDF OCR.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: th
og_description: สร้าง PDF ที่ค้นหาได้ด้วย Aspose.OCR Java คู่มือขั้นตอนต่อขั้นตอนในการโหลดภาพ
  OCR ตั้งค่าภาษาเริ่มต้น ดึงข้อความจากภาพ และบันทึกเป็น PDF OCR.
og_title: สร้าง PDF ที่ค้นหาได้ด้วย Aspose.OCR – คู่มือ Java
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: สร้าง PDF ที่ค้นหาได้ด้วย Aspose.OCR – คู่มือ Java
url: /th/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้ด้วย Aspose.OCR – คู่มือ Java

เคยต้องการ **สร้าง PDF ที่สามารถค้นหาได้** จากเอกสารสแกนแต่ไม่รู้ว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาจำนวนมากเจออุปสรรคนี้เมื่อต้องทำ OCR ด้วย Java ข่าวดีคือ Aspose.OCR ทำให้กระบวนการทั้งหมด—ตั้งแต่การโหลดภาพ การตั้งค่าภาษาเริ่มต้น ไปจนถึงการบันทึก PDF ที่รองรับ OCR—เป็นเรื่องง่ายในขั้นตอนเดียว ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบ ซึ่ง **ดึงข้อความจากภาพ**, ให้คุณ **ตั้งค่าภาษาเริ่มต้น**, และจบด้วย **บันทึก PDF OCR** ที่คุณสามารถเปิดด้วยโปรแกรมอ่านใดก็ได้

เราจะครอบคลุมเคล็ดลับปฏิบัติบางอย่าง เช่น การเปิดใช้งานการเร่งความเร็วด้วย GPU เพื่อประมวลผลที่เร็วขึ้นและการจัดการเอกสารหลายภาษา (ภาษาทมิฬ + อังกฤษในตัวอย่างของเรา) เมื่อเสร็จคุณจะได้โค้ดสแนปช็อตที่พร้อมใช้งานในโปรเจกต์ของคุณ

## สิ่งที่คุณต้องการ

- **Java 17** (หรือ JDK รุ่นใหม่ใดก็ได้; Aspose.OCR รองรับ Java 8+)
- ไลบรารี **Aspose.OCR for Java** (ดาวน์โหลดจากเว็บไซต์อย่างเป็นทางการหรือเพิ่มผ่าน Maven)
- **ไฟล์ลิขสิทธิ์** (หรือรุ่นทดลอง 30 วัน)
- ไฟล์ภาพที่มีข้อความ (ตัวอย่างใช้ `sample-mixed-tamil-eng.jpg`)

ไม่มีเฟรมเวิร์กเพิ่มเติม ไม่มีการพึ่งพาเนทีฟ—เพียง Java ธรรมดาและไฟล์ Aspose.JARs

## ขั้นตอนที่ 1: สร้าง PDF ที่สามารถค้นหาได้ – ตั้งค่าโปรเจกต์

ก่อนที่เราจะลงลึกในโค้ด ให้แน่ใจว่าโปรเจกต์พร้อมสำหรับการ **สร้าง PDF ที่สามารถค้นหาได้**  

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **เคล็ดลับมืออาชีพ:** รักษาเวอร์ชันให้เป็นปัจจุบัน; รุ่นใหม่มักมีการแก้ไขประสิทธิภาพสำหรับการใช้ GPU

ตอนนี้สร้างคลาส Java ง่าย ๆ ชื่อ `RecentFeaturesDemo` คลาสนี้จะเก็บตรรกะทั้งหมดที่เราต้องการเพื่อ **โหลด OCR ภาพ**, ตั้งค่าภาษา, และสุดท้าย **บันทึก PDF OCR**  

## ขั้นตอนที่ 2: โหลด OCR ภาพและเริ่มต้น Engine

ขั้นตอนแรกที่แท้จริงในไพรเมลไลน์คือ **โหลด OCR ภาพ** ซึ่งบอก Aspose.OCR ว่าไฟล์ใดจะต้องวิเคราะห์  

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **ทำไมจึงสำคัญ:** การเปิดใช้งาน GPU (`setUseGpu(true)`) สามารถลดเวลาประมวลผลได้ถึง 70 % บนฮาร์ดแวร์สมัยใหม่ ในขณะที่การประมวลผลแบบขนานทำให้ CPU ไม่อยู่ในสถานะพักเมื่อ GPU ทำงาน  

## ขั้นตอนที่ 3: ตั้งค่าภาษาเริ่มต้น (และภาษาเสริม)

หากข้ามขั้นตอนนี้ Aspose.OCR จะพยายามเดาภาษา ซึ่งช้ากว่าและแม่นยำน้อยกว่า นี่คือวิธี **ตั้งค่าภาษาเริ่มต้น** เป็นภาษาทมิฬและเพิ่มภาษาอังกฤษเป็นตัวสำรอง  

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **คำอธิบาย:** ภาษาหลักมีผลต่อชุดอักขระและพจนานุกรมที่ใช้ระหว่างการจดจำ การเพิ่มภาษาที่สองเป็นสิ่งสำคัญสำหรับเอกสารที่มีสคริปต์ผสม (เช่น ใบเสร็จที่มีทั้งข้อความทมิฬและอังกฤษ)  
> **กรณีขอบ:** หากเอกสารของคุณมีมากกว่าสองภาษา คุณสามารถเรียก `addAdditionalLanguage(...)` สำหรับแต่ละภาษาที่เพิ่มเข้ามา  

## ขั้นตอนที่ 4: การเตรียมภาพล่วงหน้า – แก้ไขการเอียงและลดสัญญาณรบกวน

ภาพสแกนมักมีการเอียงหรือสัญญาณรบกวนพื้นหลัง การเตรียมล่วงหน้าช่วยให้ **ดึงข้อความจากภาพ** ทำได้อย่างเชื่อถือได้มากขึ้น  

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **เคล็ดลับ:** หากคุณมั่นใจว่าภาพสะอาดแล้ว สามารถข้าม `setDenoise(true)` เพื่อลดเวลาเพียงไม่กี่มิลลิวินาที  

## ขั้นตอนที่ 5: โหลดไฟล์ภาพ

เมื่อ Engine พร้อมแล้ว เราจะชี้ไปที่ไฟล์ที่ต้องการวิเคราะห์  

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **ถ้าเส้นทางผิด?** Aspose.OCR จะโยน `FileNotFoundException` ที่ชัดเจน คุณควรห่อการเรียกใน `try‑catch` หากต้องการจัดการข้อผิดพลาดอย่างสุภาพ  

## ขั้นตอนที่ 6: รัน OCR และดึงข้อความจากภาพ

เมื่อทุกอย่างตั้งค่าเรียบร้อย ถึงเวลารันการจดจำ ขั้นตอนนี้จะทั้ง **ดึงข้อความจากภาพ** และเตรียมข้อมูลที่จำเป็นสำหรับการสร้าง PDF  

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

ผลลัพธ์ที่แสดงในคอนโซลสำหรับภาพตัวอย่างจะเป็นดังนี้  

```
வணக்கம் World
This is a mixed language sample.
```

คุณจะสังเกตเห็นว่าบรรทัดภาษาทมิฬแสดงผลอย่างถูกต้อง ตามด้วยภาษาอังกฤษ นั่นคือผลลัพธ์ของการ **ตั้งค่าภาษาเริ่มต้น** อย่างถูกต้อง  

## ขั้นตอนที่ 7: บันทึก OCR PDF – ส่วนสุดท้ายของปริศนา

ส่วนสุดท้ายของกระบวนการคือ **บันทึก OCR PDF** Aspose.OCR สามารถฝังชั้นข้อความที่มองไม่เห็นเหนือภาพต้นฉบับ ทำให้ PDF สามารถค้นหาได้  

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

เปิด `searchable.pdf` ใน Adobe Reader, กด **Ctrl + F**, คุณจะสามารถค้นหาคำทั้งภาษาทมิฬและอังกฤษได้—ตรงกับที่กระบวนการ **สร้าง PDF ที่สามารถค้นหาได้** สัญญาไว้  

## ตัวอย่างทำงานเต็มรูปแบบ (คัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคอมไพล์และรันได้ทันที แทนที่เส้นทางตัวอย่างด้วยไดเรกทอรีของคุณเอง  

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

รันด้วยคำสั่ง:  

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

คุณควรเห็นข้อความที่ดึงจากภาพแสดงในคอนโซล ตามด้วยการยืนยันว่า **PDF ที่สามารถค้นหาได้** ถูกเขียนลงดิสก์แล้ว  

## คำถามทั่วไป & กรณีขอบ

### ถ้าฉันต้องการ **โหลด OCR ภาพ** จากอาร์เรย์ไบต์?

คุณสามารถแทนที่ `ImageStream.fromFile(imagePath)` ด้วย `ImageStream.fromBytes(byteArray)` วิธีนี้สะดวกเมื่อภาพมาจากฐานข้อมูลหรือเว็บเซอร์วิส  

### ฉันจะจัดการกับ PDF ที่มีภาพอยู่แล้วอย่างไร?

Aspose.OCR สามารถทำงานกับหน้า PDF โดยตรง: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))` Engine จะทำการแรสเตอร์แต่ละหน้าโดยอัตโนมัติก่อนการจดจำ  

### GPU ของฉันไม่ถูกตรวจจับ—ควรเก็บ `setUseGpu(true)` ไว้หรือไม่?

หาก `setUseGpu(true)` ล้มเหลว Aspose.OCR จะสลับไปใช้ CPU โดยอัตโนมัติ คุณสามารถตรวจสอบ `ocrEngine.getEngineSettings().isGpuAvailable()` ก่อนเปิดใช้งานได้  

### ฉันสามารถ **บันทึก OCR PDF** พร้อมเมตาดาต้ากำหนดเองได้หรือไม่?

ได้ หลังจากจดจำเสร็จ ใช้ `ocrEngine.getPdfSaveOptions().setTitle("My Document")` หรือ `setAuthor("John Doe")` ก่อนเรียก `save`  

## เคล็ดลับประสิทธิภาพสำหรับการประมวลผลเป็นชุดใหญ่

- **การประมวลผลเป็นชุด:** ใช้ instance ของ `OcrEngine` เดียวกันสำหรับหลายภาพเท่านั้น เรียก `ocrEngine.clear()` ระหว่างการรันแต่ละครั้ง  
- **Thread pool:** ห่อแต่ละงานภาพใน `Callable` แล้วส่งให้ `ExecutorService` เนื่องจากเราเปิดการประมวลผลแบบขนานแต่ละเธรดจะได้ประโยชน์จากหลายคอร์  
- **การจัดการหน่วยความจำ:** สำหรับภาพขนาดกิกะพิกเซล พิจารณาลดขนาดด้วย `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` เพื่อให้การใช้ RAM อยู่ในระดับที่จัดการได้  

## สรุป

เราได้เดินผ่านกระบวนการ **สร้าง PDF ที่สามารถค้นหาได้** อย่างครบถ้วนด้วย Aspose.OCR สำหรับ Java ตั้งแต่ **โหลด OCR ภาพ**, เรา  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}