---
category: general
date: 2026-02-17
description: เตรียมภาพสำหรับ OCR ด้วย Aspose OCR ใน Java เรียนรู้การเพิ่มความคมของภาพ
  ตั้งค่าระดับความคม และจดจำข้อความจากภาพได้ภายในไม่กี่นาที.
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: th
og_description: เตรียมภาพล่วงหน้าสำหรับ OCR ด้วย Aspose OCR Java คู่มือนี้แสดงวิธีเพิ่มความคมชัดของภาพ
  ตั้งค่าระดับความคมชัด และจดจำข้อความจากภาพอย่างรวดเร็ว.
og_title: การเตรียมภาพสำหรับ OCR – บทเรียน Java เพื่อเพิ่มคอนทราสต์และสกัดข้อความ
tags:
- Java
- OCR
- Image Processing
title: การเตรียมภาพสำหรับ OCR – คู่มือ Java ครบวงจรเพื่อเพิ่มคอนทราสต์และดึงข้อความ
url: /th/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การเตรียมภาพสำหรับ OCR – คู่มือ Java ฉบับสมบูรณ์

เคยต้องการ **preprocess image for OCR** แต่ไม่แน่ใจว่าการตั้งค่าใดทำให้ผลลัพธ์แตกต่างจริงหรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอเรื่องนี้. นักพัฒนาส่วนใหญ่จะโยนภาพเข้าไปในเครื่อง OCR แล้วหวังว่าเวทมนตร์จะทำงาน, แต่กลับได้ผลลัพธ์ที่อ่านไม่ออก. ในบทแนะนำนี้เราจะพาคุณผ่านตัวอย่างเชิงปฏิบัติแบบครบวงจรที่ **boosts image contrast**, ปรับ **contrast level**, และสุดท้าย **recognizes text from image** ด้วย Aspose OCR for Java.

เมื่อคุณทำเสร็จแล้ว, คุณจะได้โค้ดสแนปช็อตที่สามารถใช้ซ้ำได้ซึ่ง **extracts text using OCR** อย่างเชื่อถือได้, แม้ในสแกนที่มีเสียงรบกวน. ไม่มีเทคนิคลับ, มีเพียงขั้นตอนที่ชัดเจนและเหตุผลเบื้องหลังแต่ละขั้นตอน.

## สิ่งที่คุณต้องการ

- Java 17 หรือใหม่กว่า (โค้ดสามารถคอมไพล์กับ JDK ล่าสุดใดก็ได้)
- ไลบรารี Aspose OCR for Java (ดาวน์โหลดจากเว็บไซต์อย่างเป็นทางการของ Aspose)
- ไฟล์ลิขสิทธิ์ Aspose OCR ที่ถูกต้อง (`Aspose.OCR.lic`)
- ภาพอินพุต (`input.jpg`) ที่คุณต้องการอ่าน
- IDE ที่คุณชื่นชอบหรือการตั้งค่าแบบบรรทัดคำสั่งง่าย ๆ

หากคุณมีทั้งหมดนี้แล้ว, เยี่ยม—มาเริ่มกันเลย.

## ขั้นตอนที่ 1: โหลดลิขสิทธิ์ Aspose OCR (การตั้งค่าเบื้องต้น)

ก่อนที่เครื่อง OCR จะทำงานใด ๆ, มันต้องรู้ว่าคุณมีลิขสิทธิ์แล้ว. มิฉะนั้นคุณจะเจอลายน้ำเวอร์ชันทดลอง.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**ทำไมเรื่องนี้ถึงสำคัญ:** หากไม่มีลิขสิทธิ์ที่ถูกต้อง, เครื่องจะทำงานในโหมดประเมินผล, ซึ่งอาจทำให้ผลลัพธ์ถูกตัดหรือมีลายน้ำ. การตั้งค่าลิขสิทธิ์ตั้งแต่แรกยังช่วยให้ตัวเลือกการเตรียมภาพใด ๆ ที่ตามมาถูกนำไปใช้ในโหมดเต็มคุณสมบัติ.

## ขั้นตอนที่ 2: เริ่มต้น OcrEngine

