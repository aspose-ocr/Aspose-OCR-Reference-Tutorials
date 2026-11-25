---
category: general
date: 2026-10-24
description: تعلم كيفية استخراج النص من صورة باستخدام Aspose OCR في Java، مع دعم اللغات
  الإنجليزية والأوكرانية والعربية. دليل خطوة بخطوة لتحميل الصورة للـ OCR وتشغيل الـ
  OCR على الصورة.
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- Aspose OCR Java
- multi language OCR
lastmod: 2026-10-24
og_description: تعلم كيفية استخراج النص من صورة باستخدام Aspose OCR في Java، مع دعم
  اللغات الإنجليزية والأوكرانية والعربية. خطوات تحميل الصورة للـ OCR وتشغيل الـ OCR
  على الصورة.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR in Java'
og_title: كيفية استخراج النص من صورة باستخدام Aspose OCR في Java
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to extract text from image using Aspose OCR in Java, supporting
    English, Ukrainian and Arabic. Step‑by‑step guide to load image for OCR and run
    OCR on image.
  headline: How to extract text from image with Aspose OCR in Java
  type: TechArticle
- questions:
  - answer: No, a single Aspose OCR license covers all bundled language packs.
    question: Do I need a separate license for each language pack?
  - answer: The only practical limit is memory; Aspose processes each image sequentially,
      so you can add hundreds of files without issue.
    question: Is there a limit on the number of images I can add to `OcrInput`?
  - answer: The engine analyses each text block independently, so it can switch languages
      mid‑line and still produce accurate results.
    question: How does auto‑detection handle mixed scripts on the same line?
  - answer: Yes, `OcrResult` provides a `getConfidence()` method for granular quality
      metrics.
    question: Can I get confidence scores for each recognized word?
  - answer: Aspose OCR works with Java 8 through Java 21, including LTS releases.
    question: What Java versions are supported?
  type: FAQPage
tags:
- Aspose
- OCR
- Java
- extract text from image
- multi language OCR
title: كيفية استخراج النص من صورة باستخدام Aspose OCR في Java
url: /ar/java/advanced-ocr-techniques/how-to-use-aspose-for-multi-language-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج النص من صورة باستخدام Aspose OCR في جافا

إذا كنت بحاجة إلى **استخراج النص من صورة** التي تحتوي على مزيج من الأحرف الإنجليزية والأوكرانية والعربية، فإن Aspose OCR يجعل الأمر بسيطًا. في هذا الدرس ستشاهد مثالًا كاملًا جاهزًا للتنفيذ يوضح كيفية **تحميل الصورة للتعرف الضوئي على الأحرف**، وتمكين *التعرف الضوئي على الأحرف متعدد اللغات*، وأخيرًا **تشغيل التعرف الضوئي على الصورة** لاسترجاع نص نظيف وقابل للقراءة. تم شرح الخطوات بلغة بسيطة، بحيث تفهم *ما* يجب فعله و*لماذا* هو مهم.

## إجابات سريعة
- **ما هو السطر الأول من الكود؟** `OcrEngine engine = new OcrEngine();`
- **ما هي اللغات المدعومة مباشرةً؟** English (`en`), Ukrainian (`uk`), Arabic (`ar`) and 27 additional languages.
- **هل أحتاج إلى ترخيص للاختبار؟** No, a free trial works, but a license removes the watermark.
- **هل يمكنني معالجة عدة صور في آن واحد؟** Yes, use `OcrInput` to add several files before calling `recognize`.
- **ما نسخة جافا المطلوبة؟** Java 8 or newer.

## كيفية استخراج النص من صورة باستخدام Aspose OCR في جافا؟
حمّل صورتك باستخدام `OcrInput`، قم بتكوين `OcrEngine` للغات المطلوبة، ثم استدعِ `engine.recognize(input)`. يكتشف المحرك تلقائيًا كتل اللغة، يطبق نموذج OCR المناسب، ويعيد كائن `OcrResult` يحتوي على النص المعترف به. هذا التدفق خطوة واحدة يعمل مع أي حجم صورة يصل إلى 10 000 × 10 000 بكسل ويدعم أكثر من 30 حزمة لغة.

