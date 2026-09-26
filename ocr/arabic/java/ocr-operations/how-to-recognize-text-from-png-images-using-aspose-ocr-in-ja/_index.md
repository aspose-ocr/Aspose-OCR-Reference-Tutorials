---
category: general
date: 2026-09-25
description: التعرف على النص من صور PNG باستخدام Aspose OCR في Java – دليل خطوة بخطوة
  لاستخراج النص من الصورة وتحويل الصورة إلى نص.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from png
- extract text from image
- convert image to text
- load image for ocr
- read english text image
language: ar
lastmod: 2026-09-25
og_description: التعرف على النص من صور PNG باستخدام Aspose OCR في Java. اتبع هذا الدليل
  لاستخراج النص من الصورة، تحويل الصورة إلى نص، وقراءة صورة النص الإنجليزي.
og_image_alt: Screenshot showing recognized text output after processing a PNG with
  Aspose OCR
og_title: التعرف على النص من صور PNG في جافا – دليل Aspose OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: recognize text from PNG images with Aspose OCR in Java – a step‑by‑step
    guide to extract text from image and convert image to text.
  headline: How to recognize text from PNG images using Aspose OCR in Java
  type: TechArticle
- description: recognize text from PNG images with Aspose OCR in Java – a step‑by‑step
    guide to extract text from image and convert image to text.
  name: How to recognize text from PNG images using Aspose OCR in Java
  steps:
  - name: Why each line matters
    text: '| Line | Purpose | How it helps you **extract text from image** | |------|---------|---------------------------------------------|
      | `new OcrEngine()` | Instantiates the OCR processor. | Provides the engine
      that performs character analysis. | | `engine.setImage(...)` | Loads the PNG
      file into memory'
  - name: 4.1 Missing or corrupt PNG file
    text: 'If the file path is wrong, `ImageStream.fromFile` throws an `IOException`.
      Wrap the loading code in a `try‑catch` block to present a friendly message:'
  - name: 4.2 Non‑English languages
    text: 'Aspose OCR supports many languages. To recognize French, for example, replace
      the language line with:'
  - name: 4.3 Low‑resolution PNGs
    text: OCR accuracy drops when the source image is below 300 dpi. If you notice
      poor results, consider preprocessing the PNG (e.g., scaling up with `java.awt.Image`)
      before passing it to the engine.
  type: HowTo
tags:
- Aspose OCR
- Java
- Image processing
title: كيفية التعرف على النص من صور PNG باستخدام Aspose OCR في Java
url: /ar/java/ocr-operations/how-to-recognize-text-from-png-images-using-aspose-ocr-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف على النص من صور PNG باستخدام Aspose OCR في Java

إذا كنت بحاجة إلى **التعرف على النص من ملفات PNG** في تطبيق Java، فإن هذا البرنامج التعليمي يوضح لك بالضبط كيفية القيام بذلك. بنهاية الدليل ستتمكن من **استخراج النص من الصورة**، تحويل الصورة إلى نص عادي، وعرض النتيجة في وحدة التحكم.

سنستخدم مكتبة Aspose OCR، التي توفر واجهة برمجة تطبيقات بسيطة لتحميل الصورة، اختيار اللغة، واسترجاع الأحرف المعترف بها. تغطي الخطوات أيضًا كيفية **تحميل الصورة للتعرف الضوئي على الأحرف** بأمان وما يجب فعله عندما يفشل المحرك. لا توجد خدمات خارجية مطلوبة، والكود يعمل على أي بيئة تشغيل Java 8+.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

* Java 8 أو أحدث مثبتة (JDK 8‑21 كلها مدعومة)
* Maven أو Gradle لإدارة التبعيات (سنظهر مقتطف Maven)
* ملف صورة باسم `sample.png` موجود في دليل يمكنك الإشارة إليه من الكود
* إلمام أساسي بصياغة Java وإدارة الاستثناءات

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

Aspose OCR موزعة كحزمة Maven. أضف التبعية التالية إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version available -->
</dependency>
```

إذا كنت تفضل Gradle، فإن المكافئ هو:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

إضافة المكتبة يمنحك الوصول إلى `OcrEngine` و`ImageStream` وتعدادات اللغات المطلوبة لـ **تحويل الصورة إلى نص**.

## الخطوة 2: إنشاء فئة Java واستيراد الحزم المطلوبة

أنشئ فئة جديدة تسمى `SampleDemo`. استورد فئات OCR وأي أدوات Java قياسية ستستخدمها.

```java
package com.example.ocrdemo;

