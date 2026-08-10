---
category: general
date: 2026-03-18
description: كيفية تمكين OCR بسرعة باستخدام Aspose OCR للغة Java. تعلم التعرف على
  النص من الصورة، ضبط الحد الأقصى للتوازي، استخراج النص من PNG، وتحميل الصورة للـ
  OCR.
draft: false
keywords:
- how to enable OCR
- recognize text from image
- set max parallelism
- extract text from png
- load image for OCR
language: ar
og_description: كيفية تمكين OCR باستخدام Aspose OCR للغة Java. يوضح هذا الدليل كيفية
  التعرف على النص من الصورة، وتعيين الحد الأقصى للتوازي، واستخراج النص من PNG، وتحميل
  الصورة للتعرف الضوئي على الأحرف.
og_title: كيفية تمكين OCR في جافا – دليل كامل
tags:
- Aspose OCR
- Java
- Parallel Processing
title: كيفية تمكين OCR في جافا باستخدام Aspose – دليل خطوة بخطوة كامل
url: /ar/java/ocr-operations/how-to-enable-ocr-in-java-with-aspose-complete-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين OCR في Java – دليل خطوة‑بخطوة كامل

هل تساءلت يومًا **كيف تمكّن OCR** في تطبيق Java الخاص بك دون قضاء أيام في البحث عبر وثائق الـ API؟ أنت لست الوحيد. يواجه معظم المطورين عقبة عندما يحتاجون إلى **التعرف على النص من صورة** — خاصةً ملفات PNG الكبيرة — مع الحفاظ على أداء مقبول.  

الأخبار السارة؟ مع Aspose OCR يمكنك تشغيل الميزة، تحميل صورة للـ OCR، وحتى زيادة عدد نوى المعالج لتسريع العملية. في هذا الدرس سنستعرض كل ما تحتاجه: تثبيت المكتبة، تحميل PNG، ضبط أقصى درجة للتوازي، وأخيرًا استخراج النص. في النهاية ستحصل على برنامج قابل للتنفيذ **يستخرج النص من ملفات PNG** بسرعة البرق.

### ما ستحتاجه

- Java 17 أو أحدث (الكود يُترجم مع إصدارات أقدم، لكن 17 هو الخيار المثالي)
- Maven أو Gradle لجلب ملف JAR الخاص بـ Aspose OCR (سنوضح Maven)
- صورة PNG تحتوي على نص قابل للبحث (كلما كانت أكبر، كان التوازي أفضل)
- قليل من الفضول — لا تحتاج إلى خبرة سابقة في OCR

إذا كان أي من ذلك غير مألوف لك، لا تقلق. سنغطي المتطلبات المسبقة مباشرة بعد المقدمة وسنقدم لك أوامر سريعة للإعداد.

---

## الخطوة 1: تثبيت Aspose OCR لـ Java

قبل أن تتمكن من **تمكين OCR**، يجب أن تكون المكتبة على مسار الفئات (classpath). أسهل طريقة هي إضافة تبعية Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **نصيحة احترافية:** إذا كنت تستخدم Gradle، فإن المكافئ هو  
> `implementation 'com.aspose:aspose-ocr:23.12'`.  

بمجرد حل التبعية، سيقوم بيئة التطوير المتكاملة (IDE) بتحميل ملفات JAR تلقائيًا. لا حاجة للتعامل اليدوي مع ملفات JAR.

---

## الخطوة 2: تحميل صورة للـ OCR

الخطوة العملية الأولى هي **تحميل صورة للـ OCR**. توفر Aspose طريقة ثابتة `Image.load` تقبل مسار ملف أو تدفق. لنبسط الأمر ونستخدم مسار ملف:

```java
import com.aspose.ocr.Image;

// ...

// Replace with the absolute or relative path to your PNG
String imagePath = "src/main/resources/large-document.png";
Image image = Image.load(imagePath);
```

