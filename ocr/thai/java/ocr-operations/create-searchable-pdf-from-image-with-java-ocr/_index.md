---
category: general
date: 2026-05-06
description: สร้าง PDF ที่ค้นหาได้จากภาพโดยใช้ Aspose OCR ใน Java เรียนรู้การแปลงภาพเป็น
  PDF เปิดใช้งานการแก้ไขการสะกดคำ และใช้ OCR GPU เพื่อผลลัพธ์ที่เร็วขึ้น
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: th
og_description: สร้าง PDF ที่ค้นหาได้จากภาพโดยใช้ Aspose OCR ใน Java คู่มือนี้แสดงวิธีแปลงภาพเป็น
  PDF เปิดใช้งานการแก้ไขการสะกดคำ และใช้ OCR GPU.
og_title: สร้าง PDF ที่ค้นหาได้จากภาพด้วย Java OCR
tags:
- OCR
- Java
- PDF
title: สร้าง PDF ที่ค้นหาได้จากภาพด้วย Java OCR
url: /th/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้จากรูปภาพด้วย Java OCR

เคยต้องการ **สร้าง PDF ที่สามารถค้นหาได้** จากรูปภาพที่สแกนแต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาส่วนใหญ่มักเจออุปสรรคนี้เมื่อต้องจัดการกับ PDF ที่มาจากภาพเป็นครั้งแรก โชคดีที่ด้วย Aspose OCR for Java คุณสามารถ **แปลงภาพเป็น PDF**, ทำให้ข้อความเป็นเนื้อหาที่เลือกได้, และแม้กระทั่งเพิ่มการแก้ไขการสะกดเพื่อผลลัพธ์ที่เรียบหรู

ในบทแนะนำนี้เราจะพาไปผ่านตัวอย่างที่สมบูรณ์พร้อมรันที่แสดงวิธี **ใช้ OCR GPU** เมื่อมี, วิธี **ประมวลผล OCR ของภาพ** อย่างมีประสิทธิภาพ, และเหตุผลที่การเปิดใช้งานการแก้ไขการสะกดมีความสำคัญต่อการค้นหาในขั้นต่อไป เมื่อเสร็จคุณจะมีวิธีคลิกเดียวเพื่อสร้าง PDF ที่สามารถค้นหาได้ซึ่งคุณสามารถส่งให้ผู้ใช้หรือเก็บเป็นเอกสารเพื่อการปฏิบัติตามข้อกำหนด

> **เคล็ดลับ:** หากคุณกำลังรันบนเครื่องที่ไม่มี GPU โค้ดจะสลับไปใช้ CPU อย่างราบรื่น ดังนั้นคุณไม่จำเป็นต้องเขียนใหม่ใด ๆ

## สิ่งที่คุณต้องการ

- **Java 8+** (โค้ดคอมไพล์ด้วย JDK 8 และใหม่กว่า)
- **Aspose OCR for Java** library (ดาวน์โหลด JAR ล่าสุดจากเว็บไซต์ Aspose)
- **input image** (JPEG, PNG, TIFF ฯลฯ) ที่คุณต้องการแปลงเป็น PDF ที่สามารถค้นหาได้
- (Optional) **GPU** ที่รองรับ CUDA หากคุณต้องการการจดจำที่เร็วที่สุด

ไม่มีเฟรมเวิร์กเพิ่มเติม, ไม่มีการตั้งค่า Maven/Gradle—เพียง JAR เดียวบน classpath แล้วคุณก็พร้อมใช้งาน

## ขั้นตอนที่ 1: เริ่มต้น OcrEngine – ใจกลางของกระบวนการ  

ก่อนอื่นเราจะสร้างอินสแตนซ์ `OcrEngine` และชี้ไปที่ไฟล์ต้นฉบับ วัตถุนี้เป็นเครื่องมือหลักที่จะอ่านภาพ, รันเครือข่ายประสาทเทียม, และส่งข้อความกลับมาให้เรา

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*ทำไมเรื่องนี้สำคัญ:* การเริ่มต้น engine ครั้งเดียวและใช้ซ้ำช่วยหลีกเลี่ยงค่าใช้จ่ายจากการโหลดไลบรารีเนทีฟหลายครั้ง—เป็นการเพิ่มประสิทธิภาพเล็กน้อยที่สะสมเมื่อคุณประมวลผลไฟล์หลายสิบไฟล์เป็นชุด

