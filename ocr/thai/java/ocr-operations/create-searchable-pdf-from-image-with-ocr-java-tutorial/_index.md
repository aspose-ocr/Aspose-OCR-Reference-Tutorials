---
category: general
date: 2026-01-07
description: สร้าง PDF ที่ค้นหาได้จากรูปภาพโดยใช้ Aspose OCR ใน Java เรียนรู้วิธีแปลงรูปภาพเป็น
  PDF จดจำข้อความจากรูปภาพและสร้าง PDF จาก JPG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: th
og_description: สร้าง PDF ที่ค้นหาได้จากภาพด้วย Aspose OCR ใน Java คู่มือขั้นตอนต่อขั้นตอนในการแปลงภาพเป็น
  PDF, จำแนกข้อความจากภาพและสร้าง PDF จาก JPG.
og_title: สร้าง PDF ที่ค้นหาได้จากรูปภาพ – คู่มือ Java OCR
tags:
- OCR
- Java
- PDF
- Aspose
title: สร้าง PDF ที่ค้นหาได้จากรูปภาพด้วย OCR – บทเรียน Java
url: /th/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้จากภาพด้วย OCR – บทแนะนำ Java

เคยต้องการ **สร้าง PDF ที่ค้นหาได้** จากภาพสแกนแต่ไม่รู้ว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อลองแปลง JPEG เป็น PDF ที่สามารถค้นหาได้จริง  

ในคู่มือนี้เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งจะแสดงวิธี **แปลงภาพเป็น PDF**, **จดจำข้อความจากภาพ**, และสุดท้าย **สร้าง PDF จาก JPG** ด้วย Aspose OCR for Java ไม่มีการอ้างอิงที่คลุมเครือ เพียงโค้ดที่คุณสามารถคัดลอก‑วางและรันได้ทันที  

## สิ่งที่คุณต้องเตรียม

* **Java 17** หรือใหม่กว่า (API ทำงานกับ JDK รุ่นล่าสุดใดก็ได้)  
* ไลบรารี **Aspose.OCR for Java** – คุณสามารถดาวน์โหลด JAR ล่าสุดจาก Maven Central หรือเว็บไซต์ของ Aspose  
* รูปตัวอย่าง เช่น `sample.jpg` วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงได้  
* IDE หรือเครื่องมือแก้ไขข้อความง่าย ๆ พร้อมเทอร์มินัล—อะไรก็ตามที่คุณสะดวกใช้  

เท่านี้แค่นั้น ไม่มีเฟรมเวิร์กหนัก ๆ ไม่มีการพึ่งพาเนทีฟเพิ่มเติม มาเริ่มกันเลย  

## ขั้นตอนที่ 1 – สร้าง PDF ที่ค้นหาได้: เริ่มต้น OCR Engine

สิ่งแรกที่เราทำคือสร้างอินสแตนซ์ของ `OcrEngine` และชี้ไปที่ภาพต้นฉบับ วัตถุนี้เป็นหัวใจของ Aspose OCR; มันจัดการทุกอย่างตั้งแต่การโหลดบิตแมพจนถึงการเปิดเผยข้อความที่จดจำได้  

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **ทำไมเรื่องนี้สำคัญ:** การเริ่มต้น engine อย่างถูกต้องทำให้ไลบรารีสามารถอ่านรูปแบบภาพที่คุณส่งให้ได้ หากพาธผิดคุณจะได้รับ `FileNotFoundException` และกระบวนการทั้งหมดจะหยุด  

## ขั้นตอนที่ 2 – เพิ่มประสิทธิภาพ: เปิดใช้ GPU, CPU หลายคอร์ และการแก้ไขการสะกด

OCR สามารถใช้ CPU มาก โดยเฉพาะกับเอกสารขนาดใหญ่ Aspose มีตัวเลือกหลายอย่างที่คุณสามารถปรับเพื่อทำให้กระบวนการเร็วขึ้นและแม่นยำขึ้น  

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **เคล็ดลับ:** หากคุณรันบนเซิร์ฟเวอร์ที่ไม่มี GPU, `setUseGpu(false)` จะไม่ทำให้เกิดปัญหา—คุณจะ **กลับไปใช้** การประมวลผลด้วย CPU หลายคอร์แทน  

## ขั้นตอนที่ 3 – ปรับปรุงคุณภาพภาพ: แก้ไขการเอียงและกำจัดจุดรบกวน (ไม่บังคับแต่แนะนำ)

