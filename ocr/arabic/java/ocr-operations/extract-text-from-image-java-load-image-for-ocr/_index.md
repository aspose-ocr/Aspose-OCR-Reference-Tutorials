---
category: general
date: 2026-04-29
description: استخراج النص من صورة باستخدام جافا و Aspose OCR – تعلم كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف وتعرف النص من الإيصال بصيغة JSON.
draft: false
keywords:
- extract text from image java
- load image for OCR
- recognize text from receipt
- Aspose OCR Java
- JSON OCR result
language: ar
og_description: استخراج النص من صورة باستخدام جافا و Aspose OCR. يوضح هذا الدرس كيفية
  تحميل الصورة للتعرف الضوئي على الأحرف وتحديد النص من الإيصال، وإخراج JSON.
og_title: استخراج النص من الصورة باستخدام جافا – دليل كامل
tags:
- Java
- OCR
- Aspose
title: استخراج النص من صورة جافا – تحميل الصورة للتعرف الضوئي على الأحرف
url: /ar/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة java – دليل كامل

هل احتجت يومًا إلى **extract text from image java** لكن لم تكن متأكدًا من المكتبة التي تختارها؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحاولون **load image for OCR** ثم يحصلون على النص الخام في صيغة يصعب التعامل معها.  

في هذا الدرس سنستعرض حلًا نظيفًا من البداية إلى النهاية لا يقتصر فقط على **load image for OCR** بل أيضًا على **recognize text from receipt** ويُخرج سلسلة JSON مرتبة. بنهاية الدرس ستحصل على فئة Java جاهزة للتشغيل يمكنك إدراجها في أي مشروع—بدون أي تعديل إضافي.

## ما ستتعلمه

- كيفية إعداد Aspose OCR للـ Java (المكتبة التي تجعل العمل الشاق سهلًا).  
- الخطوات الدقيقة لـ **load image for OCR** من القرص.  
- كيفية تكوين المحرك لإرجاع النتائج بصيغة JSON، وهو مثالي للمعالجة اللاحقة.  
- كيفية **recognize text from receipt** للصور والتحقق من النتيجة.  

لا تحتاج إلى خبرة سابقة مع Aspose؛ فقط JDK يعمل وIDE تشعر بالراحة في استخدامها.

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| **Java 17+** (or any recent JDK) | تأتي Aspose OCR مع ملفات تنفيذية مُجمَّعة لتشغيلات Java الحديثة. |
| **Maven or Gradle** (to pull the Aspose OCR dependency) | يسهل إدارة الاعتمادات. |
| **A sample receipt image** (e.g., `receipt.png`) | سنستخدم هذا الملف لتوضيح **recognize text from receipt**. |
| **Internet connection** (once) | مطلوب لتنزيل ملف Aspose JAR في المرة الأولى. |

إذا كان لديك هذه المتطلبات بالفعل، عظيم—لنبدأ.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

أول شيء تحتاجه هو مكتبة Aspose OCR. إذا كنت تستخدم Maven، أضف المقتطف التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

بالنسبة لـ Gradle، يبدو هكذا:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **نصيحة احترافية:** قم بتثبيت رقم الإصدار. التحديث لاحقًا قد يُدخل تغييرات دقيقة في API قد تُكسر كودك.

بعد حل الاعتمادية، ستكون جاهزًا لكتابة كود Java الذي يقوم فعليًا بـ **extract text from image java**.

## الخطوة 2: تحميل الصورة لـ OCR

الآن سنعرض السطر الدقيق الذي يقوم بـ **load image for OCR**. توفر Aspose أداة مساعدة `ImageStream.fromFile` مريحة.

```java
// Step 2: Load the image you want to process
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي لملف الإيصال الخاص بك. إذا كان المسار غير صحيح، سيُطلق المحرك استثناء `FileNotFoundException`، لذا تحقق من الإملاء.

> **لماذا هذا مهم:** تحميل الصورة بشكل صحيح هو الأساس. إذا لم تُقرأ الصورة، لن يكون لدى محرك OCR ما يتعرف عليه، وستحصل على نتيجة JSON فارغة.

## الخطوة 3: إخبار المحرك بإرجاع JSON

يمكن لـ Aspose OCR إنتاج XML أو نص عادي أو JSON. بالنسبة لواجهات برمجة التطبيقات الحديثة، JSON هو الأكثر مرونة، لذا سنحدد الصيغة صراحةً.

```java
ocrEngine.getResultSettings()
         .setResultFormat(OcrResultFormat.JSON); // XML is also available
