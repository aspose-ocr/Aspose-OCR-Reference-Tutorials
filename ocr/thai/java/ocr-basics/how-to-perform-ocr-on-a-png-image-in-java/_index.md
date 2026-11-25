---
category: general
date: 2026-10-11
description: เรียนรู้วิธีทำ OCR บนภาพ PNG ด้วย Java, ดึงข้อความจากภาพและแปลงภาพเป็นข้อความด้วยตัวอย่าง
  OcrEngine อย่างง่าย.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: th
lastmod: 2026-10-11
og_description: วิธีทำ OCR บนภาพ PNG ด้วย Java, ดึงข้อความจากภาพและแปลงภาพเป็นข้อความโดยใช้ตัวอย่างสั้นกระชับพร้อมใช้งานทันที
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: วิธีทำ OCR บนภาพ PNG ใน Java – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: วิธีทำ OCR บนภาพ PNG ด้วย Java
url: /th/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR บนภาพ PNG ใน Java

หากคุณต้องการ **perform OCR** บนไฟล์ภาพ การเรียนรู้ **how to perform OCR** ใน Java เป็นสิ่งจำเป็นสำหรับงานอัตโนมัติมากมาย ไม่ว่าคุณจะกำลังแปลงใบเสร็จเป็นดิจิทัล ทำดัชนีเอกสารที่สแกน หรือสร้างคลังภาพที่สามารถค้นหาได้ ความสามารถในการ **extract text from image** จากไฟล์ภาพช่วยประหยัดเวลามนุษย์เป็นจำนวนมาก

บทแนะนำนี้จะแสดงวิธีแก้ปัญหาที่สมบูรณ์และสามารถรันได้ ซึ่งโหลดไฟล์ PNG, เรียกใช้ OCR engine, และ **recognize text from PNG** ไฟล์ คุณจะได้เห็นวิธี **convert image to text** และจัดการกับปัญหาทั่วไป เช่น อินพุตความละเอียดต่ำหรืออักขระที่ไม่ใช่ ASCII

## สิ่งที่คุณจะได้ทำ

* โค้ด **load image java** ที่อ่านไฟล์ PNG จากดิสก์,
* เริ่มต้น OCR engine ที่มีน้ำหนักเบา,
* **extract text from image** และพิมพ์ผลลัพธ์ไปยังคอนโซล,
* ปรับโซลูชันสำหรับรูปแบบภาพอื่นหรือการประมวลผลเป็นชุด

ไม่จำเป็นต้องใช้บริการภายนอก—เพียงไลบรารี OCR แบบโอเพนซอร์สเดียว (Tess4J) และ Java SE runtime

## ข้อกำหนดเบื้องต้น

* Java 17 หรือใหม่กว่า (โค้ดคอมไพล์ด้วย JDK 17).
* Maven หรือ Gradle สำหรับการจัดการ dependencies.
* ความคุ้นเคยพื้นฐานกับบรรทัดคำสั่งและ IDE ที่คุณเลือกใช้.
* ไลบรารี `tess4j` (wrapper ของ Java สำหรับ Tesseract) เพิ่ม dependency ของ Maven ด้านล่างนี้:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

หากคุณใช้ Gradle, ตัวเทียบเท่าคือ:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

คุณยังต้องการไฟล์ข้อมูลของ Tesseract (`.traineddata`) ดาวน์โหลดแพ็คข้อมูลภาษาอังกฤษจาก repository อย่างเป็นทางการและวางไว้ในโฟลเดอร์ชื่อ `tessdata` ที่รูทของโปรเจกต์.

## ขั้นตอนที่ 1: โหลดภาพใน Java

การโหลด PNG ทำได้ง่ายด้วยคลาสมาตรฐาน `ImageIO` โค้ดด้านล่างแสดงการ **load image java** อย่างปลอดภัยและคำนึงถึงข้อยกเว้น:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Why this matters:** `ImageIO.read` จะตรวจจับรูปแบบภาพโดยอัตโนมัติ แต่เราตรวจสอบ `null` อย่างชัดเจนเพื่อหลีกเลี่ยงความล้มเหลวเงียบเมื่อ PNG เสียหาย รูปแบบนี้เป็นแนวปฏิบัติที่ดีที่สุดเมื่อคุณ **load image java** สำหรับ OCR.

