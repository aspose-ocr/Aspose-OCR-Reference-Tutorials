---
category: general
date: 2026-07-05
description: ضغط صور PDF أثناء تحويل PNG إلى PDF باستخدام Java. تعلم تمهيد الصور للتعرف
  الضوئي على الأحرف، التعرف على النص في JPG، وإجراء التعرف الضوئي على الأحرف على دفعات
  إلى PDF في دليل واحد.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: ar
og_description: ضغط صور PDF وتحويل PNG إلى PDF باستخدام Java. يغطي هذا الدليل معالجة
  الصور مسبقًا للتعرف الضوئي على الأحرف (OCR)، التعرف على النص في JPG، ومعالجة OCR
  دفعة إلى PDF.
og_title: ضغط صور PDF باستخدام Java – دليل OCR دفعي كامل
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
title: ضغط صور PDF باستخدام Java – دليل شامل لتحويل OCR دفعةً إلى PDF
url: /ar/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ضغط صور PDF باستخدام Java – دليل كامل لتحويل دفعات OCR إلى PDF

هل احتجت يومًا إلى **ضغط صور PDF** أثناء تحويل مجلد من ملفات PNG إلى ملفات PDF قابلة للبحث؟ لست وحدك. في العديد من خطوط الأتمتة، النقطة الأكثر إزعاجًا هي موازنة جودة الصورة، دقة OCR، وحجم PDF النهائي—كل ذلك في آن واحد.  

في هذا الدرس سنستعرض حلًا عمليًا يقوم **بتحويل PNG إلى PDF**، يطبق **معالجة مسبقة للصور من أجل OCR**، وأخيرًا **يضغط صور PDF** بحيث يبقى الناتج خفيفًا. بنهاية الدرس ستعرف كيف **تتعرف على نصوص JPG**، تُعدّ سير عمل **دفعة OCR إلى PDF**، وتحافظ على تنظيم ملفات PDF الخاصة بك.

## ما ستتعلمه

- إعداد Aspose OCR for Java وتطبيق الترخيص.
- تكوين المحرك للمعالجة المتعددة الخيوط، تسريع GPU، وتصحيح الأخطاء الإملائية.
- بناء خط أنابيب **معالجة مسبقة للصور من أجل OCR** قابل لإعادة الاستخدام (إزالة الضوضاء، تحسين التباين، التحويل إلى ثنائي).
- استخدام **PdfSaveOptions** لـ **ضغط صور PDF** دون التضحية بقراءة المحتوى.
- التجول عبر دليل لتحويل **PNG إلى PDF** و**التعرف على نص JPG** بالجملة.
- برنامج Java كامل جاهز للتنفيذ يمكنك إضافته إلى أي مشروع.

> **المتطلبات المسبقة**: Java 8+، Maven أو Gradle، ترخيص Aspose OCR for Java، ومجلد يحتوي على صور PNG/JPG تريد معالجتها.

---

## الخطوة 1: تطبيق ترخيص Aspose OCR (ضروري للإنتاج)

قبل أن تتمكن من استدعاء أي واجهة برمجة تطبيقات OCR، يجب تحميل ترخيص صالح؛ وإلا ستظل مقيدًا بحدود النسخة التجريبية.

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

*لماذا هذا مهم*: المحرك المرخص يفتح دعم GPU، دقة أعلى، ويزيل العلامات المائية التي قد تجعل ملفات PDF أكبر حجمًا.

---

## الخطوة 2: تكوين محرك OCR – الخيوط، GPU، وتصحيح الأخطاء الإملائية

محرك OCR السريع هو العمود الفقري لأي مهمة **دفعة OCR إلى PDF**. سننشئ عددًا من الخيوط يساوي قدرة وحدة المعالجة المركزية، نفعّل تسريع GPU (إذا كان لديك بطاقة متوافقة)، ونضبط تصحيح الأخطاء الإملائية لتنظيف أخطاء OCR.

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

*نصيحة احترافية*: إذا كنت تعمل على خادم بدون واجهة رسومية ولا يمتلك GPU، ما عليك سوى ضبط `gpu.setEnabled(false)` – سيظل الكود يعمل، لكنه سيكون أبطأ قليلًا.

---

## الخطوة 3: بناء خط أنابيب معالجة مسبقة للصور

المسحات الخام غالبًا ما تعاني من الضوضاء، انخفاض التباين، أو إضاءة غير متساوية. **معالجة مسبقة للصور من أجل OCR** تحسّن معدلات التعرف بشكل كبير، خاصة في سيناريوهات **التعرف على نص JPG**.

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

*لماذا نسلسل هذه الخطوات*: إزالة الضوضاء أولًا يمنع المُحوّل الثنائي من تضخيم البقع؛ ثم يضمن التباين بروز الأحرف؛ وأخيرًا، يعطي التحويل إلى ثنائي صورة نظيفة للمحرك OCR للعمل عليها.

