---
category: general
date: 2026-04-26
description: สร้าง PDF ที่ค้นหาได้จากภาพโดยใช้ Aspose OCR ใน Java เรียนรู้การแปลงภาพเป็น
  PDF, OCR ภาพเป็น PDF, และดึงข้อความจากภาพอย่างรวดเร็ว.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- extract text from image
- how to set language
language: th
og_description: สร้าง PDF ที่ค้นหาได้จากภาพโดยใช้ Aspose OCR คู่มือนี้แสดงวิธีแปลงภาพเป็น
  PDF, ทำ OCR ภาพเป็น PDF, และสกัดข้อความจากภาพ.
og_title: สร้าง PDF ที่ค้นหาได้จากภาพด้วย Java OCR
tags:
- Java
- OCR
- PDF
title: สร้าง PDF ที่ค้นหาได้จากภาพด้วย Java OCR
url: /th/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้จากรูปภาพด้วย Java OCR

เคยต้องการ **create searchable PDF** จากใบแจ้งหนี้ที่สแกนแล้วแต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไร? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อพวกเขาต้องการ PDF ที่สามารถค้นหาได้จริง ข่าวดีคือ? ด้วย Aspose OCR for Java คุณสามารถ **convert image to PDF**, รัน OCR แบบทันที และได้ไฟล์ที่สามารถค้นหาได้อย่างเรียบร้อยในไม่กี่บรรทัดของโค้ด

ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด: โหลดรูปภาพ, แจ้งให้เอนจินทราบว่าคาดว่าจะใช้ภาษาอะไร, ทำ OCR, และสุดท้ายบันทึกเป็น **searchable PDF**. เมื่อจบคุณจะรู้วิธี **extract text from image** ด้วยตนเอง, ปรับแต่งการตั้งค่าภาษา, และจัดการกับกรณีขอบที่พบบ่อยบางอย่าง. ไม่มีบริการภายนอก, ไม่มีเครื่องมือบรรทัดคำสั่งที่ซับซ้อน—เพียงแค่ Java ธรรมดา

## สิ่งที่คุณต้องการ

- Java 17 หรือใหม่กว่า (API ทำงานกับเวอร์ชันเก่าได้เช่นกัน แต่ 17 เป็นจุดที่เหมาะสมที่สุด).  
- ไลบรารี Aspose OCR for Java – คุณสามารถดาวน์โหลด JAR ล่าสุดจาก Maven Central (`com.aspose:aspose-ocr:23.10`).  
- ไฟล์รูปภาพที่มีข้อความที่อ่านได้ (PNG, JPG หรือ TIFF ก็ใช้ได้).  
- ความอดทนเล็กน้อยกับ IDE—IntelliJ IDEA หรือ VS Code ก็เพียงพอ.

หากคุณมีแล้ว เยี่ยม! หากยังไม่มี snippet Maven ด้านล่างจะช่วยให้คุณเริ่มต้นได้:

```xml
<!-- Add to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

ตอนนี้พื้นฐานพร้อมแล้ว, มาเจาะลึกโค้ดกันเถอะ.

## ขั้นตอนที่ 1: เริ่มต้น OCR engine – หัวใจของ **create searchable pdf**

ก่อนที่การแปลงใด ๆ จะเกิดขึ้น คุณต้องสร้างอินสแตนซ์ของ `OcrEngine` คิดว่ามันเป็นสมองที่จะอ่านพิกเซลและแปลงเป็นอักขระ.

```java
import com.aspose.ocr.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*ทำไมเรื่องนี้ถึงสำคัญ:* เอนจินเก็บการตั้งค่าการจดจำทั้งหมด (ภาษา, โหมดความแม่นยำ, ฯลฯ). การสร้างครั้งเดียวและใช้ซ้ำกับหลายภาพจะมีประสิทธิภาพกว่าการสร้างเอนจินใหม่สำหรับแต่ละไฟล์.

## ขั้นตอนที่ 2: **How to set language** – ปรับปรุงความแม่นยำสำหรับ French, German, หรือสคริปต์ใด ๆ

หากคุณรู้ภาษาของเอกสารต้นฉบับ ให้บอก OCR engine นั่นจะช่วยเร่งการประมวลผลและลดการจดจำผิดพลาด.

