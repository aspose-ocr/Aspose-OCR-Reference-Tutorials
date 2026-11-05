---
category: general
date: 2026-06-19
description: التعرف على النص من الصورة باستخدام Aspose OCR في Java وتعلم تحويل الصورة
  إلى ملف docx، واستخراج النص من png، وتحويل الصورة الممسوحة ضوئياً إلى جدول بيانات.
draft: false
keywords:
- recognize text from image
- convert image to docx
- extract text from png
- convert scanned image to spreadsheet
language: ar
og_description: التعرف على النص من الصورة في جافا باستخدام Aspose OCR. اتبع هذا الدليل
  خطوة بخطوة لتحويل الصورة إلى ملف docx، واستخراج النص من PNG، وتحويل الصورة الممسوحة
  ضوئياً إلى جدول بيانات.
og_title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل Java
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: recognize text from image using Aspose OCR in Java and learn to convert
    image to docx, extract text from png, and convert scanned image to spreadsheet.
  headline: recognize text from image with Aspose OCR – Java guide
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- Image Processing
title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل Java
url: /ar/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة باستخدام Aspose OCR – دليل Java

هل احتجت يومًا إلى **التعرف على النص من صورة** لكنك لم تكن متأكدًا أي مكتبة يمكنها التعامل مع ملفات PDF الألمانية، PNG، وحتى استخراج جدول بيانات؟ لست وحدك. في هذا الدرس سنستعرض مثالًا كاملاً بلغة Java لا يقتصر فقط على استخراج الأحرف بل أيضًا **تحويل الصورة إلى docx**، **استخراج النص من png**، وحتى **تحويل الصورة الممسوحة ضوئيًا إلى جدول بيانات**—كل ذلك ببضع أسطر فقط.

سنستخدم Aspose.OCR، مكتبة تجارية تأتي بواجهة برمجة تطبيقات بسيطة. لا تقلق إذا لم يكن لديك ترخيص؛ يعمل العرض التجريبي في وضع التقييم، رغم أن بعض الميزات (مثل الإخراج عالي الدقة) تكون محدودة. في النهاية ستحصل على برنامج قابل للتنفيذ يأخذ لقطة شاشة PNG لتقرير ويولد ملفات DOCX، XLSX، و EPUB تلقائيًا.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* **Java Development Kit (JDK) 17** أو أحدث مثبت.
* **Aspose.OCR for Java** JAR (حمّله من موقع Aspose أو أضفه عبر Maven).
* ملف **Aspose.OCR.lic** اختياري إذا أردت الاستفادة من جميع الوظائف دون علامات التقييم.
* صورة نموذجية—لنسمها `report.png`—موجودة في مجلد يمكنك الإشارة إليه من الكود.

إذا كنت تستخدم Maven، أضف هذا الاعتماد إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

الآن بعد أن أُنجزت الأساسيات، لنبدأ.

## الخطوة 1: التعرف على النص من صورة – تطبيق الترخيص (اختياري)

أولًا، نحتاج إلى إخبار Aspose بأن لدينا ترخيصًا. تخطي هذه الخطوة لن يوقف العرض التجريبي، لكنك سترى شريطًا صغيرًا “Evaluation” في ملفات الإخراج.

```java
import com.aspose.ocr.*;

public class ExportDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (optional for full functionality)
        License license = new License();
        try {
            license.setLicense("Aspose.OCR.lic");
            System.out.println("License loaded successfully.");
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }
```

> **نصيحة محترف:** ضع ملف `.lic` بجوار ملف JAR المترجم أو استخدم مسارًا مطلقًا؛ وإلا سيتسبب استدعاء `setLicense` في حدوث استثناء.

## الخطوة 2: التعرف على النص من صورة – إنشاء وتكوين محرك OCR

الآن نقوم بإنشاء محرك OCR ونحدّد اللغة المتوقعة. في هذا المثال نتعامل مع الألمانية، لكن Aspose يدعم عشرات اللغات مباشرةً.

```java
        // Create an OCR engine and set the recognition language to German
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(Language.German); // change to Language.English for English text
```

لماذا نحدد اللغة؟ يستخدم المحرك قواميس خاصة بكل لغة لتحسين الدقة، خاصةً للأحرف مثل “ß” أو “ü”. إذا تخطيت ذلك ستحصل على نتائج، لكنها ستكون أكثر ضوضاء.

## الخطوة 3: التعرف على النص من صورة – تمرير ملف PNG والحصول على النتائج الأولية

هذا هو جوهر العرض: نمرّر للمحرك مسار ملف PNG ونتركه يقوم بالمعالجة.

```java
        // Recognize text from the input image
        String inputImagePath = "YOUR_DIRECTORY/report.png"; // <-- replace with your actual path
        OcrResult ocrResult = ocrEngine.recognizeImage(inputImagePath);
        System.out.println("OCR completed. Extracted " + ocrResult.getText().length() + " characters.");
```

كائن `OcrResult` يحتوي على السلسلة Unicode الأولية، بالإضافة إلى معلومات التخطيط التي يمكنك استخدامها لاحقًا إذا أردت الحفاظ على التنسيق. إذا كانت الصورة جدولًا ممسوحًا ضوئيًا، سيعيد المحرك نصًا عاديًا—مما يُسهّل الخطوة التالية حيث **نحوّل الصورة الممسوحة إلى جدول بيانات**.

## الخطوة 4: تحويل الصورة إلى docx – حفظ النتيجة كملف Word

تجعل Aspose عملية تصدير ناتج OCR إلى ملف DOCX سهلة للغاية. هذا مفيد عندما تحتاج إلى مستند Word قابل للتحرير للمعالجة اللاحقة.

