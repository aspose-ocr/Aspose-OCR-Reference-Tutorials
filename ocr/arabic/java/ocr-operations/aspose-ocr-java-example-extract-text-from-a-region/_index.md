---
category: general
date: 2026-05-03
description: يوضح مثال Aspose OCR للغة Java كيفية تحميل صورة للتعرف الضوئي على الأحرف
  واستخراج النص من منطقة معينة في بضع أسطر من الشيفرة فقط.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: ar
og_description: مثال Aspose OCR للغة Java يوضح تحميل صورة للتعرف الضوئي على الأحرف
  واستخراج النص من منطقة محددة، وهو مثالي لمعالجة الفواتير.
og_title: مثال Aspose OCR بلغة Java – استخراج النص من المنطقة
tags:
- Aspose OCR
- Java
- Image Processing
title: 'مثال Aspose OCR بلغة Java: استخراج النص من منطقة'
url: /ar/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مثال Aspose OCR Java: استخراج النص من منطقة

هل تبحث عن **مثال Aspose OCR Java** يتيح لك استخراج الجزء الذي تحتاجه فقط من صورة؟ في هذا الدليل سنستعرض **تحميل صورة للـ OCR** و **استخراج النص من منطقة**، وهو مثالي لأرقام الفواتير، حقول النماذج، أو أي قطعة من البيانات المخفية داخل صورة أكبر.

قد تتساءل لماذا تُقيد الـ OCR بمستطيل بدلاً من مسح الصفحة بالكامل. الجواب المختصر: السرعة والدقة. عندما ينظر المحرك فقط إلى جزء محدد، يتخطى الضوضاء غير ذات الصلة، يعمل أسرع، وغالبًا ما ينتج نتائج أنظف. بنهاية هذا الشرح ستحصل على برنامج Java مستقل يقوم بذلك بالضبط، بالإضافة إلى مجموعة من النصائح لتجنب الأخطاء الشائعة التي تعيق المبتدئين.

## ما ستحتاجه

- **Java Development Kit (JDK) 11** أو أحدث مثبت.
- مكتبة **Aspose.OCR for Java** (يمكنك الحصول على أحدث JAR من مستودع Maven Central أو بوابة تحميل Aspose).
- ملف صورة يحتوي على النص الذي تريد قراءته – في مثالنا سنستخدم `invoice.png`، الذي يحتوي على رقم الفاتورة في مكان ما بالقرب من الزاوية العليا اليمنى.
- بيئة تطوير مفضلة أو محرر نصوص بسيط بالإضافة إلى الطرفية؛ أي أداة بناء (Maven، Gradle، أو مجرد `javac`) ستكفي.

هذا كل شيء. لا محركات OCR إضافية، لا ملفات تنفيذية أصلية، فقط Java صافية و Aspose.

![لقطة شاشة مثال Aspose OCR Java](/images/aspose-ocr-java-example.png "مثال Aspose OCR Java يظهر استخراج المنطقة")

## مثال Aspose OCR Java – تهيئة محرك OCR

أول شيء يحتاجه أي سير عمل OCR هو نسخة من المحرك. تقدم Aspose فئة `OcrEngine` خفيفة الوزن التي تتعامل مع كل شيء من تحميل الصورة إلى اختيار اللغة.

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**لماذا هذا مهم:** إنشاء المحرك مسبقًا يمنحك كائنًا نظيفًا لتكوينه. يمكنك إعادة استخدام نفس `OcrEngine` لعدة صور إذا كنت تعالج دفعة، مما يوفر الذاكرة ووقت التهيئة.

## تحميل صورة للـ OCR

الخطوة التالية نخبر المحرك أي صورة يجب مسحها. توفر Aspose المساعد `ImageStream.fromFile`، الذي يُجردك من تفاصيل `FileInputStream` منخفضة المستوى.

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**نصيحة:** استبدل `YOUR_DIRECTORY` بمسار مطلق أو نسبي يشير إلى المكان الذي حفظت فيه `invoice.png`. إذا لم يتم العثور على الملف، تقوم Aspose بإلقاء `IOException`، لذا قد ترغب في تغليف ذلك بكتلة try‑catch في الكود الإنتاجي.

## تعريف واستخراج النص من منطقة

الآن يأتي نجم العرض: المستطيل الذي يحدد للمحرك أين ينظر. يأخذ مُنشئ `java.awt.Rectangle` القيم `(x, y, width, height)` – كلها مقاسة بالبكسل.

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**كيف يعمل:** من خلال استدعاء `setRegion`، تقوم بتحديد مسح الـ OCR إلى شريحة عرضها 300 بكسل تبدأ 120 بكسل من الحافة اليسرى و250 بكسل من الأعلى. عدّل هذه الأرقام لتتناسب مع تخطيطك؛ طريقة سريعة للعثور عليها هي فتح الصورة في أي محرر رسومات يُظهر إحداثيات البكسل.

## تمكين اللغة وتشغيل التعرف