```java
        // Step 2: (Optional) Specify the language to improve text extraction
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

คุณสามารถแทนที่ `OcrLanguage.FRENCH` ด้วย `ENGLISH`, `SPANISH`, `GERMAN` ฯลฯ หากไม่แน่ใจ ให้ลบบรรทัดนั้นออกและให้ Aspose คาดเดา—แต่คาดว่าจะมีความแม่นยำลดลงเล็กน้อย.

## ขั้นตอนที่ 3: โหลดภาพที่คุณต้องการ **convert image to pdf**

`เมธอด` `setImage` รับพาธไฟล์, `InputStream`, หรือแม้กระทั่งอ็อบเจ็กต์ `java.awt.Image`. หากคุณมีอาร์เรย์ไบต์ (เช่นจากการอัปโหลดเว็บ) ให้ห่อไว้ใน `ByteArrayInputStream` แล้วส่งต่อโดยตรง.

```java
        // Step 3: Load the image that contains the text to be recognized
        ocrEngine.setImage("YOUR_DIRECTORY/french_invoice.png");
```

## ขั้นตอนที่ 4: ทำ OCR และ **ocr image to pdf** ในหนึ่งคำสั่ง

Aspose ทำขั้นตอนนี้ง่ายดาย: `recognizeToPdf` รันเอนจินการจดจำและเขียน PDF ที่สามารถค้นหาได้ในหนึ่งครั้ง.

```java
        // Step 4: Recognize the text and save it as a searchable PDF
        ocrEngine.recognizeToPdf("YOUR_DIRECTORY/french_invoice_searchable.pdf");
```

ภายใต้การทำงาน, ไลบรารีสร้างเลเยอร์ข้อความที่มองไม่เห็นซึ่งสอดคล้องกับภาพต้นฉบับ. เมื่อคุณเปิดไฟล์ที่ได้ใน Adobe Reader, คุณจะสามารถพิมพ์คำลงในช่องค้นหาและกระโดดไปยังตำแหน่งที่ตรงกันได้ทันที.

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์ – ผลลัพธ์ดูเป็นอย่างไร?

```java
        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF generated.");
    }
}
```

รันโปรแกรม, จากนั้นเปิด `french_invoice_searchable.pdf`. ลองค้นหาคำที่คุณรู้ว่ามีในใบแจ้งหนี้ (เช่น “Total”). หากการไฮไลท์ไปที่ตำแหน่งที่ถูกต้อง, คุณได้ **create searchable pdf** อย่างสำเร็จ.  
![ตัวอย่างการสร้าง PDF ที่สามารถค้นหาได้](example.png)<!-- alt text includes primary keyword -->

### ผลลัพธ์ที่คาดหวัง

```
Searchable PDF generated.
```

และไฟล์ PDF ที่อยู่ใน `YOUR_DIRECTORY` ที่คุณสามารถแชร์, ทำดัชนี, หรือเก็บรักษาได้.

## ขั้นตอนที่ 6: ดึงข้อความดิบจากภาพ (ทางเลือก)

บางครั้งคุณต้องการข้อความธรรมดาสำหรับการประมวลผลต่อ—อาจจะใส่ลงฐานข้อมูลหรือรันการวิเคราะห์ความรู้สึก. Aspose ให้คุณดึงข้อความที่จดจำได้โดยตรง:

```java
        // Optional: Get the extracted text as a String
        String extractedText = ocrEngine.getText();
        System.out.println("Extracted text:");
        System.out.println(extractedText);
```

โค้ดส่วนนี้แสดงวิธี **extract text from image** โดยไม่ต้องสร้าง PDF. มันมีประโยชน์เมื่อคุณสนใจเฉพาะเนื้อหา ไม่ใช่การจัดวางภาพ.

## การจัดการหลายหน้า หรือหลายภาพ

ถ้าแหล่งของคุณเป็น TIFF หลายหน้า หรือโฟลเดอร์ของ JPEG? คุณสามารถวนลูปไฟล์และเรียก `recognizeToPdf` สำหรับแต่ละไฟล์, จากนั้นรวม PDF ด้วย Aspose PDF หรือไลบรารีอื่น. นี่คือตัวอย่างสั้น ๆ:

```java
import java.io.File;
import com.aspose.pdf.*;

