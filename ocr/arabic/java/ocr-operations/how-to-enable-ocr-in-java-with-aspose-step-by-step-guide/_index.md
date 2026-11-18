---
category: general
date: 2026-04-26
description: تعلم كيفية تمكين التعرف الضوئي على الأحرف (OCR) في جافا باستخدام Aspose،
  تحميل الصورة للتعرف الضوئي على الأحرف، التعرف على المستند الممسوح ضوئياً وتفعيل
  المدقق الإملائي المدمج.
draft: false
keywords:
- how to enable OCR
- load image for OCR
- recognize scanned document
- aspose OCR Java tutorial
- built‑in spell corrector
language: ar
og_description: دليل خطوة بخطوة حول كيفية تمكين OCR في جافا، تحميل الصورة للـ OCR،
  التعرف على المستند الممسوح واستخدام المدقق الإملائي المدمج.
og_title: كيفية تمكين OCR في جافا باستخدام Aspose – دليل كامل
tags:
- Aspose
- OCR
- Java
- SpellCorrection
title: كيفية تمكين OCR في جافا باستخدام Aspose – دليل خطوة بخطوة
url: /ar/java/ocr-operations/how-to-enable-ocr-in-java-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين OCR في Java باستخدام Aspose – دليل كامل

هل تساءلت يومًا **how to enable OCR** في مشروع Java دون الحاجة إلى سحب مجموعة ضخمة من التبعيات؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى مسح صورة مشوشة، استخراج النص، والحصول على تهجئة مقبولة. في هذا الدليل سنستعرض خطوة بخطوة **how to enable OCR** باستخدام مكتبة Aspose OCR، تحميل صورة للـ OCR، وجعل المصحح الإملائي المدمج يقوم بسحره.

سنظهر لك أيضًا كيفية **recognize scanned document** المحتوى بشكل موثوق، حتى تتمكن من إدخال النتيجة مباشرةً في سير عملك. في النهاية، ستحصل على قطعة شفرة قابلة للتنفيذ، شرح واضح لكل سطر، وبعض النصائح الاحترافية لتجنب المشكلات الشائعة.

## ما ستحتاجه

- **Java 17** (أو أي JDK حديث؛ Aspose OCR يعمل مع Java 8+)
- **Aspose.OCR for Java** JAR (حمّلها من موقع Aspose أو أضفها عبر Maven)
- ملف صورة تجريبي (`scanned_doc.png`) يحتوي على النص الذي تريد استخراجَه
- بيئة التطوير المتكاملة المفضلة لديك (IntelliJ IDEA، Eclipse، VS Code… أيًا كان)

لا محركات OCR إضافية، ولا ملفات ثنائية أصلية—فقط مكتبة Aspose وصورة. بسيط، أليس كذلك؟

## كيفية تمكين OCR باستخدام Aspose OCR لـ Java

أول شيء تحتاج معرفته هو أن **how to enable OCR** في Aspose سهل مثل تبديل علم boolean في كائن `RecognitionSettings`. لنقّسم ذلك.

### الخطوة 1: إضافة Aspose OCR إلى مشروعك

إذا كنت تستخدم Maven، الصق هذا التبعيات في ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check the latest version on Aspose -->
</dependency>
```

> **نصيحة احترافية:** استخدم دائمًا أحدث نسخة مستقرة؛ الإصدارات الأحدث تحتوي على قواميس مخصصة للغات تحسن من المصحح الإملائي.

### الخطوة 2: إنشاء مثيل محرك OCR

إنشاء المحرك هو نقطة الدخول الخاصة بك. فكر فيه كالعقل الذي سيقرأ البكسلات لاحقًا ويحولها إلى أحرف.

```java
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

### الخطوة 3: تمكين المصحح الإملائي المدمج

استدعاء `setEnableSpellCorrection(true)` هو جوهر **how to enable OCR** مع مساعدة التهجئة. بدون ذلك، سيظل Aspose يقرأ النص، لكن أي خطأ إملائي ناتج عن ضوضاء الصورة سيبقى دون تعديل.

```java
// Step 3: Turn on spell correction (this is how you enable OCR spell‑checking)
ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);
```

### الخطوة 4: اختيار قاموس اللغة

توفير اللغة الصحيحة يضمن أن المصحح الإملائي المدمج يمتلك القاموس المناسب. إذا كنت تعالج اللغة الفرنسية، استبدل `ENGLISH` بـ `FRENCH`.

```java
// Step 4: Specify the language – here we use English
ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.ENGLISH);
```

### الخطوة 5: تحميل صورة للـ OCR

هذا السطر يجيب على سؤال **load image for OCR**. يمكنك أيضًا تمرير `java.io.File` أو `InputStream` إذا كانت صورتك مخزنة في قاعدة بيانات أو سحابة.

```java
// Step 5: Load the image you want to scan
ocrEngine.setImage("YOUR_DIRECTORY/scanned_doc.png");
```

### الخطوة 6: التعرف على المستند الممسوح واستخراج النص

عند استدعاء `recognize()`، يقوم Aspose بالعمل الشاق: يحلل البكسلات، يطبق نماذج اللغة، وأخيرًا يشغل المصحح الإملائي. النتيجة هي `String` نظيفة.

```java
// Step 6: Run the OCR process and get spell‑corrected output
String correctedText = ocrEngine.recognize().getText();
```

### الخطوة 7: عرض النتيجة

هذا كل شيء—سير عمل **recognize scanned document** الخاص بك اكتمل. لديك الآن سلسلة نصية تم تدقيقها إملائيًا جاهزة للفهرسة أو التخزين أو المعالجة الإضافية.

```java
// Step 7: Print the corrected OCR output
System.out.println("Corrected OCR output:\n" + correctedText);
```

