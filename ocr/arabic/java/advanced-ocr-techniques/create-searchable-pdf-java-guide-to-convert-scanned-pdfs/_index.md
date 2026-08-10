---
category: general
date: 2026-02-22
description: إنشاء ملف PDF قابل للبحث من ملف PDF ممسوح ضوئياً باستخدام Aspose OCR
  في Java. تعلم كيفية تحويل ملف PDF الممسوح، ضغط صور PDF، والتعرف على نص PDF باستخدام
  OCR بكفاءة.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: ar
og_description: إنشاء ملف PDF قابل للبحث من ملف PDF ممسوح ضوئياً باستخدام Aspose OCR
  في جافا. يوضح هذا الدليل خطوة بخطوة كيفية تحويل ملف PDF الممسوح، ضغط صور PDF، والتعرف
  الضوئي على النص في PDF.
og_title: إنشاء ملف PDF قابل للبحث – دليل جافا لتحويل ملفات PDF الممسوحة ضوئياً
tags:
- Java
- OCR
- PDF
- Aspose
title: إنشاء ملف PDF قابل للبحث – دليل جافا لتحويل ملفات PDF الممسوحة ضوئياً
url: /ar/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث – دليل Java لتحويل ملفات PDF الممسوحة ضوئياً

هل احتجت يوماً إلى **create searchable PDF** من مجموعة من المستندات الممسوحة ضوئياً؟ إنها مشكلة شائعة—ملفات PDF تبدو جيدة، لكن لا يمكنك الضغط على *Ctrl + F* للبحث عن أي شيء. الخبر السار؟ ببضع أسطر من Java و Aspose OCR يمكنك تحويل تلك الـ PDFs التي تحتوي على صور فقط إلى ملفات قابلة للبحث بالكامل، **convert scanned PDF** إلى نص، وحتى تقليل الحجم عن طريق **compressing PDF images**.  

في هذا الدرس سنستعرض مثالاً كاملاً قابلاً للتنفيذ، نشرح لماذا كل إعداد مهم، ونظهر لك كيفية تعديل العملية لحالات خاصة مثل المسحات متعددة الصفحات أو الصور منخفضة الدقة. في النهاية ستحصل على مقتطف جاهز للإنتاج **recognize pdf ocr** بشكل موثوق وينتج مستندًا بحثيًا منظمًا.

---

## ما ستحتاجه

- **Java 17** (أو أي JDK حديث؛ الـ API غير مرتبط بJDK معين)  
- مكتبة **Aspose.OCR for Java** – يمكنك الحصول عليها من Maven Central (`com.aspose:aspose-ocr`)  
- ملف PDF ممسوح ضوئيًا (صورة‑فقط) تريد جعله قابلًا للبحث  
- بيئة تطوير متكاملة أو محرر نصوص ترتاح له (IntelliJ, VS Code, Eclipse…)

لا أطر ثقيلة، لا خدمات خارجية—فقط Java نقي وملف JAR واحد من طرف ثالث.

---

![create searchable pdf example](placeholder-image.png "Illustration of a searchable PDF created from a scanned document")

*نص بديل للصورة:* **create searchable pdf** توضيح يُظهر قبل‑و‑بعد ملف PDF ممسوح تم تحويله إلى نص قابل للبحث.

---

## الخطوة 1 – تهيئة محرك OCR  

أول شيء يجب عليك فعله هو إنشاء نسخة من `OcrEngine`. فكر فيه كالعقل الذي سيحلل كل صورة نقطية داخل الـ PDF ويُخرج حروف Unicode.  

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **نصيحة احترافية:** إذا كنت تخطط لمعالجة العديد من ملفات PDF على التوالي، أعد استخدام نفس `OcrEngine` بدلاً من إنشاء جديد في كل مرة. سيوفر ذلك بضع مليثانية ويقلل استهلاك الذاكرة.

---

## الخطوة 2 – ضبط إعدادات OCR الخاصة بـ PDF  

تتيح لك Aspose ضبط كيفية بناء الـ PDF الناتج. الإعدادات الثلاثة أدناه هي الأكثر تأثيرًا على **compress pdf images** مع الحفاظ على قابلية البحث.  

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi هو نقطة التوازن المثالية؛ القيم الأقل تُسرّع العملية لكن قد تفوت الخطوط الصغيرة.  
- **CompressImages** – يُفعّل ضغط PNG بدون فقدان داخلية؛ يبقى الـ PDF القابل للبحث واضحًا لكنه أخف وزنًا.  
- **EmbedOriginalImages** – بدون هذا العلم سيتخلص المحرك من الصورة الأصلية، تاركًا النص غير المرئي فقط. إبقاء الصورة يضمن أن الـ PDF يبدو تمامًا كالمسح الأصلي، وهو ما تتطلبه العديد من فرق الامتثال.

---

## الخطوة 3 – تحميل ملف PDF الممسوح إلى `OcrInput`  