public class MultiPageDemo {
    public static void main(String[] args) throws Exception {
        OcrEngine engine = new OcrEngine();
        File folder = new File("YOUR_DIRECTORY/images");
        Document finalDoc = new Document();

        for (File img : folder.listFiles((d, n) -> n.matches(".*\\.(png|jpg|tif)"))) {
            engine.setImage(img.getAbsolutePath());
            // Save each page as a temporary PDF
            String tempPdf = img.getName() + ".pdf";
            engine.recognizeToPdf(tempPdf);
            // Append to final document
            Document pageDoc = new Document(tempPdf);
            finalDoc.getPages().add(pageDoc.getPages().get_Item(1));
        }
        finalDoc.save("YOUR_DIRECTORY/combined_searchable.pdf");
        System.out.println("All pages merged into searchable PDF.");
    }
}
```

**เคล็ดลับ:** ลบ PDF ชั่วคราวหลังการรวมเพื่อให้พื้นที่ทำงานเป็นระเบียบ.

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

- **Low‑resolution images:** ความแม่นยำของ OCR ลดลงอย่างมากเมื่อความละเอียดต่ำกว่า 150 dpi. ขยายหรือขอสแกนความละเอียดสูงขึ้นหากทำได้.  
- **Skewed pages:** ภาพที่หมุนอาจทำให้เอนจินสับสน. ใช้ `ocrEngine.getImagePreprocessingSettings().setDeskew(true)` เพื่อแก้ไขการเอียงเล็กน้อยโดยอัตโนมัติ.  
- **Unsupported language:** ตรวจสอบว่าภาษาที่คุณตั้งค่าอยู่ในลิขสิทธิ์ Aspose OCR ของคุณ; มิฉะนั้นเอนจินจะกลับไปใช้ภาษาอังกฤษ.  
- **Large files:** การประมวลผล TIFF ขนาด 30 MB อาจใช้หน่วยความจำมาก. พิจารณาแยกไฟล์เป็นส่วนย่อยหรือเพิ่มขนาด heap ของ JVM (`-Xmx2g`).

## ขั้นตอนต่อไป – ไปต่อจากที่นี่

ตอนนี้คุณได้เชี่ยวชาญพื้นฐานของ **create searchable pdf** แล้ว, คุณอาจต้องการสำรวจต่อ:

- **Batch conversion:** ผสานรูปแบบหลายหน้าเข้ากับตัวกำหนดเวลาเพื่อประมวลผลการสแกนที่เข้ามาในแต่ละคืน.  
- **Metadata injection:** ใช้ Aspose PDF เพื่อเพิ่มชื่อเรื่อง, ผู้เขียน, หรือแท็กที่กำหนดเองลงใน PDF ที่สามารถค้นหาได้.  
- **Digital signatures:** ปกป้อง PDF ด้วยใบรับรองหลัง OCR, เพื่อให้เป็นไปตามข้อกำหนดของเอกสารทางกฎหมาย.  

ส่วนขยายทั้งหมดนี้ยังคงอิงกับแนวคิดหลักที่เราได้อธิบาย: การเริ่มต้น OCR engine, การตั้งค่าภาษาแบบเลือก, การโหลดภาพ, และการเรียก `recognizeToPdf`.

---

### TL;DR

เราได้เดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งแสดงวิธี **create searchable PDF** จากภาพโดยใช้ Aspose OCR for Java. ขั้นตอนรวมถึงการเริ่มต้นเอนจิน, การตั้งค่าภาษาแบบเลือก (ตอบคำถาม “how to set language”), การโหลดภาพ, ทำ OCR, บันทึก PDF ที่สามารถค้นหาได้, และการดึงข้อความธรรมดาแบบเลือก. เรายังได้อธิบายการจัดการหลายหน้า, ข้อผิดพลาดทั่วไป, และแนวคิดสำหรับการทำอัตโนมัตืต่อไป.

ลองใช้กับใบเสร็จ, สัญญา, หรือบันทึกมือของคุณ—เปลี่ยนภาพคงที่เหล่านั้นให้เป็นเอกสารที่สามารถค้นหาได้เต็มรูปแบบในไม่กี่วินาที. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}