> **لماذا هذا مهم:** تحميل الصورة مرة واحدة وإعادة استخدام نفس كائن `Image` يتجنب عمليات I/O إضافية عندما تقوم بتشغيل عدة عمليات التعرف على نفس الملف (مثلًا، إعدادات لغة مختلفة).

إذا لم يُعثر على الملف، تُطلق Aspose استثناء `IOException`. في بيئة الإنتاج يمكنك تغليفه بـ try‑catch وربما الرجوع إلى صورة افتراضية.

---

## الخطوة 3: إنشاء محرك OCR وتمكين المعالجة المتوازية

الآن نصل إلى جوهر الموضوع—**كيف تمكّن OCR** مع التوازي. فئة `OcrEngine` تقوم بالعمل الشاق، وخصائص `ParallelSettings` تتيح لك التحكم في الخيوط.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ParallelSettings;

// ...

OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing
ParallelSettings parallelSettings = new ParallelSettings();
parallelSettings.setEnabled(true);

// Set the maximum number of threads to the number of available CPU cores
int cores = Runtime.getRuntime().availableProcessors();
parallelSettings.setMaxDegreeOfParallelism(cores);

// Apply the settings to the engine
ocrEngine.setParallelSettings(parallelSettings);
```

### لماذا نضبط `MaxDegreeOfParallelism`؟

- **الأداء:** ملفات PNG الكبيرة قد تحتوي على آلاف القطع النصية. بشكل افتراضي تقوم Aspose بمعالجتها تسلسليًا، ما قد يكون بطيئًا على الأجهزة متعددة النوى.
- **التحكم:** قد ترغب في تقييد عدد الخيوط على خادم مشترك لتجنب استنزاف موارد الخدمات الأخرى. اضبط `cores` وفقًا لذلك.

---

## الخطوة 4: التعرف على النص من الصورة

مع تهيئة المحرك، استدعاء OCR الفعلي هو سطر واحد:

```java
String recognizedText = ocrEngine.recognize(image);
```

خلف الكواليس، تقوم Aspose بتقسيم الصورة إلى كتل، تمرير كل كتلة عبر شبكة عصبونية، ثم تجميع النتائج معًا. وبما أننا فعلنا التوازي، تُعالج هذه الكتل بشكل متزامن.

---

## الخطوة 5: إخراج أو حفظ النص المستخرج

أخيرًا، قرر ما ستفعله بالنتيجة. للعرض السريع سنطبعها على وحدة التحكم، لكن يمكنك كتابة النص إلى ملف، قاعدة بيانات، أو حتى تمريره إلى خط أنابيب NLP لاحق.

```java
System.out.println("=== OCR Result ===");
System.out.println(recognizedText);
```

إذا كنت بحاجة إلى **استخراج النص من ملفات PNG** دفعة واحدة، ما عليك سوى وضع الخطوات السابقة داخل حلقة تتنقل عبر مجلد. تذكر إعادة استخدام نفس كائن `OcrEngine` — إنشاء محرك جديد لكل ملف يُفقد فائدة التوازي.

---

## مثال كامل جاهز للتنفيذ

بدمج كل ما سبق، إليك فئة Java كاملة جاهزة للتشغيل. انسخ‑الصقها في `src/main/java/com/example/ParallelOcrDemo.java` وشغّل `mvn compile exec:java`.

```java
package com.example;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ParallelSettings;
import com.aspose.ocr.Image;

/**
 * Demonstrates how to enable OCR with Aspose, set max parallelism,
 * load an image for OCR, and extract text from a PNG file.
 */
public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing to speed up recognition
        ParallelSettings parallelSettings = new ParallelSettings();
        parallelSettings.setEnabled(true);
        // Use all available CPU cores; adjust if you need to limit resources
        parallelSettings.setMaxDegreeOfParallelism(
                Runtime.getRuntime().availableProcessors()
        );
        ocrEngine.setParallelSettings(parallelSettings);

        // Step 3: Load the image that contains the text to be recognized
        // Replace the path with your own PNG file location
        Image image = Image.load("src/main/resources/large-document.png");

        // Step 4: Perform OCR on the loaded image
        String recognizedText = ocrEngine.recognize(image);

        // Step 5: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### النتيجة المتوقعة

