---
category: general
date: 2026-07-05
description: บีบอัดภาพ PDF ระหว่างแปลง PNG เป็น PDF ด้วย Java เรียนรู้การเตรียมภาพสำหรับ
  OCR จดจำข้อความจาก JPG และทำ OCR เป็นชุดเป็น PDF ในบทเรียนเดียว
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: th
og_description: บีบอัดภาพ PDF และแปลง PNG เป็น PDF ด้วย Java คู่มือนี้ครอบคลุมการเตรียมภาพสำหรับ
  OCR, การจดจำข้อความจาก JPG, และการทำ OCR เป็นชุดเป็น PDF.
og_title: บีบอัดรูปภาพ PDF ด้วย Java – การสอน OCR แบบแบตช์ครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: บีบอัดภาพ PDF ด้วย Java – คู่มือ OCR แบบเต็มชุดเป็น PDF
url: /th/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# บีบอัดรูปภาพ PDF ด้วย Java – คู่มือ Full Batch OCR to PDF

เคยต้อง **บีบอัดรูปภาพ PDF** พร้อมแปลงโฟลเดอร์ของ PNG ให้เป็น PDF ที่ค้นหาได้หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลาย ๆ pipeline ของการทำอัตโนมัติ จุดเจ็บปวดที่ใหญ่ที่สุดคือการจัดการคุณภาพของรูปภาพ, ความแม่นยำของ OCR, และขนาดสุดท้ายของ PDF – ทั้งหมดนี้พร้อมกัน  

ในบทเรียนนี้เราจะพาไปผ่านโซลูชันที่ใช้งานได้จริงซึ่ง **แปลง PNG เป็น PDF**, ทำ **image preprocessing for OCR**, และสุดท้าย **บีบอัดรูปภาพ PDF** เพื่อให้ผลลัพธ์มีน้ำหนักเบา เมื่อจบคุณจะรู้วิธี **recognize text JPG** ไฟล์, ตั้งค่า workflow **batch OCR to PDF**, และทำให้ PDF ของคุณเป็นระเบียบ

## สิ่งที่คุณจะได้เรียน

- ตั้งค่า Aspose OCR for Java และใส่ไลเซนส์
- กำหนดค่า engine สำหรับ multithreading, การเร่งด้วย GPU, และการแก้ไขการสะกดคำ
- สร้าง pipeline **image preprocessing for OCR** ที่นำกลับมาใช้ได้ (denoise, contrast, binarize)
- ใช้ **PdfSaveOptions** เพื่อ **บีบอัดรูปภาพ PDF** โดยไม่เสียความอ่านได้
- วนลูปผ่านไดเรกทอรีเพื่อ **แปลง PNG เป็น PDF** และ **recognize text JPG** แบบกลุ่ม
- โปรแกรม Java เต็มรูปแบบที่พร้อมรันและสามารถนำไปใส่ในโปรเจกต์ใดก็ได้

> **Prerequisites**: Java 8+, Maven หรือ Gradle, ไลเซนส์ Aspose OCR for Java, และโฟลเดอร์ของรูปภาพ PNG/JPG ที่คุณต้องการประมวลผล

---

## Step 1: Apply the Aspose OCR License (Essential for Production)

ก่อนที่คุณจะเรียกใช้ OCR API ใด ๆ คุณต้องโหลดไลเซนส์ที่ถูกต้อง; มิฉะนั้นคุณจะติดอยู่กับข้อจำกัดของรุ่นทดลอง

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*ทำไมจึงสำคัญ*: Engine ที่มีไลเซนส์จะเปิดใช้งาน GPU, ความแม่นยำที่สูงขึ้น, และลบ watermark ที่จะทำให้ไฟล์ PDF ของคุณบวมขึ้น

---

## Step 2: Configure the OCR Engine – Threads, GPU, and Spell Correction

OCR engine ที่เร็วเป็นหัวใจของงาน **batch OCR to PDF** ใด ๆ เราจะสปินจำนวนเธรดให้เท่ากับจำนวนคอร์ของ CPU, เปิดการเร่งด้วย GPU (ถ้ามีการ์ดที่รองรับ), และปรับการแก้ไขการสะกดให้คมชัดเพื่อลดข้อผิดพลาดของ OCR

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Pro tip*: หากคุณรันบนเซิร์ฟเวอร์ headless ที่ไม่มี GPU เพียงตั้งค่า `gpu.setEnabled(false)` – โค้ดจะยังทำงานได้ แต่ช้าลงเล็กน้อย

---

## Step 3: Build an Image Preprocessing Pipeline

สแกนดิบมักมี noise, คอนทราสต์ต่ำ, หรือแสงไม่สม่ำเสมอ **Image preprocessing for OCR** จะช่วยเพิ่มอัตราการจดจำอย่างมาก โดยเฉพาะในสถานการณ์ **recognize text JPG**

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*ทำไมเราถึงต่อกัน*: การลด noise ก่อนจะป้องกันไม่ให้ binarizer ขยาย speckles; คอนทราสต์ต่อมาจะทำให้ตัวอักษรโดดเด่น; สุดท้ายการ binarization จะให้ OCR engine ได้ภาพไบนารีที่สะอาด

