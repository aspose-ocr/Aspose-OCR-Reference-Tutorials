---
category: general
date: 2026-07-05
description: دورة تعليمية للتعرف الضوئي على الأحرف (OCR) متعدد اللغات لمطوري جافا.
  تعلم كيفية استخراج نص OCR من الصور إلى مشاريع جافا النصية باستخدام مثال OCR متعدد
  اللغات.
draft: false
keywords:
- mixed language OCR
- get OCR text
- image to text Java
- java OCR example
- multi language OCR
language: ar
og_description: شرح OCR متعدد اللغات في جافا. احصل على نص OCR من الصور باستخدام مثال
  OCR متعدد اللغات يمكنك نسخه ولصقه اليوم.
og_title: التعرف الضوئي على الأحرف متعدد اللغات في جافا – دليل برمجي شامل
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  headline: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  name: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Create a Maven Project
    text: 'Open a terminal and run:'
  - name: 2. Add the Aspose.OCR Dependency
    text: 'Edit the generated `pom.xml` and insert the following inside the `<dependencies>`
      block:'
  - name: How It Works
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **1** | `OcrEngine` object is created. | The engine encapsulates all OCR functionality;
      without it you can’t call any methods. | | **2** | `setRecognitionLanguage`
      receives `ENGLISH` and `MALAYALAM`. | Supplying both'
  - name: Low‑Quality Images
    text: 'If the image is blurry or has poor contrast, OCR accuracy drops dramatically.
      Consider these remedies:'
  - name: Unsupported Languages
    text: Aspose currently supports over 70 scripts, but Malayalam may require a language
      pack. If `RecognitionLanguage.MALAYALAM` throws an exception, download the additional
      language data from Aspose’s portal and place it in `resources/ocr-data`.
  - name: Large PDFs
    text: When processing multi‑page PDFs, feed each page as a separate image or use
      `OcrEngine.recognizePdf`. The same `setRecognitionLanguage` call applies to
      every page, giving you a seamless **multi language OCR** experience across a
      whole document.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: التعرف الضوئي على الأحرف متعدد اللغات في جافا – دليل كامل خطوة بخطوة
url: /ar/java/advanced-ocr-techniques/mixed-language-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف الضوئي على الأحرف (OCR) متعدد اللغات في جافا – دليل خطوة بخطوة كامل

هل احتجت يومًا إلى **mixed language OCR** لكن لم تكن متأكدًا من كيفية تحقيق ذلك في جافا؟ لست وحدك. سواءً كنت تقوم برقمنة مستندات قديمة تتنقل بين الإنجليزية والمالايالام، أو تبني تطبيق ماسح يدعم عدة خطوط، فإن التحدي حقيقي. في هذا الدرس سنوضح لك بالضبط كيف **get OCR text** من صورة bitmap تحتوي على اللغتين، باستخدام سير عمل **image to text Java** مختصر.

سنستعرض مثال **java OCR example** جاهز للتنفيذ، نشرح لماذا كل سطر مهم، ونغطي خصوصيات **multi language OCR** حتى تتجنب المشكلات الشائعة. في النهاية ستحصل على برنامج يعمل ويطبع النص المستخرج على وحدة التحكم – دون أي مكتبات غامضة غير مفسرة.

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي على جهازك:

* **Java Development Kit (JDK) 17** أو أحدث – يستخدم الكود نظام الوحدات الحديث لكنه يعمل أيضًا على JDK 11+.  
* **Maven** (أو Gradle) – لجلب مكتبة OCR تلقائيًا.  
* محرك OCR يدعم عدة لغات – في هذا الدليل سنستخدم **Aspose.OCR for Java**، الذي يوفر دعمًا جاهزًا للإنجليزية والمالايالام. (إذا كنت تفضّل Tesseract، الخطوات مشابهة؛ فقط استبدل عبارات الاستيراد.)  
* صورة نموذجية باسم `mixed_english_malayalam.png` موجودة في مجلد يسمى `resources` داخل مشروعك.  
* قدر بسيط من الفضول – البقية مغطاة أدناه.

> **نصيحة احترافية:** إذا كنت على نظام Windows، نفّذ `mvn -v` من موجه الأوامر للتحقق من أن Maven موجود في PATH.

## إعداد المشروع

### 1. إنشاء مشروع Maven