การสร้างอินสแตนซ์ `OcrEngine` จะทำให้คุณเข้าถึงทั้ง pipeline การจดจำและการเตรียมภาพ.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**เคล็ดลับ:** เก็บ engine เป็น singleton หากคุณวางแผนจะประมวลผลหลายภาพในชุด; มันจะเก็บแคชทรัพยากรภายในและเร่งการเรียกใช้ครั้งต่อไป.

## ขั้นตอนที่ 3: กำหนดค่าการเตรียมภาพ – Deskew, Denoise, และการเพิ่มคอนทราสต์

นี่คือจุดที่เราจะ **preprocess image for OCR**. สามตัวควบคุมที่เราจะปรับคือ:

1. **Deskew** – แก้ไขการหมุนเล็กน้อย.
2. **Denoise** – ลบจุดรบกวนที่ทำให้การแยกอักขระสับสน.
3. **Contrast enhancement** – ทำให้ข้อความสีเข้มเด่นชัดขึ้นจากพื้นหลัง.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### ทำไมต้องปรับระดับคอนทราสต์?

การเพิ่มระดับคอนทราสต์จะขยายฮิสโตแกรมของภาพ, ทำให้พิกเซลสีเข้มเข้มขึ้นและพิกเซลสีสว่างสว่างขึ้น. ในการใช้งานจริง, **contrast level** ที่ `1.3f` มักให้สมดุลที่ดีที่สุดสำหรับเอกสารพิมพ์, ในขณะที่ค่าที่มากกว่า `1.5f` อาจทำให้เส้นบาง ๆ แสงจ้าเกินไป. คุณสามารถทดลองได้ตามต้องการ; การตั้งค่านี้เปลี่ยนแปลงได้ง่ายและสามารถปรับปรุงอัตราความสำเร็จของ **recognize text from image** อย่างมาก.

## ขั้นตอนที่ 4: เตรียมภาพอินพุต

คลาส `OcrInput` จัดการไฟล์ให้คุณโดยอัตโนมัติ. คุณสามารถเพิ่มหลายภาพได้หากต้องการประมวลผลเป็นชุด.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**กรณีขอบ:** หากภาพของคุณอยู่ในรูปแบบที่ไม่มาตรฐาน (เช่น TIFF ที่มีหลายหน้า), คุณสามารถโหลดแต่ละหน้าต่างหากหรือแปลงเป็น PNG/JPEG ก่อน.

## ขั้นตอนที่ 5: ทำการจดจำ

ตอนนี้ engine จะรัน pipeline การเตรียมภาพที่เราตั้งค่าไว้, จากนั้นส่งภาพที่ทำความสะอาดแล้วไปยังอัลกอริทึม OCR หลัก.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**อะไรกำลังเกิดขึ้นเบื้องหลัง?** Aspose OCR จะทำการแปลง deskew ก่อน, จากนั้นรันฟิลเตอร์ denoise, และสุดท้ายปรับคอนทราสต์ก่อนส่งภาพไปยัง recognizer ที่ใช้ neural‑network. ลำดับนี้ตั้งใจไว้; การเปลี่ยนลำดับอาจทำให้ผลลัพธ์ไม่ดีที่สุด.

## ขั้นตอนที่ 6: แสดงข้อความที่จดจำได้

สุดท้าย, เราจะพิมพ์สตริงที่สกัดออกมาที่คอนโซล. ในแอปพลิเคชันจริงคุณอาจเขียนลงไฟล์หรือส่งผ่านเครือข่าย.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หาก `input.jpg` มีข้อความ “Hello World!” คอนโซลควรแสดง:

```
Hello World!
```

หากผลลัพธ์ดูเป็นอักขระผสม, ตรวจสอบค่าการเตรียมภาพอีกครั้ง—โดยเฉพาะ **contrast level** และ **denoise mode**—และลองใช้รูปแบบภาพอื่น.

## โบนัส: แสดงภาพที่เตรียมไว้ล่วงหน้า (ออปชัน)

บางครั้งคุณอาจต้องการดูว่า engine เห็นอย่างไรหลังจาก deskew, denoise, และการเพิ่มคอนทราสต์. Aspose OCR ให้คุณส่งออก bitmap ระหว่างขั้นตอน:

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