## ما ستتعلمه
- إضافة مكتبة Aspose OCR إلى مشروع جافا (Maven أو Gradle).  
- تهيئة محرك OCR بشكل صحيح.  
- تكوين المحرك لـ *التعرف الضوئي على الأحرف متعدد اللغات* وتمكين الكشف التلقائي.  
- تحميل صورة تحتوي على نصوص مختلطة.  
- تنفيذ التعرف و**استخراج النص من صورة**.  
- معالجة المشكلات الشائعة مثل اللغات غير المدعومة أو الملفات المفقودة.

بنهاية الدرس ستحصل على فئة جافا مستقلة يمكنك إدراجها في أي مشروع والبدء في معالجة الصور فورًا.

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| جافا 8 أو أحدث | Aspose OCR يستهدف جافا 8+. |
| Maven أو Gradle (أي أداة بناء) | يقوم بسحب ملف JAR الخاص بـ Aspose OCR تلقائيًا. |
| ملف صورة يحتوي على نص متعدد اللغات (مثال: `mixed_script.jpg`) | هذا هو ما سنقوم **بتحميل الصورة للتعرف الضوئي على الأحرف**. |
| ترخيص Aspose OCR صالح (اختياري) | بدون ترخيص ستحصل على مخرجات مائية، لكن الكود يعمل بنفس الطريقة. |

هل لديك كل ذلك؟ رائع—لنبدأ.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

### Maven

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of Feb 2026 -->
</dependency>
```

### Gradle

```groovy
// build.gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** يدعم Aspose OCR أكثر من 30 حزمة لغة ويمكنه معالجة صور تصل إلى 10 000 × 10 000 بكسل دون تحميل الملف بالكامل إلى الذاكرة، لذا يمكنك التعامل مع المسحات عالية الدقة بكفاءة.

إضافة الاعتماد هي الخطوة الملموسة الأولى في **كيفية استخدام Aspose**—المكتبة تجلب الفئات `OcrEngine`، `OcrInput`، و`OcrResult` التي سنحتاجها لاحقًا.

## الخطوة 2: تهيئة محرك OCR
فئة `OcrEngine` هي المكوّن الأساسي في Aspose OCR الذي يقوم بعملية التعرف.  

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create the OCR engine – the core object that does all the heavy lifting.
        OcrEngine engine = new OcrEngine();

        // Step 2.2: (Optional) Apply your license to avoid watermarks.
        // engine.setLicense("Aspose.Total.lic");
```

**لماذا هذا مهم:**  
إذا تخطيت تهيئة المحرك، لن يكون هناك شيء لتـ*تشغيل التعرف الضوئي على الصورة* لاحقًا، وستواجه استثناء `NullPointerException`.

## الخطوة 3: تكوين دعم متعدد اللغات والكشف التلقائي
توفر `OcrEngine` طريقة `setRecognitionLanguages` لتحديد نماذج اللغات التي يجب تحميلها، وتُمكّن `setAutoDetectLanguage` الكشف التلقائي عن اللغة لكل كتلة نصية.  

```java
        // Step 3.1: Tell the engine which languages you expect.
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });

        // Step 3.2: Enable automatic language detection – crucial for mixed‑script images.
        engine.setAutoDetectLanguage(true);
