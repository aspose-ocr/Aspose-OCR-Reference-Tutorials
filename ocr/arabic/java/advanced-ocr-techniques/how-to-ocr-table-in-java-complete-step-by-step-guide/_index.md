---
category: general
date: 2026-07-05
description: كيفية التعرف الضوئي على الجداول باستخدام تقنية تحديد المنطقة في Java
  OCR. تعلم استخراج بيانات الجدول من الصورة والتعرف على منطقة النص مع مثال جاهز للتنفيذ.
draft: false
keywords:
- how to ocr table
- ocr selected area
- extract table data image
- recognize text region
language: ar
og_description: 'كيفية التعرف الضوئي على الجداول في جافا: دليل عملي يوضح كيفية التعرف
  الضوئي على المنطقة المختارة، استخراج صورة بيانات الجدول والتعرف على منطقة النص مع
  الشيفرة المصدرية الكاملة.'
og_title: كيفية إجراء OCR للجدول في جافا – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: how to ocr table using Java OCR selected area technique. Learn to extract
    table data image and recognize text region with a ready‑to‑run example.
  headline: how to ocr table in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: how to ocr table using Java OCR selected area technique. Learn to extract
    table data image and recognize text region with a ready‑to‑run example.
  name: how to ocr table in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles on JDK 11+ as well). - An OCR library
      that provides `OcrEngine`, `Region`, and `RecognitionResult` classes (e.g.,
      Aspose.OCR for Java, Tesseract‑Java wrapper, or any vendor‑specific SDK). -
      A sample image (`rotated_table.png`) placed in a known directory. - Basi'
  - name: 1. Different Image Formats
    text: Most OCR SDKs accept PNG, JPEG, BMP, and TIFF. If you receive a PDF, convert
      the first page to an image first (e.g., using Apache PDFBox). This extra step
      ensures the **ocr selected area** logic works on a raster image.
  - name: 2. Varying Rotation Angles
    text: The automatic deskew works best for rotations up to ±15°. For extreme angles,
      pre‑rotate the image using a library like `java.awt.Graphics2D` before feeding
      it to the OCR engine.
  - name: 3. Large Images and Memory Footprint
    text: If the source image is huge (several megabytes), consider scaling it down
      while preserving DPI. Most SDKs expose a `setResolution(int dpi)` method; 300
      dpi is a good compromise between speed and accuracy.
  - name: 4. Capturing Structured Data
    text: Some OCR engines can return a table model (rows × columns) instead of plain
      text. Look for methods like `recognitionResult.getTable()` or `recognitionResult.getCsv()`.
      When available, you can directly feed the result into a database or spreadsheet.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Table Extraction
title: كيفية التعرف الضوئي على الجداول في جافا – دليل كامل خطوة بخطوة
url: /ar/java/advanced-ocr-techniques/how-to-ocr-table-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على الجداول في Java – دليل خطوة بخطوة كامل

هل تساءلت يومًا **how to ocr table** من مستند ممسوح ضوئيًا دون تحميل الصفحة بأكملها في الذاكرة؟ لست وحدك. في العديد من المشاريع الواقعية—مثل معالجة الفواتير أو ترحيل البيانات من ملفات PDF القديمة—تكون المنطقة الجدولية فقط هي المهمة، والباقي مجرد ضوضاء.

في هذا الدرس سنستعرض مثالًا مختصرًا وقابلًا للتنفيذ يوضح **how to ocr table** من خلال استهداف مستطيل محدد، مما يسمح للمحرك بتصحيح الميل تلقائيًا. في النهاية ستتمكن من **ocr selected area**، **extract table data image**، و**recognize text region** ببضع أسطر من Java فقط.

## ما ستتعلمه

- إعداد نسخة من محرك OCR في Java.
- تعريف **Region** يعزل الجدول المدور.
- السماح لمحرك OCR **recognize text region** مع تصحيح الميل تلقائيًا.
- طباعة نص الجدول المستخرج إلى وحدة التحكم.
- نصائح للتعامل مع صيغ الصور المختلفة، زوايا الدوران، وتحسين الأداء.

### المتطلبات المسبقة

- Java 17 أو أحدث (الكود يتوافق أيضًا مع JDK 11+).
- مكتبة OCR توفر الفئات `OcrEngine`، `Region`، و`RecognitionResult` (مثل Aspose.OCR for Java، أو غلاف Tesseract‑Java، أو أي SDK خاص بالمورد).
- صورة نموذجية (`rotated_table.png`) موجودة في دليل معروف.
- إلمام أساسي بـ Maven/Gradle لإدارة التبعيات.