## ขั้นตอนที่ 2: เริ่มต้น OCR engine

Tess4J หุ้มไบนารี Tesseract ดั้งเดิม ให้ API ของ Java ที่เรียบง่าย วิธีต่อไปนี้สร้างอินสแตนซ์ `Tesseract` ชี้ไปยังโฟลเดอร์ `tessdata` และตั้งค่าภาษาเป็น English:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Why we do this:** การเริ่มต้น engine ครั้งเดียวและใช้ซ้ำสำหรับหลายภาพช่วยลดภาระการเริ่มต้น `setOcrEngineMode` จะเลือกโหมดเริ่มต้น ซึ่งทำงานได้ดีสำหรับ PNG ส่วนใหญ่ หากคุณเจอสแกนที่มีสัญญาณรบกวน คุณสามารถทดลองใช้โหมดอื่น (เช่น `OEM_LSTM_ONLY`).

## ขั้นตอนที่ 3: ทำ OCR และ **recognize text from PNG**

ตอนนี้เราจะรวมตัวโหลดภาพและ OCR engine วิธีต่อไปนี้ทำ OCR บน `BufferedImage` และคืนสตริงที่สกัดออกมา:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**ตัวอย่างที่สามารถรันได้เต็มรูปแบบ**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**ผลลัพธ์ที่คาดหวัง**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

คอนโซลจะแสดงอักขระที่ engine สกัดจาก `sample.png` อย่างแม่นยำ หาก PNG มีเพียงคำเดียว ผลลัพธ์จะเป็นคำนั้นตามด้วยบรรทัดใหม่.

## ขั้นตอนที่ 4: ความหลากหลายและกรณีขอบที่พบบ่อย

### 4.1 การจัดการ PNG ความละเอียดต่ำ

Tesseract ทำงานได้ดีที่สุดกับภาพที่มีความละเอียดอย่างน้อย 300 DPI หาก PNG ต้นฉบับของคุณมีขนาดเล็กกว่า ให้ขยายขนาดก่อนทำ OCR:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

ใช้ `upscale(image, 2)` ก่อนเรียก `extractText` เพื่อเพิ่มความแม่นยำ.

### 4.2 การสกัดข้อความที่ไม่ใช่ภาษาอังกฤษ

เพื่อ **extract text from image** ที่มีภาษาอื่น ดาวน์โหลดไฟล์ `.traineddata` ที่เหมาะสมและตั้งค่ารหัสภาษา:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 การประมวลผลเป็นชุดหลาย PNG

หากคุณต้องการ **recognize text from PNG** ไฟล์ในโฟลเดอร์ ให้วนลูปผ่านไดเรกทอรี:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 การจัดการกับข้อผิดพลาดของ OCR

ข้อผิดพลาด OCR ที่พบบ่อยรวมถึงการอ่าน `0` (ศูนย์) เป็น `O` หรือ `1` เป็น `l` การประมวลผลต่อด้วย regular expressions สามารถทำความสะอาดผลลัพธ์ได้:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

## เคล็ดลับมืออาชีพสำหรับ OCR ที่เชื่อถือได้ใน Java

| Tip | Reason |
|-----|--------|
| **ใช้ PNG แบบ lossless** | ศูนย์ข้อมูลการบีบอัดใน JPEG อาจทำให้ engine สับสน. |
| **ตัดขอบสีขาวออก** | ช่องว่างที่ไม่จำเป็นเพิ่มเวลาในการประมวลผลและอาจทำให้เกิดผลบวกเท็จ. |
| **ตั้งค่า `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** เฉพาะเมื่อเลย์เอาต์ไม่ทราบ; มิฉะนั้นเลือกโหมดเฉพาะ (เช่น `PSM_SINGLE_BLOCK`). |
| **แคชอินสแตนซ์ `ITesseract`** |

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลรวมตัวอย่างโค้ดที่ทำงานได้สมบูรณ์พร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ทางเลือกในโปรเจกต์ของคุณ.

- [วิธีอ่านข้อความจากภาพใน Java ด้วย Aspose OCR – คู่มือเต็ม](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [วิธีใช้ OCR ใน Java – จดจำข้อความจากภาพอย่างรวดเร็ว](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [OCR รูปภาพเป็นชุดใน Java – สกัดข้อความจากไฟล์ PNG อย่างรวดเร็ว](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}