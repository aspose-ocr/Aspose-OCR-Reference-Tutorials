---
category: general
date: 2026-06-06
description: استخراج النص من الصورة الممسوحة ضوئياً باستخدام Aspose OCR للغة جافا.
  تعلم كيفية التعرف على النص من ملفات TIFF باستخدام المعالجة المتوازية.
draft: false
keywords:
- extract text from scanned image
- recognize text from tiff
- Aspose OCR Java tutorial
- parallel OCR processing
- Java image recognition
language: ar
og_description: استخراج النص من صورة ممسوحة ضوئياً باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية التعرف على النص من ملفات TIFF بكفاءة باستخدام Java.
og_title: استخراج النص من صورة ممسوحة ضوئياً – دليل Aspose OCR للغة Java
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  headline: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  type: TechArticle
- description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  name: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  steps:
  - name: Maven users
    text: 'Add the following dependency to your `pom.xml`:'
  - name: Manual JAR setup
    text: Download the latest `aspose-ocr-xx.jar` from the Aspose website and place
      it on your classpath.
  - name: Expected Output
    text: '``` === Extracted Text === Invoice Number: 12345 Date: 2024‑05‑01 Total:
      $1,250.00 ... ```'
  - name: What’s Next?
    text: '- **Batch processing**: Loop over a directory of TIFFs, store each result
      in its own file. - **Integrate with Elasticsearch**: Index the extracted text
      for fast full‑text search. - **Add language detection**: Use `OcrLanguage.AutoDetect`
      for multi‑lingual documents.'
  type: HowTo
- questions:
  - answer: Absolutely. `OcrInputImage` accepts any format that Java’s ImageIO can
      read. Just replace the file extension in the path.
    question: Does this work with PNG or JPEG files?
  - answer: You could, but remember other services may need CPU cycles. A good rule
      of thumb is “total cores – 1” for dedicated OCR workers.
    question: My server has 8 cores—should I set `setMaxThreads(8)`?
  - answer: 'Check that the image isn’t completely white, that you set the correct
      language, and that the resolution is at least 200 DPI. Low‑quality scans often
      need pre‑processing (deskew, contrast boost) before feeding them to Aspose OCR.
      --- ## Wrap‑Up We’ve just **extracted text from scanned image** files u'
    question: What if the OCR result is empty?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- Image Processing
title: استخراج النص من صورة ممسوحة ضوئياً في جافا – دليل Aspose OCR الكامل
url: /ar/java/advanced-ocr-techniques/extract-text-from-scanned-image-in-java-complete-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة ممسوحة ضوئياً – دليل Aspose OCR الكامل

هل احتجت يوماً إلى **استخراج النص من صورة ممسوحة ضوئياً** لكنك توقفت عند سؤال “كيف؟”؟ لست وحدك. سواء كنت تقوم برقمنة أرشيفات قديمة، أو استخراج بيانات من الفواتير، أو بناء مكتبة PDF قابلة للبحث، فإن الحصول على نص موثوق من مسح TIFF يمكن أن يكون نقطة ألم.  

خبر سار: باستخدام Aspose OCR for Java يمكنك **التعرف على النص من ملفات tiff** ببضع أسطر فقط، وحتى زيادة السرعة بتحديد عدد الأنوية التي يستخدمها المحرك. في هذا الدرس سنستعرض العملية بالكامل—من إعداد المكتبة إلى معالجة النتيجة—حتى تتمكن من نسخ مثال يعمل مباشرة.

## ما يغطيه هذا الدرس

- تثبيت Aspose OCR for Java (Maven أو JAR يدوي)
- تحميل صورة TIFF ممسوحة ضوئياً كبيرة
- ضبط المحرك لاستخدام ما يصل إلى 4 خيوط (OCR متوازي)
- تشغيل عملية OCR وطباعة النص المستخرج
- المشكلات الشائعة (الذاكرة، TIFF متعدد الصفحات) وكيفية تجنبها
- نصيحة سريعة للأداء: متى تضبط `setMaxThreads`

بنهاية الدرس ستتمكن من **استخراج النص من ملفات الصور الممسوحة ضوئياً** بثقة، وستفهم لماذا تعديل عدد الخيوط مهم عند *التعرف على النص من tiff* في خط إنتاج.

---

![استخراج النص من مثال صورة ممسوحة ضوئياً](example.png "لقطة شاشة تُظهر النص المستخرج من صورة TIFF ممسوحة")

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

1. **مجموعة تطوير جافا (JDK) 8+** – أي نسخة حديثة تعمل.
2. **Maven** (أو القدرة على إضافة JARs يدوياً) – سنستخدم Maven للسهولة.
3. رخصة **Aspose OCR for Java** (التقييم المجاني يعمل، لكنه يضيف علامة مائية).  
4. **مسح TIFF كبير** (مثال: `large_scan.tif`) تريد معالجته.

إذا كان أي من هذه غير مألوف لك، لا تقلق—كل خطوة مشروحة أدناه.

## الخطوة 1: إضافة Aspose OCR إلى مشروعك

### مستخدمي Maven

أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

### إعداد JAR يدويًا

حمّل أحدث `aspose-ocr-xx.jar` من موقع Aspose وضعه في مسار الـ classpath.  

> **نصيحة محترف:** احفظ الـ JAR في مجلد `libs/` وأشر إليه في إعدادات مشروع IDE الخاص بك. هذا يجنبك مفاجآت “class not found” لاحقًا.

## الخطوة 2: إنشاء فئة Java بسيطة

أنشئ ملفًا باسم `ParallelOcrDemo.java` في مجلد المصدر الخاص بك (`src/main/java`). ستحمل هذه الفئة سير عمل OCR بالكامل.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the scanned TIFF image you want to process
        // Replace the path with the actual location of your image
        ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/large_scan.tif"));

        // Step 2.3: Limit the engine to use up to 4 CPU cores.
        // This is useful on servers where you don't want to hog all cores.
        ocrEngine.getSettings().setMaxThreads(4);

        // Step 2.4: Run the OCR operation
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **لماذا نقيد عدد الخيوط:** بشكل افتراضي سيحاول Aspose OCR استخدام كل النوى، مما قد يحرم الخدمات الأخرى على جهاز مشترك من الموارد. ضبط `setMaxThreads(4)` يخبر المحرك بالعمل بأربعة عمال متوازيين—كافٍ لتحقيق تسريع ملحوظ على معظم المعالجات الحديثة دون استحواذ كامل على الموارد.

## الخطوة 3: التجميع والتشغيل

افتح طرفية في جذر المشروع ونفّذ:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ParallelOcrDemo"
```

