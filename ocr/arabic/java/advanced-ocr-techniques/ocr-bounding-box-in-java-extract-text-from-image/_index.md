---
category: general
date: 2026-06-16
description: يظهر دليل صندوق حدود OCR في جافا كيفية استخراج النص من الصورة، قراءة
  النص من الصورة، والحصول على درجة ثقة OCR لملفات JPG.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: ar
og_description: مربع حدود OCR في جافا يتيح لك التعرف على النص من ملفات JPG، استخراج
  النص من الصورة، وعرض درجات ثقة OCR — كل ذلك في مثال شفرة بسيط.
og_title: مربع حدود OCR في جافا – استخراج النص من الصورة
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: مربع حدود OCR في جافا – استخراج النص من الصورة
url: /ar/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مربع حدود OCR في Java – استخراج النص من الصورة

هل تساءلت يومًا كيف تحصل على **ocr bounding box** لكل قطعة نص في صورة Java؟ في هذا الدرس سنظهر لك كيفية **extract text from image**، **read text from image**، وحتى رؤية **ocr confidence score** أثناء **recognize text from jpg**. الجواب المختصر؟ بضع أسطر من الشيفرة باستخدام مكتبة OCR حديثة، بالإضافة إلى شرح بسيط لماذا كل استدعاء مهم.

في الأسفل ستجد مثالًا كاملًا جاهزًا للتنفيذ، تفصيلًا خطوة بخطوة، وبعض النصائح العملية التي يمكنك نسخها مباشرةً إلى مشروعك. في النهاية، ستتمكن من إنتاج شيء مثل:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## ما ستحتاجه

- **Java 11** أو أحدث (الصياغة أدناه تستخدم كلمة المفتاح `var` للاختصار، لكن يمكنك إزالتها لإصدارات JDK القديمة).  
- مكتبة OCR توفر واجهة برمجة تطبيقات Java – في هذا الدليل سنستخدم **[Tesseract4J](https://github.com/nguyenq/tess4j)**، غلاف خفيف حول محرك Tesseract الشهير.  
- صورة JPEG (`.jpg`) تحتوي على نص واضح ومطبوع.  
- بيئتك المفضلة IDE (IntelliJ IDEA، Eclipse، VS Code…) – أيًا كان.

إذا كنت تفتقد المكتبة، فقط أضف تبعية Maven التالية:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

الآن لنغوص في التفاصيل.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## مربع حدود OCR: إعداد المحرك

أول شيء عليك فعله هو إنشاء مثال لمحرك OCR. فكر فيه كتشغيل الماسح الضوئي الذي سيقرأ البكسلات لاحقًا.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**لماذا هذا مهم:**  
بدون تعيين `datapath`، لن يعرف Tesseract أين توجد حزم اللغات، وستحصل على خطأ غامض “Failed loading language”. استدعاء `setLanguage` اختياري إذا كنت تحتاج فقط إلى حزمة اللغة الإنجليزية الافتراضية، لكن الصراحة تجعل الشيفرة أوضح للقراء المستقبليين.

## تحميل الصورة التي تريد معالجتها

بعد ذلك، قدم للمحرك صورة JPEG التي ترغب في تحليلها. المكتبة تقبل `File` أو `BufferedImage`؛ سنستخدم `File` للبساطة.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**نصيحة احترافية:**  
إذا كانت صورتك موجودة في الموارد (مثلاً داخل JAR)، استخدم `getResourceAsStream` ولفها بـ `ImageIO.read`. بهذه الطريقة يعمل الدرس محليًا وفي تطبيق مُعبأ.

## تنفيذ التعرف على OCR

الآن نطلب من المحرك فعليًا قراءة الصورة. النتيجة هي سلسلة نصية عادية، لكننا نريد أيضًا **ocr confidence score** و **ocr bounding box** لكل سطر.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**لماذا نستخدم `getWords` بدلاً من `doOCR` العادي:**  
`doOCR` يمنحك السلسلة الخام لكنه يتجاهل المعلومات المكانية. باستدعاء `getWords` مع `RIL_WORD` (أو `RIL_TEXTLINE` إذا كنت تفضّل مربعات على مستوى السطر)، نسترجع قائمة من كائنات `Word` التي تحمل كل منها النص، الثقة، والمستطيل الحدودي. هذا هو جوهر ميزة **ocr bounding box**.

## فهم الناتج

تشغيل المقتطف أعلاه على صورة JPEG نظيفة ينتج مخرجات مشابهة لـ:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **النص** – الأحرف التي تم التعرف عليها.  
- **الثقة** – قيمة عائمة بين 0 و 1؛ كلما ارتفعت يعني أن المحرك أكثر يقينًا.  
- **المستطيل** – المستطيل الذي يحيط بالكلمة بإحداثيات البكسل (x, y, العرض, الارتفاع).

يمكنك الآن **read text from image** ومعرفة بالضبط أين يقع كل مقطع على اللوحة—مثالي للتظليل، القص، أو إمداده إلى خطوط معالجة اللغة الطبيعية اللاحقة.

## الحالات الحدية والمشكلات الشائعة

| الحالة | ما الذي يجب مراقبته | الإصلاح / الحل |
|-----------|-------------------|-------------------|
| الصورة غير واضحة أو ذات تباين منخفض | تنخفض درجات الثقة بشكل كبير (غالبًا أقل من 0.6). | معالجة مسبقة باستخدام OpenCV: زيادة التباين، تطبيق العتبة. |
| JPEG يحتوي على نص مائل | مربعات الحدود تظهر مائلة أو مفقودة. | استخدم `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` للسماح لـ Tesseract باكتشاف الاتجاه تلقائيًا. |
| الصور الكبيرة تسبب OutOfMemoryError | تملأ ذاكرة Java heap عند تحميل صور كبيرة. | قلل حجم الصورة قبل OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| تحتاج إلى مربعات على مستوى السطر بدلاً من مستوى الكلمة | `RIL_WORD` يعيد مربعات لكل كلمة. | بدّل إلى `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| الأحرف غير الإنجليزية تظهر كـ � | بيانات اللغة غير محملة. | حمّل ملف `.traineddata` المناسب ووجه `setDatapath` إلى مجلده. |

معالجة هذه المشكلات مبكرًا توفر لك ساعات من التصحيح لاحقًا.

## مثال كامل يعمل (جميع الخطوات في ملف واحد)

فيما يلي فئة Java مستقلة يمكنك نسخها ولصقها في مجلد `src/main/java` وتشغيلها باستخدام `mvn exec:java`. تجمع جميع ما ناقشنا.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من صورة Java باستخدام Aspose.OCR وضع اكتشاف المناطق](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [استخراج نص الصور – أساسيات OCR مع Aspose.OCR لـ Java](/ocr/english/java/ocr-basics/)
- [كيفية OCR نص الصورة باستخدام اللغة مع Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}