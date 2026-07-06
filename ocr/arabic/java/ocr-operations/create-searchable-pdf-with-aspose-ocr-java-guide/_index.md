---
category: general
date: 2026-03-26
description: إنشاء ملف PDF قابل للبحث باستخدام Aspose.OCR Java – تعلم كيفية تحميل
  صورة OCR، تعيين اللغة الأساسية، استخراج النص من الصورة وحفظ ملف PDF مع OCR.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث باستخدام Aspose.OCR Java. دليل خطوة بخطوة
  لتحميل صورة OCR، تعيين اللغة الأساسية، استخراج النص من الصورة، وحفظ ملف PDF OCR.
og_title: إنشاء PDF قابل للبحث باستخدام Aspose.OCR – دليل Java
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: إنشاء PDF قابل للبحث باستخدام Aspose.OCR – دليل Java
url: /ar/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث باستخدام Aspose.OCR – دليل Java

هل احتجت يومًا إلى **إنشاء PDF قابل للبحث** من مستند ممسوح ضوئيًا لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يتعاملون مع OCR في Java لأول مرة. الخبر السار هو أن Aspose.OCR يجعل سير العمل بالكامل—من تحميل الصورة إلى تعيين اللغة الأساسية وأخيرًا حفظ PDF مدعوم بـ OCR—سهلًا جدًا. في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ ي **يستخرج النص من الصورة**، يتيح لك **تعيين اللغة الأساسية**، وينتهي بـ **حفظ PDF بصيغة OCR** يمكنك فتحه في أي قارئ.

سنغطي أيضًا بعض النصائح العملية، مثل تمكين تسريع GPU لمعالجة أسرع ومعالجة المستندات متعددة اللغات (التاميل + الإنجليزية في مثالنا). في النهاية ستحصل على مقتطف جاهز للإنتاج يمكنك إدراجه في مشروعك.

## ما ستحتاجه

- **Java 17** (أو أي JDK حديث؛ Aspose.OCR يدعم Java 8+)
- مكتبة **Aspose.OCR for Java** (حمّلها من الموقع الرسمي أو أضفها عبر Maven)
- **ملف ترخيص** (أو تجربة مجانية لمدة 30 يومًا)
- ملف صورة يحتوي على نص (يستخدم المثال `sample-mixed-tamil-eng.jpg`)

لا أطر إضافية، ولا تبعيات أصلية—فقط Java عادي وملفات Aspose.JAR.

---

## الخطوة 1: إنشاء PDF قابل للبحث – إعداد المشروع

قبل أن نغوص في الكود، دعنا نتأكد أن المشروع جاهز لإنشاء ملفات **PDF قابل للبحث**.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **نصيحة احترافية:** احرص على تحديث رقم الإصدار؛ الإصدارات الأحدث غالبًا ما تتضمن تحسينات أداء لاستخدام GPU.

الآن أنشئ فئة Java بسيطة تسمى `RecentFeaturesDemo`. ستحمل هذه الفئة كل المنطق اللازم لـ **load image OCR**، ضبط إعدادات اللغة، وأخيرًا **save OCR pdf**.

---

## الخطوة 2: تحميل صورة OCR وتهيئة المحرك

الخطوة الفعلية الأولى في سير العمل هي **load image OCR**. هذا يخبر Aspose.OCR أي ملف يجب تحليله.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **لماذا هذا مهم:** تمكين GPU (`setUseGpu(true)`) يمكن أن يقلل زمن المعالجة حتى 70 % على الأجهزة الحديثة، بينما يضمن المعالجة المتوازية عدم بقاء الـ CPU غير مستخدم عندما يكون الـ GPU مشغولًا.

---

## الخطوة 3: تعيين اللغة الأساسية (ولغة ثانوية)

إذا تخطيت هذه الخطوة، سيحاول Aspose.OCR تخمين اللغة، مما يكون أبطأ وأقل دقة. إليك كيفية **set primary language** إلى التاميل وإضافة الإنجليزية كخيار احتياطي.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **شرح:** اللغة الأساسية تؤثر على مجموعة الأحرف والقاموس المستخدم أثناء التعرف. إضافة لغة ثانوية أمر حاسم للمستندات ذات النصوص المختلطة (مثل إيصال يحتوي على تاميل وإنجليزية).  
> **حالة خاصة:** إذا كان مستندك يحتوي على أكثر من لغتين، يمكنك استدعاء `addAdditionalLanguage(...)` لكل لغة إضافية.

---

## الخطوة 4: ما قبل معالجة الصورة – تصحيح الميل وإزالة الضوضاء

