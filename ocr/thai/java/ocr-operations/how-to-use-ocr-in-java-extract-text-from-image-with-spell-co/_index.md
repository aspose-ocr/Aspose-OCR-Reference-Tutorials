---
category: general
date: 2026-05-06
description: วิธีใช้ OCR เพื่อดึงข้อความจากรูปภาพใน Java. เรียนรู้การแปลงรูปภาพเป็นข้อความด้วย
  OCR, การแก้ไขข้อผิดพลาดของ OCR และการโหลดรูปภาพสำหรับ OCR ด้วย Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: th
og_description: วิธีใช้ OCR ใน Java เพื่อดึงข้อความจากภาพ, แก้ไขข้อผิดพลาดของ OCR
  และโหลดภาพสำหรับ OCR ด้วย Aspose OCR.
og_title: วิธีใช้ OCR ใน Java – คู่มือฉบับสมบูรณ์
tags:
- OCR
- Java
- Aspose
title: วิธีใช้ OCR ใน Java – แยกข้อความจากภาพพร้อมการแก้ไขการสะกด
url: /th/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน Java – แยกข้อความจากภาพพร้อมการแก้ไขการสะกด

เคยสงสัย **วิธีใช้ OCR** เพื่อเปลี่ยนรูปใบเสร็จที่เบลอให้เป็นข้อความที่สะอาดและค้นหาได้หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการ—แอปติดตามค่าใช้จ่าย, ระบบแปลงใบแจ้งหนี้เป็นดิจิทัล, หรือแม้แต่สคริปต์บันทึกโน้ตอย่างรวดเร็ว—การได้ข้อความที่เชื่อถือได้จากภาพเป็นอุปสรรคแรก  

บทเรียนนี้จะแสดงให้คุณเห็นอย่างละเอียดว่าใช้ OCR ใน Java อย่างไร ครอบคลุมตั้งแต่การโหลดภาพสำหรับ OCR ไปจนถึงการแก้ไขข้อผิดพลาดของ OCR เพื่อให้ผลลัพธ์อ่านเหมือนพิมพ์โดยมนุษย์ เมื่อเสร็จสิ้นคุณจะสามารถ **extract text from image**, ทำการแปลง **OCR image to text** และแก้ไขข้อผิดพลาดการจดจำที่พบบ่อยโดยอัตโนมัติได้

## สิ่งที่คุณจะสร้าง

เราจะสร้างโปรแกรมคอนโซล Java ขนาดเล็กที่:

1. โหลดไฟล์ PNG (หรือรูปแบบที่รองรับอื่น) เข้าไปใน Aspose OCR engine.  
2. เปิดใช้งานฟีเจอร์การแก้ไขการสะกดในตัวเพื่อ **correct OCR errors**.  
3. รันกระบวนการจดจำและพิมพ์ข้อความที่ทำความสะอาดแล้วออกมา  

ไม่มีบริการภายนอก ไม่มีเฟรมเวิร์กหนัก—แค่ JAR ไฟล์เดียวและไม่กี่บรรทัดของโค้ด

### ข้อกำหนดเบื้องต้น

- Java Development Kit (JDK) 8 หรือใหม่กว่า  
- Maven (หรือเครื่องมือสร้างอื่น) เพื่อดึงไลบรารี Aspose OCR  
- ไฟล์รูปภาพ (เช่น `receipt.png`) ที่คุณต้องการวิเคราะห์  

หากคุณยังไม่มี Aspose OCR JAR ให้เพิ่ม dependency นี้ใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Pro tip:** เวอร์ชันประเมินผลฟรีใช้ได้สำหรับการทดสอบ แต่ไลเซนส์จะลบลายน้ำการประเมินผลออก

## ขั้นตอนที่ 1 – Initialise the OCR Engine (Primary Keyword in Action)

สิ่งแรกที่คุณต้องทำคือสร้างอินสแตนซ์ของ `OcrEngine` คิดว่าเป็นสมองที่จะอ่านพิกเซลและแปลงเป็นอักขระ

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Why this matters:* การเริ่มต้นเอนจินจะตั้งค่าทรัพยากรภายใน (โมเดลภาษา, พจนานุกรม ฯลฯ) การข้ามขั้นตอนนี้จะทำให้เกิด `NullPointerException` ในภายหลังเมื่อคุณพยายามโหลดภาพ

## ขั้นตอนที่ 2 – โหลดภาพสำหรับ OCR

ตอนนี้เราจะ **load image for OCR** จริง ๆ Aspose มี helper `ImageStream.fromFile` ที่สะดวก แต่คุณก็สามารถส่ง `byte[]` ได้หากต้องการ

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Common pitfall:* เส้นทางไฟล์ต้องเป็นแบบ absolute หรือ relative ต่อไดเรกทอรีทำงาน หากไม่พบภาพเอนจินจะโยน `IOException` ตรวจสอบเส้นทางอีกครั้ง โดยเฉพาะเมื่อรันจาก IDE เทียบกับ JAR ที่บรรจุแล้ว

## ขั้นตอนที่ 3 – เปิดใช้งานการแก้ไขการสะกดเพื่อ **Correct OCR Errors**