## ขั้นตอนที่ 2: เลือกอุปกรณ์ประมวลผล – ใช้ OCR GPU เมื่อเป็นไปได้  

หากเวิร์กสเตชันของคุณมี GPU ที่รองรับ, คุณสามารถบอก Aspose ให้ทำงานหนักบน GPU ได้ มิฉะนั้น engine จะสลับไปใช้ CPU โดยอัตโนมัติ

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*ประโยชน์คืออะไร?* การเร่งด้วย GPU สามารถลดเวลาประมวลผลหลายวินาทีต่อหน้า, โดยเฉพาะสำหรับการสแกนความละเอียดสูง การสลับกลับทำให้โค้ดเดียวทำงานได้ทุกที่ นั่นคือเหตุผลที่เราแนะนำ **use OCR GPU** เป็นการตั้งค่าเริ่มต้น

## ขั้นตอนที่ 3: เร่งความเร็วการสแกน – ใช้ทุกคอร์ของ CPU  

แม้ในขณะที่ GPU กำลังทำงาน, ขั้นตอนการเตรียมข้อมูลรอบข้างสามารถทำแบบขนานได้ การตั้งจำนวนเธรดให้เท่ากับจำนวนโปรเซสเซอร์ที่พร้อมใช้งานทำให้ engine สามารถประมวลผลหลายส่วนพร้อมกัน

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*หมายเหตุ:* บนแล็ปท็อป 4‑คอร์จะเปิดสี่เธรด; บนเวิร์กสเตชัน 16‑คอร์คุณจะได้รับประโยชน์เต็มที่ เพียงระวังว่าการเพิ่มเธรดจะทำให้ใช้หน่วยความจำมากขึ้น

## ขั้นตอนที่ 4: ทำความสะอาดภาพ – ตัวกรองการเตรียมข้อมูล  

การสแกนที่เบลอหรือมีเสียงรบกวนจะทำให้ได้ข้อความที่เป็นขยะ การเพิ่มตัวกรองในตัวสองสามตัวจะเพิ่มความแม่นยำอย่างมาก

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*ทำไมต้องใช้ตัวกรองเหล่านี้?* `DeskewFilter` แก้ไขการหมุนที่มักเกิดเมื่อเอกสารถูกสแกนด้วยมุม `NoiseRemovalFilter` กำจัดพิกเซลรบกวนที่อาจถูกตีความเป็นอักขระ คิดว่าเป็นการให้ OcrEngine มีกระดาษสะอาดเพื่ออ่าน

## ขั้นตอนที่ 5: เปิดฟีเจอร์อัจฉริยะ – เปิดการแก้ไขการสะกดและการตรวจจับภาษาอัตโนมัติ  

หากคุณทำงานกับเอกสารหลายภาษา หรือแค่ต้องการลดการพิมพ์ผิด, ให้เปิดตัวตรวจสอบการสะกดในตัวและให้ engine คาดเดาภาษา

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*เมื่อใดที่เป็นประโยชน์?* สมมติว่าการสแกนของคุณมีส่วนภาษาอังกฤษและสเปน ฟีเจอร์ตรวจจับอัตโนมัติจะสลับพจนานุกรมแบบเรียลไทม์, ส่วนการแก้ไขการสะกดจะทำความสะอาดอักขระที่อ่านผิดเช่น “0” แทน “O”. ขั้นตอนนี้สำคัญสำหรับการสร้าง **PDF ที่สามารถค้นหาได้** ที่ให้ผลลัพธ์ที่ถูกต้อง

## ขั้นตอนที่ 6: บันทึกผลลัพธ์ – แปลงภาพเป็น PDF และทำให้สามารถค้นหาได้  

สุดท้ายเราขอให้ engine เขียน PDF ที่ภาพต้นฉบับอยู่ด้านหลังชั้นข้อความที่มองไม่เห็น นี่คือกระบวนการ **แปลงภาพเป็น PDF** แบบคลาสสิก, แต่ PDF นี้ตอนนี้สามารถค้นหาได้

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

ไฟล์ผลลัพธ์ (`output-searchable.pdf`) สามารถเปิดได้ในโปรแกรมอ่าน PDF ใดก็ได้; คุณจะสามารถเลือก, คัดลอก, และค้นหาข้อความได้เหมือน PDF ปกติ ไม่ต้องใช้เครื่องมือเพิ่มเติม