افتح الطرفية ونفّذ:

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=mixed-ocr-demo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

هذا يُنشئ مشروع جافا أساسي بتخطيط `src/main/java` القياسي.

### 2. إضافة تبعية Aspose.OCR

حرّر ملف `pom.xml` المُولد وأدرج التالي داخل كتلة `<dependencies>`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of July 2026 -->
</dependency>
```

نفّذ `mvn clean install` لتحميل ملفات JAR. سيتولى Maven كل شيء، ولن تحتاج إلى البحث عن ملفات DLL الأصلية.

## كتابة كود OCR متعدد اللغات

أنشئ فئة جديدة باسم `MixedLanguageOcrDemo.java` داخل `src/main/java/com/example/ocr/` والصق الكود الكامل أدناه. كل سطر مُعلّق لتعرف **why** نقوم بذلك.

```java
package com.example.ocr;

import com.aspose.ocr.*;
import com.aspose.ocr.recognition.*;

public class MixedLanguageOcrDemo {

    public static void main(String[] args) {
        // Step 1: Initialise the OCR engine – this is the entry point for all operations.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Tell the engine which languages to look for.
        // We pass both English and Malayalam; the engine will automatically switch
        // between scripts as it encounters them.
        ocrEngine.setRecognitionLanguage(
                RecognitionLanguage.ENGLISH,
                RecognitionLanguage.MALAYALAM);

        // Step 3: Load the image that contains mixed text.
        // Using a relative path keeps the example portable across machines.
        String imagePath = "resources/mixed_english_malayalam.png";

        // Optional: improve accuracy on low‑resolution scans.
        // Uncomment the next line if your image is under 300 DPI.
        // ocrEngine.setResolution(300);

        // Step 4: Perform the actual OCR operation.
        RecognitionResult result = ocrEngine.recognizeImage(imagePath);

        // Step 5: Extract the plain text – this is the "get OCR text" part.
        String extractedText = result.getText();

        // Step 6: Output the result to the console.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

### كيف يعمل

| الخطوة | ما يحدث | لماذا يهم |
|--------|----------|-----------|
| **1** | يتم إنشاء كائن `OcrEngine`. | المحرك يضم جميع وظائف OCR؛ بدون هذا لا يمكنك استدعاء أي طريقة. |
| **2** | `setRecognitionLanguage` يستقبل `ENGLISH` و `MALAYALAM`. | توفير اللغتين يفعّل **multi language OCR**؛ سيكتشف المحرك تغيّر الخطوط أثناء المعالجة. |
| **3** | يتم تعريف مسار الصورة. | الحفاظ على المسار نسبيًا يجنب الترميز الصلب للمواقع، مما يجعل **java OCR example** قابلًا لإعادة الاستخدام. |
| **4** | `recognizeImage` يعالج الـ bitmap. | هنا يتم العمل الشاق – يحلل المحرك البكسلات، يشغّل الشبكات العصبية، ويعيد `RecognitionResult`. |
| **5** | `getText()` يستخرج السلسلة النصية العادية. | هذه هي الطريقة التي تحتاجها **get OCR text** للمعالجة اللاحقة (مثل الحفظ في قاعدة بيانات). |
| **6** | `System.out.println` يطبع السلسلة. | رد الفعل البصري الفوري يساعدك على التحقق من أن خط أنابيب **image to text Java** يعمل. |

> **ملاحظة:** إذا صادفت الخطأ `java.lang.UnsatisfiedLinkError`، تأكد من أن مجلد المكتبة الأصلية موجود في `java.library.path`. تُوفر Aspose الثنائيات المطلوبة لأنظمة Windows و macOS و Linux.

## تشغيل النموذج التجريبي

قم بالترجمة والتنفيذ باستخدام Maven:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.MixedLanguageOcrDemo"
```

يجب أن ترى مخرجات مشابهة لـ:

```
=== Extracted Text ===
Welcome to the conference.
സ്വാഗതം
```

السطر الأول بالإنجليزية، والسطر الثاني بالمالايالام – دليل على نجاح **mixed language OCR**.

## التعامل مع الحالات الشائعة

### صور منخفضة الجودة

إذا كانت الصورة غير واضحة أو ذات تباين ضعيف، تنخفض دقة OCR بشكل كبير. ضع في اعتبارك هذه الحلول:

* **Pre‑process** الصورة باستخدام مكتبة مثل OpenCV – حوّلها إلى تدرج رمادي، طبّق عتبة تكيفية، وزد الدقة إلى ما لا يقل عن 300 DPI.  
* فعّل `ocrEngine.setAutoSkewCorrection(true)` لتسمح للمحرك بتصحيح النص المائل.  
* زد قيمة `ocrEngine.setConfidenceThreshold(0.6f)` إذا كنت تحتاج إلى تصفية أكثر صرامة للثقة.

### لغات غير مدعومة

تدعم Aspose حاليًا أكثر من 70 خطًا، لكن قد تحتاج إلى حزمة لغة للمالايالام. إذا ألقى `RecognitionLanguage.MALAYALAM` استثناءً، حمّل بيانات اللغة الإضافية من بوابة Aspose وضعها في `resources/ocr-data`.

### ملفات PDF كبيرة

عند معالجة ملفات PDF متعددة الصفحات، قدم كل صفحة كصورة منفصلة أو استخدم `OcrEngine.recognizePdf`. نفس استدعاء `setRecognitionLanguage` يُطبق على كل صفحة، مما يمنحك تجربة **multi language OCR** سلسة عبر المستند بأكمله.

## توسيع المثال: من وحدة التحكم إلى خدمة ويب

إذا رغبت في إتاحة هذه الوظيفة عبر نقطة نهاية REST، أضف Spring Boot:

```java
@RestController
@RequestMapping("/api/ocr")
public class OcrController {

    @PostMapping(value = "/extract", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
    public String extractText(@RequestParam("file") MultipartFile file) throws IOException {
        OcrEngine engine = new OcrEngine();
        engine.setRecognitionLanguage(RecognitionLanguage.ENGLISH, RecognitionLanguage.MALAYALM);
        // Save multipart file to a temporary location
        Path temp = Files.createTempFile("upload-", ".png");
        Files.write(temp, file.getBytes());
        RecognitionResult res = engine.recognizeImage(temp.toString());
        return res.getText();
    }
}
```

الآن يمكن لأي عميل `POST` صورة وتلقي نتيجة **get OCR text** كـ JSON عادي. يُظهر هذا التوسيع الصغير كيف يمكن لنفس **java OCR example** أن يتطور من عرض ملف واحد إلى خدمة جاهزة للإنتاج.

## لقطة شجرة المصدر الكاملة

```
mixed-ocr-demo/
├─ pom.xml
└─ src/
   └─ main/
      ├─ java/
      │  └─ com/example/ocr/
      │     └─ MixedLanguageOcrDemo.java
      └─ resources/
         └─ mixed_english_malayalam.png
```

وجود هيكل المشروع بالكامل في المقال يسهل على القرّاء نسخ البنية إلى بيئتهم المتكاملة وتشغيلها فورًا.

![mixed language OCR example output](https://example.com/assets/mixed-ocr-output.png "mixed language OCR example output")

*نص بديل للصورة:* مثال ناتج OCR متعدد اللغات – يُظهر النص الإنجليزي والمالايالام المستخرج من نفس الصورة.

## ملخص وخطوات مستقبلية

غطّينا خط أنابيب **mixed language OCR** في جافا من البداية حتى النهاية:

* إعداد مشروع Maven وإضافة تبعية Aspose OCR.  
* تكوين المحرك للإنجليزية + المالايالام، إجراء التعرف، و**got OCR text**.  
* مناقشة جودة الصورة، حزم اللغات، وكيفية تحويل تطبيق وحدة التحكم إلى خدمة ويب.

إذا كنت مستعدًا للمتابعة، جرّب الأفكار التالية:

* استبدل Aspose بـ **Tesseract** لترى كيف يتعامل محرك مفتوح المصدر مع **multi language OCR**.  
* جرّب لغات إضافية مثل الهندية أو التاميلية – فقط أضفها إلى `setRecognitionLanguage`.  
* دمج النتيجة مع فهرس بحث (مثل Elasticsearch) لتمكين بحث **image to text Java** عبر الأرشيفات الممسوحة.

لا تتردد في ترك تعليق إذا واجهت أي مشكلة، أو مشاركة تعديلاتك الخاصة. برمجة سعيدة، ولتكن مسحاتك دائمًا واضحة كالكريستال!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}