إذا لم تكن تستخدم Maven، قم بالتجميع باستخدام `javac` ثم تشغيل:

```bash
javac -cp "libs/*" src/main/java/com/example/ocr/ParallelOcrDemo.java
java -cp "libs/*:src/main/java" com.example.ocr.ParallelOcrDemo
```

### النتيجة المتوقعة

```
=== Extracted Text ===
Invoice Number: 12345
Date: 2024‑05‑01
Total: $1,250.00
...
```

ستظهر في وحدة التحكم النسخة النصية البسيطة لما كان موجودًا في الصفحة الممسوحة. إذا احتوت الصورة على صفحات متعددة، سيقوم Aspose OCR بدمجها بالترتيب.

## الخطوة 4: معالجة TIFF متعدد الصفحات (حالة حافة)

سيناريو شائع هو **TIFF متعدد الصفحات**—مثل كتاب ممسوح. بشكل افتراضي يقرأ `OcrInputImage` الإطار الأول فقط. لمعالجة جميع الصفحات، استخدم `OcrInputImage` مع `FileInputStream` وفعل دعم الصفحات المتعددة:

```java
import java.io.FileInputStream;
import com.aspose.ocr.*;

FileInputStream fis = new FileInputStream("YOUR_DIRECTORY/multi_page.tif");
ocrEngine.setImage(new OcrInputImage(fis, true)); // 'true' enables multi‑page
```

