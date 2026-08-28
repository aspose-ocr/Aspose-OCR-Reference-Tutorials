---
category: general
date: 2026-01-07
description: إنشاء ملف PDF قابل للبحث من صورة في جافا. تعلم كيفية تحويل الصورة إلى
  PDF، استخراج النص من الصورة، والتعرف على النص من PNG باستخدام Aspose OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- image to searchable pdf
- recognize text from png
language: ar
og_description: إنشاء ملف PDF قابل للبحث في Java باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية تحويل الصورة إلى PDF، واستخراج النص من الصورة، والتعرف على النص من ملف PNG.
og_title: إنشاء ملف PDF قابل للبحث من PNG – دليل جافا
tags:
- OCR
- Java
- PDF
title: إنشاء ملف PDF قابل للبحث من PNG – دليل Java الكامل
url: /ar/java/ocr-operations/create-searchable-pdf-from-png-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF قابل للبحث من PNG – دليل Java الكامل

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من صورة ممسوحة ضوئياً لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—المطورون يواجهون هذه المشكلة باستمرار عند بناء خطوط معالجة المستندات. الخبر السار؟ ببضع أسطر من Java و Aspose OCR يمكنك **تحويل الصورة إلى PDF**، وإدراج نص مخفي، والحصول على مستند قابل للبحث تمامًا.

في هذا الدرس سنستعرض العملية بالكامل: تحميل ملف PNG، تشغيل OCR، وحفظ النتيجة كملف PDF قابل للبحث. بنهاية الدرس ستتمكن من **استخراج النص من الصورة**، وتحويلها إلى أصول **صورة إلى PDF قابل للبحث**، وحتى التعامل مع الحالات الخاصة مثل ملفات TIFF متعددة الصفحات. لا خدمات خارجية، فقط كود Java نقي يمكنك تشغيله اليوم.

## إنشاء PDF قابل للبحث – نظرة عامة

قبل أن نغوص في الكود، دعونا نوضح ما يعنيه “PDF قابل للبحث”. يحتوي PDF القابل للبحث على طبقتين:

1. **طبقة الصورة المرئية** – الصورة الأصلية (PNG، JPEG، إلخ).
2. **طبقة النص المخفي** – نص تم توليده بواسطة OCR ويقع خلف الصورة، مما يجعل المستند قابلًا للبحث في أي عارض PDF.

لماذا نحتاج كلاهما؟ الصورة تحافظ على المظهر الأصلي، بينما طبقة النص تمكّن من النسخ‑اللصق، الفهرسة، والبحث النصي الكامل. هذا هو الحل المثالي للأرشفة، الامتثال القانوني، وبناء أرشيفات قابلة للبحث.

## الخطوة 1: إعداد Aspose OCR في مشروع Java الخاص بك

أولاً وقبل كل شيء—تحتاج إلى مكتبة Aspose OCR. أبسط طريقة هي إضافة تبعية Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

إذا لم تكن تستخدم Maven، فقط قم بتحميل ملف JAR من موقع Aspose وأضفه إلى classpath. **نصيحة احترافية:** حافظ على توافق نسخة المكتبة مع نسخة Java التي تستخدمها (Java 8+ تعمل بشكل جيد).

### لماذا هذا مهم

Aspose OCR يدعم مجموعة واسعة من صيغ الصور واللغات مباشرةً، لذا لا تحتاج إلى كتابة كود معالجة البكسل الخاص بك. كما يوفر لك تعداد `OcrOutputFormat.PDF` الذي سنستخدمه لاحقًا لإنشاء PDF قابل للبحث.

## الخطوة 2: تحميل الصورة التي تريد معالجتها

بعد ذلك، نحتاج إلى إخبار محرك OCR بأي ملف يقرأ. API يقبل `ImageStream`، والذي يمكن إنشاؤه من مسار ملف، أو `java.io.InputStream`، أو حتى مصفوفة بايت.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG (or any supported image) from disk
        String inputPath = "YOUR_DIRECTORY/input.png"; // replace with your actual path
        ocrEngine.setImage(ImageStream.fromFile(inputPath));
```

لاحظ أننا نستخدم `ImageStream.fromFile`. إذا احتجت يومًا إلى **تحويل الصورة إلى PDF** من تدفق (مثلاً ملف تم رفعه)، يمكنك استبدال هذا الاستدعاء بـ `ImageStream.fromInputStream(yourInputStream)`.

### تنبيه حالة حافة

إذا كانت صورتك أكبر من 10 ميغابايت، فكر في تصغيرها أولاً. الصور الكبيرة تزيد من زمن OCR بشكل كبير وقد تتسبب في أخطاء نفاد الذاكرة على الخوادم ذات الموارد المحدودة.

## الخطوة 3: تشغيل OCR والتقاط النتيجة

الآن يحدث السحر. استدعاء `recognize()` يشغّل خوارزمية OCR ويعيد كائن `OcrResult` الذي يحتوي على النص المستخرج ومعلومات التخطيط.

```java
        // Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: print extracted text to console (useful for debugging)
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());
```

هنا نقوم أيضًا **باستخراج النص من الصورة** وطباعة النتيجة. هذه الخطوة مفيدة عندما تحتاج فقط إلى النص الخام دون إنشاء PDF. يتم لاحقًا إعادة استخدام كائن `ocrResult` نفسه لإنشاء PDF القابل للبحث.

### لماذا هذه الخطوة حاسمة

محرك OCR لا يقرأ الأحرف فقط، بل يحافظ أيضًا على مواقعها، وهذا ما يتيح طبقة النص المخفي في PDF النهائي. تخطي هذه الخطوة يعني فقدان القدرة على البحث.

## الخطوة 4: حفظ النتيجة كملف PDF قابل للبحث

أخيرًا، نخبر Aspose OCR بكتابة الناتج بصيغة PDF. طريقة `save` تأخذ اسم الملف الهدف وتعداد `OcrOutputFormat`.

```java
        // Save the OCR result as a searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // replace with your desired output
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