## ตัวอย่างทำงานเต็มรูปแบบ – คัดลอกและรัน  

ด้านล่างเป็นโปรแกรมทั้งหมดพร้อมคอมไพล์ แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์ที่เก็บ `input.jpg`

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เมื่อคุณรันโปรแกรมคุณจะเห็นบรรทัดคอนโซล *“Searchable PDF generated successfully.”* การเปิด `output-searchable.pdf` ใน Adobe Reader จะทำให้คุณพิมพ์คำจากภาพต้นฉบับในช่องค้นหาและกระโดดไปยังตำแหน่งนั้นทันที

## คำถามทั่วไปและกรณีขอบ  

- **GPU ไม่ถูกตรวจพบจะทำอย่างไร?**  
  การเรียก `setDeviceType(OcrDeviceType.GPU)` ไม่ทำให้เกิดข้อผิดพลาด; มันเพียงสั่งให้ engine พยายามใช้ GPU ก่อน หากล้มเหลว engine จะสลับไปใช้ CPU อย่างเงียบ ๆ  

- **สามารถประมวลผลหลายภาพในรอบเดียวได้หรือไม่?**  
  ได้. ใส่โค้ดในลูป, เปลี่ยนชื่อไฟล์ในแต่ละรอบ, และใช้ `OcrEngine` อินสแตนซ์เดียวกันเพื่อรักษาการใช้หน่วยความจำให้ต่ำ  

- **PDF ของฉันใหญ่เกินไป—จะลดขนาดอย่างไร?**  
  หลังจาก OCR คุณสามารถใช้ API การปรับแต่ง PDF ของ Aspose, หรือเพียงลดขนาดภาพต้นฉบับก่อนส่งให้ engine (`ImageStream.fromFile(...).setResolution(150)` สำหรับ 150 DPI)  

- **ฉันต้องการรักษาความละเอียดของภาพต้นฉบับเพื่อการปฏิบัติตามกฎหมาย.**  
  ฟอร์แมต `PDF_SEARCHABLE` จะคงบิตแมพต้นฉบับไว้โดยตรง; ชั้นข้อความที่มองไม่เห็นจะถูกเพิ่มบนภาพโดยไม่เปลี่ยนแปลงคุณภาพภาพ  

## สรุปภาพรวม  

![ตัวอย่างการสร้าง PDF ที่สามารถค้นหาได้](placeholder-image.png "ตัวอย่างการสร้าง PDF ที่สามารถค้นหาได้")

*ข้อความแทนภาพ:* *ตัวอย่างการสร้าง PDF ที่สามารถค้นหาได้ – เครื่องมือ Java OCR แปลง JPG ที่สแกนเป็น PDF ที่สามารถค้นหาได้.*

## สรุป  

ตอนนี้คุณมี **โซลูชันครบวงจร** สำหรับการแปลงภาพใด ๆ ให้เป็น **PDF ที่สามารถค้นหาได้** ด้วย Aspose OCR for Java โดย **แปลงภาพเป็น PDF**, **เปิดใช้งานการแก้ไขการสะกด**, และ **ใช้ OCR GPU** เมื่อเป็นไปได้ คุณจะได้ผลลัพธ์ที่เร็ว, แม่นยำ, และสามารถค้นหาได้ซึ่งทำงานบนหลายแพลตฟอร์ม  

ต่อไปทำอะไร? ลองทดลองกับ:  

- **รูปแบบผลลัพธ์ที่ต่างกัน** (`PDF`, `DOCX`, `HTML`) เพื่อดูว่าชั้นข้อความทำงานอย่างไร  
- **พจนานุกรมกำหนดเอง** หากคุณประมวลผลศัพท์เฉพาะโดเมน  
- **การประมวลผลเป็นชุด** เพื่อจัดการสแกนหลายพันไฟล์โดยอัตโนมัติ  

คุณสามารถปรับจำนวนเธรด, เปลี่ยนตัวกรอง, หรือเชื่อมต่อ pipeline การเตรียมข้อมูลของคุณเองได้อย่างอิสระ รูปแบบหลักยังคงเหมือนเดิม: load → preprocess → configure → OCR → save.  

ขอให้เขียนโค้ดอย่างสนุกสนาน, และขอให้ PDF ของคุณสามารถค้นหาได้เสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}