```

يمكنك التحويل إلى `OcrResultFormat.XML` بتعديل واحد إذا كان نظامك اللاحق يفضّل XML. تم تصميم API لتكون قابلة للتبديل.

## الخطوة 4: تشغيل عملية التعرف

بعد تحميل الصورة وتحديد الصيغة، الخطوة التالية هي فعليًا **recognize text from receipt**. هنا يحدث العمل الشاق.

```java
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.recognize();
```

يُعرقل استدعاء `recognize()` حتى ينتهي المحرك من تحليل الصورة. بالنسبة للصور الكبيرة قد ترغب في تشغيله في خيط خلفي، لكن بالنسبة لإيصال عادي يكتمل خلال جزء من الثانية.

## الخطوة 5: الحصول على نتيجة JSON

أخيرًا، نستخرج سلسلة JSON الخام ونطبعها. تحتوي هذه السلسلة على كل قطعة من النص المعترف به، ومربع الحد، ودرجات الثقة، وأكثر.

```java
// Step 5: Retrieve the JSON string
String jsonResult = ocrResult.getResultAsString();
System.out.println(jsonResult);
```

### النتيجة المتوقعة

تشغيل البرنامج الكامل على إيصال واضح ينتج شيئًا مثل:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "rectangle": { "x": 12, "y": 15, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2026-04-28",
          "confidence": 0.95,
          "rectangle": { "x": 12, "y": 50, "width": 180, "height": 20 }
        },
        {
          "text": "Total $23.45",
          "confidence": 0.99,
          "rectangle": { "x": 12, "y": 120, "width": 150, "height": 25 }
        }
      ]
    }
  ]
}
```

لاحظ كيف أن كل سطر من الإيصال هو كتلة منفصلة مع درجة ثقة. يمكنك الآن تمرير هذا JSON إلى أي نظام لاحق—تخزينه في قاعدة بيانات، إرساله عبر HTTP، أو إرساله إلى نموذج تعلم آلي.

## مثال كامل يعمل

فيما يلي الفئة الكاملة المستقلة في Java التي تجمع كل شيء معًا. انسخها وألصقها، عدل مسار الصورة، وشغّل `mvn compile exec:java` (أو الأمر المكافئ في Gradle).

```java
import com.aspose.ocr.*;

public class JsonExportExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Make sure the path points to a real receipt image on your machine
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Configure the engine to return results in JSON format
        ocrEngine.getResultSettings()
                 .setResultFormat(OcrResultFormat.JSON); // XML is also available

        // Step 4: Run the OCR recognition process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Retrieve the raw JSON string and output it
        String jsonResult = ocrResult.getResultAsString();
        System.out.println(jsonResult);
    }
}
```

> **احذر من:**  
> • **أخطاء مسار الملف** – تحقق مرة أخرى من الشرطات في Windows مقابل macOS/Linux.  
> • **نفاد الذاكرة** – قد تحتاج الصور الكبيرة إلى `ocrEngine.setMemoryOptimization(true)`.  
> • **إعدادات اللغة** – إذا كان الإيصال يحتوي على أحرف غير لاتينية، استدعِ `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (أو أي لغة مدعومة) قبل `recognize()`.

## اختبار الحل

1. **شغّل البرنامج** – يجب أن ترى كتلة JSON مطبوعة في وحدة التحكم.  
2. **تحقق من صحة JSON** – انسخ النتيجة إلى <https://jsonlint.com/> للتأكد من أنها صالحة.  
3. **قم بتحليلها** – في مشروع حقيقي ستستخدم مكتبة مثل Jackson أو Gson لتحويل JSON إلى كائنات POJO لتسهيل المعالجة.

إذا واجهت مصفوفة `pages` فارغة، فإن أكثر الأسباب شيوعًا هي: عدم العثور على ملف الصورة، أو أن الصورة غير واضحة بما يكفي لإعدادات المحرك الافتراضية. في الحالة الأخيرة، حاول زيادة DPI أو تطبيق خطوة ما قبل المعالجة (مثل التحويل إلى ثنائي) قبل إمداده إلى Aspose.

## التغييرات والحالات الخاصة

| السيناريو | ما الذي يجب تغييره |
|----------|----------------|
| **Multiple pages** (e.g., multi‑page PDF converted to images) | تكرار على كل صورة، استدعِ `ocrEngine.setImage(...)` داخل الحلقة، وجمع نتائج JSON. |
| **Different output format** | استبدل `OcrResultFormat.JSON` بـ `OcrResultFormat.XML` أو `OcrResultFormat.PLAIN_TEXT`. |
| **Performance tuning** | استخدم `ocrEngine.setRecognitionMode(OcrRecognitionMode.FAST)` للسرعة، أو `OcrRecognitionMode.ACCURATE` للجودة. |
| **Non‑receipt documents** | اضبط `ocrEngine.getPageSegmentationSettings().setDetectTables(true)` إذا كنت تحتاج إلى استخراج الجداول. |

## الخلاصة

لقد استعرضنا للتو طريقة مختصرة وجاهزة للإنتاج لـ **extract text from image java** باستخدام Aspose OCR. باتباع الخطوات الخمس—إنشاء المحرك، **load image for OCR**، ضبط إخراج JSON، **recognize text from receipt**، وأخيرًا قراءة JSON—يمكنك دمج OCR في أي خلفية Java بأقل جهد.

من هنا قد ترغب في:

- تخزين JSON في قاعدة بيانات NoSQL للتحليلات المستقبلية.  
- تمرير النتيجة إلى روبوت محادثة يجيب على أسئلة حول الإيصالات.  
- دمج ذلك مع Apache Tika لمعالجة ملفات PDF، DOCX، وغيرها من الصيغ.

جرّبه، عدّل الإعدادات لتتناسب مع مستنداتك الخاصة، ودع الآلة تقوم بالعمل الشاق بينما تركز أنت على إضافة القيمة.

![استخراج النص من صورة java](placeholder-image.png "استخراج النص من صورة java")

*الشكل: تمثيل بصري لأنبوب OCR – من ملف الصورة إلى إخراج JSON.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}