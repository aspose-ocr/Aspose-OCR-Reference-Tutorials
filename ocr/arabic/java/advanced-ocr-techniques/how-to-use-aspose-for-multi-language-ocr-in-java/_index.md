---
category: general
date: 2026-02-22
description: كيفية استخدام Aspose لإجراء OCR متعدد اللغات واستخراج النص من ملفات الصور
  — تعلم كيفية تحميل الصورة للـ OCR وتشغيل OCR على الصورة بكفاءة.
draft: false
keywords:
- how to use aspose
- multi language ocr
- extract text from image
- load image for ocr
- run ocr on image
language: ar
og_description: كيفية استخدام Aspose لتشغيل OCR على الصور بعدة لغات – دليل خطوة بخطوة
  لتحميل الصورة للـ OCR واستخراج النص من الصورة.
og_title: كيفية استخدام Aspose للتعرف الضوئي على الأحرف متعدد اللغات في جافا
tags:
- Aspose
- OCR
- Java
title: كيفية استخدام Aspose للتعرف الضوئي على النص متعدد اللغات في Java
url: /ar/java/advanced-ocr-techniques/how-to-use-aspose-for-multi-language-ocr-in-java/
---

Aspose OCR يُظهر كود Java". Keep alt attribute.

Then closing shortcodes.

Proceed to produce final content.

Be careful to keep code block placeholders unchanged.

Also ensure markdown formatting preserved.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Aspose للتعرف الضوئي على الحروف (OCR) متعدد اللغات في Java

هل تساءلت يومًا **كيفية استخدام Aspose** عندما تحتوي صورتك على نص إنجليزي وأوكراني وعربي في آن واحد؟ لست وحدك—فالعديد من المطورين يواجهون هذه المشكلة عندما يحتاجون إلى *استخراج النص من الصورة* للملفات التي ليست أحادية اللغة.  

في هذا الدرس سنستعرض مثالًا كاملًا جاهزًا للتنفيذ يوضح لك كيف **تحمّل صورة للتعرف الضوئي (OCR)**، وتفعّل *التعرف الضوئي متعدد اللغات*، وأخيرًا **تشغّل OCR على الصورة** للحصول على نص نظيف وقابل للقراءة. لا مراجع غامضة، فقط كود ملموس وتفسير لكل سطر.

## ما ستتعلمه

- إضافة مكتبة Aspose OCR إلى مشروع Java (Maven أو Gradle).  
- تهيئة محرك OCR بشكل صحيح.  
- ضبط المحرك لـ *التعرف الضوئي متعدد اللغات* وتمكين الكشف التلقائي.  
- تحميل صورة تحتوي على نصوص مختلطة.  
- تنفيذ عملية التعرف و**استخراج النص من الصورة**.  
- التعامل مع المشكلات الشائعة مثل اللغات غير المدعومة أو الملفات المفقودة.

بنهاية هذا الدرس ستحصل على فئة Java مستقلة يمكنك إدراجها في أي مشروع والبدء في معالجة الصور فورًا.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

| المتطلب | لماذا يهم |
|-------------|----------------|
| Java 8 أو أحدث | Aspose OCR يستهدف Java 8+. |
| Maven أو Gradle (أي أداة بناء) | لسحب ملف JAR الخاص بـ Aspose OCR تلقائيًا. |
| ملف صورة يحتوي على نص متعدد اللغات (مثال: `mixed_script.jpg`) | هذا هو ما سنـ**حمّل صورة للتعرف الضوئي**. |
| رخصة Aspose OCR صالحة (اختياري) | بدون رخصة ستحصل على مخرجات مائية، لكن الكود سيعمل بنفس الطريقة. |

هل لديك كل ذلك؟ رائع—لنبدأ.

---

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

> **نصيحة احترافية:** راقب رقم الإصدار؛ الإصدارات الأحدث تضيف حزم لغات وتحسينات في الأداء.

إضافة الاعتماد هو الخطوة الأولى الملموسة في **كيفية استخدام Aspose**—المكتبة تجلب الفئات `OcrEngine` و`OcrInput` و`OcrResult` التي سنحتاجها لاحقًا.

---

## الخطوة 2: تهيئة محرك OCR

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
`OcrEngine` يضم خوارزميات التعرف. إذا تخطيت هذه الخطوة، لن يكون هناك شيء لتـ*تشغيل OCR على الصورة* لاحقًا، وستواجه `NullPointerException`.

---

## الخطوة 3: ضبط دعم متعدد اللغات والكشف التلقائي

```java
        // Step 3.1: Tell the engine which languages you expect.
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });

        // Step 3.2: Enable automatic language detection – crucial for mixed‑script images.
        engine.setAutoDetectLanguage(true);
```