> **نصيحة احترافية:** إذا كنت تستخدم Maven، أضف تبعية مكتبة OCR إلى ملف `pom.xml`. بالنسبة لـ Gradle، ضعها في `build.gradle`. تختلف الإحداثيات حسب المورد، لكنها عادةً ما تكون مثل `com.aspose:aspose-ocr:23.10`.

---

## الخطوة 1: تهيئة محرك OCR – جوهر **how to ocr table**

إنشاء نسخة من المحرك هو أول ما تقوم به كلما أردت **ocr selected area**. فكر في المحرك كالعقل الذي سيفسر لاحقًا البكسلات داخل المستطيل الذي تحدده.

```java
// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** بدون محرك لا توجد سياق للغة، وضع الكشف، أو خيارات تصحيح الميل. تسمح معظم SDKs بتعديل هذه الإعدادات (مثل `ocrEngine.setLanguage(Language.English)`) قبل استدعاء أي طريقة التعرف.

---

## الخطوة 2: تعريف المنطقة التي تحتوي على الجدول المدور

كائن **Region** يصف إحداثيات `(x, y, width, height)` للمنطقة التي تريد معالجتها. في مثالنا يقع الجدول عند `(120, 350)` ويقيس `800 × 500` بكسل. عدّل هذه القيم لتتناسب مع مستندك.

```java
// Step 2: Define the region (x, y, width, height) that contains the rotated table
Region tableRegion = new Region(120, 350, 800, 500);
```

> **لماذا هذا مهم:** بتحديد **selected area** تقلل بشكل كبير من زمن المعالجة وتزيد الدقة. سيقوم المحرك أيضًا بتصحيح الميل داخل هذا المستطيل تلقائيًا، وهو أمر أساسي عندما يكون الجدول مدورًا.

---

## الخطوة 3: التعرف على النص داخل المنطقة – **recognize text region** عمليًا

الآن نمرر إلى المحرك مسار الصورة والـ `Region` المعرفة مسبقًا. تقوم طريقة `recognizeRegion` بعملين: تقص الصورة إلى المستطيل ثم تنفذ OCR مع تطبيق أي تصحيح دوران ضروري.

```java
// Step 3: Recognize text only within the specified region; the engine will deskew it automatically
RecognitionResult recognitionResult = ocrEngine.recognizeRegion(
        "YOUR_DIRECTORY/rotated_table.png",   // path to your image
        tableRegion);                         // the region we defined above