## مثال كامل يعمل

فيما يلي البرنامج الكامل، جاهز للنسخ واللصق في ملف `SpellCorrectDemo.java`. يتضمن جميع الخطوات السابقة بالإضافة إلى بعض الفحوصات الوقائية.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable the built‑in spell‑corrector (how to enable OCR spell‑checking)
        ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);

        // 3️⃣ Set the language dictionary – English in this case
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.ENGLISH);

        // 4️⃣ Load the image you want to process (load image for OCR)
        String imagePath = "YOUR_DIRECTORY/scanned_doc.png";
        ocrEngine.setImage(imagePath);

        // 5️⃣ Run OCR and obtain the corrected text (recognize scanned document)
        String correctedText = ocrEngine.recognize().getText();

        // 6️⃣ Show the output
        System.out.println("Corrected OCR output:\n" + correctedText);
    }
}
```

### النتيجة المتوقعة

إذا كان `scanned_doc.png` يحتوي على العبارة *“Ths is a smple test.”* (لاحظ الحروف المفقودة)، سيطبع الطرفية:

```
Corrected OCR output:
This is a simple test.
```

المصحح الإملائي المدمج صحح الأخطاء تلقائيًا—بالضبط ما تتوقعه عندما تتبع **how to enable OCR** بشكل صحيح.

## فهم المصحح الإملائي المدمج

يعمل المصحح الإملائي على خوارزمية **المسافة ليفنشتاين القائمة على القاموس**. ببساطة، ينظر إلى كل كلمة تم التعرف عليها، يقارنها بأقرب مدخل في قاموس اللغة، ويستبدلها إذا كانت مسافة التحرير منخفضة بما يكفي. لهذا السبب اختيار `OcrLanguage` المناسب مهم؛ الخوارزمية تعرف فقط الكلمات الموجودة في ذلك القاموس.

> **حالة حافة:** إذا كان المستند يحتوي على العديد من الأسماء الخاصة (مثل أسماء العلامات التجارية)، قد يقوم المصحح “بتصحيح”ها بشكل غير صحيح. في مثل هذه الحالات، يمكنك تعطيل التدقيق الإملائي لتشغيل محدد:

```java
ocrEngine.getRecognitionSettings().setEnableSpellCorrection(false);
```

أو يمكنك تعزيز القاموس بتوفير قائمة كلمات مخصصة—شيء يدعمه Aspose عبر `addUserDictionary`.

## المشكلات الشائعة والنصائح الاحترافية

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **صورة غير واضحة تنتج نفايات** | دقة OCR تعتمد على جودة الصورة. | قم بالمعالجة المسبقة باستخدام مرشح تعزيز الحدة أو استخدم مسحًا بدقة أعلى. |
| **المصحح الإملائي يغيّر المصطلحات الخاصة بالمجال** | القاموس لا يحتوي على تلك المصطلحات. | أضفها إلى قاموس مستخدم مخصص (`ocrEngine.getRecognitionSettings().addUserDictionary("MyTerm")`). |
| **`FileNotFoundException` على `setImage`** | مسار خاطئ أو نقص في أذونات الملف. | استخدم مسارًا مطلقًا أو تحقق من أذونات القراءة؛ يمكنك أيضًا التحميل عبر `InputStream`. |
| **تأخر الأداء على ملفات PDF الكبيرة** | يعمل OCR على كل صفحة على التوالي. | قم بالتوازي بإنشاء عدة مثيلات `OcrEngine` (هي آمنة للخطوط المتعددة). |

## تحميل صور متعددة (متقدم)

إذا كنت بحاجة إلى **load image for OCR** على دفعات، فقط قم بالتكرار عبر قائمة:

```java
String[] images = {"page1.png", "page2.png", "page3.png"};
StringBuilder fullText = new StringBuilder();

for (String img : images) {
    ocrEngine.setImage(img);
    fullText.append(ocrEngine.recognize().getText()).append("\n");
}
System.out.println(fullText);
```

## نظرة بصرية

![لقطة شاشة مثال كيفية تمكين OCR](image-placeholder.png "مثال كيفية تمكين OCR")

*الصورة أعلاه توضح التدفق: تحميل صورة → تمكين المصحح الإملائي → التعرف → الإخراج.*

## ملخص: ما تم تغطيته

- **How to enable OCR** في Aspose عبر تبديل `setEnableSpellCorrection(true)`.
- الخطوات الدقيقة لـ **load image for OCR** وتحديد اللغة.
- كيفية **recognize scanned document** واستخراج النص المدقق إملائيًا.
- نظرة على **built‑in spell corrector** ومتى يجب تعديل إعداداته.
- كود Java كامل جاهز للنسخ واللصق مع معالجة حالات الحافة.

## ما التالي؟

الآن بعد أن أتقنت الأساسيات، فكر في استكشاف:

- مواضيع **aspose OCR Java tutorial** مثل OCR لملفات PDF متعددة الصفحات أو اكتشاف الباركود.
- دمج النتيجة مع **Apache Lucene** لإنشاء فهارس قابلة للبحث.
- استخدام **cloud storage** (AWS S3، Azure Blob) كمصدر لـ `setImage`.
- بناء خدمة REST صغيرة تقبل الصور وتعيد النص المصحح.

لا تتردد في التجربة—بدّل اللغات، قدّم ملاحظات مكتوبة يدويًا، أو اجمعها مع واجهة برمجة تطبيقات ترجمة اللغة. السماء هي الحد عندما تعرف **how to enable OCR** بشكل صحيح.

*برمجة سعيدة! إذا واجهت مشكلة، اترك تعليقًا أدناه وسنقوم بحلها معًا.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}