---

## Step 4: Prepare PDF Save Options – **Compress PDF Images** Efficiently

Aspose ให้คุณปรับแต่งผลลัพธ์ PDF เราจะเปิดการบีบอัดรูปภาพและตั้งค่าคุณภาพที่สมดุลระหว่างขนาดและความอ่านได้

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*ผลลัพธ์*: PDF ที่ค้นหาได้แต่ละไฟล์จะเล็กลงอย่างเห็นได้ชัด – เหมาะสำหรับการเก็บถาวรหรือส่งอีเมล

---

## Step 5: Process the Folder – **Convert PNG to PDF** and **Recognize Text JPG** in One Loop

ตอนนี้เราจะรวมทุกอย่างเข้าด้วยกัน ลูปจะเดินทางผ่านไดเรกทอรีอินพุต, รัน OCR บนแต่ละ PNG หรือ JPG, และเขียน PDF ที่ค้นหาได้ลงในโฟลเดอร์เอาต์พุต ชื่อ PDF จะตรงกับชื่อไฟล์รูปต้นฉบับ

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Expected Output

เมื่อรันโปรแกรมจะแสดงบรรทัดสำหรับแต่ละรูปภาพ เช่น:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

เปิด PDF ใด ๆ ที่ได้ใน viewer คุณจะเห็นข้อความที่เลือกได้และค้นหาได้ ขณะเดียวกันขนาดไฟล์จะเล็กลง **30‑50 %** เมื่อเทียบกับไฟล์ที่ไม่ได้บีบอัด

---

## Common Questions & Edge Cases

### What if my server has no GPU?
เพียงตั้งค่า `gpuSettings.setEnabled(false)` ส่วนที่เหลือของ pipeline จะยังคงทำงานตามเดิม และคุณยังคงได้การประมวลผลแบบ multithreaded บน CPU

### My PDFs are still too large—can I lower the quality further?
ได้เลย ปรับ `options.setImageQuality(70)` หรือแม้แต่ `50` ค่าใต้มักทำให้ขนาดลดลงมากขึ้นแต่อาจทำให้ glyph บางตัวเบลอ ทดสอบกับตัวอย่างที่เป็นตัวแทนก่อน

### How do I handle other image formats (TIFF, BMP)?
เพิ่มส่วนขยายลงใน lambda filter:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

Pipeline การ preprocessing เดียวกันทำงานได้กับรูปแบบ raster ส่วนใหญ่

### Can I keep the original color images instead of binarizing?
เปลี่ยน `.addBinarize()` เป็น `.addGrayscale()` ใน builder ของ preprocessor หากคุณต้องการรักษาสีสำหรับการวิเคราะห์ต่อไป

---

## Pro Tips for Production‑Ready Batch OCR

- **Memory management**: ใช้ `OcrEngine` ตัวเดียว (ตามที่แสดง) เพื่อหลีกเลี่ยงค่าใช้จ่ายจากการสร้าง/ทำลายอ็อบเจ็กต์ต่อภาพ
- **Error handling**: ห่อบล็อก per‑file ด้วย `try/catch` เพื่อบันทึกข้อผิดพลาดโดยไม่หยุดการทำงานของ batch ทั้งหมด
- **Logging**: ใช้เฟรมเวิร์ก logging ที่เหมาะสม (SLF4J, Log4j) แทน `System.out.println` สำหรับโซลูชันที่ขยายได้
- **Parallelism**: สำหรับโฟลเดอร์ขนาดใหญ่ พิจารณาประมวลผล sub‑directories ด้วย parallel streams แต่ต้องระวังการแย่ง GPU
- **Security**: เก็บไฟล์ไลเซนส์นอก repository และปกป้องด้วย permission ของระบบไฟล์

---

## Conclusion

เราได้สาธิตวิธี **บีบอัดรูปภาพ PDF** พร้อมทำ **batch OCR to PDF** ที่ **แปลง PNG เป็น PDF**, **recognize text JPG**, และใช้ pipeline **image preprocessing for OCR** ที่แข็งแรง โปรแกรม Java เต็มรูปแบบเป็นอิสระ, ทำงานบน JDK สมัยใหม่ใดก็ได้, และสร้าง PDF ที่ค้นหาได้และน้ำหนักเบาพร้อมสำหรับการเก็บถาวรหรือการวิเคราะห์ต่อไป

ขั้นตอนต่อไป? ทดลองปรับพารามิเตอร์ preprocessing ต่าง ๆ, ลองใช้ภาษา OCR นอกเหนือจากอังกฤษ, หรือผสาน workflow นี้เข้าไปใน Spring Boot microservice ที่คอยเฝ้าดูโฟลเดอร์และประมวลผลไฟล์แบบเรียลไทม์ แนวคิดหลัก – โหลดไลเซนส์, ตั้งค่า engine, preprocessing, และบีบอัด PDF – ยังคงเหมือนเดิม ให้คุณมีพื้นฐานที่มั่นคงสำหรับโครงการที่ขับเคลื่อนด้วย OCR ใด ๆ

มีคำถามหรืออยากแชร์การปรับแต่งของคุณ? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")


## What Should You Learn Next?


บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}