إذا كان `large-document.png` يحتوي على العبارة “Hello World”، سترى شيئًا مشابهًا:

```
=== OCR Result ===
Hello World
```

في حالة المسحات متعددة الصفحات سيكون الإخراج سلسلة واحدة مع فواصل أسطر (`\n`) تفصل كل سطر نصي.

---

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو كان PNG ضخمًا (مثلاً 10 000 × 10 000 بكسل)؟** | تقوم Aspose تلقائيًا بتقسيم الصورة إلى مربعات. يمكنك التحكم في حجم المربعات عبر `OcrEngine.setTileSize(int width, int height)` إذا احتجت تحكمًا أدق. |
| **هل يمكنني تحديد حد للذاكرة؟** | نعم — اضبط `ocrEngine.setMemoryLimit(long bytes)` لتجنب أخطاء OutOfMemory على الأجهزة منخفضة المواصفات. |
| **هل يعمل التوازي على Windows وLinux على حد سواء؟** | بالتأكيد. تجريد `ParallelSettings` يستخدم `ForkJoinPool` في Java، وهو متعدد المنصات. |
| **ما اللغات المدعومة؟** | أكثر من 100 لغة مدمجة. استخدم `ocrEngine.setLanguage("eng")` للإنجليزية، `"spa"` للإسبانية، إلخ. |
| **أريد فقط التعرف على الأرقام.** | استخدم `ocrEngine.setCharacterWhitelist("0123456789")` لتقييد مجموعة الأحرف. |

---

## نصائح لتجهيز OCR للإنتاج

1. **احتفظ بـ `OcrEngine` في الذاكرة** – إن إنشاءه مرارًا يضيف عبئًا. استخدم نمط Singleton إذا كنت تعالج العديد من الصور.  
2. **تحقق من صحة المدخلات** – افحص حجم الملف وأبعاده قبل إرساله إلى المحرك؛ الملفات الضخمة جدًا قد تُثقل JVM رغم التوازي.  
3. **ضبط مجموعة الخيوط** – إذا كان تطبيقك يشارك JVM مع خدمات أخرى، فكر في ضبط `parallelSettings.setMaxDegreeOfParallelism(Runtime.getRuntime().availableProcessors() / 2)` لتكون مواطنًا جيدًا.  
4. **المعالجة اللاحقة** – OCR ليس مثاليًا. استخدم مدقق إملائي أو تنظيف regex لتحسين الدقة، خاصةً للجداول الممسوحة.

---

## الخلاصة

غطّينا **كيفية تمكين OCR** في Java باستخدام Aspose، وأظهرنا **كيفية التعرف على النص من صورة**، وشرحنا **كيفية ضبط أقصى درجة للتوازي** لتسريع المعالجة، وبيّنّا **كيفية استخراج النص من PNG**، وأوضحنا الطريقة الصحيحة **لتحميل صورة للـ OCR**. الشيفرة الكاملة أعلاه جاهزة للتنفيذ، والمفاهيم تنطبق على أي مشروع Java يحتاج إلى استخراج نص سريع وموثوق.

هل أنت مستعد للخطوة التالية؟ جرّب معالجة مجلد كامل من PNGs، جرب حزم لغات مختلفة، أو صلّ ناتج OCR إلى فهرس بحث. السماء هي الحد عندما تتقن الأساسيات.

هل لديك أسئلة أو واجهت مشكلة؟ اترك تعليقًا، وسنساعدك على حلها معًا. برمجة سعيدة!  



![كيفية تمكين OCR illustration](https://example.com/placeholder-image.png "كيفية تمكين OCR في Java باستخدام Aspose")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}