OCR ที่ใช้โดยตรงอาจมีเสียงรบกวน—เช่น “l0ve” แทน “love” หรือ “0” แทน “O” การเปิดใช้งานการแก้ไขการสะกดบอกเอนจินให้รันขั้นตอน post‑processing ที่แก้ไขข้อผิดพลาดทั่วไป

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Why you’d want this:* หากไม่มีการแก้ไขการสะกด คุณอาจต้องทำความสะอาดผลลัพธ์ด้วยตนเอง ซึ่งทำลายจุดประสงค์ของการอัตโนมัติ พจนานุกรมในตัวทำงานได้ดีสำหรับภาษาอังกฤษและหลายภาษาอื่น

## ขั้นตอนที่ 4 – ทำการจดจำ (**OCR Image to Text**)

เมื่อโหลดภาพและเปิดการแก้ไขการสะกดแล้ว เราสามารถขอให้เอนจินจดจำข้อความได้เลย

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Edge case:* หากภาพมีคอนทราสต์ต่ำหรือเอียงมาก ผลลัพธ์อาจยังคงเป็นตัวอักษรไร้ความหมาย พิจารณาการทำ pre‑processing (เช่น binarisation, deskew) ก่อนส่งให้เอนจิน

## ขั้นตอนที่ 5 – แสดงผลข้อความที่ทำความสะอาดแล้ว

ขั้นตอนสุดท้ายคือการพิมพ์ผลลัพธ์ออกมา ในแอปพลิเคชันจริงคุณอาจบันทึกลงฐานข้อมูลหรือไฟล์ แต่สำหรับการสาธิตนี้ `System.out` เพียงพอ

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `receipt.png` มีรายการสินค้าอย่างชัดเจน คุณอาจเห็นผลลัพธ์ประมาณนี้:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

สังเกตว่า “Qty” และ “Price” ถูกสะกดอย่างถูกต้อง แม้ว่าการสแกนต้นฉบับอาจมี “Qy” ปรากฏอยู่

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในไฟล์ชื่อ `SpellCorrectDemo.java` ตรวจสอบให้แน่ใจว่า Aspose OCR JAR อยู่ใน classpath

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Run it with:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

คุณควรเห็นข้อความที่ทำความสะอาดแล้วพิมพ์ออกมาที่คอนโซล

## โบนัส: ปรับแต่งการตั้งค่าเพื่อความแม่นยำที่ดียิ่งขึ้น

แม้การตั้งค่าเริ่มต้นจะทำงานได้กับเอกสารพิมพ์ส่วนใหญ่ คุณอาจต้องปรับพารามิเตอร์บางอย่างสำหรับสถานการณ์พิเศษ:

| การตั้งค่า | ทำอะไร | เมื่อควรเปลี่ยน |
|-----------|--------|-----------------|
| `setLanguage(OcrLanguage.English)` | บังคับใช้พจนานุกรมภาษาอังกฤษ (ลดผลบวกเท็จ) | หากภาพของคุณมีเฉพาะข้อความภาษาอังกฤษ |
| `setResolution(300)` | แจ้งให้เอนจินทราบ DPI ของภาพต้นฉบับ | สำหรับสแกนความละเอียดสูง |
| `setEnableAutoSkewCorrection(true)` | หมุนอัตโนมัติหน้าที่เอียงเล็กน้อย | เมื่อภาพถูกถ่ายด้วยโทรศัพท์ |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## คำถามที่พบบ่อย

**Q: Does this work with PDFs?**  
A: ใช่. แปลงแต่ละหน้า PDF เป็นภาพ (เช่น ใช้ Aspose PDF) แล้วส่งภาพให้ OCR engine

**Q: What if my image is in BMP format?**  
A: `ImageStream.fromFile` รองรับ PNG, JPEG, BMP, TIFF, และ GIF โดยตรง เพียงเปลี่ยนส่วนต่อท้ายไฟล์

**Q: Can I disable spell correction?**  
A: แน่นอน—ตั้งค่า `setEnableSpellCorrection(false)` หากคุณต้องการผลลัพธ์ OCR ดิบสำหรับการประมวลผลต่อไป

## สรุป

คุณตอนนี้รู้ **วิธีใช้ OCR** ใน Java เพื่อ **extract text from image**, แก้ไข **OCR errors** อัตโนมัติ และ **load image for OCR** อย่างถูกต้องด้วย Aspose OCR กระบวนการห้าขั้นตอน—initialise, load, enable spell correction, recognise, และ output—ครอบคลุมงาน OCR ประจำวันส่วนใหญ่  

จากนี้ลองต่อเชื่อมตรรกะนี้กับการเขียนกลับไปยังฐานข้อมูล, endpoint REST, หรือ batch processor เพื่อจัดการใบเสร็จหลายสิบใบพร้อมกัน ทดลองปรับค่าตารางด้านบนเพื่อดึงความแม่นยำสูงสุดออกมา

ขอให้สนุกกับการเขียนโค้ด และขอให้ผลลัพธ์ OCR ของคุณสะอาดกว่ารอยกาแฟบนใบเสร็จเสมอ!

![แผนภาพวิธีใช้ OCR แสดงภาพ → OCR engine → ข้อความที่แก้ไขแล้ว]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}