الآن سيعيد `ocrEngine.process()` كائن `OcrResult` واحد يحتوي على النص المدمج من كل صفحة.

## الخطوة 5: تحسين دقة التعرف

إذا لاحظت **حروفًا مشوشة** أو كلمات مفقودة، جرّب هذه التعديلات:

| الإعداد | ما يفعله | متى تستخدمه |
|---------|----------|--------------|
| `ocrEngine.getSettings().setLanguage(OcrLanguage.English)` | يفرض نموذج اللغة الإنجليزية (أسرع وأكثر دقة للمستندات الإنجليزية) | مستندك أحادي اللغة الإنجليزية |
| `ocrEngine.getSettings().setResolution(300)` | يرفع دقة الصور منخفضة الدقة قبل التعرف | مسحات أقل من 200 DPI |
| `ocrEngine.getSettings().setNoiseRemoval(true)` | يحاول تنظيف البقع والضوضاء | مسحات ذات ضوضاء عالية |

مقتطف مثال:

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setNoiseRemoval(true);
```

## الخطوة 6: تصدير النتائج إلى ملف

الطباعة إلى وحدة التحكم مناسبة للعرض، لكن الكود الإنتاجي عادةً يكتب النتيجة إلى مكان مفيد:

```java
import java.io.FileWriter;
import java.io.IOException;

// After processing
String extractedText = ocrResult.getText();
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write(extractedText);
}
System.out.println("Text saved to output.txt");
```

الآن لديك ملف نصي بسيط يمكنك إرساله إلى فهرس بحث، قاعدة بيانات، أو خط أنابيب تحليلي لاحق.

---

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع ملفات PNG أو JPEG؟**  
ج: بالتأكيد. `OcrInputImage` يقبل أي صيغة يمكن لـ Java ImageIO قراءتها. فقط استبدل امتداد الملف في المسار.

**س: خادمي يحتوي على 8 نوى—هل يجب أن أضع `setMaxThreads(8)`؟**  
ج: يمكنك ذلك، لكن تذكّر أن الخدمات الأخرى قد تحتاج إلى دورات CPU. القاعدة العامة “عدد النوى الكلي – 1” للعمال المخصصين لـ OCR.

**س: ماذا لو كانت نتيجة OCR فارغة؟**  
ج: تأكد أن الصورة ليست بيضاء بالكامل، وأنك ضبطت اللغة الصحيحة، وأن الدقة لا تقل عن 200 DPI. المسحات منخفضة الجودة غالبًا ما تحتاج إلى معالجة مسبقة (تصحيح الميل، تعزيز التباين) قبل تمريرها إلى Aspose OCR.

---

## الخلاصة

لقد **استخدمنا Aspose OCR for Java لاستخراج النص من ملفات الصور الممسوحة ضوئياً**، وتعلمت الآن كيف **تتعرف على النص من tiff** بفعالية باستخدام المعالجة المتوازية. الكود الكامل موجود في المقتطفات أعلاه، ويمكنك نسخه ولصقه في مشروعك فورًا.

### ما التالي؟

- **معالجة دفعات**: حلق عبر مجلد من ملفات TIFF، واحفظ كل نتيجة في ملف منفصل.  
- **التكامل مع Elasticsearch**: فهرس النص المستخرج للبحث السريع.  
- **إضافة كشف اللغة**: استخدم `OcrLanguage.AutoDetect` للمستندات متعددة اللغات.  

جرّب هذه الأفكار، وستحوّل جبلًا من الأوراق الممسوحة إلى بيانات قابلة للبحث والعمل.

برمجة سعيدة، ولا تتردد في ترك تعليق إذا واجهت أي مشكلة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}