import com.aspose.ocr.*;
import java.io.IOException;
```

سطر `import com.aspose.ocr.*;` يجلب كل ما يلزم لعمليات OCR، بينما سيساعدنا `java.io.IOException` في معالجة الأخطاء المتعلقة بالملفات.

## ## التعرف على النص من PNG باستخدام Aspose OCR

النواة الأساسية للحل تكمن في طريقة `main`. اتبع الخطوات المرقمة داخل الطريقة لترى كيف يعمل كل جزء.

```java
public class SampleDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image to be processed (load image for OCR)
        // Replace "YOUR_DIRECTORY" with the actual path to your PNG file.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));

        // Step 3: (Optional) Specify the language for recognition.
        // The default language is English, but we set it explicitly to
        // demonstrate how to read english text image.
        engine.setLanguage(OcrLanguage.English);

        // Step 4: Execute the OCR process
        if (engine.process()) {
            // Step 5: Retrieve and display the recognized text
            String text = engine.getText();
            System.out.println("Recognized text: " + text);
        } else {
            System.err.println("OCR processing failed.");
        }
    }
}
```

### لماذا كل سطر مهم

| السطر | الغرض | كيف يساعدك **استخراج النص من الصورة** |
|------|---------|---------------------------------------------|
| `new OcrEngine()` | ينشئ معالج OCR. | يوفر المحرك الذي يقوم بتحليل الأحرف. |
| `engine.setImage(...)` | يحمل ملف PNG في الذاكرة. | هذه هي خطوة **تحميل الصورة للتعرف الضوئي على الأحرف**؛ بدونها لا يملك المحرك ما يقرأه. |
| `engine.setLanguage(OcrLanguage.English)` | يخبر المحرك أي نموذج لغة يستخدم. | يضمن التعرف الدقيق لسيناريوهات **قراءة صورة نص إنجليزي**. |
| `engine.process()` | يشغل خوارزمية التعرف. | قلب **تحويل الصورة إلى نص** – يمرر البت ماب ويُنشئ سلسلة نصية. |
| `engine.getText()` | يُعيد الأحرف المعترف بها كسلسلة Java `String`. | يمنحك النتيجة النهائية للنص العادي الذي يمكنك تخزينه أو البحث فيه أو عرضه. |

## الخطوة 4: معالجة الحالات الشائعة

حتى تدفق OCR المكتوب جيدًا قد يواجه مشاكل. إليك بعض النصائح العملية.

### 4.1 ملف PNG مفقود أو تالف

إذا كان مسار الملف غير صحيح، فإن `ImageStream.fromFile` يطرح استثناء `IOException`. غلف كود التحميل داخل كتلة `try‑catch` لتقديم رسالة ودية:

```java
try {
    engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));
} catch (IOException e) {
    System.err.println("Unable to load image: " + e.getMessage());
    return;
}
```

### 4.2 لغات غير إنجليزية

يدعم Aspose OCR العديد من اللغات. للتعرف على الفرنسية، على سبيل المثال، استبدل سطر اللغة بـ:

```java
engine.setLanguage(OcrLanguage.French);
```

نفس النهج يعمل للغة الصينية، العربية، إلخ، مما يتيح لك **استخراج النص من الصورة** بغض النظر عن الخط.

### 4.3 PNG منخفض الدقة

تنخفض دقة OCR عندما تكون الصورة الأصلية أقل من 300 dpi. إذا لاحظت نتائج ضعيفة، فكر في معالجة PNG مسبقًا (مثل تكبيره باستخدام `java.awt.Image`) قبل تمريره إلى المحرك.

## الخطوة 5: التحقق من المخرجات

شغّل البرنامج من بيئة التطوير المتكاملة أو سطر الأوامر:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.SampleDemo"
```

من المفترض أن ترى شيئًا مثل:

```
Recognized text: Hello, world! This is a sample PNG image.
```

إذا طبع الطرفية `OCR processing failed.`، فتأكد من مسار الملف وتأكد من أن الصورة غير تالفة.

## نصائح إضافية للاستخدام في الإنتاج

* **المعالجة الدفعية** – كرر عبر دليل يحتوي على ملفات PNG، مع إعادة استخدام كائن `OcrEngine` واحد لتحسين الأداء.
* **إدارة الذاكرة** – استدعِ `engine.dispose()` بعد معالجة الصور الكبيرة لتحرير الموارد الأصلية.
* **التسجيل** – دمج إطار تسجيل (SLF4J، Log4j) بدلاً من `System.out` لتطبيقات قابلة للتوسع.
* **رموز الأخطاء** – `engine.process()` يُعيد `false` لأسباب متعددة؛ استخدم `engine.getErrorCode()` لتشخيص الفشل المحدد.

## الخلاصة

أنت الآن تعرف كيف **تتعرف على النص من صور PNG** في Java باستخدام Aspose OCR. سير العمل الكامل—**تحميل الصورة للتعرف الضوئي على الأحرف**، اختيار اللغة اختياريًا لـ **قراءة صورة نص إنجليزي**، **المعالجة**، و**استخراج النص من الصورة**—جاهز للتكامل مع أي مشروع Java. من هنا يمكنك توسيع الحل إلى **تحويل الصورة إلى نص** للملفات PDF، المستندات الممسوحة، أو تدفقات الكاميرا في الوقت الحقيقي.

## الخطوات التالية

* استكشف واجهة برمجة تطبيقات **تحويل الصورة إلى نص** لتنسيقات PDF أو TIFF.
* دمج تدفق OCR هذا مع Apache Tika لفهرسة النص المستخرج في محرك بحث.
* جرب الدعم متعدد اللغات عن طريق استبدال `OcrLanguage.English` بتعدادات لغات أخرى.
* اطلع على الإعدادات المتقدمة لـ Aspose OCR (مثل `engine.setPreprocessOptions`) لتحسين الدقة على PNG ذات الضوضاء.

برمجة سعيدة، واستمتع بتحويل الصور إلى نص قابل للبحث!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [Recognize Text from Image with Aspose OCR – Full Java Guide](/ocr/english/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)
- [recognize text image using Aspose OCR GPU – Java](/ocr/english/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}