عند فتح `output.pdf` في Adobe Reader أو أي عارض PDF حديث، سترى PNG الأصلي، لكن يمكنك أيضًا البحث عن أي كلمة ظهرت في الصورة. هذا هو جوهر **إنشاء PDF قابل للبحث**.

### تنويعات قد تحتاجها
- **Multiple pages:** إذا كان لديك ملف TIFF متعدد الصفحات، ببساطة قم بالتكرار على كل صفحة، استدعِ `ocrEngine.setImage` لكل منها، وأضف النتائج إلى نفس `OcrResult` قبل الحفظ.
- **Different languages:** استخدم `ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);` (أو أي لغة مدعومة) قبل استدعاء `recognize()`.
- **Custom DPI:** للماسحات الضبابية، يمكنك تحسين الدقة بتعيين `ocrEngine.getImage().setResolution(300);`.

## الخطوة 5: التحقق من النتيجة (ما المتوقع)

بعد تشغيل البرنامج، تحقق من ملف `output.pdf`:

1. **الطبقة البصرية:** يعرض PDF PNG بالضبط الذي قدمته.
2. **طبقة النص:** اضغط `Ctrl+F` (أو Cmd+F) وابحث عن كلمة تعرف أنها موجودة في الصورة. يجب أن يتم العثور عليها فورًا.
3. **نسخ‑لصق:** حاول تحديد فقرة ونسخها إلى محرر نصوص؛ ستحصل على نص نظيف وقابل للبحث.

إذا فشل البحث، تحقق مرة أخرى من أن الصورة ليست منخفضة الدقة أو أن اللغة الصحيحة تم ضبطها. غالبًا ما يحل رفع DPI بسيط المشكلة.

## أسئلة شائعة ونصائح احترافية

- **هل أحتاج إلى ترخيص؟**  
  Aspose OCR يعمل في وضع التجربة مع علامة مائية. للإنتاج، اشترِ ترخيصًا واضبطه عبر `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

- **هل يمكنني **تحويل الصورة إلى PDF** بدون OCR؟**  
  نعم—استخدم `OcrOutputFormat.PDF` مع `ocrEngine.setRecognizeText(false);` قبل `recognize()`. سيعطيك ذلك PDF يحتوي على الصورة فقط.

- **ماذا لو أردت فقط النص المستخرج؟**  
  تخطّ استدعاء `save` واستخدم `ocrResult.getText()`؛ يمكنك كتابة النتيجة إلى ملف `.txt` أو إمداده إلى فهرس بحث.

- **نصيحة أداء:**  
  أعد استخدام نفس كائن `OcrEngine` لعدة صور؛ فهذا يقلل من عبء التهيئة.

## مثال كامل يعمل (الكل معًا)

فيما يلي البرنامج الكامل الجاهز للتنفيذ بلغة Java. استبدل مسارات العناصر النائبة بمساراتك الخاصة، أضف تبعية Maven، وستكون جاهزًا للبدء.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the image (PNG, JPG, TIFF, etc.)
        String inputPath = "YOUR_DIRECTORY/input.png"; // <-- change this
        ocrEngine.setImage(ImageStream.fromFile(inputPath));

        // 3️⃣ Run OCR to get text and layout
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: display extracted text in console
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());

        // 4️⃣ Save as searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // <-- change this
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

**الناتج المتوقع:**  
```
Extracted Text:
[...the plain text that was recognized from the PNG...]
Searchable PDF created at: YOUR_DIRECTORY/output.pdf
```

افتح `output.pdf` في أي عارض PDF وجرب البحث عن كلمة من النص المستخرج—يجب أن تظهر مميزة، مما يؤكد أنك نجحت في **إنشاء PDF قابل للبحث**.

## الخلاصة

لقد أظهرنا لك الآن كيفية **إنشاء PDF قابل للبحث** من PNG باستخدام Java و Aspose OCR. الخطوات بسيطة: إعداد المكتبة، تحميل الصورة، تشغيل OCR، وحفظ النتيجة كملف PDF. خلال العملية تعلمت أيضًا كيفية **تحويل الصورة إلى PDF**، **استخراج النص من الصورة**، وحتى **التعرف على النص من PNG** لمواقف أكثر تقدماً.

ما الخطوة التالية؟ جرّب معالجة دفعة من الفواتير الممسوحة في حلقة، خزن النص المخفي في قاعدة بيانات للبحث النصي الكامل، أو جرب لغات مختلفة وتقنيات ما قبل معالجة الصور. نفس النمط يعمل مع صيغ أخرى—فقط استبدل ملف الإدخال وستتمكن من **تحويل الصورة إلى PDF قابل للبحث** في لحظات.

هل لديك أسئلة أو تواجه مشاكل؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}