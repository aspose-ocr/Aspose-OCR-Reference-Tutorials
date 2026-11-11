---
category: general
date: 2026-08-18
description: كيفية تمكين وحدة معالجة الرسومات (GPU) للتعرف الضوئي على الحروف (OCR)
  في جافا والتعرف بسرعة على نص الصورة، استخراج نص JPG، إضافة فلتر، وتعيين اللغة باستخدام
  Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: ar
lastmod: 2026-08-18
og_description: كيفية تمكين وحدة معالجة الرسومات (GPU) لتقنية التعرف الضوئي على الأحرف
  (OCR) في جافا والتعرف فورًا على نص الصورة، استخراج النص من ملف JPG، إضافة فلتر،
  وتعيين اللغة باستخدام Aspose.OCR.
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: كيفية تمكين GPU للتعرف الضوئي على الأحرف (OCR) في Java – دليل Aspose.OCR
  الكامل
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: كيفية تمكين GPU للتعرف الضوئي على الحروف (OCR) في جافا باستخدام Aspose.OCR
url: /ar/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين وحدة معالجة الرسومات (GPU) للتعرف الضوئي على الأحرف (OCR) في جافا باستخدام Aspose.OCR

إذا كنت بحاجة إلى **كيفية تمكين GPU** للتعرف الضوئي على الأحرف في جافا، فإن هذا الدليل يوضح لك الخطوات الدقيقة. تمكين تسريع GPU يتيح لك **التعرف على نص الصورة** بسرعة أكبر بضع مرات، وهو أمر أساسي عندما تحتاج إلى **استخراج نص من ملفات JPG** بالجملة. سنغطي أيضًا **كيفية إضافة مرشح**، **كيفية تعيين اللغة**، وكيفية استرجاع النتيجة النهائية.

في نهاية هذا الدرس ستحصل على برنامج كامل قابل للتنفيذ يحتوي على:

* يبدأ محرك Aspose.OCR بدعم GPU.  
* يضبط لغة OCR (مثال: الإنجليزية).  
* يطبق مرشح إزالة الضوضاء لتحسين الدقة.  
* يحمل صورة JPEG، ينفذ التعرف، ويطبع النص المستخرج.

> **المتطلبات المسبقة:** Java 17 أو أحدث، Maven، ورخصة Aspose.OCR لجافا (الإصدار التجريبي المجاني يعمل للتقييم).

![How to enable GPU for OCR in Java](/images/ocr-gpu.png){alt="كيفية تمكين GPU للتعرف الضوئي على الأحرف في جافا"}

## ما ستحتاجه

| العنصر | السبب |
|------|--------|
| **Java Development Kit (JDK) 17+** | مطلوب لتجميع وتشغيل المثال. |
| **Maven** | يبسط إدارة التبعيات لـ Aspose.OCR. |
| **Aspose.OCR for Java** | يوفر الفئة `OcrEngine` ودعم GPU. |
| **A sample JPEG image** (`sample.jpg`) | يُستخدم لتوضيح **استخراج نص JPG**. |
| **GPU‑compatible hardware** (optional but recommended) | يُمكّن تعزيز الأداء الذي سنقوم بتكوينه. |

## الخطوة 1: إعداد مشروع Maven

أنشئ مشروع Maven جديد (أو أضف إلى مشروع موجود) وضمن تبعية Aspose.OCR:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **نصيحة احترافية:** حافظ على تحديث رقم الإصدار؛ الإصدارات الأحدث تحسن معالجة GPU وتضيف حزم اللغات.

## الخطوة 2: تهيئة محرك OCR و **كيفية تمكين GPU**

جوهر الحل هو `OcrEngine`. إنشاء نسخة منه سهل، لكن يجب عليك تشغيل تسريع GPU صراحةً:

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**لماذا تمكين GPU؟**  
عند استدعاء `setUseGpu(true)`, تقوم Aspose.OCR بتحميل نوى معالجة الصور الثقيلة إلى بطاقة الرسومات. على بطاقة NVIDIA/AMD حديثة، يمكن أن تزداد سرعة التعرف من ~200 ms لكل صفحة إلى < 80 ms، مما يقلل بشكل كبير من الوقت الإجمالي للمعالجة للدفعات الكبيرة.

## الخطوة 3: **كيفية تعيين اللغة** و **كيفية إضافة مرشح**

### 3.1 تعيين لغة OCR

تأتي Aspose.OCR مع حزم لغات لأكثر من 100 لغة. استبدل `ENGLISH` بـ `FRENCH` أو `CHINESE_SIMPLIFIED`، إلخ، لتتناسب مع المادة المصدرية.

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

### 3.2 إضافة مرشح ما قبل المعالجة