```

**التفسير:**  
- `"en"` = English, `"uk"` = Ukrainian, `"ar"` = Arabic.  
- يتيح الكشف التلقائي لـ Aspose فحص الصورة، تحديد اللغة التي ينتمي إليها كل مقطع، وتطبيق نموذج OCR المناسب. بدون ذلك سيتعين عليك تشغيل ثلاث عمليات تعرف منفصلة—مما يكون مرهقًا وعرضة للأخطاء.

## الخطوة 4: تحميل الصورة للتعرف الضوئي على الأحرف
`OcrInput` هو حاوية Aspose OCR التي تحتفظ بتدفقات صورة واحدة أو أكثر للمعالجة.  

```java
        // Step 4.1: Prepare an OcrInput container.
        OcrInput input = new OcrInput();

        // Step 4.2: Add the image file. Replace the path with your actual location.
        input.add("YOUR_DIRECTORY/mixed_script.jpg");
```

> **لماذا نستخدم `OcrInput`:** يمكنه احتواء صفحات أو صور متعددة، مما يمنحك المرونة **لتحميل الصورة للتعرف الضوئي على الأحرف** في وضع الدفعة لاحقًا. إذا لم يُعثر على الملف، يرمي Aspose استثناء `FileNotFoundException`. فحص سريع (`if (!new File(path).exists())`) يوفر وقت التصحيح.

## الخطوة 5: تشغيل التعرف الضوئي على الصورة
طريقة `recognize` تحلل الصورة، تكتشف كتل اللغة، وتنتج كائن `OcrResult` يحتوي على النص المعترف به.  

```java
        // Step 5.1: Execute the recognition process.
        OcrResult result = engine.recognize(input);
```

## الخطوة 6: استخراج النص من الصورة وعرضه
`OcrResult` يضم الإخراج النصي النهائي، بما في ذلك فواصل الأسطر ونقاط الثقة.  

```java
        // Step 6.1: Pull the plain text out of the result.
        String extractedText = result.getText();

        // Step 6.2: Print it to the console – you could also write it to a file.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

**ما ستراه:**  
إذا كان ملف `mixed_script.jpg` يحتوي على “Hello мир مرحبا”، فإن مخرجات وحدة التحكم ستكون:

```
=== Extracted Text ===
Hello мир مرحبا
```

هذا هو الحل الكامل لـ **كيفية استخدام Aspose** لـ **استخراج النص من صورة** مع لغات متعددة.

## حالات الحافة والأسئلة الشائعة

### ماذا لو لم يتم التعرف على لغة؟
يدعم Aspose فقط اللغات التي يتوفر لها نماذج OCR. لإضافة اليابانية، أدرج `"ja"` في `setRecognitionLanguages`. إذا لم يكن النموذج موجودًا، يعود المحرك إلى اللغة الافتراضية (الإنجليزية) وستحصل على أحرف مشوشة.

### كيف تحسن الدقة على الصور منخفضة الدقة؟
تحدد `setResolution` قيمة DPI التي يفترضها المحرك للصورة المدخلة، مما يساعد في المسحات منخفضة الدقة.  
تختار `setPreprocessOptions` إجراءات ما قبل المعالجة مثل التدوير التلقائي قبل OCR.  

- قم بمعالجة الصورة مسبقًا (زيادة DPI، تطبيق التثليث).  
- استخدم `engine.setResolution(300)` لإبلاغ المحرك بـ DPI المتوقع.  
- فعّل `engine.setPreprocessOptions(OcrEngine.PreprocessOptions.AutoRotate)` للصور المدورة.

### هل يمكنني معالجة مجلد من الصور؟
بالطبع. ضع استدعاء `input.add()` داخل حلقة تت iterates على جميع الملفات في دليل. استدعاء `engine.recognize(input)` نفسه سيعيد النص المدمج لكل صفحة.

## مثال كامل يعمل (جاهز للنسخ واللصق)

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Optional: apply your license to avoid watermarks
        // engine.setLicense("Aspose.Total.lic");

        // Configure languages (English, Ukrainian, Arabic) and enable auto‑detect
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });
        engine.setAutoDetectLanguage(true);

        // Load the image that contains mixed‑language text
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/mixed_script.jpg"); // <-- replace with your path

        // Run the recognition process
        OcrResult result = engine.recognize(input);

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