```java
        // Save the recognized text in DOCX format
        String outputDocxPath = "YOUR_DIRECTORY/report.docx";
        ocrResult.save(outputDocxPath, OutputFormat.Docx);
        System.out.println("Saved DOCX to " + outputDocxPath);
```

في الخلفية، تُنشئ المكتبة مستند Word بسيط يحتوي على فقرة واحدة تضم النص المستخرج. إذا احتجت إلى تنسيق أكثر تعقيدًا (عناوين، جداول)، يمكنك تعديل ملف DOCX لاحقًا باستخدام Apache POI أو Aspose.Words.

## الخطوة 5: تحويل الصورة الممسوحة إلى جدول بيانات – تصدير إلى XLSX

أحيانًا يكون من الأسهل التعامل مع فاتورة ممسوحة أو جدول مالي في Excel. يمكن حفظ نفس كائن `OcrResult` كملف XLSX، وستحاول Aspose الحفاظ على البنى الجدولية إذا اكتشفتها.

```java
        // Save the same result in additional formats (XLSX, EPUB)
        String outputXlsxPath = "YOUR_DIRECTORY/report.xlsx";
        ocrResult.save(outputXlsxPath, OutputFormat.Xlsx);
        System.out.println("Saved XLSX to " + outputXlsxPath);
```

إذا كان PNG الأصلي يحتوي على شبكة نظيفة، سيتكون جدول البيانات من خلايا منفصلة لكل عمود. وإلا ستحصل على عمود واحد مع فواصل أسطر—ما يزال أفضل من النسخ واللصق يدويًا.

## الخطوة 6: استخراج النص من png – وتصدير إلى EPUB (اختياري)

لإكمال الصورة، نوضح كيفية إنشاء كتاب إلكتروني بصيغة EPUB. يوضح ذلك مرونة طريقة `save` في Aspose ويعطيك طريقة أخرى لـ **استخراج النص من png** للنشر.

```java
        // Optional: export to EPUB for e‑reading devices
        String outputEpubPath = "YOUR_DIRECTORY/report.epub";
        ocrResult.save(outputEpubPath, OutputFormat.Epub);
        System.out.println("Saved EPUB to " + outputEpubPath);
    }
}
```

هذا هو البرنامج بالكامل. قم بترجمته (`javac ExportDemo.java`) ثم تشغيله (`java ExportDemo`). إذا تم إعداد كل شيء بشكل صحيح، ستظهر أربعة ملفات في `YOUR_DIRECTORY`: `report.docx`، `report.xlsx`، `report.epub`، وستظهر في وحدة التحكم عدد الأحرف المستخرجة.

## المشكلات الشائعة وكيفية تجنّبها

| المشكلة | السبب | الحل |
|-------|-------|-----|
| **الترخيص غير موجود** | مسار `Aspose.OCR.lic` غير صحيح أو مفقود. | ضع الملف بجوار الـ JAR أو استخدم مسارًا مطلقًا في `setLicense`. |
| **حروف غير مفهومة** | تم تعيين لغة خاطئة (مثلاً الإنجليزية للنص الألماني). | استدعِ `ocrEngine.setLanguage(Language.German)` أو اللغة المناسبة. |
| **ملفات إخراج فارغة** | خطأ في مسار صورة الإدخال أو تنسيق غير مدعوم. | تحقق من المسار، تأكد من وجود الملف، وتأكد من أنه من تنسيق نقطي مدعوم (PNG, JPEG, BMP). |
| **حجم ملف كبير** | استخدام صور عالية الدقة دون تقليل الحجم. | قلل حجم الصورة إلى ~300 dpi قبل OCR؛ يمكن لـ Aspose القيام بذلك تلقائيًا عبر `ocrEngine.setResolution(300)`. |

## توسيع الحل

الآن بعد أن أصبحت قادرًا على **التعرف على النص من صورة** و**تحويل الصورة الممسوحة إلى جدول بيانات**، قد تتساءل عن ما يمكن فعله أيضًا:

* **معالجة دفعات** – تكرار عبر مجلد PNGs وإنشاء ملف ZIP يحتوي على ملفات DOCX/XLSX.
* **معالجة لاحقة** – استخدام تعبيرات نمطية لتنظيف ضوضاء OCR (مثل فواصل الأسطر الزائدة).
* **تكامل** – ربط الكود بنقطة نهاية REST في Spring Boot تستقبل تحميلات الصور وتعيد ملف DOCX قابل للتنزيل.

كل هذه الأفكار تبنى على الخطوات الأساسية التي غطيناها للتو.

## الخلاصة

لقد تعلمت الآن كيفية **التعرف على النص من صورة** باستخدام Aspose OCR للـ Java، وعرفت أيضًا كيفية **تحويل الصورة إلى docx**، **استخراج النص من png**، و**تحويل الصورة الممسوحة إلى جدول بيانات** ببضع نداءات للطرق. المثال الكامل القابل للتنفيذ أعلاه يوضح كل استيراد، كل تكوين، والنتيجة المتوقعة بدقة.

الخطوة التالية: جرّب تغيير اللغة إلى الإنجليزية، أو معالجة ملف TIFF متعدد الصفحات، أو ربط ناتج DOCX بـ Aspose.Words لتنسيق متقدم. لا حدود لما يمكنك تحقيقه عندما تجمع بين OCR ومكتبات توليد المستندات.

هل لديك أسئلة أو واجهت مشكلة؟ اترك تعليقًا، وتمنياتنا لك ببرمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}