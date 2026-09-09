---
category: general
date: 2026-01-07
description: احصل على نص OCR من صورة باستخدام Aspose OCR Java. تعلم كيفية استخراج
  نص الصورة، تحميل صورة OCR، وتشغيل مثال OCR بلغة Java في دقائق.
draft: false
keywords:
- get OCR text
- extract text image
- java OCR example
- aspose OCR Java
- load image OCR
language: ar
og_description: احصل على نص OCR من الصور باستخدام Aspose OCR Java. يوضح هذا الدليل
  مثالًا على OCR في جافا، كيفية استخراج نص الصورة، وكيفية تحميل OCR للصور بكفاءة.
og_title: احصل على نص OCR في جافا – دليل Aspose OCR الكامل
tags:
- OCR
- Java
- Aspose
- Image Processing
title: احصل على نص OCR في جافا – مثال كامل لأسبوز OCR
url: /ar/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# احصل على نص OCR في Java – مثال كامل لـ Aspose OCR

هل احتجت يومًا إلى **الحصول على نص OCR** من مستند ممسوح ضوئيًا ولكنك لم تكن متأكدًا أي مكتبة تختار؟ لست وحدك. في العديد من المشاريع الواقعية—مثل أتمتة الفواتير، معالجة الإيصالات، أو رقمنة النماذج متعددة اللغات—يُعد استخراج النص من الصور الخطوة الأولى نحو الأتمتة.  

في هذا البرنامج التعليمي سنستعرض **مثال java OCR** يستخدم مكتبة Aspose OCR for Java. بنهاية الدرس ستعرف كيف **تحمل صورة OCR**، تشغل المحرك، و**استخراج نص الصورة** ببضع أسطر من الشيفرة فقط. لا إطالة، مجرد حل عملي يمكنك نسخه ولصقه في مشروعك.

## ما ستتعلمه

- كيفية إعداد Aspose OCR for Java (بما في ذلك إحداثيات Maven).  
- الخطوات الدقيقة لـ **load image OCR** وتحديد لغة.  
- كيفية **get OCR text** كسلسلة نصية عادية وطباعةها على وحدة التحكم.  
- نصائح للتعامل مع الصور متعددة اللغات واكتشاف اللغات تلقائيًا.  

*المتطلبات المسبقة*: Java 8 أو أحدث، بيئة تطوير متوافقة مع Maven (IntelliJ IDEA، Eclipse، أو VS Code)، ورخصة صالحة لـ Aspose OCR for Java (الإصدار التجريبي المجاني يعمل للتقييم).

![مخطط يوضح كيفية الحصول على نص OCR من صورة باستخدام Aspose OCR Java](https://example.com/ocr-flowchart.png "مخطط تدفق الحصول على نص OCR")

## الخطوة 1 – إضافة تبعية Aspose OCR (Load Image OCR)

أولاً، أخبر Maven بجلب مكتبة Aspose OCR. افتح ملف `pom.xml` وأدرج كتلة `<dependency>` التالية داخل `<dependencies>`:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **نصيحة احترافية**: إذا كنت تستخدم Gradle، المكافئ هو `implementation 'com.aspose:aspose-ocr:23.9'`. إضافة التبعية هي الطريقة الأسرع للحصول على قدرات **load image OCR** في مشروعك.

## الخطوة 2 – إنشاء محرك OCR وتحميل صورتك

الآن سنكتب فئة Java صغيرة تنشئ كائن `OcrEngine`، تشير إليه إلى ملف صورة، وتخبر المحرك أي لغة يجب التعرف عليها. تُحدد اللغة برمز ISO‑639‑2 (مثال، `"tam"` للغة التاميلية).

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### لماذا تحديد اللغة صراحةً؟

تحديد اللغة يقلل من الإيجابيات الكاذبة ويسرّع عملية التعرف. بالنسبة لملفات PDF متعددة اللغات يمكنك التكرار عبر مصفوفة من رموز اللغات، أو تمكين الاكتشاف التلقائي للراحة.

## الخطوة 3 – تشغيل عملية OCR و **Get OCR Text**

مع تكوين المحرك، السطر التالي يقوم فعليًا بعملية التعرف. يحتوي كائن النتيجة على السلسلة المستخرجة وبيانات وصفية إضافية.

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

عند تشغيل `LanguageExample`، يجب أن ترى شيئًا مشابهًا لـ:

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

إذا استخدمت `setAutoDetectLanguage(true)`، سيحاول المحرك تخمين اللغة لك، وهو مفيد عند التعامل مع مستندات غير معروفة.

## الخطوة 4 – معالجة الحالات الشائعة (Extract Text Image Variations)

### التعامل مع الصور منخفضة الدقة

تنخفض دقة OCR بشكل كبير تحت 300 dpi. إذا كانت صورتك المصدرية منخفضة الدقة، فكر في تكبيرها أولاً:

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### إزالة الضوضاء الخلفية

أحيانًا تحتوي النماذج الممسوحة على بقع تُربك المحرك. يمكنك تمكين المعالجة المسبقة:

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### استخراج النص من مناطق محددة

إذا كنت تحتاج النص فقط من مستطيل معين (مثال، خلية جدول)، عيّن `Rectangle` قبل استدعاء `recognize()`:

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

هذه التعديلات تجعل **java OCR example** قويًا بما يكفي لأعباء العمل الإنتاجية.

## الخطوة 5 – التحقق من النتيجة (ما الذي يجب أن تتوقعه؟)

تشغيل ناجح سيطبع النسخة النصية العادية للصورة. بالنسبة للصور متعددة اللغات قد ترى نصوصًا مختلطة:

```
Hello World
こんにちは世界
مرحبا بالعالم
```

إذا كان الإخراج فارغًا أو مشوشًا، تحقق مرة أخرى:

1. مسار الملف في `setImage` (هل هو صحيح؟).  
2. رمز اللغة يتطابق مع النص في الصورة.  
3. جودة الصورة (التباين، DPI) كافية.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي الملف بالكامل، جاهز للتجميع والتشغيل. استبدل `YOUR_DIRECTORY/multilingual.png` بالمسار الفعلي لصورتك التجريبية.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

قم بالتجميع وتشغيل:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

يجب الآن أن ترى المحتوى المستخرج يُطبع على وحدة التحكم الخاصة بك.

---

## الخاتمة

لقد أظهرنا لك الآن **كيفية الحصول على نص OCR** من صورة باستخدام Aspose OCR for Java. باتباع هذا **java OCR example**، يمكنك **استخراج نص الصورة**، **load image OCR**، وحتى تعديل المحرك للمدخلات متعددة اللغات أو ذات الضوضاء.

من هنا قد:

- دمج خطوة OCR في سير عمل أكبر (مثال، تخزين النص في قاعدة بيانات).  
- دمجها مع واجهة برمجة تطبيقات ترجمة لتحويل المسحات متعددة اللغات إلى لغة واحدة.  
- تجربة ميزات Aspose OCR الأخرى مثل تحويل PDF أو اكتشاف الباركود.

جرّبه، اكسر بعض الأشياء، ثم عدّل الإعدادات حتى يصبح الإخراج مثاليًا. برمجة سعيدة، ولتكن OCR دائمًا واضحة كالكريستال!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}