การสแกนมักไม่สมบูรณ์แบบ การเอียงเล็กน้อยหรือสัญญาณรบกวนอาจทำให้ตัวจดจำทำงานผิดพลาด คลาส `ImageProcessingOptions` ช่วยให้คุณทำความสะอาดภาพก่อนที่ engine จะพยายามอ่าน  

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **กรณีขอบ:** หากภาพต้นฉบับของคุณสะอาดแล้ว คุณสามารถข้ามขั้นตอนนี้ได้ มันไม่ทำให้เกิดปัญหา แต่จะเพิ่มเวลาเพียงไม่กี่มิลลิวินาที  

## ขั้นตอนที่ 4 – จดจำข้อความจากภาพและสร้าง PDF

ตอนนี้จุดสำคัญเกิดขึ้น เราเรียก `recognize()` และ engine จะคืนค่า `OcrResult` จากนั้นเราสามารถบันทึกผลลัพธ์ในหลายรูปแบบ—PDF เป็นรูปแบบที่พบบ่อยที่สุดสำหรับเอกสารที่ค้นหาได้  

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **สิ่งที่คุณจะเห็น:** `sample-output.pdf` มีภาพต้นฉบับเป็นชั้นพื้นหลัง ส่วนข้อความที่จดจำได้อยู่ด้านบนเป็นเลเยอร์ที่มองไม่เห็น เปิดไฟล์ใน Adobe Reader แล้วลองเลือกข้อความ—คุณจะต้องประหลาดใจ  

## ขั้นตอนที่ 5 – ตรวจสอบผลลัพธ์ของการสร้าง PDF ที่ค้นหาได้

หลังจากไฟล์ถูกเขียนแล้ว การตรวจสอบอีกครั้งว่ามีการค้นหาได้จริงเป็นแนวปฏิบัติที่ดี  

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

เปิด PDF, กด **Ctrl F**, พิมพ์คำที่คุณรู้ว่ามีอยู่ในภาพ—หากการค้นหาพบคำนั้น คุณได้ **สร้าง PDF ที่ค้นหาได้** อย่างสำเร็จ!  

## วิธีใช้ OCR ในสถานการณ์จริง (โบนัส)

* **การประมวลผลเป็นชุด:** ใส่โค้ดในลูปที่วนผ่านโฟลเดอร์ของ JPGs จำไว้ว่าให้ใช้ `OcrEngine` ตัวเดียวเพื่อประหยัดหน่วยความจำ  
* **การสนับสนุนภาษา:** Aspose OCR รองรับกว่า 60 ภาษา เพียงเรียก `ocrEngine.getEngineOptions().setLanguage(Language.English);` (หรือค่า enum อื่น)  
* **การจัดการข้อผิดพลาด:** ดัก `OcrException` เพื่อจัดการไฟล์ที่เสียหายอย่างราบรื่น  

การปรับแต่งเหล่านี้ทำให้โซลูชันมีความทนทานพอสำหรับไพรไลน์การผลิต  

## ตัวอย่าง Java ครบชุด – สร้าง PDF ที่ค้นหาได้จาก JPG

ด้านล่างเป็นโปรแกรมเต็มรูปแบบที่สามารถคอมไพล์และรันได้ทันที แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริงบนเครื่องของคุณ  

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

เปิด PDF ที่สร้างขึ้นและคุณควรจะสามารถค้นหาคำใดก็ได้ที่ปรากฏใน `sample.jpg` หากคุณไม่เห็นเลเยอร์ข้อความ ให้ตรวจสอบพาธของภาพอีกครั้งและตรวจสอบว่า OCR engine ไม่ได้โยนข้อยกเว้นที่ซ่อนอยู่  

## สรุป

เราเพิ่งแสดงวิธี **สร้าง PDF ที่ค้นหาได้** จาก JPEG ด้วย Aspose OCR for Java ตั้งแต่การโหลดภาพ, ปรับตั้งค่าประสิทธิภาพ, ทำความสะอาดภาพ, จนถึงการจดจำข้อความและบันทึกเป็น PDF ที่ค้นหาได้—แต่ละขั้นตอนอธิบายด้วย *เหตุผล* และ *วิธีทำ*  

ตอนนี้คุณสามารถ **แปลงภาพเป็น PDF**, **จดจำข้อความจากภาพ**, และ **สร้าง PDF จาก JPG** ในแอปของคุณเอง ขั้นต่อไป ลองประมวลผลโฟลเดอร์สแกนทั้งหมด, ทดลองกับภาษาต่าง ๆ, หรือเพิ่มการป้องกันด้วยรหัสผ่านให้กับ PDF ที่ออกมา ไม่มีขีดจำกัด  

มีคำถามเกี่ยวกับกรณีขอบ, การไลเซนส์, หรือการปรับประสิทธิภาพ? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!  

![Diagram illustrating OCR pipeline – create searchable pdf](/images/ocr-pipeline.png "Create searchable PDF diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}