**التفسير:**  
- `"en"` = English، `"uk"` = Ukrainian، `"ar"` = Arabic.  
- الكشف التلقائي يسمح لـ Aspose بمسح الصورة، وتحديد اللغة التي ينتمي إليها كل جزء، وتطبيق نموذج OCR المناسب. بدون ذلك سيتعين عليك تشغيل ثلاث عمليات تعرّف منفصلة—مما يسبب تعقيدًا وأخطاء.

---

## الخطوة 4: تحميل الصورة للتعرف الضوئي

```java
        // Step 4.1: Prepare an OcrInput container.
        OcrInput input = new OcrInput();

        // Step 4.2: Add the image file. Replace the path with your actual location.
        input.add("YOUR_DIRECTORY/mixed_script.jpg");
```

> **لماذا نستخدم `OcrInput`:** يمكنه احتواء صفحات أو صور متعددة، مما يمنحك المرونة لـ *تحميل صورة للتعرف الضوئي* في وضع الدفعة لاحقًا.

إذا لم يُعثر على الملف، ستطرح Aspose استثناءً من نوع `FileNotFoundException`. يمكن لشرط سريع مثل `if (!new File(path).exists())` أن يوفر عليك وقت التصحيح.

---

## الخطوة 5: تشغيل OCR على الصورة

```java
        // Step 5.1: Execute the recognition process.
        OcrResult result = engine.recognize(input);
```

في هذه المرحلة يحلل المحرك الصورة، يكتشف كتل اللغات، وينتج كائن `OcrResult` يحتوي على النص المُعترف به.

---

## الخطوة 6: استخراج النص من الصورة وعرضه

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
إذا كان ملف `mixed_script.jpg` يحتوي على “Hello мир مرحبا”، فستكون مخرجات وحدة التحكم:

```
=== Extracted Text ===
Hello мир مرحبا
```

هذه هي الحل الكامل لـ **كيفية استخدام Aspose** لـ *استخراج النص من الصورة* باستخدام عدة لغات.

---

## الحالات الخاصة والأسئلة الشائعة

### ماذا لو لم يتم التعرف على لغة معينة؟

Aspose يدعم فقط اللغات التي يتوفر لها نماذج OCR. إذا احتجت، على سبيل المثال، اليابانية، أضف `"ja"` إلى `setRecognitionLanguages`. إذا لم يكن النموذج موجودًا، سيعود المحرك إلى الإعداد الافتراضي (عادةً الإنجليزية) وستحصل على أحرف مشوشة.

### كيف يمكن تحسين الدقة في الصور منخفضة الدقة؟

- عالج الصورة مسبقًا (زيادة DPI، تطبيق التحويل إلى ثنائي).  
- استخدم `engine.setResolution(300)` لإبلاغ المحرك بالدقة المتوقعة.  
- فعّل `engine.setPreprocessOptions(OcrEngine.PreprocessOptions.AutoRotate)` للصور المائلة.

### هل يمكنني معالجة مجلد من الصور؟

بالتأكيد. ضع استدعاء `input.add()` داخل حلقة تتنقل عبر جميع الملفات في الدليل. استدعاء `engine.recognize(input)` نفسه سيعيد النص المدمج لكل صفحة.

---

## مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

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

احفظه باسم `MultiLangOcrDemo.java`، ثم قم بترجمته باستخدام `javac`، وشغّله بـ `java MultiLangOcrDemo`. إذا تم إعداد كل شيء بشكل صحيح، سترى النص المُعترف به يُطبع على وحدة التحكم.

---

## الخلاصة

غطّينا **كيفية استخدام Aspose** من البداية إلى النهاية: بدءًا من إضافة المكتبة، مرورًا بضبط *التعرف الضوئي متعدد اللغات*، إلى **تحميل صورة للتعرف الضوئي**، **تشغيل OCR على الصورة**، وأخيرًا **استخراج النص من الصورة**. النهج قابل للتوسيع—فقط أضف رموز لغات أخرى أو قوائم ملفات، وستحصل على خط أنابيب OCR قوي في دقائق.

ما التالي؟ جرّب هذه الأفكار:

- **معالجة دفعات:** كرّر عبر دليل واكتب كل نتيجة في ملف `.txt` منفصل.  
- **معالجة ما بعد التعرف:** استخدم تعبيرات regex أو مكتبات NLP لتنظيف المخرجات (إزالة الفواصل غير المرغوبة، تصحيح الأخطاء الشائعة).  
- **التكامل:** اربط خطوة OCR بنقطة نهاية REST في Spring Boot حتى تتمكن الخدمات الأخرى من إرسال صور واستلام نص مشفر بصيغة JSON.

لا تتردد في التجربة، وكسر الأشياء، ثم إصلاحها—هذه هي الطريقة لتصبح محترفًا في OCR باستخدام Aspose. إذا واجهت أي صعوبات، اترك تعليقًا أدناه. برمجة سعيدة!  

---

![how to use aspose OCR screenshot](/images/aspose-ocr-demo.png){alt="مثال على كيفية استخدام Aspose OCR يُظهر كود Java"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}