---

## الخطوة 4: إعداد خيارات حفظ PDF – **ضغط صور PDF** بفعالية

تتيح لك Aspose ضبط مخرجات PDF بدقة. سنفعل ضغط الصور ونحدد مستوى جودة يوازن بين الحجم والوضوح.

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

*النتيجة*: كل ملف PDF قابل للبحث سيكون أصغر حجمًا بشكل ملحوظ—مثالي للأرشفة أو الإرسال عبر البريد الإلكتروني.

---

## الخطوة 5: معالجة المجلد – **تحويل PNG إلى PDF** و**التعرف على نص JPG** في حلقة واحدة

الآن نجمع كل شيء معًا. الحلقة تتجول في دليل الإدخال، تُجري OCR على كل ملف PNG أو JPG، وتكتب PDF قابل للبحث في دليل الإخراج. اسم ملف PDF يطابق اسم الصورة الأصلية.

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

### النتيجة المتوقعة

تشغيل البرنامج يطبع سطرًا لكل صورة، مثلًا:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

افتح أي PDF ناتج في عارض وسترى نصًا قابلًا للتحديد والبحث بينما يكون حجم الملف عادةً **أصغر بنسبة 30‑50 %** مقارنةً بنسخة غير مضغوطة.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كان الخادم لا يمتلك GPU؟

ما عليك سوى ضبط `gpuSettings.setEnabled(false)`. يبقى باقي خط الأنابيب دون تغيير، وستستمر المعالجة المتعددة الخيوط على وحدة المعالجة المركزية.

### ملفات PDF لا تزال كبيرة—هل يمكن خفض الجودة أكثر؟

نعم. عدّل `options.setImageQuality(70)` أو حتى `50`. القيم الأقل تقلل الحجم بشكل أكبر لكن قد تُطمس بعض الحروف الدقيقة. اختبر على عينة تمثيلية.

### كيف أتعامل مع صيغ صور أخرى (TIFF, BMP)؟

أضف الامتدادات إلى دالة الفلترة lambda:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

خط الأنابيب نفسه يعمل مع معظم صيغ الصور النقطية.

### هل يمكن الاحتفاظ بالصور الملونة الأصلية بدلاً من التحويل إلى ثنائي؟

استبدل `.addBinarize()` بـ `.addGrayscale()` في مُنشئ المعالج إذا كنت تحتاج إلى الحفاظ على الألوان للتحليل اللاحق.

## نصائح احترافية لتشغيل دفعة OCR جاهزة للإنتاج

- **إدارة الذاكرة**: أعد استخدام نسخة واحدة من كائن `OcrEngine` (كما هو موضح) لتجنب تكلفة إنشاء/تدمير الكائنات لكل صورة.
- **معالجة الأخطاء**: غلف كتلة كل ملف بـ `try/catch` لتسجيل الفشل دون إيقاف الدفعة بالكامل.
- **التسجيل (Logging)**: استخدم إطار تسجيل مناسب (SLF4J، Log4j) بدلًا من `System.out.println` لحلول قابلة للتوسع.
- **التوازي**: للمجلدات الضخمة، فكر في معالجة الأدلة الفرعية عبر تدفقات متوازية، لكن راقب تنافسية الـ GPU.
- **الأمان**: احفظ ملف الترخيص خارج المستودع واحمِه بأذونات نظام الملفات.

## الخلاصة

لقد أوضحنا للتو كيفية **ضغط صور PDF** أثناء إجراء تحويل **دفعة OCR إلى PDF** يشمل **تحويل PNG إلى PDF**، **التعرف على نص JPG**، وتطبيق خط أنابيب **معالجة مسبقة للصور من أجل OCR** قوي. البرنامج الكامل بلغة Java مستقل، يعمل على أي JDK حديث، وينتج ملفات PDF قابلة للبحث وخفيفة الوزن جاهزة للأرشفة أو التحليل اللاحق.

ما الخطوات التالية؟ جرّب معلمات معالجة مسبقة مختلفة، اختبر لغات OCR غير الإنجليزية، أو دمج سير العمل في خدمة مصغرة Spring Boot تراقب دليلًا وتُعالج الملفات فورًا. المفاهيم الأساسية—تحميل الترخيص، تكوين المحرك، المعالجة المسبقة، وضغط PDF—تبقى ثابتة، مما يمنحك أساسًا قويًا لأي مشروع يعتمد على OCR.

هل لديك أسئلة أو تريد مشاركة تعديلاتك؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبنى على التقنيات التي تم استعراضها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [التعرف على نص PDF – عمليات OCR مع Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [التعرف على نص الصورة باستخدام Aspose OCR – دليل OCR كامل بلغة Java](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [تحويل الصورة إلى نص في Java باستخدام Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}