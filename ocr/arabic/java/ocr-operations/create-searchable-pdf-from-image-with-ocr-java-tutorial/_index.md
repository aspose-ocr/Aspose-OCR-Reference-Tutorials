---
category: general
date: 2026-01-07
description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR في Java. تعلم كيفية
  تحويل الصورة إلى PDF، التعرف على النص من الصورة، وإنشاء PDF من JPG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة باستخدام Aspose OCR في Java. دليل
  خطوة بخطوة لتحويل الصورة إلى PDF، والتعرف على النص من الصورة، وإنشاء PDF من JPG.
og_title: إنشاء ملف PDF قابل للبحث من صورة – دليل جافا للتعرف الضوئي على الحروف
tags:
- OCR
- Java
- PDF
- Aspose
title: إنشاء ملف PDF قابل للبحث من صورة باستخدام OCR – درس جافا
url: /ar/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF قابل للبحث من صورة باستخدام OCR – دليل Java

هل احتجت يوماً إلى **إنشاء ملف PDF قابل للبحث** من صورة ممسوحة ضوئياً لكن لم تعرف من أين تبدأ؟ لست وحدك—الكثير من المطورين يواجهون هذه المشكلة عندما يحاولون أول مرة تحويل JPEG إلى PDF يمكنك فعلاً البحث فيه.  

في هذا الدليل سنستعرض مثالاً كاملاً قابلاً للتنفيذ يوضح لك كيفية **تحويل الصورة إلى PDF**، **التعرف على النص من الصورة**، وأخيراً **إنشاء PDF من JPG** باستخدام Aspose OCR for Java. لا مراجع غامضة، فقط كود يمكنك نسخه‑ولصقه وتشغيله اليوم.

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي على جهازك:

* **Java 17** أو أحدث (تعمل الواجهة البرمجية مع أي JDK حديث).  
* مكتبة **Aspose.OCR for Java** – يمكنك الحصول على أحدث JAR من Maven Central أو موقع Aspose.  
* صورة تجريبية، مثل `sample.jpg`، موجودة في مجلد يمكنك الإشارة إليه.  
* بيئة تطوير متكاملة أو محرر نصوص بسيط بالإضافة إلى الطرفية—أيًا كان ما ترتاح له.

هذا كل شيء. لا أطر عمل ثقيلة، ولا تبعيات أصلية إضافية. هيا نبدأ.

## الخطوة 1 – إنشاء PDF قابل للبحث: تهيئة محرك OCR

أول ما نقوم به هو إنشاء نسخة من `OcrEngine` وتوجيهها إلى صورة المصدر. هذا الكائن هو قلب Aspose OCR؛ فهو يتعامل مع كل شيء من تحميل البت ماب إلى إظهار النص المُعترف به.

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **لماذا هذا مهم:** تهيئة المحرك بشكل صحيح يضمن أن المكتبة تستطيع قراءة صيغة الصورة التي تزودها إياها. إذا كان المسار خاطئًا، ستحصل على `FileNotFoundException` وسيتوقف سير العمل بالكامل.

## الخطوة 2 – تعزيز الأداء: تمكين GPU، المعالجة متعددة النوى وتصحيح الإملاء

يمكن أن يكون OCR مستهلكًا للمعالج، خاصةً مع المستندات الكبيرة. توفر لك Aspose مجموعة من الخيارات التي يمكنك تعديلها لجعل العملية أسرع وأكثر دقة.

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **نصيحة احترافية:** إذا كنت تعمل على خادم بدون GPU، فإن `setUseGpu(false)` لن يضر—سيتراجع فقط إلى المعالجة متعددة النوى على المعالج.

## الخطوة 3 – تحسين جودة الصورة: تصحيح الميل وإزالة البقع (اختياري لكن موصى به)

المسحات النادرة ما تكون مثالية. قليل من الميل أو الضوضاء يمكن أن يربك برنامج التعرف. تسمح لك فئة `ImageProcessingOptions` بتنظيف الصورة قبل أن يحاول المحرك قراءتها.

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **حالة حافة:** إذا كانت صورة المصدر نظيفة بالفعل، يمكنك تخطي هذه الخطوة. لن تضر، لكنها تضيف بضع مللي ثانية من الحمل الزائد.

## الخطوة 4 – التعرف على النص من الصورة وإنشاء PDF

الآن يحدث السحر. نستدعي `recognize()` ويعيد المحرك كائن `OcrResult`. من هناك يمكننا حفظ النتيجة بعدة صيغ—PDF هي الأكثر شيوعًا للوثائق القابلة للبحث.

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **ما ستراه:** يحتوي `sample-output.pdf` على الصورة الأصلية كطبقة خلفية، بينما يُوضع النص المُعترف به فوقها كطبقة غير مرئية. افتحه في Adobe Reader وجرب تحديد النص—ستتفاجأ.

## الخطوة 5 – التحقق من ناتج إنشاء PDF القابل للبحث

بعد كتابة الملف، من الجيد التحقق مرة أخرى أن الـ PDF قابل للبحث فعليًا.

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

افتح الـ PDF، اضغط **Ctrl F**، واكتب كلمة تعلم أنها موجودة في الصورة—إذا وجد البحث الكلمة، فقد نجحت في **إنشاء ملف PDF قابل للبحث**!

## كيفية استخدام OCR في سيناريوهات العالم الحقيقي (إضافة)

* **المعالجة الدفعية:** ضع الكود داخل حلقة تتكرر على مجلد من JPGs. تذكر إعادة استخدام نسخة واحدة من `OcrEngine` لتقليل استهلاك الذاكرة.  
* **دعم اللغات:** يدعم Aspose OCR أكثر من 60 لغة. فقط استدعِ `ocrEngine.getEngineOptions().setLanguage(Language.English);` (أو أي قيمة أخرى من الـ enum).  
* **معالجة الأخطاء:** امسك `OcrException` للتعامل بلطف مع الملفات التالفة.  

هذه التعديلات تجعل الحل قويًا بما يكفي لخطوط الإنتاج.

## مثال Java كامل – إنشاء PDF قابل للبحث من JPG

فيما يلي البرنامج الكامل المستقل الذي يمكنك تجميعه وتشغيله كما هو. استبدل `YOUR_DIRECTORY` بالمسار الفعلي على جهازك.

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**الناتج المتوقع:**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

افتح الـ PDF المُولد ويجب أن تكون قادرًا على البحث عن أي كلمة ظهرت في `sample.jpg`. إذا لم ترى طبقة النص، تحقق مرة أخرى من مسار الصورة وتأكد أن محرك OCR لا يطلق استثناءات مخفية.

## الخلاصة

لقد أظهرنا لك الآن كيفية **إنشاء ملف PDF قابل للبحث** من JPEG باستخدام Aspose OCR for Java. من تحميل الصورة، تعديل إعدادات الأداء، تنظيف الصورة، إلى التعرف على النص وحفظ PDF قابل للبحث—تم شرح كل خطوة مع *السبب* و*الطريقة*.  

الآن يمكنك **تحويل الصورة إلى PDF**، **التعرف على النص من الصورة**، و**إنشاء PDF من JPG** في تطبيقاتك الخاصة. الخطوة التالية، جرّب معالجة مجلد كامل من المسحات، جرب لغات مختلفة، أو أضف حماية كلمة مرور إلى ملف PDF الناتج. السماء هي الحد.

هل لديك أسئلة حول حالات الحافة، الترخيص، أو تحسين الأداء؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة! 

![مخطط يوضح خط أنابيب OCR – إنشاء PDF قابل للبحث](/images/ocr-pipeline.png "مخطط إنشاء PDF قابل للبحث")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}