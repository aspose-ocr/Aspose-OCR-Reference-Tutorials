---
category: general
date: 2026-02-17
description: كيفية استخدام OCR في Java لاستخراج النص من PDF، وتحويل PDF إلى صور، وإجراء
  OCR على ملفات PDF الممسوحة ضوئياً باستخدام Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: ar
og_description: كيفية استخدام OCR في جافا لاستخراج النص من ملفات PDF. تعلم تحويل PDF
  إلى صور والتعرف على PDF الممسوح ضوئياً باستخدام Aspose.OCR.
og_title: كيفية استخدام OCR في جافا – دليل كامل
tags:
- OCR
- Java
- Aspose
title: كيفية استخدام OCR في جافا – استخراج النص من PDF باستخدام Aspose.OCR
url: /ar/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في جافا – استخراج النص من PDF باستخدام Aspose.OCR

هل تساءلت يومًا **كيف تستخدم OCR** لتحويل ملف PDF ممسوح ضوئيًا إلى نص قابل للبحث؟ لست وحدك. يواجه معظم المطورين مشكلة عندما يأتي PDF على شكل مجموعة من الصور، وتُعيد أدوات استخراج النص العادية لا شيء. الخبر السار؟ ببضع أسطر من جافا و Aspose.OCR يمكنك **استخراج النص من PDF**، **تحويل PDF إلى صور**، و **التعرف على PDF الممسوح** في سير عمل واحد وسهل.

في هذا الدرس سنستعرض كل ما تحتاج معرفته — من ترخيص المكتبة إلى طباعة النتيجة النهائية. بنهاية الدرس ستحصل على برنامج جاهز للتنفيذ يخرج النص العادي من أي تقرير، فاتورة أو كتاب إلكتروني ممسوح. لا خدمات خارجية، لا سحر — مجرد كود جافا نقي تتحكم فيه.

## ما الذي ستحتاجه

- **Java Development Kit (JDK) 8+** — أي نسخة حديثة تعمل.
- **Aspose.OCR for Java** JAR (حمّله من موقع Aspose).  
- ملف **ترخيص Aspose.OCR صالح** (`Aspose.OCR.lic`). النسخة التجريبية مجانية، لكن الترخيص يفتح الدقة الكاملة.
- **ملف PDF ممسوح** (مثال: `scanned-report.pdf`).  
- بيئة تطوير متكاملة أو محرر نصوص بسيط بالإضافة إلى الطرفية.

هذا كل شيء. لا Maven، لا Gradle، ولا تبعيات إضافية — فقط ملف JAR الخاص بـ Aspose.OCR على مسار الـ classpath.

![مثال على كيفية استخدام OCR](image-placeholder.png "مثال على كيفية استخدام OCR")

## الخطوة 1 – تحميل ترخيص Aspose.OCR (لماذا هو مهم)

قبل أن يعمل المحرك بأقصى سرعته يجب إخبارها بمكان وجود الترخيص. تخطي هذه الخطوة يجعل المكتبة تعمل في وضع التقييم، مما يضيف علامات مائية إلى الناتج وقد يحد من الدقة.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**لماذا يعمل هذا:** تقوم فئة `License` بقراءة ملف `.lic` وتسجيله عالميًا. بمجرد ضبطه، كل كائن `OcrEngine` تنشئه سيستخدم الميزات المرخصة تلقائيًا.

## الخطوة 2 – إنشاء محرك OCR (المحرك وراء السحر)

كائن `OcrEngine` هو العامل الأساسي الذي يمسح الصور ويُخرج النص. فكر فيه كالعقل الذي يفسر أنماط البكسل.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**نصيحة احترافية:** يمكنك تعديل اللغة، عتبات الثقة، أو حتى تمكين تسريع GPU عبر خصائص المحرك. بالنسبة لمعظم ملفات PDF الإنجليزية الإعدادات الافتراضية كافية.

## الخطوة 3 – إعداد الإدخال: إضافة ملف PDF (تحويل PDF إلى صور خلفيًا)

يتعامل Aspose.OCR مع كل صفحة من PDF كصورة. عندما تستدعي `addPdf`، تقوم المكتبة بتحويل كل صفحة إلى صورة بصمت، وهذا بالضبط ما تحتاجه **لتحويل PDF إلى صور** قبل التعرف.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**ما يحدث:**  
- يتم فتح ملف PDF.  
- تُرسم كل صفحة بدقة 300 dpi (الإعداد الافتراضي) للحفاظ على تفاصيل الحروف.  
- تُخزن كائنات الـ bitmap المُرَسَمة في مجموعة `OcrInput`.