يدعم Aspose OCR عشرات اللغات، ولكن لرقم الفاتورة نحتاج فقط إلى الإنجليزية. تمكين اللغة المناسبة يقلل الإيجابيات الزائفة بشكل كبير.

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**لماذا تمكين الإنجليزية فقط؟** سيحاول محرك OCR مطابقة الأحرف من كل مجموعة لغات مفعلة، مما قد يربكه عندما يكون النص أبجديًا رقميًا بسيطًا. تضييق نطاق اللغة يحسن كلًا من السرعة والدقة.

### النتيجة المتوقعة

عند توافق كل شيء، سترى شيئًا مثل:

```
Extracted region text: INV-12345
```

إذا كان المستطيل غير محاذٍ ببضع بكسلات، قد يكون الناتج مشوشًا أو فارغًا. هذه طريقة فحص بسيطة: شغّل البرنامج، انظر إلى وحدة التحكم، وتأكد أن النص يطابق ما تراه في الصورة.

## تشغيل الكود والتحقق من الناتج

بافتراض أنك تستخدم Maven، أضف تبعية Aspose OCR إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

قم بالترجمة والتنفيذ:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

أو، إذا كنت تفضّل استخدام `javac` العادي:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

يجب أن ترى سطر **Extracted region text** يُطبع في وحدة التحكم. إذا حصلت على رسالة “OCR recognition failed”، فتحقق مرة أخرى من مسار الملف وتأكد أن المنطقة تحتوي فعليًا على أحرف قابلة للقراءة.

## الحالات الخاصة والاختلافات الشائعة

| الحالة | ما الذي يجب تغييره |
|-----------|----------------|
| **لغات متعددة** (مثلاً الإنجليزية + الإسبانية) | استدعِ `ocrEngine.getLanguage().setSpanish(true);` إلى جانب الإنجليزية. |
| **منطقة خارج حدود الصورة** | ستقوم Aspose بقطع المستطيل بصمت، لكنك ستفقد البيانات. استخدم `ImageInfo` (`ocrEngine.getImage().getWidth()`) للتحقق من الأبعاد قبل تعيين المنطقة. |
| **فواتير ديناميكية** (تصاميم مختلفة) | فكر في إجراء فحص مسبق خفيف على الصورة بالكامل لتحديد كلمات مفتاحية مثل “Invoice #” ثم احسب المستطيل برمجيًا. |
| **صور بدقة DPI أعلى** | زد `ocrEngine.getImage().setResolution(300);` للحصول على دقة أفضل في المستندات الممسوحة. |
| **تحسين الأداء** | عطل اللغات غير الضرورية، اجعل المنطقة صغيرة قدر الإمكان، وأعد استخدام نسخة واحدة من `OcrEngine` عبر العديد من الملفات. |

## نصائح احترافية من الميدان

- **نصيحة احترافية:** إذا كنت تحتاج فقط إلى الأرقام (شائع لأرقام الفواتير)، فعّل وضع الأرقام باستخدام `ocrEngine.getLanguage().setDigits(true);`. هذا يزيل الضوضاء الأبجدية.
- **احذر من:** ملفات PNG الشفافة. أحيانًا تفسر Aspose قناة alpha بشكل خاطئ؛ تحويل الصورة إلى JPEG بخلفية صلبة أولاً يمكن أن يحل مخرجات فارغة غريبة.
- **تذكر:** المستطيل يستخدم نظام إحداثيات الصورة الأصلي، وليس أي مقياس واجهة مستخدم قد تراه على الشاشة. اختبر دائمًا باستخدام الملف الدقيق الذي ستعالجه في الإنتاج.

## ما التالي؟

الآن بعد أن لديك **مثال Aspose OCR Java** قوي لاستخراج مبني على المنطقة، يمكنك توسيعه في عدة اتجاهات مفيدة:

- **معالجة دفعات:** تكرار عبر مجلد الفواتير، وإعادة استخدام نفس `OcrEngine` لتحسين الإنتاجية.
- **تحقق من البيانات:** تمرير النص المستخرج عبر تعبير نمطي مثل `INV-\\d{5}` للتأكد من أنك حصلت على رقم فاتورة صالح.
- **التكامل مع PDF:** استخدم Aspose.PDF لتراكب النص المستخرج مرة أخرى على المستند الأصلي لتتبع المراجعة.
- **نشر سحابي:** غلف الكود في خدمة REST خفيفة (Spring Boot) حتى تتمكن الأنظمة الأخرى من استدعائه عند الحاجة.

كل من هذه الخطوات يتضمن بطبيعة الحال نفس المفاهيم الأساسية—**تحميل صورة للـ OCR**، **استخراج النص من منطقة**، ومعالجة النتائج—لذا ستجد الانتقال سهلًا.

---

*برمجة سعيدة! إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو تحقق من منتديات Aspose حيث يشارك المجتمع تعديلات واقعية لتنسيقات صعبة.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}