```

> **لماذا هذا مهم:** هذه الدعوة الواحدة تحل محل سلسلة من الخطوات اليدوية التي تشمل القص، تصحيح الميل، ثم OCR. إنها قلب **how to ocr table** بكفاءة.

---

## الخطوة 4: إخراج نص الجدول المستخرج – تحقق من نتيجة **extract table data image**

أخيرًا، نطبع ناتج OCR. عادةً ما يحتوي كائن `RecognitionResult` على النص الخام، درجات الثقة، وربما تمثيل منظم (مثل سلسلة CSV).

```java
// Step 4: Output the extracted text
System.out.println("Table text:");
System.out.println(recognitionResult.getText());
```

> **الناتج المتوقع (مثال):**  

```
Table text:
Item   Qty   Price
Apple   10   $1.20
Banana   5   $0.80
Total        $16.00
```

إذا كان الجدول لا يزال غير محاذٍ، يمكنك تعديل أبعاد `Region` أو تمكين معالجة بدقة أعلى عبر إعدادات المحرك.

---

## معالجة الحالات الشائعة

### 1. صيغ الصور المختلفة

تقريبًا جميع SDKs تدعم PNG، JPEG، BMP، وTIFF. إذا استلمت ملف PDF، حوّل الصفحة الأولى إلى صورة أولًا (مثلاً باستخدام Apache PDFBox). هذه الخطوة الإضافية تضمن أن منطق **ocr selected area** يعمل على صورة نقطية.

### 2. زوايا الدوران المتفاوتة

يعمل تصحيح الميل التلقائي بأفضل شكل للدوارات حتى ±15°. للزوايا الكبيرة، قم بلف الصورة مسبقًا باستخدام مكتبة مثل `java.awt.Graphics2D` قبل تمريرها إلى محرك OCR.

```java
BufferedImage src = ImageIO.read(new File("rotated_table.png"));
AffineTransform tx = new AffineTransform();
tx.rotate(Math.toRadians(30), src.getWidth() / 2, src.getHeight() / 2);
AffineTransformOp op = new AffineTransformOp(tx, AffineTransformOp.TYPE_BILINEAR);
BufferedImage rotated = op.filter(src, null);
ImageIO.write(rotated, "png", new File("pre_rotated.png"));
```

ثم وجه `recognizeRegion` إلى `pre_rotated.png`.

### 3. الصور الكبيرة واستهلاك الذاكرة

إذا كانت الصورة المصدر ضخمة (عدة ميغابايت)، فكر في تصغيرها مع الحفاظ على DPI. معظم SDKs توفر طريقة `setResolution(int dpi)`؛ 300 dpi يعتبر توازنًا جيدًا بين السرعة والدقة.

### 4. استخراج البيانات المنظمة

بعض محركات OCR يمكنها إرجاع نموذج جدول (صفوف × أعمدة) بدلًا من النص العادي. ابحث عن طرق مثل `recognitionResult.getTable()` أو `recognitionResult.getCsv()`. عندما تكون متاحة، يمكنك إرسال النتيجة مباشرة إلى قاعدة بيانات أو جدول بيانات.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل القابل للتنفيذ بلغة Java الذي يجمع كل الأجزاء معًا. استبدل `YOUR_DIRECTORY` بالمسار الفعلي لصورتك.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.Region;

public class TableOcrDemo {
    public static void main(String[] args) {
        // Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: set language and other settings
        // ocrEngine.setLanguage(Language.English);
        // ocrEngine.setResolution(300);

        // Define the region that contains the rotated table
        Region tableRegion = new Region(120, 350, 800, 500);

        // Perform OCR on the selected area – the engine deskews automatically
        RecognitionResult recognitionResult = ocrEngine.recognizeRegion(
                "YOUR_DIRECTORY/rotated_table.png",
                tableRegion);

        // Print the extracted table text
        System.out.println("Table text:");
        System.out.println(recognitionResult.getText());
    }
}
```

**تشغيل البرنامج** (`javac TableOcrDemo.java && java TableOcrDemo`) يجب أن يطبع محتويات الجدول إلى وحدة التحكم، مؤكدًا أنك نجحت في **extract table data image** من مصدر مدور.

---

## نصائح احترافية وملاحظات

- **المعالجة الدفعية:** ضع المنطق السابق داخل حلقة إذا كان لديك عدة صور. إعادة استخدام نفس نسخة `OcrEngine` يقلل من تكلفة التهيئة.
- **تصفية الثقة:** بعض المحركات توفر `recognitionResult.getConfidence()`. تجاهل الصفوف التي تقل ثقتها عن 80 % وضع علامة عليها للمراجعة اليدوية.
- **تحسين الأداء:** للدفعات الكبيرة، فعّل تعدد الخيوط (`ExecutorService`) لكن تذكر أن معظم محركات OCR تعتمد على CPU وقد لا تتوسع خطيًا.
- **ملاحظة قانونية:** احترم حقوق النشر عند معالجة المستندات الممسوحة؛ تأكد من أن لديك الحق في استخراج البيانات.

---

## الخلاصة

لقد أكملنا الآن دليلًا مختصرًا لكنه شامل حول **how to ocr table** يوضح كيفية **ocr selected area**، **extract table data image**، و**recognize text region** باستخدام محرك OCR في Java. الخطوات الأساسية—إنشاء المحرك، تعريف المنطقة، التعرف القائم على المنطقة، والإخراج—تشكل نمطًا قابلاً لإعادة الاستخدام يمكنك تطبيقه على أي سيناريو استخراج جداول.

هل أنت مستعد للتحدي التالي؟ جرّب تصدير نتيجة OCR إلى CSV، أو تغذيتها إلى نموذج تعلم آلي، أو بناء خدمة مصغرة تستقبل رابط صورة وتُعيد JSON منظم. السماء هي الحد عندما تتقن **how to ocr table** في Java.

برمجة سعيدة، ولا تتردد في طرح أسئلتك أو مشاركة قصص نجاحك في التعليقات أدناه! 

![مثال على كيفية التعرف الضوئي على الجداول](ocr-table-diagram.png "مثال على كيفية التعرف الضوئي على الجداول")


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية التعرف على مستطيلات الصفحة لتعرف النص في Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [التعرف على صورة نصية باستخدام Aspose OCR – دليل OCR كامل بلغة Java](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}