إذا احتجت الصور الخام (للتصحيح أو المعالجة المسبقة المخصصة)، استدعِ `ocrInput.getPages()` بعد هذه الخطوة.

## الخطوة 4 – تشغيل عملية OCR (أداء OCR على PDF)

الآن يبدأ العمل الشاق. تقوم طريقة `recognize` بالتكرار على كل صورة، تشغيل خوارزمية التعرف، وتجميع النتائج في كائن `OcrResult`.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**لماذا يهمك ذلك:** يحتوي `OcrResult` ليس فقط على النص العادي بل أيضًا على درجات الثقة، الصناديق المحيطة، وإشارة إلى الصورة الأصلية. في معظم الحالات ستحتاج فقط إلى `getText()`.

## الخطوة 5 – استرجاع وعرض النص المستخرج

أخيرًا، استخرج سلسلة النص العادي من النتيجة واطبعها. يمكنك أيضًا كتابة النص إلى ملف، إرساله إلى فهرس بحث، أو تمريره إلى خط أنابيب NLP لاحق.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### النتيجة المتوقعة

إذا كان `scanned-report.pdf` يحتوي على فقرة بسيطة، سترى شيء مثل:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

التنسيق الدقيق يعكس التخطيط الأصلي، مع الحفاظ على فواصل الأسطر قدر الإمكان.

## معالجة الحالات الشائعة

### 1. ملفات PDF متعددة اللغات

إذا كان المستند يحتوي على نص فرنسي أو إسباني، اضبط اللغة قبل استدعاء `recognize`:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

يمكنك تمرير مصفوفة من اللغات لتمكين المحرك من الكشف التلقائي.

### 2. مسحات منخفضة الدقة

عند التعامل مع مسحات بدقة 150 dpi، زد DPI الداخلي للرندر:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

زيادة DPI تحسن وضوح الحروف لكنها تستهلك المزيد من الذاكرة.

### 3. ملفات PDF الكبيرة (إدارة الذاكرة)

لملفات PDF التي تحتوي على عشرات الصفحات، عالجها على دفعات:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

هذه الطريقة تمنع تضخم ذاكرة JVM.

## مثال كامل وجاهز للتنفيذ

فيما يلي البرنامج الكامل — بما في ذلك الاستيرادات ومعالجة الترخيص — لتتمكن من نسخه ولصقه وتشغيله فورًا.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

شغّله باستخدام:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

سترى النص المستخرج يُطبع على وحدة التحكم.

## ملخص – ما تم تغطيته

- **كيفية استخدام OCR** في جافا مع Aspose.OCR.  
- سير العمل **لاستخراج النص من ملفات PDF**.  
- داخليًا، تقوم المكتبة **بتحويل PDF إلى صور** قبل التعرف على الأحرف.  
- نصائح **لأداء OCR على PDF** مع لغات متعددة، مسحات منخفضة الدقة، ومستندات كبيرة.  
- عينة كود كاملة قابلة للتنفيذ يمكنك إدماجها في أي مشروع جافا.

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن أصبحت قادرًا على **التعرف على PDF الممسوح**، فكر في الأفكار التالية:

- **إنشاء PDF قابل للبحث** — أضف نص OCR مرة أخرى إلى PDF الأصلي لإنشاء مستند قابل للبحث.  
- **خدمة معالجة دفعات** — غلف الكود في خدمة مايكرو Spring Boot تستقبل ملفات PDF عبر REST.  
- **التكامل مع Elasticsearch** — فهرس النص المستخرج للبحث النصي الكامل السريع عبر مستودع المستندات.  
- **معالجة الصور مسبقًا** — استخدم OpenCV لتصحيح الميل أو إزالة الضوضاء من الصفحات قبل OCR للحصول على دقة أعلى.

كل من هذه المواضيع يبني على المفاهيم الأساسية التي استعرضناها، لذا لا تتردد في التجربة ودع محرك OCR يقوم بالعمل الشاق.

---

*برمجة سعيدة! إذا واجهت أي مشاكل — مثل أخطاء الترخيص أو نتائج `null` غير متوقعة — اترك تعليقًا أدناه. أنا دائمًا مستعد لجلسة تصحيح.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}