غالبًا ما تعاني الصور الممسوحة من دوران أو ضوضاء خلفية. تساعد المعالجة المسبقة محرك OCR على **extract text from image** بشكل أكثر موثوقية.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **نصيحة:** إذا كنت تعلم أن الصورة نظيفة بالفعل، يمكنك تخطي `setDenoise(true)` لتوفير بضع مليثانية.

---

## الخطوة 5: تحميل ملف الصورة

الآن بعد أن أصبح المحرك جاهزًا، نشير إليه إلى الملف الذي نريد تحليله.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **ماذا لو كان المسار غير صحيح؟** يطرح Aspose.OCR استثناء واضح `FileNotFoundException`. احرص على وضع الاستدعاء داخل `try‑catch` إذا كنت تحتاج إلى معالجة الأخطاء برفق.

---

## الخطوة 6: تشغيل OCR واستخراج النص من الصورة

مع كل الإعدادات جاهزة، حان الوقت لتشغيل عملية التعرف فعليًا. هذه الخطوة تقوم بـ **extract text from image** وتجهز البيانات اللازمة لإنشاء PDF.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

الإخراج النموذجي في وحدة التحكم للصورة التجريبية يكون كالتالي:

```
வணக்கம் World
This is a mixed language sample.
```

ستلاحظ أن السطر التاميلي تم عرضه بشكل صحيح، يليه النص الإنجليزي. هذا هو ناتج **set primary language** بشكل صحيح.

---

## الخطوة 7: حفظ PDF بصيغة OCR – القطعة الأخيرة

القطعة الأخيرة من اللغز هي **save OCR pdf**. يستطيع Aspose.OCR تضمين طبقة نص غير مرئية فوق الصورة الأصلية، مما يجعل PDF قابلًا للبحث.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

افتح `searchable.pdf` في Adobe Reader، اضغط **Ctrl + F**، وستتمكن من البحث عن كلمات التاميل والإنجليزية معًا—تمامًا ما يقدمه سير عمل **create searchable pdf**.

---

## مثال كامل يعمل (نسخ‑لصق)

فيما يلي البرنامج الكامل الذي يمكنك تجميعه وتشغيله كما هو. استبدل مسارات الملفات الوهمية بمساراتك الخاصة.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

شغّله باستخدام:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

يجب أن ترى النص المستخرج يُطبع في وحدة التحكم، يليه تأكيد أن **searchable pdf** تم حفظه على القرص.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو أردت **load image OCR** من مصفوفة بايت؟

يمكنك استبدال `ImageStream.fromFile(imagePath)` بـ `ImageStream.fromBytes(byteArray)`. هذا مفيد عندما تأتي الصورة من قاعدة بيانات أو خدمة ويب.

### كيف أتعامل مع ملفات PDF التي تحتوي بالفعل على صور؟

يمكن لـ Aspose.OCR العمل مباشرة على صفحات PDF: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. سيقوم المحرك بتحويل كل صفحة إلى صورة داخلية قبل التعرف.

### الـ GPU الخاص بي غير مكتشف—هل يجب أن أبقي `setUseGpu(true)`؟

إذا فشل `setUseGpu(true)`, فإن Aspose.OCR ينتقل تلقائيًا إلى CPU. يمكنك التحقق من `ocrEngine.getEngineSettings().isGpuAvailable()` قبل تمكينه.

### هل يمكنني **save OCR pdf** مع بيانات تعريف مخصصة؟

نعم. بعد التعرف، استخدم `ocrEngine.getPdfSaveOptions().setTitle("My Document")` أو `setAuthor("John Doe")` قبل استدعاء `save`.

---

## نصائح أداء للدفعات الكبيرة

- **معالجة دفعات:** أعد استخدام نفس كائن `OcrEngine` عبر عدة صور. استدعِ `ocrEngine.clear()` فقط بين كل تشغيل.
- **مجمع خيوط:** غلف كل مهمة صورة داخل `Callable` وقدِّمها إلى `ExecutorService`. بما أننا فعلنا المعالجة المتوازية، سيستفيد كل خيط من تعدد النوى.
- **إدارة الذاكرة:** للصور ذات الدقة الضخمة (جيغابكسل)، فكر في تقليل الحجم باستخدام `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` للحفاظ على استهلاك الذاكرة ضمن الحدود المعقولة.

---

## الخلاصة

لقد استعرضنا الآن سير عمل كامل لإنشاء **PDF قابل للبحث** باستخدام Aspose.OCR للـ Java. بدءًا من **load image OCR**، قمنا بـ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}