تقرأ Aspose الملف المصدر عبر غلاف `OcrInput`. يمكنك إضافة ملفات متعددة، لكن في هذا العرض سنركز على **image PDF** واحد فقط.  

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **لماذا لا نمرر `File` مباشرةً؟** استخدام `OcrInput` يمنحك المرونة لدمج عدة ملفات PDF أو حتى خلط ملفات صور (PNG, JPEG) قبل الـ OCR. هذا هو النمط الموصى به عند **convert scanned pdf** قد يكون مقسمًا على مصادر متعددة.

---

## الخطوة 4 – تنفيذ OCR والحصول على PDF قابل للبحث كمصفوفة بايت  

الآن يحدث السحر. يحلل المحرك كل صفحة، يشغل محرك OCR الخاص به، ويُنشئ PDF جديد يحتوي على الصورة الأصلية وطبقة نص مخفية.  

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

إذا كنت بحاجة إلى النص الخام لأغراض أخرى (مثل الفهرسة)، يمكنك أيضًا استدعاء `ocrEngine.recognize(ocrInput)` الذي يُعيد `String`. لكن لهدف **create searchable pdf**، مصفوفة البايت هي ما ستكتبه إلى القرص.

---

## الخطوة 5 – حفظ PDF القابل للبحث إلى القرص  

أخيرًا، اكتب مصفوفة البايت إلى ملف. تجعلك NIO في Java تقوم بذلك بسطر واحد.  

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

عند فتح `searchable_output.pdf` في Adobe Acrobat أو أي عارض حديث، ستلاحظ أنك الآن تستطيع تحديد النص، نسخه، والبحث فيه—تمامًا ما يعد به تحويل **image pdf to text**.

---

## تحويل PDF الممسوح إلى نص باستخدام OCR (اختياري)

أحيانًا تحتاج فقط إلى النص المستخرج، وليس PDF جديد. يمكنك إعادة استخدام نفس المحرك:  

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

هذا المقتطف يوضح مدى سهولة **recognize pdf ocr** للمعالجة اللاحقة مثل تغذية فهرس بحث أو إجراء تحليل لغوي طبيعي.

---

## ضغط صور PDF لتقليل حجم الملفات  

إذا كانت مسحاتك المصدرية ضخمة (مثلاً مسحات ملونة بدقة 600 dpi)، قد يظل الـ PDF القابل للبحث كبيرًا. إلى جانب علم `setCompressImages(true)`، يمكنك تقليل الدقة يدويًا قبل الـ OCR:  

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

خفض الـ DPI سيقلل حجم الملف تقريبًا إلى النصف، لكن اختبر قابلية القراءة—بعض الخطوط تصبح غير مقروءة تحت 150 dpi. التوازن بين **compress pdf images** ودقة OCR هو ما ستحدده بناءً على قيود التخزين لديك.

---

## شرح إعدادات OCR للـ PDF  

| الإعداد                     | تأثيره على الناتج                         | حالة الاستخدام النموذجية                                   |
|----------------------------|-------------------------------------------|------------------------------------------------------------|
| `setOutputDpi(int)`        | يتحكم في دقة الصورة النقطية لإخراج OCR      | أرشيفات عالية الجودة (300 dpi) مقابل PDFs خفيفة للويب (150 dpi) |
| `setCompressImages`        | يُفعّل ضغط PNG                           | عندما تحتاج لإرسال PDFs عبر البريد الإلكتروني أو تخزينها في السحابة |
| `setEmbedOriginalImages`   | يحافظ على الصورة الأصلية                 | مستندات قانونية أو امتثال يجب أن تحتفظ بالمظهر الأصلي |
| `setLanguage` (اختياري)   | يفرض نموذج اللغة (مثل "eng")             | مجموعات نصوص متعددة اللغات حيث قد يخطئ الاكتشاف التلقائي |

فهم هذه المفاتيح يساعدك على **recognize pdf ocr** بذكاء وتجنب فخ "النص الضبابي".

---

## PDF صورة إلى نص – الأخطاء الشائعة وكيفية تجنّبها  

1. **Low‑resolution scans** – دقة OCR تنخفض بشكل حاد تحت 150 dpi. قم بزيادة حجم المصدر قبل إرساله إلى Aspose، أو اطلب DPI أعلى من الماسح.  
2. **Rotated pages** – إذا كانت الصفحات ممسوحة جانبياً، فعّل auto‑rotate: `pdfOcrOptions.setAutoRotate(true);`.  
3. **Encrypted PDFs** – لا يستطيع المحرك قراءة الملفات المحمية بكلمة مرور؛ فك التشفير أولاً باستخدام `PdfDocument` من Aspose.PDF.  
4. **Mixed raster and text** – بعض ملفات PDF تحتوي بالفعل على طبقة نص مخفية. تشغيل OCR مرة أخرى قد يكرر النص. استخدم `PdfOcrOptions.setSkipExistingText(true);` للحفاظ على الطبقة الأصلية.

معالجة هذه القضايا تضمن أن خط أنابيب **create searchable pdf** الخاص بك قوي عبر مجموعات المستندات الواقعية.

---

## مثال كامل يعمل (جميع الخطوات في ملف واحد)

فيما يلي الفئة الكاملة بلغة Java التي يمكنك نسخها ولصقها في بيئتك التطويرية. استبدل `YOUR_DIRECTORY` بمسار المجلد الفعلي.  

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure PDF‑specific OCR options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}