احفظ هذا كملف `MultiLangOcrDemo.java`، ثم قم بالترجمة باستخدام `javac`، وشغّله بـ `java MultiLangOcrDemo`. إذا تم إعداد كل شيء بشكل صحيح، سترى النص المعترف به مطبوعًا في وحدة التحكم.

## الأسئلة المتكررة

**س: هل أحتاج إلى ترخيص منفصل لكل حزمة لغة؟**  
ج: لا، ترخيص واحد لـ Aspose OCR يغطي جميع حزم اللغة المدمجة.

**س: هل هناك حد لعدد الصور التي يمكنني إضافتها إلى `OcrInput`؟**  
ج: الحد العملي الوحيد هو الذاكرة؛ Aspose يعالج كل صورة على حدة، لذا يمكنك إضافة مئات الملفات دون مشكلة.

**س: كيف يتعامل الكشف التلقائي مع النصوص المختلطة في نفس السطر؟**  
ج: يحلل المحرك كل كتلة نصية بشكل مستقل، وبالتالي يمكنه تبديل اللغات داخل السطر وإنتاج نتائج دقيقة.

**س: هل يمكنني الحصول على درجات الثقة لكل كلمة معترف بها؟**  
ج: نعم، يوفر `OcrResult` طريقة `getConfidence()` للحصول على مقاييس جودة دقيقة.

**س: ما إصدارات جافا المدعومة؟**  
ج: يعمل Aspose OCR مع جافا 8 حتى جافا 21، بما في ذلك إصدارات LTS.

## الخلاصة
غطينا **كيفية استخدام Aspose** من البداية إلى النهاية: من إضافة المكتبة، مرورًا بتكوين *التعرف الضوئي على الأحرف متعدد اللغات*، إلى **تحميل الصورة للتعرف الضوئي على الأحرف**، **تشغيل التعرف الضوئي على الصورة**، وأخيرًا **استخراج النص من صورة**. النهج قابل للتوسع—فقط أضف رموز لغات إضافية أو قدم قائمة ملفات، وستحصل على خط أنابيب OCR قوي في دقائق.

ما التالي؟ جرّب هذه الأفكار:

- **معالجة دفعات:** كرّر عبر دليل واكتب كل نتيجة إلى ملف `.txt` منفصل.  
- **معالجة لاحقة:** استخدم regex أو مكتبات NLP لتنظيف الإخراج (إزالة فواصل الأسطر الزائدة، تصحيح أخطاء OCR الشائعة).  
- **تكامل:** عرّف خطوة OCR عبر نقطة نهاية REST في Spring Boot حتى تتمكن الخدمات الأخرى من إرسال صور واستلام نص مشفر بـ JSON.

لا تتردد في التجربة، كسر الأشياء، ثم إصلاحها—هذه هي الطريقة لتصبح محترفًا في OCR مع Aspose. إذا واجهت أي صعوبات، اترك تعليقًا أدناه. برمجة سعيدة!  

---

![how to use aspose OCR screenshot](/images/aspose-ocr-demo.png){alt="مثال على كيفية استخدام Aspose OCR يظهر كود جافا"}

[لقطة شاشة لاستخدام Aspose OCR](/images/aspose-ocr-demo.png)

**آخر تحديث:** 2026-10-24  
**تم الاختبار مع:** Aspose OCR 24.11 for Java  
**المؤلف:** Aspose

## دروس ذات صلة

- [تحميل صورة للتعرف الضوئي على الأحرف في جافا دليل خطوة بخطوة](/ocr/java/ocr-operations/load-image-for-ocr-in-java-step-by-step-guide/)
- [الكشف التلقائي عن اللغة في جافا OCR دليل خطوة بخطوة](/ocr/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/)
- [كيفية تمكين GPU للتعرف الضوئي على الأحرف في جافا استخراج النص من الصورة](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}