เปิด `processed.png` ข้าง ๆ กับภาพต้นฉบับ; คุณจะสังเกตเห็นแนวขอบที่ตรงขึ้นและข้อความที่คมชัดขึ้น. ขั้นตอนนี้เป็นประโยชน์เมื่อคุณกำลังแก้ปัญหาว่าทำไมสแกนบางภาพถึงล้มเหลว.

![preprocess image for OCR example](/images/ocr-preprocess-example.png "preprocess image for OCR – ก่อนและหลังการเพิ่มคอนทราสต์")

*ภาพด้านบนแสดงให้เห็นว่าการเพิ่มคอนทราสต์และการลดสัญญาณรบกวนทำให้สแกนที่เบลอกลายเป็นภาพที่สะอาดและพร้อมสำหรับ OCR.*

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| Pitfall | Why it Happens | Fix |
|---------|----------------|-----|
| **Over‑contrasting** (`setContrastLevel` สูงเกินไป) | พื้นหลังสีอ่อนกลายเป็นสีขาว, ทำให้ตัวอักษรที่จางหายไป | ตั้งระดับไว้ระหว่าง 1.1 และ 1.4 สำหรับข้อความพิมพ์ส่วนใหญ่ |
| **Deskew tolerance too low** | การหมุนเล็กน้อยยังไม่ได้รับการแก้ไข | เพิ่มค่า `setDeskewAngleTolerance` เป็น 0.2 หรือ 0.3 สำหรับหนังสือที่สแกน |
| **Using GAUSSIAN denoise on binary images** | ทำให้ขอบเบลอ, ตัวอักษรรวมกัน | ใช้ `DenoiseMode.MEDIAN` สำหรับสแกนขาว‑ดำ |
| **Missing license** | Engine กลับไปใช้โหมดทดลอง, ทำให้ผลลัพธ์ถูกตัด | ตรวจสอบเส้นทางไปยัง `Aspose.OCR.lic` และไฟล์สามารถอ่านได้ |

## ขั้นตอนต่อไป: ไปไกลกว่าการเตรียมภาพพื้นฐาน

ตอนนี้คุณสามารถ **preprocess image for OCR** และ **extract text using OCR** แล้ว, พิจารณาการขยายต่อไปนี้:

- **Language packs** – โหลดพจนานุกรมภาษาที่เฉพาะเจาะจงเพื่อปรับปรุงความแม่นยำสำหรับข้อความที่ไม่ใช่ภาษาอังกฤษ.
- **Region‑of‑interest (ROI) cropping** – โฟกัสที่ส่วนย่อยของภาพหากคุณต้องการเพียงบางส่วนของหน้า.
- **Batch processing** – วนลูปผ่านไดเรกทอรีของภาพ, ใช้ `OcrEngine` อินสแตนซ์เดียวกันเพื่อความเร็ว.
- **Integrate with PDF** – ผสาน Aspose OCR กับ Aspose PDF เพื่อแปลง PDF ที่สแกนเป็น PDF ที่ค้นหาได้ใน pipeline เดียว.

แต่ละหัวข้อเหล่านี้จะรวมคีย์เวิร์ดรองของเราโดยธรรมชาติ: คุณยังคง **boost image contrast**, **set contrast level**, และยังคง **recognize text from image** ในหลายสถานการณ์.

## สรุป

เราได้ครอบคลุมทุกสิ่งที่คุณต้องการเพื่อ **preprocess image for OCR** ด้วย Aspose OCR for Java: การโหลดลิขสิทธิ์, การตั้งค่า deskew, denoise, และการเพิ่มคอนทราสต์, การส่งภาพ, และสุดท้าย **recognize text from image**. ด้วยตัวอย่างที่สมบูรณ์และสามารถรันได้ข้างต้น, คุณสามารถ **extract text using OCR** บนภาพใด ๆ ที่เตรียมไว้อย่างเหมาะสมได้แล้ว.

ลองรันโค้ด, ปรับ **contrast level**, และดูความแม่นยำเพิ่มขึ้น. เมื่อคุณพร้อม, สำรวจโมเดลเฉพาะภาษา หรือ pipeline แบบ batch เพื่อเปลี่ยนเดโมภาพเดียวนี้ให้เป็นโซลูชันระดับการผลิต.

*ขอให้เขียนโค้ดอย่างสนุกสนาน, และสแกนของคุณมีความคมชัดเสมอ!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}