الضوضاء، أو عيوب الضغط، أو الإضاءة غير المتساوية يمكن أن تضر بالدقة. إضافة مرشح إزالة الضوضاء هو النهج المعتاد **كيفية إضافة مرشح**:

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

تشمل الفلاتر المفيدة الأخرى `FilterType.CONTRAST` و `FilterType.BRIGHTNESS` و `FilterType.BINARIZE`. يمكنك ربط عدة فلاتر عن طريق استدعاء `addPreprocessFilter` بشكل متكرر.

## الخطوة 4: تحميل الصورة – **استخراج نص JPG**

الآن نوجه المحرك إلى ملف JPEG الذي نريد معالجته:

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

استبدل `YOUR_DIRECTORY` بالمسار الفعلي حيث يوجد `sample.jpg`. تدعم Aspose.OCR أيضًا PNG و BMP و TIFF و PDF؛ نفس الاستدعاء يعمل لتلك الصيغ.

## الخطوة 5: تنفيذ OCR و **التعرف على نص الصورة**

مع تكوين المحرك، استدعِ روتين التعرف:

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

طريقة `recognize()` تعالج الصورة على GPU (إذا كان مفعلاً) وتملأ المخزن الداخلي للنص. `getText()` تُرجع `String` نصًا عاديًا، يمكنك كتابته إلى ملف، قاعدة بيانات، أو تمريره إلى خطوط معالجة اللغة الطبيعية اللاحقة.

### النتيجة المتوقعة

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

## الخطوة 6: التحقق من استخدام GPU (اختياري)

لتأكيد أن GPU يُستخدم فعليًا، فعّل تسجيل Aspose:

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

افحص `ocr-debug.log` بعد تشغيل؛ يجب أن ترى سجلات مثل `GPU device: NVIDIA GeForce RTX 3080` و `Processing time (GPU): 78 ms`. إذا ذكر السجل **CPU**، فتحقق من تثبيت برنامج التشغيل وتأكد من وجود استدعاء `setUseGpu(true)`.

## الأخطاء الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | مكتبات GPU الأصلية مفقودة | ثبت أحدث برنامج تشغيل GPU وتأكد من وجود ملفات `aspose-ocr` الأصلية في `java.library.path`. |
| **ضعف الدقة في الصور الداكنة** | عدم وجود مرشح ما قبل المعالجة | أضف `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` أو زد `FilterType.CONTRAST`. |
| **`OutOfMemoryError` على دفعات كبيرة** | نفاد ذاكرة GPU | عالج الصور على دفعات أصغر أو عطل GPU (`engine.setUseGpu(false)`) للصور ذات الدقة العالية جدًا. |
| **إخراج لغة غير صحيح** | تعيين لغة خاطئ | تحقق من أن `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` يتطابق مع النص المصدر. |

## مثال كامل قابل للتنفيذ

فيما يلي الفئة Java الكاملة التي يمكنك نسخها ولصقها في `src/main/java/com/example/HelloWorldOcr.java`. تتضمن جميع الخطوات، معالجة الأخطاء، وتسجيل اختياري.

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

**تشغيل البرنامج**

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

يجب أن ترى النص المعترف به يُطبع على وحدة التحكم ويُحفظ في `output.txt`. ملف `ocr-debug.log` سيؤكد استخدام GPU.

## الخلاصة

في هذا الدرس أظهرنا **كيفية تمكين GPU** لـ Aspose.OCR في جافا، وكيفية **التعرف على نص الصورة**، **استخراج نص JPG**، **كيفية إضافة مرشح**، و**كيفية تعيين اللغة**—كل ذلك في برنامج واحد مستقل. بتمكين GPU تحصل على زيادة كبيرة في السرعة، بينما تضمن الفلاتر وإعدادات اللغة دقة عالية عبر مصادر الصور المتنوعة.

**الخطوات التالية**

* جرب فلاتر إضافية مثل `FilterType.BINARIZE` للمستندات الممسوحة.  
* انتقل إلى لغات أخرى (`OcrLanguage.SPANISH`, `OcrLanguage.CHINESE_SIMPLIFIED`) لتوسيع الدعم متعدد اللغات.  
* ادمج خط أنابيب OCR هذا مع Apache PDFBox لاستخراج النص مباشرةً من صفحات PDF.  

لا تتردد في تعديل الكود للمعالجة الدفعية، دمجه في خدمة Spring Boot، أو ربطه مع طابور رسائل لمعالجة OCR في الوقت الفعلي. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية قراءة النص من صورة في جافا باستخدام Aspose OCR – دليل كامل](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [كيفية التعرف على نص الصورة باستخدام اللغة مع Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [معالجة صورة OCR مسبقًا في جافا باستخدام Aspose OCR – تحسين الدقة واستخراج النص](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}